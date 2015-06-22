# Resumo - Paradigmas de Linguagens de Programação

---

## Linguagens Funcionais

Consideram o programa como uma função matemática.

## Lisp

> Primeira linguagem funcional.
>> Tudo é representado por listas. O próprio programa, funções e dados utilizados.
>> Listas são representadas por `( )`.

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
- `cond` é um `if` para manipular várias expressões. No caso temos 3 expressões:
  + `(null L)`. Caso esta expressão seja verdadeira, `cond` retorna `nil`.
  + `(eq x (car L))`
  + `T`.
