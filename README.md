# Bancada

Sistema de estoque, produção e caixa para recondicionamento de amortecedores.

## Fluxo

1. **Lote** – o caminhão de sucata chega: registra data, sucateiro, valor pago e quantidade aproximada. Ninguém conta peça por peça.
2. **Triagem** – ao separar nas baias, um toque no modelo para cada núcleo aproveitável (opcional, só para os modelos em destaque).
3. **Pronto** – a peça recondicionada ganha uma etiqueta com código de barras. **Só aqui ela entra no estoque de venda.**
4. **Pedido** – a venda é cadastrada e já reserva as peças (na Fase 2 entra sozinha do Mercado Livre).
5. **Embalagem** – bipa a etiqueta de cada peça do pedido; o sistema bloqueia peça errada.

Na tela **Estoque**, a coluna **Para anunciar** = prontas − reservadas − folga. É o número a usar nos anúncios.

## Papéis

| Papel | Telas |
|---|---|
| Dono | Tudo, inclusive Financeiro e Equipe |
| Gerente | Painel, Estoque, Pedidos, Lotes, SKUs, Triagem, Pronto, Embalagem |
| Produção | Triagem, Pronto, Estoque |
| Embalagem | Embalagem, Estoque |

## Implantação

1. **Supabase**: criar projeto (região South America – São Paulo). No SQL Editor, rodar `supabase/schema.sql` inteiro, uma vez.
2. **Supabase → Authentication → Providers → Email**: desligar "Confirm email" (opcional, facilita o primeiro acesso).
3. **Vercel**: importar este repositório do GitHub e configurar as variáveis de ambiente (valores em Supabase → Project Settings → API):
   - `NEXT_PUBLIC_SUPABASE_URL`
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - `SUPABASE_SERVICE_ROLE_KEY` (secreta; só no servidor)
4. Abrir o endereço publicado → **Primeiro acesso? Criar conta**. A primeira conta vira **Dono**.
5. Depois do primeiro acesso, em **Supabase → Authentication → Sign In / Providers**, desligar "Allow new users to sign up". A equipe passa a ser criada pela tela **Equipe**.

## Etiquetas

Tamanhos: 40×25, 50×30, 60×40 e 100×50 mm. Na impressão escolher a impressora térmica, o mesmo tamanho de papel e margens "nenhuma". O código é `A` + 7 dígitos (ex.: `A0000123`), em Code 128 — lido por leitor de pistola ou pela câmera do celular na tela Embalagem.

## Desenvolvimento

```
cp .env.example .env.local   # preencher
npm install
npm run dev
```

## Próximas fases

- **Fase 2**: Mercado Livre (3 contas) — importar pedidos automaticamente e atualizar a quantidade dos anúncios pelo SKU.
- **Fase 3**: Shopee (requer aprovação na Shopee Open Platform).
