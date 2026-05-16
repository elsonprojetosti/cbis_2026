# Módulo Vigilância de Óbitos — Integração SIM × e-SUS PEC

## Propósito

O **Módulo de Vigilância de Óbitos** integra o Sistema de Informação sobre Mortalidade (SIM) ao Prontuário Eletrônico do Cidadão (e-SUS PEC) para identificar **inconsistências cadastrais críticas**: pessoas com registro de óbito no SIM que ainda constam com cadastro ativo e prontuário aberto na APS.

---

## Problema que Resolve

Antes da implantação do módulo, cidadãos registrados como óbito no SIM continuavam com:
- Cadastro ativo na APS
- Prontuário aberto com consultas sendo registradas
- Resultados de exames sendo lançados
- Visitas domiciliares sendo computadas

Isso gerava distorções nos indicadores assistenciais, desperdício de recursos e impossibilidade de higienização das bases cadastrais.

---

## Resultados Mensurados

| Indicador | Antes | Depois | Variação |
|-----------|-------|--------|---------|
| Óbitos com cadastro ativo na APS | 6.117 (2024) | 4.485 (set/2025) | **-27%** |
| Atendimentos pós-óbito (jul-set/2025) | Linha de base | — | **-90%** |

---

## Funcionalidades

### 1. Lista Nominal de Inconsistências

Tabela com todos os cidadãos identificados na seguinte condição:
- Registro de óbito no SIM (com data e causa mortis)
- Cadastro ainda ativo no e-SUS PEC
- Últimas produções registradas após a data do óbito

Filtros:
- Por CNES de vinculação
- Por Distrito Sanitário
- Por período de óbito
- Por tipo de causa mortis (CID-10)

### 2. Painel de Inconsistências por Distrito

Visão gerencial:
- Total de inconsistências por Distrito Sanitário
- Percentual de resolução (higienizados vs. pendentes)
- Ranking de CNES com mais inconsistências pendentes
- Evolução temporal da redução de inconsistências

### 3. Busca Ativa

Geração de relatório para equipes de Saúde da Família realizarem busca ativa:
- Lista impressa por microárea ou ACS
- Formato para verificação em campo
- Registro de confirmação ou correção do óbito

---

## Fluxo Operacional

```
SIM (óbito registrado)
      ↓
Cruzamento automático diário (NIS, Nome, Data Nascimento)
      ↓
Identificação de cidadão ainda ativo no e-SUS PEC
      ↓
Alerta no painel do CNES responsável
      ↓
Equipe realiza busca ativa / confirma situação
      ↓
Cadastro inativado no e-SUS PEC
      ↓
Indicadores higienizados
```

---

## Usuários-Alvo

| Perfil | Uso principal |
|--------|-------------|
| **Agentes Comunitários de Saúde** | Busca ativa para confirmação de óbito |
| **Coordenadores de CNES** | Monitoramento e resolução de inconsistências da unidade |
| **Gestores Distritais** | Acompanhamento da higienização por distrito |
| **Epidemiologistas** | Análise da qualidade das bases cadastrais |

---

## Fontes de Dados

| Sistema | Dados utilizados |
|---------|----------------|
| **SIM** | Registros de óbito (data, causa, identificação) |
| **e-SUS PEC** | Cadastros ativos, últimas produções, vínculos CNES |

---

## Inovação

Esta é a primeira integração SIM × e-SUS PEC implementada em **escala municipal** (2,2 milhões de habitantes) com atualização diária e interface de gestão para equipes de APS. A abordagem sem infraestrutura adicional (exclusivamente via queries SQL cruzadas entre schemas PostgreSQL) demonstra a viabilidade da higienização de grandes bases de dados de saúde pública com recursos computacionais de uma secretaria municipal.
