## 1. TIPOS DE DADOS

``QUALITATIVA NOMINAIS`` - Atributos sem nenhum tipo de ordem.
```
Exemplo: Sexo, Estado civil, País de origem, Ser fumante ou não.
```

``QUALITATIVA ORDINAL`` - Atributos com algum tipo de ordem ou grau:
```
Exemplo: Escolaridade, Classe social, Status de pedido.
```

``QUANTITATIVA DISCRETA`` - Valores númericos inteiros.
```
Exemplo: Idade em anos inteiros, Número de filhos, Quantidade de vendas.
```
  
``QUANTITATIVA CONTÍNUA`` - Valores numéricos racionais.
```
Exemplo: Salário, Preço, Temperatura.
```

<br>

## 2 DISTRIBUIÇÃO DE FREQUÊNCIAS

### 2.1 QUALITATIVAS (tabela cruzada)

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

porcentagem_cruzada = pd.crosstab(dados['Sexo'], dados['Cor'], normalize=True) * 100
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

**Agora fazemos a tabela de frequência normalmente**
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

<br>

### 2.3 QUANTITATIVAS (classes de amplitude fixa)
``Regra de Sturges``

![image](https://github.com/OtavioSotnas/Estatistica/assets/142911747/b9c46532-26f2-4ae9-ac3e-4d507eebaa96)

**Caso não definirmos as faixas, podemos utilizar a fórmula de Sturges**
```python
import numpy as np

n = dados.shape[0]
k = 1 + 10/3 * np.log10(n)
k = int(np.ceil(k)) # Devemos sempre arredondar o valor de k para cima
```
**Agora podemos fazer a tabela normalmente**
```python
frequencia = pd.cut(x = dados.Renda, bins = k).value_counts(sort=False)
percentual = pd.cut(x = dados.Renda, bins = k).value_counts(normalize=True) * 100

pd.DataFrame({'Frequencia': frequencia, 'Porcentagem (%)': round(percentual,2)})
```
|       Renda       | Frequencia | Porcentagem (%) |
|-------------------|------------|-----------------|
| (-200.001, 11111.111] |   75583    |      98.36      |
| (11111.111, 22222.222] |   1023     |       1.33      |
| (22222.222, 33333.333] |    165     |       0.21      |
| (33333.333, 44444.444] |    30      |       0.04      |
| (44444.444, 55555.556] |    17      |       0.02      |
| (55555.556, 66666.667] |     7      |       0.01      |
| (66666.667, 77777.778] |     0      |       0.00      |
| (77777.778, 88888.889] |     4      |       0.01      |
| (88888.889, 100000.0]  |     7      |       0.01      |
| (100000.0, 111111.111] |     0      |       0.00      |
| (111111.111, 122222.222] |     1      |       0.00      |
| (122222.222, 133333.333] |     0      |       0.00      |
| (133333.333, 144444.444] |     0      |       0.00      |
| (144444.444, 155555.556] |     0      |       0.00      |
| (155555.556, 166666.667] |     0      |       0.00      |
| (166666.667, 177777.778] |     0      |       0.00      |
| (177777.778, 188888.889] |     0      |       0.00      |
| (188888.889, 200000.0]  |     3      |       0.00      |

Nota-se que essa distribuição esta estranha devido aos outliers

<br>

## 3 MEDIDAS DE TENDÊNCIA CENTRAL

| Matérias   | Fulano | Beltrano | Sicrano |
|------------|--------|----------|---------|
| Matemática | 8      | 10.0     | 7.5     |
| Português  | 10     | 2.0      | 8.0     |
| Inglês     | 4      | 0.5      | 7.0     |
| Geografia  | 8      | 1.0      | 8.0     |
| História   | 6      | 3.0      | 8.0     |
| Física     | 10     | 9.5      | 8.5     |
| Química    | 8      | 10.0     | 7.0     |

### 3.1 MÉDIA
Seja $X$ uma variável quantitativa e $x_1,x_2,x_3, ...$ os valores assumidos por X. Define-se média de $\overline{X}$ como sendo :
![image](https://github.com/OtavioSotnas/Estatistica/assets/142911747/a49b7378-0121-4475-9b33-0be2808c323c)

```python
(8 + 10 + 4 + 8 + 6 + 10 + 8) / 7
```

OU

```python
notas['Fulano'].mean()
```

### 3.2 MEDIANA
Quando $n$ for ímpar:

![image](https://github.com/OtavioSotnas/Estatistica/assets/142911747/795ae277-8ac1-44b6-9e0a-d8a319816ba0)
```python
# Primeiro precisamos ordernar os valores
notas = notas.Fulano.sort_values()

# Depois encontar N e o Elemento Mediano
n = notas.shape[0]
elemento_md = (n + 1) / 2
mediana = notas[elemento_md - 1]
```

Quando $n$ for par:

![image](https://github.com/OtavioSotnas/Estatistica/assets/142911747/b4478557-d4cc-446a-a35f-8068202863d1)

```python
# O comando SAMPLE uma amostra de 6 elementos
notas_beltrano = df.Beltrano.sample(6, random_state = 101)
notas_beltrano = notas_beltrano.sort_values()

n = notas_beltrano.shape[0]
elemento_md = n / 2
mediana = (notas.Beltrano.loc[elemento_md - 1] + notas.Beltrano.loc[elemento_md]) / 2
```

Ou

```python
notas.median()
```
### 3.3 MODA

### 3.4 RELAÇÕES ENTRE MEDIDAS
