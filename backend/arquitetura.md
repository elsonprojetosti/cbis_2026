# Arquitetura do Sistema Águia

## Padrão Arquitetural

O Sistema Águia implementa o padrão **MVC (Model-View-Controller)** do framework Laravel, com extensões para:
- Multi-conexão de banco de dados (7 conexões PostgreSQL ativas)
- Separação OLTP/OLAP via schemas isolados
- Feature Store analítica (tabela `glenda.tb_npn`)
- Pipeline ETL/ELT nativo em PostgreSQL (CTEs modulares)

---

## Diagrama de Componentes

```
Browser (Profissional/Gestor)
          ↓
Router (routes/web.php)
          ↓
Middleware Pipeline
  ├── auth:sanctum (autenticação)
  ├── ExigeLgpd (aceite LGPD)
  └── RequireModule (controle de acesso por módulo)
          ↓
Controllers
  ├── GestanteController → Módulo NPN
  ├── SaudeMulherController → OMMA
  ├── MonitorAPSController → Monitor APS
  ├── ObitoController → Vigilância de Óbitos
  └── ItbController → Vigi Manaus
          ↓
Models (Eloquent ORM — cada Model declara sua conexão)
          ↓
PostgreSQL (múltiplos schemas)
  ├── aguia (analítico — dados transformados)
  ├── portaldid (usuários e autenticação)
  ├── e-SUS PEC public (prontuário eletrônico)
  ├── SIM / SINASC (mortalidade / nascimentos)
  ├── SISCAN (câncer)
  ├── cofinanciamento (indicadores APS)
  └── itb (tuberculose)
```

---

## Múltiplas Conexões PostgreSQL

| Conexão | Schema/Banco | Origem dos Dados | Tipo |
|---------|-------------|-----------------|------|
| `pgsql_aguia` | `aguia` | Dados analíticos Águia | **OLAP** (escrita analítica) |
| `pgsql_did` | `portaldid` | Usuários, autenticação | OLTP |
| `pgsql_esus` | `public` | e-SUS PEC — prontuário | OLTP (somente leitura) |
| `pgsql_ada` | `novo_ada` | Sistema ADA | OLTP |
| `pgsql_cofap` | `cofinanciamento` | Indicadores PREVINE Brasil | OLTP |
| `pgsql_serverdados_itb` | `itb` | Tuberculose / SINAN | OLTP |

---

## Separação OLTP/OLAP

**Abordagem**: A separação entre dados transacionais e analíticos é implementada **exclusivamente via múltiplas conexões PostgreSQL e schemas isolados**, sem ferramentas de data warehouse externas, sem Big Data e sem licenças proprietárias.

- **Bases OLTP** (e-SUS PEC, SIM, SINASC): lidas como *read replicas* lógicas — queries de leitura apenas, sem escrita nos bancos de produção
- **Schema `aguia`** (OLAP): recebe os dados transformados, enriquecidos e indexados via pipelines SQL nativos

**Vantagem**: Consultas analíticas pesadas (ex: processamento de 200k gestações) não impactam os bancos transacionais em produção.

---

## Feature Store — `glenda.tb_npn`

A **Feature Store** é o repositório central de dados analíticos do Módulo Gestante:

| Característica | Detalhe |
|---------------|---------|
| Tabela | `glenda.tb_npn` |
| Granularidade | 1 linha por gestação |
| Variáveis | 140+ por gestação |
| Domínios | 7 (identificação, cronológico, histórico obstétrico, transacionais por trimestre, totalizadores, algoritmo, features preditivas) |
| Atualização | UPSERT atômico diário (`INSERT ... ON CONFLICT DO UPDATE`) |
| Janela temporal | 336 dias (gestação + puerpério + margem) |
| Volume | 200.000+ gestações |

### Pipeline ETL/ELT Nativo

O processamento é feito via **CTEs (Common Table Expressions) modulares** em PostgreSQL:
- Cada CTE isola um domínio de dados (vacinas, exames, consultas, sinais vitais)
- CTEs são compostas via JOIN sobre a chave gestacional
- Resultado é consolidado em UPSERT atômico na Feature Store

---

## Padrões de Projeto

| Padrão | Implementação |
|--------|-------------|
| MVC | Controllers / Models / Blade Views |
| Active Record | Eloquent ORM com `$connection` por Model |
| Multi-Connection ORM | `pgsql_aguia`, `pgsql_did`, `pgsql_esus`, etc. |
| Feature Store / Staging | `glenda.tb_npn` como repositório analítico |
| ETL/ELT Nativo | Pipeline SQL com CTEs modulares |
| UPSERT Atômico | `ON CONFLICT DO UPDATE` (zero downtime) |
| Middleware Chain | Auth → LGPD → Módulo |
| OLTP/OLAP Separation | Leitura de fontes vs. escrita analítica |

---

## Inovação Arquitetural

**OLTP/OLAP sem infraestrutura adicional**: A separação entre camadas transacionais e analíticas foi implementada exclusivamente via múltiplas conexões PostgreSQL com schemas isolados, sem necessidade de:
- Data warehouses externos (Redshift, BigQuery, Snowflake)
- Ferramentas ETL proprietárias (Talend, Informatica)
- Infraestrutura de Big Data (Hadoop, Spark)
- Licenças de software comercial

Isso demonstra que **plataformas de inteligência em saúde pública são viáveis** dentro dos recursos computacionais de uma secretaria municipal de saúde, com stack 100% open-source.
