# Métodos
- a sintaxe para um método sempre será:
```java
  modificadorDeAcesso tipoRetorno nomeCamelCase(parâmetros){
    código
  }
```
- exemplo:
```java
  public int somaNumeros (int a, int b){
    return a + b;
  }
```
- **DICA**: para por exemplo ver que tipo de dado tem que ser colocado no construtor ou nos parâmetros de um método, aperte cntrl + p
- o return pode ser usado analogamente a um break, só que em métodos, exemplo:
```java
  public void imprimeDivisao(int a, int b){
    if(b == 0){
      System.out.println("Não existe divisão por 0");
    }
    System.out.println((double) a / b);
```
- ao executar o código acima e o segundo argumento da chamada da função for 0, ele vai executar a condicional, pois b == 0, porém ele também vai executar a divisão mesmo assim, então usamos o return para ajustar esse problema:
```java
  public void imprimeDivisao(int a, int b){
    if(b == 0){
      System.out.println("Não existe divisão por 0");
      return;
    }
    System.out.println((double) a / b);
```
- ainda usando do mesmo exemplo, podemos falar sobre os parâmetros, quando passamos na main valores como parâmetros para uma função, o que o método na outra classe faz é COPIAR o valor e mudar dentro do MÉTODO apenas, logo, no programa principal, os valores NÃO vão se alterar.
- porém, é diferente com valores do tipo referência, exemplo String, você passa a REFERÊNCIA, logo, qualquer mudança dentro do método no argumento, vai afetar a variável no escopo "principal".
- **DICA**: se quiser por exemplo, alterar uma parte do código que se repete muito, um nome, uma classe, seleciona ela + shift + f6;
- **VarArgs** é uma ferramenta para simplificar o argumento quando for um array, a sintaxe dele é (tipo)... nomeVariavel, exemplo:
```java
  public void imprimeArray(int... numeros){
    for(int temp : numeros){
      System.out.println(temp);
    }
  }
```
- entretanto, não pode passar nenhum argumento depois além dele
