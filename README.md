# Análise Comparativa: Algoritmo Genético vs. Evolução Diferencial

Este repositório contém o código e a análise de um estudo comparativo entre um Algoritmo Genético (AG) e um algoritmo de Evolução Diferencial (ED) para a otimização de uma função de benchmark complexa. O objetivo foi explorar, otimizar e comparar a eficácia e a eficiência de cada meta-heurística.

## O Problema de Otimização: Função de Rastrigin

O problema central deste estudo é encontrar o mínimo global da **Função de Rastrigin**, uma função não-convexa e multimodal, notoriamente difícil de otimizar. A sua paisagem é composta por um vale parabólico global, mas coberta por um grande número de mínimos locais, que funcionam como "armadilhas" para algoritmos de otimização.

A função é definida matematicamente como:
$$f(\mathbf{x}) = An + \sum_{i=1}^{n} [x_i^2 - A \cos(2\pi x_i)]$$
Onde, para este projeto, utilizou-se `A = 10` e a dimensão de 2 (f(x,y)). O mínimo global conhecido é `f(x) = 0` no ponto `x = [0, 0, ..., 0]`.

## Metodologia Experimental

Para garantir uma análise estatisticamente relevante, foi desenvolvida uma estrutura de testes robusta que consiste em:
1.  Executar cada configuração de algoritmo múltiplas vezes (25 experimentos independentes).
2.  Recolher o melhor valor da função objetivo (`f(x)`) a cada geração para cada experimento.
3.  Consolidar os dados numa tabela `pandas` com a estrutura `Geração vs. Experimento`.
4.  Analisar os resultados através de métricas quantitativas e visuais, incluindo:
    * Gráficos de convergência da média do melhor `f(x)`.
    * Box plots para analisar a distribuição e consistência dos resultados.
    * Cálculo da performance média final e do desvio padrão.
    * Identificação da melhor performance de pico.

## Algoritmos Utilizados

### 1. Algoritmo Genético (AG)
Foi utilizada a biblioteca `geneticalgorithm2`, configurada com uma abordagem elitista. Diversos hiperparâmetros foram testados, incluindo tipos de mutação, tipos de crossover e taxas de probabilidade. Uma das configurações de base mais eficazes encontradas foi:

```python
A melhor configuração de GA foi a 4


```python

algorithm_param_cfg4_com_poda = {
    'max_num_iteration': 108,
    'population_size': 300,
    'mutation_probability': 0.08,
    'mutation_type': 'gauss_by_x',
    'crossover_type': 'uniform',
    'crossover_probability': 0.75,
    'elit_ratio': 0.10,
    'parents_portion': 0.9,
    'selection_type': 'tournament',
}
```

E para atingir o objetivo do trabalho (menor número de gerações) considerei um f(x,y) <= 0.01 = 0 e para isso foram necessário 108 gerações e 300 indivíduos em média.

### 2. Evolução diferencial (DE)
A evolução diferencial, no entanto se demonstrou bem melhor, com 14 gerações e 300 indivíduos em média.

usando os parâmetros:

n_dimensao = 2
params_de_para_poda = {
    'maxiter': 14,
    'popsize': 300 // n_dimensao,
    'strategy': 'best1bin',
    'tol': 0,
}
