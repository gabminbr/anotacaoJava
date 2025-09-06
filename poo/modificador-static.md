# Modificador Static 
- é usado para criar membros (variáveis e métodos) que pertencem à classe em vez de pertencerem a instâncias individuais (objetos).
- **variáveis estáticas**: cria uma variável que vai ser compartilhada por todas as instâncias, exemplo:
```java
  public class Contador {
    // Variável estática - compartilhada por todas as instâncias
    private static int totalInstancias = 0;
    
    // Variável de instância - única para cada objeto
    private int id;
    
    public Contador() {
        totalInstancias++; // Incrementa o contador compartilhado
        id = totalInstancias;
    }
    
    public static int getTotalInstancias() {
        return totalInstancias;
    }
    
    public int getId() {
        return id;
    }
  }

  // Uso:
  Contador c1 = new Contador();
  Contador c2 = new Contador();
  Contador c3 = new Contador();

  System.out.println(c1.getId()); // 1
  System.out.println(c2.getId()); // 2
  System.out.println(c3.getId()); // 3
  System.out.println(Contador.getTotalInstancias()); // 3
```
- se eu usar um set e mudar o valor dessa variavel estatica para um objeto, vai mudar o valor dela para TODOS os objetos que pertençam a mesma classe.
- para fazer referência a ela agora dentro da classe, ao invés de usarmos this.variavel, usaremos NomeDaClasse.variavel, pois agora ela pertence a **classe** e não a instância.

# Métodos Estáticos
- métodos estáticos seguem o mesmo modelo das variáveis, permite você acessar o método sem ter a necessidade de criar a instância, porém, dentro de um método estático, você só pode acessar variáveis estáticas, e não pode acessar variáveis de instância.

# Bloco de Inicialização Estático
- o bloco de inicialização sendo estático, só será executado uma vez, logo, só pode acessar variáveis e métodos também estáticos, pois na ordem de execução da JVM, esse bloco vai ser executado antes de serem alocadas memórias para os atributos de instância.
