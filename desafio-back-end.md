# Desafio de Programação Back-End
Olá e muitíssimo obrigado pelo interesse na UmHelp! Somos uma startup em rápido
crescimento, e sempre buscamos pessoas boas para compor nossa equipe de
tecnologia. Esperamos ter você a bordo conosco em breve!

Pedimos que leia este documento **inteiro** com atenção para maximizar suas
chances de sucesso.

O teste que você irá realizar consiste em elaborar 3 **microsserviços** que
possibilitam o agendamento de serviços de limpeza por parte de um usuário, com
a possibilidade de aplicação de descontos promocionais. Os serviços deverão
expor, publicamente, uma **interface REST** que deve ser provida pelo serviço
de _gateway_, conforme abaixo descrito. Não deve ser elaborado um front-end
web ou de outro formato.

## Sobre este documento
- O processo de envio da sua solução e os critérios que serão avaliados pela
equipe de tecnologia da UmHelp estão descritos abaixo, na seção **Avaliação**.
- As regras que o sistema deve seguir estão descritas na seção **Regras de
Negócio**.
- Algumas restrições adicionais estão descritas na seção **Restrições**.
- A interface que cada microsserviço deve expor está descrita na seção **Serviços**.
- As descrições de interfaces ocasionalmente referenciam entidades descritas na seção **Entidades**.

Caso não tenha certeza sobre qualquer coisa explicada neste documento (ou
qualquer dúvida em geral), fique à vontade para enviar um email para
pedrocastilho@da1help.com com suas dúvidas.

## Avaliação
Seu desafio deverá ser disponibilizado por meio de um repositório Git
(podendo este ser hosteado da forma que for mais conveniente a você, por
exemplo usando uma plataforma como GitHub ou GitLab). A única restrição é que
o repositório deve ser acessível à equipe da UmHelp. Caso não queira
disponibilizar seu código publicamente, converse conosco sobre como podemos
fazer para obter acesso a seu código.

### Critérios
Uma vez que ele seja disponibilizado a nós, a avaliação de seu código será feita de acordo com os seguintes critérios, em ordem aproximada de importância:

#### Ausência de bugs
Seu código deve funcionar corretamente, atendendo a todos os requisitos da especificação representada por este documento

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

#### Arquitetura Orientada a Serviços
Busque informar-se sobre boas práticas de Arquitetura Orientada a Serviços e
usá-las. Seu sistema deve ser robusto quando visto como um todo coerente.
Busque lembrar que em uma AOS, não é possível assumir que qualquer outro
serviço esteja em um estado válido. Pense em casos excepcionais e busque lidar
com eles tanto quanto possível.

#### Opcionais
Os pontos a seguir são opcionais, mas apreciamos vê-los:
- Testes unitários e de integração
- Sistema deployado em algum provedor de cloud
- Validações e erros bem estruturados

#### Após o desafio técnico
Em geral, iremos avaliar seu código poucos dias após o envio. Uma vez que nossa
avaliação esteja completa, iremos enviar um feedback sobre sua resolução. Caso
seu código seja aprovado, além do feedback, iremos marcar uma data para uma
entrevista presencial ou uma conversa por videochamada com você.

#### Entrevista presencial
Na entrevista presencial, conversaremos com você sobre a estrutura do seu código e as escolhas feitas por você. Esteja pronta(o) para explicar as decisões que tomou e conversar sobre alternativas. Alguns tópicos nos quais iremos tocar (mas não os únicos) serão: escolha de bancos de dados, estruturas de interfaces, arquitetura de código. Além disso, poderemos mudar as condições do desafio e perguntar o que você teria feito diferentemente.

## Regras de negócio

1. Uma vez que um pedido de limpeza é cadastrado, se um desconto foi utilizado, o desconto deve ser consumido (removido da base de descontos). Portanto, o mesmo desconto não deve ser aplicado mais de uma vez.
2. Descontos não devem ser consumidos quando um preço é apenas visualizado.
3. Se um usuário tiver múltiplos descontos cadastrados, o desconto que resulte no menor preço total deve ser aplicado ao pedido de limpeza dele.
4. Uma vez que um pedido de limpeza seja registrado, ele deve ser persistido indefinidamente.
5. O preço base de um serviço de limpeza (sem aplicação de nenhum desconto) deve ser considerado como sendo de R$ 50 por hora.

## Restrições

1. Os serviços devem usar ao menos 2 linguagens de programação diferentes.
2. Os serviços podem usar um único banco de dados compartilhado, ou bancos de dados separados. Lembre que essa decisão também será questionada.

## Serviços
A comunicação entre os serviços pode ser feita usando qualquer padrão de comunicação que você deseje. Lembre-se apenas que você terá que justificar
suas escolhas durante a entrevista técnica. É recomendado pesquisar sobre padrões de comunicação entre microsserviços para realizar essa escolha.

### Serviço 1: Gateway
Esse serviço deve expor uma interface REST pública, com os seguintes
_endpoints_:

- **GET** `/price`:
  Recebe a especificação de um pedido de limpeza (conforme descrita na seção
  **Entidades**) e retorna o preço de um pedido de limpeza para o usuário
  especificado, sem registrar o serviço e sem consumir descontos.

- **POST** `/requests`:
  Cadastra um novo pedido de limpeza com os parâmetros passados. Retorna os
  dados do pedido, incluindo o preço final.

- **GET** `/requests`:
  Retorna todos os pedidos de limpeza atualmente cadastrados.

- **POST** `/discounts`:
  Cadastra um novo desconto.

Além dos verbos já especificados, os verbos **PUT**, **PATCH** e **DELETE**
também devem ser implemntados para os endpoints `/requests` e `/discounts`, com
comportamento de acordo com a semântica padrão REST.
Adicionalmente, deve ser possível acessar os pedidos de limpeza individualmente
através do uso de um identificados. Outros endpoints ou verbos podem ser
criados caso você julgue necessário, mas tenha em mente os requisitos de segurança da aplicação!
O serviço _gateway_ deve realizar suas funcionalidades através de comunicação
com os outros serviços, descritos a seguir:

### Serviço 2: Pedidos de limpeza
Este serviço deve receber requisições de pedidos de limpeza a partir do serviço gateway e calcular os dados que não serão dados no pedido (em especial, o preço do pedido, levando em consideração a aplicação de desconto, caso exista desconto cadastrado no serviço 3. Este serviço também deve ser responsável pelo cadastro persistente de pedidos de limpeza.

### Serviço 3: Descontos individuais
ste serviço será responsável por cadastrar descontos individuais. Além disso, ele será consultado pelo serviço 2, que o usará para determinar a existência ou não de descontos. Além disso, quando um pedido de limpeza for cadastrado, este serviço será responsável por garantir que a regra 1 seja respeitada.

## Entidades

### Pedido de limpeza
Um pedido de limpeza deve conter, ao menos, as seguintes informações:
- Data do pedido
- Duração da limpeza
- Identificação do usuário solicitante

### Desconto
Um desconto deve conter, ao menos, as seguintes informações:
- Tipo do desconto (valor absoluto ou porcentagem)
- Valor do desconto
- Identificação do usuário que tem direito ao desconto
