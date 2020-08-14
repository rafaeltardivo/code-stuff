### LBYL ou Look before you leap

Look before you leap (ou olhe antes de pular) foi provavelmente a primeira abordagem para tratamento de exceções que você aprendeu. Nela você não assume riscos e verifica sempre antes de executar.


### Exemplo 1 - Divisão de dois números em C.
```c
#include <stdlib.h>

float divide_numbers(float dividend, float divisor){

    if(divisor == 0){
        printf("Cannot divide by 0!");
        exit(0);
    }

    return dividend/divisor;
}
```

### EAFP

Easier to ask for forgiveness than permission (É mais fácil pedir perdão que permissão) É a abordagem onde se assume que o fluxo correto será o executado na maioria das vezes.


### Exemplo 3 - Divisão de dois números em Python usando EAFP.
```python
def divide_numbers(dividend, divisor):

    try:
        result = dividend/divisor
    except ZeroDivisionError:
        raise ValueError(f"invalid divisor {divisor}")

    return result
```

Analise as duas abordagens com os inputs abaixo:
```bash
2, 2
4, 4
10, 2
4, 0
```


## Obtendo um registro no Django

### EAFP
```python
try:
    p = Pessoa.objects.get(cpf=1)
except Pessoa.DoesNotExist:
    logger.exception("Pessoa nao existe")
except Pessoa.MultipleObjectsReturnes:
    logger.exception("Mais de uma pessoa com o mesmo CPF!")
```

### LBYL
```python
p = Pessoa.objects.filter(cpf=1).first()
# Existe?
# Quantos existem?
# Deveria existir mais que um?
# Devo lançar alguma exceção?
# Que exceção lanço caso não existam registros?
# Que exceção devo lançar caso existam multiplos registros iguais?

```

Referências externas:  

https://docs.quantifiedcode.com/python-anti-patterns/readability/asking_for_permission_instead_of_forgiveness_when_working_with_files.html

https://devblogs.microsoft.com/python/idiomatic-python-eafp-versus-lbyl/






