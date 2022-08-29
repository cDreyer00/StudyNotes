# Arvore binária

[Referencia](http://www.euroinformatica.ro/documentation/programming/!!!Algorithms_CORMEN!!!/DDU0072.html)

conjunto de dados  que se interligam por ramificações, patindo de um ponto principal e se extendendo por camadas.

cada dado geralmente tem acesso ao dado minimo, maximo, anterior e sucessor, alguns apenas ao dado sucessor.

![[Pasted image 20220828180751.jpg]]

## Buscar um valor

para  achar um valor especifico em uma arvore, é dado um ponto inicial de busca e o valor a ser achado e o valor de busca atual. 
Se o valor de busca atual for igual ao valor a ser encontrado dentro da lista de pontos visitados, é enviado de volta o valor de busca atual.
Se o valor de busca atual for menor do que o valor a ser encontrado, continua a busca pela ramificação do lado direita
Se o valor de busca atual for maior do que o valor a ser encontrado, continua a busca pela ramificação do lado esquerdo

ORDEM LÓGICA:

Pesquisa('valorInicial', 'valorDeBusca');

	'valorAtual' é igual a 'valorInitial';
	
	SE 'valorAtual' for igual ao 'valorDeBusca':
		retorna 'valorAtual';
	SE 'valorAtual' for menor que o 'valorDeBusca':
		retorna Pesquisa(Direita('valorAtual'), 'valorDeBusca');
	SE 'valorAtual' for maior que o 'valorDeBusca':
		retorna Pesquisa(Esquerda('valorAtual'), 'valorDeBusca');


## Achar o valor minimo e máximo

Para achar o valor minimo, é dado um valor inicial de busca, sempre verifica se há um valor antecessor (esquerda) do valor atual. Continue repetindo isso até não haver nenhum valor a esquerda.
Para achar o valor máximo é só repetir o mesmo processo mas indo para à direita (valores sucessores).

ORDEM LÓGICA:	

	'valorAtual' = 'valorInicial';
	
	ENQUANTO 'valorAtual' possuir um valor a sua esquerda:
		'valorAtual' se torna seu valor a esquerda;
	
	retorna 'valorAtual';


#Algoritimos 