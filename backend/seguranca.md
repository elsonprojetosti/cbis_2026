# Segurança e Conformidade LGPD — Sistema Águia

## Modelo de Segurança

O Sistema Águia implementa segurança em **três camadas em cascata**, todas visíveis e transparentes ao usuário:

```
Camada 1: Autenticação
          ↓
Camada 2: Conformidade LGPD (aceite obrigatório)
          ↓
Camada 3: Autorização Modular (acesso por CPF e perfil)
```

---

## Camada 1 — Autenticação (Laravel Jetstream + Fortify)

| Componente | Implementação |
|-----------|-------------|
| Framework | Laravel Jetstream com Fortify |
| Autenticação primária | CPF + senha |
| 2FA obrigatório | TOTP (Time-based One-Time Password) via app autenticador |
| Gestão de sessão | Tokens Sanctum para requisições AJAX |
| Proteção contra brute-force | Rate limiting nativo do Fortify |

O **2FA via TOTP** é obrigatório para todos os usuários — não há acesso ao sistema sem o segundo fator configurado.

---

## Camada 2 — Conformidade LGPD (Middleware `ExigeLgpd`)

O middleware `ExigeLgpd` é executado após a autenticação bem-sucedida e **bloqueia qualquer acesso a dados** até o aceite explícito do Termo de Uso e Conformidade com a LGPD.

### Fluxo de Aceite

```
Usuário autenticado → Verifica ControlleAcesso::needsLgpd(cpf)
          ├── Aceite pendente → Redireciona para tela de aceite
          │     ├── Exibe Termo de Uso completo
          │     └── Usuário confirma → Registra aceite (data, IP, versão do termo)
          └── Aceite vigente → Prossegue para o sistema
```

### Conformidade com LGPD

| Princípio LGPD | Implementação |
|---------------|-------------|
| **Finalidade** | Dados usados exclusivamente para gestão assistencial e epidemiológica |
| **Adequação** | Apenas dados necessários para cada módulo são acessados |
| **Necessidade** | Filtragem geográfica limita escopo ao CNES/Distrito do usuário |
| **Livre Acesso** | Usuário pode consultar seu aceite e histórico |
| **Segurança** | 2FA, sessão segura, HTTPS obrigatório |
| **Transparência** | Termo de uso claro sobre quais dados são acessados e por quê |
| **Não Discriminação** | Acesso baseado em função, não em características pessoais |

---

## Camada 3 — Autorização Modular

### Tabela de Controle de Acesso

A tabela `tb_controle_acesso` (schema `aguia`) armazena permissões por CPF:

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `cpf` | VARCHAR | CPF do profissional |
| `mod_gestante` | BOOLEAN | Acesso ao Módulo Gestante / NPN |
| `mod_saude_mulher` | BOOLEAN | Acesso ao OMMA |
| `mod_monitora_aps` | BOOLEAN | Acesso ao Monitor APS |
| `mod_vigi_manaus` | BOOLEAN | Acesso ao Vigi Manaus + Vigilância de Óbitos |
| `admin` | BOOLEAN | Acesso ao painel administrativo |
| `distrito` | VARCHAR | Distrito Sanitário de vinculação |
| `cnes` | VARCHAR | CNES de vinculação |

### Princípio do Mínimo Privilégio

Cada usuário acessa **apenas os dados da sua unidade de saúde** (CNES) ou distrito, conforme seu vínculo. Gestores municipais e epidemiologistas têm escopo ampliado (todo o município).

---

## Dados: Origem e Classificação

| Base de Dados | Classificação | Uso no Águia |
|-------------|-------------|-------------|
| e-SUS PEC | Dado pessoal de saúde (sensível, LGPD art. 11) | Leitura apenas; dados identificados só para usuários autorizados |
| SIM | Dado pessoal (pós-óbito) | Leitura apenas; cruzamento para higienização cadastral |
| SINASC | Dado pessoal (nascimento) | Leitura apenas; vinculação com gestações |
| SINAN | Dado pessoal de saúde (sensível) | Leitura apenas; notificações |
| SISCAN | Dado pessoal de saúde (sensível) | Leitura apenas; exames preventivos |

**Todos os dados são secundários** — coletados originalmente por outros sistemas do SUS, utilizados no Águia para fins de gestão assistencial e epidemiológica no âmbito das atribuições institucionais da SEMSA Manaus.

---

## Declaração Ética

O Sistema Águia opera exclusivamente sobre dados secundários de sistemas oficiais do SUS, no âmbito das atribuições institucionais da SEMSA Manaus. O acesso é restrito a profissionais da rede municipal, condicionado ao aceite da LGPD, e realizado exclusivamente para fins de gestão assistencial e vigilância epidemiológica. Não houve coleta primária de dados de pacientes.

Conforme as diretrizes do CBIS 2026, o presente trabalho caracteriza-se como relato de experiência de desenvolvimento e implantação de sistema de informação em saúde no âmbito institucional público, não se enquadrando nos critérios que exigem submissão a Comitê de Ética em Pesquisa (CEP).
