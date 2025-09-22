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
