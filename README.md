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
**Fake.br Corp
