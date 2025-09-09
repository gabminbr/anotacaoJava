# Herança
- quando queremos que uma classe herde outra, usamos a palavra extends logo após do (modificador de acesso) NomeDaClasse extends NomeDaClasseMae
- entretanto, agora usaremos um novo modificador de acesso, o *protected*, ele basicamente só deixa visível o atributo para as classes que estão no mesmo pacote e para subclasses (que herdam).
- ao aplicarmos o conceito de herança, estenderemos as funcionalidade da classe mae, exemplo:
```java
  public class Pessoa{
    protected String nome;
    protected int idade;

    public Pessoa(String nome, int idade){
      this.nome = nome;
      this.idade = idade;
    }
  }

  public class Funcionario extends Pessoa{
    private double salario;

    public Funcionario(String nome, int idade, double salario){
      super(nome, idade);
      this.salario = salario;
    }
  }
```
- para referenciar a classe mãe, usaremos o termo 'super', exemplo, para sobrescrever um método da classe mãe:
```java
  public class Pessoa{
    private String nome;
    private int idade;

    public void imprime(){
      System.out.println(this.nome);
      System.out.println(this.idade);
    }
  }

  public class Funcionario extends Pessoa{
    private double salario;

    public void imprime(){
      super.imprime();
      System.out.println(this.salario);
