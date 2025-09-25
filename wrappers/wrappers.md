# Wrappers
- No java, temos os tipos primitivos, que guardam o valor diretamente na memória e são de rápido acesso, entretanto, o pilar que o Java trabalha, é a orientação a *objetos*, logo, surgem ocasiões em que é necessário trabalhar com tipos primitivos como se fossem objetos.
- Alguns dos motivos são por exemplo, usando em coleções e genéricos, não posso criar um ArrayList<int>, mas posso criar o ArrayList<Integer>.
- Ao usar wrappers, também permite que possamos utilizar métodos utilitários, também podemos colocar valores null.
- Autoboxing: É a conversão automática que o compilador Java faz de um tipo primitivo para sua classe Wrapper correspondente, ex:
```java
  // Autoboxing: o compilador converte o int 10 para um Integer
  Integer numeroWrapper = 10;
```
- Unboxing: É o processo inverso, a conversão automática de um objeto Wrapper para o seu tipo primitivo correspondente, ex:
```java
  // Unboxing: o compilador converte o Integer para um int
  int numeroPrimitivo = numeroWrapper;
```
