# Projeto CodeGuardian AI - Sistema Inteligente de Garantia de Qualidade de Software

**Programa:** Residência Tecnológica TAKEOFF 2026.1
**Instituição:** Senac
**Turma:** Accenture 1
**Professor:** Júlio Cesar
**Equipe/Alunos:** Phelipe Leandro, Nikolas Messias, Ronald da Paixão, Vinicius Manoel

**Status:** Andamento do Projeto (Fase 1)

## Visão Geral
O CodeGuardian AI é um sistema multiagente projetado para avaliar, auditar e otimizar a qualidade de um software durante o seu planejamento. O projeto simula o funcionamento de uma equipe autônoma de QA (Quality Assurance) discutindo critérios de qualidade, padrões de boas práticas e riscos de falhas por meio de linguagem natural, sem a geração de código.

Nesta etapa inicial, validamos a infraestrutura local de Inteligência Artificial e implementamos o fluxo núcleo de orquestração técnica, focando na auditoria de CI/CD e escalabilidade de infraestrutura.

---

## 1. Documentação dos Agentes
Para esta primeira entrega, estabelecemos a comunicação e a hierarquia entre o orquestrador e o primeiro especialista do time de 8 agentes previstos na arquitetura.

* **Quality Orchestrator AI:** Analista de requisitos que coordena os demais agentes. Atua no gerenciamento da equipe, definindo etapas e consolidando o relatório técnico.
* **DevOps Engineer:** Especialista em automação responsável por sugerir automação de CI/CD e controle de qualidade contínua.

A documentação completa contendo as *System Messages*, formatação e personalidades exatas utilizadas no AutoGen Studio encontra-se no arquivo dedicado:
* **[Acessar a Documentação de Agentes (agentes.md)](docs/agentes.md)**

---

## 2. Prompts e Inputs Iniciais
Para validar o sistema, inserimos um cenário focado em uma stack moderna lidando com alta disponibilidade (plataforma de locação de equipamentos audiovisuais). 

**Input Inicial Fornecido ao Sistema:**
> "We are planning a new inventory and rental management platform for audiovisual equipment. The system needs to handle real-time availability updates and high-traffic bursts during local film festivals. Quality Orchestrator AI, initiate an audit with the DevOps Engineer focusing on CI/CD pipelines, automated testing integrations, and infrastructure scalability. Remember, discuss best practices and potential failures without writing code."

---

## 3. Evidências de Funcionamento e Execução
A infraestrutura foi configurada utilizando o modelo local `gpt-oss-20b` hospedado via LM Studio e orquestrado pela interface do AutoGen Studio.

As evidências visuais obrigatórias do funcionamento do sistema estão localizadas na pasta `/evidencias`:
* `01_autoGen_team.png`: Demonstra a arquitetura hierárquica no Team Builder, com o Orquestrador alocado na primeira posição do fluxo.
* `02_autoGen+lmStudio_fluxo.jpg`: Comprova a comunicação entre o front-end (AutoGen) e o servidor local do LM Studio (consumo assíncrono e logs de processamento).
* `03_autoGen_fluxo_Agents.png`: Apresenta o grafo visual do fluxo de execução, detalhando a passagem de turnos e o consumo de tokens entre o UserProxy, Orquestrador e DevOps Engineer.
* `04_Agent_Steps_01.png`, `05_Agent_Steps_02.png` e `06_Agent_Steps_03.png`: Capturas de tela sequenciais comprovando a comunicação detalhada, a delegação de tarefas e os relatórios gerados pelos agentes na interface.

---

## 4. Roteiro Textual das Interações
O sistema provou ser capaz de operar de forma assíncrona. O Orquestrador recebeu o escopo, estruturou o plano de auditoria e delegou os tópicos de infraestrutura ao DevOps Engineer. Após a devolutiva do especialista, o Orquestrador consolidou um relatório com recomendações práticas.

O roteiro textual completo e não editado da primeira interação, contendo as decisões de projeto recomendadas pela IA, encontra-se no arquivo dedicado:
* **[Acessar a Interação Completa (sessao_01_devops.md)](interacoes/sessao_01_devops.md)**

---

## 5. Explicação Técnica (Resolução de Problemas)
Durante a implementação e integração das ferramentas, os seguintes desafios técnicos foram mapeados e solucionados:

* **Problema de Compatibilidade de Modelo:** O AutoGen rejeitou a nomenclatura padrão do modelo local (`openai/gpt-oss-20b`) exigindo o parâmetro estrito `model_info`.
* **Solução Aplicada:** A configuração foi sobrescrita via edição do JSON do componente de modelo. O parâmetro `structured_output` foi definido como `false` para garantir a compatibilidade de parsing com o servidor do LM Studio, permitindo o carregamento bem-sucedido.
* **Problema de Interface (Timeout Visual):** Modelos mais pesados (20B parâmetros) apresentaram um tempo de resposta (TTFB) elevado, gerando a impressão de travamento na interface de inferência do AutoGen.
* **Solução Aplicada:** O monitoramento de orquestração foi deslocado para o console nativo do LM Studio, permitindo a verificação de streaming de tokens em tempo real para confirmar a execução assíncrona sem interromper a sessão.
