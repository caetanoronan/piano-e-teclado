# Evolucao Do Projeto E Guia Para Clonagem

Este documento registra como o `Mapa Base do Piano e Teclado` evoluiu, quais problemas apareceram durante a construcao e como o projeto pode ser clonado para novos instrumentos ou novas versoes pedagogicas.

## 1. Origem Da Ideia

O projeto nasceu depois do `Mapa Base do Trombone`, que usava:

- mapa visual;
- cores para notas;
- funcoes harmonicas;
- estudo em blocos curtos;
- PWA para acesso rapido e offline.

Ao migrar para piano/teclado, a logica mudou.

No trombone, o foco era:

```text
nota + posicao da vara + registro
```

No piano, o foco passou a ser:

```text
tecla + nota + grau da escala + dedo + leitura na pauta
```

Essa mudanca foi o ponto principal da adaptacao.

## 2. Primeira Versao

A primeira versao criou uma pasta propria:

```text
Piano_e_Teclado/
```

Com:

- `index.html`;
- `relatorio.html`;
- `manifest.webmanifest`;
- `sw.js`;
- `icons/icon.svg`.

O app principal ja nasceu como PWA e com a estrutura do mapa em uma tela real de uso, nao como landing page.

## 3. Problemas Encontrados E Como Foram Resolvidos

### Problema 1: Teclado Nao Cabia Na Tela

No comeco, o teclado usava largura fixa em pixels. Em telas menores, ele estourava o layout e exigia rolagem horizontal.

Solucao:

- o teclado passou a usar largura proporcional;
- as teclas brancas usam `calc(100% / quantidadeDeTeclas)`;
- as teclas pretas sao posicionadas em porcentagem;
- o teclado passou a caber inteiro no painel.

### Problema 2: Informacoes Misturadas No Relatorio

O relatorio inicialmente tinha blocos soltos como:

- conteudos do mapa;
- fluxo para TDAH;
- modos implementados;
- possiveis evolucoes.

Isso deixou a apresentacao repetitiva e confusa.

Solucao:

- transformar o relatorio em abas;
- cada assunto ganhou seu proprio painel;
- itens importantes viraram abas no mesmo nivel, nao cards escondidos.

Abas finais:

- Conteudos do mapa;
- Fluxo de estudo;
- Modos do app;
- Pauta desenhada;
- Exercicios por nivel;
- Audio das notas;
- Dados em JSON;
- Cores e legenda;
- PWA e acesso;
- Proximos passos.

### Problema 3: Pauta Desenhada Estava So Em Texto

A aba `Pauta desenhada` explicava a ideia, mas nao mostrava visualmente a relacao entre teclado e partitura.

Solucao:

- adicionar mini teclado clicavel;
- desenhar pauta em clave de sol;
- desenhar pauta em clave de fa;
- marcar a nota selecionada nas duas pautas;
- tocar a nota ao clicar no teclado;
- adicionar subtopicos internos:
  - Clave de sol;
  - Clave de fa;
  - Nota destacada;
  - Leitura ativa.

### Problema 4: Som Sem Arquivos Externos

A ideia era adicionar som sem baixar varios arquivos `.mp3`.

Solucao:

- usar Web Audio API;
- calcular frequencias matematicamente;
- sintetizar notas com osciladores;
- adicionar envelope com ataque e fade out.

Vantagens:

- funciona offline;
- nao pesa o repositorio;
- nao depende de servidor externo;
- permite mudar timbre e duracao.

### Problema 5: Controle De Timbre, Volume E Duracao

Depois do som funcionar, faltava controle musical.

Solucao:

- adicionar volume;
- adicionar duracao;
- adicionar timbres:
  - `triangle`;
  - `sine`;
  - `square`;
  - `sawtooth`.

Esses controles foram adicionados no app principal e na demonstracao do relatorio.

### Problema 6: Cores Precisavam Ser Pedagogicas

O mapa do trombone usava cores para fixar notas e funcoes. No piano, era importante manter esse recurso, mas com outra logica.

Solucao:

- criar cores por nota natural;
- criar cores por funcao harmonica;
- permitir alternar visualizacao:
  - Notas + funcoes;
  - Notas;
  - Funcoes;
  - Sem cores.

Isso permite estudar com apoio visual no inicio e reduzir as cores depois.

### Problema 7: Cache Do PWA Segurava Versoes Antigas

Durante a evolucao, o navegador podia manter uma versao antiga em cache.

Solucao:

- atualizar `CACHE_NAME` no `sw.js` a cada mudanca relevante;
- orientar o uso de `Ctrl + F5` quando necessario;
- manter `sw.js` simples e previsivel.

## 4. Estrutura Pedagogica Atual

O produto atual tem quatro camadas de estudo:

### Camada Visual

- teclado;
- cores;
- pauta;
- nota destacada.

### Camada Auditiva

- nota sintetizada;
- controle de timbre;
- controle de duracao;
- controle de volume.

### Camada Teorica

- graus;
- funcoes;
- acordes;
- campo harmonico.

### Camada De Pratica

- leitura;
- tarefas curtas;
- timer;
- estudo por blocos.

## 5. Como Clonar Para Um Novo Projeto

### Passo 1: Copiar A Pasta

```bash
cp -r Piano_e_Teclado Novo_Instrumento
```

No Windows, pode duplicar a pasta manualmente.

### Passo 2: Trocar Nomes

Atualize:

- `<title>`;
- `h1`;
- `manifest.webmanifest`;
- textos principais;
- `CACHE_NAME` no `sw.js`;
- nome do icone, se houver.

### Passo 3: Identificar A Logica Do Instrumento

Antes de editar visualmente, defina qual sera a unidade principal do mapa.

Exemplos:

```text
Piano: tecla + nota + dedo + pauta
Trombone: posicao + nota + registro
Violao: corda + casa + dedo + acorde
Flauta: digitacao + nota + registro
```

### Passo 4: Separar Dados Musicais

O ideal para futuras versoes e mover dados para JSON:

```text
data/
├── notas.json
├── escalas.json
├── acordes.json
└── exercicios.json
```

Isso facilita adaptar o app sem reescrever todo o HTML.

### Passo 5: Adaptar O Visual

Cada instrumento precisa de uma representacao propria.

Exemplos:

- piano: teclado;
- violao: braco com casas;
- sopros: tabela de digitacao;
- cordas: cordas e posicoes;
- bateria: mapa de pecas.

### Passo 6: Preservar O PWA

Mantenha:

- `manifest.webmanifest`;
- `sw.js`;
- icones;
- links no `<head>`;
- registro do service worker.

Isso garante que o material continue instalavel e offline.

## 6. Sugestoes Para Repositorio Publico

Nome sugerido:

```text
mapa-base-piano-teclado
```

Descricao curta:

```text
PWA educativo para estudar piano e teclado com mapa visual, leitura, som sintetizado e pratica em blocos curtos.
```

Topicos sugeridos no GitHub:

```text
piano
teclado
educacao-musical
pwa
web-audio
javascript
html-css
musica
leitura-musical
```

## 7. README Do Repositorio

O `README.md` deve explicar:

- o que e o projeto;
- como rodar localmente;
- como publicar no GitHub Pages;
- quais arquivos existem;
- como adaptar para outro instrumento;
- quais funcionalidades ja existem;
- quais evolucoes estao planejadas.

Este repositorio ja possui um README pronto para isso.

## 8. Boas Praticas Para Proximas Versoes

- Evitar colocar informacao duplicada fora das abas.
- Cada assunto importante deve ter sua propria aba ou painel.
- Manter o teclado como experiencia principal.
- Evitar dependencias externas pesadas.
- Testar sempre:
  - sintaxe JS;
  - manifesto;
  - service worker;
  - layout mobile;
  - cache atualizado.
- Atualizar `CACHE_NAME` sempre que a experiencia mudar.

## 9. Proximas Melhorias Recomendadas

1. Salvar preferencias de som no `localStorage`.
2. Salvar modo de cor escolhido.
3. Adicionar exercicios com pontuacao.
4. Criar treino auditivo.
5. Adicionar mais escalas.
6. Separar dados em JSON.
7. Criar pagina de professor.
8. Criar instalador/guia para GitHub Pages.

## 10. Conclusao

O projeto evoluiu de uma ideia simples para uma ferramenta pedagogica completa:

- visual;
- sonora;
- instalavel;
- offline;
- responsiva;
- adaptavel;
- sem frameworks;
- pronta para clonagem.

A maior licao do processo foi que a organizacao da informacao importa tanto quanto a funcionalidade. Quando cada assunto ganhou sua propria aba, o projeto ficou mais claro, mais didatico e mais facil de expandir.

