
# Azure Machine-learning

Para a realização deste laboratório, necessita de ter uma conta no portal [Azure](https://www.azure.microsoft.com)

# Passo 1 - Criar um recurso no Azure Machine Learning

Aceda ao [portal Azure](https://portal.azure.com) e faça login com as suas credênciais.

Selecione a o menu "Create a resource" e procure por "Machine Learning".

![](https://github.com/vicalmeida/MLearnAI900Lab1/blob/main/img1.png)

Ao selecionar abrirá uma lista vazia. Clique então em criar.

![](https://github.com/vicalmeida/MLearnAI900Lab1/blob/main/img2.png)

É necessário preencher a seguinte informação:

	. Subscription (Deixe o valor)
	. Resource group (Crie um)
	. Name 
	. Region (Deixe a rede como pública)
	
Os restantes campos (Storage account, key vault e application insights) pode deixar com os valores padrão.

![](https://github.com/vicalmeida/MLearnAI900Lab1/blob/main/img3.png)

Selecione **Criar** para confirmar. Aguarde até que conclua a criação da workspace.

# Passo 2 - Iniciar o Machine Learning Studio

Depois de criada a workspace, clique na opção **Go to Resource**.

![](https://github.com/vicalmeida/MLearnAI900Lab1/blob/main/img4.png)

Em seguida clique em **Launch Studio**

![](https://github.com/vicalmeida/MLearnAI900Lab1/blob/main/img5.png)

# Passo 3 - Treinar um modelo

No Azure Machine Learning Studio selecione no menu a esquerda a opção **ML Automatizado**.

Clicar em **Novo trabalho de ML Automatizado**.

![](https://github.com/vicalmeida/MLearnAI900Lab1/blob/main/img6.png)

Escolha **Treinar automaticamente**. Insira nome do trabalho, criar novo experimento, insira a descrição e clicar em avançar.

![](https://github.com/vicalmeida/MLearnAI900Lab1/blob/main/img7.png)

Na fonte de dados, escolha "De arquivos da Web".

![](https://github.com/vicalmeida/MLearnAI900Lab1/blob/main/img9.png)


Inserir URL https://aka.ms/bike-rentals

![](https://github.com/vicalmeida/MLearnAI900Lab1/blob/main/img10.png)


### Configurações 

    . Formato de arquivo: Delimitado
    . Delimitador: Vírgula
    . Encoding: UTF-8 
    . Cabeçalhos de coluna: Somente o primeiro arquivo tem cabeçalhos

![](https://github.com/vicalmeida/MLearnAI900Lab1/blob/main/img11.png)

Clique em criar.

### Configurações de tarefa

    . Tipo de tarefa: Regressão
    . Tipo de dados: Tabular.
    . Coluna de destino: Rentals

### Configurações adicionais

    . Métrica primária: NormalizedRootMeanSquareError
    . Desmarcar campos: "Explicar o melhor modelo","Habilitar empilhamento de ensemble" e "Usar todos os modelos suportados".
    . Modelos permitidos:RamdomForest e LightGBM. 

Clicar em salvar.

![](https://github.com/vicalmeida/MLearnAI900Lab1/blob/main/img15.png)


### Limites

    . máximo de avaliações 3
    . máximo de avaliações simultâneas 3
    . máximo de nós 3
    . limite de pontuação da métrica 0.085
    . templo limite do experimento (minutos) 15
    . tempo limite de iteração (minutos) 15 
    . habilitar encerramento antecipado marcado.

![](https://github.com/vicalmeida/MLearnAI900Lab1/blob/main/img16.png)

### Validar e Testar

    . Tipo de validação: Divisão de validação de treinamento. 
    . Validação de percentual de dados: 10.
    . Dados de teste: nenhum.

![](https://github.com/vicalmeida/MLearnAI900Lab1/blob/main/img17.png)

### Computação

    . Tipo computação: Sem servidor
    . Tipo de máquina virtual: CPU
    . Tipo de máquina virtual: Dedicado
    . Tamanho da máquina virtual: Standard_DS3_V2 
    . Número de instâncias: 1

![](https://github.com/vicalmeida/MLearnAI900Lab1/blob/main/img18.png)

O modelo será processado por cerca de 15 minutos.

![](https://github.com/vicalmeida/MLearnAI900Lab1/blob/main/img19.png)

# Passo 4 - Verificando o Modelo

Com o processamento concluído, poderá ser possível avaliar o modelo. Basta clicar no nome dos algoritmos do modelo.

No modelo gerado, acesse então a aba de métricas.


# Passo 5 - Teste

Para validar e testar o modelo, basta selecionar o modelo e ir na aba "Testar".

Preencha o json conforme a previsão desejada e clique em testar:

![](https://github.com/vicalmeida/MLearnAI900Lab1/blob/main/img20.png)


### Pontos de extremidade

#### Entrada de dados 
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

#### Resultado 

{
    "Results": [
      360.4150044515
    ]
}
