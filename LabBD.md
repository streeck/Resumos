# Resumo - LabBD

---

## Transação:

- Unidade lógica de processamento no BD.
- Operações: `INSERT`, `DELETE`, `UPDATE`, `SELECT`
- Conjunto de operações de leitura e escrita. Read/write.

---

#### Escalonamento:

- Operações: `read`, `write`, `commit`, `abort`
##### Abort:
- Quando uma transação é abortada, seus efeitos devem ser **descartados**.
##### Efeitos:
- Nos dados: `undo` nos valores escritos pela transação.
- Em outras transações: `abortar` transações que leram valores escritos da transação orignialmente abortada.
- `Commit` garante que a transação não será mais abortada.
- Como evitá-los: Serialização
	- Execução sequencial, ineficiente.

---

#### Recuperação(Restauração)

**Propósito:** manter o banco sempre consistente.

Ao submeter uma transação, o sistema deve garantir que:
> Todas as operações na transação se completem com sucesso e seus efeitos sejam registrados permanentemente.
> **OU**
> A transação não terá absolutamente nenhum efeito sobre o BD ou outras transações.

- Cada transação possui uma área de trabalho que é criada quando iniciada e destruida quando a transação é efetivada ou abortada.

Estratégias em caso de perda por:

1. Falha catastrófica
	- Reconstrução `REDO`. Utilizar backup com *checkpoint* mais próximo da falha.
2. Falha não catastrófica
	- Inconsistência, reverter mudanças `UNDO`.
		1. Atualização adiada.
			- Banco atualizado depois do `commit`.
			- Caso a transação falhe antes do `commit` **não** é necessário o `REDO` pois ela ainda não foi escrita efetivamente no banco.
			- Nunca será necessário `UNDO` e o `REDO` é necessário em alguns casos.
		2. Atualização imediata.
			- Banco atualizado para alguns casos antes do `commit`.
			- As atulizações são feitas no *log* antes de serem aplicadas no banco, para tornar a recuperação possível.
			- Caso a transação falhe após registrar algumas operações no banco, mas antes de ter alcançado o `commit`, tais operações devem ser desfeitas, ou seja um `rollback` deve ser feito.
			- `UNDO` e `REDO` necessários para o caso de falhas.

---

#### Controle de concorrência

- Evitar os seguintes problemas:
	- `Atualização perdida`, `Atualização temporária`, `Agregação incorreta`, `Leitura não repetida`
- Transação só pode realizar suas operações após receber um ***Grant***
- Técnicas de bloqueio: `lock`
	- Uma transação ***T*** deve reaizar uma operação de `lock-S(Q)` ou `lock-X(Q)` antes de qualquer `read(Q)` ou `write(Q)` em ***T***.
- Protocolo de bloqueio de 2 fases.
	- **Fase 1:** a transação realiza bloqueios mas **não** os libera.
	- **Fase 2:** a transação libera seus bloqueios e **não** pode mais realizar bloqueios.
> Garante **seriabilidade** mas pode causar ***Deadlock***

##### Deadlock
> Preferível à um estado inconsistente, pois é possível dar um `rollback`.
> Dados incosistentes causam problemas reais que não podem ser tratados.

---

## Segurança

##### Abrangência
> Direito a informação, Informações confidenciais, Implementação, Como utilizar.

##### Possíveis ameaças
> **Perda de:** `integridade`, `disponibilidade`, `confidencialidade`.

##### Medidas de proteção
> **Controle de:** acesso, inferência, fluxo.
> Criptografia

##### Rotinas de segurança
- Criar usuário.
- Conceder privilégios.
- Revogar privilégios.
- Atribuir niveis de segurança.

##### Visões
> Importantes para customizar autorizações e assim  atender as necessidades específicas do usuário.
>> A view deve ser **atualizável** pelo sistema que a implementa.

##### *SQL Injection*
> É um ataque ao banco de dados, no qual um código malicioso é inserido em forma de string que será executado pelo servidor.

Qualquer procedimento que construa instruções SQL deve ser verificado.
Caso o procedimento esteja vulnerável, todas as consultas sintaticamente válidas serão executadas.

> Antes de um `EXECUTE` com uma string, valide-a.
>> **Nunca** execute um procedimento construido a partir da entrada de um usuário sem validá-lo.

> Evitar dar detalhes de erros para o usuário de forma a expor nomes de tabelas, campos, etc.

---

## Leitura complementar:

##### Transação
- **Capítulo 15** do livro: Silberschatz, Abraham; Korth, Henry F; Sudarshan, S. **Sistema de banco de dados**.
- **Capítulo 17** do livro: Elmasri, Ramez; Navathe, Shamkant B. **Sistemas de banco de dados**.

##### Segurança
- **Capítulo 23** do livro: Elmasri, Ramez; Navathe, Shamkant B. **Sistemas de banco de dados** (4a. Ed.)
