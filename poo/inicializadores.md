# Inicializadores
- são seções do código que são executadas sempre **antes** dos construtores, exemplo:
```java
  public class Exemplo {
    private int x;
    private String nome;
    
    // Bloco de inicialização de instância
    {
        System.out.println("Bloco de inicialização executado!");
        x = 10;
        nome = "Padrão";
    }
    
    public Exemplo() {
        System.out.println("Construtor executado!");
    }
    
    public static void main(String[] args) {
        Exemplo obj = new Exemplo();
        // Saída:
        // Bloco de inicialização executado!
        // Construtor executado!
    }
  }
```
- também temos o bloco de inicialização **estático**, que só é executado uma vez quando a classe é carregada pela JVM, exemplo:
```java
  public class ExemploEstatico {
    private static int contador;
    private static final double PI;
    
    // Bloco de inicialização estático
    static {
        System.out.println("Bloco estático executado!");
        contador = 0;
        PI = 3.14159;
    }
    
    public ExemploEstatico() {
        contador++;
        System.out.println("Objeto criado. Total: " + contador);
    }
    
    public static void main(String[] args) {
        new ExemploEstatico(); // Bloco estático executa aqui
        new ExemploEstatico(); // Bloco estático NÃO executa novamente
    }
  }
```
