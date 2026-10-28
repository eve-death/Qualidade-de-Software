# Atividade 2: Organização da Qualidade no LocalEats

**Unidade Curricular:** Qualidade de Software

**Projeto:** LocalEats

**Modalidade:** Individual

**Integrante:** Mariana Borges

## Tarefa 1: Diagnóstico da situação

| **Problema identificado**                                                      | **Possível consequência para o produto ou para a equipe**                                                                                                                       |
|--------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Os critérios para considerar uma funcionalidade pronta não estão claros.       | Funcionalidades chegam aos usuários com defeitos, cada pessoa entende "pronto" de um jeito e há retrabalho e discussões no fim do desenvolvimento.                              |
| Alguns integrantes acreditam que somente o QA deve testar.                     | O QA vira gargalo e fica sobrecarregado, quem desenvolve não cria testes nem revisa o próprio trabalho, e os defeitos são descobertos tarde, quando são mais caros de corrigir. |
| Os defeitos são identificados, mas nem sempre são registrados ou acompanhados. | Defeitos se perdem, reaparecem para os usuários, não há histórico nem prioridade, e a equipe não sabe quem está corrigindo o quê.                                               |

**A qualidade do LocalEats deve ser responsabilidade exclusiva do profissional de QA? Justifiquem.**

Não. A qualidade é construída ao longo do desenvolvimento, por vários papéis: o PO define critérios de aceitação, quem desenvolve implementa e cria testes unitários, a liderança técnica revisa e o QA planeja e executa os testes do sistema. Se só o QA for responsável, ele vira gargalo e os defeitos aparecem tarde, quando já chegaram perto do usuário. O QA orienta, verifica e dá visibilidade à qualidade, mas não a garante sozinho.

## Tarefa 2: Papéis e competências

Foram definidos quatro papéis: Responsável pelo produto (PO), Desenvolvedor, QA e Liderança técnica. O analista de negócio e o DevOps não viraram papéis separados para manter a proposta simples; a definição dos critérios fica com o PO e a prontidão técnica da versão com a liderança técnica.

| **Integrante** | **Papel analisado**           | **Responsabilidades relacionadas à qualidade**                                                                                                                                                                                       | **Competências técnicas**                                                                                                                                                                                                                                                                                                                                   | **Competências comportamentais**                                                                           |
|----------------|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
| Mariana Borges | Responsável pelo produto (PO) | Definir os critérios de aceitação junto com a equipe, priorizar a correção dos defeitos de acordo com o impacto no usuário, aceitar ou rejeitar as entregas e aprovar a disponibilização da versão.                                  | Escrita de histórias e critérios de aceitação, técnicas de priorização (valor e impacto), conhecimento do negócio de restaurantes e pedidos, leitura básica de indicadores de uso e de defeitos.                                                                                                                                                            | Comunicação clara, tomada de decisão, negociação entre prazo e qualidade e foco no usuário.                |
| Mariana Borges | Desenvolvedor                 | Implementar a funcionalidade, criar testes unitários, revisar o código dos colegas, corrigir defeitos e manter atualizado o status do que está corrigindo.                                                                           | Linguagem e frameworks do projeto, testes unitários, controle de versão (Git) e revisão de código, depuração de defeitos.                                                                                                                                                                                                                                   | Responsabilidade sobre o próprio código, colaboração, abertura para receber feedback e atenção a detalhes. |
| Mariana Borges | QA ou analista de qualidade   | Revisar requisitos quanto a clareza e possibilidade de teste, planejar e executar testes do sistema, registrar e acompanhar defeitos, dar um parecer de qualidade antes da liberação e orientar o time sobre boas práticas de teste. | Técnicas de teste (partição de equivalência, valor limite), escrita de casos de teste e relatos de defeito, ferramentas de gestão de defeitos, noções de automação e das características de qualidade da ISO/IEC 25010. Certificações como a ISTQB CTFL podem apoiar o desenvolvimento profissional, sem substituir a experiência e sem serem obrigatórias. | Pensamento crítico, comunicação objetiva e respeitosa ao relatar defeitos, curiosidade e organização.      |
| Mariana Borges | Liderança técnica             | Revisar o código, definir os padrões técnicos e os critérios técnicos de "pronto" (como revisão e testes unitários), garantir a prontidão técnica da versão e apoiar as decisões técnicas do time.                                   | Arquitetura de software, boas práticas de engenharia (revisão de código, integração contínua), análise de riscos técnicos.                                                                                                                                                                                                                                  | Mentoria, liderança, comunicação com perfis técnicos e não técnicos e mediação de conflitos.               |

## Tarefa 3: Matriz de responsabilidades

| **Atividade de qualidade**            | **Responsável pelo produto (PO)** | **Desenvolvedor** | **QA** | **Liderança técnica** |
|---------------------------------------|-----------------------------------|-------------------|--------|-----------------------|
| Definir critérios de aceitação        | A/R                               | C                 | C      | I                     |
| Revisar requisitos                    | A                                 | R                 | R      | C                     |
| Implementar a funcionalidade          | I                                 | A/R               | I      | C                     |
| Revisar o código                      | \-                                | R                 | I      | A/R                   |
| Criar testes unitários                | \-                                | A/R               | C      | C                     |
| Planejar e executar testes do sistema | C                                 | C                 | A/R    | I                     |
| Registrar e acompanhar defeitos       | I                                 | R                 | A/R    | I                     |
| Priorizar a correção dos defeitos     | A/R                               | C                 | C      | C                     |
| Aprovar a disponibilização da versão  | A/R                               | I                 | C      | C                     |

Legenda: R (Responsável), A (Aprovador), C (Consultado), I (Informado). A/R indica que o mesmo papel executa e responde pelo resultado. O sinal "-" indica que o papel não participa da atividade.

**Lacuna ou conflito encontrado**

A atividade "Aprovar a disponibilização da versão" fica concentrada no PO (A/R), com o QA e a liderança técnica apenas consultados. Isso pode levar a liberar uma versão com defeitos críticos conhecidos para cumprir prazo. Para reduzir o risco, o parecer do QA e a confirmação de prontidão técnica passam a ser exigidos antes da aprovação, e a Definition of Done serve como critério objetivo.

**Práticas recomendadas**

| **Prática recomendada**                                                                                                                                                            | **Problema que ajuda a resolver**                                                                                                                                                              | **Papéis envolvidos**                     |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------|
| Definição de "pronto" (Definition of Done) com critérios de aceitação escritos para cada funcionalidade, incluindo testes unitários, revisão de código e teste do sistema.         | Critérios de pronto pouco claros, funcionalidades que chegam aos usuários com defeitos e a ideia de que só o QA testa, porque os testes e a revisão passam a fazer parte do "pronto" de todos. | PO, Desenvolvedor, QA e Liderança técnica |
| Registro de todos os defeitos em um único quadro (por exemplo, GitHub Issues) com modelo padrão e uma reunião curta e regular de triagem para priorizar e atribuir um responsável. | Defeitos que não são registrados nem acompanhados, atividades sem responsável e falta de prioridade na correção.                                                                               | QA, Desenvolvedor e PO                    |

## Uso de inteligência artificial

**Ferramenta utilizada:**

Claude (Anthropic).

**Como foi utilizada:**

Usei como apoio para entender o enunciado, sugerir os papéis, a matriz RACI e as práticas de QA e ajudar a redigir o texto do documento.

**Como as respostas foram verificadas:**

Conferi a matriz com as regras do enunciado (ao menos um R e um único A por atividade), revisei se as responsabilidades de cada papel fazem sentido para o LocalEats e verifiquei se os problemas e as práticas estão ligados às situações descritas no contexto.
