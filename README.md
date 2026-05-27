# CodeGuardian AI 🛡️

Sistema multiagente de garantia de qualidade de software, desenvolvido com **AutoGen + LM Studio (GPT-OSS 20B local)** como projeto acadêmico de Agentic AI.

---

## 🎯 Objetivo

O CodeGuardian AI simula uma equipe autônoma de QA que **avalia, audita e debate** a qualidade de um software em fase de planejamento — tudo via diálogo em linguagem natural entre agentes especializados com vieses opostos.

Os agentes **não geram código**: eles discutem critérios de qualidade, boas práticas, riscos e melhorias de processo — e **entram em conflito produtivo** para chegar ao melhor diagnóstico possível.

---

## 🤖 Estrutura de Agentes

| # | Agente | Papel | Descrição |
|---|--------|-------|-----------|
| 1 | **Quality_Orchestrator** | Orquestrador e Mediador | Interpreta o briefing do cliente, define o plano de auditoria e medeia os conflitos entre especialistas para consolidar um relatório final coeso e fundamentado. |
| 2 | **Requirements_Reviewer** | Analista de Requisitos — o Cético | Analisa clareza, completude, rastreabilidade e testabilidade dos requisitos para garantir que nenhuma funcionalidade seja desenvolvida sobre premissas ambíguas ou indefinidas. |
| 3 | **Architecture_Inspector** | Arquiteto de Software — o Visionário | Avalia modularidade, acoplamento, padrões de design e separação de responsabilidades para identificar decisões arquiteturais que comprometam escalabilidade ou manutenibilidade futura. |
| 4 | **Code_Practices_Advisor** | Consultor de Boas Práticas — o Pragmático | Examina convenções de nomenclatura, processos de revisão de código, padrões de estilo e estratégias de documentação para assegurar que a base de código seja sustentável pelo time a longo prazo. |
| 5 | **Test_Strategist** | Engenheiro de Testes — o Paranoico | Define tipos de teste, metas de cobertura, estratégia de dados e critérios de aceitação para garantir que nenhuma funcionalidade seja considerada entregue sem validação verificável. |
| 6 | **DevOps_Engineer** | Especialista em Automação — o Pragmático da Entrega | Audita pipelines de CI/CD, separação de ambientes, containerização e observabilidade para assegurar que o processo de entrega seja automatizado, rastreável e livre de intervenção manual. |
| 7 | **Security_Analyst** | Analista de Segurança — o Inflexível | Identifica vulnerabilidades em autenticação, proteção de dados, validação de entradas e conformidade com LGPD para garantir que dados sensíveis nunca sejam tratados como responsabilidade secundária. |
| 8 | **Metrics_Reporter** | Gerador de Relatórios — o Árbitro dos Números | Consolida os scores individuais, mapeia pontos de conflito entre agentes e gera o scorecard final para transformar o debate qualitativo da equipe em indicadores objetivos e acionáveis. |

---

## ⚔️ Filosofia de Conflito Produtivo


As evidências visuais obrigatórias do funcionamento do sistema estão localizadas na pasta `/evidencias`:
* `01_autoGen_team.png`: Demonstra a arquitetura hierárquica no Team Builder, com o Orquestrador alocado na primeira posição do fluxo.
* `02_autoGen+lmStudio_fluxo.jpg`: Comprova a comunicação entre o front-end (AutoGen) e o servidor local do LM Studio (consumo assíncrono e logs de processamento).
* `03_autoGen_fluxo_Agents.png`: Apresenta o grafo visual do fluxo de execução, detalhando a passagem de turnos e o consumo de tokens entre o UserProxy, Orquestrador e DevOps Engineer.
* `04_Agent_Steps_01.png`, `05_Agent_Steps_02.png` e `06_Agent_Steps_03.png`: Capturas de tela sequenciais comprovando a comunicação detalhada, a delegação de tarefas e os relatórios gerados pelos agentes na interface.
=======
Agentes que concordam com tudo produzem relatórios sem valor. O CodeGuardian AI foi projetado para que cada especialista **defenda seu ponto de vista com convicção**, desafiando os outros quando necessário.

| Conflito | Tensão |
|----------|--------|
| Requirements_Reviewer ↔ Architecture_Inspector | Escopo real vs. elegância técnica |
| Architecture_Inspector ↔ Code_Practices_Advisor | Visão de longo prazo vs. praticidade do time |
| Test_Strategist ↔ DevOps_Engineer | Cobertura antes do deploy vs. velocidade de entrega |
| Security_Analyst ↔ DevOps_Engineer | Controles de segurança vs. agilidade do pipeline |
| Security_Analyst ↔ Code_Practices_Advisor | Compliance LGPD vs. produtividade do dev |
| Requirements_Reviewer ↔ Security_Analyst | Escopo definido vs. LGPD não negociável |

O **Orquestrador** não suprime os conflitos — ele os nomeia, medeia e extrai o melhor resultado de cada tensão.

---

## 🔁 Fluxo de Execução

```
User_Proxy (briefing do cliente)
        ↓
Quality_Orchestrator     ← apresenta o projeto e convoca o time
        ↓
Requirements_Reviewer    ← avalia requisitos e desafia suposições
        ↓
Architecture_Inspector   ← avalia arquitetura e contra-argumenta
        ↓
Code_Practices_Advisor   ← avalia práticas e questiona complexidade
        ↓
Test_Strategist          ← avalia testes e pressiona por cobertura
        ↓
DevOps_Engineer          ← avalia CI/CD e negocia gates incrementais
        ↓
Security_Analyst         ← avalia segurança e não cede em LGPD
        ↓
Metrics_Reporter         ← gera scorecard e mapeia conflitos
        ↓
Quality_Orchestrator     ← medeia, resolve e entrega relatório final em pt-BR
```

---

## 🧪 Caso de Teste — Projeto EduTrack

* **Problema de Compatibilidade de Modelo:** O AutoGen rejeitou a nomenclatura padrão do modelo local (`openai/gpt-oss-20b`) exigindo o parâmetro estrito `model_info`.
* **Solução Aplicada:** A configuração foi sobrescrita via edição do JSON do componente de modelo. O parâmetro `structured_output` foi definido como `false` para garantir a compatibilidade de parsing com o servidor do LM Studio, permitindo o carregamento bem-sucedido.
* **Problema de Interface (Timeout Visual):** Modelos mais pesados (20B parâmetros) apresentaram um tempo de resposta (TTFB) elevado, gerando a impressão de travamento na interface de inferência do AutoGen.
* **Solução Aplicada:** O monitoramento de orquestração foi deslocado para o console nativo do LM Studio, permitindo a verificação de streaming de tokens em tempo real para confirmar a execução assíncrona sem interromper a sessão.
=======
O briefing usado para a primeira auditoria foi o **EduTrack**, um sistema de gestão de desempenho escolar:

- **Cliente:** Rede de escolas privadas, 5.000 alunos, 10 unidades
- **Stack:** React + Node.js/Express + PostgreSQL, hospedagem VPS
- **Problemas intencionais:** sem framework de autenticação, sem estratégia de testes, sem CI/CD, equipe de 3 devs júnior + 1 tech lead part-time, prazo de 4 meses

### Resultado da Auditoria (primeira execução)

| Dimensão | Score | Status |
|----------|-------|--------|
| Requirements | 6/10 | ⚠ |
| Architecture | 5/10 | ⚠ |
| Code Practices | 7/10 | ✓ |
| Testing | 4/10 | ✗ |
| DevOps | 0/10 | ✗ |
| Security | 2/10 | ✗ |
| **OVERALL** | **5.5/10** | ⚠ |

### Principais Conflitos Identificados

1. **Code Practices vs Testing** — Code_Practices_Advisor (7/10) vs Test_Strategist (4/10): debate sobre padrões de código sem testes automatizados.
2. **Requirements vs Security** — Requirements_Reviewer (6/10) vs Security_Analyst: ausência de regras de negócio críticas expõe dados de menores.
3. **Architecture vs Velocidade** — Architecture_Inspector (5/10) vs urgência de entrega em 4 meses: monólito viável mas com risco de acoplamento extremo.

---

## 🖥️ Evidências de Funcionamento

### Execução da Auditoria

| Screenshot | Conteúdo |
|------------|----------|
| `01_briefing_enviado.png` | User Proxy enviando o briefing do EduTrack ao Orquestrador |
| `02_orchestrator_plano_auditoria.png` | Quality Orchestrator apresentando o projeto e convocando os agentes |
| `03_requirements_reviewer_analise.png` | Requirements Reviewer avaliando clareza e completude dos requisitos |
| `04_architecture_inspector_conflito.png` | Architecture Inspector desafiando Requirements Reviewer sobre escopo vs. arquitetura |
| `05_code_practices_evaluation.png` | Code Practices Advisor com bloco `<evaluation>` — Score 7/10 |
| `06_test_strategist_evaluation.png` | Test Strategist com bloco `<evaluation>` — Score 4/10 |
| `07_devops_riscos_pipeline.png` | DevOps Engineer listando riscos de deploy manual e conflito com Test Strategist |
| `08_security_analyst_lgpd.png` | Security Analyst — Score 2/10, identificando risco LGPD para dados de menores |
| `09_metrics_scorecard.png` | Metrics Reporter gerando o scorecard final com TOP CONFLICT POINTS |
| `10_orchestrator_relatorio_final.png` | Quality Orchestrator entregando relatório consolidado em pt-BR |
| `11_segunda_rodada_requirements.png` | Segunda rodada — Requirements Reviewer com evaluation de Architecture |
| `12_segunda_rodada_architecture.png` | Segunda rodada — Architecture Inspector revisando posição |
| `13_segunda_rodada_code_practices.png` | Segunda rodada — Code Practices Advisor auditoria completa |
| `14_segunda_rodada_test_strategist.png` | Segunda rodada — Test Strategist reforçando necessidade de cobertura |
| `15_segunda_rodada_devops.png` | Segunda rodada — DevOps Engineer propondo gates incrementais |

---

## 🗂️ Estrutura do Repositório

```
CodeGuardian-AI/
├── README.md
├── V2/
│   ├── codeguardian.py          ← script principal (AutoGen + LM Studio)
│   └── docs/
│       └── agentes.md           ← system messages completos de cada agente
└── prints/
    ├── 01_briefing_enviado.png
    ├── 02_orchestrator_plano_auditoria.png
    ├── 03_requirements_reviewer_analise.png
    ├── 04_architecture_inspector_conflito.png
    ├── 05_code_practices_evaluation.png
    ├── 06_test_strategist_evaluation.png
    ├── 07_devops_riscos_pipeline.png
    ├── 08_security_analyst_lgpd.png
    ├── 09_metrics_scorecard.png
    ├── 10_orchestrator_relatorio_final.png
    ├── 11_segunda_rodada_requirements.png
    ├── 12_segunda_rodada_architecture.png
    ├── 13_segunda_rodada_code_practices.png
    ├── 14_segunda_rodada_test_strategist.png
    └── 15_segunda_rodada_devops.png
```

---

## ⚙️ Stack Tecnológica

| Componente | Tecnologia |
|------------|------------|
| LLM local | GPT-OSS 20B via LM Studio |
| Orquestração | AutoGen (pyautogen==0.2.35) |
| Linguagem | Python 3.11 |
| Interface | Terminal (PowerShell) |

### Hardware utilizado
- CPU: Intel i7-10750H
- RAM: 16 GB
- GPU: RTX 2060 6GB

---

## 🚀 Como Executar

### 1. Pré-requisitos

```cmd
C:\...python.exe -m pip install pyautogen==0.2.35
```

### 2. Iniciar o LM Studio

- Abrir o LM Studio
- Carregar o modelo `GPT-OSS 20B`
- Ir em **Local Server → Start Server**
- Confirmar que está rodando em `http://localhost:1234`

### 3. Rodar o script

```cmd
codeguardian.py
```

Pressione **Enter** cada vez que o terminal pausar para o próximo agente falar.

---

## 📋 Andamento do Projeto

### ✅ Entrega Parcial 
- [x] Definição e documentação dos 8 agentes com system messages completos
- [x] Implementação do conflito produtivo entre agentes
- [x] Configuração do LM Studio como provedor local (GPT-OSS 20B)
- [x] Script funcional com GroupChat orquestrado via AutoGen
- [x] Briefing de cliente para teste (projeto EduTrack)
- [x] Primeira execução completa com evidências (15 prints)
- [x] Scorecard gerado automaticamente pelo Metrics Reporter
- [x] Relatório final em português entregue pelo Orquestrador

### 🔄 Próximas Entregas
- [ ] Roteiro textual completo das interações
- [ ] Análise das curiosidades (conflitos, personalidades, riscos por agente)
- [ ] Melhorias na coordenação multiagente
- [ ] Apresentação final no CodeDay


