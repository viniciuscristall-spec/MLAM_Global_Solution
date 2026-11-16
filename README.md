[README.md](https://github.com/user-attachments/files/34895438/README.md)
# CitizenTech - Global Solution MLAM

Análise estatística e modelagem preditiva da relação entre **área cultivada** e **valor da produção agrícola** das microrregiões brasileiras, usando dados reais do IBGE.

## Integrantes

| Nome | RM |
|------|----|
| André Debiazzi | 569062 |
| Kaique da Silva | 572718 |
| Vinicius Cristal | 572049 |

## Sobre o projeto

**Desafio CitizenTech (tema: campo).** A produção agrícola sustenta milhares de comunidades rurais, mas varia muito de uma região para outra. Este trabalho investiga como a área cultivada se relaciona com o valor da produção e se é possível **prever** e **classificar** esse valor a partir das áreas plantada e colhida.

### Objetivos

1. Caracterizar a distribuição do valor da produção.
2. Testar hipóteses sobre a área colhida.
3. Medir e modelar a relação entre área e valor (regressão linear simples e múltipla).
4. Classificar microrregiões de alto e baixo valor de produção (regressão logística binária).

## Base de dados

| Item | Descrição |
|------|-----------|
| **Fonte** | IBGE - SIDRA, Pesquisa Agrícola Municipal (PAM), [tabela 1612](https://sidra.ibge.gov.br/tabela/1612) |
| **Arquivo** | `tabela1612.csv` (dados reais) |
| **Unidade de análise** | Microrregião geográfica |
| **Variáveis** | Área plantada (hectares), Área colhida (hectares) e Valor da produção (mil reais) |

O produto e o ano de referência constam no cabeçalho do arquivo, que o notebook imprime na seção 1.

**Tratamento dos dados:**

- O símbolo `-` do SIDRA é convertido em zero; os demais símbolos (`X`, `...`) viram valores ausentes.
- A tabela original traz 137 mesorregiões seguidas de 558 microrregiões. O notebook confere que os totais dos dois níveis coincidem e mantém **apenas as microrregiões**, para não contar a mesma região duas vezes.
- Registros com valores ausentes são removidos antes das análises.

## Estrutura do notebook

| Seção | Conteúdo |
|-------|----------|
| Configuração | Importação das bibliotecas, semente aleatória (`SEED = 42`) e funções auxiliares (`forca_correlacao`, `teste_f`) |
| **1. Importação e tratamento** | Download da base, leitura do CSV, renomeação de colunas, limpeza e estatísticas descritivas |
| **2. Distribuição normal** | Probabilidades `P(X < média)` e `P(X > mediana)` do valor da produção, com classificação do evento |
| **3. Testes de hipóteses** | Teste Z para a média da área colhida: (a) cauda inferior, n = 20, α = 6%; (b) cauda superior, n = 25, α = 9% |
| **4. Análise bivariada** | Dispersão, covariância, correlação de Pearson, regressão linear simples (Área plantada → Valor), R², teste F e previsão |
| **5. Regressão linear múltipla** | Área plantada e área colhida como preditoras: dispersão, matrizes de covariância e correlação, equação, R² ajustado, teste F, VIF e previsão |
| **6. Regressão logística binária** | Classificação em alto/baixo valor (acima ou abaixo da mediana): equação, matriz de confusão, acurácia e classificação de um novo caso |
| Conclusões e limitações | Leitura geral e ressalvas metodológicas |

## Como executar

### Requisitos

- Python 3.9 ou superior
- Jupyter Notebook, JupyterLab ou Google Colab

### Dependências

```bash
pip install numpy pandas matplotlib seaborn scipy scikit-learn
```

### Passos

1. Baixe o arquivo `Global_Solution_MLAM.ipynb`.
2. Abra no Jupyter ou envie para o Google Colab.
3. Execute as células em ordem (**Run All**).

A base `tabela1612.csv` é baixada automaticamente do [repositório do projeto](https://github.com/viniciuscristall-spec/MLAM_Global_Solution) na primeira execução, se ainda não estiver na pasta do notebook. É preciso ter conexão com a internet nessa etapa. Se preferir, coloque o arquivo manualmente na mesma pasta do notebook.

> As amostras aleatórias usam `SEED = 42`, então os resultados do teste de hipóteses são reproduzíveis.

## Principais limitações

- **Normalidade:** os itens 2 e 3 assumem distribuição normal, mas os dados são assimétricos à direita; as probabilidades são aproximações.
- **Teste de hipóteses:** as amostras saem da própria base de referência, então H0 é verdadeira por construção. O teste ilustra o procedimento.
- **Pontos de alavanca:** poucas microrregiões muito grandes influenciam fortemente correlações e retas de regressão.
- **Multicolinearidade:** as áreas plantada e colhida são quase redundantes, o que torna instáveis os coeficientes individuais das regressões múltipla e logística.
- **Avaliação do modelo logístico:** a acurácia é calculada na mesma base do ajuste, sem separação treino/teste, e tende a ser otimista.
- **Escopo:** recorte único de produto e ano, valores nominais e agregados por microrregião; os resultados não se estendem a propriedades, municípios ou outros anos.
- **Causalidade:** os resultados indicam associação estatística, não relação de causa e efeito.

## Tecnologias

Python · pandas · NumPy · SciPy · scikit-learn · matplotlib · seaborn

## Fonte dos dados

IBGE - Sistema IBGE de Recuperação Automática (SIDRA), Pesquisa Agrícola Municipal. <https://sidra.ibge.gov.br/tabela/1612>
