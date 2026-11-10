# Ônibus Assassino

Jogo de stop-motion em HTML5 Canvas, em português, feito para rodar no navegador
do computador e do celular. Tudo (HTML, CSS, JavaScript e sons) vive em um único
arquivo: **`index.html`**. Não tem build, nem dependências.

Versão atual: **2.6** (o número aparece no canto da tela de título e fica em `CONFIG.VERSAO`).

## Como rodar

Basta abrir `index.html` no navegador. Ou, para servir por HTTP (recomendado para
testar no celular na mesma rede):

```bash
python3 -m http.server 8000
# depois abra http://localhost:8000
```

## Os dois modos

| Modo | Como funciona |
| --- | --- |
| 🏃 **Fuga** | O ônibus passeia pela rua, te vê, persegue e atira. Você pega as estrelas, se esconde nas caixas, joga iscas e foge pela saída. |
| 🗿 **Estátua** | Ande só pela calçada (a ponte no meio é a única travessia). Quando o ônibus **avisar** e depois **olhar**, fique parado — se você se mexer, é pego. |

## Controles

**Computador:** setas/WASD andar · Shift correr · Espaço virar estátua · E (ou Q) iscar ·
Esc pausa · R recomeçar · M menu · N som · F tela cheia

**Celular:** arraste o dedo para andar · botões na tela ESTÁTUA, CORRER e ISCA ·
⏸ pausa · ↻ recomeçar · ⛶ tela cheia

## Regras rápidas

- A vida é 100 e cada batida/tiro tira `CONFIG.DANO` (34) → aguenta 3.
- Caixa escondida, ponte e modo estátua deixam você imune ao ônibus e aos tiros.
- 3 moedas compram uma bebida no menu de **Pausa** (recupera 1 batida).
- Vencer sobe de fase (o ônibus acelera um pouco) e a fase fica salva no navegador.
- Recordes de tempo são salvos no `localStorage`.

## Onde mexer (tudo em `index.html`)

O bloco `CONFIG` no começo do `<script>` controla o jogo sem precisar bagunçar o resto:

```js
AMEACA: 1        // 1 = o ônibus tem vida própria e arma | 2 = uma pessoa atira de cima
OBJETIVO: 3      // 1 = só pegar itens | 2 = só chegar na saída | 3 = itens e depois a saída
ITENS_META: 6    // quantos itens pegar por fase
DANO: 34         // dano por batida/tiro
MOEDAS_QTD: 4    // moedas por fase
ESCURIDAO: true  // holofote de visão em volta do jogador
MOEDAS_LOJA: 3   // preço da bebida
STOP_MOTION_FPS: 8  // quadros por segundo do "tremidinho" de stop motion
TREMOR: 2.2      // intensidade do tremor, em pixels
IMAGENS: {...}   // caminho das fotos de stop motion (vazio = desenho vetorial)
```

**Trocar os desenhos pelas suas fotos:** coloque os arquivos numa pasta (ex.: `fotos/`) e
preencha `IMAGENS`, por exemplo `jogador: "fotos/jogador.png"`. Tamanhos sugeridos:
logo 420×160 · chão 960×540 · jogador 40×40 · ônibus 100×44 (visto de cima, frente
para a direita) · pessoa 20×20 · item 24×24 · isca 24×24 · esconderijo 80×64 ·
saída 56×56. As imagens vazias continuam com o desenho vetorial, então dá para
trocar uma de cada vez.

## Estrutura do código

`index.html` é dividido em seções numeradas dentro do `<script>`:

1. `CONFIG` 2. preparação (canvas/mundo 960×540) 3. variáveis e recordes
4. efeito de stop motion 5. ajudantes de desenho e som 6. começar jogo
7. controles 8. movimento do jogador 9. IA do ônibus e arma 10. isca/itens/saída/vida
11. atualizar 12. desenhar (título, tutorial, jogo, pausa, fim) 13. loop principal

© Motion Games — nome do estúdio ainda provisório (aparece no topo de `index.html`
e na tela de título).
