# Sistema de Recomendação de Filmes Baseado em NLP (TF-IDF + Similaridade de Cosseno)

Este projeto implementa um sistema de recomendação de filmes simples, mas eficaz, utilizando técnicas de Processamento de Linguagem Natural (PLN) para identificar a similaridade entre filmes com base em seus gêneros. O objetivo principal é demonstrar como a vetorização de texto com TF-IDF e a medição de similaridade por Cosseno podem ser aplicadas para construir um recomendador de conteúdo.

O sistema processa metadados de filmes para criar representações numéricas e, em seguida, sugere filmes semelhantes àqueles que um usuário pode ter gostado.

## Integrantes

- [Felipe Gibin]()
- [Halycia]()
- [Paulo Lamounier](https://github.com/Nanashii76)
- [Samuel Arthur]()
- [Yasmin Dayrell]()

## Funcionalidades

- Vetorização de Gêneros: Transforma a lista de gêneros de cada filme em um vetor numérico usando a técnica TF-IDF.
- Cálculo de Similaridade: Determina a similaridade entre filmes calculando o cosseno do ângulo entre seus vetores de gênero.
- Recomendação Personalizada: Sugere filmes com base na similaridade de gêneros com um filme de referência escolhido.
- Interface Simples (Streamlit): Oferece uma interface web interativa para que os usuários possam facilmente buscar filmes e obter recomendações.
- Integração com ngrok (Colab): Permite expor o aplicativo Streamlit rodando no Google Colab para a internet, facilitando o compartilhamento e teste.

## Datasets

O projeto utiliza dois datasets principais do Kaggle:

- `movies.csv`:
    - `movieId`: ID único do filme.
    - `title`: Título do filme.
    - `genres`: Gêneros associados ao filme (separados por |).
- `ratings.csv`: (Mencionado no notebook, mas não diretamente utilizado na lógica de recomendação de gênero mostrada. Pode ser útil para futuras melhorias.)
    - `userId`: ID do usuário que avaliou o filme.
    - `movieId`: ID do filme avaliado.
    - `rating`: Nota dada pelo usuário ao filme.
    - `timestamp`: Momento da avaliação.

[disponíveis aqui](https://www.kaggle.com/datasets/gargmanas/movierecommenderdataset?resource=download&select=movies.csv)

## Metodologia

1. Pré-processamento de Gêneros: A coluna genres de cada filme é tratada como um "documento". Os gêneros são tokenizados e convertidos para minúsculas.
2. Vetorização TF-IDF: O TfidfVectorizer é aplicado a todos os gêneros de todos os filmes para criar uma matriz onde cada linha representa um filme, e as colunas representam os gêneros, com valores TF-IDF indicando a importância de cada gênero para aquele filme em relação à coleção.
3. Cálculo de Similaridade: A cosine_similarity é utilizada para medir a similaridade entre os vetores TF-IDF dos filmes. Filmes com vetores mais próximos (menor ângulo) são considerados mais semelhantes em seus gêneros.
4. Recomendação: Dada uma entrada de filme, o sistema encontra os filmes com as maiores pontuações de similaridade de cosseno, sugerindo-os ao usuário.

## Como usar

Este projeto foi desenvolvido para ser executado em um ambiente como o Google Colab, aproveitando a integração com ngrok para exposição da interface Streamlit.

1. Clone este repositório (ou baixe o arquivo .ipynb):

``` bash
git clone https://github.com/Nanashii76/CIS-Recomendacao-Filmes
cd seu-repositorio
```

2. Abra o arquivo Sistema_de_recomendação_de_filmes_NLP.ipynb no Google Colab.

3. Faça o upload dos datasets movies.csv e ratings.csv para o ambiente do Colab (ou ajuste os caminhos para onde eles estiverem).

4. Ajuste sua chave API ao final do código do streamlit

``` python
...

# Iniciar o túnel ngrok (Mantenha o seu token aqui)
ngrok.set_auth_token("{CHAVE_API_NGROK}") # Substitua pelo seu token

print("Aguarde, iniciando o Streamlit e o túnel ngrok...")
public_url = ngrok.connect(8501)
print(f"Seu aplicativo Streamlit está disponível em: {public_url}")

...
```

5. Execute todas as células do notebook sequencialmente.

## Estrutura do Projeto

```
./
├── Sistema_de_recomendação_de_filmes_NLP.ipynb # Notebook principal do projeto
├── data/                                       # Pasta com os datasets
├───── movies.csv                               # Dataset de filmes
├───── ratings.csv                              # Datast de avaliações
├── Sistema de recomendação de filmes NLP.pdf   # Slides usados na apresentação
└── README.md                                   # Este arquivo
```

