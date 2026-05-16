# Backend — Arquitetura do Sistema Águia

> **Nota**: Esta documentação apresenta a arquitetura em **nível conceitual**, para subsidiar avaliadores do CBIS 2026 e desenvolvedores interessados na abordagem técnica. Não contém código-fonte.

---

## Visão Geral

O Sistema Águia é uma plataforma web **multicamada** baseada no padrão MVC (*Model-View-Controller*), construída sobre Laravel 11 com PostgreSQL 15+ como banco de dados principal.

A decisão arquitetural mais relevante é o uso de **múltiplas conexões PostgreSQL**, cada uma mapeando um banco ou schema distinto de sistemas do SUS, permitindo integração de dados sem necessidade de ETL externo ou replicação de dados.

---

## Stack Tecnológica

| Camada | Tecnologia | Versão | Justificativa |
|--------|-----------|--------|--------------|
| Backend | Laravel (PHP) | 11.x | Framework MVC maduro, ecossistema robusto, suporte a múltiplas conexões de banco |
| Banco de dados | PostgreSQL | 15+ | Robustez, múltiplos schemas isolados, JSONB nativo, índices B-Tree avançados |
| ORM | Eloquent (Active Record) | nativo | Suporte a múltiplas conexões por Model |
| Autenticação | Jetstream + Fortify | 5.x | 2FA (TOTP), gestão de sessão |
| Frontend | Blade + Tailwind CSS + Vite | 3.x | SSR com assets compilados |
| Autorização | Custom (ControlleAcesso) | — | Controle modular por CPF e flags de permissão |

Veja também:
- [Arquitetura detalhada](arquitetura.md)
- [Segurança e LGPD](seguranca.md)
