# Sistema Águia — Repositório de Documentação Científica (CBIS 2026)

[![CBIS 2026](https://img.shields.io/badge/CBIS-2026-blue)](https://cbis.ufma.br)
[![SEMSA Manaus](https://img.shields.io/badge/SEMSA-Manaus-green)](https://semsa.manaus.am.gov.br)
[![Laravel](https://img.shields.io/badge/Laravel-11.x-red)](https://laravel.com)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15+-blue)](https://postgresql.org)

> **Repositório de documentação técnico-científica** do Sistema Águia para subsidiar avaliadores dos trabalhos submetidos ao XXI Congresso Brasileiro de Informática em Saúde (CBIS 2026).
>
> Este repositório **não contém código-fonte**. É um acervo estruturado de documentação de interface, arquitetura e resultados, organizado para a comunidade científica e desenvolvedores interessados na solução.

---

## O que é o Sistema Águia?

O **Sistema Águia** é uma plataforma web de **integração e inteligência em saúde digital** desenvolvida pela Gerência de Epidemiologia e Informação (GEIND) da Diretoria de Inteligência de Dados (DID) da Secretaria Municipal de Saúde de Manaus (SEMSA), para apoio à gestão da Atenção Primária à Saúde (APS) de Manaus.

O sistema integra dados de múltiplos sistemas oficiais do SUS — e-SUS PEC, SIM, SINASC, SINAN e SISCAN — transformando dados brutos e fragmentados em informação qualificada para profissionais de saúde e gestores.

**Contexto**: Manaus, maior município da Amazônia, com mais de 2,2 milhões de habitantes e extensa rede de APS.

---

## Módulos do Sistema

| Módulo | Descrição | Fonte de Dados | Documentação |
|--------|-----------|---------------|--------------|
| **Gestante / NPN** | Monitoramento do pré-natal com Score NPN (0-9) | e-SUS PEC, SINASC, SINAN | [Ver módulo](frontend/modulos/gestante_npn.md) |
| **OMMA** | Observatório da Mulher Manauara — rastreio de câncer do colo | SISCAN, SIM | [Ver módulo](frontend/modulos/omma.md) |
| **Monitor APS** | Indicadores de performance da Atenção Primária | e-SUS PEC, Cofinanciamento | [Ver módulo](frontend/modulos/monitor_aps.md) |
| **Vigilância de Óbitos** | Integração SIM × e-SUS para higienização cadastral | SIM, e-SUS PEC | [Ver módulo](frontend/modulos/vigilancia_obitos.md) |
| **Vigi Manaus** | Vigilância epidemiológica (TB, agravos) | SINAN, ITB | [Ver módulo](frontend/modulos/vigi_manaus.md) |

---

## Resultados Operacionais

| Indicador | Resultado |
|-----------|-----------|
| Registros gestacionais processados/dia | **+200.000** |
| Atualização | **D-1** (incremental diária) |
| Redução de óbitos com cadastro ativo na APS | **-27%** (6.117 → 4.485) |
| Redução de atendimentos pós-óbito | **-90%** (jul-set/2025) |
| Módulos operacionais em produção | **5 módulos** |
| Conformidade LGPD | **100%** dos acessos |

---

## Telas e Interface Visual

Para visualizar com detalhes as capturas de tela dos módulos, painéis e fluxos do sistema (como Dashboard, Busca Ativa NPN, Módulo OMMA, etc), acesse a documentação do frontend:

👉 **[Ver Galeria de Telas e Interface do Sistema Águia](frontend/README.md)**

---

## Estrutura deste Repositório

```
cbis_2026/
├── README.md                    # Este arquivo
├── frontend/                    # Interface web do Águia
│   ├── README.md                # Visão geral da interface
│   ├── modulos/                 # Documentação por módulo
│   └── fluxos/                  # Fluxos de navegação e UX
└── backend/                     # Arquitetura do sistema (visão geral)
    ├── README.md
    ├── arquitetura.md
    └── seguranca.md
```

---

## Stack Tecnológica

| Camada | Tecnologia |
|--------|-----------|
| Backend | Laravel 11 (PHP) + Eloquent ORM |
| Banco de Dados | PostgreSQL 15+ (multi-schema) |
| Frontend | Blade + Tailwind CSS + Vite |
| Gráficos | Chart.js, DataTables |
| Autenticação | Jetstream + Fortify + 2FA (TOTP) |
| Autorização | Controle modular por CPF e flags |

---

## Conformidade Ética e Legal

O Sistema Águia opera exclusivamente sobre **dados secundários anonimizados** de sistemas oficiais do SUS, no âmbito das atribuições institucionais da SEMSA Manaus. O acesso é condicionado ao aceite do Termo de Conformidade com a **LGPD (Lei nº 13.709/2018)**, implementado via middleware no sistema.

---

## Informação Institucional

**Instituição**: Secretaria Municipal de Saúde de Manaus (SEMSA)  
**Unidade**: Diretoria de Inteligência de Dados (DID) — Gerência de Epidemiologia e Informação (GEIND)  
**Cidade**: Manaus, Amazonas, Brasil  
**Evento**: XXI Congresso Brasileiro de Informática em Saúde — CBIS 2026  

---

*Documentação para fins científicos e acadêmicos — CBIS 2026*
