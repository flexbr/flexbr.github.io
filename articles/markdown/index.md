# Markdown

**Markdown** é uma linguagem simples de marcação originalmente criada por [John Gruber](daringfireball.net/projects/markdown). 
Ela converte texto em HTML válido. É a linguagem oficial de documentação no [GitHub](guides.github.com/features/mastering-markdown). Toda a documentação da [Microsoft](docs.microsoft.com) é escrita nela. Como acabou tornando-se um padrão de documentação é importante para todo desenvolvedor conhecê-la e saber utilizá-la.

---

## Pricipais Marcadores

### 1 - Cabeçalhos (equivalente a h1-h6 do html):
# Titulo 1
## Titulo 2
### Titulo 3
#### Titulo 4
##### Titulo 5
###### Titulo 6

```md
# Titulo 1
## Titulo 2
### Titulo 3
#### Titulo 4
##### Titulo 5
###### Titulo 6
```

### 2 - Parágrafos
Basta escrever uma ou mais frases. Para quebrar apenas uma linha, use dois espaços  Agora estamos em uma nova linha. Putz, não deu certo(no preview), mas no gitHub dá. Outra maneira(workaround) é usar a tag br do html.<br>Agora sim, até no preview estamos em outra linha. Para quebrar uma linha com espaçamento maior, dê enter no final.
Agora estamos em outra linha. (rever essas opções no github).

### 3 - Ênfase 

**Negrito** basta colocar dois asteriscos ou dois _(underline) antes e depois do texto:

```md
**Negrito**
__Negrito__
```
*Itálico* basta colocar um asteriscos ou um _(underline) antes e depois do texto:

```md
**Itálico**
__Itálico__
```
***Negrito e Itálico*** ao mesmo tempo, basta utilizar os dois, ou seja três asteriscos, três underline ou mesclar as duas formas:

```md
***Negrito e Itálico***
___Negrito e Itálico___
**_Negrito e Itálico_**
__*Negrito e Itálico*__

```

~~Riscado~~, utilizar dois ~(til) antes e depois:

```md
~~Riscado~~
```

> Citação, basta colocar um sinal de >(maior) no início do parágrafo:

```md
> Esta é uma citação.
```

> Citação, com **Negrito** e *Itálico*, basta iniciar com a citação e utilizar os dois:

```md
> Esta é *uma* **citação**.
```

### 4 - Linhas horizontais

Basta utilizar três *(asteriscos) ou três -(traços), pode também colocar espaços entre eles, e colocar mais asteriscos ou traços, que é ignorado, mas pode facilitar na hora de visualizar somente o código md:

***

```md
***
---
* * *
- - -
**************************************
--------------------------------------
```

### 5 - Listas não ordenadas

* Item 01
* Item 02
* Item 03

Basta colocar um *(asterisco), um -(traço) ou +(mais) na frente dos itens:

```md
* Item 01
* Item 02
* Item 03

- Item 01
- Item 02
- Item 03

+ Item 01
+ Item 02
+ Item 03
```
Para criar subitens basta identar, usando o tab:

* Item 01
    * Subitem 1
    * Subitem 2
* Item 02
* Item 03

```md
* Item 01
    * Subitem 1
    * Subitem 2
* Item 02
* Item 03

* Item 01
    - Subitem 1
    - Subitem 2
* Item 02
* Item 03

- Item 01
    + Subitem 1
    - Subitem 2
* Item 02
* Item 03
```

Para espaçar um pouco mais os itens, basta dar enter entre eles:

* Item 01
    - Subitem 1

    - Subitem 2

* Item 02
    - Subitem 3
    - Subitem 4

* Item 03

```md
* Item 01
    - Subitem 1

    - Subitem 2

* Item 02
    - Subitem 3
    - Subitem 4

* Item 03
```

### 6 - Listas ordenadas

Basta colocar um número seguido de .(ponto):

1. Item 01
2. Item 02
3. Item 03

```md
1. Item 01
2. Item 02
3. Item 03

1. Item 01
1. Item 02
1. Item 03
```

A lista inicia pelo primeiro número informado:

5. Item 05
666. Item 06
1. Item 07

```md
5. Item 05
6. Item 06
7. Item 07

5. Item 05
666. Item 06
2. Item 07
```

E se eu precisar fazer uma lista com números diferentes? Basta colocar o caracter de escape \(barra invertida) antes do ponto. Mas não será uma lista e você terá que quebrar a linha com dois espaços(  ) no final ou enter para um espaçamento maior:

1990\. Airton Senna  
2000\. Schumacher  
2010\. Vettel

```md
1990\. Airton Senna  
2000\. Schumacher  
2010\. Vettel

1990\. Airton Senna

2000\. Schumacher

2010\. Vettel
```

### 7 - Links

Para criar um link basta utilizar colchetes em volta do texto, seguido de parênteses contendo o link em sí `[Texto clicável](link)`:

[Vai para o site do Ricardo Ramires](http://rramires.github.io/)

```md
[Vai para o site do Ricardo Ramires](http://rramires.github.io/)
```

Para utilizar o alt text, basta dar um espaço e colocálo entre aspas:

[Vai para o site do Ricardo Ramires](http://rramires.github.io/ "Clique nesse link para ser redirecionado")

Outra forma, é criar uma variável contendo o link e depois acessála:

[url-do-google]: http://www.google.com
[Clique para ir ao Google][url-do-google]

```md
[url-do-google]: http://www.google.com
[Clique para ir ao Google][url-do-google]
```

Isso pode ser útil para um link que será utilizado muitas vezes, facilitando alterar em um único local.

### 8 - Imagens

Para inserir imanges, é similar ao link. Colchetes com o nome, seguidos de parênteses com o enrereço da imagem. Só que no início vai um ponto de !(exclamação) `![Minha Imagem](img/foto.jpg)`

![Minha Imagem](img/watchmen.png)

```md
![Figura do Watchmen](img/watchmen.png)
```

Outra maneira é utilizando variáveis, como já vimos no link:

[path-da-imagem]: img/watchmen.png
![Figura do Watchmen][path-da-imagem]

```md
[path-da-imagem]: img/watchmen.png
![Figura do Watchmen][path-da-imagem]
```

Imagem com link, basta colocar a imagem dentro dos colchetes que é a área clicável do link:

[![Logo Google](img/google.png)](http://www.google.com)

```md
[![Logo Google](img/google.png)](http://www.google.com)
```

Para usar variáveis para o link e imagem, basta criá-las e substituir onde iria o caminho e a url:

[url-google]: http://www.google.com
[path-da-imagem-google]: img/google.png

[![Logo Google][path-da-imagem-google]][url-google]]

```md
[url-google]: http://www.google.com
[path-da-imagem-google]: img/google.png

[![Logo Google][path-da-imagem-google]][url-google]]
```


























