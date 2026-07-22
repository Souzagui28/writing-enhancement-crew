# Writing Enhancement Crew

Sistema multiagente que recebe um texto e devolve um relatório de aprimoramento, combinando revisão gramatical, comparação com o próprio histórico de escrita do autor e pesquisa externa sobre o tema.

## Como funciona

Um pipeline sequencial de 4 agentes (via [CrewAI](https://github.com/crewAIInc/crewAI)):

1. **Revisor Gramatical e Estilístico** — revisa o texto e devolve versão corrigida + justificativas das correções.
2. **Analista de Coesão de Conteúdo** — usa uma ferramenta de RAG customizada (`UserTextRetrieverTool`) para buscar textos anteriores do próprio usuário (base vetorial ChromaDB) e identificar padrões/conexões com o texto atual.
3. **Pesquisador de Conhecimento Externo** — pesquisa na web (via Serper) fontes relevantes sobre o tema do texto.
4. **Editor Final de Relatórios** — compila os três resultados anteriores num relatório markdown único e coeso.

A ideia central é usar IA não só para revisar gramática, mas para cruzar um texto novo com o **próprio histórico de escrita do autor** (via RAG sobre uma base pessoal de textos) e com pesquisa externa, gerando insights que o autor sozinho não teria.

## Stack

- [CrewAI](https://github.com/crewAIInc/crewAI) — orquestração dos agentes (processo sequencial)
- LangChain + ChromaDB — RAG sobre a base pessoal de textos (`user_texts/`)
- Google Generative AI (Gemini) — LLM e embeddings
- Serper — busca na web

## Status

Desenvolvido como trabalho prático da disciplina de Tópicos Especiais em Inteligência Artificial (UFAM). As dependências (CrewAI, LangChain, ChromaDB) foram fixadas na versão da época do desenvolvimento; como frameworks de IA generativa evoluem rápido, versões mais recentes dessas bibliotecas já mudaram partes da API.

## Como executar

1. `conda create --name tp4-souzagui python=3.10 -y`
2. `conda activate tp4-souzagui`
3. `pip install -r requirements.txt`
4. Copiar `.env.example` para `.env` e preencher as chaves de API:
   - [Serper](https://serper.dev/signup)
   - [Google AI Studio (Gemini)](https://aistudio.google.com/app/apikey)
5. Adicionar textos próprios (`.txt`) na pasta `user_texts/`
6. Selecionar o ambiente conda `tp4-souzagui` no VS Code (ícone no canto superior direito do notebook) e executar as células do `notebook.ipynb`

**Obs:** o kernel pode cair durante a execução caso a API do Gemini não responda a tempo — nesse caso, reabrir o VS Code e executar as células novamente costuma resolver.
