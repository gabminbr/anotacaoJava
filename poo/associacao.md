# Associação
- temos vários tipos de associação, mas é bem lógico para entendê-las, por exemplo, a associação um para um, basta pensar num jogo (que não permita usar personagens repetidos), um jogador só pode estar relacionado com um personagem, e vice-versa.
- vamos ao exemplo com a relação *time de futebol* com *jogador*:
```java
  public class Jogador{
    private String nome;
    private Time time;
  }

  public class Time{
    private String nome;
    private Jogador[] jogadores;
  }
```

