# Atividade 1: Fundamentos e Características da Qualidade no LocalEats

**Aluna:** Mariana Borges
**Modalidade:** Individual
**Projeto:** LocalEats — https://local-eats-unisenac.vercel.app/

## Tarefa 1: Fundamentos da qualidade

| Tipo | Necessidade | Interessado | Consequência se não for atendida |
|---|---|---|---|
| Explícita | O sistema deve permitir criar conta e entrar no sistema | Usuário | Sem login, o usuário não consegue favoritar restaurantes, fazer pedidos nem consultar seu histórico, tornando o app inutilizável para seu propósito principal |
| Explícita | O sistema deve permitir pesquisar e filtrar restaurantes por especialidade ou localização | Usuário | Sem uma forma eficaz de encontrar restaurantes de interesse, a navegação se torna inviável à medida que a base de restaurantes cresce |
| Implícita | A pesquisa por texto deve retornar resultados corretos e coerentes com o termo digitado | Usuário | O usuário perde a confiança na busca por texto, deixa de utilizá-la e passa a depender só dos filtros prontos, o que limita a usabilidade do sistema |
| Implícita | Os itens adicionados a um pedido devem permanecer disponíveis enquanto o usuário continua navegando pelo aplicativo | Usuário / Negócio | O usuário perde os itens já escolhidos, precisa refazer o pedido do zero, o que gera frustração e pode levar ao abandono da compra, com prejuízo para o restaurante e para a plataforma |

**Um sistema que implementa todas as funcionalidades explicitamente solicitadas pode, ainda assim, apresentar baixa qualidade?**

Sim. O LocalEats implementa todas as funcionalidades descritas (criar conta, explorar, pesquisar, favoritar, pedir, consultar pedidos), mas isso não garante qualidade. Por exemplo, a necessidade implícita de manter os itens do pedido durante a navegação não é atendida: ao voltar à lista de restaurantes, o item adicionado desaparece. A funcionalidade "existe", mas não funciona de forma confiável, o que compromete a experiência do usuário mesmo sem faltar nenhum requisito explícito.

## Tarefa 2: Exploração da aplicação

| Integrante | Funcionalidade | O que foi realizado | O que foi observado | Evidência |
|---|---|---|---|---|
| Mariana Borges | Fazer pedido | Uso esperado: adicionou um prato ao pedido em um restaurante e conferiu o painel "Seu Pedido". Uso alternativo/incompleto: tentou adicionar um segundo prato do mesmo restaurante com o painel de pedido aberto e, em seguida, voltou à lista de restaurantes | No uso esperado, o painel "Seu Pedido" atualizou corretamente, exibindo o item e o total. No uso alternativo, o painel permaneceu fixo no canto inferior direito mesmo ao rolar a página, cobrindo o botão "Adicionar" de outros pratos do mesmo restaurante; ao retornar à lista de restaurantes, o item que havia sido adicionado ao pedido desapareceu | Arquivos anexados |

## Tarefa 3: Requisitos e características de qualidade

| Integrante | Requisito de Qualidade | Característica ou subcaracterística | Justificativa | Como avaliar |
|---|---|---|---|---|
| Mariana Borges | O sistema deve manter os itens adicionados a um pedido visíveis e disponíveis durante toda a navegação do usuário, até que ele finalize ou cancele o pedido explicitamente | Adequação Funcional — Correção Funcional | No LocalEats, o pedido perde itens quando o usuário navega de volta à lista de restaurantes, ou seja, o sistema não produz o resultado correto esperado pelo usuário (manter o que foi selecionado). Isso não é uma questão de facilidade de uso, e sim de o sistema fazer o que deveria fazer | Testar repetidamente o fluxo de adicionar um ou mais itens ao pedido e navegar entre páginas do app, verificando se os itens permanecem no carrinho após a navegação; contar em quantas tentativas, de um conjunto definido, o item é perdido |

## Uso de inteligência artificial

**Ferramenta utilizada:** Claude (Anthropic).

**Como foi utilizada:** Utilizei o Claude para entender o que cada tarefa da atividade estava pedindo, para organizar minhas observações de teste no LocalEats nas tabelas solicitadas e para revisar a redação das respostas e do requisito de qualidade da Tarefa 3.

**Como as respostas foram verificadas:** Os testes na aplicação (busca, adicionar item ao pedido, navegação entre páginas) foram realizados por mim, com prints e vídeo como evidência. As classificações de característica/subcaracterística de qualidade foram conferidas com o material de aula sobre a ISO/IEC 25010.
