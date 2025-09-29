# Regex
- é uma ferramenta para achar padrões no texto.
## Fundamentos
- Caracteres literais:  regex mais simples é um texto literal. O padrão gato vai encontrar exatamente a sequência de caracteres gato. Simples assim.
- O ponto '.' (curinga universal): Aqui começa a ficar interessante. O ponto . é um "metacaractere" que funciona como um curinga: ele representa qualquer caractere único (letra, número, símbolo, etc.).
ex: c.t, funciona para cot, cat, cit, cet, c&t
- Colchetes [] (curinga específico): podemos criar uma lista de caracteres permitidos para uma única posição:
```
  padrão: b[aiu]g
  encontra: bag, big, bug
  não encontra: beg, bxg, b&g, bog, etc

  podemos criar intervalos com hífens também:
  b[a-z]g
```
- se quisermos deixar opcional o uso ou não de certo caractere, usaremos os **quantificadores**:
```
  ? -> zero ou uma vez (opcional):
    anos?, vai aceitar ano e anos
    co?r, vai aceitar cor e cr

  * -> zero ou mais vezes:
    co*r, encontra cor, cr, coor, cooor

  + -> uma ou mais vezes:
    co+r, encontra cor, coor, cooor, mas não encontra cr.
```
- para achar elementos em linhas específicas como inicio do texto e fim do texto, usaremos as **âncoras**:
```
  ^ (Acento circunflexo): Representa o início de uma linha.
  $ (Cifrão): Representa o fim de uma linha.

  exemplo: queremos achar a palavra Erro mas só se tiver no começo da linha.
  ^Erro, vai encotrar na String "Erro, falha na lógica", porém não vai achar no "Ocorreu um erro".
  para achar no fim usamos o 'erro$'.
```
- exemplo de uso:
```java
  public class ValidadorDeCep {

    public static void main(String[] args) {
        // IMPORTANTE: Em uma String Java, a barra invertida \ é um caractere especial.
        // Para usar o \d, precisamos "escapá-la", escrevendo \\d.
        String regexCep = "\\d{5}-\\d{3}";

        String cepValido = "01001-000";
        String cepInvalido = "abcde-fgh";
        String cepComTextoExtra = "Meu CEP é 01001-000";

        System.out.println("'" + cepValido + "' é válido? " + cepValido.matches(regexCep));
        System.out.println("'" + cepInvalido + "' é válido? " + cepInvalido.matches(regexCep));
        System.out.println("'" + cepComTextoExtra + "' é válido? " + cepComTextoExtra.matches(regexCep));
    }
  }

  /* saída
  '01001-000' é válido? true
  'abcde-fgh' é válido? false
  'Meu CEP é 01001-000' é válido? false
  */
```
