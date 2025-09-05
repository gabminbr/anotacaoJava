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
- 
