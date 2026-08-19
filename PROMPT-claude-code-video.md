# Prompt para o Claude Code — Melhorar o protótipo Vitryx para o vídeo

> **Como usar:** coloque numa mesma pasta o arquivo HTML do protótipo (ex.: `vitryx.html`) e o arquivo `REQUISITOS-Desafio01-Medianeira.md`. Abra o Claude Code nessa pasta e cole o texto abaixo. Ajuste o nome do arquivo HTML se for diferente.

---

Você vai trabalhar em um único arquivo HTML: **`vitryx.html`** (ajuste o nome se necessário). É uma SPA em HTML + Tailwind (via CDN) + Lucide + Leaflet, com todo o JavaScript embutido e `localStorage` para dados de demonstração. É um protótipo da plataforma **Vitryx Conecta**, para o município de Medianeira-PR, que vou usar para **gravar um vídeo de demonstração** de um edital público (CPSI nº 01/2026, Desafio 01 — Páginas Amarelas Inteligentes).

Antes de qualquer alteração, **leia estes dois arquivos**:
1. `vitryx.html` — o protótipo atual, para entender a estrutura existente.
2. `REQUISITOS-Desafio01-Medianeira.md` — os requisitos oficiais do desafio, já conferidos contra o edital. Use como referência do que a solução precisa demonstrar.

## Contexto e objetivo

O objetivo **não é** tornar o sistema real ou funcional em produção. É deixá-lo **coerente e convincente para uma gravação de vídeo**. O critério de sucesso é: *um avaliador atento que compare as telas entre si não deve encontrar nenhuma contradição, e todo requisito do desafio deve ter uma tela ou elemento que o evidencie.*

## Regras invioláveis

1. **Trabalhe sempre no arquivo existente. Não reescreva do zero.** Faça edições cirúrgicas, preservando estrutura, estilo e o que já funciona.
2. **Nenhum número exibido nos painéis pode ser fixo/hardcoded.** Todo indicador (total de empresas, percentuais, contagens, gráficos) deve ser **calculado dinamicamente a partir da base de dados de demonstração**. Se a base tem 15 empresas, o painel diz 15 — nunca 412.
3. Mantenha o padrão visual atual (azul `brand`, laranja `accent`, sem emojis, fonte Inter).
4. Após terminar, faça uma **varredura final** e me relate: (a) o que mudou, (b) qualquer número que ainda seja fixo, (c) qualquer requisito do desafio que ainda não tenha evidência na tela.
5. Se algo não puder ser feito sem quebrar outra parte, **pare e me pergunte** — não improvise.

## Trabalho a fazer, em ordem

### 1. Base de demonstração — ~15 negócios coerentes de Medianeira
Ajuste o seed de negócios para **cerca de 15 registros** plausíveis para Medianeira-PR, no mesmo formato dos existentes:
- Nomes e endereços plausíveis (bairros reais: Centro, Ipê, Nazaré, Bairro Fron, Belo Horizonte, Cidade Alta, Parque Independência).
- Coordenadas próximas ao centro (aprox. `-25.2983, -54.0933`), variando levemente.
- Categorias variadas: Beleza, Casa e Manutenção, Automotivo, Alimentação, Comércio, Serviços, Tecnologia, Rural/Agricultura familiar.
- Campo de **origem** variado: `Cadastro do Empreendedor`, `Base Importada` (cadastrada pela Prefeitura), `Sincronizado`.
- **3 ou 4 negócios com origem "Base Importada" e SEM vitrine pública / sem catálogo** — representando o caso do edital (item 4.1.5) em que a Prefeitura cadastra a empresa (nome, CNAE, porte, endereço) sem vitrine ainda.
- **2 ou 3 com validação "pendente"** (para haver o que aprovar ao vivo), o resto "validado".
- Inclua uma **Marcenaria** com palavras-chave `marcenaria, conserto, móveis, cadeira` (para casar com a busca de conserto e a demanda pública de reparo de mobiliário escolar).
- **NÃO inclua** negócio de ar-condicionado (esse termo precisa retornar vazio — ver passo 4).
- `stats` de cada negócio com números pequenos e realistas (dezenas).

### 2. Todos os indicadores do painel do gestor — derivar da base
Reescreva os cálculos para serem derivados da base do passo 1:
- Total de empresas = tamanho da base.
- Distribuição por porte / segmento / origem = contagem real.
- Com vitrine × sem vitrine = contagem real (as "Base Importada" sem catálogo contam como sem vitrine).
- Georreferenciadas (%) = % com lat/lng válidos.
- Atualizadas (%) = % com data nos últimos 12 meses.
- Validadas × pendentes = contagem real.
- Gráficos alimentados pelos mesmos números.
- Se um card exibir número que não dá para calcular da base, **remova o card**.

### 3. Painel de Impacto — coerente e honesto
Recalcule com base em eventos proporcionais à base (algumas centenas de buscas, não milhares) **ou** reduza os números fixos para valores plausíveis para Medianeira. Em qualquer caso, mantenha visível o rótulo **"dados demonstrativos"**. Nunca sugira que são dados reais de operação.

### 4. Fluxo da lacuna ("instalador de ar") — precisa funcionar
Buscar por **"instalador de ar"** / **"ar condicionado"** (na busca pública e no chat da assistente) **não deve retornar nenhum negócio** e deve **registrar a demanda** para a Prefeitura. Esse termo deve então aparecer na tela de **lacunas / buscas sem resultado** do gestor, com contagem plausível.

### 5. Prefeitura cadastra sem vitrine — deixar visível na narrativa
Na tela **Base Econômica** do gestor:
- Exiba coluna/etiqueta de **Origem** e marcação clara de **"Sem vitrine"** para os importados.
- Ao clicar num negócio importado, o modal de detalhes mostra os **dados cadastrais** (nome, porte, CNAE, endereço, origem) e deixa claro que **ainda não há vitrine pública** (texto tipo "Aguardando reivindicação do empreendedor" — apenas texto, sem fluxo real).

### 6. Textos de apoio no cadastro (onboarding do empreendedor)
- Campo **Descrição Pública**: `placeholder` ex.: `Ex: Faço unhas em gel, alongamento e esmaltação. Atendo com hora marcada no Centro.`
- Campo **Palavras-chave**: texto de ajuda pequeno abaixo: `Ex: manicure, unha em gel, alongamento. Digite um termo e aperte Enter.`
- Campo **CNAE (opcional)**: texto de ajuda: `Código da sua atividade econômica. Se não souber, deixe em branco — a Prefeitura pode preencher depois.`

### 7. Análise de Lacuna — remover "CNAE Sugerido"
No modal de análise de lacuna, **remova o card "CNAE Sugerido"** (promete algo que não é gerado). Mantenha termo buscado, contagem de buscas e "Ação Recomendada". Ajuste o layout.

### 8. Solicitar Correção — indicar canal
Quando o gestor solicitar ajuste ao empreendedor, o toast deve dizer: `Solicitação de ajuste enviada. O empreendedor será notificado no WhatsApp cadastrado.` (Só texto — sem integração real.)

### 9. Evidência dos requisitos que hoje são invisíveis
Alguns requisitos do desafio são "capacidade do produto" e não aparecem em tela. Sem forçar, adicione evidências leves e honestas onde fizer sentido, por exemplo:
- Na tela de exportação, manter os três formatos (**CSV, JSON, GeoJSON**) com o selo de LGPD (item 4.1.1 IX).
- Na auditoria, deixar claro que registra acesso, alteração, exportação (item 4.1.1 III).
- No rodapé ou numa tela "sobre", uma nota curta de que a plataforma observa disponibilidade, criptografia em trânsito e reversibilidade dos dados (itens 4.1.1 e 4.1.3) — como texto informativo, não número inventado.
Não crie telas falsas nem números fabricados; apenas torne visível o que a solução se propõe a cumprir.

### 10. Varredura final anti-contradição
Antes de finalizar, procure e corrija qualquer número, rótulo ou placeholder ("lorem ipsum", "412 empresas", "5.420 buscas", nomes genéricos) que contradiga a base de 15 negócios. Depois me entregue o relatório pedido na regra 4.

---

**Comece lendo os dois arquivos e me apresentando um plano curto do que vai mudar, antes de editar.** Quero aprovar o plano antes de você começar a alterar o HTML.
