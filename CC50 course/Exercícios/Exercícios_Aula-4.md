# Exercício 1: Filter
**[VIDEO](https://www.youtube.com/watch?v=ZFZYkpi_sic&list=PLOqY1R7P7NS-i9xZLcRSHcORsklxoRmWG&ab_channel=Funda%C3%A7%C3%A3oEstudar)**

Implemente um programa que aplique filtros a BMPs, conforme a seguir.

$ ./filter -r image.bmp reflected.bmp

## **Background**

## Bitmaps

Talvez a maneira mais simples de representar uma imagem seja com uma grade de pixels (ou seja, pontos), cada um dos quais pode ser de uma cor diferente. Para imagens em preto e branco, precisamos, portanto, de 1 bit por pixel, já que 0 pode representar preto e 1 pode representar branco, como mostrado a seguir.

![](https://cs50.harvard.edu/x/2021/psets/4/filter/more/bitmap.png)

Nesse sentido, então, uma imagem é apenas um bitmap (ou seja, um mapa de bits). Para imagens mais coloridas, você simplesmente precisa de mais bits por pixel. Um formato de arquivo (como BMP , JPEG ou PNG ) que suporta “cores de 24 bits” usa 24 bits por pixel. (BMP, na verdade, suporta cores de 1, 4, 8, 16, 24 e 32 bits.)

Um BMP de 24 bits usa 8 bits para significar a quantidade de vermelho na cor de um pixel, 8 bits para significar a quantidade de verde na cor de um pixel e 8 bits para significar a quantidade de azul na cor de um pixel. Se você já ouviu falar em cores RGB, bem, aí está: vermelho, verde, azul.

Se os valores R, G e B de algum pixel em um BMP são, digamos, 0xff , 0x00 e 0x00 em hexadecimal, esse pixel é puramente vermelho, pois 0xff (também conhecido como 255 em decimal) implica "muito vermelho , ”Enquanto 0x00 e 0x00 implicam“ sem verde ”e“ sem azul ”, respectivamente.

## Um Bit(map) Mais Técnico

Lembre-se de que um arquivo é apenas uma sequência de bits, organizados de alguma forma. Um arquivo BMP de 24 bits, então, é essencialmente apenas uma sequência de bits, (quase) cada 24 dos quais representam a cor de algum pixel. Mas um arquivo BMP também contém alguns “metadados”, informações como a altura e largura de uma imagem. Esses metadados são armazenados no início do arquivo na forma de duas estruturas de dados geralmente chamadas de “cabeçalhos”, não devem ser confundidos com os arquivos de cabeçalho de C. (Aliás, esses cabeçalhos evoluíram com o tempo. Esse problema usa a versão mais recente do formato BMP da Microsoft, 4.0, que estreou com o Windows 95.)

O primeiro desses cabeçalhos, chamado BITMAPFILEHEADER , tem 14 bytes de comprimento. (Lembre-se de que 1 byte é igual a 8 bits.) O segundo desses cabeçalhos, chamado BITMAPINFOHEADER , tem 40 bytes de comprimento. Imediatamente após esses cabeçalhos está o bitmap real: uma matriz de bytes, triplos dos quais representam a cor de um pixel. No entanto, o BMP armazena esses triplos ao contrário (ou seja, como BGR), com 8 bits para o azul, seguidos por 8 bits para o verde, seguidos por 8 bits para o vermelho. (Alguns BMPs também armazenam todo o bitmap de trás para frente, com a linha superior de uma imagem no final do arquivo BMP. Mas armazenamos os BMPs desse conjunto de problemas conforme descrito aqui, com cada linha superior do bitmap primeiro e a linha inferior por último.) Em outras palavras, se convertêssemos o smiley de 1 bit acima em um smiley de 24 bits, substituindo vermelho por preto, um BMP de 24 bits armazenaria esse bitmap da seguinte maneira, onde 0000ff significa vermelho e ffffff significa branco; destacamos em vermelho todas as ocorrências de 0000ff .

![](https://cs50.harvard.edu/x/2021/psets/4/filter/more/red_smile.png)

Como apresentamos esses bits da esquerda para a direita, de cima para baixo, em 8 colunas, você pode realmente ver o emoticon vermelho se der um passo para trás.

Para ser claro, lembre-se de que um dígito hexadecimal representa 4 bits. Consequentemente, ffffff em hexadecimal realmente significa 111111111111111111111111 em binário.

Observe que você pode representar um bitmap como uma matriz bidimensional de pixels: onde a imagem é uma matriz de linhas, cada linha é uma matriz de pixels. Na verdade, é assim que escolhemos representar as imagens de bitmap neste problema.

## Filtragem de Imagens

O que significa filtrar uma imagem? Você pode pensar em filtrar uma imagem como pegar os pixels de alguma imagem original e modificar cada pixel de forma que um efeito específico seja aparente na imagem resultante.

## Escala de cinza

Um filtro comum é o filtro “escala de cinza”, onde pegamos uma imagem e queremos convertê-la em preto e branco. Como isso funciona?

Lembre-se de que se os valores de vermelho, verde e azul estiverem todos configurados para 0x00 (hexadecimal para 0 ), o pixel é preto. E se todos os valores forem configurados para 0xff (hexadecimal para 255 ), o pixel é branco. Contanto que os valores de vermelho, verde e azul sejam todos iguais, o resultado será tons de cinza variados ao longo do espectro preto e branco, com valores mais altos significando tons mais claros (mais perto de branco) e valores mais baixos significando tons mais escuros (mais perto de Preto).

Portanto, para converter um pixel em tons de cinza, só precisamos ter certeza de que os valores de vermelho, verde e azul são todos iguais. Mas como sabemos que valor devemos criá-los? Bem, provavelmente é razoável esperar que, se os valores originais de vermelho, verde e azul fossem todos muito altos, o novo valor também deveria ser muito alto. E se os valores originais fossem todos baixos, o novo valor também deveria ser baixo.

Na verdade, para garantir que cada pixel da nova imagem ainda tenha o mesmo brilho ou escuridão geral da imagem antiga, podemos obter a média dos valores de vermelho, verde e azul para determinar qual tom de cinza deve ser feito no novo pixel.

Se você aplicar isso a cada pixel da imagem, o resultado será uma imagem convertida em tons de cinza.

## Sépia

A maioria dos programas de edição de imagem oferece suporte a um filtro “sépia”, que dá às imagens uma aparência antiga, fazendo com que toda a imagem pareça um pouco marrom-avermelhada.

Uma imagem pode ser convertida em sépia tomando cada pixel e computando novos valores de vermelho, verde e azul com base nos valores originais dos três.

Existem vários algoritmos para converter uma imagem em sépia, mas, para esse problema, pediremos que você use o seguinte algoritmo. Para cada pixel, os valores da cor sépia devem ser calculados com base nos valores da cor original conforme a seguir.

sepiaRed = .393 * originalRed + .769 * originalGreen + .189 * originalBlue  
sepiaGreen = .349 * originalRed + .686 * originalGreen + .168 * originalBlue  
sepiaBlue = 0,272 * originalRed + 0,534 * originalGreen + 0,131 * originalBlue

Obviamente, o resultado de cada uma dessas fórmulas pode não ser um número inteiro, mas cada valor pode ser arredondado para o número inteiro mais próximo. Também é possível que o resultado da fórmula seja um número maior que 255, o valor máximo para um valor de cor de 8 bits. Nesse caso, os valores de vermelho, verde e azul devem ser limitados a 255. Como resultado, podemos garantir que os valores de vermelho, verde e azul resultantes serão números inteiros entre 0 e 255, inclusive.

## Refletir

Alguns filtros também podem mover pixels. Refletir uma imagem, por exemplo, é um filtro em que a imagem resultante é o que você obteria colocando a imagem original na frente de um espelho. Portanto, quaisquer pixels no lado esquerdo da imagem devem terminar no lado direito e vice-versa.

Observe que todos os pixels originais da imagem original ainda estarão presentes na imagem refletida, mas esses pixels podem ter sido reorganizados para estar em um local diferente na imagem.

## Blur

Existem várias maneiras de criar o efeito de desfocar ou suavizar uma imagem. Para este problema, usaremos o “box blur”, que funciona pegando cada pixel e, para cada valor de cor, dando a ele um novo valor calculando a média dos valores de cor dos pixels vizinhos.

Considere a seguinte grade de pixels, onde numeramos cada pixel.

![](https://cs50.harvard.edu/x/2021/psets/4/filter/more/grid.png)

O novo valor de cada pixel seria a média dos valores de todos os pixels que estão dentro de 1 linha e coluna do pixel original (formando uma caixa 3x3). Por exemplo, cada um dos valores de cor para o pixel 6 seria obtido pela média dos valores de cor originais dos pixels 1, 2, 3, 5, 6, 7, 9, 10 e 11 (observe que o próprio pixel 6 está incluído no média). Da mesma forma, os valores de cor para o pixel 11 seriam obtidos pela média dos valores de cor dos pixels 6, 7, 8, 10, 11, 12, 14, 15 e 16.

Para um pixel ao longo da borda ou canto, como o pixel 15, ainda procuraríamos todos os pixels em 1 linha e coluna: neste caso, os pixels 10, 11, 12, 14, 15 e 16.

## Arestas

Em algoritmos de inteligência artificial para processamento de imagens, muitas vezes é útil detectar bordas em uma imagem: linhas na imagem que criam um limite entre um objeto e outro. Uma maneira de obter esse efeito é aplicando o operador Sobel à imagem.

Assim como o desfoque da imagem, a detecção de bordas também funciona pegando cada pixel e modificando-o com base na grade 3x3 de pixels que circunda esse pixel. Mas em vez de apenas tirar a média dos nove pixels, o operador Sobel calcula o novo valor de cada pixel tomando uma soma ponderada dos valores para os pixels circundantes. E como as bordas entre os objetos podem ocorrer nas direções vertical e horizontal, você realmente calculará duas somas ponderadas: uma para detectar bordas na direção x e outra para detectar bordas na direção y. Em particular, você usará os seguintes dois “kernels”:

![](https://cs50.harvard.edu/x/2021/psets/4/filter/more/sobel.png)

Como interpretar esses kernels? Resumindo, para cada um dos três valores de cor de cada pixel, calcularemos dois valores Gx e Gy . Para calcular Gx para o valor do canal vermelho de um pixel, por exemplo, pegaremos os valores vermelhos originais para os nove pixels que formam uma caixa 3x3 ao redor do pixel, multiplicaremos cada um pelo valor correspondente no kernel Gx e tomaremos a soma dos valores resultantes.

Por que esses valores particulares para o kernel? Na direção Gx , por exemplo, estamos multiplicando os pixels à direita do pixel alvo por um número positivo e multiplicando os pixels à esquerda do pixel alvo por um número negativo. Quando fazemos a soma, se os pixels da direita forem de cor semelhante aos pixels da esquerda, o resultado será próximo de 0 (os números se cancelam). Mas se os pixels da direita forem muito diferentes dos pixels da esquerda, o valor resultante será muito positivo ou muito negativo, indicando uma mudança na cor que provavelmente é o resultado de um limite entre os objetos. E um argumento semelhante é válido para calcular arestas na direção y .

Usando esses kernels, podemos gerar um valor Gx e Gy para cada um dos canais vermelho, verde e azul de um pixel. Mas cada canal pode assumir apenas um valor, não dois: portanto, precisamos de alguma forma para combinar Gx e Gy em um único valor. O algoritmo de filtro de Sobel combina Gx e Gy em um valor final calculando a raiz quadrada de Gx ^ 2 + Gy ^ 2 . E uma vez que os valores do canal só podem assumir valores inteiros de 0 a 255, certifique-se de que o valor resultante seja arredondado para o inteiro mais próximo e limitado a 255!

E quanto ao manuseio de pixels na borda ou no canto da imagem? Existem muitas maneiras de lidar com pixels na borda, mas para os fins deste problema, pediremos que você trate a imagem como se houvesse uma borda preta sólida de 1 pixel ao redor da borda da imagem: portanto, tentando acessar um pixel além da borda da imagem deve ser tratado como um pixel preto sólido (valores de 0 para cada vermelho, verde e azul). Isso irá efetivamente ignorar esses pixels de nossos cálculos de Gx e Gy .

# Exercício 2: Filter - Versão desafiadora


# Exercício 3: Recover