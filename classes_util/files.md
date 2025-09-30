# Arquivos (pacote NIO)
- assim como datas, a forma de trabalhar com arquivos em Java evoluiu, antes era usado o pacote java.io, porém hoje se recomenda o uso da java.nio.

## Ler arquivos
- usaremos duas classes principais: *Paths* (que vai ser uma classe para criar um objeto que representa o path do arquivo) e *Files* (que vai conter de fato os métodos para operar sobre os arquivos).
- exemplo, imagine que exista um arquivo chamado meu-arquivo.txt com o seguinte conteúdo:
```
  Olá, Instrutor Java!
  Esta é a segunda linha.
  Fim.
```
- o método mais simples para ler um arquivo de texto pequeno é o Files.readAllLines(), vai ler todas as linhas do arquivo e retornar em uma List<String>;
```java
  import java.io.IOException;
  import java.nio.file.Files;
  import java.nio.file.Path;
  import java.nio.file.Paths;
  import java.util.List;
  
  public class LeitorDeArquivo {
      public static void main(String[] args) {
  
          // 1. Crie o objeto Path que representa o arquivo
          Path caminhoDoArquivo = Paths.get("meu-arquivo.txt");
  
          try {
              // 2. Leia todas as linhas do arquivo
              List<String> linhas = Files.readAllLines(caminhoDoArquivo);
  
              System.out.println("--- Conteúdo do Arquivo ---");
  
              // 3. Percorra a lista e imprima cada linha
              for (String linha : linhas) {
                  System.out.println(linha);
              }
  
          } catch (IOException e) {
              // 4. Trate possíveis erros (ex: arquivo não encontrado)
              System.err.println("Erro ao ler o arquivo: " + e.getMessage());
          }
      }
  }
```
- esse exemplo serviu para entender como mexer com arquivos pequenos, para arquivos grandes, usaremos o *Files.lines()*, ele não vai ler nada para a memória ainda, vai abrir o arquivo e nos dar um Stream<String>, que é como um "encanamento" por onde as linhas vão passar uma a uma.
- Essa Stream vai precisar ser fechada para que o arquivo seja liberado, Stream vai funcionar como uma esteira para lidar com um arquivo muito grande, ele vai carregar o arquivo em pequenas partes e a medida q termina a tarefa vai passando pra próxima, usaremos o try-with-resources.
```java
  import java.io.IOException;
  import java.nio.file.Files;
  import java.nio.file.Path;
  import java.nio.file.Paths;
  import java.util.stream.Stream;
  
  public class LeitorArquivoGrande {
      public static void main(String[] args) {
          Path caminho = Paths.get("arquivo_grande.txt");
  
          // Esta é a forma correta de usar o try-with-resources com arquivos
          try (Stream<String> streamDeLinhas = Files.lines(caminho)) {
  
              System.out.println("Processando o arquivo grande linha por linha:");
              
              // O método forEach processa cada linha do stream, uma por vez.
              // Isso usa uma quantidade mínima de memória!
              streamDeLinhas.forEach(System.out::println);
  
          } catch (IOException e) {
              System.err.println("Erro ao ler o arquivo: " + e.getMessage());
          }
      }
  }
```

## Escrever em Arquivos
- vamos usar o *Files.writeString()*.
- exemplo, existe um documento chamado log.txt:
```java
  import java.io.IOException;
  import java.nio.file.Files;
  import java.nio.file.Path;
  import java.nio.file.Paths;
  import java.nio.file.StandardOpenOption;
  
  public class EscritorDeArquivo {
      public static void main(String[] args) {
  
          Path caminhoDoArquivo = Paths.get("log.txt");
          String textoInicial = "--- INÍCIO DO LOG ---" + System.lineSeparator() + "Processo iniciado.";
  
          try {
              // 1. Escrevendo no arquivo.
              // Por padrão, este método CRIA um arquivo novo ou SOBRESCREVE um existente.
              Files.writeString(caminhoDoArquivo, textoInicial);
              System.out.println("Arquivo 'log.txt' criado com sucesso.");
  
              // 2. Adicionando mais texto ao final do arquivo.
              // Para isso, usamos uma "opção" a mais no método.
              String textoAdicional = System.lineSeparator() + "Processo finalizado.";
              Files.writeString(caminhoDoArquivo, textoAdicional, StandardOpenOption.APPEND);
              System.out.println("Texto adicional inserido no final do arquivo.");
  
  
          } catch (IOException e) {
              System.err.println("Erro ao escrever no arquivo: " + e.getMessage());
          }
      }
  }
```
- Files.writeString(caminho, texto): A forma mais simples. Cria/sobrescreve o arquivo com o texto.
- System.lineSeparator(): É a forma correta de adicionar uma quebra de linha que funciona em qualquer sistema operacional (Windows, Linux, etc.).
- StandardOpenOption.APPEND: Este é o ponto chave. É um parâmetro extra que diz ao método para adicionar o conteúdo ao final do arquivo (append), em vez de sobrescrevê-lo.

## Verificar Arquivos
```java
  import java.io.IOException;
  import java.nio.file.Files;
  import java.nio.file.Path;
  import java.nio.file.Paths;
  
  public class VerificadorDeArquivo {
  
      public static void main(String[] args) {
          Path caminho = Paths.get("log.txt");
          // Para testar o caso de um diretório, você poderia usar Paths.get(".");
          // O "." representa o diretório atual.
  
          System.out.println("Verificando: " + caminho.toAbsolutePath());
  
          // 1. O mais importante: checar se o arquivo ou diretório existe
          if (Files.exists(caminho)) {
              System.out.println("-> O caminho existe.");
  
              // 2. É um arquivo comum? (não um diretório)
              if (Files.isRegularFile(caminho)) {
                  System.out.println("-> É um arquivo comum.");
                  try {
                      // Aproveitando, vamos ver o tamanho dele
                      long tamanho = Files.size(caminho);
                      System.out.println("-> Tamanho: " + tamanho + " bytes.");
                  } catch (IOException e) {
                      System.err.println("Não consegui ler o tamanho do arquivo.");
                  }
              }
  
              // 3. É um diretório?
              if (Files.isDirectory(caminho)) {
                  System.out.println("-> É um diretório.");
              }
  
          } else {
              System.out.println("-> O caminho NÃO existe.");
          }
      }
  }
```
- Files.exists(path): A verificação mais fundamental. Retorna true se o caminho aponta para algo que existe.
- Files.isRegularFile(path): Retorna true se for um arquivo normal.
- Files.isDirectory(path): Retorna true se for um diretório.
- Files.size(path): Retorna o tamanho do arquivo em bytes. (Note que ele pode lançar uma IOException, por isso o try/catch).
