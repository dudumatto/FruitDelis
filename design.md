# Frutidélis — Design System

Fontes: site <https://frutidelis.com.br/> (WordPress + Elementor, tema Blazin, CSS computado) e PDF "FRUTIDELIS - PRESENÇA E EXPANSÃO" (4 páginas, A4, valores de cor amostrados dos pixels renderizados).

## 1. Marca

- Nome: **Frutidélis** (grafia com acento em "é"; logo: "frut!délis" com picolé laranja no lugar do "i").
- Logo: texto branco em bold arredondado sobre coral, contido em elipse com contorno branco fino. Picolé laranja `#e5853b` (tom do sorvete no "i").
- Variantes: `Frutidelis-Sem-Fundo.png` (site, fundo transparente), versão elipse sobre coral (PDF).
- Favicon: `/wp-content/uploads/2024/12/cropped-favicon-{32x32,180x180,192x192}.png`.
- Tom: acolhedor, direto, franquia/expansão. Ex.: "Cada cidade, uma conexão.", "O próximo capítulo pode começar com você."

## 2. Cores

### 2.1 Paleta de marca (PDF — mais fiel à identidade atual)

| Token | Hex | Uso |
|---|---|---|
| `coral` | `#f26246` | Fundo capa, faixa de header, bloco "Próximas aberturas", números de destaque |
| `cream` | `#fffdf8` | Fundo de página e cards (nunca branco puro) |
| `brown-900` | `#56352e` | Títulos, números secundários, texto forte |
| `brown-600` | `#6d5049` | Subtítulos, notas, rodapé |
| `blush` | `#fceae4` | Zebra de tabela (linhas ímpares) |
| `white` | `#ffffff` | Texto sobre coral |
| `orange-pop` | `#e5853b` | Detalhe do picolé no logo |

### 2.2 Paleta do site (Elementor global colors)

| Token | Hex |
|---|---|
| `--e-global-color-primary` | `#1c1c1c` |
| `--e-global-color-secondary` / `accent` | `#f6a440` (laranja-dourado) |
| `--e-global-color-text` | `#6d6c6c` |
| `--e-global-color-white` | `#ffffff` |
| `--e-global-color-dark-grayish` | `#a69ea5` |
| `--e-global-color-strong-red` | `#b51b41` |
| `--e-global-color-very-dark-gray` | `#686868` |
| `--e-global-color-light-gray` / `mostly-white` | `#f9f9f9` |
| `--e-global-color-very-light-gray` | `#ebebeb` |

Cores adicionais usadas em seções/botões do site:

| Hex | Onde |
|---|---|
| `#ec6c44` | Fundo de seção (CTA) e títulos H2 coral |
| `#f07140` | Recorrente em CSS (laranja-coral) |
| `#54595f` | Fundo de seção escura; texto de botão/ícones |
| `#69727d` | Botão cinza |
| `#61ce70` | Botão verde (CTA) e dot ativo do carrossel |
| `#25d366` | Botão flutuante WhatsApp |
| `#7a7a7a` | Texto corpo (body) |
| `#d1d1d1` | Dots inativos |
| `#12121a`/`#121a2f` | Azul-escuro do tema (pouco usado) |

> Observação: o site mistura laranja-dourado `#f6a440` e coral `#ec6c44`; o PDF consolida o coral em `#f26246`. Para material novo, usar a paleta 2.1 e `#f6a440` como acento.

### 2.3 Ruído do tema (ignorar)
Presets do WordPress/Bootstrap (`--wp--preset--*`, `#007bff`, `#dc3545`, `#28a745`…) vêm do tema Blazin e não fazem parte da marca.

### 2.4 Contraste
- Branco sobre `coral` `#f26246`: ~3.4:1 — OK só para texto grande/bold (≥18px bold). Para texto pequeno sobre coral, preferir peso 600+ ou `brown-900` sobre `cream`.
- `brown-900` sobre `cream`: ~11:1 (AAA).

## 3. Tipografia

| Contexto | Fonte | Observação |
|---|---|---|
| Site — tudo | **Manrope** (Google Fonts, via Elementor) | body 16px/500, títulos 800 |
| Site — secundárias | Roboto, Roboto Slab, Raleway (tema), Dosis | uso residual, parágrafos soltos |
| PDF | Sans-serif grotesca (Arial/Helvetica-like), bold nos títulos | |
| Ícones | FontAwesome 4/5/6, Flaticon, ElementsKit icons | |

Escala (site):

| Papel | Tamanho / peso | Cor |
|---|---|---|
| H1 hero | 36px / 800 | `#fff` |
| H3 destaque numérico | 42px / 800 | `#f6a440` |
| H2 seção | 22px / 800 | `#f6a440`, `#ec6c44`, `#fff`, `#54595f` |
| Body | 16px / 500 | `#7a7a7a` |
| Botão | 15px / 700 | — |
| Copyright | 14px / 400 | — |
| Presets WP | small 13 · medium 20 · large 36 · x-large 42 | |

Escala (PDF, A4 595×842pt): título capa ~48pt bold branco; número hero (151) ~80pt bold coral; título de página ~28pt bold `brown-900`; subtítulo ~13pt regular `brown-600`; tabela 10pt; cabeçalho de coluna 7pt caixa-alta com tracking; rodapé 8pt caixa-alta.

## 4. Espaçamento, forma, sombra

- Espaçamento (WP): `0.44 · 0.67 · 1 · 1.5 · 2.25 · 3.38 · 5.06 rem`.
- Raios: botão padrão `3px`; botão CTA pílula `20px`; WhatsApp `10px`; busca `50px`; logo em elipse total.
- Cards/blocos do PDF: retângulos de cantos retos, sem sombra, sem borda.
- Sombras do tema: `6px 6px 9px rgba(0,0,0,.2)` (natural), `12px 12px 50px rgba(0,0,0,.4)` (deep). Marca usa visual chapado — preferir sem sombra.
- Margens do PDF: ~55px laterais; linha fina branca separa header coral; linha fina cinza-clara separa rodapé.

## 5. Componentes

**Header (PDF):** faixa coral de ~100px, logo-elipse à esquerda, rótulo "PRESENÇA E EXPANSÃO" caixa-alta branco 600 à direita, filete branco inferior.

**Capa:** fundo coral total; eyebrow caixa-alta; H1 branco 2 linhas; subtítulo regular; card `cream` com métrica hero (coral) + métrica secundária (`brown-900`) + legenda; chamada final branca.

**Tabela (cidades × lojas):** 2 colunas lado a lado; cabeçalho 7pt caixa-alta `brown-600`; linhas alternadas `blush` / transparente; coluna "LOJAS" alinhada à direita em bold `brown-900`; linhas ~25px.

**Bloco de destaque:** retângulo coral, eyebrow caixa-alta, nome(s) em caixa-alta bold branco, nota pequena.

**Botões (site):** primário verde `#61ce70` (texto `#fff` ou `#54595f`, raio 3–20px, 15px/700); secundário cinza `#69727d` texto branco; WhatsApp flutuante `#25d366`.

**Carrossel:** Owl Carousel; dots `#d1d1d1`, ativo `#61ce70`.

**Rodapé (PDF):** filete, rótulo caixa-alta `brown-600` à esquerda, nº de página bold à direita.

## 6. Layout do site (home)

Seções em ordem: banner hero (vídeo/imagem + H1 branco) → diferenciais (cards com ícones PNG: Treinamento, Sorvetes, Ingredientes, Zero Royalties, Investimento com retorno certo) → produtos (Picolés, Massas, Clientes) → fábrica/vídeos → Missão / Visão / Valores → Mapa de unidades → números de franquia (investimento inicial, lucratividade média, retorno, funcionários, área mínima) → "Entre em contato" (formulário MetForm) → rodapé. Grid Bootstrap 12 col + Elementor; responsivo.

## 7. Imagens e assets

Base: `https://frutidelis.com.br/wp-content/uploads/`

**Logo / elementos**
- `2024/09/Frutidelis-Sem-Fundo.png` (+ `-300x182`)
- `2024/09/Elemento-Generico-01-1.png`, `Elemento-Generico-02.png`, `Elemento-Generico-03.png`
- `2023/05/scroll_down_image.png`
- `2024/12/cropped-favicon-*.png`

**Ícones de diferenciais**
- `2024/09/Treinamento.png`, `Sorvetes.png`, `Ingredientes.png`, `Clientes-1.png`, `Picoles-1.png`, `Massas-1.png`
- `2024/10/00-Zero-Royalties-e1729015389333.png`
- `2024/10/00-Investimento-com-retorno-certo-e1729015546706.png`
- `2024/10/Ativo-1fruti-e1729015687195.png`
- `2024/09/Missao.png`, `Visao.png`, `Valores.png`

**Números de franquia**
- `2024/10/01-Investimento-inicial-e1729015373420.png`
- `2024/10/02-Lucratividade-media.png`, `03-Funcionarios.png`, `04-Retorno.png`, `06-Area-minima.png`

**Fotografia**
- `2024/10/frutidelis_rodape.jpg`, `2024/10/fabrica.jpg`
- `2024/11/picole.jpg`, `2024/11/Panetone-com-pistache.00_02_40_20.Quadro003.jpg`
- `2024/11/Mapa-1.jpg`
- `2024/09/Entre-em-contato.jpg`, `Sobre-Nos.jpg`, `Sobre-Nos-2.jpg`, `Sobre-Nos-3.jpg`, `Sobre-Nos-3-1.jpg`

Estilo de imagem: ícones/ilustrações PNG recortados (fundo transparente), fotos de produto em close, cores quentes (coral/laranja) coerentes com a paleta.

## 8. Tokens CSS sugeridos

```css
:root {
  /* marca */
  --fd-coral: #f26246;
  --fd-cream: #fffdf8;
  --fd-brown-900: #56352e;
  --fd-brown-600: #6d5049;
  --fd-blush: #fceae4;
  --fd-orange: #f6a440;
  --fd-orange-logo: #e5853b;
  /* apoio (site) */
  --fd-text: #6d6c6c;
  --fd-ink: #1c1c1c;
  --fd-gray-100: #f9f9f9;
  --fd-gray-200: #ebebeb;
  --fd-green-cta: #61ce70;
  --fd-whatsapp: #25d366;
  --fd-red: #b51b41;
  /* tipografia */
  --fd-font: "Manrope", sans-serif;
  --fd-fs-body: 16px;
  --fd-fs-h2: 22px;
  --fd-fs-h1: 36px;
  --fd-fs-display: 42px;
  /* forma */
  --fd-radius-sm: 3px;
  --fd-radius-pill: 20px;
}
body { font-family: var(--fd-font); background: var(--fd-cream); color: var(--fd-brown-900); }
```

## 9. Dados do PDF (conteúdo de referência)

- 151 unidades no total (149 lojas ativas + 2 a inaugurar); 114 localidades com lojas ativas.
- Maiores praças: Birigui (13), Araçatuba (10), Bauru/Ilha Solteira/Ribeirão Preto (3).
- UF identificada: MS (8 cidades), MG (Iturama), PR (Maringá, Nova Esperança). Demais cidades sem UF na planilha (não inferir).
- Próximas aberturas: Teodoro Sampaio, Hortolândia.
- Fonte: `FRUTIDELIS CIDADES.xlsx`, aba Cidades.
