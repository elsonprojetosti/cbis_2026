# Fluxos de Navegação — Sistema Águia

## Fluxo de Acesso e Autenticação

```
Usuário acessa URL do Sistema Águia
          ↓
Tela de Login
  ├── Inserir CPF + Senha
  └── Clique em "Entrar"
          ↓
Verificação de 2FA (TOTP)
  ├── Inserir código do aplicativo autenticador
  └── Confirmação
          ↓
Verificação de Aceite LGPD
  ├── Primeira vez: Tela de aceite do Termo LGPD (obrigatório)
  └── Já aceitou: segue direto
          ↓
Dashboard Principal
  └── Módulos liberados conforme perfil do usuário
```

---

## Hierarquia de Acesso

O acesso é controlado por dois níveis:

### Nível 1 — Módulos Acessíveis
Cada usuário vê apenas os módulos aos quais foi liberado:
- `mod_gestante` → Módulo Gestante / NPN
- `mod_saude_mulher` → OMMA
- `mod_monitora_aps` → Monitor APS
- `mod_vigi_manaus` → Vigi Manaus + Vigilância de Óbitos
- `admin` → Painel Administrativo (gestão de usuários e acessos)

### Nível 2 — Escopo Geográfico
Dentro de cada módulo, os dados são filtrados pelo vínculo do usuário:
- Profissional de CNES → vê apenas dados da sua unidade
- Gestor Distrital → vê dados de todas as unidades do distrito
- Gestor Municipal / Epidemiologista → vê dados de todo o município

---

## Fluxo do Módulo Gestante (Exemplo)

```
Dashboard Principal → Módulo Gestante
          ↓
Painel Gerencial (visão do CNES/Distrito)
  ├── Gráfico: Distribuição por faixa de NPN
  ├── Tabela: Top unidades por cobertura
  └── Alertas: Gestantes com NPN crítico
          ↓
Clique em gestante ou CNES específico
          ↓
Painel Individual da Gestante
  ├── Dados cadastrais
  ├── Score NPN atual (colorimétrico)
  ├── IATs por trimestre (T1, T2, T3, T0)
  ├── Cuidados realizados vs. esperados
  └── Próximas ações recomendadas
          ↓
Exportar lista nominal (PDF/Excel)
```

---

## Navegação entre Módulos

O menu lateral (sidebar) permanece visível em todas as telas e permite navegação direta entre módulos sem retornar ao Dashboard:

```
[Sidebar]
  ├── 🏠 Dashboard
  ├── 🤰 Gestante / NPN
  ├── 🔬 OMMA
  ├── 📊 Monitor APS
  ├── ⚰️ Vigilância de Óbitos
  ├── 🦠 Vigi Manaus
  └── ⚙️ Administração (admin only)
```

---

## Elementos de Interface Padronizados

| Elemento | Cor | Significado |
|---------|-----|-------------|
| Indicador Vermelho 🔴 | #EF4444 | Crítico — ação urgente necessária |
| Indicador Amarelo 🟡 | #F59E0B | Atenção — acompanhamento reforçado |
| Indicador Verde 🟢 | #10B981 | Adequado — monitoramento de rotina |
| Badge de alerta 🔔 | Vermelho | Pendências que requerem ação |
| Tabela DataTables | — | Busca, paginação, exportação integrados |
| Gráfico Chart.js | — | Interativo, tooltip ao hover |
