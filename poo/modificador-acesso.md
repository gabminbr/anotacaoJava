# Modificadores de Acesso
- temos que evitar as classes estarem muito conectadas, para isso, usaremos do princípio do **acoplamento**, devemos ir atrás do **baixo** acoplamento.
- então, começaremos a usar o modificador de acesso *private*, que vai fazer com que os atributos de uma classe só possam ser acessados pela mesma.
- porém, ainda temos que poder **visualizar** os atributos, certo? para isso servem os getters (podemos visualizar o valor) e os setters(podemos atribuir valores).
- o exemplo de um código usando de tudo isso:
```java
  public class Pessoa {
    private String nome;
    private int idade;

    public String getNome(){
      return this.nome;
    }

    public int getIdade(){
      return this.idade;
    }

    public void setNome(String nome){
      this.nome = nome;
    }

    public void setIdade(int idade){
      this.idade = idade;
    }
  }
```
- em geral, buscaremos sempre a **alta** coesão, e o **baixo** acoplamento, a primeira é basicamente: uma classe/método deve fazer sua única função, e não servir como um "canivete suíço".

    
