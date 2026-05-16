# Módulo Gestante / NPN — Monitoramento do Pré-Natal

## Propósito

O Módulo Gestante é o componente de maior complexidade analítica do Sistema Águia. Seu objetivo é monitorar a **qualidade e adequação do pré-natal** para todas as gestantes cadastradas na rede de Atenção Primária à Saúde de Manaus, por meio do indicador **NPN — Nível de Pré-Natal**.

---

## O que é o NPN?

O **NPN (Nível de Pré-Natal)** é um algoritmo de *Fenotipagem Computável* que supera os indicadores tradicionais de volume (ex: "proporção com ≥7 consultas") ao avaliar simultaneamente a **quantidade** e a **oportunidade temporal** do cuidado prestado.

### Score NPN (0 a 9)

| Faixa | Interpretação | Ação |
|-------|-------------|------|
| 0–3 | Pré-natal inadequado | Alerta vermelho — busca ativa urgente |
| 4–5 | Pré-natal insuficiente | Alerta amarelo — acompanhamento reforçado |
| 6–7 | Pré-natal adequado | Acompanhamento regular |
| 8–9 | Pré-natal ótimo | Monitoramento de rotina |

### Fórmula do Score NPN

```
NPN = FLOOR( Σ(IAT_k × teto_k) / Base_Ideal × 9 )
```

Onde:
- **IAT_k** = min(pontos_obtidos / teto_esperado, 1,0) para cada trimestre *k*
- **Efeito de Teto (Capping)**: excessos em um trimestre **não compensam** déficits em outro
- **Base_Ideal expandida** para gestantes de Alto Risco (idade <14 ou ≥35 anos, comorbidades)

---

## Cuidados Avaliados

O NPN avalia **23 cuidados essenciais** em **67 pontos de observação**, distribuídos em 4 janelas temporais:

| Trimestre | Período | Cuidados incluídos |
|-----------|---------|-------------------|
| **T1** | ≤ 13 semanas | Consultas, exames iniciais, tipagem sanguínea, sorologias |
| **T2** | 14–27 semanas | Consultas, exames de seguimento, ultrassonografia |
| **T3** | 28+ semanas | Consultas finais, vacinas, exames de terceiro trimestre |
| **T0** | Puerpério (até 42 dias) | Consulta puerperal, revisão pós-parto |

---

## Interface do Módulo

### Painel Individual

Exibe para cada gestante:
- Score NPN atual (colorimétrico: vermelho/amarelo/verde)
- Progresso por trimestre (IATs individuais)
- Cuidados realizados vs. esperados
- Data da última consulta e próxima consulta prevista
- Alertas nominais para cuidados em atraso

### Painel Gerencial

Visão agregada por CNES/Distrito Sanitário:
- Distribuição de gestantes por faixa de NPN
- Percentual de gestantes com NPN ≥ 6 (meta assistencial)
- Ranking de unidades de saúde por qualidade do pré-natal
- Tendência temporal do score médio

### Monitoramento de Sífilis Gestacional

Cruzamento automático SINAN × e-SUS PEC:
- Lista nominal de gestantes com notificação de sífilis
- Status de tratamento e parceiro tratado
- Alertas para casos em atraso de tratamento

### Rastreio de Inconsistências

Identifica gestações com:
- Data de última menstruação (DUM) inconsistente
- Gestação encerrada sem registro de parto/aborto
- Duplicidade de cadastros gestacionais

---

## Usuários-Alvo

| Perfil | Uso principal |
|--------|-------------|
| **Médicos/Enfermeiros da APS** | Monitoramento individual de gestantes da equipe |
| **Coordenadores de CNES** | Gestão de desempenho da unidade |
| **Gestores de Distrito Sanitário** | Comparação entre unidades e priorização |
| **Epidemiologistas** | Análise territorial e identificação de clusters |

---

## Volume e Performance

- **200.000+** gestações processadas diariamente
- Atualização em **D-1** (UPSERT atômico, zero *downtime*)
- Janela de processamento: 336 dias (gestação + puerpério + margem)
- Tempo de resposta: compatível com uso clínico em tempo real

---

## Fontes de Dados

| Sistema | Dados utilizados |
|---------|----------------|
| **e-SUS PEC** | Consultas, exames, sinais vitais, cadastros |
| **SINASC** | Dados de nascimento para encerramento de gestação |
| **SINAN** | Notificações de sífilis gestacional |

---

## Imagens de Referência

*(Diagramas e fluxos disponíveis na pasta `imgs/`)*

- Diagrama de módulos do Águia: `imgs/4.Módulos-águia.png`
- Arquitetura de recuperação de dados: `imgs/3-Arquitetura de recuperação de dados.png`
- Distribuição NPN por faixa: `imgs/grafico_distribuicao_npn.png`
- Médias IAT por trimestre: `imgs/grafico_media_iat.png`
