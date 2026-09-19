# Detecção de Fake News em Português Brasileiro

Iniciação científica (UFCAT) sobre detecção de fake news em português
usando NLP e modelos de linguagem.

## Etapas
- [x] 01 - Baseline: TF-IDF + Regressão Logística
- [ ] 02 - Outros classificadores clássicos
- [ ] 03 - Fine-tuning do BERTimbau

## Dataset
Fake.br Corpus: 7.200 notícias (3.600 verdadeiras, 3.600 falsas).

Link: https://github.com/roneysco/Fake.br-Corpus

Referência: Monteiro et al. (2018). Contributions to the Study of Fake News
in Portuguese: New Corpus and Automatic Detection Results. PROPOR 2018.

## Resultados
| Modelo | Acurácia | F1 |
|---|---|---|
| TF-IDF (5000 features) + Regressão Logística | 94,2% | 0,94 |

Divisão 80% treino / 20% teste. Resultado inicial (baseline).
