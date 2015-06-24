# Resumo - Paradigmas de Linguagens de Programação

##### Linguagens Funcionais
Estudar o texto da apostila + artigo _"Algebraic Data Type"_

##### _Prolog_
- Seção ~~5.5 Manipulação da Base de Dados~~
- Seção 5.6 Aspectos Não Lógicos de _Prolog_. **(Opcional)**
  + Explicar algum exemplo como os desta seção, no entanto tal explicação pode ser feita apenas com conhecimentos de seções anteriores.
- `cut` e `fail` será exigido apenas como eles funcionam.
  + ~~discussão de eficiência e cuts vermelhos/verdes~~

##### Linguagens Baseadas em Fluxos de Dados

---

## Linguagens Funcionais

Consideram o programa como uma função matemática. Todas as computações são feitas por funções que recebem como parâmetros outras funções.
Conceito de variável não existe. Não há atribuição.

O professor discorre na apostila sobre o paradigma imperativo, etc.

##### Como eliminar características dinâmicas de algoritmos?
> Remover o comando de atribuição e consequentemente comandos de repetição como `for` e `while`.

> Não há mais passagem de parâmetro por referência e nem váriaveis globais.
>> Existe no entanto **constantes globais**.

Na passagem de parâmetros o valor dos parâmetros reais é copiado.
> Isto é chamado de **inicialização** que é diferente de atribuição.
>> Inicialização cria uma posição de memória e aloca um valor imediatamente após sua criação.
>> 
>> Após inicializado, o valor armazenado não pode ser modificado.

Mecanismo principal de repetição de código: **recursão**.

##### Diferença entre linguagens Imperativas e Declarativas.
Imperativas:
- Significado depende da dinâmica do programa.

Declarativa:
- Significado estático.

##### Transparência Referencial
> Função cujo valor de retorno depende apenas dos valores dos parâmetros.

O resultado de um trecho não afetará de modo algum outro trecho, a menos que o primeiro trecho seja uma expressão passada como parâmetro ao segundo.

> Visto que não existem efeitos colaterais, uma função em uma Linguagem Funcional retornará sempre o mesmo valor dados os mesmo parâmetros.
>> Logo, é possível avaliar em paralelo funções em uma expressão.
>
> **Exemplo:** `f( g(x), h(x) ) + p(y)`
> 
> Pode-se calcular `g(x)` `h(x)` e `p(y)` ao mesmo tempo.

##### Tudo é função
Inclusive o `if`. Que possui a seguinte forma:

`if exp then exp1 else exp2`

O que é equivalente a uma função de forma explicita:

`(if exp, exp1, exp2)`

### Lisp

> **Primeira linguagem funcional.**
>> Tudo é representado por listas. O próprio programa, funções e dados utilizados.
>> Listas são representadas por `( )`.

> **Dinamicamente Tipada.**
>> Todas as funções são polimórficas.

>> Podem ocorrer erros de tipo em **execução**.

```lisp
(def membro (lambda(x L)
  (cond ((null L) nil)
    ((eq x (car L)) T)
      (T(membro x (cdr L)))
  )
))
```
- Função `membro` que recebe uma lista ***L*** e um valor ***x***.
  + Retorna `true` se o valor se encontra na lista ou `nil` caso contrário.
- `nil == false` em Lisp.
- A função `car` retorna o **primeiro elemento** da lista.
- A função `cdr` retorna a lista **retirando** o primeiro elemento.

**Exemplo:**
```lisp
(car ’(1 2 3)) -> 1
(cdr ’(1 2 3)) -> (2 3)
```
- Comparação de igualdade feito com `eq`
- `cond` é um `if` para manipular várias expressões. No caso temos 3 expressões:
  + `(null L)`. Caso esta expressão seja verdadeira, `cond` retorna `nil`.
  + `(eq x (car L))`. Compara **x** com **(car L)**. Se forem iguais, retorna `true`.
  + `(T(membro x (cdr L)))`. Chamada recursiva.

### Linguagem FP
> Puramente funcional. Não possui variáveis e oferece muitas possibilidades de combinar funções além da composição.

Creio aqui que a única coisa que valha a pena mencionar são os diferentes mecanismos de combinar funções.

1. Composição
2. Construção
3. Aplique a todos
4. Condição
5. Enquanto

### Haskell e SML
> Linguagens funcionais puras, estaticamente tipadas e com alto grau de polimorfismo.

#### SML
> Suporte a tipos básicos: `int`, `boolean`, `String`, etc.
> 
> Listas de forma semelhante a LISP. Exemplo: `[1, 2, 3]`.

Sendo fortemente tipada, listas heterogêneas(elementos de vários tipos) são ilegais.

No entanto, parâmetros de função podem ser declarados sem tipo. Exemplo:
```sml
succ(n) = n + 1
```











