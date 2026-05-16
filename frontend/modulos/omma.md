# Módulo OMMA — Observatório da Mulher Manauara

## Propósito

O **OMMA (Observatório da Mulher Manauara)** monitora os exames citopatológicos (Papanicolau) realizados na rede municipal de Manaus, consolidando dados do SISCAN para rastreio do câncer do colo do útero e análise de desfechos.

---

## Funcionalidades Principais

### 1. Painel de Exames Citopatológicos

Exibe por mulher:
- Data de coleta do exame
- Resultado do laudo (Normal, ASCUS, LSIL, HSIL, Carcinoma)
- Data de liberação do laudo
- Desfecho e conduta recomendada
- Status: pendente, laudo disponível, colposcopia agendada

Filtros disponíveis:
- Por unidade de saúde (CNES)
- Por Distrito Sanitário
- Por período de coleta
- Por resultado do laudo
- Por faixa etária

### 2. Painel de Óbitos — SISCAN × SIM

Cruzamento automático entre mulheres com exames no SISCAN e registros de óbito no SIM:
- Identifica óbitos de mulheres que realizaram preventivo
- Análise de tempo entre último exame e óbito
- Classificação da causa do óbito (neoplasia do colo x outras causas)
- Suporte à auditoria e avaliação da qualidade do rastreio

### 3. Módulo Ampulheta — Tempo Coleta-Laudo

Monitora o **tempo entre a coleta do exame e a liberação do laudo** para identificar gargalos no fluxo laboratorial:

| Indicador | Descrição |
|-----------|-----------|
| Tempo médio por laboratório | Média de dias entre coleta e laudo |
| Tempo máximo | Casos com maior demora |
| Percentual dentro do prazo | Exames laudados em até X dias (meta configurável) |
| Tendência temporal | Gráfico de linha com evolução mensal |

Alertas automáticos para laudos em atraso (acima do prazo estabelecido pelo protocolo).

---

## Usuários-Alvo

| Perfil | Uso principal |
|--------|-------------|
| **Enfermeiros/Médicos da APS** | Acompanhamento de resultados de pacientes da unidade |
| **Coordenadores de CNES** | Monitoramento de cobertura de rastreio |
| **Gestores de Saúde da Mulher** | Análise de desfechos e qualidade do rastreio |
| **Epidemiologistas** | Análise territorial de câncer do colo do útero |

---

## Fonte de Dados

| Sistema | Dados utilizados |
|---------|----------------|
| **SISCAN** | Exames citopatológicos, laudos, resultados |
| **SIM** | Registros de óbito para cruzamento |
| **e-SUS PEC** | Cadastro e identificação da paciente |

---

## Impacto Esperado

- Aumento da taxa de rastreio por identificação de mulheres sem exame recente
- Redução do tempo entre coleta e laudo por identificação de gargalos laboratoriais
- Melhoria do seguimento de casos alterados
- Dados para auditoria clínica e avaliação de programa de rastreio municipal
