# Pokédex Simples

## Autor
Yan Rocha Lino — Matrícula 706.450.451-01

## Descrição
Uma aplicação web que permite buscar Pokémon pelo nome ou número e visualizar informações básicas sobre eles, como imagem, altura, peso e tipo.

## API utilizada
- Nome da API: PokeAPI — https://pokeapi.co/docs/v2
- Endpoint consumido: GET /api/v2/pokemon/{nome-ou-id}

## Funcionalidades
- Buscar um Pokémon digitando nome ou número
- Visualizar imagem, altura, peso e tipo(s) do Pokémon
- Buscar apertando o botão ou a tecla Enter
- Receber mensagem amigável quando o Pokémon não é encontrado

## Como executar localmente
1. Clone: `git clone https://github.com/yanrochalino/pokedex-bootcamp.git`
2. Abra o arquivo `index.html` no navegador

## Links
- **Aplicação no ar (GitHub Pages):** https://yanrochalino.github.io/pokedex-bootcamp/
- **Repositório:** https://github.com/yanrochalino/pokedex-bootcamp
'Adiciona README com instrucoes do projeto'
## Links

- **Aplicação no ar (GitHub Pages):** https://yanrochalino.github.io/pokedex-bootcamp/
- **Repositório GitHub:** https://github.com/yanrochalino/pokedex-bootcamp
- **Repositório no Docker Hub:** https://hub.docker.com/r/SEU-USUARIO/bootcamp2-app

## Como rodar com Docker

Com o Docker instalado, execute uma única linha:

```
docker run -d -p 8080:80 SEU-USUARIO/bootcamp2-app:1.1
```

Depois acesse http://localhost:8080

## Persistência de dados

- **Banco escolhido:** Supabase (PostgreSQL), acessado direto do frontend com a biblioteca `supabase-js`.
- **O que é salvo:** o time de Pokémon do usuário (máximo de 6).
- **Operações:** criar (adicionar ao time), listar (carrega ao abrir a página) e excluir (botão em cada Pokémon).
- **Estrutura da tabela `time_pokemon`:**

| Coluna | Tipo | Descrição |
|---|---|---|
| id | bigint (chave primária) | Identificador do registro |
| criado_em | timestamptz | Data/hora em que foi adicionado |
| pokemon_id | int | Número do Pokémon na PokeAPI |
| nome | text | Nome do Pokémon |
| imagem | text | URL da imagem |
| tipos | text | Tipo(s) do Pokémon |

- **Limitação conhecida:** as políticas de acesso (RLS) estão abertas para o papel `anon`, ou seja, qualquer visitante pode ler, inserir e excluir registros. É aceitável nesta etapa; em produção seria necessário autenticação.

## Sidequests

### SQ1 · .dockerignore

O arquivo `.dockerignore` exclui da imagem o que ela não precisa (`.git`, `README.md`, prints, rascunhos). Assim o contexto enviado ao Docker no `docker build` é menor, o build fica mais rápido e a imagem final fica menor, sem arquivos desnecessários.

### SQ2 · Versionamento de imagem

Publicadas no Docker Hub as tags `1.0` (primeira versão funcional), `1.1` (após a melhoria: DESCREVA AQUI A MELHORIA) e `latest`.

### SQ3 · Descrição no Docker Hub

O overview do repositório no Docker Hub contém o que é a aplicação, o comando `docker run` pronto e o link do GitHub.

### SQ4 · Orquestração

Dois containers rodando ao mesmo tempo, nas portas 8080 e 8081:

![docker ps com dois containers](print-sq4.png)

**Se eu tivesse 100 containers, como gerenciaria?**

ESCREVA AQUI COM AS SUAS PALAVRAS, depois de pesquisar. Pontos que o parágrafo deve cobrir: gerenciar 100 containers manualmente com `docker run` não é viável; o Kubernetes é um orquestrador que automatiza isso; um **cluster** é o conjunto de máquinas gerenciadas pelo Kubernetes; um **pod** é a menor unidade, que executa um ou mais containers; uma **réplica** é uma cópia do mesmo pod, e o Kubernetes mantém o número desejado de réplicas, recriando as que falham e distribuindo o tráfego entre elas.
