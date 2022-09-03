# Exercício 0: Legibilidade

**[VIDEO](https://www.youtube.com/watch?v=vTsVt_kDS2M&ab_channel=Funda%C3%A7%C3%A3oEstudar)**

Implemente um programa que calcule o nível (representado a partir de uma série, como na escola) aproximado necessário para compreender algum texto, conforme a seguir.

$ ./readability  
Texto: Parabéns! Hoje é seu dia. Você está indo para ótimos lugares! Você está com tudo!  
Grade 3

## Níveis de leitura

De acordo com a Scholastic , “Charlotte's Web” de EB White está entre o nível de leitura da segunda e quarta séries, e “The Giver” de Lois Lowry está entre um nível de leitura da oitava série e um nível de leitura da décima segunda série. No entanto, o que significa um livro estar no “nível de leitura da quarta série”?

Bem, em muitos casos, um especialista humano pode ler um livro e tomar uma decisão sobre a série para a qual acha que o livro é mais apropriado. Mas você também pode imaginar um algoritmo tentando descobrir qual é o nível de leitura de um texto.

Então, que tipo de características são características de níveis de leitura mais altos? Bem, palavras mais longas provavelmente se correlacionam com níveis de leitura mais altos. Da mesma forma, frases mais longas provavelmente se correlacionam com níveis mais altos de leitura também. Vários “testes de legibilidade” foram desenvolvidos ao longo dos anos, para fornecer um processo estereotipado para calcular o nível de leitura de um texto.

Um desses testes de legibilidade é o índice Coleman-Liau. O índice Coleman-Liau de um texto é projetado para mostrar qual nível escolar (EUA) é necessário para entender o texto. A fórmula é:

índice = 0,0588 * L - 0,296 * S - 15,8

Aqui, **L** é o número médio de letras por 100 palavras no texto e S é o número médio de sentenças por 100 palavras no texto.

Vamos escrever um programa chamado **readability** que pega um texto e determina seu nível de leitura. Por exemplo, se o usuário digitar uma linha do Dr. Seuss:

	$ ./readability  
	Texto: Congratulations! Today is your day. You're off to Great Places! You're off and away!  
	Grade 3

O texto que o usuário inseriu tem 65 letras, 4 sentenças e 14 palavras. 65 letras por 14 palavras é uma média de cerca de 464,29 letras por 100 palavras. E 4 sentenças por 14 palavras é uma média de cerca de 28,57 sentenças por 100 palavras. Conectados à fórmula Coleman-Liau e arredondados para o número inteiro mais próximo, obtemos uma resposta de 3: portanto, esta passagem está em um nível de leitura da terceira série.

Vamos tentar outro:

	$ ./readability  
	Text: Harry Potter was a highly unusual boy in many ways. For one thing, he hated the summer holidays more than any other time of year. For another, he really wanted to do his homework, but was forced to do it in secret, in the dead of the night. And he also happened to be a wizard.  
	Grade 5

Este texto contém 214 letras, 4 frases e 56 palavras. Isso resulta em cerca de 382,14 letras por 100 palavras e 7,14 frases por 100 palavras. Conectados à fórmula Coleman-Liau, chegamos ao nível de leitura da quinta série.

À medida que o número médio de letras e palavras por frase aumenta, o índice de Coleman-Liau dá ao texto um nível de leitura mais alto. Se você pegasse este parágrafo, por exemplo, que tem palavras e sentenças mais longas do que qualquer um dos dois exemplos anteriores, a fórmula daria ao texto um nível de leitura de décimo primeiro ano.

	$ ./readability  
	Text: As the average number of letters and words per sentence increases, the Coleman-Liau index gives the text a higher reading level. If you were to take this paragraph, for instance, which has longer words and sentences than either of the prior two examples, the formula would give the text an eleventh grade reading level.  
	Grade 11
	
---
# Exercício 1: Caesar

**[VIDEO](https://www.youtube.com/watch?v=82pMEmDMnxI&ab_channel=Funda%C3%A7%C3%A3oEstudar)**

Implemente um programa que criptografa mensagens usando a cifra de César, conforme a seguir.

$ ./caesar 13  
plaintext: HELLO  
ciphertext: URYYB

**Lembre-se que plaintext significa _texto simples_ e ciphertext é o _texto cifrado_!** 

## **Background**

Supostamente, César (sim, aquele César) costumava “criptografar” (ou seja, ocultar de forma reversível) mensagens confidenciais deslocando cada letra nelas em algum número de lugares. Por exemplo, ele pode escrever A como B, B como C, C como D, ..., e, agrupando em ordem alfabética, Z como A. E então, para dizer HELLO para alguém, César pode escrever IFMMP. Ao receber essas mensagens de César, os destinatários teriam que “decifrá-las” deslocando as letras na direção oposta no mesmo número de lugares.

O segredo desse “criptosistema” dependia apenas de César e dos destinatários saberem de um segredo, o número de lugares pelos quais César havia mudado suas cartas (por exemplo, 1). Não é particularmente seguro para os padrões modernos, mas, ei, se você é talvez o primeiro no mundo a fazer isso, bastante seguro!

O texto não criptografado é geralmente chamado de texto simples . O texto criptografado é geralmente chamado de texto cifrado . E o segredo usado é chamado de chave .

Para ser claro, então, aqui está como criptografar **HELLO** com uma chave de 1 resulta em **IFMMP** :

plaintext (texto simples)

H

E

L

L

O

+ key(chave)

1

1

1

1

1

= ciphertext (texto cifrado)

I

F

M

M

P

Mais formalmente, o algoritmo de César (isto é, cifra) criptografa mensagens “girando” cada letra em k posições. Mais formalmente, se p é algum texto simples (ou seja, uma mensagem não criptografada), pi é o i-ésimo caractere em p , e k é uma chave secreta (ou seja, um inteiro não negativo), então cada letra, c i , em o texto cifrado, c , é calculado como

c i = (p i + k)% 26

em que **%26** aqui significa "resto ao dividir por 26." Essa fórmula talvez faça a cifra parecer mais complicada do que é, mas na verdade é apenas uma maneira concisa de expressar o algoritmo com precisão. De fato, para fins de discussão, pense em A (ou a) como 0, B (ou b) como 1, ..., H (ou h) como 7, I (ou i) como 8, ... e Z (ou z) como 25. Suponha que César apenas queira dizer Oi para alguém confidencialmente usando, desta vez, uma chave, k , de 3. E então seu texto simples, p , é Hi, em cujo caso o primeiro caractere de seu texto simples, p 0 , é H (também conhecido como 7), e o segundo caractere de seu texto simples, p 1 , é i (também conhecido como 8). O primeiro caractere de seu texto cifrado, c 0 , é portanto K, e o segundo caractere de seu texto cifrado, c 1 , é assim L. Você pode ver por quê?

Vamos escrever um programa chamado **ceasar** que permite criptografar mensagens usando a cifra de César. No momento em que o usuário executa o programa, ele deve decidir, fornecendo um argumento de linha de comando, qual deve ser a chave na mensagem secreta que fornecerá no tempo de execução. Não devemos necessariamente presumir que a chave do usuário será um número; embora você possa assumir que, se for um número, será um inteiro positivo.

Aqui estão alguns exemplos de como o programa pode funcionar. Por exemplo, se o usuário inserir uma chave de **1** e um texto simples de HELLO :

```
$ ./caesar 1
plaintext:  HELLO
ciphertext: IFMMP
```

Veja como o programa pode funcionar se o usuário fornecer uma chave **13** e um texto simples de hello, world : 

```
$ ./caesar 13
plaintext:  hello, world
ciphertext: uryyb, jbeyq
```

Observe que nem a vírgula nem o espaço foram "deslocados" pela cifra. Gire apenas caracteres alfabéticos!

Que tal mais um? Veja como o programa pode funcionar se o usuário fornecer uma chave **13** novamente, com um texto simples mais complexo: 

```
$ ./caesar 13
plaintext:  be sure to drink your Ovaltine
ciphertext: or fher gb qevax lbhe Binygvar
```

Observe que a caixa da mensagem original foi preservada. As letras minúsculas permanecem minúsculas e as maiúsculas permanecem maiúsculas.

E se um usuário não cooperar?

```
$ ./caesar HELLO
Usage: ./caesar key
```

Ou realmente não coopera?

	$ ./caesar
	Usage: ./caesar key

Ou mesmo ...

	$ ./caesar 1 2 3
	Usage: ./caesar key

---

# Exercício 2: Substituição (desafio)

**[VIDEO](https://www.youtube.com/watch?v=yOGX9KxvYnA&ab_channel=Funda%C3%A7%C3%A3oEstudar)**

Implemente um programa que implemente uma cifra de substituição, conforme a seguir.

$ ./substitution JTREKYAVOGDXPSNCUIZLFBMWHQ  
texto simples: HELLO  
texto cifrado: VKXXN

## Background

Em uma cifra de substituição, “criptografamos” (ou seja, ocultamos de forma reversível) uma mensagem substituindo cada letra por outra. Para isso, usamos uma chave : neste caso, um mapeamento de cada uma das letras do alfabeto à letra correspondente quando criptografada. Para “decifrar” a mensagem, o receptor da mensagem precisaria saber a chave, para que pudesse reverter o processo: traduzir o texto criptografado (geralmente chamado de texto cifrado ) de volta na mensagem original (geralmente chamado de texto simples ).

Uma chave, por exemplo, pode ser a sequencia NQXPOMAFTRHLZGECYJIUWSKDVB. Esta chave de 26 caracteres significa que **A** (a primeira letra do alfabeto) deve ser convertido em **N** (o primeiro caractere da chave), **B** (a segunda letra do alfabeto) deve ser convertido em **Q** (o segundo caractere do chave), e assim por diante.

Uma mensagem como **HELLO** , então, seria criptografada como **FOLLE** , substituindo cada uma das letras de acordo com o mapeamento determinado pela chave.

Vamos escrever um programa chamado **substitution** que permite criptografar mensagens usando uma cifra de substituição. No momento em que o usuário executa o programa, ele deve decidir, fornecendo um argumento de linha de comando, qual deve ser a chave na mensagem secreta que fornecerá durante a execução.

Aqui estão alguns exemplos de como o programa pode funcionar. Por exemplo, se o usuário inserir uma chave de **YTNSHKVEFXRBAUQZCLWDMIPGJO** e um texto simples de **HELLO** :

$ ./substitution YTNSHKVEFXRBAUQZCLWDMIPGJO  
texto simples: HELLO  
texto cifrado: EHBBQ

Veja como o programa pode funcionar se o usuário fornecer uma chave de **VCHPRZGJNTLSKFBDQWAXEUYMOI** e um texto simples de **hello, world** :

$ ./substitution VCHPRZGJNTLSKFBDQWAXEUYMOI  
texto simples: hello, world  
texto cifrado: jrssb, ybwsp

Observe que nem a vírgula nem o espaço foram substituídos pela cifra. Substitua apenas caracteres alfabéticos! Observe também que o case da mensagem original foi preservado. As letras minúsculas permanecem minúsculas e as maiúsculas permanecem maiúsculas.

Não importa se os caracteres da própria chave são maiúsculas ou minúsculas. Uma chave de **VCHPRZGJNTLSKFBDQWAXEUYMOI** é funcionalmente idêntica a uma chave de **vchprzgjntlskfbdqwaxeuymoi** (como é, nesse caso, **VcHpRzGjNtLsKfBdQwAxEuYmOi** ).

E se um usuário não fornecer uma chave válida?

$ ./substitution ABC  
A chave deve conter 26 caracteres.

Ou realmente não coopera?

$ ./substitution  
Uso: ./ chave de substituição

Ou mesmo ...

$ ./substituição 1 2 3  
Uso: ./ chave de substituição