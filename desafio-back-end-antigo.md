# Desafio de Programação Back-End
Olá e muito obrigado pelo seu interesse na Cumbuca! Somos uma fintech que busca ajudar as pessoas a organizar as finanças junto de quem elas amam, simplificando a vida de nossos usuário e ajudando-os a organizarem-se financeiramente. No âmbito dessa missão, sempre buscamos pessoas excepcionais para nossa equipe. Esperamos ter você a bordo conosco em breve!

Pedimos que leia este documento **inteiro** com atenção para maximizar suas
chances de sucesso.

O teste que você irá realizar consiste em elaborar um servidor de registro de
contas e transações financeiras. Esse sistema deve conseguir receber vários
pedidos de transação **simultaneamente**, registrar de forma persistente o histórico
de transações e retornar o saldo atual de cada conta. O sistema deve manter
a todo momento a consistência dos dados fornecidos e ser capaz de escalar de
forma simples.

## Sobre este documento
- O processo de envio da sua solução e os critérios que serão avaliados pela
equipe de tecnologia da Cumbuca estão descritos abaixo, na seção **Avaliação**.
- A interface que deve ser exposta pelo servidor está descrita na seção **Interface**.
- As regras que o sistema deve seguir estão descritas na seção **Regras de
Negócio**.
- As descrições de interfaces ocasionalmente referenciam entidades descritas na seção **Entidades**.

Caso não tenha certeza sobre qualquer coisa explicada neste documento (ou
qualquer dúvida em geral), fique à vontade para enviar um email para
tech@cumbuca.com com suas dúvidas.

## Avaliação
Seu desafio deverá ser disponibilizado por meio de um repositório Git
(podendo este ser hosteado da forma que for mais conveniente a você, por
exemplo usando uma plataforma como GitHub ou GitLab). A única restrição é que
o repositório deve ser acessível à equipe da Cumbuca. Caso não queira
disponibilizar seu código publicamente, converse conosco sobre como podemos
fazer para obter acesso a seu código.

### Critérios
Uma vez que ele seja disponibilizado a nós, a avaliação de seu código será feita de acordo com os seguintes critérios, em ordem aproximada de importância:

#### Ausência de bugs
Seu código deve funcionar corretamente, atendendo a todos os requisitos da especificação representada por este documento. Isso inclui ausência de bugs de concorrência.

##### Consistência Concorrente de Dados
**ATENÇÃO**: Caso esteja realizando este teste para a vaga no nível **Júnior**, este sub-requisito é **opcional**. Para os níveis **Pleno** e **Sênior**, ele é **obrigatório**.

Como parte do critério de Ausência de Bugs, os dados do sistema devem se manter
sempre consistentes, mesmo sob grande volume de requisições simultâneas.
Deve ser considerado que o sistema irá ser escalado horizontalmente, portanto
considere que os dados devem se manter consistentes mesmo sob modificações
concorrentes.

#### Legibilidade e Formatação
Lembre-se que um trecho de código em geral será lido muito mais vezes do que
escrito. Escreva seu código pensando em quem for lê-lo. Busque minimizar
dificuldades de leitura. Use a indentação a seu favor. Siga boas práticas de
formatação de código da linguagem escolhida.

#### Clareza
Seu código deve deixar a sua intenção clara para o leitor. Tanto quanto seja
plausível, deve ser possível entender o que o código faz apenas lendo ele.
Explicações usando comentários deveriam ser redundantes.

#### Desacoplamento
Seu código não deve criar dependências desnecessárias entre módulos.
Ao alterar uma parte do código, não deveria ser necessário alterar partes sem
relação lógica com a parte alterada.

#### Extensibilidade
Embora este desafio seja apenas teórico, busque considerar o código que você
desenvolverá como se ele fosse ser apenas uma parte de uma solução maior. Pense
no esforço necessário para realizar adições ao seu código e busque
minimizá-lo.

#### Manutenibilidade
Escreva seu código como se ele fosse ser mantido por muito tempo após você
criá-lo, por várias pessoas com níveis de experiência variados. Pense no
esforço necessário para alterar seu código e busque minimizá-lo. Se eu quiser mudar apenas um aspecto do código, precisarei mudar quantas partes dele?

#### Adicionais
**ATENÇÃO**: Caso esteja realizando o teste no nível **Sênior**, a presença de testes unitários e de integração é **obrigatória**.

- Testes unitários e de integração
- Sistema deployado em algum provedor de cloud
- Validações e erros bem estruturados

#### Após o desafio técnico
Em geral, iremos avaliar seu código poucos dias após o envio. Uma vez que nossa
avaliação esteja completa, iremos enviar um feedback sobre sua resolução. Caso
seu código seja aprovado, além do feedback, iremos marcar uma data para uma
conversa por videochamada com você.

#### Conversa pós-entrega
Após a entrega de seu desafio, conversaremos com você sobre a estrutura do seu código e as escolhas feitas por você. Esteja pronta(o) para explicar as decisões que tomou e conversar sobre alternativas. Alguns tópicos nos quais iremos tocar (mas não os únicos) serão: escolha de bancos de dados, estruturas de interfaces, arquitetura de código. Além disso, poderemos mudar as condições do desafio e perguntar o que você teria feito diferentemente.

## Interface

A interface do servidor pode ser realizada através do padrão de API de escolha
do candidato (alguns exemplos são os padrões REST, GraphQL e gRPC), desde que se atenha aos
requisitos especificados aqui.

### Funcionalidades

Independentemente da tecnologia escolhida para realizar a API, a interface exposta
deve permitir - de forma clara - realizar as operações descritas abaixo. Recomendamos documentar como realizar as operações no README do seu projeto para facilitar os testes que realizaremos.

#### Cadastro de conta

Neste endpoint, devem ser enviados os dados de uma conta e ela deve ser cadastrada na base de contas, caso os dados de usuário estejam válidos de acordo com a seção **Regras de negócio**.

#### Autenticação

Neste endpoint, devem ser enviados os dados de login de uma conta já cadastrada.
Esses dados devem ser validados e deve ser retornado um token que será utilizado
para validar transações do usuário. Nos próximos endpoints, o token deve ser
enviado para identificar o usuário logado.

#### Cadastro de transação

Neste endpoint, devem ser enviados os dados de uma transação e ela deve ser
cadastrada na base de transações, caso ela seja feita entre contas válidas e
caso haja saldo suficiente na conta do usuário logado para realização dela.

#### Estorno de transação
**ATENÇÃO**: Caso esteja realizando este teste no nível **Júnior** ou **Pleno**, este endpoint é **opcional**.

Neste endpoint, deve ser enviado o ID de uma transação já cadastrada e os efeitos dessa transação devem ser revertidos, caso seja possível e a transação tenha sido iniciada pelo usuário logado.

#### Busca de transações por data

Neste endpoint, devem ser enviadas datas inicial e final.
O endpoint deve retornar todas as transações realizadas pelo usuário logado entre essas datas em ordem cronológica.

#### Visualização de saldo

Neste endpoint, deve ser visualizado o saldo do usuário logado.

## Regras de negócio

1. Não deve ser possível forjar um token de autenticação. Os tokens devem identificar de forma única o usuário logado.
2. Uma transação só deve ser realizada caso haja saldo suficiente na conta do usuário para realizá-la.
3. Após a realização de uma transação, a conta do usuário enviante deve ter seu valor descontado do valor da transação e a do usuário recebedor acrescentada do valor da transação.
4. Todas as transações realizadas devem ser registradas no banco de dados.
5. Caso todas as transações no banco de dados sejam realizadas novamente a partir do estado inicial de todas as contas, os saldos devem equivaler aos saldos expostos na interface. Em outros termos: Para toda conta, se somarmos os valores de todas as transações no histórico dela a qualquer momento, o saldo total da conta deve ser o saldo atual.
6. Uma transação só pode ser estornada uma vez.

## Entidades

As entidades descritas abaixo são especificações do mínimo de dados necessários para as operações do sistema. Podem ser adicionados outros campos conforme o candidato considere necessário.

### Conta de usuário
Uma conta de usuário precisa no mínimo dos seguintes dados para criação:

- Nome e sobrenome do portador
- CPF do portador
- Saldo inicial

Adicionalmente, a conta deve armazenar no mínimo os seguintes dados:

- Identificador único
- Data de criação

### Transação

Uma transação precisa no mínimo dos seguintes dados para criação:

- Identificador da conta enviante
- Identificador da conta recebedora
- Valor

Adicionalmente, o registro deve conter no mínimo os seguintes dados:

- Data de processamento
- Identificador único
