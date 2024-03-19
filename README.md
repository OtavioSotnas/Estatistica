# Estatistica

## 1 TIPOS DE DADOS

``QUALITATIVA NOMINAIS`` - Atrivbutos sem nenhum tipo de ordem.
```
Exemplo: Sexo, Estado civil, País de origem, Ser fumante ou não.
```

``QUANTITATIVA ORDINAL`` - Atributos com algum tipo de ordem ou grau:
```
Exemplo: Escolaridade, Classe social, Status de pedido.
```

``QUANTITATIVA DISCRETA`` - Valores númericos inteiros.
```
Exemplo: Idade em anos inteiros, Número de filhos, Quantidade de vendas.
```
  
``QUALITATIVA CONTÍNUA`` - Valores numéricos racionais.
```
Exemplo: Salário, Preço, Temperatura.
```  
## 2 DISTRIBUIÇÃO DE FREQUÊNCIAS

### 2.1 Para Variáveis Qualitativas

``Método com CrossTab``
```python
tabela_cruzada = pd.crosstab(dados['Sexo'], dados['Cor'])
```
| Cor/Sexo | 0    | 2     | 4    | 6   | 8     |
|----------|------|-------|------|-----|-------|
| 0        | 256  | 22194 | 5502 | 235 | 25063 |
| 1        | 101  | 9621  | 2889 | 117 | 10862 |

- Podemos renomear as colunas atráves de um dict e transformar em % com Normalize
```python
cor = {0:'Indígena', 2:'Branca',4:'Preta',6:'Amarela',8:'Parda', 9:'Sem declaração'}
sexo = {0:'Masculino', 1:'Feminino'}

porcentagem_cruzada = round(pd.crosstab(dados['Sexo'], dados['Cor'], normalize=True) * 100, 2)
porcentagem_cruzada.rename(index=sexo, columns=cor, inplace=True)
```
| Cor/Sexo | Indígena | Branca | Preta | Amarela | Parda |
|----------|------|-------|------|-----|-------|
| Masculino | 0.33  | 28.88 | 7.16 | 0.31 | 32.62 |
| Feminino | 0.13  | 12.52  | 3.76 | 0.15 | 14.14 |
