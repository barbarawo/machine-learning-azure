# machine-learning-azure

Exercício de uso de recurso de aprendizado de máquina automatizado no Azure Machine Learning para treinar e avaliar um modelo de aprendizado de máquina.

## 1. Criei um ML automatizado com as seguintes configurações:
### Configurações básicas:
Nome do trabalho: mslearn-bike-automl

Novo nome do experimento: mslearn-bike-rental

Descrição: Automated machine learning for bike rental prediction

Marcadores: nenhum

### Tipo de tarefa e dados:
Tipo de tarefa: Regressão

Conjunto de dados: crie um novo conjunto de dados com as seguintes configurações:

Tipo de dados:
Nome: bike-rentals
Descrição: Historic bike rental data
Tipo: Tabular

Fonte de dados:
Selecione Dos arquivos da web

URL da Web:
URL da Web: https://aka.ms/bike-rentals

Ignorar validação de dados: não selecionar

Configurações:

Formato de arquivo: Delimitado

Delimitador: Vírgula

Codificação: UTF-8

Cabeçalhos de coluna: apenas o primeiro arquivo possui cabeçalhos

Pular linhas: Nenhum

O conjunto de dados contém dados multilinhas: não selecione

Esquema:
Incluir todas as colunas exceto Caminho
Revise os tipos detectados automaticamente

Selecionei Criar. Após a criação do conjunto de dados, selecionei o conjunto de dados de aluguel de bicicletas para continuar a enviar o trabalho de ML automatizado.

## Configurações de tarefa:

Tipo de tarefa: Regressão

Conjunto de dados: bike-rentals

Coluna de destino: Rentals (integer)

Configurações adicionais:

Métrica primária: raiz do erro quadrático médio normalizado

Explique o melhor modelo: Não selecionado

Usar todos os modelos suportados: Desmarcado.

Modelos permitidos: apenas RandomForest e LightGBM

Limites:

Máximo de testes: 3

Máximo de testes simultâneos: 3

Máximo de nós: 3

Limite de pontuação da métrica: 0,085

Tempo limite: 15

Tempo limite de iteração: 15

Habilitar rescisão antecipada: selecionado

Validação e teste:

Tipo de validação: Train-validation split

Porcentagem de dados de validação: 10

Conjunto de dados de teste: Nenhum

### Calcular:
Selecione o tipo de computação: sem servidor

Tipo de máquina virtual: CPU

Camada de máquina virtual: Dedicada

Tamanho da máquina virtual: Standard_DS3_V2*

Número de instâncias: 1

Enviei o trabalho de treinamento.

## 2. Após constar o status como concluído, revisei o modelo treinado.

## 3. Na guia “modelo”, selecionei “implantar” e usei a opção “serviço Web”, com as seguintes configurações:
Nome: predict-rentals

Descrição: Predict cycle rentals

Tipo de computação: Azure Container Instance

Habilitar autenticação: selecionado

## 4. Após constar o status como êxito, foi testado o serviço implantado.

## 5. No menu esquerdo, cliquei em “Modelos”, no ml criado, em “Pontos de extremidade”, no arquivo criado e, em seguida, em “Testar”, inserindo o seguinte código:
  
    {      
       "Inputs": {     
         "data": [     
       {       
         "day": 1,         
         "mnth": 1,            
         "year": 2022,         
         "season": 2,         
         "holiday": 0,         
         "weekday": 1,         
         "workingday": 1,         
         "weathersit": 2,          
         "temp": 0.3,          
         "atemp": 0.3,         
         "hum": 0.3,         
         "windspeed": 0.3          
       }       
     ]    
    },
    "GlobalParameters": 1.0
    }
  
  
 Clicando no botão “Testar”, o resultado é:
 
	{   
    "Results": [    
    465.89092963787937
    ]    
     }
  
#### Tem-se, assim, o número previsto de aluguéis de bicicletas, extraído de um modelo que prevê o número de alugueres de bicicletas esperados num determinado dia, com base em características sazonais e meteorológicas.
