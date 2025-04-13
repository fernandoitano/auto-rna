# Auto RNA: Desenvolvimento Automático de Redes Neurais utilizando Algoritmos Genéticos

Este repositório contém a implementação desenvolvida na tese de doutorado "Auto RNA: Desenvolvimento automático de redes neurais utilizando algoritmos genéticos" por Fernando Itano.

A primeira versão deste código foi desenvolvida em conjunto com Eder Fernando Urbinate, e os resultados foram publicados no ICAISC 2023 com o artigo "CNN-LSTM Optimized by Genetic Algorithm in Time Series Forecasting: An Automatic Method to use Deep Learning".

## Visão Geral
Este projeto implementa um framework para otimizar automaticamente arquiteturas de redes neurais (CNN-LSTM) usando algoritmos genéticos. O algoritmo genético evolui populações de arquiteturas de rede para encontrar configurações otimizadas.

## Estrutura do Projeto
```
/
├── data/                      # Diretório para arquivos de dados
│   ├── Lynx.csv               # Série temporal de população de linces
│   ├── USmonthlysales.csv     # Dados de vendas mensais dos EUA
│   ├── monthly-sunspots.csv   # Dados de manchas solares
│   └── SCI000001.csv          # Dados do índice SCI
├── ensaios/                   # Resultados dos experimentos
├── cnn_lstm_ga_libs.py        # Biblioteca de funções do algoritmo genético
├── main.py                    # Script principal de execução
└── requirements.txt           # Dependências do projeto
```

## Requisitos
```
tensorflow>=2.8.0
keras>=2.8.0
numpy>=1.22.2
pandas>=1.4.1
matplotlib>=3.5.1
scikit-learn>=1.0.2
```

Para instalar as dependências:
```
pip install -r requirements.txt
```

## Como Usar
Execução Básica
Para executar o algoritmo com as configurações padrão:
```
python cnn_lstm_ga.py
```

## Personalização do Dataset
O código está configurado para trabalhar com vários conjuntos de dados de séries temporais. Para mudar o conjunto de dados, modifique a seção de carregamento de dados no script principal:

### Exemplo para usar o dataset Lynx
```
dataset = 'Lynx.csv'
file = f'data/{dataset}'
data = genfromtxt(file, delimiter=',')
data = data[1:len(data)-1]
```

## Configuração dos Parâmetros do Algoritmo Genético
Os principais parâmetros que podem ser ajustados incluem:

```
num_pop = 100       # Tamanho da população
generations = 10    # Número de gerações
p_crossover = 0.75  # Probabilidade de cruzamento
p_mutation = 0.05   # Probabilidade de mutação
```

## Personalização da Arquitetura Neural
O algoritmo genético otimiza diversos parâmetros da arquitetura CNN-LSTM, definidos no conjunto de cromossomos:
```
chromosome_set = ['f1','f3','f4',    # Parâmetros das camadas CNN
                  'k',                # Kernel size
                  'a1','a4',          # Parâmetros de ativação
                  'd1','d3','d4',     # Parâmetros de dropout
                  'op','ep','n',      # Otimizador, épocas, neurônios
                  'rmse', 'loss', 'type']
```

## Interpretação dos Resultados
Após a execução, o algoritmo produz:

1. Modelos salvos: Todos os modelos treinados são salvos no diretório ensaios/[dataset]/cnn_models_[timestamp]/

2. Log de evolução: Um arquivo CSV detalhando o desempenho de cada cromossomo em cada geração

3. Melhor modelo: O modelo com menor RMSE representa a arquitetura CNN-LSTM otimizada para o problema

## Funções da Biblioteca de Algoritmo Genético
O módulo cnn_lstm_ga_libs.py contém as principais funções para a implementação do algoritmo genético:

- generate_population(): Gera a população inicial de cromossomos
- assess_chromosome(): Avalia o desempenho de um cromossomo específico
- elitism_selection(): Seleciona os melhores indivíduos para preservação
- selection_tournament(): Implementa seleção por torneio
- population_crossover(): Realiza operações de cruzamento entre cromossomos
- population_mutation(): Aplica mutações aos cromossomos
- find_cnn(): Verifica se um cromossomo já foi avaliado anteriormente

## Citação
Se você usar este código em sua pesquisa, por favor cite:

```
@phdthesis{itano2023autorna,
  title={Auto RNA: Desenvolvimento automático de redes neurais utilizando algoritmos genéticos},
  author={Itano, Fernando},
  school={Universidade de São Paulo},
  year={2025}
}
```

## Licença
Este projeto está licenciado sob a licença MIT - veja o arquivo LICENSE para detalhes.

## Contato
Fernando Itano - f.itano@gmail.com
Link do projeto: https://github.com/fernandoitano/auto-rna
