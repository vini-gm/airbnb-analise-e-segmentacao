# 📊 Análise Imobiliária e Segmentação - Airbnb Rio de Janeiro

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2C2D72?style=for-the-badge&logo=pandas&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-%233F4F75.svg?style=for-the-badge&logo=plotly&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=for-the-badge&logo=Matplotlib&logoColor=black)
![Seaborn](https://img.shields.io/badge/Seaborn-3776AB?style=for-the-badge&logo=seaborn&logoColor=white)

## 🎯 O Desafio e Objetivo
Compreender a dinâmica de preços do mercado imobiliário de locação por temporada é um desafio complexo. Fatores como quantidade de quartos e localização se misturam com a percepção de valor dos hóspedes. 

Este projeto constrói um **pipeline de análise de dados ponta a ponta** utilizando dados reais do Airbnb (Rio de Janeiro) para extrair insights estatísticos sobre precificação e aplicar algoritmos de Machine Learning Não-Supervisionado. O foco principal é segmentar o mercado imobiliário, passando pelas seguintes etapas 
* Estruturar um fluxo de tratamento e limpeza de dados (Data Quality);
* Analisar a relação entre estrutura física, localização e o valor das diárias;
* Identificar e mitigar o impacto de imóveis fora da curva (Outliers);
* Mapear as avaliações de custo-benefício na percepção dos usuários.

---

## 📌 Questões de Negócio Respondidas
O projeto foi guiado para responder analiticamente às seguintes perguntas:
* Qual o preço médio por tipo de hospedagem (comparando Média vs. Mediana)?
* Qual a distribuição de valores por tipo de hospedagem e como identificar/tratar anomalias (outliers)?
* Qual bairro oferece a melhor relação preço/avaliação na percepção do hóspede?
* Como os imóveis se agrupam e quais seus perfis de imóveis do RJ considerando estrutura e preço?

---

## 🗂️ Sobre a Base de Dados
A análise foi construída sobre os dados oficiais extraídos do portal [Inside Airbnb](https://insideairbnb.com/get-the-data/). As principais variáveis utilizadas incluem:
* **Detalhes do Imóvel:** Id, nome, descrição, tipo de propriedade e tipo de quarto, etc.
* **Localização Geoespacial:** Bairro, Longitude e Latitude.
* **Métricas de Capacidade e Valor:** Preço por diária, quantidade de hóspedes, número de banheiros, quartos, camas e avaliações de custo-benefício (`review_scores_value`).

---

## 🏗️ Arquitetura do Projeto (Data Pipeline)
O projeto foi estruturado como uma esteira de dados, dividida em três etapas lógicas para garantir escalabilidade e reprodutibilidade:

* **📁 `01_coleta_e_manipulacao.ipynb`**: Foco em engenharia e qualidade de dados. Extração, correção de erros de encoding em strings), tipagem correta de dados monetários e imputação inteligente de valores nulos (NaN) baseada em estatística de agrupamento.
* **📁 `02_eda_estatistica_e_visualizacao.ipynb`**: Análise Exploratória de Dados (EDA). Uso de estatística descritiva para identificar distribuições assimétricas e tratamento matemático de outliers. Visualização de dados e teste de hipóteses usando Seaborn/Matplotlib.
* **📁 `03_ml_kmeans_clustering.ipynb`**: Aplicação de Machine Learning. Padronização de features, validação matemática da quantidade de clusters e visualização de alta dimensionalidade.
    
---


## 💡 Principais Insights de Negócio

1. **Ilusão Média vs. Mediana:** Propriedades do tipo *Entire home/apt* apresentam forte assimetria positiva devido a outliers de altíssimo luxo. Enquanto a média sugere que são os mais caros, a mediana revela que **quartos de hotel possuem o preço "típico" (piso) mais elevado e consistente do mercado**.
2. **Mapa de Percepção de Valor:** O cruzamento de dados geoespaciais com a métrica de avaliações revelou os bairros que entregam o melhor custo-benefício, mostrando que o maior valor percebido não está necessariamente nas áreas mais nobres da Zona Sul.
3. **Segmentação Estratégica (K-Means):** O mercado se divide em 3 perfis operacionais:
   * **Econômico (Alta densidade):** Imóveis focados em volume de camas e baixo custo.
   * **Padrão (Equilíbrio):** Propriedades residenciais típicas para famílias.
   * **Premium (Exclusividade):** Onde o preço descola das características físicas e é ditado pela exclusividade.

---

## 🛠️ Decisões Técnicas e Metodologia Avançada

Para garantir o rigor técnico do modelo de Machine Learning, as seguintes abordagens foram aplicadas:

* **Filtro Estatístico de Outliers (Método IQR):}** Aplicação do Intervalo Interquartil para definir limites superiores matemáticos, evitando que imóveis com diárias exorbitantes distorcessem a clusterização.
* **Feature Scaling (`StandardScaler`):** Essencial para algoritmos baseados em Distância Euclidiana (como o K-Means). Evitou que a alta magnitude da variável ``price`` enviesasse o modelo e ignorasse variáveis estruturais (quartos/camas).
* **Método do Cotovelo (Elbow Method):** Utilizado para embasar matematicamente a escolha de `k=3` clusters, analisando a curva de inércia.
* **Redução de Dimensionalidade (`PCA`):** Principal Component Analysis aplicado para projetar as variáveis em 2D, permitindo a validação visual da separação dos clusters criados.

*(Gráfico do Método Cotovelo)*
> ![Gráfico do Cotovelo](https://github.com/vini-gm/airbnb-analise-e-segmentacao/blob/main/imagens/metodo_cotovelo.png)

---

*(Top 10 bairros com melhor custo-benefício)*
> ![Top 10 bairros](https://github.com/vini-gm/airbnb-analise-e-segmentacao/blob/main/imagens/top10_bairros.png)

---

*(Clusters Finais)*
> ![Clusters finais](https://github.com/vini-gm/airbnb-analise-e-segmentacao/blob/main/imagens/clusters_finais.png)

---


## 🚀 Como Reproduzir o Projeto

1. Clone este repositório:
   ```bash
   git clone [https://github.com/SeuUsuario/nome-do-repositorio.git](https://github.com/SeuUsuario/nome-do-repositorio.git)

2. Instale as dependências listadas no requirements.txt:
   ```bash
   pip install -r requirements.txt

3. Execute os notebooks sequencialmente (01 -> 02 -> 03) para reproduzir o pipeline. Os dados base original e processado encontram-se na pasta `data/raw`.
