# Enumeração
- **DICA**, para comparar o conteúdo de strings, usamos o *.equals*, e se quisermos ignorar o upper/lower, usamos .ignoreCase().
- a enumeração serve para evitar a inconsistência de dados, a sua sintaxe é *public enum NomeDaClasseEnumeracao*
- todo atributo que for criado nela, vão ser constantes, ou seja, vão ter o *final static*, exemplo de uso:
```java
  public enum TipoPessoa{
    PESSOA_JURIDICA,
    PESSOA_FISICA
  }

  // usando em uma classe que tenha relação com essa enumeração

  public class Cliente{
    private String nome;
    private int id;
    private TipoPessoa tipoCliente;

    public Cliente(String nome, int id, TipoPessoa tipoCliente){
      this.nome = nome;
      this.id = id;
      this.tipoCliente = tipoCliente;
    }
  }

  // ao instanciar usaremos:

  public static void main(String[] args){
    Cliente cliente = new Cliente("Carlos", 129819, TipoPessoa.PESSOA_JURIDICA);
  }
```
- também é possível usar valores para representar os atributos da enumeração, exemplo, voce quer q digite 1 se o pagamento é debito e 2 se credito, entretanto, precisaremos criar o construtor:
```java
  public enum TipoPagamento{
    DEBITO(1), // não precisa necessariamente ser um valor int, pode ser string também
    CREDITO(2);

    // precisamos declarar a variável DEPOIS das enumeracoes!!!
    private int tipo;

    TipoPagamento(int tipo){
      this.tipo = tipo;
    }

    public int getTipo(){
      return this.tipo;
    }
  }

  // aqui pegaremos o valor numerico do dia:
  public class Main {
    public static void main(String[] args) {
        DiaDaSemana hoje = DiaDaSemana.QUARTA;
        System.out.println("Hoje é o dia número: " + hoje.getNumeroDoDia());
    }
  }

  // já aqui, pegaremos o valor string dele:
  DiaDaSemana dia = DiaDaSemana.fromNumero(5);
  System.out.println(dia); // SEXTA
```
- podemos fazer a sobrescrita de métodos também, por exemplo, queremos que calcule um desconto se for no credito e outro se no debito, porem sem usar if else:
```java
  public enum TipoPagamento{
    DEBITO(1){
      @Override
      public double calcularDesconto(int valor){
        return valor -= 0.10 * valor;
    }, CREDITO(2){
      @Override
      public double calcularDesconto(int valor){
        return valor -= 0.20 * valor;
      }
    };

    private int tipo;
    TipoPagamento(int tipo){
      this.tipo = tipo;
    }

    public double calcularDesconto(int valor){
      return 0;
    }
```
