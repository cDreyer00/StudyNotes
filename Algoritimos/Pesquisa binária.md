# PESQUISA BINARIA:

dado uma LISTA e um TARGET, procura o TARGET na LISTA pegando metade da base de valor MINIMO e MAXIMO atual.
Se encontrar o TARGET, retorna sua posição.
Se não encontrar o TARGET, retonal 'nil'.


**ORDEM LÓGICA**

Ex: 'Lista  = (1, 4, 7, 12, 24)', 'TARGET = 7';
	
	'máximo' = 'tamanhoDaLista';
	'minimo' = 0;
	'valorAtual' = 'tamanhoDaLista' / 2;

	ENQUANTO 'minimo' < 'máximo':
		SE 'Lista(valorAtual)' for igual a 'TARGET':
			retorna 'valorAtual';			
		SE 'Lista(valorAtual)' for menor que 'TARGET':
			'minimo' = valorAtual + 1;
		SE 'Lista(valorAtual)' for maior que 'TARGET':
			'maximo' = valorAtual - 1;

	retorna -1;


O(log n)

#Algoritimos