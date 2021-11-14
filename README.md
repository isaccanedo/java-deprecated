# 1. Visão Geral
Neste tutorial rápido, veremos APIs obsoletas em Java e como usar a anotação @Deprecated.

# 2. A anotação @Deprecated
Conforme um projeto evolui, sua API muda. Com o tempo, existem certos construtores, campos, tipos ou métodos que não queremos mais que as pessoas usem.

Em vez de quebrar a compatibilidade com versões anteriores da API do projeto, podemos marcar esses elementos com a anotação @Deprecated.

@Deprecated diz a outros desenvolvedores que o elemento marcado não deve mais ser usado. É comum também adicionar algum Javadoc ao lado da anotação @Deprecated para explicar o que seria uma alternativa melhor que atende ao comportamento correto:

```
public class Worker {
    /**
     * Calculate period between versions
     * @deprecated
     * This method is no longer acceptable to compute time between versions.
     * <p> Use {@link Utils#calculatePeriod(Machine)} instead.
     *
     * @param machine instance
     * @return computed time
     */
    @Deprecated
    public int calculate(Machine machine) {
        return machine.exportVersions().size() * 10;
    }
}
```

Lembre-se de que um compilador só exibe o aviso de API obsoleta se o elemento Java anotado for usado em algum lugar do código. Portanto, neste caso, só apareceria se houvesse um código que chamasse o método de cálculo.

Além disso, podemos comunicar o status de descontinuado na documentação também usando a tag Javadoc @deprecated.

# 3. Atributos opcionais adicionados em Java 9
Java 9 adiciona alguns atributos opcionais à anotação @Deprecated: since e forRemoval.

O atributo since requer uma string que nos permite definir em qual versão o elemento foi preterido. O valor padrão é uma string vazia.

E forRemoval é um booleano que nos permite especificar se o elemento será removido na próxima versão. Seu valor padrão é falso:

```
public class Worker {
    /**
     * Calculate period between versions
     * @deprecated
     * This method is no longer acceptable to compute time between versions.
     * <p> Use {@link Utils#calculatePeriod(Machine)} instead.
     *
     * @param machine instance
     * @return computed time
     */
    @Deprecated(since = "4.5", forRemoval = true)
    public int calculate(Machine machine) {
        return machine.exportVersions().size() * 10;
    }
}
```

Simplificando, o uso acima significa que o calculador foi descontinuado desde 4.5 de nossa biblioteca e que está programado para remoção na próxima versão principal.

É útil adicionarmos isso, pois o compilador nos dará um aviso mais forte se descobrir que estamos usando um método com esse valor.

E já existe suporte de IDEs para detectar usos de um método marcado com forRemoval = true. O IntelliJ, por exemplo, risca o código com uma linha vermelha em vez de preta.

# 4. Conclusão
Neste artigo rápido, vimos como usar a anotação @Deprecated e seus atributos opcionais para marcar o código que não deve mais ser usado