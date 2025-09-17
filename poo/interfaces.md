# Interfaces
- uma interface serve como um 'contrato' que as classes que implementam ela, têm de sobrescrever todos os métodos que estão contidos nessa interface, exemplo:
```java
  public interface Animal{
    void comer();
    void dormir();
  }

  // para uma classe implementar ela, deve usar a palavra *implements*
  public class Cachorro implements Animal{
    @Override
    public void comer(){
      System.out.println("AU");
    }

    @Override
    public void dormir(){
      System.out.println("auu..");
    }
```
- os métodos nas interfaces podem ou não ter o corpo (a partir do Java 8), com o uso do *default*:
```java
  public interface Veiculo{
    void acelerar();

    default void buzinar(){ // a classe que implementar pode escolher se sobrescreve ou não esse método
      System.out.println("BIIIII");
    }
  }
```
- uma classe pode herdar e implementar ao msm tempo, e embora não possa herdar de mais de uma classe, ele pode implementar de mais de uma interface.
- em interfaces também pode ter atributos (por obrigação eles serão public static final) e métodos estáticos (só podem ser chamados pela interface).
