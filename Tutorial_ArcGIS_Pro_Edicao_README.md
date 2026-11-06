<p align="center">
  <img src="./img/edicao-arcgis/logo-geoapuc.png" alt="Logo GeoAPUC" width="200"/>
</p>

# 🛠️ Tutorial Edição no ArcGIS Pro — Manual de manutenção

**Como alterar o tutorial pelo VS Code com o Claude**

Este arquivo explica como o tutorial **Edição no ArcGIS Pro para o Cadastro** está organizado e como fazer alterações futuras pedindo ao Claude (extensão do VS Code). Ele vale para o professor e para o Claude: **o Claude deve ler este arquivo inteiro antes de qualquer alteração.**

- Tutorial publicado: <https://engemap.github.io/GeoApuc_Tutoriais/Tutorial_ArcGIS_Pro_Edicao.html>
- Versão em texto: [Tutorial_ArcGIS_Pro_Edicao.md](./Tutorial_ArcGIS_Pro_Edicao.md)

---

## 📑 Índice

1. [Os arquivos do tutorial](#arquivos)
2. [A regra de ouro: alterar os dois](#regra)
3. [Como pedir uma alteração](#pedir)
4. [Como o HTML é montado](#html)
5. [Trocar ou acrescentar uma tela (print)](#prints)
6. [Testes rápidos (quiz)](#quiz)
7. [Base de treino](#base)
8. [Publicar no GitHub](#publicar)
9. [O que nunca fazer](#nunca)

---

## 📁 Os arquivos do tutorial <a id="arquivos"></a>

Tudo fica na raiz do repositório `GeoApuc_Tutoriais`:

| Arquivo / pasta | O que é |
|---|---|
| `Tutorial_ArcGIS_Pro_Edicao.html` | **A página publicada.** É o que os alunos abrem. |
| `Tutorial_ArcGIS_Pro_Edicao.md` | **O texto de referência**, em Markdown. Mais fácil de ler e revisar. |
| `Tutorial_ArcGIS_Pro_Edicao_README.md` | Este manual. |
| `img/edicao-arcgis/` | As 34 telas do tutorial + `logo-geoapuc.png` e `logo-geoapuc-branco.png`. |
| `dados/CTM_Treino_Centro.zip` | A base de treino que o aluno baixa (≈ 0,5 MB). |
| `index.html` | Página inicial do repositório; tem o link para este tutorial. |

> ⚠️ **Atenção:** o `README.md` da raiz é do tutorial **Viabilidade Econômica**. Não altere esse arquivo quando o assunto for o tutorial de edição.

> 🔒 **Fora do repositório (só com o professor):** `Gabarito_Professor_Tutorial_ArcGIS_Pro_Edicao.html` / `.pdf`, com as respostas dos testes e o que esperar de cada exercício. **Nunca** coloque o gabarito no GitHub — o repositório é público.

---

## 🥇 A regra de ouro: alterar os dois <a id="regra"></a>

O `.md` é o texto de referência; o `.html` é o que vai para o ar. **Toda alteração de conteúdo é feita nos dois arquivos, na mesma resposta.**

1. O Claude altera o trecho no `Tutorial_ArcGIS_Pro_Edicao.md`.
2. O Claude localiza o trecho correspondente no `Tutorial_ArcGIS_Pro_Edicao.html` e aplica **a mesma** alteração, respeitando os componentes do HTML (passos, carrosséis, marcadores, caixas, quiz).
3. O Claude mostra um resumo do que mudou nos dois arquivos e avisa se algo **só existe** em um deles (por exemplo, a posição de um marcador só existe no HTML).

Se os dois arquivos discordarem, o **HTML publicado** é o que os alunos viram: o Claude pergunta antes de "corrigir" um pelo outro.

---

## 💬 Como pedir uma alteração <a id="pedir"></a>

No chat do Claude no VS Code, cite este manual com `@` e diga o que quer. Exemplos:

```text
@Tutorial_ArcGIS_Pro_Edicao_README.md No Bloco C, passo 1, troque "Midpoint" por "Edge" e replique no HTML.
```

```text
@Tutorial_ArcGIS_Pro_Edicao_README.md Acrescente no Bloco D um exercício D5 sobre Select By Location, no mesmo formato dos outros exercícios, nos dois arquivos.
```

```text
@Tutorial_ArcGIS_Pro_Edicao_README.md Coloquei a imagem img/edicao-arcgis/B11_trace.png. Crie uma tela no carrossel do Bloco B, passo 2, com 3 marcadores: (1) botão Trace, (2) linha seguida, (3) Finish.
```

```text
@Tutorial_ArcGIS_Pro_Edicao_README.md Mude a resposta certa da pergunta 2 do teste do Bloco A e me diga o que preciso atualizar no gabarito.
```

> 💡 **Dica:** peça uma coisa por vez e confira no navegador (abra o `.html` direto do disco) antes de publicar. Se não gostar, peça "desfaça a última alteração nos dois arquivos".

---

## 🧱 Como o HTML é montado <a id="html"></a>

O HTML é **um arquivo só**, com o CSS e o JavaScript embutidos no próprio arquivo. As imagens ficam em `./img/edicao-arcgis/`. Não há etapa de "build": edite o HTML diretamente.

### Seções e menu lateral

Cada parte é uma `<section class="bloco" id="...">`. O menu lateral aponta para estes `id` — **não renomeie**:

| id | Seção | Prefixo dos ids internos |
|---|---|---|
| `introducao` | 🎯 Introdução | — |
| `ambiente` | 🧰 Preparar o ambiente | — |
| `bloco-a` | 🖥️ Bloco A — guia Edit | `a-` |
| `bloco-b` | 🧲 Bloco B — Snapping e construção | `b-` |
| `epilogo` | 📜 Epílogo (dentro do Bloco B) | — |
| `bloco-c` | 🧩 Bloco C — Editar lotes | `c-` |
| `bloco-d` | 🗂️ Bloco D — Atributos | `d-` |
| `atalhos` | ⌨️ Atalhos e glossário | — |

Dentro de cada bloco: **A · Passo a passo**, **B · Mão na massa**, **C · Teste rápido**, **D · Para aprofundar** (títulos `h3.sub`). No fim de cada bloco há a navegação anterior/próximo. Se uma seção nova for criada, ela precisa de um item no menu lateral (`nav`) e na lista do Índice do `.md`.

### Componentes e como aparecem no `.md`

| Componente no HTML | Para que serve | Como aparece no `.md` |
|---|---|---|
| `<details class="passo"><summary><span class="num">1</span>Título<span class="seta">›</span></summary><div class="corpo">…</div></details>` | Passo numerado que abre/fecha | `#### 1️⃣ Título` |
| `<ol class="passos">` | Lista de cliques do passo | Lista numerada |
| `<div class="carrossel" id="a-c1">` com `<figure class="slide">` | Telas com setas ‹ › | Imagens em sequência + legenda |
| `<span class="mk" style="left:X%;top:Y%">1</span>` | Marcador numerado sobre a tela | `- **(1)** texto` |
| `<ol class="leg">` dentro do `figcaption` | Legenda dos marcadores | Mesma lista acima |
| `<div class="box dica">` / `info` / `aviso` / `perigo` | Caixas 💡 🗺️ ⚠️ 🛑 | `> **💡 Título**` (citação) |
| `<div class="confira">` | ✅ Confira | `> ✅ Confira` + lista |
| `<div class="exercicio">` (+ `desafio`) | Exercício com tempo e Confira | `#### Exercício X1 — …` |
| `<details class="dica-desafio">` | Dica/solução escondida do desafio de 1 ha | `<details><summary>…</summary>` |
| `<span class="caminho">` | Caminho, campo ou expressão | `` `código` `` |
| `<kbd>G</kbd>` | Tecla | `<kbd>G</kbd>` |
| `<svg>` dentro de `.svgbox` | Diagramas do epílogo e do memorial | _(Diagrama no tutorial HTML: …)_ |

### Carrossel: regras

- Cada `figure.slide` tem: `div.tela` (com `style="max-width:Lpx"` = largura da imagem), o `img` com `width`/`height` reais, os `span.mk` e o `figcaption` com `<strong>n/total · Título</strong>` e a `ol.leg`.
- O **primeiro** slide leva `class="slide ativo"`.
- Abaixo dos slides há `div.nav` com um botão `dot` por slide (`data-i="0"`, `"1"`…; o primeiro com `ativo`). **Ao acrescentar ou remover um slide, ajuste os dots e a numeração `n/total` de todos os slides daquele carrossel.**
- O número do marcador (`span.mk`) e o da legenda (`span.mkl`) têm que coincidir.

---

## 🖼️ Trocar ou acrescentar uma tela (print) <a id="prints"></a>

1. **Nome da imagem:** letra do bloco + número + descrição, em `img/edicao-arcgis/`. Ex.: `B11_trace.png`, `D04_select_location.png`. Prefira PNG, com até ~1000 px de largura, já recortado só na parte que interessa.
2. **Posição do marcador:** em porcentagem da imagem.
   - `left = x_pixel ÷ largura × 100`
   - `top = y_pixel ÷ altura × 100`
   - Use o centro do botão/campo indicado, com 2 casas decimais. Se recortar a imagem, desconte o recorte antes de calcular.
   - Para o Claude calcular, diga a posição em pixels (ex.: "marcador 1 no pixel 210, 85") ou descreva o elemento e peça para ele estimar — e confira no navegador.
3. **No `.md`:** `![Texto alternativo](./img/edicao-arcgis/B11_trace.png)` + legenda em itálico + lista `**(1)**…`.
4. **Evite marcadores sobrepostos:** deixe pelo menos ~5% entre eles.

> 💡 **Dica:** telas sempre sobre a **base de treino** (bookmark *quadra 101.014*), sem camadas extras no Contents e sem dados pessoais (LGPD).

---

## ❓ Testes rápidos (quiz) <a id="quiz"></a>

As perguntas **não** estão escritas no HTML visível: ficam no objeto `QUIZ` no `<script>` do fim do arquivo e são desenhadas pelo JavaScript em `<div id="quiz-a">`, `quiz-b`, `quiz-c`, `quiz-d`.

```js
var QUIZ={"a":[
  {p:'Pergunta?', o:['Opção A','Opção B','Opção C'], c:1, e:'Explicação mostrada depois da resposta.'},
  …
],"b":[…],"c":[…],"d":[…]};
```

- `p` = pergunta · `o` = opções (2 a 4) · `c` = **índice** da certa, começando em 0 (0 = A, 1 = B, 2 = C, 3 = D) · `e` = explicação.
- Todas as perguntas têm **uma única resposta certa**.
- Use aspas simples nos textos; se o texto tiver apóstrofo, escreva `\'`.
- No `.md`, as perguntas aparecem como lista com a resposta dentro de `<details><summary>Ver resposta</summary>`.

> 🛑 **Mudou uma pergunta, uma opção ou a resposta certa?** O gabarito do professor fica desatualizado. O Claude deve **avisar** quais perguntas mudaram, para o professor atualizar o gabarito (que fica fora do repositório).

---

## 🗺️ Base de treino <a id="base"></a>

`dados/CTM_Treino_Centro.zip` contém `CTM_Treino.gdb` (SIRGAS 2000 / UTM 22S, EPSG 31982), `Bookmarks_Tutorial_CTM.bkmx` e `LEIA-ME.txt`.

| Camada | Feições |
|---|---|
| Lotes | 5.020 (bairro Centro, campos pessoais e fiscais removidos) |
| Quadras | 219 |
| Logradouros | 120 |
| Edificacoes | 0 (vazia, para desenhar) |

Números usados nos exercícios (se a base mudar, eles precisam ser revistos no `.md`, no HTML e no gabarito):

- Lote D2 `101-014-0355-001`: 30 × 38,5 = **1155 m²**; metades de **577,50 m²**.
- Lote vago V2 `101-014-0240-001`: **406,48 m²** no desenho × **375 m²** no cadastro.
- Edificação: 10 × 12 = **120 m²**; lados da quadra 101.014 a **165°17'23"** e **75°17'23"** (NAz).
- O tamanho do zip aparece no botão de download (`~0,5 MB`) — atualize se trocar o arquivo.

---

## 🚀 Publicar no GitHub <a id="publicar"></a>

1. No repositório `engemap/GeoApuc_Tutoriais`: **Add file › Upload files**.
2. Arraste os arquivos alterados (`.html`, `.md` e, se houver, as imagens novas dentro de `img/edicao-arcgis/`).
3. Escreva uma mensagem curta (ex.: "Bloco C: corrige passo 1") › **Commit changes**.
4. Aguarde o GitHub Pages publicar (aba **Actions**, alguns minutos) e abra o tutorial com <kbd>Ctrl</kbd>+<kbd>F5</kbd> para não ver a versão antiga do cache.

> 💡 **Dica:** se o repositório estiver clonado no computador, dá para fazer commit e push pelo próprio VS Code.

---

## 🚫 O que nunca fazer <a id="nunca"></a>

- Colocar o **gabarito** do professor no repositório.
- Publicar dados com **nome, CPF, endereço de contribuinte ou valores fiscais** (LGPD).
- Alterar o `README.md` da raiz (é do tutorial Viabilidade Econômica).
- Renomear os `id` das seções ou os nomes das imagens sem atualizar todas as referências.
- Mudar a **ordem das opções** dos testes sem atualizar o gabarito.
- Reintroduzir temas que foram retirados de propósito por serem avançados para iniciantes: **domínios, topologia/validação, rastreabilidade de processos e versionamento** (e Parcel Fabric, que não há licença).
- Escrever "ArcGIS Pro Standard": o nome usado no tutorial é **ArcGIS Professional**.

---

**Tutorial - Edição no ArcGIS Pro para o Cadastro | Apucarana - PR**
📧 idepplan@apucarana.pv.gov.br · 📱 (43) 3422-4000
