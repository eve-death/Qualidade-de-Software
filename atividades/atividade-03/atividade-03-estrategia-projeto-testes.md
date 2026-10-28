# Atividade 3: Estratégia e Projeto de Testes do LocalEats

**Unidade Curricular:** Qualidade de Software

**Projeto:** LocalEats (https://local-eats-unisenac.vercel.app/)

**Modalidade:** Individual

**Integrante:** Mariana Borges

**Funcionalidade analisada:** Fazer pedido

## Tarefa 1: Planejamento dos testes

### 1.1 Objetivo dos testes

Verificar se o usuário consegue montar e finalizar um pedido no LocalEats de forma consistente: os pratos escolhidos devem ser mantidos enquanto ele navega pelo aplicativo, e o pedido só pode ser finalizado por um usuário autenticado e com pelo menos um item.

### 1.2 Escopo

| **Integrante** | **Funcionalidade incluída** | **O que será verificado**                                                                                                               |
|----------------|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| Mariana Borges | Fazer pedido                | Manutenção dos pratos no pedido em andamento e condições para finalizar o pedido (usuário autenticado e pedido com pelo menos um item). |

| **Funcionalidade não incluída**       | **Justificativa**                                                                                    |
|---------------------------------------|------------------------------------------------------------------------------------------------------|
| Criar conta                           | Não faz parte do fluxo de pedido escolhido; a conta de teste será criada antes do início dos testes. |
| Favoritar e desfavoritar restaurantes | É independente do fluxo de montagem e finalização do pedido.                                         |
| Pesquisar e filtrar restaurantes      | É usada apenas para chegar ao restaurante; o foco dos testes está no pedido.                         |

### 1.3 Abordagem

| **Item**                                | **Decisão da equipe**                    | **Justificativa**                                                                                                                                                                          |
|-----------------------------------------|------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Níveis de teste                         | Sistema                                  | O fluxo será analisado pela interface, da escolha do prato até o pedido registrado.                                                                                                        |
| Tipos de teste                          | Funcional                                | O objetivo é verificar as regras de montagem e de finalização do pedido.                                                                                                                   |
| Perspectiva caixa-preta ou caixa-branca | Caixa-preta                              | Serão consideradas entradas e resultados observáveis na tela, sem acesso ao código.                                                                                                        |
| Técnicas de teste                       | Transição de estados e tabela de decisão | O pedido em andamento muda de situação conforme as ações do usuário (transição de estados) e a finalização depende da combinação entre autenticação e itens no pedido (tabela de decisão). |

### 1.4 Ambiente e responsabilidades

| **Item**                                  | **Definição**                                                                                                                                                                                                                 |
|-------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Ambiente necessário                       | Aplicação em https://local-eats-unisenac.vercel.app/, navegador de computador atualizado, conexão estável à internet, uma conta de teste com dados fictícios e pelo menos um restaurante com dois ou mais pratos no cardápio. |
| Responsáveis pelo planejamento            | Mariana Borges                                                                                                                                                                                                                |
| Responsáveis pela especificação dos casos | Mariana Borges                                                                                                                                                                                                                |
| Responsáveis pela futura execução         | Mariana Borges                                                                                                                                                                                                                |

### 1.5 Critérios

| **Critério** | **Definição da equipe**                                                                                          |
|--------------|------------------------------------------------------------------------------------------------------------------|
| Entrada      | Aplicação disponível, conta de teste cadastrada e pelo menos um restaurante com dois ou mais pratos no cardápio. |
| Saída        | Os três casos planejados executados e os resultados registrados.                                                 |
| Suspensão    | Aplicação indisponível, impossibilidade de entrar com a conta de teste ou lista de restaurantes que não carrega. |

## Tarefa 2: Riscos e técnicas de teste

### 2.1 Análise dos riscos

| **ID** | **Integrante** | **Funcionalidade** | **Risco**                                                                                          | **Consequência**                                                                                                                            | **Probabilidade** | **Impacto** | **Prioridade** | **Justificativa**                                                                                                                                                                   |
|--------|----------------|--------------------|----------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|-------------------|-------------|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| R01    | Mariana Borges | Fazer pedido       | Os pratos adicionados ao pedido desaparecerem quando o usuário volta para a lista de restaurantes. | O usuário perde o pedido em andamento, precisa refazê-lo e pode desistir; o restaurante perde a venda.                                      | Alta              | Média       | Alta           | A perda dos itens foi percebida na exploração da funcionalidade (Atividade 1) e pode atingir qualquer usuário que navegue durante o pedido, mas o usuário ainda consegue refazê-lo. |
| R02    | Mariana Borges | Fazer pedido       | O pedido ser finalizado sem itens ou por um usuário não autenticado.                               | Um pedido vazio ou sem dono é registrado, o restaurante recebe um pedido inválido e o usuário pode achar que fez uma compra que não existe. | Média             | Alta        | Alta           | A finalização é a etapa final do fluxo e afeta usuário e restaurante. Como o sistema não oferece cancelamento de pedido, um registro indevido é difícil de corrigir.                |

### 2.2 Aplicação da técnica

**Técnica 1**

**Integrante responsável:** Mariana Borges

**Funcionalidade:** Fazer pedido

**Risco relacionado:** R01

**Técnica escolhida:** Transição de estados

**Por que a técnica foi escolhida?**

O pedido em andamento muda de situação conforme o usuário adiciona pratos, remove pratos, navega pelo aplicativo e finaliza. O risco R01 está justamente em uma dessas transições (navegar para a lista e voltar), que deve manter os itens. A técnica permite listar as transições permitidas e as bloqueadas e escolher quais verificar.

**Aplicação da técnica**

Estados identificados: Vazio, Com itens e Pedido registrado.

| **Transição**                 | **Evento**                                                     | **Situação**                                    |
|-------------------------------|----------------------------------------------------------------|-------------------------------------------------|
| Vazio → Com itens             | Adicionar um prato                                             | Válida                                          |
| Com itens → Com itens         | Adicionar outro prato ou remover um prato mantendo ao menos um | Válida                                          |
| Com itens → Com itens         | Navegar para a lista de restaurantes e voltar                  | Válida: os itens devem ser mantidos (risco R01) |
| Com itens → Vazio             | Remover o único prato                                          | Válida                                          |
| Com itens → Pedido registrado | Finalizar o pedido com usuário autenticado                     | Válida                                          |
| Vazio → Pedido registrado     | Finalizar o pedido sem itens                                   | Inválida: deve ser bloqueada (risco R02)        |

**Casos derivados**

CT01, que verifica a transição Com itens → Com itens ao navegar para a lista e voltar. A transição inválida Vazio → Pedido registrado é verificada pelo CT02, derivado da tabela de decisão.

**Técnica 2**

**Integrante responsável:** Mariana Borges

**Funcionalidade:** Fazer pedido

**Risco relacionado:** R02

**Técnica escolhida:** Tabela de decisão

**Por que a técnica foi escolhida?**

O resultado da finalização depende da combinação de duas condições: o usuário estar autenticado e o pedido ter itens. A tabela de decisão organiza todas as combinações e o resultado esperado de cada uma, o que é adequado ao risco R02.

**Aplicação da técnica**

| **Regra** | **Usuário autenticado?** | **Pedido tem itens?** | **Resultado esperado**                          |
|-----------|--------------------------|-----------------------|-------------------------------------------------|
| 1         | Sim                      | Sim                   | Permitir a finalização e registrar o pedido     |
| 2         | Sim                      | Não                   | Impedir a finalização e não registrar o pedido  |
| 3         | Não                      | Sim                   | Solicitar autenticação e não registrar o pedido |
| 4         | Não                      | Não                   | Solicitar autenticação e não registrar o pedido |

As regras 2 e 3 representam as condições inválidas do risco e foram priorizadas. A regra 1 é o fluxo principal e a regra 4 combina as duas condições inválidas, com resultado semelhante ao da regra 3; elas ficam fora dos três casos previstos para esta entrega.

**Casos derivados**

CT02 (regra 2) e CT03 (regra 3).

## Tarefa 3: Casos de teste e rastreabilidade

### 3.1 Especificação dos casos de teste

### CT01: Manter os pratos do pedido ao navegar para a lista e voltar

**Integrante responsável:** Mariana Borges

**Funcionalidade:** Fazer pedido

**Risco relacionado:** R01

**Técnica utilizada:** Transição de estados (Com itens → Com itens ao navegar e voltar)

**Pré-condição:**

O usuário está autenticado com a conta de teste, o pedido em andamento está vazio e existe um restaurante com pelo menos um prato no cardápio.

**Dados de entrada:**

Restaurante: Restaurante Sabor 1 (ou outro com cardápio disponível)

Prato: Prato Especial 0, uma unidade

**Passos:**

1.  Acessar a lista de restaurantes e abrir o Restaurante Sabor 1.

2.  Adicionar o Prato Especial 0 ao pedido e confirmar que ele aparece no resumo do pedido.

3.  Voltar para a lista de restaurantes.

4.  Abrir novamente o Restaurante Sabor 1.

**Resultado esperado:**

O resumo do pedido continua exibindo 1x Prato Especial 0, com o total correspondente ao valor do prato, e nenhum item foi removido.

### CT02: Impedir a finalização de um pedido sem itens

**Integrante responsável:** Mariana Borges

**Funcionalidade:** Fazer pedido

**Risco relacionado:** R02

**Técnica utilizada:** Tabela de decisão (regra 2: autenticado e pedido sem itens)

**Pré-condição:**

O usuário está autenticado com a conta de teste e a quantidade de pedidos existentes em "Meus Pedidos" foi anotada.

**Dados de entrada:**

Restaurante: Restaurante Sabor 1 (ou outro com cardápio disponível)

Prato: Prato Especial 0, adicionado e depois removido

**Passos:**

1.  Abrir o Restaurante Sabor 1 e adicionar o Prato Especial 0 ao pedido.

2.  Remover o prato pelo controle de remoção do resumo do pedido, deixando o pedido sem itens.

3.  Tentar acionar "Finalizar Pedido".

4.  Abrir "Meus Pedidos" e comparar a quantidade de pedidos com a anotada antes do teste.

**Resultado esperado:**

O sistema não registra o pedido: o botão de finalizar fica indisponível ou uma mensagem informa que o pedido está vazio. A quantidade de pedidos em "Meus Pedidos" continua a mesma.

### CT03: Impedir a finalização do pedido por usuário não autenticado

**Integrante responsável:** Mariana Borges

**Funcionalidade:** Fazer pedido

**Risco relacionado:** R02

**Técnica utilizada:** Tabela de decisão (regra 3: não autenticado e pedido com itens)

**Pré-condição:**

Nenhum usuário está autenticado (sessão encerrada) e a conta de teste está disponível para uma verificação posterior.

**Dados de entrada:**

Restaurante: Restaurante Sabor 1 (ou outro com cardápio disponível)

Prato: Prato Especial 0, uma unidade

**Passos:**

1.  Sem entrar no sistema, acessar https://local-eats-unisenac.vercel.app/ e abrir o Restaurante Sabor 1.

2.  Adicionar o Prato Especial 0 ao pedido.

3.  Tentar acionar "Finalizar Pedido".

4.  Entrar com a conta de teste e abrir "Meus Pedidos".

**Resultado esperado:**

O sistema não registra o pedido e exige que o usuário se autentique antes de finalizar (ao adicionar o prato ou ao finalizar). Em "Meus Pedidos" não existe um pedido criado por essa tentativa.

### 3.2 Matriz de rastreabilidade

| **Integrante** | **Funcionalidade** | **Risco ou requisito**                                        | **Técnica utilizada** | **Casos de teste** |
|----------------|--------------------|---------------------------------------------------------------|-----------------------|--------------------|
| Mariana Borges | Fazer pedido       | R01: perda dos pratos ao navegar para a lista de restaurantes | Transição de estados  | CT01               |
| Mariana Borges | Fazer pedido       | R02: pedido finalizado sem itens ou sem autenticação          | Tabela de decisão     | CT02 e CT03        |

Todos os riscos identificados têm pelo menos um caso de teste. Nenhum risco ficou sem cobertura.

## Uso de inteligência artificial

**Ferramenta utilizada:**

Claude (Anthropic).

**Como foi utilizada:**

Usei como apoio para entender o enunciado, sugerir os riscos, comparar as técnicas e ajudar a redigir o plano, os casos de teste e a matriz de rastreabilidade.

**Uma sugestão que precisou ser alterada ou rejeitada:**

Na Atividade 1, a IA sugeriu inicialmente que a coluna "Evidência" da Tarefa 2 listasse o nome de cada arquivo anexado (ex.: mariana-pedido-painel-fixo.mp4). Rejeitei essa sugestão e defini eu mesma a formatação da tabela, orientando a IA a substituir por "Arquivos anexados", sem listar nomes individuais, e a manter essa mesma estrutura de organização dos arquivos nas demais atividades.

**Como as respostas foram verificadas:**

Revisei se os riscos são coerentes com o LocalEats, se as técnicas se aplicam às regras analisadas e se os passos e resultados esperados dos casos são compreensíveis e observáveis. Os casos ainda não foram executados.
