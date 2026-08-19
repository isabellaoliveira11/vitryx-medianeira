# Requisitos do Desafio 01 — CPSI nº 01/2026 Medianeira/PR
## "Páginas Amarelas Inteligentes: conectando a oferta local às demandas públicas e privadas"

> Documento de referência interno. Consolida os requisitos do **Termo de Referência oficial do Desafio 01** (Processo Administrativo 1.832/2026, Fase Preparatória), conferidos item a item contra o texto assinado. A coluna "Status no protótipo" é um rascunho para você ajustar conforme for validando cada tela.
>
> **Validado contra o documento oficial em 18/08/2026.** Numeração de itens, percentuais dos marcos e metas conferidos e corretos.

---

## Contexto do desafio (item 4.1)

A solução deve estruturar e dar visibilidade à economia local de Medianeira — comércio, prestadores de serviço, autônomos e agricultura familiar — em um portal público, funcionando como "páginas amarelas inteligentes". Deve servir simultaneamente ao **cidadão** (encontrar oferta local), ao **empreendedor** (visibilidade) e à **gestão pública** (inteligência econômica territorial), e ser **aberta ao público**, favorecendo também vendas **B2B** (entre empresas) e **B2C** (empresa ao consumidor) e a atração de clientela regional.

**Ponto crítico (item 4.1.5):** a **coleta de dados junto às empresas é responsabilidade da Prefeitura**. Cabe à solução fornecer os mecanismos de **armazenamento, tratamento, organização e análise** dos dados coletados e **sugerir fontes de dados** que possam alimentar a plataforma. Ou seja, a solução precisa permitir que a Prefeitura **cadastre/importe empresas mesmo sem vitrine pública**.

---

## A. Requisitos funcionais mínimos (item 4.1)

| # | Requisito | Status no protótipo |
|---|-----------|---------------------|
| A1 | **Cadastro estruturado** de empresas, prestadores e produtores locais | Atende (vitrine + dados de negócio) |
| A2 | **Classificação** por porte, CNAE, segmento/categoria, tags e palavras-chave | Atende (busca e filtros por esses campos) |
| A3 | **Georreferenciamento** das empresas (localização em mapa) | Atende (Leaflet / mapa) |
| A4 | **Busca inteligente** por necessidade, com filtros avançados | Atende (busca com sinônimos + filtros) |
| A5 | **Painel gerencial** com indicadores econômicos e de compras públicas | Atende (visão territorial) — checar números |
| A6 | **Atualização e validação periódica** das informações | Atende (fluxo de validação municipal) |
| A7 | **Importação de dados** e integração futura com bases públicas | Parcial (tela existe; import real é do produto) |
| A8 | **Indicadores de participação** de empresas locais em compras públicas | Parcial (cruzamento informativo demanda × oferta) |
| A9 | **Geração de relatórios** e planilhas gerenciais | Parcial (exportação; relatórios a detalhar) |
| A10 | **Rastreabilidade e histórico** de atualização dos registros | Atende (trilha de auditoria) |
| A11 | **Controle de acesso por perfis** de usuário | Atende (cidadão, empreendedor, gestão) |
| A12 | **Conformidade com a LGPD** | Atende (minimização, proteção de endereço, anonimização) |

---

## B. Segurança da informação (item 4.1.1)

| # | Requisito | Status no protótipo |
|---|-----------|---------------------|
| B1 | Autenticação de usuários | Atende (login por perfil) |
| B2 | Controle de acesso baseado em perfis | Atende |
| B3 | Registro de logs de acesso e alteração | Atende (auditoria) |
| B4 | Criptografia em trânsito (HTTPS/TLS) | Capacidade do produto (não visível no protótipo) |
| B5 | Política de backup e restauração | Capacidade do produto |
| B6 | Separação entre ambiente de teste e produção | Capacidade do produto |
| B7 | Exportação em formato aberto, estruturado e interoperável | Atende (CSV / JSON / GeoJSON — botões demonstrativos) |
| B8 | Reversibilidade dos dados ao término do contrato | Capacidade do produto (garantida em proposta) |

---

## C. Uso responsável de inteligência / IA (item 4.1.2)

> Aplicável porque a solução usa inteligência aplicada à busca e organização. Se houver IA, deve observar:

| # | Requisito | Status no protótipo |
|---|-----------|---------------------|
| C1 | Finalidade específica e transparente do uso de inteligência | Atende (busca e organização da oferta) |
| C2 | Critérios de classificação claros | Atende ("apareceu por: nome, catálogo, categoria, palavra-chave") |
| C3 | Rastreabilidade das fontes de dados | Atende (origem do dado + auditoria) |
| C4 | Revisão humana das decisões | Atende (validação pela gestão) |
| C5 | Explicabilidade mínima dos resultados | Atende (selo "apareceu por") |
| C6 | Ausência de viés/direcionamento — sem ranqueamento pago | Atende (neutralidade por concepção) |
| C7 | Logs das operações de inteligência | Atende (auditoria) |

---

## D. Parâmetros de desempenho e qualidade (item 4.1.3)

| # | Requisito | Meta | Status no protótipo |
|---|-----------|------|---------------------|
| D1 | Disponibilidade mínima | ≥ 95% | Capacidade do produto |
| D2 | Tempo médio de resposta em consultas gerenciais | < 5 segundos | Capacidade do produto |
| D3 | Completude dos registros | > 90% | A pactuar no piloto |
| D4 | Geração automatizada de relatórios e indicadores | — | Parcial |
| D5 | Rastreabilidade das alterações na base | — | Atende (auditoria) |

---

## E. Perfis de usuário e experiências (item 4.1 / fluxos)

| # | Perfil | O que deve fazer | Status no protótipo |
|---|--------|------------------|---------------------|
| E1 | **Cidadão** (público, sem login) | Buscar por necessidade, ver lista + mapa, ver vitrine, contatar por WhatsApp | Atende |
| E2 | **Empreendedor** | Criar/gerir vitrine, catálogo, horários, localização com proteção de endereço, ver indicadores | Atende |
| E3 | **Gestão municipal** | Visão territorial, validar cadastros, ver lacunas, relacionar demandas, importar/exportar, auditar | Atende — checar números |
| E4 | **Prefeitura como cadastradora** (item 4.1.5) | Cadastrar/importar empresa **sem vitrine** (dado bruto: nome, CNAE, porte, endereço) | A evidenciar (seed "Base Importada / Sem vitrine") |

---

## F. Escopo de valor / metas de referência (item 4.1.6)

| # | Item | Referência do TR |
|---|------|------------------|
| F1 | Cobertura da base | Ao menos **30% das empresas de cada porte** (MEI, ME, EPP) |
| F2 | Adoção pela gestão | Entre **10 e 20 servidores** usuários |
| F3 | Abertura ao público | Plataforma pública, com uso B2B e B2C |
| F4 | Inteligência gerada | Mapa de lacunas + relatório de impacto ao final |

---

## G. Marcos de entrega e pagamento (item 10.3.2)

| Marco | Entrega principal | % | Valor (sobre R$ 60.000) |
|-------|-------------------|---|--------------------------|
| M-1 | Imersão e Mapeamento do Ecossistema Local (Plano de Trabalho aprovado) | 10% | R$ 6.000,00 |
| M-2 | Estruturação da Base de Dados (taxonomia, tags, CNAEs, georreferenciamento) | 10% | R$ 6.000,00 |
| M-3 | Desenvolvimento da Solução (busca inteligente, painéis, interface) | 20% | R$ 12.000,00 |
| M-4 | Capacitação e Preparação Operacional (usuários treinados, material) | 10% | R$ 6.000,00 |
| M-5 | Implantação Piloto e Validação Operacional (plataforma em uso real) | 30% | R$ 18.000,00 |
| M-6 | Consolidação e Validação Final (relatório de impacto e viabilidade) | 20% | R$ 12.000,00 |
| — | **TOTAL** | **100%** | **R$ 60.000,00** |

> **Observação sobre custeio:** todos os custos de hospedagem, suporte, armazenamento, ambiente de teste, backup e operação assistida durante o piloto devem estar incluídos no valor total de R$ 60.000,00 (item 1.5 do TR: o valor máximo compreende "todas as despesas necessárias à execução da proposta"). Não há cobrança mensal autônoma durante o objeto de teste.

---

## H. Restrições e princípios (transversais)

| # | Princípio | Observação |
|---|-----------|------------|
| H1 | **A plataforma não realiza contratação** | Demandas públicas são **apenas informativas** — nenhum processo de compra acontece na ferramenta. Reforçar sempre. |
| H2 | **Neutralidade** | Sem ranqueamento pago, patrocínio ou destaque comercial. |
| H3 | **Privacidade do cidadão** | Cidadão não se cadastra; eventos de uso anônimos e agregados. |
| H4 | **Proteção de endereço** | Negócios residenciais/rurais podem ocultar endereço exato (área aproximada no mapa). |
| H5 | **Propriedade dos dados** | Base econômica é do Município; exportação aberta a qualquer tempo (reversibilidade). |

---

## Notas de verificação — CONFERIDAS contra o documento oficial

Os pontos abaixo foram conferidos diretamente no Termo de Referência assinado (Proc. 1.832/2026):

- [x] **Numeração dos itens** — os requisitos funcionais estão no item **4.1** (incisos I a XII); segurança em **4.1.1**; IA em **4.1.2**; desempenho em **4.1.3**; pilotos em **4.1.4**; abrangência/coleta pela Prefeitura em **4.1.5**; usuários em **4.1.6**. Confirmado.
- [x] **Percentuais dos 6 marcos** — item **10.3.2**: M-1 10%, M-2 10%, M-3 20%, M-4 10%, M-5 30%, M-6 20%. Confirmado (a proposta está correta).
- [x] **Metas de referência** — item 4.1.6: pelo menos **30% das empresas de cada porte** (MEI, ME, EPP e demais); **10 a 20 servidores**; gestores das áreas de desenvolvimento econômico, compras e planejamento. Confirmado.
- [x] **Nome oficial do desafio** — "Páginas Amarelas Inteligentes: conectando a oferta local às demandas públicas e privadas". Confirmado.
- [x] **Parâmetros de desempenho** (item 4.1.3): disponibilidade ≥ 95%; resposta < 5s; completude > 90%. Confirmado.
- [x] **Valor e prazo** — R$ 60.000,00 (item 1.5); execução de 6 a 12 meses (item 1.6). Confirmado.

### Achados adicionais do documento oficial (não estavam no meu resumo anterior)

- **Requisito de segurança mais extenso do que eu tinha (item 4.1.1):** o TR lista **10 medidas**, incluindo duas que vale citar na proposta e não estavam: *"documentação de incidentes e plano de resposta"* (inciso VIII) e *"mecanismos de prevenção contra acesso não autorizado"* (inciso VII). O restante (autenticação, perfis, logs, criptografia em trânsito, backup, segregação teste/produção, exportação aberta, reversibilidade) você já cobre.
- **IA — o inciso VI é forte a seu favor (item 4.1.2):** o TR exige explicitamente *"medidas para evitar discriminação, viés indevido, direcionamento de fornecedores ou restrição à competitividade"*. Sua neutralidade por concepção (sem ranqueamento pago) atende isso diretamente — vale enfatizar com essas palavras.
- **Volume esperado (item 4.1.7):** "centenas de empresas" cadastradas e "milhares de registros estruturados". Bom saber para o discurso de escala — sua arquitetura PostGIS aguenta, e a proposta pode mencionar.
- **Marcos têm subnumeração (M-1.1, M-2.3, M-3.4 etc.):** cada marco tem subitens identificados. Não é obrigatório espelhar no Plano de Trabalho agora, mas ao montar o cronograma executivo (pós-seleção) convém seguir essa numeração.
- **Marco 4 tem meta dura:** aprovação exige que *no mínimo 90% dos usuários indicados* tenham participado dos treinamentos. Relevante para o Plano de Trabalho, não para a proposta.
- **Existe uma Matriz de Riscos oficial de 15 páginas** para o Desafio 01 no processo. Se você quiser fortalecer o Plano de Trabalho (pós-seleção), vale ler — a Administração já mapeou os riscos que espera ver tratados.
