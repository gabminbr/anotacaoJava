# Polimorfismo
- upcasting é quando você converte (ou atribui) um objeto de uma subclasse para uma variável do tipo da superclasse, exemplo:
```java
  class Animal {
      void fazerSom() {
          System.out.println("Som genérico");
      }
  }

  class Cachorro extends Animal {
      void fazerSom() {
          System.out.println("Latido");
      }
    
      void correr() {
          System.out.println("Cachorro correndo");
      }
  }

  public class Main {
      public static void main(String[] args) {
          Cachorro c = new Cachorro();

          // Upcasting automático: cachorro vira um animal
          Animal a = c;

          a.fazerSom();  // "Latido" (polimorfismo)

          // a.correr();  --> ERRO! Animal não tem método correr()
      }
  }
```
- Downcasting é quando você converte uma variável do tipo superclasse para o tipo da subclasse, ele não é seguro automaticamente, então é necessário garantir que o objeto seja realmente do tipo da subclasse
- por isso, o downcasting precisa ser feito explicitamente, com a sintaxe de cast, e se errar, vai lançar uma *ClassCastException*, exemplo:
```java
  Animal a = new Cachorro(); // upcasting
  Cachorro c = (Cachorro) a; // downcasting explícito, não dá problema, pois fizemos o cast de um objeto que é Cachorro(só está armazenado numa variável do tipo Animal)
  c.correr();
```
- porém cuidado, o objeto tem que ser o mesmo da variavel que estamos atribuindo, mesmo que animal seja a classe pai de cachorro, a variavel é mais especifica que o objeto e pode tentar acessar comandos que a classe pai nao sabe!
```java
  Animal a = new Animal();
  Cachorro c = (Cachorro) a;  // Vai compilar, mas vai lançar ClassCastException em tempo de execução!
```
- para evitar erros de downcasting, usaremos o instanceof:
```java
  if (a instanceof Cachorro) {
    Cachorro c = (Cachorro) a;
    c.correr();
  } else {
    System.out.println("Não é um cachorro!");
  }
```
