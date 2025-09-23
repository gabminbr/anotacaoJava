# Errors
- todas as exceções em java herdam da classe Throwable, e da classe Throwable se divide em Errors e Exception
- os errors são problemas que você não consegue tratar durante o código, voce nao consegue escrever o que o programa deve fazer caso aquilo ocorra
- normalmente são problemas mais graves, por exemplo o OutOfMemoryError, que diz que acabou a memória.

# Exceptions
- as exceções por sua vez, *Exception* é uma classe que herda de Throwable, e tem tambem sua subclasse RunTimeException.
## Checked 
- elas são *filhas* da classe Exception diretamente.
- são exceções que o compilador obriga você a tratar (ou declarar que lança)
- Geralmente representam situações que o programa pode esperar que aconteçam e deve se preparar para elas
- Exemplo: IOException (problema ao ler ou abrir arquivo)
- Para essas, você precisa usar try-catch ou adicionar throws na assinatura do método, senão o código nem compila.
## Unchecked 
- elas são filhas da RunTimeException, que por sua vez é filha de Exception, e não necessitam ser tratadas obrigatoriamente.

# Try - Catch
- o bloco try catch vai ser o que usaremos para lidar com as exceções, é o que deve ter quando no código teremos uma Exception do tipo checked.
- o catch inclusive, pode ter vários catch se quiser capturar varias excecoes, porém as excecoes de cima pra baixo tem que ser da menos generica para a mais generica.
- uso:
```java
  public class Teste{
    public static void main(String[] args){

    }

    private static void criarNovoArquivo(){
      // se criarmos esse objeto, vai acusar erro pois o método create new file lança uma IOException.
      File file = new File("arquivo");
      file.createNewFile(); 
    }
  }
```
```java
  public class Teste2{
    public static void main(String[] args){

    }

    private static void criarNovoArquivo(){
      // logo, para resolver o problema, teremos que fazer o try catch:
      File file = new File("arquivo");
      try{
        file.createNewFile();
      } catch (IOException e){
        System.out.println("deu erro");
      }
    }
```
# Bloco Finally
- o bloco finally vem em conjunto do try catch, ele basicamente vai ser o bloco que vai ser sempre executado, independente de ter dado exceção ou não:
```java
  import java.io.File;
  import java.io.FileNotFoundException;
  import java.util.Scanner;

  public class ExemploFinally {
      public static void main(String[] args) {
        Scanner leitor = null; // Declarado aqui para ser acessível no finally
        try {
            System.out.println("Tentando abrir o arquivo...");
            File arquivo = new File("documento.txt");
            leitor = new Scanner(arquivo);
            
            // Simula a leitura do arquivo
            System.out.println("Lendo o arquivo: " + leitor.nextLine());

        } catch (FileNotFoundException e) {
            System.err.println("Oops! O arquivo não foi encontrado.");

        } finally {
            System.out.println("Executando o bloco finally...");
            if (leitor != null) {
                leitor.close(); // Garante que o leitor seja fechado
                System.out.println("Arquivo fechado com sucesso.");
            }
        }
    }
  }
```
# Try With Resources
- entretanto, depois do java 7, foi criado o try-with-resources, que meio que anula a necessidade do finally, vamos comparar primeiro sem ele, e depois usando ele:
```java
  Scanner leitor = null;
  try {
    leitor = new Scanner(new File("documento.txt"));
    // ... código para ler o arquivo ...

  } catch (FileNotFoundException e) {
    System.err.println("Arquivo não encontrado.");

  } finally {
    if (leitor != null) {
        leitor.close();
    }
  }
```
```java
  try (Scanner leitor = new Scanner(new File("documento.txt"))) {
    // 1. O recurso (Scanner) é declarado nos parênteses do try.
    
    // ... código para ler o arquivo ...

  } catch (FileNotFoundException e) {
    System.err.println("Arquivo não encontrado.");
  }
  // 2. O bloco finally desaparece! O Java fecha o leitor para você.
```
# Lançar Exceções
- quando por exemplo, criamos um método que pode lançar exceções, porém não queremos tratar dela naquele método em si, por uma questão de lógica e arquitetura, podemos fazer uma *assinatura* no método, que indica que aquele método vai lançar uma exceção, e vai ser responsabilidade daquele que chamou ele, tratar, exemplo:
```java
  // 1. O "throws Exception" AVISA sobre o risco.
  public void sacar(double valor) throws Exception {
    
    if (valor <= 0) {
        // 2. O "throw new" LANÇA o erro e para o método aqui.
        throw new Exception("O valor do saque deve ser positivo.");
    }
    
    if (valor > this.saldo) {
        throw new Exception("Saldo insuficiente.");
    }

    this.saldo = this.saldo - valor;
    System.out.println("Saque realizado com sucesso.");
  }
```
- *throw*: É a ação de lançar a exceção. Ela é usada dentro do método para criar e disparar o erro.
- *throws*: É o aviso. Ela é usada na assinatura do método para avisar a quem for usá-lo que "este método pode, sob certas condições, lançar este tipo de exceção".
- No último exemplo, usamos uma exceção muito genérica, o que é um problema para os desenvolvedores, pois temos que tratar, agora um exemplo com uma exceção mais "certa" e tratando ela no codigo que chamou:
```java
  // Agora avisamos que o erro é sobre um argumento inválido.
  public void sacar(double valor) throws IllegalArgumentException {
    
    if (valor <= 0) {
        throw new IllegalArgumentException("O valor do saque deve ser positivo.");
    }
    
    if (valor > this.saldo) {
        // O ideal aqui seria uma exceção customizada, mas vamos manter esta por enquanto.
        throw new IllegalArgumentException("Saldo insuficiente.");
    }

    this.saldo = this.saldo - valor;
  }

  // na classe que chamou, faremos:
  try {
    conta.sacar(valor);
  } catch (IllegalArgumentException e) {
    // Se o erro for um argumento inválido, a culpa é da entrada de dados.
    System.out.println("Erro de entrada: " + e.getMessage());

  } catch (SaldoInsuficienteException e) { // Supondo que criamos essa exceção.
    // Se o erro for saldo insuficiente, é uma falha na regra de negócio.
    System.out.println("Operação não permitida: " + e.getMessage());
  }
```
# Criação de Exceções
- podemos criar nossa própria exceção, também, basta herdar do tipo (checked/unchecked) de exceção que queremos:
```java
  // 1. Nossa classe herda de 'Exception', tornando-se uma exceção do tipo 'checked'.
  public class SaldoInsuficienteException extends Exception {

    // 2. Criamos um construtor que recebe a mensagem de erro.
    public SaldoInsuficienteException(String mensagem) {
      // 3. A palavra 'super' passa a mensagem para o construtor da classe pai (Exception).
          super(mensagem);
    }
}
```
- agora está pronta para uso, podemos fazer tanto um throw new SaldoInsuficienteException(msg) quanto um catch.
