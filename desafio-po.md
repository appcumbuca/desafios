# Desafio Técnico - Product Owner
## Sobre Nós
Olá e muito obrigado pelo seu interesse na Cumbuca! Somos uma fintech que busca ajudar as pessoas a organizar as finanças junto de quem elas amam, simplificando a vida de nossos usuário e ajudando-os a organizarem-se financeiramente. No âmbito dessa missão, sempre buscamos pessoas excepcionais para nossa equipe. Esperamos ter você a bordo conosco em breve!

Pedimos que leia este documento **inteiro** com atenção para maximizar suas chances de sucesso.

O teste que você irá realizar consiste em construir um backlog de tarefas técnicas priorizadas a partir da especificação e protótipos de uma feature a ser implementada no aplicativo da Cumbuca. Especificamente, você irá mostrar como coordenaria a implementação dos fluxos de pagamento Pix e pagamento de boletos já presentes no app.

## O Desafio
### O Problema
Atualmente, o aplicativo da Cumbuca realiza pagamentos via Pix e pagamentos de boletos que podem ser divididos entre os membros de um grupo. Seu desafio é especificar as tarefas necessárias para a implementação, no aplicativo e no backend, dos fluxos de pagamento conforme especificados abaixo:

Um grupo, na Cumbuca, consiste em vários usuários que dividem pagamentos entre si. Membros de um grupo podem ser usuários comuns, que só têm autorização de movimentar o próprio dinheiro, ou administradores, que podem movimentar o dinheiro de qualquer membro do grupo.

O grupo é considerado como tendo um saldo total igual à soma dos saldos de todos os membros do grupo. Portanto, se um usuário administrador inicia um pagamento, ele pode realizar um pagamento cujo valor seja, no máximo o valor do saldo total do grupo, podendo dividir o pagamento entre quaisquer membros do grupo, com cada um contribuindo até o limite de seu próprio saldo. Todavia, um usuário comum só poderia realizar um pagamento até o valor total de seu próprio saldo, usando apenas este mesmo saldo para o pagamento.

#### Implementação no aplicativo

A implementação no aplicativo deve se ater aos fluxos conforme especificados no link a seguir, especificando todas as tarefas necessárias para implementá-los:

https://xd.adobe.com/view/f9b2400b-e02d-4745-8c11-a4d88c7d6781-ace1/

#### Implementação no backend

Nosso backend é implementado utilizando GraphQL. Todavia, para a sua especificação, você pode assumir que usaremos a tecnologia de interface de sua escolha (ex.: REST, gRPC, GraphQL), pois não desejamos atrelar este teste a conhecimento de alguma tecnologia específica.

Presuma que temos acesso a uma API que realiza pagamentos Pix e outra que realiza pagamentos de boleto. Temos o saldo de cada usuário guardado e atualizável de forma segura no banco de dados, mas ambas as APIs de pagamento tiram dinheiro de saldos individuais que pertencem à empresa Cumbuca, sendo portanto importante pensar na sincronização e consistência entre esses saldos. As informações de quais usuários pertencem a quais grupos e quais usuários são administradores ou usuários comuns também estão presentes no backend. Considere que cada usuário pertence a somente um grupo.

Você deve especificar todas as operações que devem ser implementadas no backend, explicando em alto nível como elas devem funcionar. Não é necessário entrar em detalhes operacionais de baixo nível, mas deve ser claro quais operações serão chamadas pelo front-end em cada fluxo e como elas funcionarão.

### Dúvidas
Se tiver qualquer dúvida ou sentir que necessita fazer qualquer pergunta, sinta-se à vontade para enviar e-mail para `pedrocastilho@cumbuca.com` para esclarecimentos sobre aspectos de tecnologia do desafio ou `rodrigo.cortez@cumbuca.com` para esclarecimentos sobre os fluxos de UI.

## Avaliação
### Entrega
Seu desafio deverá ser disponibilizado como um arquivo `.pdf` contendo as especificações das tarefas a serem executadas pela equipe de tecnologia. Esse arquivo deve ser enviado para os emails `pedrocastilho@cumbuca.com` quando completo, com o assunto `Desafio Product Owner Cumbuca`.

### Critérios
Uma vez disponibilizado a nós, a avaliação do seu backlog será realizada de acordo com os seguintes critérios:

#### Completude
As tarefas providas cobrem toda a especificação das features? É possível, baseado nessas tarefas, que o time de tecnologia implemente os fluxos _completamente_?

#### Corretude
As tarefas especificam corretamente os detalhes do fluxo? Se há partes mais complexas, elas estão especificadas em detalhes? A forma como as tarefas foram explicadas é suficiente para que o time de tecnologia implemente os fluxos _corretamente_?

#### Clareza
As tarefas estão escritas de forma clara e direta? A linguagem é inambígua? As especificações evitam introduzir complexidades desnecessárias à compreensão das tarefas?

#### Viabilidade Técnica
A forma como as tarefas foram divididas e especificadas é tecnicamente viável de ser executada? Serão necessárias muitas revisões técnicas por parte do time de tecnologia antes que as tarefas possam de fato ser iniciadas? As tarefas levam em consideração as informações providas sobre o sistema?

#### Divisão Justa
Existem tarefas significativamente mais complexas do que outras? Existem tarefas que poderiam ser divididas em tarefas menores? Caso seja necessário haver tarefas com maior complexidade de execução, isso está devidamente especificado?

### Após o desafio
Em geral, iremos avaliar sua submissão poucos dias após o envio. Uma vez que nossa
avaliação esteja completa, iremos enviar um feedback sobre sua resolução. Caso
esta seja aprovada, além do feedback, iremos marcar uma data para uma conversa por
videochamada com você.

#### Entrevista pós-desafio
Na entrevista após a entrega, conversaremos sobre principalmente sobre as 
decisões que você tomou ao resolver o desafio. Esteja pronta(o) para explicar as 
decisões que tomou, justificá-las e conversar sobre potenciais alternativas. 
Durante a entrevista, poderemos apresentar mudanças nas condições do desafio e 
perguntar sobre o que você faria diferentemente.
