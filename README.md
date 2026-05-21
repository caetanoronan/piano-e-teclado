# Mapa Base do Piano e Teclado

Aplicativo educativo em HTML, CSS e JavaScript puro para estudar piano e teclado com visual atualizado, teclado interativo, leitura, escalas, acordes, campo harmonico, som sintetizado e funcionamento offline como PWA.

O projeto nasceu como uma adaptacao do fluxo pedagogico usado no mapa do trombone de vara, mas foi redesenhado para a logica do piano: tecla, nota, grau da escala, dedilhado, leitura e funcao harmonica.

O visual atual segue a mesma identidade do guia de layout do hub musical: fundo suave com elementos decorativos, blocos em gradiente, cards organizados e foco em leitura clara tanto no `index.html` quanto no `relatorio.html`.

## O Que O App Faz

- Mostra um teclado interativo de 2 ou 3 oitavas.
- Permite escolher tonalidade e modo: maior ou menor natural.
- Acende as notas da escala selecionada.
- Mostra nome da nota em notacao internacional e solfejo.
- Mostra grau da escala e funcao harmonica.
- Sugere dedilhado para mao direita e mao esquerda.
- Toca as notas com Web Audio API, sem arquivos MP3.
- Permite controlar volume, duracao e timbre.
- Mostra legenda de cores para notas e funcoes.
- Inclui modos de estudo: teclado, leitura, acordes e campo harmonico.
- Inclui pratica curta com timer e tarefas rapidas.
- Funciona como PWA: instalavel e com cache offline.
- Inclui relatorio interativo com abas, pauta desenhada e blocos explicativos.

## Identidade Visual

O layout foi ajustado para ficar mais próximo do padrao visual do hub musical.

### Principios

- fundo com gradientes suaves e camada decorativa musical;
- blocos com bordas arredondadas e sombra leve;
- destaque visual em titulo, tag e seções principais;
- leitura limpa no desktop e no celular;
- reducao de movimento respeitada quando o sistema pedir.

### O Que Foi Alinhado

- pagina principal com cabecalho mais integrado ao conjunto;
- relatorio com a mesma linguagem visual da pagina principal;
- responsividade reforcada para tela estreita;
- tema claro e escuro com a mesma paleta base do projeto.

## Elementos Musicais no Layout

Esta seção descreve como representar visualmente elementos musicais no layout sem alterar a estrutura funcional do app. Siga estas recomendações para manter consistência visual, acessibilidade e compatibilidade com o `GUIA_LAYOUT.md` do hub.

1. Notas e oitavas:
    - Use classes e atributos semânticos (por exemplo, `data-note`, `data-octave`) nas teclas e nos pontos de partitura para facilitar estilização e leitura por scripts.
    - Mostre nome internacional e solfejo juntos quando houver espaço; ex.: `C4 / Dó`.
    - Ao colorir por nota, mantenha uma paleta consistente (Dó, Ré, Mi, Fá, Sol, Lá, Si) e documente as cores no `relatorio.html` e na legenda.

2. Claves e pauta:
    - Renderize pautas como SVG (`.score`) para manter nitidez em qualquer tela.
    - Use elementos com classes como `.clef-label`, `.staff-line`, `.note-dot` para permitir estilização independente.
    - Mantenha as claves decorativas em pseudo-elementos ou SVGs separados para não interferir no fluxo do conteúdo.

3. Tempo, compasso e pulsação:
    - Exiba marcações de andamento e compasso como texto curto (ex.: `♩ = 80`, `4/4`) dentro de elementos com `aria-label` claros (`aria-label="andamento: semicolcheia igual a 80"`).
    - Para exercícios rítmicos, ofereça controle visual e sonoro (metronomo) com opção de silenciar e de reduzir animação para usuários sensíveis a movimento.

4. Notação e legibilidade:
    - Evite animacões rápidas sobre a pauta; use transições lentas e respeite `prefers-reduced-motion`.
    - Quando destacar uma nota na pauta e no teclado simultaneamente, sincronize foco e `aria-live` para leitores de tela.
    - Forneça contraste suficiente entre pontos de nota e linhas da pauta (sugestão: `note-dot` com contorno escuro leve quando o fundo for claro, e o contrário no modo escuro).

5. Boas práticas de implementação:
    - Não renomeie classes essenciais do layout (`wrap`, `hero`, `grid`, `card`, `section`, `btn`, `nav`, `tag`, `stack`, `flow`).
    - Ao adicionar ícones musicais decorativos (𝄞, ♪, ♫), use `pointer-events: none` em pseudo-elementos e opacidade baixa.
    - Documente qualquer nova classe no `relatorio.html` e no `README.md` para facilitar manutenção.

Seguindo essas regras, o app mantém clareza pedagógica e compatibilidade visual com o hub de produtos musicais.

## Arquivos Principais

```text
Piano_e_Teclado/
|-- index.html              # Aplicativo principal
|-- relatorio.html          # Relatorio explicativo e interativo
|-- manifest.webmanifest    # Configuracao do PWA
|-- sw.js                   # Service worker para cache offline
`-- icons/
    `-- icon.svg            # Icone do app
```

## Estrutura Da Interface

### index.html

- guia rapido de uso;
- barra de controles;
- teclado interativo;
- painel de nota selecionada;
- modos de estudo;
- pratica curta.

### relatorio.html

- visao geral do mapa;
- abas tematicas sobre conteudo, fluxo, modos e acessibilidade;
- demonstracao de pauta desenhada;
- explicacao do audio, dados e PWA;
- proximos passos do projeto.

## Como Rodar Localmente

Voce pode abrir o arquivo `index.html` diretamente no navegador, mas para testar PWA e service worker use um servidor local:

```bash
cd Piano_e_Teclado
python -m http.server 8000
```

Depois acesse:

```text
http://127.0.0.1:8000/
```

## Como Validar O Layout

Depois de alterar o visual, confira:

1. Abra `index.html` e `relatorio.html` no navegador.
2. Teste a pagina em tela larga e em largura reduzida.
3. Clique em `Modo escuro` nas duas paginas.
4. Verifique se o teclado, as abas e a pauta continuam legiveis.
5. Confirme que o fundo nao atrapalha o texto nem os controles.

## Como Publicar No GitHub Pages

1. Crie um repositorio no GitHub.
2. Envie a pasta `Piano_e_Teclado` para o repositorio.
3. No GitHub, va em `Settings > Pages`.
4. Em `Build and deployment`, escolha `Deploy from a branch`.
5. Escolha a branch `main` e a pasta raiz ou `/docs`, conforme sua organizacao.
6. Acesse a URL publicada pelo GitHub Pages.

Exemplo de comandos:

```bash
git init
git add .
git commit -m "Publica mapa base do piano e teclado"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/mapa-base-piano-teclado.git
git push -u origin main
```

Troque `SEU-USUARIO` pelo seu usuario do GitHub.

## Observacao Sobre O Link Publicado

Se a pagina principal estiver publicada em GitHub Pages, a versao atualizada deve ser acessada pela URL do repositorio, mantendo o arquivo `index.html` como entrada principal do site.

## Funcionalidades Do Index

### Teclado Interativo

O teclado mostra notas naturais e acidentes, com destaque para as notas da escala escolhida.

Cada tecla pode mostrar:

- nome da nota;
- grau da escala;
- dedilhado sugerido;
- cor por nota;
- cor por funcao harmonica;
- estado selecionado.

### Escalas

O app atualmente trabalha com:

- escalas maiores;
- escalas menores naturais.

O seletor de tonalidade muda a escala e atualiza o teclado automaticamente.

### Acordes

O modo de acordes mostra formacoes basicas:

- triade;
- acorde de setima;
- sus4;
- diminuto.

### Campo Harmonico

Mostra os graus da tonalidade em numerais romanos:

```text
I ii iii IV V vi vii°
```

ou, no menor natural:

```text
i ii° III iv v VI VII
```

### Leitura

O modo leitura gera uma nota aleatoria para o estudante encontrar no teclado.

### Pratica Curta

O app inclui:

- tarefa aleatoria;
- timer de 5 minutos;
- timer de 10 minutos;
- iniciar, pausar e reiniciar.

## Sistema De Cores

O app usa duas camadas de cor:

### Cor Por Nota

As notas naturais recebem cores proprias:

- Do
- Re
- Mi
- Fa
- Sol
- La
- Si

Isso ajuda a localizar padroes no teclado.

### Cor Por Funcao

Algumas funcoes harmonicas recebem destaque especial:

- Tonica
- Terca
- Quinta
- Sensivel

O seletor `Mostrar cores` permite alternar entre:

- Notas + funcoes
- Notas
- Funcoes
- Sem cores

## Web Audio API

O app nao usa arquivos de audio. As notas sao sintetizadas no navegador com Web Audio API.

Cada nota e calculada matematicamente a partir do MIDI:

```js
440 * (2 ** ((midi - 69) / 12))
```

O som usa:

- `AudioContext`;
- `OscillatorNode`;
- `GainNode`;
- envelope curto com ataque e fade out.

Controles disponiveis:

- volume;
- duracao;
- timbre.

Timbres:

- Suave: `triangle`
- Redondo: `sine`
- Brilhante: `square`
- Metalico: `sawtooth`

## Relatorio Interativo

O `relatorio.html` funciona como documentacao navegavel do produto e segue a mesma identidade visual da pagina principal.

Abas atuais:

- Conteudos do mapa
- Fluxo de estudo
- Modos do app
- Pauta desenhada
- Exercicios por nivel
- Audio das notas
- Dados em JSON
- Cores e legenda
- PWA e acesso
- Proximos passos

### Pauta Desenhada

A aba de pauta desenhada inclui:

- mini teclado clicavel;
- pauta em clave de sol;
- pauta em clave de fa;
- nota destacada nas duas pautas;
- som ao clicar nas teclas;
- controles de volume, duracao e timbre.

Tambem possui subtopicos:

- Clave de sol;
- Clave de fa;
- Nota destacada;
- Leitura ativa.

## PWA E Offline

O app inclui:

- `manifest.webmanifest`;
- `sw.js`;
- icone SVG;
- cache dos arquivos principais;
- modo standalone;
- suporte para instalacao em celulares.

Depois do primeiro acesso em servidor HTTPS, como GitHub Pages, o app pode funcionar offline.

## Tema Claro E Escuro

O app e o relatorio compartilham a mesma preferencia de tema usando `localStorage`.

Quando o usuario alterna entre modo claro e modo escuro em uma pagina, a escolha tambem vale para a outra.

## Como Clonar Para Outro Instrumento

Este projeto pode virar modelo para outros instrumentos.

Para clonar:

1. Copie a pasta `Piano_e_Teclado`.
2. Renomeie a pasta para o novo instrumento.
3. Troque titulo, manifest e textos.
4. Separe a logica visual especifica do instrumento.
5. Preserve a estrutura PWA.
6. Adapte os dados musicais.

Exemplos:

- teclado infantil;
- violao;
- flauta doce;
- saxofone;
- trompete;
- leitura musical geral.

## Ideias De Evolucao

- Salvar preferencias de som no `localStorage`.
- Separar escalas, acordes e exercicios em JSON.
- Adicionar mais escalas: menor harmonica, menor melodica, pentatonicas e modos gregos.
- Criar exercicios avaliativos com pontuacao.
- Adicionar treino auditivo: ouvir nota e encontrar tecla.
- Melhorar desenho da pauta com mais oitavas e linhas suplementares.
- Criar modo professor/aluno.
- Publicar como repositorio independente.

## Licenca

Uso livre para estudo, ensino e adaptacao educacional.
