# Estatistica

## 1 TIPOS DE DADOS
```
QUANTITATIVA ORDINAL: Podem ser ordenadas ou hierarquizardas.

- Ex: Grau de escolaridade e Faixas de idade

  
QUALITATIVA NOMINAIS: Não podem ser ordenadas ou hierarquizardas.

- Ex: Estados, Sexo e Cores

  
QUANTITATIVA DISCRETA: Representam uma contagem de um conjunto finito.

- Ex: Anos completos, Nº de filhos e Qtd carros vendidos

  
QUALITATIVA CONTÍNUA: Asumem valores em uma escala contínua.

- Ex: Idade exata com meses e dias, Altura, Peso e Tempo
```
## 2 DISTRIBUIÇÃO DE FREQUÊNCIAS

### 2.1 PARA VARIÁVEIS QUALITATIVAS

- Método com CrossTab
```python
tabela_cruzada = pd.crosstab(dados['Sexo'], dados['Cor'])
```
Output:

| Cor/Sexo | 0    | 2     | 4    | 6   | 8     |
|----------|------|-------|------|-----|-------|
| 0        | 256  | 22194 | 5502 | 235 | 25063 |
| 1        | 101  | 9621  | 2889 | 117 | 10862 |
