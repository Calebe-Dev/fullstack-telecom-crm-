# OcHub — Portfolio Summary

## Elevator Pitch

Plataforma administrativa full-stack para distribuidoras de telecomunicações que centraliza CRM, ordens de serviço, marketing automatizado com IA e integrações com Google Workspace em uma interface Angular 20 SSR com API Express companion. Sistema em produção com 32 módulos, 4 containers Docker e SDK próprio para integrações externas.

---

## Stack de Tecnologias

![Angular](https://img.shields.io/badge/Angular-20_SSR-DD0031?style=for-the-badge&logo=angular&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5.9-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-20_LTS-339933?style=for-the-badge&logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express-5-000000?style=for-the-badge&logo=express&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-3-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![Google APIs](https://img.shields.io/badge/Google_APIs-OAuth_+_Workspace-4285F4?style=for-the-badge&logo=google&logoColor=white)
![Backend API](https://img.shields.io/badge/Backend API-Headless_CMS-64F?style=for-the-badge&logo=backend&logoColor=white)

---

## Números de Escala

| Métrica | Valor |
|---|---|
| 🏗️ Módulos de feature Angular | **32 módulos** |
| ⚙️ Services Angular (core) | **34 services** |
| 🛣️ Rotas lazy-loaded | **28+ rotas** |
| 🔌 Integrações externas | **3 (Backend API, Google, Freepik)** |
| 🐳 Containers em produção | **4 containers** |
| 📦 Versões do SDK | **4 releases (v1.0.2 → v1.1.0)** |
| 🤖 Sub-módulos do Worker IA | **7 (core, scrapers, skills, workflows...)** |
| 📜 Scripts de automação | **40+ scripts** |

---

## Destaques Técnicos para Portfolio

### 🤖 Sistema de IA em Produção
Pipeline end-to-end de geração de conteúdo editorial: agente de IA em container Docker isolado consome fila do CMS, gera HTML com LLM, enriquece com imagens via Freepik e publica em WordPress automaticamente. Sistema RAG local preserva confidencialidade do codebase.

### 📦 SDK Próprio Distribuído
`@grupooc/ochub-sdk` — biblioteca TypeScript versionada (4 releases) que permite a sistemas WordPress externos integrarem-se ao CRM sem acesso ao código-fonte. Demonstra capacidade de projetar interfaces públicas estáveis.

### 🔐 Autenticação OAuth 2.0 Completa
Implementação robusta de Google OAuth com renovação automática de token, múltiplos escopos (Calendar, Drive, Sheets), diagnóstico por stage de falha e health check integrado.

### 🏗️ Arquitetura Feature-Based com Lazy Loading
32 módulos Angular com carregamento sob demanda e strategy de preloading seletivo customizada para módulos de navbar, balanceando velocidade de inicialização e uso de bandwidth.

### 🔄 Infraestrutura Docker Multi-Serviço
4 containers orquestrados com limites de recursos configuráveis, volumes compartilhados, health checks e pipeline de deploy via shell script com página de manutenção automática.

### 📊 Observabilidade em Produção
Sistema de logs estruturados com persistência, métricas de performance de navegação coletadas automaticamente e health check unificado de todos os serviços externos.

### 🗄️ Migração de Dados em Escala
Suite completa de 10+ scripts de migração com snapshots, dry-run, staging e validação para migração de dados de clientes e pedidos sem downtime.

---

## Status do Projeto

🟢 **Em Produção** — Sistema ativo com deploy contínuo em servidor dedicado via Docker Compose. Desenvolvido e mantido como produto interno para um grupo de distribuidoras de telecomunicações.

---

## Repositório

> Este é um repositório **privado** de sistema interno. A documentação pública disponível nesta pasta representa uma visão portfolio-friendly sem exposição de dados sensíveis, credenciais ou lógica de negócio proprietária.

---

*Documentação gerada por: Antigravity Portfolio Orchestrator — 2026-06-17*
