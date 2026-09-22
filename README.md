# Redesign AutoCare / DRIVEX

Documento do redesign da home de estética automotiva. O ponto de partida é o site antigo em [arnaldojseixasjr.github.io/site-antigo-autocare](https://arnaldojseixasjr.github.io/site-antigo-autocare/). A versão atual está em `index.html`, estilizada com Tailwind CSS.

## Cenário anterior

A página original, datada de 2012, é uma home única e estática. O conteúdo se resume a um título, um menu de quatro links, um parágrafo de boas-vindas, três serviços (polimento, vitrificação e lavagem) e um formulário de orçamento com nome e telefone.

A estrutura é uma coluna central de largura fixa. Não há imagens, hierarquia visual entre seções nem adaptação para telas menores. O próprio código marca as escolhas como práticas ruins de propósito: contraste ilegível, container rígido e marcação sem semântica.

## Três falhas graves

Estas três quebram o uso da página. As demais, listadas em seguida, pioram a leitura, mas não impedem sozinhas que alguém entenda a oferta ou conclua um pedido.

### 1. Contraste ilegível

O fundo é `#111111` e o texto do corpo é `#333333`. Títulos usam `#555555` e links `#777777`. Texto escuro sobre fundo escuro fica abaixo do mínimo de contraste para texto comum (WCAG 2.2, critério 1.4.3, razão 4.5:1). Na prática a home não se lê: o visitante não distingue serviços, preço “a combinar” nem o pedido de orçamento. Um redesign só se justifica se a informação principal voltar a ser visível.

### 2. Largura fixa, sem viewport

O conteúdo está em um bloco de `1200px`, sem `meta viewport`. Em um celular a página não se reflow: o navegador reduz o documento inteiro ou abre rolagem horizontal. Menu, parágrafos e campos do formulário saem da área útil. A maior parte do acesso a um serviço local acontece no telefone, então a página falha justamente no dispositivo em que o cliente tentaria chamar no WhatsApp ou preencher o orçamento.

### 3. Formulário que nunca envia

O único caminho de conversão é o pedido de orçamento. O `submit` chama `alert('Erro no servidor!...')` e retorna `false`. Não há validação, os rótulos não estão ligados aos campos (`for`/`id`) e o botão usa cinza `#666` sobre `#333`. O visitante preenche nome e telefone e recebe um erro falso. A ação de negócio da página está bloqueada.

## Falhas mapeadas

| Área | O que o site antigo faz | Efeito |
| --- | --- | --- |
| Contraste | Texto `#333` e títulos `#555` sobre fundo `#111` | O conteúdo some. O visitante não lê a oferta. |
| Tipografia | Times New Roman em todo o corpo | Visual de documento antigo, difícil de escanear. |
| Layout | Container de `1200px` fixos, sem `viewport` | A página quebra no celular e exige rolagem horizontal. |
| Semântica | `div` no lugar de `header`, `main`, `nav` e `footer` | Leitores de tela e mecanismos de busca não identificam as regiões. |
| Navegação | Links sublinhados em cinza, separados por `|` | O menu não indica a seção atual e não leva a âncoras reais (`href="#"`). |
| Serviços | Três caixas empilhadas, com borda e sem ícone | Os três serviços têm o mesmo peso visual e não se diferenciam. |
| Conteúdo | Texto sem acentuação e sem prova visual do resultado | A promessa de brilho e proteção não aparece na interface. |
| Formulário | `alert` de “erro no servidor” em todo envio | O pedido de orçamento nunca se completa. Não há validação nem rótulos ligados aos campos. |
| Marca | Título em caixa alta, sem logotipo | A empresa não tem uma marca reconhecível no topo. |

## O que o redesign implementou

A nova página mantém a mesma função — apresentar a estética automotiva e receber um pedido de orçamento — e reorganiza a interface em blocos com função clara.

- **Cabeçalho fixo** com o logotipo DRIVEX, menu para Início, Sobre, Serviços e Contato, e atalho de orçamento. No celular o menu vira uma faixa rolável. O item da seção visível fica marcado.
- **Hero** com a arte institucional da empresa. A imagem concentra marca, slogan e o que o serviço entrega: brilho, proteção de longa duração, aparência de novo, limpeza e valorização. Abaixo ficam os botões Ver Serviços e Entrar em Contato.
- **Carrossel de avaliações** com fotos de carros polidos (Unsplash), nota, serviço e depoimento. Há setas, pontos, deslize e troca automática que pausa quando o cursor está sobre o bloco.
- **Sobre e serviços** lado a lado no desktop. À esquerda, o texto institucional e o cartão “Acabamento sob medida”. À direita, cartões de Polimento, Vitrificação, Lavagem e Orçamento, com ícone e etiquetas.
- **Formulário de orçamento** com nome, telefone e serviço. Campos vazios ou telefone curto mostram o erro ao lado do campo. O envio válido troca o formulário por uma confirmação de retorno em até 48 horas. Não há servidor: a confirmação acontece na própria página.
- **Rodapé** com a identificação da empresa e os serviços.

A estilização usa Tailwind pelo CDN, a fonte Inter e uma paleta escura (fundo `#050816`, cartões em azul-noite, destaque em verde). O fundo tem uma grade discreta. Tudo se ajusta à largura da tela.

## Comparação direta

| | Site anterior | Redesign |
| --- | --- | --- |
| Documento | HTML com CSS interno | `index.html` + Tailwind |
| Marcação | `div` genéricas | `header`, `nav`, `main`, `section`, `form`, `footer` |
| Largura | 1200px fixos | Coluna fluida até `72rem`, com respiro lateral |
| Leitura | Texto escuro em fundo escuro | Texto claro sobre fundo escuro, com hierarquia de tamanho |
| Marca | “AUTOCARE ESTETICA AUTOMOTIVA” | Logotipo DRIVEX e banner institucional |
| Prova do serviço | Só texto | Banner e carrossel com carros polidos |
| Orçamento | Alerta de erro | Validação e mensagem de pedido recebido |
| Celular | Quebra a página | Menu, cartões e formulário empilham |

## Como abrir

Abra `index.html` no navegador. O Tailwind e as fotos do carrossel vêm da rede. O logotipo (`logo-drivex.png`) e o banner (`drivex-hero.png`) ficam na pasta do projeto.
