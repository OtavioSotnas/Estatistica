# Estatistica

## 1 TIPOS DE DADOS
```
QUALITATIVA NOMINAIS: Atrivbutos sem nenhum tipo de ordem.

- Ex: Sexo, Estado civil, País de origem, Ser fumante ou não, etc ...


QUANTITATIVA ORDINAL: Atributos com algum tipo de ordem ou grau:

- Ex: Escolaridade, Classe social, Status de pedido, etc...


QUANTITATIVA DISCRETA: Valores númericos inteiros.

- Ex: Idade em anos inteiros, Número de filhos, Quantidade de vendas, etc ...

  
QUALITATIVA CONTÍNUA: Valores numéricos racionais.

- Ex: Salário, Preço, Temperatura, etc ...
```
## 2 DISTRIBUIÇÃO DE FREQUÊNCIAS

### 2.1 PARA VARIÁVEIS QUALITATIVAS

``Método com CrossTab``
```python
tabela_cruzada = pd.crosstab(dados['Sexo'], dados['Cor'])
```
| Cor/Sexo | 0    | 2     | 4    | 6   | 8     |
|----------|------|-------|------|-----|-------|
| 0        | 256  | 22194 | 5502 | 235 | 25063 |
| 1        | 101  | 9621  | 2889 | 117 | 10862 |

Podemos renomear as colunas atráves de um dict
```python
cor = {0:'Indígena', 2:'Branca',4:'Preta',6:'Amarela',8:'Parda', 9:'Sem declaração'}
sexo = {0:'Masculino', 1:'Feminino'}

tabela_cruzada.rename(index=sexo, columns=cor, inplace=True)
```
| Cor/Sexo | Indígena | Branca | Preta | Amarela | Parda |
|----------|------|-------|------|-----|-------|
| Masculino | 256  | 22194 | 5502 | 235 | 25063 |
| Feminino | 101  | 9621  | 2889 | 117 | 10862 |
