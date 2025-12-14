# Respostas do Trabalho - Pipeline de ML

## Identificação do Grupo

- **Integrantes:**
1. Micael Macedo Pereira da Trindade
2. Pedro Henrique de Magalhães Casimiro
3. Daniel Barrozo Lima
4. Pedro Guilherme Feitoza Melo
5. Bruno Sampaio

---

## Parte 1: Resultados do Pipeline

### 1.1 O pipeline executou sem erros?
<!-- Marque com X a opção correta -->
- [X] Sim
- [ ] Não

### 1.2 F1-Score obtido:
<!-- Copie o valor exibido ao final da execução -->
```
F1-Score: 0.4043
```

### 1.3 Cole aqui o output final do pipeline:
<!-- Execute: python main.py e copie a saída -->
```
🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀
INICIANDO PIPELINE DE ML
🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀🚀


[ETAPA 1/4] Carregando dados...
==================================================
EXPLORAÇÃO DOS DADOS
==================================================
Shape: (5000, 8)

Tipos de Colunas:
cliente_id              int64
idade                   int64
renda_mensal          float64
tempo_conta_meses       int64
num_produtos            int64
tem_cartao_credito      int64
score_credito         float64
respondeu_campanha      int64
dtype: object

Primeiras 5 Linhas:
   cliente_id  idade  renda_mensal  ...  tem_cartao_credito  score_credito  respondeu_campanha
0           1     56      46917.46  ...                   1          600.0                   1
1           2     69      41274.41  ...                   0          758.2                   0
2           3     46      40649.98  ...                   1          595.7                   1
3           4     32      44336.79  ...                   1          584.3                   0
4           5     60      35301.68  ...                   0          797.8                   0

[5 rows x 8 columns]
==================================================

DISTRIBUIÇÃO DO TARGET
------------------------------
Contagem de Valores que responderam a campanha:
respondeu_campanha
0    2803
1    2197
Name: count, dtype: int64

Proporção de Valores que responderam a campanha:
respondeu_campanha
0    56.06%
1    43.94%
Name: proportion, dtype: object
------------------------------

[ETAPA 2/4] Validando dados...
Validando dados...
✅ Dados válidos!

[ETAPA 3/4] Treinando modelo...
==================================================
PREPARANDO OS DADOS...
==================================================

Dados de treino: 4000 registros
Dados de teste: 1000 registros

==================================================
TREINANDO MODELO...
==================================================
✅ Modelo treinado!

==================================================
SALVANDO MODELO EM: ../models/modelo_campanha.pkl
==================================================
✅ Modelo salvo!

[ETAPA 4/4] Avaliando modelo...

==================================================
RESULTADOS DA AVALIAÇÃO
==================================================

📊 MÉTRICAS:
   Accuracy:  0.5550 (55.50%)
   Precision: 0.4951
   Recall:    0.3416
   F1-Score:  0.4043

📋 MATRIZ DE CONFUSÃO:
   Verdadeiros Negativos (TN): 404
   Falsos Positivos (FP):      154
   Falsos Negativos (FN):      291
   Verdadeiros Positivos (TP): 151

==================================================
🎯 F1-SCORE FINAL: 0.4043
==================================================

✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅
PIPELINE CONCLUÍDO COM SUCESSO!
✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅✅

📝 Anote o F1-Score no arquivo RESPOSTAS.md: 0.4043
```

---

## Parte 2: Interpretação dos Resultados

### 2.1 O modelo é bom ou ruim? Por quê?
<!-- Considere: F1 de 0.5 seria jogar moeda. Acima de 0.5 = melhor que aleatório. -->
O modelo apresenta um desempenho ruim, pois obteve um F1-Score de 0.4043, valor inferior a 0.5, que representa um desempenho equivalente ao acaso. Isso indica que o modelo ainda não consegue equilibrar bem precisão e recall, errando bastante nas previsões da classe positiva.



### 2.2 O dataset é balanceado ou desbalanceado? Como você descobriu?
<!-- Dica: veja a proporção da variável target na exploração dos dados -->
O dataset é relativamente balanceado, pois a variável target apresenta aproximadamente 56% da classe 0 e 44% da classe 1, conforme observado na exploração dos dados. Apesar de não ser perfeitamente equilibrado, não há um desbalanceamento severo.



### 2.3 Por que usamos F1-Score e não apenas Accuracy neste caso?
<!-- Dica: pense no que aconteceria se o modelo previsse sempre 0 -->
Utilizamos o F1-Score porque ele considera simultaneamente precisão e recall, sendo mais adequado para avaliar o desempenho da classe positiva. Apenas a accuracy pode ser enganosa, pois um modelo que previsse sempre a classe 0 ainda teria uma accuracy razoável, mas falharia completamente em identificar clientes que responderiam à campanha.


---

## Parte 3: Validação de Dados

### 3.1 Liste as validações Pandera que você implementou:
<!-- Descreva cada validação que você adicionou -->

1. cliente_id: o id do cliente não pode ser nulo por se tratar de um campo chave, e deve ser um número inteiro, único.
2. idade: por se tratar de tempo em anos, deve ser número inteiro e, negocialmente, deve estar entre 0 e 80.
3. renda_mensal: deve ser decimal (float), por se tratar de moeda, e, negocialmente, estar entre 1000 e 50000.
4. score_credito: negocialmente, deve estar entre 300 e 850 e, por ser valor quebrado, deve ser do tipo float.
5. respondeu_campanha: nesse campo, precisa-se saber apenas se a campanha foi ou não respóndida, bastando ser true ou false, 0 ou 1 nesse caso.

### 3.2 Por que validar dados ANTES de treinar o modelo?
<!-- Pense no contexto de produção: o que aconteceria se dados inválidos entrassem no modelo? -->
A validação de dados antes do treinamento é fundamental para garantir a qualidade e consistência dos dados. Dados inválidos, ausentes ou fora do padrão podem causar erros no treinamento ou gerar modelos incorretos. Em ambientes de produção, a validação evita que dados inconsistentes comprometam o desempenho e a confiabilidade do modelo.


---

## Parte 4: Versionamento

### 4.1 Liste os commits que vocês fizeram (copie do git log):
<!-- Execute: git log --oneline e cole aqui -->
```
743d909 (origin/main, origin/HEAD) Atualiza respostas e corrige caminho de dados no treino
24003e8 Merge pull request #5 from phmcasimiro/feature/ajuste-main-pipeline
0ab9ea0 (origin/feature/ajuste-main-pipeline) Ajusta fluxo do main.py e finalização do pipeline
9e26582 Merge pull request #4 from phmcasimiro/feat/casimiro/validar.py
e41d565 (origin/feat/casimiro/validar.py) commit casimiro validar.py
33064c3 Merge pull request #2 from phmcasimiro/feature-treinamento
a698744 (origin/feature-treinamento) Conclusão do treinar.py com ajustes de caminho
ffddd63 Implementa treinamento RandomForest e regras de ignorar modelos
052858f Merge pull request #1 from phmcasimiro/carregamento_dados
839bb0d (origin/carregamento_dados) Realizando o carregamento dos dados do arquivo csv
3c4c6f6 feat/casimiro/Commit inicial do projeto de avaliação da disciplina de Pipeline de dados
```

### 4.2 Por que mensagens de commit descritivas são importantes?
<!-- Pense: se outra pessoa olhar o histórico, vai entender o que foi feito? -->

Essas mensagens são compartilhadas com todo o time de desenvolvimento, sendo que deve ser orientadora, clara e concisa para que outro desenvolvedor possa ler e entender de antemão o que a alteração em questão implementou, reduzindo assim o retrabalho e facilitando a manutenção. 

---

## Parte 5: Reflexão (Opcional)

### 5.1 Qual foi a maior dificuldade do grupo?

Alinhar as etapas de implementações e commits entre os membros da equipe.

### 5.2 O que vocês fariam diferente se fossem refazer?

O primeiro commit seria feito em conjunto, em uma reunião, explicando os detalhes e necessidades.

---

**Data de entrega:** 16/12/2025
