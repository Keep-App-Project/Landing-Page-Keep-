# Keep — Landing Page

Landing page do **Keep**, plataforma web e mobile para gerenciamento de despensa, controle de validade de alimentos e redução de desperdício doméstico e comercial.

Projeto desenvolvido como Trabalho de Conclusão de Curso (TCC) — Técnico em Desenvolvimento de Sistemas, ETEC Taboão da Serra, Centro Paula Souza (2026).

---

## 🔗 Visão geral

Site construído em **HTML, CSS e JavaScript puros** (sem frameworks ou bibliotecas externas), com foco em:

- Uma experiência de rolagem guiada por seções (scroll-snap), com indicador visual de progresso
- Animações de entrada ao rolar a página
- Um sistema de "quadros" reutilizável (cartões com borda laranja e cantos arredondados) que dá identidade visual consistente a todas as seções
- Formulários funcionais (cadastro de usuário e avaliação) com validação em JavaScript puro, sem dependências

---

## 🗂️ Estrutura de pastas

```
/
├── index.html              → landing page principal
├── cadastro.html           → página de criação de conta
├── css/
│   ├── style.css           → estilos da landing page (compartilhado com cadastro.html)
│   └── cadastro.css        → estilos específicos da página de cadastro
├── js/
│   └── script.js           → toda a lógica JS do site (ver detalhes abaixo)
└── Images/
    └── ...                 → logos, ícones, ilustrações e fotos da equipe
```

> `style.css` é carregado em **ambas** as páginas (`index.html` e `cadastro.html`), pois concentra as variáveis de cor e componentes reutilizados (header, botões, cartões). Por isso, `script.js` também é compartilhado — cada bloco de funcionalidade nele é protegido por uma checagem (`if (elemento) { ... }`) para não quebrar em páginas onde aquele elemento específico não existe.

---

## 🎨 Paleta de cores

Definida como variáveis CSS no topo do `style.css` (`:root`), para que qualquer alteração de cor se propague pelo site inteiro a partir de um único lugar:

| Variável | Uso |
|---|---|
| `--laranja` | cor principal da marca |
| `--laranja-escuro` | hover de botões e detalhes |
| `--fundo-rosa` | fundo claro de seções específicas |
| `--texto` | texto escuro principal |
| `--texto-suave` | texto secundário/descrições |
| `--branco` | fundo de cartões e texto sobre fundo escuro |

O fundo da landing page (dentro do `.scroll-container`) é um **gradiente laranja contínuo**, que percorre a altura somada de todas as seções (usando `background-attachment: local`), criando a sensação de um "fundo único" por trás dos quadros sobrepostos — em vez de cada seção ter sua própria cor de fundo isolada.

---

## 🧱 Estrutura da página (`index.html`)

A página é dividida nas seguintes seções, todas dentro de um `.scroll-container` com `scroll-snap`:

1. **Hero** — headline principal, chamada para ação e ilustração do aplicativo (dois celulares sobrepostos)
2. **O Projeto** — contexto do TCC, o problema, a solução, e um bloco de documentação (monografia, apresentação, repositório)
3. **Por trás do Keep** — missão/visão da equipe, com cartões em efeito "vidro fosco" (glassmorphism) sobre uma imagem de fundo
4. **Principais Funcionalidades** — recursos do aplicativo
5. **Planos** — comparação entre Keep Home e Keep Business, com preços mensal/anual
6. **Nossa Equipe** — carrossel horizontal com foto, nome, função e links (GitHub/LinkedIn) de cada integrante
7. **Avaliação** — formulário de feedback com sistema de estrelas (1 a 5) e campo de comentário
8. **Footer** — logo, contatos, informações do TCC e créditos

A navegação do header (pílula flutuante fixa no topo) linka diretamente para os `id`s dessas seções.

---

## ⚙️ Funcionalidades em JavaScript (`js/script.js`)

Cada funcionalidade é isolada em seu próprio bloco, protegido por uma checagem de existência do elemento — o que permite que o mesmo arquivo seja usado em páginas diferentes sem gerar erros:

- **Indicador de progresso** — gera automaticamente uma bolha para cada `<section>` e destaca a atual usando `IntersectionObserver`; clicar em uma bolha rola até a seção correspondente.
- **Botão voltar ao topo** — aparece após 300px de rolagem; rola suavemente de volta ao início.
- **Animação de entrada** — qualquer elemento com a classe `.anima-entrada` (e opcionalmente `.atraso-1/2/3` para efeito cascata) sobe suavemente e ganha opacidade ao entrar na área visível, tanto subindo quanto descendo a página.
- **Carrossel da equipe** — navegação manual pelas setas (‹ ›), com loop infinito e destaque visual (`scale`) no card centralizado. **Sem avanço automático por tempo** — a rolagem é 100% controlada pelo usuário.
- **Formulário de cadastro** (`cadastro.html`) — validação de nome, e-mail, telefone e endereço; seleção de plano feita com checkboxes que se comportam como seleção única (mutuamente exclusivos via JS).
- **Formulário de avaliação** — sistema de estrelas construído com CSS puro (usando `flex-direction: row-reverse` + seletor `~`) para o efeito de preenchimento no hover; o clique fixa a nota escolhida.

> Nenhum formulário está conectado a um back-end real ainda — ambos fazem `console.log()` dos dados no envio, com um comentário no código indicando exatamente onde plugar uma API, Google Forms, Firebase ou serviço equivalente.

---

## 🖱️ Comportamento de rolagem

A landing page usa `scroll-snap-type: y` no container principal para que a maioria das seções "encaixe" ao rolar. **Duas exceções**, por conterem conteúdo de altura variável:

- `#equipe` (carrossel)
- Seções cujo conteúdo pode ultrapassar a altura de uma tela

Essas seções têm `scroll-snap-align: none` e `min-height: auto`, rolando livremente para evitar corte de conteúdo.

---

## 📱 Responsividade

O layout é *desktop-first*: grades multi-coluna (hero, cartões, planos) colapsam para coluna única em telas com largura até `860px`, via media queries ao final do `style.css`.


## 👥 Equipe

Desenvolvido pela equipe Keep — Vilturm Tecnologia e Soluções Digitais Ltda., como projeto de TCC da ETEC Taboão da Serra (Técnico em Desenvolvimento de Sistemas, 2026).
