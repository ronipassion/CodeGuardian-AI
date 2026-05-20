# Projeto CodeGuardian AI - Sistema Inteligente de Garantia de Qualidade de Software

**Programa:** Residência Tecnológica TAKEOFF 2026.1
**Instituição:** Senac
**Turma:** Accenture 1
**Professor:** Júlio Cesar
**Equipe/Alunos:** Phelipe Leandro, Nikolas Messias, Ronald da Paixão, Vinicius Manoel

**Status:** Andamento do Projeto (Fase 1)

## Visão Geral
[cite_start]O CodeGuardian AI é um sistema multiagente projetado para avaliar, auditar e otimizar a qualidade de um software durante o seu planejamento[cite: 164]. [cite_start]O projeto simula o funcionamento de uma equipe autônoma de QA (Quality Assurance) discutindo critérios de qualidade, padrões de boas práticas e riscos de falhas por meio de linguagem natural, sem a geração de código[cite: 161, 162, 164].

[cite_start]Nesta etapa inicial, validamos a infraestrutura local de Inteligência Artificial e implementamos o fluxo núcleo de orquestração técnica, focando na auditoria de CI/CD e escalabilidade de infraestrutura[cite: 3].

---

## 1. Documentação dos Agentes
[cite_start]Para esta primeira entrega, estabelecemos a comunicação e a hierarquia entre o orquestrador e o primeiro especialista do time de 8 agentes previstos na arquitetura[cite: 165].

* **Quality Orchestrator AI:** Analista de requisitos que coordena os demais agentes. [cite_start]Atua no gerenciamento da equipe, definindo etapas e consolidando o relatório técnico[cite: 167].
* [cite_start]**DevOps Engineer:** Especialista em automação responsável por sugerir automação de CI/CD e controle de qualidade contínua[cite: 167].

[cite_start]A documentation completa contendo as *System Messages*, formatação e personalidades exatas utilizadas no AutoGen Studio encontra-se no arquivo dedicado[cite: 124]:
* **[Acessar a Documentação de Agentes (agentes.md)](docs/agentes.md)**

---

## 2. Prompts e Inputs Iniciais
[cite_start]Para validar o sistema, inserimos um cenário focado em uma stack moderna lidando com alta disponibilidade (plataforma de locação de equipamentos audiovisuais)[cite: 191, 192]. 

**Input Inicial Fornecido ao Sistema:**
> [cite_start]"We are planning a new inventory and rental management platform for audiovisual equipment. The system needs to handle real-time availability updates and high-traffic bursts during local film festivals. Quality Orchestrator AI, initiate an audit with the DevOps Engineer focusing on CI/CD pipelines, automated testing integrations, and infrastructure scalability. Remember, discuss best practices and potential failures without writing code." [cite: 191, 192, 193, 194]

---

## 3. Evidências de Funcionamento e Execução
[cite_start]A infraestrutura foi configurada utilizando o modelo local `gpt-oss-20b` hospedado via LM Studio e orquestrado pela interface do AutoGen Studio[cite: 3, 15].

[cite_start]As evidências visuais obrigatórias do funcionamento do sistema estão localizadas na pasta `/evidencias`[cite: 128]:
* `config_modelo.png`: Demonstra a validação do modelo com o bypass estrutural JSON.
* [cite_start]`fluxo_team.png`: Demonstra a arquitetura hierárquica no Team Builder, com o Orquestrador alocado na primeira posição do fluxo[cite: 59, 60].
* [cite_start]`logs_lmstudio.jpg`: Comprova o consumo assíncrono e a geração de tokens diretamente no servidor local[cite: 83, 84, 85].
* `execucao_chat.png`: Captura do AutoGen Studio processando as respostas e a comunicação entre os agentes.

---

## 4. Roteiro Textual das Interações
[cite_start]O sistema provou ser capaz de operar de forma assíncrona[cite: 85]. [cite_start]O Orquestrador recebeu o escopo, estruturou o plano de auditoria e delegou os tópicos de infraestrutura ao DevOps Engineer[cite: 170, 171]. [cite_start]Após a devolutiva do especialista, o Orquestrador consolidou um relatório com recomendações práticas[cite: 167].

[cite_start]O roteiro textual completo e não editado da primeira interação, contendo as decisões de projeto recomendadas pela IA, encontra-se no arquivo dedicado[cite: 183]:
* **[Acessar a Interação Completa (sessao_01_devops.md)](interacoes/sessao_01_devops.md)**

---

## [cite_start]5. Explicação Técnica (Resolução de Problemas) [cite: 132]
[cite_start]Durante a implementação e integração das ferramentas, os seguintes desafios técnicos foram mapeados e solucionados[cite: 136, 137]:

* [cite_start]**Problema de Compatibilidade de Modelo:** O AutoGen rejeitou a nomenclatura padrão do modelo local (`openai/gpt-oss-20b`) exigindo o parâmetro estrito `model_info`[cite: 35, 36].
* **Solução Aplicada:** A configuração foi sobrescrita via edição do JSON do componente de modelo. O parâmetro `structured_output` foi definido como `false` para garantir a compatibilidade de parsing com o servidor do LM Studio, permitindo o carregamento bem-sucedido.
* [cite_start]**Problema de Interface (Timeout Visual):** Modelos mais pesados (20B parâmetros) apresentaram um tempo de resposta (TTFB) elevado, gerando a impressão de travamento na interface de inferência do AutoGen[cite: 18, 19].
* [cite_start]**Solução Aplicada:** O monitoramento de orquestração foi deslocado para o console nativo do LM Studio, permitindo a verificação de streaming de tokens em tempo real para confirmar a execução assíncrona sem interromper a sessão[cite: 84, 85].