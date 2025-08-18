![](ibmec2.png)


# Projeto da Disciplina — **PROJETO DE MACHINE LEARNING**
> Agente de IA para **Varredura Digital**: coleta de posts e conteúdos, **rank de influenciadores**, **NLP** (tópicos, sentimento pt-BR, resumos) e **dashboard/API** para insights acionáveis.

## Objetivo (MVP)
Entregar um **MVP reprodutível** que:
1. **Coleta** conteúdo (redes sociais + RSS/portais/blogs) com governança/ToS.
2. **Ranqueia influenciadores** via grafo de interações e métricas de engajamento.
3. **Analisa sentimento e temas** (baseline clássico $\Rightarrow$ embeddings/BERTopic/BERTimbau).
4. **Resume tendências** e gera séries temporais de sentimento/engajamento.
5. **Expõe** via **Dashboard (Streamlit/Gradio)** e **API (FastAPI)**.
6. **Documenta** decisões técnicas, riscos éticos e limitações.

## Papéis
- **Alunos**: execução técnica, documentação e apresentação.
- **Professor**: orientação metodológica, validação científica.
- **Parceiro externo**: contexto/escopo, eventual apoio de dados/LLMs.

---

## Por que este é um bom Projeto de ML?
Projeto aplicado, com **dados reais**, tarefas de **NLP** (sentimento/tópicos), **ranking** por grafo, **dashboard/API** e **MLOps leve**. Dá para formular hipóteses, comparar **baselines vs. modelos modernos**, validar temporalmente e discutir ética/ToS — tudo o que se espera de um capstone de ML.

---

## Checklist de Necessidades do Projeto
1. **Pergunta de pesquisa + hipóteses claras**
   *Ex.: “BERTopic detecta tendências com maior lead-time que NMF?”*
2. **Baselines sólidos** (léxico/NB/NMF) **vs. modernos** (BERTimbau/embeddings/BERTopic) com **tabela de benchmark**.
3. **Validação temporal** (treina no passado, testa no futuro) e, se possível, **fora de domínio** (YouTube vs. RSS).
4. **Análise de erro** e **ablações** (sem LLM, sem embeddings, sem grafo) com conclusões objetivas.
5. **MLOps/reprodutibilidade**: MLflow + seeds + configs; README com comando único para reproduzir.
6. **Ética/ToS/LGPD**: o que coletamos, por quê, limites e riscos (Data Card / Model Card).
7. **Métricas certas por tarefa**
   - Sentimento: **F1-macro**, PR e confusão normalizada
   - Tópicos: **coerência** + **diversidade**
   - Ranking: **Precision@K** + estabilidade (Kendall τ)
   - Tendência: **lead-time** (antecipação)

---


## Upgrades que elevam o nível acadêmico (não obrigatório)
- **Active Learning** para rotulagem: laço de incerteza (margem/entropia) e gráfico custo × ganho em F1.
- **Weak supervision** (regras/heurísticas combinadas) e análise de ruído tolerado.
- **Detecção de tendências “de verdade”**: rupturas (ruptures/Kleinberg bursts) e correlação com eventos externos; medir **lead-time**.
- **Grafo de influenciadores** “de gente grande”: PageRank/Betweenness + **detecção de comunidades**; estabilidade do ranking ao longo do tempo (Kendall τ).
- **Generalização entre domínios**: treina num canal/tema, testa em outro (domain shift).
- **Custo/latência**: custo por 1k itens (com/sem LLM), cache, distillation/quantization.
- **Robustez**: ruídos (typos/emoji/gíria), teste A/B de normalização.
- **Calibração**: confiabilidade das probabilidades (reliability diagram, ECE).

---

## Estrutura do repositório (sugestão)

```
.
├── README.md
├── environment.yml
├── requirements.txt
├── configs/
│   ├── base.yaml
│   └── experiment_example.yaml
├── data/
│   ├── raw/           # dados brutos (não versionar grandes arquivos)
│   └── processed/     # dados processados (amostras pequenas)
├── notebooks/
│   ├── 00_eda.ipynb
│   ├── 01_baselines_sentimento.ipynb
│   ├── 02_baselines_topicos.ipynb
│   ├── 03_grafo_influenciadores.ipynb
│   └── 04_llm_in_the_loop.ipynb
├── src/
│   ├── ingestion/     # coletas, loaders, deduplicação
│   ├── processing/    # limpeza, normalização, idioma, regex
│   ├── nlp/           # sentimento, tópicos, rotuladores, embeddings
│   ├── ranking/       # grafo, centralidades, engajamento
│   ├── eval/          # métricas, ablações, validações temporais
│   └── app/           # fastapi endpoints
├── app/
│   ├── main.py        # FastAPI
│   └── dashboard.py   # Streamlit/Gradio
├── experiments/       # MLflow tracking (artefatos/ids)
└── docs/
    ├── one-pager.md
    └── slides/
```


---

## Métricas (técnicas e de negócio)
- **Sentimento**: F1-macro (classes balanceadas por amostra), curva PR, análise de erro.
- **Tópicos**: coerência (`c_npmi`, `u_mass`), diversidade, estabilidade ao longo do tempo.
- **Ranking**: Precision@K, estabilidade (Kendall/τ) entre janelas, engajamento normalizado.
- **Tendência**: **lead-time** de detecção (dias) vs. ocorrência/menções externas.
- **Operacionais**: custo/latência (LLM), throughput, % de falhas de coleta.

---

## Governança & Ética
- Respeitar **ToS** e **LGPD**; coletar somente o necessário; anonimizar.
- Transparência de limitações; evitar conclusões prescritivas sem evidências.
- Registro de prompts/decisões; reprodutibilidade acima de tudo.

---

## Cronograma sugerido
> Datas: **18/08, 20/08, 25/08, 27/08, 01/09, 03/09, 08/09, 10/09, 15/09, 17/09, 22/09, 08/10, 15/10, 20/10, 22/10, 27/10, 29/10, 03/11, 05/11, 10/11**.

### 18/08 — Kickoff & framing
- Definição do problema, **KPIs**, riscos, squads, criação do repositório.

### 20/08 — Dados & governança
- Fontes (redes, RSS), limites legais/ToS, amostragem, plano de coleta/labeling.

### 25/08 — Ingestão v0
- Coleta mínima funcional (RSS + 1 rede), schema, deduplicação.

### 27/08 — EDA & labeling
- EDA, guia de anotação, setup de ferramenta de rótulos (Label Studio/Streamlit).

### 01/09 — Baselines (sentimento/tópicos)
- VADER pt adaptado / NB linear; TF-IDF + NMF/LDA; métricas de F1 e coerência.

### 03/09 — Grafo & ranking de influenciadores
- Construção do grafo, centralidades e métrica de engajamento.

### 08/09 — NLP moderno
- Embeddings pt-BR, BERTopic; comparação com baseline.

### 10/09 — LLM-in-the-loop
- Zero/few-shot para rótulos difíceis; resumos automáticos; custo/latência/fallback.

### 15/09 — Pipelines & rastreabilidade
- Orquestração (Prefect/Airflow), MLflow, DVC, configs.

### 17/09 — Dry-run parcial
- Revisão cruzada, análise de erro, plano de iteração.

### 22/09 — **Apresentações parciais individuais**
- Contribuição técnica própria (módulo/experimento/análise).
- **Rubrica**: método, métricas, clareza, próximos passos.

### 08/10 — Robustez, viés e fairness
- Testes de estresse, auditoria de viés e mitigação.

### 15/10 — Tendências emergentes
- Rupturas/bursts, correlação com eventos; **lead-time**.

### 20/10 — Dashboard & API v1
- Streamlit/Gradio + FastAPI; endpoints de consulta.

### 22/10 — Backtesting & ablações
- Validação temporal out-of-sample; ablação de componentes.

### 27/10 — Empacotamento & CI
- Docker, testes automatizados, lint/type checks.

### 29/10 — Storytelling & relatório
- One-pager executivo + apêndice técnico.

### 03/11 — Rehearsal completo
- Ensaio cronometrado, feedback de pares, checklist.

### 05/11 — Freeze & QA
- Congelar features, testes finais, plano de contingência.

### 10/11 — **Apresentação FINAL**
- Demo ao vivo, dashboard, API; Q&A técnico/negócio; entrega final.

---

## Rubrica de avaliação (sugerida)
- 10% **Escopo/definição & KPIs**
- 10% **Dados & pipelines**
- 30% **Modelagem (tópicos, sentimento, ranking)**
- 20% **Avaliação & análise de erro**
- 10% **MLOps leve (tracking, configs, reprodutibilidade)**
- 10% **Dashboard/API**
- 10% **Relatório & apresentação**

---

## Guia de contribuição
- Pull requests pequenas e frequentes, com descrição clara.
- Commits semânticos (`feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`).
- Issues com rótulos: `data`, `nlp`, `ranking`, `dashboard`, `infra`, `ethics`.
- **Reprodutibilidade**: seeds fixas, versões pinadas, configs no `configs/`.
