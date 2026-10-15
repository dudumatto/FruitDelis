# FruitDelis — Aplicação

## Contexto do cliente

- 160 lojas em vários estados, sem padrão de loja.
- Tributação: ICMS varia por produto e localização; maior parte no Sudeste/Sul.
- 40–60 produtos.
- 200 logins/usuários.
- Sem domínio próprio.
- Admin com acesso para inserir produtos novos e clientes novos.

### Fluxo desejado

1. Entrar com login.
2. Selecionar produtos e colocar no carrinho.
3. Fechar a compra.
4. Gerar pedido e ordem de serviço.
5. Transformar em PDF e enviar por WhatsApp/e-mail, com notificação, dados da compra e produtos.

Cada produto tem foto, descrição, preço etc.

## O que preciso

- Custo
- Prazo de entrega
- Aplicar a paleta da empresa

## Escopo

**Páginas**

- Login
- Marketplace com os produtos
- Carrinho
- Informações da conta

**Outros**

- E-mail para cada unidade/loja.

---

## Detalhamento

### Stack e infraestrutura

Combinação escolhida: **Supabase Pro** (banco e backend) + **Cloudflare Pages** (site) + **serviço de e-mail transacional** (envio ao vendedor). Custo fixo: ~**R$ 145/mês**.

| Camada | Ferramenta | Função |
|---|---|---|
| Front-end | Cloudflare Pages | Hospeda o site mobile first (PWA) acessado pelos clientes. Plano gratuito, banda ilimitada |
| Banco de dados | Supabase Pro (região São Paulo) | Postgres com lojas, regiões, produtos, preços, pedidos e ordens de serviço |
| Login | Supabase Auth | Cadastro público desativado, JWT, perfis de acesso |
| Backend | Edge Functions do Supabase | Cálculo de preço e ICMS, geração do PDF, envio do e-mail |
| Arquivos | Supabase Storage (privado) | Fotos dos produtos e PDFs dos pedidos |
| E-mail | Resend ou similar | Envia o pedido ao vendedor |

### Fluxo da compra

1. O cliente faz login e seleciona os produtos.
2. Fecha a compra no carrinho.
3. O sistema gera o pedido e a ordem de serviço, com o preço da região e o ICMS calculados.
4. O sistema gera o PDF com os dados do cliente e da compra.
5. Um e-mail com todos os dados da compra e os produtos chega ao vendedor.

### Arquitetura e segurança

Toda regra que afeta dinheiro ou acesso roda no servidor; o navegador só exibe e envia as escolhas do usuário.

> *[Conteúdo embutido: fluxo do pedido · 5 componentes]*

Ao fechar o carrinho, a Edge Function lê e grava no banco, salva o PDF no Storage e chama o serviço de e-mail, que entrega o pedido ao vendedor.

#### Perfis de acesso

- **Admin (empresa):** cadastra produtos, regiões, lojas e clientes; altera preços e taxas; cadastra os e-mails dos clientes das lojas. Tudo pelo sistema.
- **Gerente / vendedor (loja):** perfis de loja, com isolamento por loja via RLS.
- **Cliente:** vê só o catálogo, os preços da sua região e os próprios pedidos e compras.
- **Cadastro fechado:** signup público desativado no Supabase; só e-mails pré-cadastrados entram. Cada cliente fica vinculado à sua loja e região.

#### Motor de preço e ICMS

- Uma tabela de regiões e UFs guarda a taxa de custo e as regras de ICMS por produto e localização.
- O preço é calculado no servidor e **congelado no pedido**, para que uma mudança de tabela não altere pedidos antigos.
- As regras fiscais vêm da fórmula e da tabela de ICMS da empresa, validadas pelo contador. Não são inventadas pelo projeto.

#### PDF e e-mail

- Ao fechar o carrinho, uma Edge Function recalcula tudo, grava o pedido e a ordem de serviço e gera o PDF com o design da empresa.
- O PDF fica em bucket privado; o cliente recebe um link com expiração, e o e-mail leva o PDF anexado ou esse link.
- O status do envio fica gravado, com nova tentativa automática e botão de reenviar.

#### Segurança

- Row Level Security (RLS) em todas as tabelas, com perfis (admin, gerente, vendedor) e isolamento por loja.
- Cadastro público desativado no Supabase. Só entram e-mails pré-cadastrados.
- Autenticação por JWT do Supabase, validada nas regras do banco e nas funções.
- Chave `service_role` só nas Edge Functions, nunca no front-end. Chaves de WhatsApp e do serviço de e-mail também só no servidor.
- Storage privado, com links assinados e expiração.
- Validação de entrada no servidor e limite de requisições.
- Log de auditoria: quem criou ou alterou pedido, produto e preço.
- Autenticação em dois fatores (MFA) obrigatória para admins.
- Revisão de segurança antes de publicar, testando acesso a dados de outra loja.
- Backup diário no plano Pro. Recuperação em ponto específico (PITR) é add-on pago, a avaliar conforme o volume de pedidos.
- Conformidade com a LGPD: não obriga hospedar no Brasil, mas exige contrato com o fornecedor e atenção à transferência internacional.

### Funcionalidades e design

O MVP tem nove entregas, todas desenhadas para celular primeiro e instaláveis como aplicativo (PWA).

- [ ] Login com cadastro fechado, JWT e perfis (admin, cliente)
- [ ] Catálogo de ~60 produtos com foto, descrição e preço da região do cliente
- [ ] Motor de preço por região e ICMS por produto e localização, calculado no servidor
- [ ] Carrinho e fechamento da compra, com preços congelados no pedido
- [ ] Pedido e ordem de serviço gerados juntos
- [ ] PDF com os dados do cliente e da compra, no design da empresa
- [ ] E-mail ao vendedor com os dados da compra e os produtos, com status de envio e reenvio
- [ ] Painel admin para cadastrar produtos, lojas, clientes e regiões
- [ ] Testes, revisão de segurança e publicação

#### Design e mobile

- Paleta, fontes, logo e modelos de documento da empresa já foram extraídos e viram os tokens do design system: cores, tipografia, espaçamentos e componentes.
- O mesmo design é aplicado no app e no PDF; aplicar também as informações/logo do vendedor.
- Mobile first: telas pensadas para o celular e depois ampliadas para o computador.
- Instalável como PWA, com possibilidade de notificação no aparelho.
