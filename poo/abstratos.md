# Classes Abstratas
- classes abstratas são basicamente um *template* para classes que vão herdar dela, ela não vai poder ser instanciada diretamente, apenas suas sub-classes, exemplo:
```java
  public abstract class Funcionario{
    protected String nome;
    protected int id;

    public Funcionario(String nome, int id){
      this.nome = nome;
      this.id = id;
    }
  }

  public final class Repositor extends Funcionario{
    public Repositor(String nome, int id){
      super(nome, id);
    }
  }
```
# Métodos Abstratos
- serve de template para classes que irão herdar da classe e sobrescrever o método, esses métodos não podem ter corpo, exemplo:
```java
  public abstract class Funcionario{ // um método abstrato só pode ser feito dentro de uma classe abstrata (ou uma interface)
    protected String nome;
    protected int id;

    public Funcionario(String nome, int id){
      this.nome = nome;
      this.id = id;
    }

    public abstract double calculaBonus();
  }

  public class Repositor extends Funcionario{
    private double salario;

    public Repositor(String nome, int id, double salario){
      super(nome, id);
      this.salario = salario;
    }

    @Override
    public double calculaBonus(){
      return salario * 0.15;
    }
  }
```
