# Arrays
- sintaxe para criar é: tipo[] nomeArray = new tipo[tamanho];
- **exemplo**: ```java int[] numeros = new int[3];```
- **outra forma**: ```java int[] numeros = {0, 1, 2, 3};```
- para iterar sobre um array, como são objetos e não tipos primitivos, podemos acessar seu tamanho usando o atributo length, exemplo: numeros.length;
- **foreach** é uma forma mais prática de iterar sobre um array, nele vc declara uma variável **do tipo do array**, que vai percorrer cada elemento do array.
- **exemplo**: ```java for(int numero : numeros){ codigo }```
- sintaxe é: ```java for(tipoArray variavelTemp : nomeArray){ código }```

# Arrays Multidimensionais
- para criar um array de 2 dimensões por exemplo:
- int[][] matriz = new int[3][3]; **aqui criei uma matriz 3x3**
- **DICA:** para selecionar o codigo, segura shift e move a seta pra onde quiser, vai selecionar tudo.
- usando foreach num bidimensional, voce faz:
```java
for(int[] arrBase : array){
  for(int elemento : arrBase){
    código
  }
}
```
- um array bidimensional, cada "vetor menor" pode ter tamanhos diferentes de arrays, por exemplo: int[][] numeros = new int[3][]; aqui, ele tem 3 arrays menores, e cada um pode ser inicializado com tamanhos diferentes
- exemplo:  numeros[0] = new int[4]; numeros[1] = new int[1]; e assim vai.





