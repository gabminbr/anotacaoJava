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
- 
