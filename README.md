# Detecção de Fake News em Português Brasileiro

Iniciação científica (UFCAT, Bacharelado em Inteligência Artificial) sobre detecção
de fake news em português usando Processamento de Linguagem Natural e modelos de linguagem.

## Etapas
- [x] 01 · Linha de base: TF-IDF + Regressão Logística
- [x] 02 · Scraping de fake news recentes (Boatos.org)
- [x] 03 · Coleta de notícias verdadeiras (G1) e montagem do corpus de 2026
- [x] 04 · Comparação de algoritmos clássicos
- [x] 05 · Rede neural LSTM e pipeline de verificação de notícias
- [ ] 06 · Fine-tuning do BERTimbau
- [ ] Ampliar o corpus de 2026 para 300 a 500 notícias

## Notebooks
| Notebook | O que faz |
|---|---|
| `01_baseline_tfidf_logreg` | Treina e testa TF-IDF + Regressão Logística no Fake.br |
| `02_scraping_boatos` | Coleta fake news recentes do Boatos.org com scraping |
| `03_coleta_g1_e_corpus` | Coleta notícias do G1 pelo RSS, junta, limpa e monta o corpus de 2026 |
| `04_comparacao_algoritmos` | Compara 5 algoritmos clássicos no Fake.br e no corpus de 2026 |
| `05_lstm_e_pipeline` | Treina a LSTM, compara com a Regressão Logística e demonstra o pipeline |

## Pipeline
Notícia → Limpeza → Representação → Modelo → Veredito

1. **Entrada:** o texto da notícia.
2. **Limpeza:** corta em 150 palavras, minúsculas, sem pontuação.
3. **Representação:** TF-IDF (5.000 palavras) para os modelos clássicos, ou sequência de palavras para a LSTM.
4. **Modelo:** calcula a probabilidade de a notícia ser falsa.
5. **Veredito:** fake ou fato, com a confiança e as palavras que mais pesaram.

A função `verificar_noticia`, no notebook 05, executa todas as etapas para qualquer texto.

## Dados
**Fake.br Corpus (2018):** 7.200 notícias, 3.600 verdadeiras e 3.600 falsas. Usado para treinar os modelos.
Link: https://github.com/roneysco/Fake.br-Corpus

**Corpus de 2026 (próprio):** 100 notícias de outubro de 2026, usadas só para teste.
- 40 falsas, coletadas do Boatos.org com scraping (notebook 02)
- 60 verdadeiras, coletadas do G1 pelo feed RSS (notebook 03)
- Limpeza: remoção de matérias antigas, de páginas que não eram boatos e das marcas do site nos textos falsos; todos os textos cortados em 150 palavras

Por direitos autorais, o repositório guarda só os links, datas, categorias e rótulos
(`dados/corpus_2026_metadados.csv`). Os textos podem ser coletados de novo com os notebooks 02 e 03.

## Resultados

### Algoritmos clássicos (TF-IDF com 5.000 palavras)
| Algoritmo | Fake.br (2018) | Corpus de 2026 |
|---|---|---|
| Regressão Logística | 95,4% | 89% |
| Random Forest | 95,8% | 85% |
| SVM linear | 96,5% | 84% |
| Passive Aggressive | 95,8% | 83% |
| Naive Bayes | 88,0% | 80% |

Acurácia. Fake.br: validação cruzada em 5 partes, texto completo.
Corpus de 2026: treino no Fake.br inteiro (textos de 150 palavras) e teste nas 100 notícias.

### LSTM x Regressão Logística
| Modelo | Fake.br (2018) | Corpus de 2026 | Fakes de 2026 detectadas |
|---|---|---|---|
| Regressão Logística | 92,7% | 87% | 78% |
| LSTM | 92,0% | 76% | 58% |
| LSTM bidirecional | 87,6% | 79% | 50% |

Mesma divisão de 80% para treino e 20% para teste e textos de 150 palavras para todos os modelos.
Os resultados da LSTM variam bastante entre execuções.

## Principais conclusões
- **Com poucos dados, o modelo simples ganha:** a LSTM empatou com a Regressão Logística no Fake.br e perdeu nas notícias de 2026.
- **A LSTM sobreajusta:** chega a 99% de acerto no treino, mas fica perto de 90% na validação.
- **Os modelos caem com notícias atuais:** todos erram mais as fake news de 2026 do que as verdadeiras. Uma hipótese é que aprendem palavras de assunto comuns nas fakes de 2018, e não sinais de falsidade.

## Próximos passos
- Fine-tuning do BERTimbau, que já vem pré-treinado em português
- Ampliar o corpus de 2026 para 300 a 500 notícias
- Analisar as palavras que mais pesam nas decisões dos modelos

## Referências
- Monteiro, R. A. et al. (2018). Contributions to the Study of Fake News in Portuguese: New Corpus and Automatic Detection Results. PROPOR 2018.
- Souza, F.; Nogueira, R.; Lotufo, R. (2020). BERTimbau: Pretrained BERT Models for Brazilian Portuguese. BRACIS 2020.
- Garcia, G. L. et al. (2024).
