# Atmosphere

Goal: create and implement metrics to measure Transparency and Trustworthiness

## Motivation

(5) Com a aplicação de ML e DL em áreas mais críticas como medicina, justiça criminal e aplicações financeiras a inabilidade de entender estes modelos é um problema.

(2) Prover igualdade: exemplo, um algoritmo para ajudar a tomar decisões de contratação ou justiça criminal devem não apenas otimizar acurácia, mas também otimizar ética e justiça. Como otimizar áreas que não podemos mensurar?

(2) Exemplo: na pesquisa (5) é descrito um modelo para predizer a probabilidade de morte de um paciente com pneumonia, esse modelo dizia que um paciente tinha menor probabilidade de morte se ele tbm tem asthma. Ou seja, o modelo achava que se um paciente tinha asthma, então ele tinha menos chance de morrer e portanto um tratamento menos agressivo pode ser feito. Na verdade quem tem asthma já tem acesso a um tratamento mais agressivo, portanto o modelo previa menor chance de morte devido ao tratamento que já está sendo feito e não devido a presença de asthma.

(2) ataques adversariais são uma realidade, tanto para classificação de imagens como para outros casos, como por exemplo credit-seekers podem tomar certas atitudes antes de pedir crédito para maximizar suas chances de obter mais crédito.

(2) Nova lei na união Européia (2016) propõe direito de explicação para usuários.
(5) discute o tradeoff entre acurácia e interpretabilidade/facilidade de entender o modelo para casos médicos. Eles sugerem um modelo (GA²M) que é o estado da arte no problema de classificar como low-risk or high-risk casos de pneumonia, enquanto é interpretável, modular e editável. 
O autor cita um caso em que uma rede neural tinha acurácia de 86% e uma regressão logística de 77% foi usada por considerarem o uso de redes neurais muito “arriscadas” para casos reais.
Para maior interpretabilidade tentaram rule-base learning (SVM e boosted trees não eram comuns, e random forests não existiam), uma das regras era temAsthma(x) -> menor risco de morte. Esse padrão de fato existe nos dados mas não deveria ser seguido.
A decisão de não usar redes neurais não foi pela dificuldade de conter esse padrão de aparecer nos dados, mas sim porque devido a dificuldade de entender o funcionamento do modelo fica difícil saber quais outros problemas possam estar ocorrendo.

## Interpretabilidade - Interpretability

(2) utiliza apenas modelos supervisionados de aprendizado. Segundo (2) a definição de interpretabilidade não se refere há um conceito, mas sim várias interpretações de interpretabilidade. Há duas formas de interpretar:
Transparência. No sentido de modelo, componentes do modelo, algoritmo.
modelo: dizemos que o modelo é transparente se o usuário tem acesso ao modelo e consegue entendê-lo. Portanto deve ser simples, pense que você poderia colocar o input no modelo e em tempo razoável fazer todos os cálculos para chegar ao output. transparência(Modelos lineares complexos) < transparência(Redes neurais simples).
componentes do modelo: cada parte do modelo (input, parametro, cálculos) admite uma explicação intuitiva. 
algoritmo: por exemplo, entender como o erro é calculado como o gradiente descendente é feito, etc. (deep learning é complicado garantir esse tipo de transparência)
post-hoc interpretations. Explicar predições sem tentar explicar como o modelo funciona. Algumas abordagens comuns são: visualização, explicações em linguagem natural, e explicação por exemplo.
Explicação por exemplo: esse tumor foi classificado como tumor porque o modelo o acha parecido com esses outros tumores, que são malignos.
After training a deep neural network or latent variable model for a discriminative task, we then have access not only to predictions but also to the learned representations. Then, for any example, in addition to generating a prediction, we can use the activations of the hidden layers to identify the k-nearest neighbors based on the proximity in the space learned by the model. This sort of explanation by example has precedent in how humans sometimes justify actions by analogy. For example, doctors often refer to case studies to support a planned treatment protocol.
Linguagem natural: (6) utiliza um modelo para predições e outro modelo (uma RNN) para gerar uma explicação em linguagem natural.
Visualização: pesquisas para visualizar neurônios e layers de CNNs
Explicações locais: cita o trabalho de (4) entre outros.


## Confiança - Trustfulness

(2) ter “fé” na performance, robustez, ou alguma outra propriedade das decisões tomadas pelo modelo?
(2) Considerando que ter fé num modelo é confiar que o modelo se comportará bem no mundo real, e portanto utilizá-lo para tomar decisões. É importante mensurar não somente o quanto o modelo acerta (acurácia) mas também em que casos ele acerta. Se o modelo erra nos mesmos casos que humanos e acerta quando humanos acertam então de boas. mas se o modelo erra em casos que humanos geralmente acertam então uma supervisão humana no algoritmo pode ser necessária.


## Transparência - Transparency

(2) podemos observar transparência de 3 formas:
olhar para o algoritmo, ele converge?
olhar para os parâmetros, entendemos o que cada parâmetro do modelo representa? 
olhar para a complexidade, é simples o suficiente para ser examinado por uma pessoa?


## Justiça - Fairness

(3) tenta assegurar fairness na escolha de features através da opinião das pessoas. O que a autora chama de process fairness. Ou seja justiça durante o processo.
“Suppose a learning method, say a classifier C, has been trained to make decisions using a set of features F. C will be considered fair by an user U only if all features used by C (set F) are considered fair by this user. In this way the fairness of C is the fraction of all users that consider the use of all it’s features fair.”
Fairness = (intersecao de usuarios que acharam todas as features justas) / total de usuarios
São definidas 3 tipos de fairness:
Apriori fairness: features consideradas justas mesmo sem conhecimento sobre como a feature afeta o desempenho do modelo.
accuracy fairness: features consideradas justas quando sabem que ela revela uma maior acurácia quando adicionada ao modelo.
disparity fairness: features consideradas justas quando sabem que ela diminui a disparidade entre minorias (brancos vs negros).

Logistic regression com 9 features. 512 modelos base possíveis.

## Awareness
usuários, donos, designers… devem estar cientes do possível bias presente nos modelos e do possível dando que esse bias pode trazer para sociedade. “O que estou comprando?”


## References

1. [Semantics derived automatically from language corpora contain human-like biases](http://science.sciencemag.org/content/356/6334/183)
2. [Lipton, “The Mythos of Model Interpretability”](https://arxiv.org/abs/1606.03490)
3. [The Case for Process Fairness in Learning: Feature Selection for Fair Decision Making](http://www.mlandthelaw.org/papers/grgic.pdf)
4. [Why should I trust you?](https://arxiv.org/abs/1602.04938)
5. [Intelligible Models for HealthCare: Predicting Pneumonia Risk and Hospital 30-day Readmission](http://people.dbmi.columbia.edu/noemie/papers/15kdd.pdf)
6. [Learning From explanations using sentimental and advice in rl](http://ieeexplore.ieee.org/document/7742965/)
