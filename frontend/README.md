# Frontend — Interface Web do Sistema Águia

## Visão Geral

A interface web do Sistema Águia foi desenvolvida para ser o ponto de acesso de **profissionais de saúde e gestores** da rede municipal de Manaus à informação integrada do SUS. O design prioriza clareza, responsividade e tomada de decisão ágil.

---

## Stack Frontend

| Tecnologia | Uso |
|-----------|-----|
| **Blade (Laravel)** | Motor de templates SSR (*Server-Side Rendering*) |
| **Tailwind CSS** | Estilização utilitária e responsividade |
| **Vite** | Compilação e *hot reload* de assets |
| **Chart.js** | Gráficos interativos (barras, radar, linha, pizza) |
| **DataTables** | Listagens nominais com paginação, busca e exportação |
| **Alpine.js** | Micro-interatividade sem overhead de framework |

---

## Princípios de UX Adotados

1. **Alertas colorimétricos**: vermelho para situações críticas (ex: NPN < 5), amarelo para atenção, verde para adequado — comunicação visual imediata sem necessidade de leitura numérica
2. **Listagens nominais**: dados individualizados por gestante, mulher ou paciente, com filtros por unidade, distrito e período
3. **Dashboards gerenciais**: painéis agregados por CNES, Distrito Sanitário e município para gestores
4. **Responsividade**: interface funcional em desktop e tablet (uso em reuniões de equipe)
5. **Acesso modular**: cada usuário vê apenas os módulos aos quais tem permissão, reduzindo sobrecarga cognitiva

---

## Mapa de Módulos

```
Sistema Águia
├── Módulo Gestante / NPN
│   ├── Painel Individual (por gestante)
│   ├── Painel Gerencial (por CNES/Distrito)
│   ├── Monitoramento de Sífilis Gestacional
│   └── Rastreio de Inconsistências Cadastrais
├── Módulo OMMA
│   ├── Painel de Exames Citopatológicos
│   ├── Painel de Óbitos (SISCAN × SIM)
│   └── Módulo Ampulheta (tempo coleta-laudo)
├── Módulo Monitor APS
│   ├── Indicadores de Performance por CNES
│   ├── Histórico de Escores
│   └── Indicadores de Cofinanciamento (PREVINE Brasil)
├── Módulo Vigilância de Óbitos
│   ├── Lista Nominal (SIM × e-SUS)
│   └── Painel de Inconsistências por Distrito
└── Módulo Vigi Manaus
    ├── Painel de Tuberculose
    └── Estatísticas SINAN / CID-CIAP
```

---

## Documentação por Módulo

- [Gestante / NPN](modulos/gestante_npn.md) — Monitoramento pré-natal com Score NPN 0-9
- [OMMA](modulos/omma.md) — Observatório da Mulher Manauara
- [Monitor APS](modulos/monitor_aps.md) — Indicadores de Atenção Primária
- [Vigilância de Óbitos](modulos/vigilancia_obitos.md) — Integração SIM × e-SUS PEC
- [Vigi Manaus](modulos/vigi_manaus.md) — Vigilância epidemiológica

---

## Fluxos de Navegação

- [Fluxo geral de navegação](fluxos/navegacao.md) — Acesso, autenticação, navegação entre módulos

---

## Segurança na Interface

O acesso é protegido por três camadas visíveis ao usuário:
1. **Login com 2FA** (código TOTP via aplicativo autenticador)
2. **Aceite obrigatório da LGPD** (antes do primeiro acesso aos dados)
3. **Controle modular** (usuário vê apenas módulos autorizados)

---

## Telas do Sistema Águia

### 1. Módulos Águia
![Módulos Águia](imgs/1.Módulos-águia.png)

### 2. Fluxo de Entrada - Login
![Fluxo de Entrada - Login](imgs/2.Fluxo%20de%20entrada-login.png)

### 3. Tela Principal
![Tela Principal](imgs/3.Tela_Principal.png)

### 4. Consulta de Gestantes
![Consulta de Gestantes](imgs/4.Consulta_Gestantes.png)

### 5. Acompanhamento de Gestantes (Sífilis)
![Acompanhamento Sífilis](imgs/5.Acompanhamento_Gestantes_Sifilis.png)

### 6. Aplicação - Sífilis na Gestante
![Aplicação Sífilis](imgs/6.Aplicacao_Sifilis_Gestante.png)

### 7. Gestações em Aberto
![Gestações em Aberto](imgs/7.Gestacoes_Aberto.png)

### 8. Busca Ativa NPN
![Busca Ativa NPN](imgs/8.Busca_ativa_NPN.png)

### 9. OMMA (Observatório da Mulher Manauara)
![OMMA](imgs/9.OMMA.png)

### 10. OMMA - Exames Citopatológicos por Faixa Etária
![OMMA Citopatológicos](imgs/10.OMMA_Citopatologicos_Faixa.png)

### 11. OMMA - Ampulheta
![OMMA Ampulheta](imgs/11.OMMA_Ampulheta.png)

### 12. Raio-X ITB
![Raio-X ITB](imgs/12.Raio_X_ITB.png)

### 13. Óbito - Prontuários em Aberto
![Óbito Prontuários em Aberto](imgs/13.Obito_Prontuarios_Aberto.png)

### 14. Óbito - Atendimento Pós-Óbito
![Óbito Atendimento Pós-Óbito](imgs/14.Obito_Atendimento_Pos_Obito.png)

### 15. Registros de Notificação SIM (CID)
![Registros Notificação SIM CID](imgs/15.Registros_Notificacao_SIM_CID.png)

### 16. Registros de Notificação SIM (Grupo)
![Registros Notificação SIM Grupo](imgs/16.Registros_Notificacao_SIM_Grupo.png)
