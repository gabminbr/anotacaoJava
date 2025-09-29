# Data e Hora
- Para lidar com isso, no pacote *java.time* temos 3 classes para tal:
- LocalDate: para lidar com datas.
- LocalTime: para lidar com o tempo.
- LocalDateTime: para lidar com ambos.

- para pegar o atual, usaremos o método estático *.now()*:
```java
  // Para pegar a data e hora ATUAIS
  LocalDate dataDeHoje = LocalDate.now();
  LocalTime horaAtual = LocalTime.now();
  LocalDateTime dataEHoraAtual = LocalDateTime.now();
  
  System.out.println("Hoje é: " + dataDeHoje);
  System.out.println("Agora são: " + horaAtual);
  System.out.println("Data e hora completas: " + dataEHoraAtual);

  /* saída:
  Hoje é: 2025-09-29 -> note que sai sempre no formato ANO-MÊS-DIA
  Agora são: 08:29:03.123456
  Data e hora completas: 2025-09-29T08:29:03.123456
  */
```
- e para datas específicas? usaremos o *.of()*:
```java
  // Criando uma data específica (um marco na história do Brasil)
  LocalDate diaDaIndependencia = LocalDate.of(1822, 9, 7);
  System.out.println("Dia da Independência: " + diaDaIndependencia);
  
  // Criando um horário específico
  LocalTime horaDoAlmoco = LocalTime.of(12, 30); // 12h30
  System.out.println("Horário do almoço: " + horaDoAlmoco);
  
  // Juntando os dois com LocalDateTime
  LocalDateTime momentoExato = LocalDateTime.of(1822, 9, 7, 12, 30);
  System.out.println("Momento exato: " + momentoExato);

  /* saída:
  Dia da Independência: 1822-09-07
  Horário do almoço: 12:30
  Momento exato: 1822-09-07T12:30
  */
```
- lembrando que esses objetos são imutáveis, logo, sempre que fazemos um método para alterar a data/hora.
- bem óbvio, para adicionar dias, horas etc, usaremos *.plusDays(numero)*, *.plusWeeks(numero)*, *.plusHours(numero)*, e para tirar, analogamente, usamos *.minusDays()*;
- se quisermos formatar uma data para o jeito que queremos, usaremos a classe *DateTimeFormatter*, os símbolos são: dd(dia com 2 dígitos), MM(mês com 2 dígitos), yyyy(ano), HH(hora com 2 dígitos), mm(minutos), ss(segundos):
```java
  // 1. Nossa data e hora
  LocalDateTime agora = LocalDateTime.now();
  
  // 2. Criamos o formatador com o padrão desejado
  DateTimeFormatter formatador = DateTimeFormatter.ofPattern("dd/MM/yyyy 'às' HH:mm:ss");
  
  // 3. Usamos o método .format() para transformar nosso objeto em texto
  String dataFormatada = agora.format(formatador);
  
  System.out.println("Data sem formatação: " + agora);
  System.out.println("Data com formatação: " + dataFormatada);

  /* saída
  Data sem formatação: 2025-09-29T09:21:45.123
  Data com formatação: 29/09/2025 às 09:21:45
  */
```
- podemos fazer o caminho inverso também:
```java
  String textoData = "07/09/1822";
  DateTimeFormatter formatadorDeData = DateTimeFormatter.ofPattern("dd/MM/yyyy");
  
  LocalDate dataDoTexto = LocalDate.parse(textoData, formatadorDeData);
  
  System.out.println("O texto foi convertido para um objeto LocalDate: " + dataDoTexto);
```
## Duração / Período
- Period: Usamos para medir a diferença em anos, meses e dias. É ideal para datas de calendário (LocalDate). Pense em "Qual a idade de uma pessoa?"
- Duration: Usamos para medir a diferença em horas, minutos e segundos (uma quantidade exata de tempo). É ideal para LocalDateTime ou LocalTime. Pense em "Quanto tempo uma tarefa demorou para ser executada?"
- *period* exemplo:
```java
  LocalDate dataNascimento = LocalDate.of(1995, 5, 23);
  LocalDate hoje = LocalDate.now();

  Period idade = Period.between(dataNascimento, hoje);  
  System.out.println("O período calculado é: " + idade);

  // saída: P30Y4M6D
```
- exemplo completo agora pegando coisas especificas do data:
```java
  import java.time.LocalDate;
  import java.time.Period;
  
  public class CalculoIdade {
      public static void main(String[] args) {
          LocalDate dataNascimento = LocalDate.of(1995, 5, 23);
          LocalDate hoje = LocalDate.now();
  
          Period idade = Period.between(dataNascimento, hoje);
  
          System.out.printf("Você tem %d anos, %d meses e %d dias.%n",
              idade.getYears(),
              idade.getMonths(),
              idade.getDays());
      }
  }
```
- *duration* exemplo:
```java
  import java.time.LocalTime;
  import java.time.Duration;
  
  public class MedirTempo {
      public static void main(String[] args) {
          LocalTime inicio = LocalTime.of(10, 0, 0);
          LocalTime fim = LocalTime.of(10, 0, 15);
  
          Duration duracao = Duration.between(inicio, fim);
          System.out.println("Duração padrão: " + duracao);
      }
  }

  // saída: PT15S
```
