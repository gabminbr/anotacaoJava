# Método ToString
- esse método vem da classe Object, e ela serve como a formatação do print de objetos dessa classe, como que vai se comportar ao ser usada como output
- ela na classe object é *public String toString() { código }*, e podemos usar o @Override para ter a certeza que estamos sobrescrevendo, exemplo:
```java
  public class Pessoa {
    private String nome;

    @Override
    public String toString(){
      return "Nome: " + this.nome
  }
```
- porém, podemos usar um atalho do intellij, usamos alt + insert.
