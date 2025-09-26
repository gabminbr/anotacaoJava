# Strings
- primeiro, devemos entender a diferença entra memória heap e String Constant Pool:
- *heap* é a principal área de memória em Java, onde todos os objetos são criados.
- *SCP*: é uma área dentro da heap, a JVM a utiliza para guardar uma única cópia de cada String literal (texto entre aspas). O objetivo é economizar a memória.
- um exemplo:
```java
  String s1 = "Java";
  String s2 = "Java";
```
- O que ocorre: para s1, a JVM pergunta para a SCP se a string "Java" já existe lá, a resposta é não, então a JVM cria a string dentro da pool e faz s1 apontar para ela.
- já na s2, a JVM faz a mesma pergunta e a resposta agora é sim, então, para economizar memória, a JVM faz s2 apontar para a mesma string que s1 está apontando, assim, s1 e s2 apontam para o mesmo objeto.
- para forçar a JVM a criar uma nova string mesmo ela já existindo na pool, faça assim:
```java
  String s3 = new String("Java");
```
- assim, a string Java é criada e fora da pool, na heap.
```
    +--------------------------------+
    |           HEAP MEMORY          |
    |                                |
    |   +------------------------+   |
    |   |  String Constant Pool  |   |
    |   |                        |   |
    |   | s1 --> ["Java"] <-- s2 |   |
    |   +------------------------+   |
    |                                |
    |       s3 --> ["Java"]          |
    |                                |
    +--------------------------------+
```
## Concatenação
- As strings são imutáveis, entretanto, o que acontece ao fazer o seguinte:
```java
  String saudacao = "Olá";
  saudacao = saudacao + ", Mundo!"; // Como isso é possível se a String é imutável?
```
- ao fazer saudacao + ", Mundo!", a JVM cria um objeto completamente novo, porém, esse conteúdo novo vai pra *heap*, não para a pool.
- Entretanto, o objeto original "Olá", não é "destruído", ele fica na pool e pode ser usado mesmo sem alguém apontando para ele.
- Então, como concatenar de um jeito mais fácil?
- StringBuilder e StringBuffer: É como um rascunho em um editor de texto. Você pode adicionar, apagar e alterar o texto no mesmo lugar, sem precisar criar um novo arquivo a cada mudança.
- a diferença entre os dois é a segurança em ambientes com múltiplos processos (Thread Safety).
- Imagine um programa com vários "trabalhadores" (chamados threads) tentando executar tarefas ao mesmo tempo.
- **StringBuffer**: é thread safe, é como uma sala de edição com apenas uma cadeira e uma tranca na porta. Apenas um "trabalhador" (thread) pode entrar e modificar o texto por vez. Os outros precisam esperar na fila.
- **StringBuilder**: É uma sala de edição com várias cadeiras e sem tranca na porta. Vários "trabalhadores" podem tentar alterar o texto ao mesmo tempo.
```java
  // Ineficiente com String
  String listaDeCompras = "";
  listaDeCompras += "Maçã\n";
  listaDeCompras += "Banana\n";
  listaDeCompras += "Leite\n";
  // (Foram criados 4 objetos String na memória para chegar aqui!)
  
  // Eficiente com StringBuilder
  StringBuilder sb = new StringBuilder();
  sb.append("Maçã\n");
  sb.append("Banana\n");
  sb.append("Leite\n");
  String listaFinal = sb.toString(); // Só cria a String final uma vez!
```



