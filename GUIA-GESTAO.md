# NORD STEEL — Guia de Gestão da Loja Online

Este guia explica como o proprietário da NORD STEEL pode gerir a loja online sem precisar de editar código. As instruções abaixo aplicam-se ao projeto Next.js construído.

## Onde estão os ficheiros principais

| O quê | Onde |
| --- | --- |
| Configuração da marca (nome, contactos, e-mail, Instagram) | `src/lib/brand.ts` |
| Cores da marca | `src/app/globals.css` (variáveis `--color-nord-*`) |
| Categorias de produtos | `src/data/categories.ts` |
| Catálogo de produtos | `src/data/products.ts` |
| Perguntas frequentes (FAQ) | `src/data/faq.ts` |
| Logótipo | `public/nord-steel-logo.svg` (substitui o ficheiro por um oficial) |

## 1. Adicionar ou editar produtos

Edita o ficheiro `src/data/products.ts` e segue o modelo de cada produto existente:

```ts
{
  id: "slug-do-produto",       // único, sem espaços
  name: "Nome do Produto",
  category: "pulseiras",       // usa um ID de categoria existente
  price: 1450,                 // em meticais
  inStock: true,               // false se esgotado
  shortDescription: "...",
  description: "...",
  material: "...",
  color: "Prata",
  sizes: ["M", "L"],
  isDemo: true,                // muda para false quando for um produto real
  gradient: "...",
  symbol: "◇",
}
```

## 2. Editar contactos (WhatsApp, e-mail, Instagram)

Edita `src/lib/brand.ts` e altera as constantes no início:

- `whatsappNumber` (ex.: `"258853170267"`)
- `whatsappDisplay` (ex.: `"+258 85 317 0267"`)
- `email` (ex.: `"nords.steel@gmail.com"`)
- `instagramHandle` e `instagramUrl`

Todos os botões de WhatsApp, e-mail e Instagram do website usam estes valores automaticamente.

## 3. Alterar o nome da marca ou slogan

Em `src/lib/brand.ts`:
- `name` — o nome da marca aparece em todo o site
- `slogan` — aparece como título principal da home
- `subtitle` — subtítulo da home
- `shortDescription` — aparece no rodapé

## 4. Substituir o logótipo

1. Coloca o ficheiro oficial em `public/nord-steel-logo.svg` (substitui o existente)
2. OU edita o componente `src/components/nord/Logo.tsx` para usar uma tag `<img>` real

## 5. Alterar as cores da marca

Edita as variáveis no topo de `src/app/globals.css`:

```css
--color-nord-black: #0B0B0B;       /* fundo principal */
--color-nord-secondary: #171717;    /* cartões */
--color-nord-white: #FFFFFF;        /* texto */
--color-nord-silver: #BFC3C7;       /* texto secundário */
--color-nord-light: #E8E8E8;        /* bordas e fundos claros */
```

## 6. Adicionar fotografias reais dos produtos

Para cada produto, em vez do gradiente demonstrativo, edita o componente `src/components/nord/ProductImage.tsx` para usar uma `<img src="/images/produtos/..." />`. As imagens devem viver em `public/images/produtos/`.

## 7. Editar perguntas frequentes (FAQ)

Edita `src/data/faq.ts` — cada item tem `question` e `answer`. Podes adicionar, remover ou reordenar livremente.

## 8. Ativar métodos de pagamento (M-Pesa, e-Mola)

Atualmente as encomendas são confirmadas via WhatsApp. Para ativar pagamentos online:

1. Confirmar a disponibilidade do fornecedor em Moçambique
2. Verificar compatibilidade com a plataforma
3. Configurar credenciais em variáveis de ambiente (`.env`)
4. Implementar a integração num endpoint API em `src/app/api/`
5. Testar antes de publicar como ativo

**Não apresentar estes métodos como ativos antes da configuração e dos testes.**

## 9. Ativar o envio automático do formulário de contacto

Atualmente o formulário abre o cliente de e-mail do utilizador. Para envio automático:

1. Configurar um serviço de e-mail (ex.: Wix Email Marketing, SendGrid, Resend)
2. Criar um endpoint API em `src/app/api/contact/route.ts`
3. Substituir o `window.location.href = mailtoUrl` por `fetch("/api/contact", ...)`
4. Não expor credenciais no código — usar variáveis de ambiente

## 10. Ligar um domínio próprio

Quando o site estiver pronto para publicação:

1. Adquirir um domínio (ex.: `nordsteel.co.mz`)
2. Configurar os DNS conforme as instruções da plataforma de hosting
3. Atualizar o `metadata` em `src/app/layout.tsx` com o URL oficial
4. Testar todos os fluxos antes de anunciar publicamente

## Próximos passos recomendados

1. **Substituir os produtos demonstrativos por produtos reais** (com fotografias, preços e características confirmados pelo fornecedor)
2. **Definir e publicar as políticas comerciais oficiais** (entregas, trocas, devoluções)
3. **Confirmar os métodos de pagamento** antes de os apresentar como ativos
4. **Configurar o envio automático do formulário** com um serviço de e-mail confiável
5. **Ligar um domínio próprio** antes do lançamento público
6. **Testar em dispositivos reais** (Android, iPhone, tablet) antes de publicar

---

**Contactos oficiais da marca:**
- WhatsApp: +258 85 317 0267
- E-mail: nords.steel@gmail.com
- Instagram: @nords.steel
