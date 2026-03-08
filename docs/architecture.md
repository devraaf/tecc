# Arquitetura do projeto

O sistema segue uma arquitetura backend + frontend desacoplados, onde o backend fornece os dados das teorias e o frontend renderiza as experiências interativas.

Fluxo:<br>
**Banco de dados → API → Frontend → Renderização dos experimentos**

## Backend
Tecnologias:
- Java
- Spring Boot e Web
- JPA/Hibernate
- MySQL

Responsabilidades:
- fornecer API das teorias
- fornecer dados de experimentos
- gerenciar conteúdo educacional

## Arquitetura de Experimentos

Cada teoria pode possuir um ou mais experimentos.

O comportamento do experimento é definido por:
- tipo do experimento
- mídias associadas
- configuração em JSON

Isso permite que o frontend interprete a configuração e gere interações diferentes.

## Banco de dados
Para permitir páginas flexíveis com texto, imagens, vídeos e experimentos interativos, o TECC utiliza uma estrutura baseada em blocos de conteúdo.

Cada teoria é composta por uma sequência ordenada de blocos que o frontend renderiza dinamicamente.


### Tabela theories

Armazena as teorias científicas.

Campos:

- id
- title
- slug
- category 

### Tabela content_blocks

Define os blocos de conteúdo que compõem a página da teoria.

Campos:

- id
- theory_id
- type
- content
- order_index

O campo *type* define o tipo do bloco.

Exemplos de tipos:

- text
- image
- experiment
- video
- curiosity

O campo *order_index* define a ordem em que os blocos aparecem na página.

### Tabela experiments

Armazena os experimentos interativos relacionados às teorias.

Campos:

- id
- theory_id
- title
- type
- description
- config_json

O campo *type* define qual componente de experimento o frontend deve renderizar.

Exemplos de tipos:

- random_simulation
- image_sequence
- animation
- canvas_simulation
- interactive_demo

O campo *config_json* define parâmetros do experimento.

### Tabela media_assets

Armazena mídias reutilizáveis.

Campos:

- id
- url
- type
- alt_text

<br>

Tipos de mídia:

- image
- gif
- video
- svg

### Tabela experiment_media

Relaciona mídias com experimentos.

Campos:

- id
- experiment_id
- media_id
- role
- order_index

O campo role define o uso da mídia dentro do experimento.

Exemplos:

- initial
- result_a
- result_b
- step_1
- step_2

## Frontend
Tecnologias:
- HTML
- CSS
- JavaScript
- React

Responsável por:
- renderizar teorias
- navegação entre páginas
- executar experimentos interativos