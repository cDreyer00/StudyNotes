# Exercício 1: Plurality

Implemente um programa que execute uma eleição de pluralidade, conforme a seguir.

$ ./plurality Alice Bob Charlie  
Número de eleitores: 4  
Voto: Alice  
Voto: Bob  
Voto: Charlie  
Voto: Alice  
Alice

## Background

As eleições acontecem em todas as formas e tamanhos. No Reino Unido, o [primeiro-ministro](https://www.parliament.uk/about/how/elections-and-voting/general/) é oficialmente nomeado pelo monarca, que geralmente escolhe o líder do partido político que obtém mais cadeiras na Câmara dos Comuns. Os Estados Unidos usam um processo de [Colégio Eleitoral](https://www.archives.gov/electoral-college/about) de várias etapas , no qual os cidadãos votam em como cada estado deve alocar os Eleitores que então elegem o Presidente.

Talvez a maneira mais simples de realizar uma eleição, no entanto, seja por meio de um método comumente conhecido como “voto plural” (também conhecido como “primeiro a chegar” ou “o vencedor leva tudo”). Na votação por pluralidade, cada eleitor pode votar em um candidato. No final da eleição, o candidato que obtiver o maior número de votos é declarado vencedor da eleição.

## Vamos começar!

Veja como baixar o “código de distribuição” desse problema (ou seja, código inicial) em seu próprio CS50 IDE. Faça login no [**CS50 IDE**](https://ide.cs50.io/) e, em uma janela de terminal, execute cada um dos itens abaixo.

-   Execute cd ~ (ou simplesmente **cd** sem argumentos) para garantir que você está no seu diretório pessoal).
-   Execute mkdir pset3 para fazer (ou seja, criar) um diretório chamado **pset3** .
-   Execute cd pset3 para mudar para (ou seja, abrir) esse diretório.
-   Execute mkdir plurality para fazer (ou seja, criar) um diretório chamado **plurality** em seu diretório **pset3** .
-   Execute cd plurality para mudar para (isto é, abrir) esse diretório.
-   Execute wget https://cdn.cs50.net/2020/fall/psets/3/plurality/plurality.c para baixar o código de distribuição deste problema.
-   Execute ls . Você deve ver o código de distribuição deste problema, em um arquivo chamado **plurality.c** .

## **Entendendo...**

### Este vídeo irá te ajudar a entender o problema ;)

**Atenção:** _para adicionar legendas ao vídeo clique no botão CC localizado no Player e selecione a opção "Português (Brasil)"._

Vamos agora dar uma olhada em  **plurality.c**  e ler o código de distribuição que foi fornecido a você.

A linha **#define MAX 9** é alguma sintaxe usada aqui para significar que **MAX** é uma constante (igual a **9**) que pode ser usada em todo o programa. Aqui, ele representa o número máximo de candidatos que uma eleição pode ter.

O arquivo então define uma **struct** chamada **candidate** . Cada **candidate** tem dois campos: uma **string** chamada **name** representando o nome do candidato e um **int** chamado **votes** representando o número de votos que o candidato possui. Em seguida, o arquivo define uma matriz global de **candidates** , em que cada elemento é ele próprio um **candidate** .

Agora, dê uma olhada na própria função **main** . Veja se você consegue descobrir onde o programa define uma variável global **candidate_count** representando o número de candidatos na eleição, copia os argumentos da linha de comando para a vetor **candidates** e pede ao usuário para digitar o número de eleitores. Em seguida, o programa permite que cada eleitor digite um voto (entendeu como?), acionando a função de **vote** em cada candidato votado. Finalmente, main faz uma chamada para a função **print_winner** para imprimir o vencedor (ou vencedores) da eleição.

Se você olhar mais abaixo no arquivo, no entanto, notará que as funções **vote** e **print_winner** foram deixadas em branco. Esta parte depende de você concluir!

## Especificações

Complete a implementação de plurality.c de tal forma que o programa simule uma eleição de voto plural.

-   Complete a função de **vote**.
    -   **vote** leva um único argumento, uma **string** chamada **name** , que representa o nome do candidato que foi votado.
    -   Se o **name** corresponder a um dos nomes dos candidatos na eleição, atualize o total de votos desse candidato para contabilizar a nova votação. A função de votação(**vote**) neste caso deve retornar **true** para indicar uma votação bem-sucedida.
    -   Se o **name** não corresponder ao nome de nenhum dos candidatos na eleição, nenhum total de votos deve mudar e a função de voto(**vote**) deve retornar **false** para indicar uma cédula inválida.
    -   Você pode presumir que dois candidatos não terão o mesmo nome.
-   Conclua a função **print_winner** .
    -   A função deve imprimir o nome do candidato que recebeu mais votos na eleição e, em seguida, imprimir uma nova linha.
    -   É possível que a eleição termine em empate se vários candidatos tiverem, cada um, o número máximo de votos. Nesse caso, você deve imprimir os nomes de cada um dos candidatos vencedores, cada um em uma linha separada.

Você não deve modificar nada mais em plurality.c além das implementações das funções **vote** e **print_winner** (e a inclusão de arquivos de cabeçalho adicionais, se desejar).

## **Uso**

Seu programa deve se comportar de acordo com os exemplos abaixo.

-   $ ./plurality Alice Bob  
    Number of voters: 3  
    Vote: Alice  
    Vote: Bob  
    Vote: Alice  
    Alice
-   $ ./plurality Alice Bob  
    Number of voters: 3  
    Vote: Alice  
    Vote: Charlie  
    Invalid vote.  
    Vote: Alice  
    Alice
-   $ ./plurality Alice Bob Charlie  
    Number of voters: 5  
    Vote: Alice  
    Vote: Charlie  
    Vote: Bob  
    Vote: Bob  
    Vote: Alice  
    Alice  
    Bob


---

# Exercício 2: Runoff

**[VÍDEO](https://www.youtube.com/watch?v=V2LVq_yNPss&feature=emb_imp_woyt&ab_channel=Funda%C3%A7%C3%A3oEstudar)**

Implemente um programa que execute uma eleição de segundo turno, conforme a seguir.

	./runoff Alice Bob Charlie  
	Número de eleitores: 5  
	Rank 1: Alice  
	Rank 2: Bob  
	Rank 3: Charlie  
  
	Rank 1: Alice  
	Rank 2: Charlie  
	Rank 3: Bob  
 
	Rank 1: Bob  
	Rank 2: Charlie  
	Rank 3: Alice  

	Rank 1: Bob  
	Rank 2: Alice  
	Rank 3: Charlie  
  
	Rank 1: Charlie  
	Rank 2: Alice  
	Rank 3: Bob  

	Alice

## Background

Você já conhece as eleições pluralistas, que seguem um algoritmo muito simples para determinar o vencedor de uma eleição: cada eleitor ganha um voto e o candidato com mais votos vence.

Mas o voto de pluralidade tem algumas desvantagens. O que acontece, por exemplo, em uma eleição com três candidatos, e as cédulas abaixo são lançadas?

![Exemplo do exercício](https://cs50.harvard.edu/x/2021/psets/3/fptp_ballot_1.png)

Uma votação de pluralidade declararia aqui um empate entre Alice e Bob, uma vez que cada um tem dois votos. Mas esse é o resultado certo?

Existe outro tipo de sistema de votação conhecido como sistema de votação por escolha ranqueada. Em um sistema de escolha ranqueada, os eleitores podem votar em mais de um candidato. Em vez de apenas votar na primeira escolha, eles podem classificar os candidatos em ordem de preferência. As cédulas resultantes podem, portanto, ser semelhantes às apresentadas a seguir.

 ![Exemplo do exercício](https://cs50.harvard.edu/x/2021/psets/3/ranked_ballot_1.png)

Aqui, cada eleitor, além de especificar seu primeiro candidato preferencial, também indicou sua segunda e terceira opções. E agora, o que antes era uma eleição empatada, agora pode ter um vencedor. A corrida foi originalmente empatada entre Alice e Bob, então Charlie estava fora da corrida. Mas o eleitor que escolheu Charlie preferiu Alice a Bob, então Alice poderia ser declarada vencedora.

A votação por escolha ranqueada também pode resolver outra desvantagem potencial da votação por pluralidade. Dê uma olhada nas seguintes cédulas.

 ![Exemplo do exercício](https://cs50.harvard.edu/x/2021/psets/3/ranked_ballot_3.png)

Quem deve ganhar esta eleição? Em uma votação de pluralidade em que cada eleitor escolhe apenas sua primeira preferência, Charlie vence esta eleição com quatro votos, em comparação com apenas três para Bob e dois para Alice. Mas a maioria dos eleitores (5 de 9) ficaria mais feliz com Alice ou Bob em vez de Charlie. Ao considerar as preferências ranqueadas, um sistema de votação pode ser capaz de escolher um vencedor que reflita melhor as preferências dos eleitores.

Uma dessas opções de sistema de votação por classificação é o sistema de runoff instantâneo (ou uma eleição com turnos). Em uma eleição de runoff instantâneo, os eleitores podem rankear quantos candidatos quiserem. Se algum candidato tiver a maioria (mais de 50%) dos votos da primeira preferência, esse candidato é declarado vencedor da eleição.

Se nenhum candidato tiver mais de 50% dos votos, ocorre um “runoff instantaneo”. O candidato que recebeu o menor número de votos é eliminado da eleição, e quem originalmente escolheu esse candidato como sua primeira preferência agora tem sua segunda preferência considerada. Por que fazer assim? Efetivamente, isso simula o que teria acontecido se o candidato menos popular não tivesse estado na eleição para começar.

O processo repete-se: se nenhum candidato obtiver a maioria dos votos, o último candidato colocado é eliminado e quem votou nele votará na sua próxima preferência (os que ainda não foram eliminados). Uma vez que um candidato tenha a maioria, ele é declarado o vencedor.

Vamos considerar as nove cédulas acima e examinar como ocorreria uma eleição com turnos.

Alice tem dois votos, Bob tem três votos e Charlie tem quatro votos. Para ganhar uma eleição com nove pessoas, é necessária uma maioria (cinco votos). Como ninguém tem maioria, é necessário realizar um segundo turno. Alice tem o menor número de votos (com apenas dois), então Alice é eliminada. Os eleitores que votaram originalmente em Alice listaram Bob como segunda preferência, então Bob obtém os dois votos extras. Bob agora tem cinco votos e Charlie ainda tem quatro votos. Bob agora tem a maioria e Bob é declarado o vencedor.

Que casos extremos precisamos considerar aqui?

Uma possibilidade é que haja um empate para quem deve ser eliminado. Podemos lidar com esse cenário dizendo que todos os candidatos que estão empatados no último lugar serão eliminados. Se todos os candidatos restantes tiverem exatamente o mesmo número de votos, porém, eliminar os candidatos empatados em último lugar significa eliminar todos! Então, nesse caso, teremos que ter cuidado para não eliminar todos, e apenas declarar a eleição um empate entre todos os candidatos restantes.

Algumas eleições de runoff instantâneo não exigem que os eleitores classifiquem todas as suas preferências - portanto, pode haver cinco candidatos em uma eleição, mas um eleitor pode escolher apenas dois. Para os fins deste problema, entretanto, vamos ignorar esse caso particular e presumir que todos os eleitores classificarão todos os candidatos em sua ordem preferida.

Parece um pouco mais complicado do que uma votação plural, não é? Mas pode-se argumentar que tem a vantagem de ser um sistema eleitoral em que o vencedor da eleição representa com mais precisão as preferências dos eleitores.

---

# Exercício 3: Tideman

**[VIDEO](https://www.youtube.com/watch?v=bwlFwoWH3hM&ab_channel=Funda%C3%A7%C3%A3oEstudar)**

Implemente um programa que execute uma eleição Tideman (ou eleição de pares ranqueados), conforme a seguir.

	./tideman Alice Bob Charlie  
	Número de eleitores: 5  
	Rank 1: Alice  
	Rank 2: Charlie  
	Rank 3: Bob  
	  
	Rank 1: Alice  
	Rank 2: Charlie  
	Rank 3: Bob  
	  
	Rank 1: Bob  
	Rank 2: Charlie  
	Rank 3: Alice  
	  
	Rank 1: Bob  
	Rank 2: Charlie  
	Rank 3: Alice  
	  
	Rank 1: Charlie  
	Rank 2: Alice  
	Rank 3: Bob  
	  
	Charlie

## Background

Você já conhece as eleições pluralistas, que seguem um algoritmo muito simples para determinar o vencedor de uma eleição: cada eleitor ganha um voto e o candidato com mais votos vence.

Mas o voto de pluralidade tem algumas desvantagens. O que acontece, por exemplo, em uma eleição com três candidatos, e as cédulas abaixo são lançadas?

![Exemplo do exercício](https://cs50.harvard.edu/x/2021/psets/3/fptp_ballot_1.png)

Uma votação de pluralidade declararia aqui um empate entre Alice e Bob, uma vez que cada um tem dois votos. Mas esse é o resultado certo?

Existe outro tipo de sistema de votação conhecido como sistema de votação por escolha ranqueada. Em um sistema de escolha ranqueada, os eleitores podem votar em mais de um candidato. Em vez de apenas votar na primeira escolha, eles podem classificar os candidatos em ordem de preferência. As cédulas resultantes podem, portanto, ser semelhantes às apresentadas a seguir.

![Exemplo do exercício](https://cs50.harvard.edu/x/2021/psets/3/ranked_ballot_1.png)

Aqui, cada eleitor, além de especificar seu primeiro candidato preferencial, também indicou sua segunda e terceira opções. E agora, o que antes era uma eleição empatada, agora pode ter um vencedor. A corrida foi originalmente empatada entre Alice e Bob, então Charlie estava fora da corrida. Mas o eleitor que escolheu Charlie preferiu Alice a Bob, então Alice poderia ser declarada vencedora.

A votação por escolha ranqueada também pode resolver outra desvantagem potencial da votação por pluralidade. Dê uma olhada nas seguintes cédulas.

![Exemplo do exercício](https://cs50.harvard.edu/x/2021/psets/3/condorcet_1.png)

Quem deve ganhar esta eleição? Em uma votação de pluralidade em que cada eleitor escolhe apenas sua primeira preferência, Charlie vence a eleição com quatro votos, em comparação com apenas três para Bob e dois para Alice. (Observe que, se você estiver familiarizado com o sistema de runoff instantâneo,ou eleição em turnos, Charlie também vence nesse sistema). Alice, no entanto, pode razoavelmente argumentar que ela deveria ser a vencedora da eleição em vez de Charlie: afinal, dos nove eleitores, a maioria (cinco deles) preferia Alice a Charlie, então a maioria das pessoas ficaria mais feliz com Alice como o vencedor em vez de Charlie.

Alice é, nesta eleição, a chamada “vencedora Condorcet” da eleição: a pessoa que teria vencido qualquer confronto direto com outro candidato. Se a eleição tivesse sido apenas Alice e Bob, ou apenas Alice e Charlie, Alice teria vencido.

O método de votação Tideman (também conhecido como “pares ranqueados”) é um método de votação de escolha ranqueada que garante o vencedor da eleição de Condorcet, se houver.

De modo geral, o método Tideman funciona construindo um “gráfico” de candidatos, onde uma seta (isto é, aresta) do candidato A ao candidato B indica que o candidato A vence o candidato B em um confronto direto. O gráfico para a eleição acima, então, seria parecido com o abaixo.

![Exemplo do exercício](https://cs50.harvard.edu/x/2021/psets/3/condorcet_graph_1.png)

A seta de Alice para Bob significa que mais eleitores preferem Alice a Bob (5 preferem Alice, 4 preferem Bob). Da mesma forma, as outras setas significam que mais eleitores preferem Alice a Charlie e mais eleitores preferem Charlie a Bob.

Olhando para este gráfico, o método Tideman diz que o vencedor da eleição deve ser a “fonte” do gráfico (ou seja, o candidato que não tem uma seta apontando para ele). Nesse caso, a fonte é Alice - Alice é a única que não tem uma seta apontando para ela, o que significa que ninguém é preferido frente a frente com a Alice. Alice é, portanto, declarada a vencedora da eleição.

É possível, entretanto, que quando as flechas forem puxadas, não haja um vencedor Condorcet. Considere as cédulas abaixo.

![Exemplo do exercício](https://cs50.harvard.edu/x/2021/psets/3/no_condorcet_1.png)

Entre Alice e Bob, Alice tem preferência sobre Bob por uma margem de 7-2. Entre Bob e Charlie, Bob é o preferido em relação a Charlie por uma margem de 5-4. Mas entre Charlie e Alice, Charlie é o preferido a Alice por uma margem de 6-3. Se desenharmos o gráfico, não haverá fonte! Temos um ciclo de candidatos, onde Alice vence Bob que vence Charlie que vence Alice (muito parecido com um jogo de pedra-papel-tesoura). Nesse caso, parece que não há como escolher um vencedor.

Para lidar com isso, o algoritmo Tideman deve ser cuidadoso para evitar a criação de ciclos no gráfico candidato. Como é feito isso? O algoritmo “bloqueia” as setas mais “fortes” primeiro, uma vez que essas são, sem dúvida, as mais significativas. Em particular, o algoritmo do Tideman especifica que as setas de cada “duelo” devem ser "travadas" no gráfico, uma de cada vez, com base na "força" da vitória (quanto mais pessoas preferirem um candidato ao adversário, mais forte será a vitória) . Desde que a aresta possa ser travada no gráfico sem criar um ciclo, a aresta é adicionada; caso contrário,é ignorada.

Como isso funcionaria no caso dos votos acima? Bem, a maior margem de vitória para um par é Alice derrotando Bob, já que 7 eleitores preferem Alice a Bob (nenhuma outra disputa direta tem um vencedor preferido por mais de 7 eleitores). Portanto, a seta Alice-Bob é travada no gráfico primeiro. A próxima maior margem de vitória é a vitória de Charlie por 6-3 sobre Alice, de modo que a flecha é a próxima.

A seguir vem a vitória de Bob por 5-4 sobre Charlie. Mas observe: se adicionássemos uma flecha de Bob a Charlie agora, criaríamos um ciclo! Uma vez que o gráfico não permite ciclos, devemos pular esta borda e não adicioná-la ao gráfico. Se houvesse mais setas a serem consideradas, olharíamos para as próximas, mas essa foi a última seta, então o gráfico está completo.

Este processo passo a passo é mostrado abaixo, com o gráfico final à direita.

![Exemplo do exercício](https://cs50.harvard.edu/x/2021/psets/3/lockin.png)

Com base no gráfico resultante, Charlie é a fonte (não há nenhuma seta apontando para Charlie), então Charlie é declarado o vencedor desta eleição.

Colocado de forma mais formal, o método de votação do Tideman consiste em três partes:

-   **Contagem/Tally**: Uma vez que todos os eleitores indicaram todas as suas preferências, determine, para cada par de candidatos, quem é o candidato preferido e com que margem ele é preferido.
-   **Classificação/Ordenação/Sort** : Classifique os pares de candidatos em ordem decrescente de força de vitória, onde a força de vitória é definida pelo número de eleitores que preferem o candidato preferido.
-   **Decisão/Lock**: começando com o par mais forte, passe pelos pares de candidatos em ordem e “trave” cada par no gráfico candidato, contanto que travar nesse par não crie um ciclo no gráfico.

Assim que o gráfico estiver completo, a fonte do gráfico (aquela sem arestas apontando para ele) é a vencedora!