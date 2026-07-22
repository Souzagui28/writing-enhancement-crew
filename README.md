# Writing Enhancement Crew

Sistema multiagente (CrewAI) que revisa um texto, compara com textos anteriores do autor via RAG e complementa com pesquisa externa, gerando um relatório final.

## Agentes

1. Revisor Gramatical e Estilístico: revisa gramática e estilo, com justificativa das correções.
2. Analista de Coesão de Conteúdo: usa RAG (`UserTextRetrieverTool`, ChromaDB) sobre textos anteriores do usuário para achar padrões e conexões.
3. Pesquisador de Conhecimento Externo: busca fontes na web (Serper) sobre o tema do texto.
4. Editor Final de Relatórios: compila os três resultados num relatório único.

Execução sequencial via CrewAI.

## Stack

CrewAI, LangChain, ChromaDB, Google Generative AI (Gemini), Serper.

## Status

Trabalho prático da disciplina de Tópicos Especiais em Inteligência Artificial (UFAM). Dependências fixadas na época; versões mais recentes de CrewAI, LangChain e ChromaDB já mudaram partes da API.

## Como executar

1. `conda create --name tp4-souzagui python=3.10 -y`
2. `conda activate tp4-souzagui`
3. `pip install -r requirements.txt`
4. Copiar `.env.example` para `.env` e preencher as chaves (Serper, Gemini)
5. Adicionar textos próprios (`.txt`) em `user_texts/`
6. Selecionar o ambiente conda no VS Code e executar o `notebook.ipynb`

Obs: o kernel pode cair se a API do Gemini não responder a tempo; reabrir o VS Code resolve.
