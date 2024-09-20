# Simulação de Monte Carlo para Previsão de Preços
Este projeto tem como objetivo comparar o uso de simulações de Monte Carlo para prever os preços de Bitcoin (BTC-USD) e grandes ações.

## Integrantes do grupo:
- Kaiky Alvaro de Miranda RM:98118
- Lucas Rodrigues da Silva RM:98344
- Juan Pinheiro de França RM:552202

## Bibliotecas Necessárias
Para executar este projeto, você precisará das seguintes bibliotecas Python:

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import yfinance as yf
```


## Funções Implementadas
1. ```calcular_retornos_logaritmicos(historico)```

  Calcula os retornos logarítmicos de uma série temporal de preços.


2. ```simular_monte_carlo(historico, simulacoes=1000, periodo=252)```

  Realiza simulações de Monte Carlo para uma série temporal de preços. 

3. ```plotar_simulacoes(simulacoes_df, titulo='Simulações de Monte Carlo', xlabel='Dias de negociação', ylabel='Preço simulado')```

  Gera um gráfico das simulações de Monte Carlo.

4. ```rodar_simulacao_monte_carlo(ticker, start_date, end_date, simulacoes=1000, periodo=252)```

  Executa a simulação de Monte Carlo para um determinado ativo.

5. ```calcular_mape(valores_reais, valores_previstos)```

  Calcula o Erro Percentual Absoluto Médio (MAPE) entre valores reais e valores previstos.

## Como Executar
1. **Baixar os Dados**: Utilize a função ```yf.download``` da biblioteca ```yfinance``` para baixar os dados históricos dos ativos desejados.
2. **Rodar Simulações**: Utilize a função ```rodar_simulacao_monte_carlo``` para executar as simulações de Monte Carlo.
3. **Plotar Resultados**: Utilize a função ```plotar_simulacoes``` para visualizar os resultados das simulações.
4. **Calcular MAPE**: Utilize a função ```calcular_mape``` para calcular o Erro Percentual Absoluto Médio entre os valores reais e previstos.

## Exemplo de Uso
### Simulação para Bitcoin (BTC-USD)

### 1. Obter o gráfico da simulação Monte Carlo
``` 
# Executando a simulação
historico, simulacoes_df = rodar_simulacao_monte_carlo('BTC-USD', '2021-09-19', '2023-09-19')
```

### 2. Obter a MAPE da simulaçao com dados posteriores
```
# Comparando com os valores reais para o novo intervalo
valores_reais_novo = yf.download('BTC-USD', start='2023-09-19', end='2024-09-19')['Close'].dropna().values

# Pegando os valores previstos da simulação
valores_previstos = simulacoes_df.iloc[:, 0].values[1:]  # Usando a primeira simulação

# Ajuste o tamanho dos arrays para que sejam do mesmo tamanho
min_len = min(len(valores_reais_novo), len(valores_previstos))
valores_reais_novo = valores_reais_novo[:min_len]
valores_previstos = valores_previstos[:min_len]

# Calculando o MAPE com os valores ajustados
mape_simulacao = calcular_mape(valores_reais_novo, valores_previstos)
print(f"\nO MAPE da simulação é: {mape_simulacao:.2f}%")
``` 
