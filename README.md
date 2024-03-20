## 1. TIPOS DE DADOS

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

---

## 2 DISTRIBUIÇÃO DE FREQUÊNCIAS

### 2.1 QUALITATIVAS

[``pandas.crosstab()``](https://pandas.pydata.org/pandas-docs/version/0.22/generated/pandas.crosstab.html)

```python
tabela_cruzada = pd.crosstab(dados['Sexo'], dados['Cor'])
```
| Cor/Sexo | 0    | 2     | 4    | 6   | 8     |
|----------|------|-------|------|-----|-------|
| 0        | 256  | 22194 | 5502 | 235 | 25063 |
| 1        | 101  | 9621  | 2889 | 117 | 10862 |

**Podemos renomear as colunas atráves de um dict e transformar em % com ``normalize=True``**
```python
cor = {0:'Indígena', 2:'Branca',4:'Preta',6:'Amarela',8:'Parda', 9:'Sem declaração'}
sexo = {0:'Masculino', 1:'Feminino'}

porcentagem_cruzada = round(pd.crosstab(dados['Sexo'], dados['Cor'], normalize=True) * 100, 2)
porcentagem_cruzada.rename(index=sexo, columns=cor, inplace=True)
```
|  Cor/Sexo | Indígena | Branca | Preta | Amarela | Parda |
|-----------|----------|---------|------|---------|-------|
| Masculino | 0.33     | 28.88   | 7.16 | 0.31    | 32.62 |
| Feminino  | 0.13     | 12.52   | 3.76 | 0.15    | 14.14 |

<br>

### 2.2 QUANTITATIVAS (classes personalizadas)

[``pandas.cut()``](https://pandas.pydata.org/pandas-docs/version/0.22/generated/pandas.cut.html)

**Primeiro criamos uma lista com as faixas de valores incluindo o min e o max**
```python
classes = [dados.Renda.min(), 1_576, 3_152, 7_880, 15_760, dados.Renda.max()]
labels = ['E','D','C','B','A']
```

**E depois fazemos a tabela de frequência normalmente**
```python
frequencia = pd.cut(x = dados.Renda, 
                    bins = classes, 
                    labels = labels, 
                    include_lowest = True
                    ).value_counts()

percentual = 'copia do código acima'.value_counts(normalize=True) * 100
tabela_frequencia = pd.DataFrame({'Frequência' : frequencia, 'Porcentagem (%)' : percentual})
tabela_frequencia.sort_index(ascending=False)
```
| Renda | Frequência | Porcentagem (%) |
|-------|------------|-----------------|
| A     | 608        | 0.79            |
| B     | 2178       | 2.83            |
| C     | 7599       | 9.89            |
| D     | 16700      | 21.73           |
| E     | 49755      | 64.75           |

---

### 2.2 QUANTITATIVAS (classes de amplitude fixa)
