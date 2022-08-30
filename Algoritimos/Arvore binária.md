# Arvore Binária

[Referencia](http://www.euroinformatica.ro/documentation/programming/!!!Algorithms_CORMEN!!!/DDU0072.html)

conjunto de dados  que se interligam por ramificações, patindo de um ponto principal e se extendendo por camadas.

os dados possiveis de se acessar são os dado minimos, máximos, antepassado, descendente, esquerdo e direito;

![[Pasted image 20220829122458.jpg]]

## Buscar um valor
(só funciona caso a arvore seja ordenada)

para  achar um valor especifico em uma arvore, é dado um ponto inicial de busca e o valor a ser achado e o valor de busca atual. 
Se o valor de busca atual for igual ao valor a ser encontrado dentro da lista de pontos visitados, é enviado de volta o valor de busca atual.
Se o valor de busca atual for menor do que o valor a ser encontrado, continua a busca pela ramificação do lado direita
Se o valor de busca atual for maior do que o valor a ser encontrado, continua a busca pela ramificação do lado esquerdo

**ORDEM LÓGICA:**

Pesquisa('valorInicial', 'valorDeBusca');

	'valorAtual' é igual a 'valorInicial';
	
	SE 'valorAtual' for igual ao 'valorDeBusca':
		retorna 'valorAtual';
	SE 'valorAtual' for menor que o 'valorDeBusca':
		retorna Pesquisa(Direita('valorAtual'), 'valorDeBusca');
	SE 'valorAtual' for maior que o 'valorDeBusca':
		retorna Pesquisa(Esquerda('valorAtual'), 'valorDeBusca');

O(n)

## Achar o ponto initial e  ponto final

Para achar o ponto inicial, é dado um valor inicial de busca, sempre verifica se há um valor descendente  para o lado esquerdo do valor atual. Continue repetindo isso até não haver nenhum valor a esquerda.
Para achar o ponto final é só repetir o mesmo processo mas indo para à direita.

**ORDEM LÓGICA:**

	'valorAtual' = 'valorInicial';
	
	ENQUANTO 'valorAtual' possuir um descendente a sua esquerda:
		'valorAtual' se torna o seu descendente à esquerda;
	
	retorna 'valorAtual';

O(n)

#Algoritimo