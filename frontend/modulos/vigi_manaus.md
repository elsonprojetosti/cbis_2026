# Módulo Vigi Manaus — Vigilância Epidemiológica

## Propósito

O **Vigi Manaus** é o módulo de vigilância epidemiológica do Sistema Águia, com foco inicial em **tuberculose** e agravos de notificação do SINAN, conectando dados do servidor de vigilância epidemiológica de Manaus.

---

## Funcionalidades Principais

### 1. Painel de Tuberculose

Monitoramento dos casos de tuberculose na rede municipal:
- Lista nominal de casos notificados por CNES/Distrito
- Status de tratamento (em tratamento, cura, abandono, óbito)
- Controle de contatos examinados
- Exames de escarro e resultados de cultura
- Histórico de tratamentos anteriores (retratamento)

### 2. Análise de Notificações SINAN

Indicadores epidemiológicos de agravos de notificação:
- Cobertura de notificação por CNES
- Tendência de incidência por agravo
- Análise de sazonalidade (curva epidêmica)
- Comparação com séries históricas municipais

### 3. Estatísticas CID/CIAP

Análise das causas de atendimento na APS:
- Distribuição dos atendimentos por CID-10/CIAP-2
- Identificação dos agravos mais frequentes por território
- Evolução temporal da morbidade por CNES

---

## Usuários-Alvo

| Perfil | Uso principal |
|--------|-------------|
| **Equipes de Saúde da Família** | Monitoramento de casos de TB na microárea |
| **Enfermeiros de Vigilância** | Controle de tratamentos e contatos |
| **Coordenadores Distritais** | Gestão da vigilância epidemiológica local |
| **Epidemiologistas (GEIND/DID)** | Análise municipal e subsídio para tomada de decisão |

---

## Fontes de Dados

| Sistema | Dados utilizados |
|---------|----------------|
| **SINAN** | Notificações compulsórias (TB, outras doenças) |
| **ITB (servidor de dados)** | Base específica de vigilância de tuberculose |
| **e-SUS PEC** | Produção assistencial e cadastros |

---

## Próximas Expansões Previstas

- Ampliação para outros agravos prioritários (Dengue, HIV/AIDS, Hepatites)
- Integração com sistema de georreferenciamento para mapas epidemiológicos
- Alertas automáticos para surtos (sistema de detecção precoce)
