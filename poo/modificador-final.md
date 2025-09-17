# Modificador Final
- no java, podemos usar o *final* para criar constantes, ou seja, quando não queremos que o valor possa ser alterado de forma alguma durante a execução do programa.
- a convenção para a escrita de constantes em java deve ser tudo em uppercase e separados por um upscore(_), ex: NOME_DO_PAI;
- ao usar em variáveis do tipo referência, fazemos com que não seja mais possível mudar a **referência** daquela variável, porém podemos mudar o **conteúdo**.
- ao usar em classes, fará com que aquela classe com o *final* não possa ser herdada mais, ex: public final class Funcionario{}
- e analogamente, ao usar na assinatura de métodos, aquele método NUNCA poderá ser sobrescrito.
