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

Consideram o programa como uma função matemática.

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
  + `(eq x (car L))`. Compara **x** com **(car L)**.
  + `T`.
