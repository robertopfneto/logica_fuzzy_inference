# Lógica Fuzzy: cálculo de gorjeta

Este notebook foi desenvolvido durante a disciplina de Inteligência Artificial do curso de Ciência da Computação da Universidade Católica Dom Bosco (UCDB), na aula do Prof. Dr. Gustavo da Silva Andrade.

A atividade explora a construção de um sistema de inferência fuzzy para sugerir o percentual de gorjeta em um restaurante, considerando a qualidade da comida e do serviço. A implementação utiliza Python e a biblioteca `scikit-fuzzy`, importada no código como `skfuzzy`.

Aplicar os conceitos de variáveis linguísticas, funções de pertinência e regras de decisão em um exemplo prático, acompanhando a definição das entradas e da saída, a construção do controlador e a simulação do resultado.

## Notebook

O arquivo `logica_fuzzy.ipynb` contém as explicações, o código e as visualizações da atividade.

## Variáveis do sistema

| Variável | Papel | Intervalo | Conjuntos linguísticos no código |
| --- | --- | --- | --- |
| Comida | Entrada | 0 a 10 | `pessima`, `comível`, `deliciosa` |
| Serviço | Entrada | 0 a 10 | `ruim`, `aceitavel`, `excelente` |
| Gorjeta | Saída | 0 a 25% | `baixa`, `media`, `alta` |

## Funções de pertinência utilizadas

| Variável | Conjunto | Função ou método | Parâmetros no código |
| --- | --- | --- | --- |
| Comida | Todos os conjuntos | `automf` | `names=['pessima', 'comível', 'deliciosa']` |
| Serviço | `ruim` | `fuzz.trimf` | `[0, 0, 5]` |
| Serviço | `aceitavel` | `fuzz.gaussmf` | Média `5` e desvio padrão `2` |
| Serviço | `excelente` | `fuzz.gaussmf` | Média `10` e desvio padrão `3` |
| Gorjeta | `baixa` | `fuzz.trimf` | `[0, 0, 13]` |
| Gorjeta | `media` | `fuzz.trapmf` | `[0, 13, 15, 25]` |
| Gorjeta | `alta` | `fuzz.trimf` | `[15, 25, 25]` |

O método `automf` define automaticamente os conjuntos da variável comida. Para as demais variáveis, as funções de pertinência são configuradas manualmente. O notebook também apresenta gráficos dessas funções antes e depois da simulação.

## Regras de decisão

O controlador utiliza três regras:

1. Se o serviço foi excelente **ou** a comida estava deliciosa, então a gorjeta deve ser alta.
2. Se o serviço foi aceitável **ou** a comida estava deliciosa, então a gorjeta deve ser média.
3. Se o serviço foi ruim **e** a comida estava péssima, então a gorjeta deve ser baixa.

As regras são reunidas em um `ControlSystem`, e a simulação é realizada por meio de `ControlSystemSimulation`.

## Como executar

Utilize um ambiente Python com suporte a notebooks, como Jupyter Notebook, JupyterLab ou VS Code com a extensão Jupyter.

Instale as dependências no ambiente que será utilizado pelo notebook:

```bash
python -m pip install numpy scipy matplotlib "networkx>=3.0" scikit-fuzzy jupyter
```

Para abrir pelo Jupyter Notebook, execute na pasta do arquivo:

```bash
jupyter notebook logica_fuzzy.ipynb
```

Execute as células na ordem em que aparecem. Se as dependências já estiverem instaladas, a célula de instalação do notebook pode ser pulada.

## Exemplo de simulação

O exemplo presente no notebook utiliza as seguintes entradas:

```python
gorjeta_simulador.input['comida'] = 5
gorjeta_simulador.input['servico'] = 9.4
```

Após a execução de `gorjeta_simulador.compute()`, a saída registrada no notebook é de aproximadamente **18,58% de gorjeta**.

Para explorar o comportamento do sistema, altere os valores de entrada dentro do intervalo de 0 a 10 e execute novamente as células de cálculo e visualização.

## Contexto acadêmico

- Roberto Pereira de Freitas Neto, Atualizado em 26/10/2026
