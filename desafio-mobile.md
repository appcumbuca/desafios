# Desafio de Programação Mobile
Olá e muitíssimo obrigada pelo interesse na Cumbuca! Somos uma startup em
rápido crescimento, e sempre buscamos pessoas boas para compor nossa equipe de
tecnologia. Esperamos ter você a bordo com a gente em breve!

Pedimos que leia este documento **inteiro** com atenção para maximizar suas
chances de sucesso.

O teste que você irá realizar consiste em elaborar uma interface que irá
permitir que a pessoa usuária edite uma lista de produtos. Essa implementação deve ser feita **Como um aplicativo móvel híbrido**, utilizando **React Native**. Fique a vontade para utilizar o [Expo](https://expo.io/) ou a CLI do React Native, como descrito na [documentação](https://reactnative.dev/docs/environment-setup).

## Sobre este documento
- O processo de envio da sua solução e os critérios que serão avaliados pela equipe de tecnologia da Cumbuca estão descritos na seção **Avaliação**.
- As regras que o sistema deve seguir estão descritas na seção **Regras de negócio**.
- Algumas restrições adicionais estão descritas na seção **Restrições**.
- A interface a ser implementada está descrita na seção **Interface**.
- A descrição de interface referencia entidades descritas na seção **Entidades**.

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
Seu código deve funcionar corretamente, atendendo a todos os requisitos da especificação representada por este documento.

#### Responsividade
A sua interface deve adaptar-se a dispositivos e tamanhos de tela distintos, independente do dispositivos utilizado para acessar o conteúdo, apresentando uma interface adequada a cada tamanho de tela.

#### Reatividade
A sua interface deve reagir aos inputs do usuário sem que haja delay percebido por ele, mesmo em dispositivos não tão poderosos.

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
Seu código não deve criar dependências desnecessárias entre módulos e serviços.
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

#### Testes
**ATENÇÃO**: Caso esteja realizando este teste no nível **Júnior**, a presença de testes é opcional. Para os níveis **Pleno** e **Sênior**, testes são **obrigatórios**.

Esperamos que o código esteja testado de forma a validar as regras de negócio aqui descritas e o funcionamento correto do código.

#### Após o desafio técnico
Em geral, iremos avaliar seu código poucos dias após o envio. Uma vez que nossa
avaliação esteja completa, iremos enviar um feedback sobre sua resolução. Caso
seu código seja aprovado, além do feedback, iremos marcar uma data para uma
conversa por videochamada com você.

#### Conversa pós-entrega
Após a entrega de seu desafio, conversaremos com você sobre a estrutura do seu código e as escolhas feitas por você. Esteja pronta(o) para explicar as decisões que tomou e conversar sobre alternativas. Alguns tópicos nos quais iremos tocar (mas não os únicos) serão: estruturas de interfaces, arquitetura de código, escolha de mecanismos de gestão de estado e de persistência, etc. Além disso, poderemos mudar as condições do desafio e perguntar o que você teria feito diferentemente.

## Regras de negócio
1.A entrada no aplicativo desafio deverá conter um login e senha (CPF + senha de no mínimo 8 dígitos), o qual deverá ocorrer o cadastro na primeira entrada e depois deverá conferir usuário e senha. O CPF deverá ser validado e caso não confira o DV, deverá ser informado o erro. Caso a senha não esteja correta, deverá ser informado o erro.

2. Uma vez que a lista de produtos é modificada, a alteração deve ser localmente persistida. Isto é, se o usuário sair do aplicativo, a lista de produtos na qual ele estava trabalhando deve continuar como estava antes da atualização.
3. Uma vez que seja inserido texto na barra de busca, a lista de produtos deve exibir apenas os produtos cujo nome corresponda (total ou parcialmente) ao texto inserido na barra. Isso não deve afetar a lista de produtos, afetando apenas quais produtos da lista são exibidos.
4. O id do produto não deve ser fornecido através de campo: Ao invés disso, o produto deve receber um id sequencial, iniciando em 1.
5. Caso o usuário tente criar um produto e os inputs nos campos do formulário de input não corresponderem aos tipos especificados na entidade Produto, deve ser exibido um erro.
6. Caso o usuário tente criar um produto com 0 unidades em estoque, deve ser exibido um erro.
7. Caso a quantidade de unidades em estoque de um produto seja alterada para 0, o produto deve ser excluído.
8. O valor total do produto não deve ser fornecido através de campo: Ao invés disso, ele deve ser determinado multiplicando o valor unitário do produto pela quantidade de unidades em estoque. Caso a quantidade de unidades em estoque seja alterada, o valor total do produto deve ser alterado correspondentemente.
9. Caso um produto seja excluído, o id dele deve ser reutilizado para novos produtos adicionados. Segue um exemplo:
  - Usuário cria  4 produtos (IDs 1, 2, 3, e 4)
  - Usuário deleta produtos 2 e 3
  - Usuário cadastra novo produto. Esse produto deve receber o ID 2 (e não 5)
  - Usuário cadastra novo produto. Esse produto deve receber o ID 3 (e não 6)
  - Usuário cadastra novo produto. Esse produto deve receber o id 5 (e não 7)

## Restrições
1. Tente utilizar o mínimo de biliotecas possíveis. De preferência, apenas as bibliotecas necessárias para inicializar o projeto (dependências do Expo e/ou React Native).

Aqui, "bibliotecas" são definidas como código pronto que seja incluso no
output que será enviado ao cliente. Ferramentas que sejam usadas apenas
pelo desenvolvedor como minificadores ou pré-processadores ainda são
permitidas.


## Interface
Os detalhes gráficos da interface não serão especificados por nós. Você pode implementar a interface como desejar - apenas atente-se às consequências de usabilidade de suas escolhas. Segue a descrição funcional da interface a ser implementada:

A primeira tela de entrada do aplicativo deverá conter o Login ou permitir diretamente a entrada por biometria/identificação facial.

Após o login a segunda tela dever possui:

No topo da interface, deve haver uma barra de busca que permita a inserção de texto, e um pequeno indicador de menu para uma segunda tela de opções.

Imediatamente abaixo da barra de texto, deve haver uma série de campos que permitam a especificação de um produto (conforme a entidade **Produto** descrita na seção **Entidades**). Junto a esses campos deve haver um botão que permita a criação de um produto de acordo com os inputs especificados nos campos (Exceto o identificador e o valor total, que será atribuído aos produtos criados conforme especificado na seção **Regras de Negócio**). Os campos e botão serão referidos doravante como o “formulário de input”.

Abaixo do formulário de input, deve haver uma lista dos produtos inseridos. Essa lista deve ter um cabeçalho com o nome de cada campo do produto. Ao clicar em um campo no cabeçalho, a lista deve ser ordenada de acordo com aquele campo.

Cada item deve:
- exibir os dados de um produto
- exibir um controle que permita incrementar ou decrementar a quantidade em estoque daquele item
- exibir um controle que permita a remoção daquele item

Caso esteja realizando este teste no nível **Pleno** ou **Sênior**, os itens devem poder ser reordenados através de “arrastar e soltar” (_drag-and-drop_).

A segunda tela de opções deverá conter:

- Opção para troca para **Dark Mode**
- Habilitar/Desabilitar login por biometria/identificação facial, dependendo do aparelho.
- Deverá existir no tipo da tela uma seta visando retornar a tela principal.


## Entidades

### Login
O login deve consistir das seguintes informações:
- CPF
- Senha (não precisa ser critografada)
- Data do último acesso

### Produto
O produto deve consistir das seguinte informações:
- Identificador (número)
- Nome (string)
- Quantidade em estoque (número)
- Valor unitário (número)
- Valor total (número)
