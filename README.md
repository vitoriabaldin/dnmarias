Dona Maria, IA e Controvérsia Política no Instagram
Análise exploratória dos comentários publicados no Reel do perfil @metropoles (Instagram) sobre o pedido judicial da Federação Brasil da Esperança (PT, PV e PCdoB) pela remoção do perfil da personagem "Dona Maria", criada por inteligência artificial e associada à produção de conteúdos políticos críticos ao governo Lula.
Pergunta de pesquisa: como os comentários no Reel do Metrópoles sobre a personagem "Dona Maria" articulam inteligência artificial, autenticidade discursiva, fake news e polarização política no Instagram?

1. Objetivos da pesquisa
Investigar como usuários do Instagram comentam a controvérsia em torno de uma personagem política gerada por IA, considerando não apenas o texto dos comentários, mas também objetos nativamente digitais da plataforma (curtidas, emojis, padrões de coocorrência e engajamento), na perspectiva dos métodos digitais (ROGERS, 2025).
Identificar os eixos discursivos predominantes do corpus (personagem, IA, polarização político-partidária, disputa verdade × fake news).
Testar a hipótese interpretativa de que a artificialidade da personagem não elimina sua eficácia comunicacional: parte dos usuários desloca a discussão da autenticidade da personagem para a suposta autenticidade do discurso ("mesmo sendo IA, fala verdades" × "por ser IA, é fake/manipulação").
Mapear sinais de possível efeito Streisand decorrentes da tentativa de remoção judicial do perfil.

2. Corpus e contexto
Plataforma:	Instagram
Objeto:	Comentários do Reel do @metropoles sobre a personagem "Dona Maria"
URL do post:	https://www.instagram.com/reels/DXkyjneEfDp/ (publicado em 25 abr. 2026)
Data da coleta:	18 de maio de 2026
Corpus final (pós-limpeza)	: 627 comentários
Unidade de análise:	Comentário individual (texto, autor anonimizado, curtidas, emojis)

3. Estratégia de coleta
Ferramenta de coleta: extensão de navegador Instant Data Scraper (raspagem automatizada do DOM da página do Reel, com rolagem manual até esgotar o carregamento de comentários visíveis).
Procedimento: abertura do post no navegador logado, expansão de respostas/comentários, execução do scraper e exportação da tabela bruta (autor, texto do comentário, nº de curtidas).
Exportação: planilha bruta salva em /data.
Limites da coleta: a raspagem depende do que a interface do Instagram renderiza no momento da coleta (ordenação algorítmica, comentários ocultados/removidos, respostas colapsadas). O corpus é, portanto, um recorte situado — não a totalidade das interações do post. A coleta em outra data ou sessão pode produzir corpus diferente, o que restringe a reprodutibilidade da etapa de coleta.

4. Queries utilizadas
A coleta não utilizou queries de busca (não houve consulta por palavras-chave em API ou motor de busca): o corpus foi delimitado por URL única — todos os comentários carregáveis do post https://www.instagram.com/reels/DXkyjneEfDp/.
As "queries" do projeto operam na etapa de análise, sobre o corpus já coletado:
Filtro Streisand: classificação por expressões regulares/listas de termos em três categorias:
vou seguir (intenção declarada de seguir o perfil);
censura (enquadramento do pedido judicial como censura);
pedindo o arroba (busca ativa pelo @ do perfil).
Segregação de emojis: extração via biblioteca emoji (correspondência Unicode).
Vocabulário lexical: tokenização + remoção de stopwords em português + filtro de comprimento mínimo (> 2 caracteres).
As listas de termos e padrões exatos estão versionadas em /script

5. Ferramenta / Biblioteca
Instant Data Scraper (extensão Chrome)	Raspagem dos comentários
Python	Linguagem de processamento e análise
pandas	Manipulação tabular
openpyxl	Leitura/escrita de .xlsx
matplotlib	Visualizações
wordcloud	Nuvem de palavras
emoji	Extração e contagem de emojis
nltk	Tokenização e stopwords (pt-BR)
scikit-learn	TF-IDF, coocorrência, LDA
pysentimiento	Classificação automática de sentimentos (exploratória)
Claude (Anthropic)	Apoio à programação (assistência de código)

6. Procedimentos de tratamento dos dados (pré-processamento)

Aplicados nesta ordem, via script em /script:

Remoção de ruído estrutural: URLs, menções (@usuario) e caracteres não alfabéticos irrelevantes para a análise lexical.
Extração e segregação de emojis: os emojis são copiados para um campo próprio antes da limpeza textual (preservando-os para a análise de emojis) e removidos do texto tokenizável.
Deduplicação por par (autor, comentário): elimina duplicatas geradas pela raspagem (repetição de linhas no scroll).
Normalização e tokenização lexical (minúsculas, tokenização por palavra).
Remoção de stopwords (lista NLTK pt-BR, com eventuais acréscimos manuais documentados no script).
Filtragem por comprimento mínimo: descarte de tokens com até 2 caracteres.
Anonimização: os nomes de usuário não são mobilizados na análise nem expostos nos resultados; comentários citados no texto do trabalho são reproduzidos com parcimônia e sem identificação.

7. Organização do repositório
.
├── README.md                     
          
├── /data (com os comentários brutos, exportação do Instant Data Scraper)
├── /script
│   └── analise_comentarios.py     (pipeline completo: pré-processamento e análises )
├── 01_nuvem_palavras.png          (nuvem de palavras do corpus)
├── 02_top_palavras.png            (top 10 palavras por frequência lexical) 
├── 03_tfidf.png                   (termos por TF-IDF médio)
├── 04_coocorrencia.png            (top 10 pares coocorrentes) 
├── 05_lda_topicos.png             (peso total e participação relativa dos tópicos LDA)
├── 06_top_emojis.png              (top 10 emojis) 
├── 07_streisand_categorias.png    (categorias de sinais de efeito Streisand) 
└── 08_streisand_curtidas.png      (curtidas: comentários com/sem sinal Streisand)

8. Como reproduzir
   A partir do corpus tratado incluído em /data:
# 1. Clonar o repositório
# 2. Criar ambiente e instalar dependências
# 3. Baixar recursos do NLTK (stopwords/tokenizadores pt-BR)
# 4. Executar o pipeline
python script/analise_comentarios.py

9. Ética e uso dos dados
Os comentários são tratados como dados públicos/semipúblicos de plataforma, coletados de um post aberto de veículo jornalístico. O objetivo é compreender padrões discursivos e sociotécnicos de uma controvérsia pública, não identificar indivíduos.
