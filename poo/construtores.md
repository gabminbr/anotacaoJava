# Sobrecarga de Métodos
- **DICA**: para adicionar rápido os get e set, aperta alt + insert no código, e seleciona os que voce quer.
- O Java permite sobrecarga de métodos, ou seja, fazer o mesmo método com mesmo nome e etc, desde que o número de parâmetros seja diferente.

# Construtores
- construtores são um método especial invocado automaticamente no momento da criação de um objeto (com new), cujo propósito fundamental é inicializar o novo objeto em um estado válido e consistente.
- por regra, se não é criado um construtor na classe, o java automaticamente inicializa com um construtor vazio, logo, é obrigatório que sempre crie o construtor.
- a sintaxe é modificadorDeAcesso NomeDaClasse(os atributos que vai querer que sejam obrigatoriamente inicializados ao criar uma instância){ código }
- ele é executado antes de qualquer método da classe.
- exemplo:
```java
  public class Pessoa {
    private String nome;
    private int idade;
    private char sexo;

    public Pessoa(String nome, int idade, char sexo){
      this.nome = nome;
      this.idade = idade;
      this.sexo = sexo;
    }
```
- podemos também usar a sobrecarga para construtores, se quiser que seja possível inicializar o objeto com diferentes quantidades de argumentos, exemplo:
```java
  public class Pessoa {
    private String nome;
    private int idade;
    private char sexo;

    public Pessoa(){
    }

    public Pessoa(String nome, int idade, char sexo){
      this.nome = nome;
      this.idade = idade;
      this.sexo = sexo;
    }

    public Pessoa(String nome, int idade){
      this.nome = nome;
      this.idade = idade;
    }

    // temos 3 tipos de construtores, e posso inicializar o objeto de diferentes maneiras, como new Pessoa("alan", 19), ou new Pessoa();
```
- para referenciar o construtor dentro da própria classe, usamos o this();
```java
  public class Pessoa {
    private String nome;
    private int idade;
    private char sexo;

    public Pessoa(String nome, int idade){
      this.nome = nome;
      this.idade = idade;
    }

    public Pessoa(String nome, int idade, char sexo){
      this(nome, idade);
      this.sexo = sexo;
    }
```
- **porém**, só consigo utilizar o this(), dentro de construtores, e ele tem que ser a primeira linha dentro do construtor que está chamando o this().
