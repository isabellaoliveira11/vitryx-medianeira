# Documento de Requisitos para Implementação da VITRYX

## Desafio 01 — Páginas Amarelas Inteligentes

**Versão:** 1.0 — Documento consolidado para desenvolvimento da PoC/MVP e execução do piloto

**Fontes consideradas:** Estudo Técnico Preliminar, Termo de Referência e protótipo HTML VITRYX.

> **Importante:** este é um documento técnico de implementação baseado nos arquivos fornecidos. Ele não substitui a leitura do edital completo, do contrato, do Plano de Trabalho aprovado nem a revisão jurídica especializada antes da submissão ou da operação com dados pessoais.

## 1. Objetivo do produto

A VITRYX deverá ser uma solução pública de **inteligência econômica territorial** capaz de organizar, atualizar, pesquisar e analisar a oferta de produtos e serviços das empresas de Medianeira, conectando-a às demandas de cidadãos, empresas e Administração Pública.

A solução não deverá ser apresentada como um simples catálogo de nomes empresariais. O núcleo do produto é permitir a busca por **necessidade, item, produto, serviço, especialidade, palavra-chave e proximidade geográfica**, além de produzir informações úteis para desenvolvimento econômico, pesquisas de mercado e planejamento público [1] [2].

O piloto possui natureza experimental. Portanto, a VITRYX deve ser implementada para gerar evidências sobre três dimensões: **viabilidade técnica, viabilidade operacional e viabilidade econômica**. O produto final do piloto não é apenas o sistema, mas também o conjunto de métricas, relatórios, bases, documentos e aprendizados que permitirão decidir sobre eventual escala futura.

## 2. Escopo e limites

### 2.1 Incluído no escopo

| Área | Escopo obrigatório |
|---|---|
| Portal público | Consulta sem cadastro obrigatório, busca por necessidade, resultados, filtros, mapa e vitrine pública. |
| Base econômica | Cadastro estruturado de negócios urbanos e rurais, classificação, origem do dado, status e atualização. |
| Empreendedor | Cadastro, reivindicação de perfil, edição de vitrine, produtos/serviços, horários, tags e acompanhamento da validação. |
| Gestão municipal | Consulta da base, validação, lacunas, demandas públicas, indicadores, mapas, relatórios e histórico. |
| Busca | Pesquisa por nome, produto, serviço, especialidade, tags, descrição, CNAE, categoria e sinônimos administráveis. |
| Georreferenciamento | Coordenadas, consulta por proximidade e proteção de endereço quando necessário. |
| Dados e qualidade | Importação inicial, completude, atualização, validação, origem e trilha de alterações. |
| Segurança | Autenticação, perfis, logs, criptografia em trânsito, backup, restauração, separação de ambientes e resposta a incidentes. |
| Interoperabilidade | Exportação aberta em CSV, JSON e GeoJSON, com minimização e reversibilidade. |
| Piloto | Operação em ambiente real, com empresas, servidores, gestores, treinamento, monitoramento e avaliação final. |

### 2.2 Fora do escopo ou condicionado

A VITRYX **não deverá realizar contratações públicas, escolher automaticamente o vencedor de uma compra, substituir os sistemas oficiais de compras, criar ranqueamento pago ou direcionar fornecedor**. O sistema poderá apoiar a descoberta e a pesquisa de mercado, mas a contratação continuará sujeita aos procedimentos administrativos próprios.

Integrações com sistemas municipais podem ser planejadas como evolução futura. No primeiro ciclo, é aceitável entregar importação e exportação estruturadas, dicionário de dados, identificadores estáveis e arquitetura preparada para APIs, desde que o Plano de Trabalho defina quais integrações serão efetivamente testadas.

## 3. Linguagem normativa

Neste documento, **MUST** significa requisito obrigatório para o piloto; **SHOULD** significa requisito recomendado, que deve ser implementado salvo justificativa; **MAY** significa funcionalidade opcional ou experimental.

## 4. Perfis de usuário e permissões

| Perfil | Permissões mínimas |
|---|---|
| Cidadão/visitante | Pesquisar, filtrar, visualizar vitrines públicas, consultar mapa e iniciar contato. Não precisa criar conta. |
| Empreendedor | Criar ou reivindicar negócio, editar dados próprios, cadastrar produtos/serviços, anexar documentação, acompanhar pendências e consultar métricas da própria vitrine. |
| Operador municipal | Consultar base, revisar cadastros, validar, rejeitar, solicitar ajustes, corrigir dados administrativos e registrar justificativas. |
| Analista municipal | Consultar indicadores, lacunas, demandas, mapas, relatórios e cruzamentos de oferta, sem necessariamente alterar cadastros. |
| Gestor municipal | Acessar visões estratégicas, aprovar indicadores, cadastrar demandas e acompanhar resultados do piloto. |
| Administrador do sistema | Gerenciar usuários, perfis, taxonomias, configurações, integrações, backups e parâmetros. |
| Auditor | Consultar logs, eventos e relatórios de conformidade sem alterar registros. |

O sistema MUST aplicar controle de acesso no servidor, por perfil e por recurso. A troca visual de persona do protótipo não pode ser usada como mecanismo de autorização em produção.

## 5. Requisitos funcionais

### 5.1 Cadastro e base econômica

| ID | Requisito | Prioridade | Critério de aceite |
|---|---|---:|---|
| RF-001 | O sistema MUST manter cadastro estruturado de empresas locais, profissionais e produtores rurais. | P0 | Um registro deve poder ser criado, editado, validado, publicado, despublicado e auditado. |
| RF-002 | Cada negócio MUST possuir nome, nome fantasia quando aplicável, categoria, segmento, porte, CNAE, tags, descrição, produtos/serviços, origem, status e data de atualização. | P0 | O dicionário de dados deve listar tipo, obrigatoriedade e regra de validação de cada campo. |
| RF-003 | O sistema MUST registrar a origem de cada informação: cadastro do empreendedor, importação municipal, fonte pública ou sincronização. | P0 | Cada registro exibido no painel deve permitir identificar sua origem e data de atualização. |
| RF-004 | O sistema MUST permitir empresas com e sem vitrine pública. | P0 | A Prefeitura pode manter a empresa na base econômica sem publicar dados pessoais ou sem vitrine reivindicada. |
| RF-005 | O sistema MUST armazenar centenas de empresas e milhares de registros estruturados sem degradação significativa. | P0 | Teste de carga deve simular o volume do piloto e registrar tempo de resposta e erros. |
| RF-006 | O sistema SHOULD permitir campos de contato, horário, endereço comercial, área de atendimento, modalidade urbana/rural e tipo de atendimento. | P1 | O registro deve permitir distinguir endereço público, endereço aproximado e localização protegida. |
| RF-007 | O sistema MUST permitir atualização periódica e identificar registros desatualizados. | P0 | Um relatório deve listar registros sem atualização dentro do período definido no Plano de Trabalho. |

### 5.2 Classificação e taxonomia

| ID | Requisito | Prioridade | Critério de aceite |
|---|---|---:|---|
| RF-010 | O sistema MUST classificar por porte, CNAE, segmento, categoria, tags, palavras-chave, localização e tipo de produto/serviço. | P0 | Um gestor deve conseguir filtrar e agrupar a base por cada dimensão. |
| RF-011 | A taxonomia SHOULD ser administrável pelo Município. | P1 | Um administrador autorizado deve criar, editar, desativar e versionar categorias e tags. |
| RF-012 | O sistema MUST permitir sinônimos e variações linguísticas. | P0 | “Faxina”, “diarista” e “limpeza”, por exemplo, devem poder ser relacionados sem duplicar empresas. |
| RF-013 | O sistema SHOULD normalizar acentos, plurais, caixa, abreviações e erros comuns. | P1 | Uma suíte de testes deve cobrir consultas reais coletadas no piloto. |

### 5.3 Busca inteligente e resultados

| ID | Requisito | Prioridade | Critério de aceite |
|---|---|---:|---|
| RF-020 | O cidadão e o gestor MUST pesquisar por necessidade, produto, serviço, especialidade, tag, descrição e palavra-chave, não apenas por nome de empresa. | P0 | A consulta “conserto de cadeira” deve retornar um negócio pelo item de catálogo, tag ou descrição correspondente. |
| RF-021 | O mecanismo MUST indexar a descrição comercial. | P0 | Uma empresa cujo serviço aparece somente na descrição deve ser encontrada pela consulta correspondente. |
| RF-022 | O mecanismo MUST ordenar resultados com critérios documentados. | P0 | A documentação deve explicar pesos e desempates para nome, catálogo, descrição, tags, categoria e proximidade. |
| RF-023 | Cada resultado SHOULD mostrar uma explicação mínima do motivo da correspondência. | P1 | O resultado pode mostrar “correspondência no catálogo”, “tag relacionada” ou “descrição”. |
| RF-024 | O sistema MUST oferecer filtros avançados por status, categoria, porte, tipo, zona, distância, validação, vitrine e horário. | P0 | A aplicação de filtros deve atualizar lista, contagem e mapa de forma consistente. |
| RF-025 | O sistema MUST registrar buscas anonimizadas, resultados, abertura de vitrine e contato sem identificar desnecessariamente o cidadão. | P0 | O painel deve apresentar eventos agregados por período, termo e resultado. |
| RF-026 | Quando não houver resultado, o sistema MUST registrar a lacuna de oferta e permitir classificação pelo gestor. | P0 | Uma consulta sem resultado deve aparecer em uma fila de lacunas com termo, quantidade, período e status. |

### 5.4 Vitrine pública e contato

| ID | Requisito | Prioridade | Critério de aceite |
|---|---|---:|---|
| RF-030 | A vitrine MUST exibir somente dados aprovados e destinados ao público. | P0 | Dados pendentes ou documentos privados não podem aparecer no portal público. |
| RF-031 | A vitrine SHOULD exibir descrição, categoria, catálogo, horários, situação de funcionamento, validação, área de atendimento e origem da informação. | P1 | O visitante deve conseguir avaliar se o negócio atende à necessidade sem acessar o painel privado. |
| RF-032 | O sistema MUST proteger endereço de residência, produtor rural ou autônomo quando configurado. | P0 | O público vê apenas área aproximada; o endereço exato fica restrito a usuários autorizados. |
| RF-033 | WhatsApp, telefone e rota MUST abrir ações reais no piloto ou ser rotulados claramente como simulação na demonstração. | P0 | O teste deve confirmar `https`, `tel:` ou rota válida, conforme o canal configurado. |
| RF-034 | O sistema SHOULD registrar visualização de vitrine, intenção de contato e compartilhamento de forma agregada. | P1 | O empreendedor e o gestor devem ver métricas sem expor a identidade do cidadão. |

### 5.5 Cadastro, reivindicação e validação do empreendedor

| ID | Requisito | Prioridade | Critério de aceite |
|---|---|---:|---|
| RF-040 | O empreendedor MUST criar ou reivindicar um cadastro existente. | P0 | O fluxo deve impedir que uma pessoa reivindique negócio sem passar pelo processo de verificação. |
| RF-041 | O sistema MUST permitir edição da vitrine, produtos, serviços, tags, horários e descrição. | P0 | Alterações devem gerar versão pendente quando afetarem informação sensível ou pública. |
| RF-042 | O sistema MUST possuir estados de validação: pendente, aprovado, ajuste solicitado, rejeitado e despublicado. | P0 | Cada transição deve exigir usuário, data e justificativa quando aplicável. |
| RF-043 | O empreendedor SHOULD acompanhar o status da análise e o motivo de pendência ou rejeição. | P1 | O painel deve exibir mensagens acionáveis e prazo ou próxima etapa quando definido. |
| RF-044 | O sistema MUST suportar envio seguro de comprovantes quando exigidos. | P0 | O arquivo deve ser armazenado privadamente, com limite de tamanho/formato, acesso auditado e política de retenção. |
| RF-045 | CPF/CNPJ MUST ser validado conforme regra adequada ao documento e não apenas pelo tamanho do texto. | P0 | O cadastro deve rejeitar formato inválido e registrar o resultado da validação. |

### 5.6 Demandas públicas e oportunidades

| ID | Requisito | Prioridade | Critério de aceite |
|---|---|---:|---|
| RF-050 | O gestor MUST criar demandas públicas com título, secretaria, categoria, tags, palavras-chave, CNAE, descrição, prazo e status. | P0 | Uma demanda salva deve manter todos os campos e aparecer no painel. |
| RF-051 | As tags digitadas pelo gestor MUST ser persistidas e usadas no cruzamento. | P0 | Criar demanda com tags novas deve alterar os resultados relacionados; este é um bug atual a corrigir. |
| RF-052 | O sistema MUST cruzar demanda pública com empresas por categoria, CNAE, tags, descrição, catálogo e localização. | P0 | O resultado deve indicar os critérios de correspondência e permitir revisão humana. |
| RF-053 | O sistema MUST permitir estados de demanda: rascunho, em análise, planejamento, publicada internamente, atendida, encerrada e arquivada. | P1 | A alteração de estado deve ser auditável e restrita a perfis autorizados. |
| RF-054 | O sistema MUST deixar claro que o cruzamento não realiza contratação nem direciona fornecedor. | P0 | A interface e o manual devem conter aviso de apoio à prospecção/pesquisa de mercado. |
| RF-055 | O sistema SHOULD permitir exportar lista de fornecedores relacionados para análise administrativa. | P1 | A exportação deve preservar critérios, data e usuário responsável. |

### 5.7 Painel gerencial

| ID | Requisito | Prioridade | Critério de aceite |
|---|---|---:|---|
| RF-060 | O gestor MUST consultar base total, vitrines, validações, lacunas, origem, segmentos, portes e atualização. | P0 | Todos os cards devem ser calculados a partir do banco e possuir período/fonte. |
| RF-061 | O painel MUST apresentar indicadores econômicos e de participação de empresas locais nas compras públicas. | P0 | A proposta deve definir fonte, fórmula e limites do indicador; não usar números sem origem. |
| RF-062 | O painel MUST permitir análise por segmento, porte, CNAE, localização, origem e status. | P0 | Filtros aplicados devem refletir em cards, gráficos, tabela e mapa. |
| RF-063 | O painel MUST apresentar lacunas de oferta e demandas públicas relacionadas. | P0 | O gestor deve conseguir sair de uma lacuna para uma ação de análise ou cadastro de demanda. |
| RF-064 | O painel SHOULD apresentar qualidade cadastral, completude, georreferenciamento, atualização e validação. | P1 | A qualidade deve ser calculada por fórmula documentada. |
| RF-065 | O painel MUST apresentar histórico de eventos relevantes. | P0 | O auditor deve localizar quem fez o quê, quando, em qual registro e com qual resultado. |

### 5.8 Importação, atualização e integração

| ID | Requisito | Prioridade | Critério de aceite |
|---|---|---:|---|
| RF-070 | O sistema MUST importar base municipal em formato estruturado. | P0 | Um arquivo de teste deve ser validado, pré-visualizado, importado e gerar relatório de erros. |
| RF-071 | O sistema SHOULD suportar atualização incremental sem duplicação. | P1 | Identificador estável e regra de reconciliação devem ser documentados. |
| RF-072 | O sistema MUST sugerir fontes de dados adequadas ao contexto municipal. | P0 | A proposta deve listar fontes, campos, periodicidade, limites de uso e responsável pela disponibilização. |
| RF-073 | A arquitetura MUST permitir integração futura com sistemas de compras, desenvolvimento econômico, cadastro mobiliário e gestão empresarial. | P0 | Deve existir API ou especificação de integração, dicionário de dados e identificadores estáveis. |
| RF-074 | A Prefeitura será responsável pela coleta junto às empresas, enquanto a solução MUST prover armazenamento, tratamento, organização e análise. | P0 | O Plano de Trabalho deve separar claramente responsabilidade da Prefeitura e da contratada. |

### 5.9 Relatórios e exportação

| ID | Requisito | Prioridade | Critério de aceite |
|---|---|---:|---|
| RF-080 | O sistema MUST gerar relatórios gerenciais automatizados. | P0 | Um relatório deve ser gerado a partir de filtros e conter período, fonte, metodologia e data de geração. |
| RF-081 | O sistema MUST exportar CSV e JSON abertos e estruturados. | P0 | Os arquivos devem ser baixáveis, reimportáveis e documentados. |
| RF-082 | O sistema SHOULD exportar GeoJSON para dados georreferenciados. | P1 | O arquivo deve conter coordenadas válidas e respeitar localização protegida. |
| RF-083 | O sistema SHOULD gerar relatório executivo em PDF ou formato equivalente. | P1 | O relatório deve conter indicadores, limitações, metodologia, resultados e evidências. |
| RF-084 | A exportação MUST aplicar minimização e registrar o evento. | P0 | Documentos pessoais não podem sair na exportação; cada saída registra usuário, formato, filtros e quantidade. |
| RF-085 | A solução MUST ser reversível ao final do contrato. | P0 | O Município deve receber base, dicionário, arquivos, relatórios, documentação e instruções para restauração/uso. |

## 6. Requisitos de segurança e proteção de dados

| ID | Requisito | Prioridade | Critério de aceite |
|---|---|---:|---|
| RS-001 | Autenticação MUST ser real para perfis privados. | P0 | Login, recuperação, expiração, revogação e teste de permissão devem existir. |
| RS-002 | Controle de acesso MUST ser baseado em papéis e menor privilégio. | P0 | Testes devem demonstrar que cidadão, empreendedor, operador, gestor e auditor veem apenas o permitido. |
| RS-003 | A aplicação MUST usar criptografia em trânsito. | P0 | Ambiente publicado deve utilizar HTTPS/TLS válido. |
| RS-004 | O sistema MUST registrar logs de acesso, consulta, criação, alteração, exportação, exclusão, login e falha de autorização. | P0 | Logs devem ser pesquisáveis, protegidos contra alteração indevida e possuir retenção definida. |
| RS-005 | O sistema MUST ter backup e restauração testados. | P0 | Deve existir relatório de teste de restauração com data, escopo e resultado. |
| RS-006 | Ambientes de teste e produção MUST ser segregados quando aplicável. | P0 | Dados de produção não podem ser usados livremente em desenvolvimento. |
| RS-007 | O sistema MUST possuir mecanismos contra acesso não autorizado. | P0 | Implementar sessões seguras, limites de tentativa, validação de entrada, proteção contra injeção e gestão de segredos. |
| RS-008 | A equipe MUST documentar incidentes e plano de resposta. | P0 | O documento deve informar detecção, contenção, comunicação, recuperação e pós-incidente. |
| RS-009 | Documentos de validação MUST ficar em armazenamento privado. | P0 | O arquivo não pode ser acessado apenas por conhecer uma URL pública. |
| RS-010 | O sistema SHOULD possuir monitoramento de disponibilidade, erros e desempenho. | P1 | Relatório mensal deve demonstrar disponibilidade e principais incidentes. |

### 6.1 Requisitos de LGPD

A implementação deve manter um inventário dos dados tratados e limitar cada campo à finalidade necessária. CPF/CNPJ, comprovantes, e-mails e telefone não devem ser exibidos no portal público sem justificativa. Endereços residenciais, rurais ou de autônomos devem poder ser aproximados ou ocultados.

O produto deve definir aviso de privacidade, finalidade, base de tratamento, período de retenção, controle de acesso, processo de correção e exclusão, resposta a solicitações e regras de anonimização dos dados de uso. O cidadão não deve precisar criar conta para pesquisar, e os eventos de uso devem ser agregados/anônimos sempre que possível.

O documento deve ser revisado por responsável competente antes do tratamento real de dados. A interface atual possui consentimento visual e proteção aproximada, mas isso não substitui governança, segurança, retenção e gestão de direitos.

## 7. Requisitos para uso de inteligência artificial ou ranqueamento

A implementação recomendada para a primeira versão é uma **busca inteligente determinística e explicável**, com normalização, sinônimos, catálogo, descrição, tags, categoria, CNAE e proximidade. Isso reduz riscos e é suficiente para demonstrar o núcleo do desafio.

Se a VITRYX utilizar IA, embeddings, recomendação automática ou classificação de fornecedores, MUST documentar:

| Controle | Implementação necessária |
|---|---|
| Finalidade | Explicar qual decisão ou consulta a IA apoia. |
| Critérios | Descrever campos, pesos, modelo, limiares e desempates. |
| Fontes | Registrar origem, data e versão dos dados usados. |
| Revisão humana | Permitir ao gestor revisar, corrigir e contestar resultados. |
| Logs | Guardar consulta, recomendação, versão do modelo e resultado. |
| Viés/competitividade | Evitar direcionamento, exclusão indevida e ranqueamento pago. |
| Explicabilidade | Mostrar ao gestor por que uma empresa apareceu. |

A Vitória, no estado atual, deve ser descrita como **assistente de consulta da base municipal** ou chatbot baseado em regras. Não é recomendável afirmar que existe IA avançada validada se o sistema ainda não tiver modelo, fontes, logs e avaliação.

## 8. Requisitos de desempenho e qualidade

| Indicador obrigatório ou recomendado | Meta/critério |
|---|---|
| Disponibilidade | Mínimo de 95% durante o período medido. |
| Consulta gerencial | Tempo médio inferior a 5 segundos. |
| Escala do piloto | Centenas de empresas e milhares de registros estruturados. |
| Completude | Taxa superior a 90%, com fórmula e campos considerados documentados. |
| Atualização | Processo contínuo e relatório de registros desatualizados. |
| Relatórios | Geração automatizada e rastreável. |
| Auditoria | 100% das operações sensíveis registradas no piloto. |
| Exportação | Arquivos abertos, reimportáveis e testados. |
| Busca | Suíte de consultas reais com resultado esperado definido. |
| Adoção | Pelo menos 30% das empresas de cada porte e 10–20 servidores participantes. |

Os números de 95%, 5 segundos, 90%, 30% e 10–20 servidores vêm do ETP/Termo de Referência. Outras metas, como precisão da busca, satisfação e redução de tempo, devem ser propostas no Plano de Trabalho como indicadores experimentais, sempre com baseline T0 e método de coleta [1].

## 9. Modelo de dados mínimo

| Entidade | Campos principais |
|---|---|
| Business | id, razão/nome, nome fantasia, porte, CNAE, segmento, tipo, status, origem, data de atualização, responsável. |
| Offer | id, business_id, tipo, nome, descrição, categoria, tags, preço opcional, disponibilidade. |
| Location | business_id, endereço, bairro, cidade, latitude, longitude, precisão, proteção, área de atendimento. |
| User | id, perfil, nome, e-mail, status, instituição, último acesso. |
| Claim | business_id, user_id, evidências, estado, justificativa, datas. |
| Validation | business_id, revisor, estado, motivo, data, versão aprovada. |
| Demand | id, secretaria, título, descrição, categoria, CNAE, tags, prazo, status, responsável. |
| Match | demand_id, business_id, critérios, score, revisão humana, data. |
| Source | tipo, nome, arquivo/API, data de coleta, periodicidade, licença, responsável. |
| AuditEvent | usuário, ação, recurso, id, antes, depois, data, IP/sessão, resultado. |
| MetricEvent | sessão anônima, evento, termo, resultado, data, contexto mínimo. |
| ExportJob | usuário, formato, filtros, quantidade, data, arquivo, expiração, status. |
| Document | proprietário, tipo, localização privada, hash, tamanho, status, retenção, acessos. |

## 10. Estados essenciais

### 10.1 Negócio

`importado → pendente de qualificação → qualificado → pendente de validação → validado → publicado`.

Estados alternativos: `ajuste solicitado`, `rejeitado`, `despublicado`, `desatualizado` e `arquivado`.

Toda transição relevante deve ter usuário, data, motivo e versão. Um negócio importado pode existir na base econômica antes de possuir vitrine pública.

### 10.2 Demanda pública

`rascunho → em análise → planejamento → publicada internamente → atendida/encerrada → arquivada`.

A demanda não deve ser exibida como processo de contratação nem produzir qualquer direcionamento automático. Ela representa uma necessidade para análise, planejamento e pesquisa de mercado.

## 11. Arquitetura recomendada para a implementação

Os documentos oficiais não impõem linguagem, framework ou provedor. Portanto, a arquitetura abaixo é uma recomendação de implementação, não uma exigência jurídica.

| Camada | Recomendação |
|---|---|
| Frontend | Aplicação web responsiva com portal público, ambiente empreendedor e painel municipal. |
| API | Serviços para negócios, ofertas, busca, demandas, validações, métricas, relatórios e auditoria. |
| Banco | Banco relacional com migrações, integridade, histórico e índices de busca. |
| Busca | Busca lexical normalizada; índice semântico somente se houver documentação e revisão humana. |
| Geografia | Coordenadas com precisão registrada, geocodificação revisável e mapa público. |
| Arquivos | Armazenamento privado para documentos e exportações temporárias, com expiração. |
| Observabilidade | Métricas de disponibilidade, latência, erros, volume, logs e alertas. |
| Segurança | HTTPS/TLS, gestão de segredos, RBAC, sessões seguras, validação de entrada e backup. |
| Integração | Importação CSV no primeiro ciclo; API/contratos de dados para integrações futuras. |
| Ambientes | Desenvolvimento, homologação/teste e produção separados. |

## 12. Backlog priorizado de implementação

### P0 — obrigatório antes de chamar de PoC/MVP

| Item | Entrega |
|---|---|
| P0-01 | Migrar dados e persistência do `localStorage` para backend e banco centralizado. |
| P0-02 | Implementar autenticação e RBAC real. |
| P0-03 | Corrigir tags de demandas públicas e indexar descrição na busca. |
| P0-04 | Implementar cadastro, reivindicação, validação e estados auditáveis. |
| P0-05 | Implementar busca com nome, catálogo, descrição, tags, categoria, CNAE e sinônimos. |
| P0-06 | Implementar importação estruturada com validação, prévia e relatório de erros. |
| P0-07 | Implementar logs de acesso, consulta, alteração, exportação e exclusão. |
| P0-08 | Implementar CSV/JSON reais e preparar GeoJSON. |
| P0-09 | Implementar backup, restauração, monitoramento e segregação de ambientes. |
| P0-10 | Implementar proteção de documentos e localização aproximada. |
| P0-11 | Implementar métricas com fonte, fórmula, período e anonimização. |
| P0-12 | Realizar testes de segurança, carga, permissões, restauração e exportação. |

### P1 — necessário para piloto forte

| Item | Entrega |
|---|---|
| P1-01 | Painel de completude e atualização com alertas. |
| P1-02 | GeoJSON e relatório executivo automatizado. |
| P1-03 | Ações reais de WhatsApp, telefone e rota. |
| P1-04 | Taxonomia e sinônimos administráveis pela Prefeitura. |
| P1-05 | API documentada e identificadores estáveis para integrações futuras. |
| P1-06 | Suíte de testes de relevância da busca com termos reais. |
| P1-07 | Plano de incidentes, retenção, exclusão e reversibilidade. |
| P1-08 | Treinamento, manual operacional e suporte assistido. |

### P2 — evolução após validação inicial

| Item | Entrega |
|---|---|
| P2-01 | Busca semântica/embeddings com avaliação comparativa. |
| P2-02 | Integração direta com sistemas públicos, se autorizada e priorizada. |
| P2-03 | Painéis avançados de compras públicas e séries temporais. |
| P2-04 | Notificações, recomendações e automações com revisão humana. |
| P2-05 | Escala regional ou integração com entidades de apoio ao empreendedorismo. |

## 13. Marcos do piloto e critérios de aceite

O cronograma deve seguir os seis marcos oficiais. Os valores abaixo são a distribuição referencial do Termo de Referência e do ETP, totalizando R$ 60.000,00 [1] [2].

| Marco | Valor | Entregas mínimas | Critérios de aceite |
|---|---:|---|---|
| M-1 — Imersão e mapeamento | R$ 6.000 | Plano de Trabalho, usuários, processos, T0, riscos, dados, fontes e indicadores. | Plano aprovado, responsabilidades definidas, matriz de riscos e baseline registrados. |
| M-2 — Base empresarial | R$ 6.000 | Modelo de dados, importação inicial, taxonomia, fontes, atualização e georreferenciamento. | Carga de teste validada, relatório de qualidade e cobertura urbana/rural. |
| M-3 — Desenvolvimento/adaptação | R$ 12.000 | Backend, frontend funcional, autenticação, busca, mapa, vitrine, painel e validação. | URL de homologação, casos de teste aprovados, logs e versão funcional disponível. |
| M-4 — Capacitação | R$ 6.000 | Treinamento de 10–20 servidores, manuais, permissões e procedimentos operacionais. | Lista de presença, avaliação de compreensão, acessos individuais e suporte definido. |
| M-5 — Piloto real | R$ 18.000 | Operação em todo o Município, participação empresarial, uso por gestores, monitoramento e relatório intermediário. | Evidência de 30% das empresas de cada porte, usuários participantes, métricas e incidentes registrados. |
| M-6 — Consolidação | R$ 12.000 | Relatório final, bases, exportações, evidências, documentação, reversibilidade e conclusão de viabilidade. | Arquivos entregues, restauração testada, metas comparadas com T0 e decisão técnica documentada. |

## 14. Indicadores e método de medição

| ID | Indicador | Meta oficial/proposta | Método |
|---|---|---:|---|
| KPI-01 | Disponibilidade | ≥ 95% | Monitoramento externo mensal, excluindo janelas de manutenção documentadas conforme regra aprovada. |
| KPI-02 | Tempo médio de consulta gerencial | < 5 segundos | Teste automatizado e amostra de consultas reais. |
| KPI-03 | Completude dos registros | > 90% | Percentual de campos obrigatórios preenchidos e válidos. |
| KPI-04 | Participação empresarial | ≥ 30% de cada porte | Empresas participantes / universo municipal de cada porte, com definição da base. |
| KPI-05 | Usuários municipais | 10–20 servidores | Usuários com acesso, capacitação e participação registrada. |
| KPI-06 | Atualização | Meta definida no M-1 | Registros atualizados dentro do período de validade. |
| KPI-07 | Lacunas identificadas | Medir T0 e evolução | Buscas sem resultado normalizadas por período e categoria. |
| KPI-08 | Fornecedores relacionados a demandas | Meta definida no M-1 | Demandas com pelo menos um match revisado humanamente. |
| KPI-09 | Tempo de pesquisa de fornecedor | Redução versus T0 | Teste controlado com servidores antes e depois. |
| KPI-10 | Exportação | 100% dos formatos previstos testados | Download, abertura, reimportação e verificação dos campos. |
| KPI-11 | Auditoria | 100% das operações sensíveis | Amostragem de eventos e reconciliação com ações executadas. |
| KPI-12 | Satisfação/usabilidade | Meta definida no M-1 | Questionário de cidadãos, empreendedores e servidores, com método documentado. |

A VITRYX não deve apresentar os dados semeados do protótipo como indicadores do Município. Eles podem ser usados como dados demonstrativos, mas o piloto precisa coletar T0, definir metas e registrar resultados reais.

## 15. Evidências que devem ser produzidas

| Evidência | Fase | Finalidade |
|---|---|---|
| URL do ambiente de homologação | M-3 | Comprovar versão funcional. |
| URL do ambiente de piloto | M-5 | Comprovar operação real. |
| Plano de Trabalho | M-1 | Definir escopo, responsabilidades, metas e riscos. |
| Dicionário de dados | M-1/M-2 | Provar estrutura, origem e governança dos dados. |
| Relatório de importação | M-2 | Provar qualidade, erros e cobertura da carga. |
| Casos e resultados de teste | M-3 | Provar busca, permissões, segurança, desempenho e exportação. |
| Relatório de disponibilidade e latência | M-3/M-5 | Provar 95% e menos de 5 segundos. |
| Lista de usuários e capacitação | M-4 | Provar 10–20 servidores participantes. |
| Logs de auditoria | M-3/M-5/M-6 | Provar rastreabilidade. |
| Relatório intermediário | M-5 | Provar evolução e riscos do piloto. |
| Relatório final | M-6 | Provar viabilidade técnica, operacional e econômica. |
| Exportações e instrução de restauração | M-6 | Provar formato aberto e reversibilidade. |
| Evidência de equipe | Proposta/M-1 | Provar capacidade de execução. |
| Orçamento por marco | Proposta/M-1 | Provar viabilidade econômica. |

## 16. Riscos e mitigação

| Risco | Consequência | Mitigação |
|---|---|---|
| Baixa adesão das empresas | Base incompleta e baixa utilidade pública. | Mobilização da Prefeitura, cadastro assistido, comunicação por segmento e metas por porte. |
| Dados desatualizados | Resultados incorretos e perda de confiança. | Data de atualização, alertas, validação periódica e status de desatualização. |
| Atraso na entrega da base municipal | M-2 e M-3 comprometidos. | Formatos definidos em M-1, carga sintética de teste e responsabilidades documentadas. |
| Endereços sem coordenada | Mapa incompleto. | Geocodificação revisável, fila de pendência e precisão registrada. |
| Vazamento de documento ou endereço | Risco de privacidade e perda de confiança. | Armazenamento privado, RBAC, logs, minimização, localização aproximada e testes de acesso. |
| Baixa adoção por servidores | Painel sem impacto institucional. | Treinamento, usuários-piloto indicados, suporte e metas de uso. |
| Falsa promessa de IA | Questionamento de explicabilidade e viés. | Busca determinística explicável ou documentação completa de IA. |
| Exportação não reversível | Dependência técnica e risco contratual. | CSV/JSON/GeoJSON, dicionário, backups e teste de restauração. |
| Custo subestimado | Falha na entrega do piloto. | Orçamento por marco, premissas, custos operacionais e reserva técnica. |
| Falha de serviço externo | Mapa, geocodificação ou contato indisponível. | Cache, fallback, monitoramento e declaração de dependências. |

## 17. Definição de pronto para a apresentação

A VITRYX só deve ser apresentada como **PoC/MVP funcional** quando conseguir demonstrar, em um ambiente publicado, os seguintes fluxos: busca por necessidade; resultado por catálogo/descrição/tag; filtro e mapa; vitrine pública; cadastro/reivindicação; validação municipal; demanda pública com tags persistidas; cruzamento de fornecedores; painel de indicadores; exportação real; autenticação por perfil; logs; backup/restauração e proteção de localização/documentos.

Se ainda houver somente HTML e `localStorage`, a descrição correta é **protótipo demonstrativo com fluxos preparados para o piloto**. Essa distinção é importante para não transformar uma limitação técnica em perda de credibilidade perante a comissão.

## 18. Ordem prática de implementação

A sequência recomendada é:

**Primeiro**, corrigir o protótipo: tags das demandas, indexação da descrição, estado de validação, ações de contato e exportação. **Depois**, criar o backend mínimo com banco, autenticação, perfis, documentos privados e logs. **Em seguida**, implementar importação, qualidade, georreferenciamento, métricas e relatórios. **Na fase seguinte**, executar testes de permissão, segurança, carga, backup, restauração e busca. **Por fim**, publicar a versão de piloto, capacitar usuários, coletar T0, operar com empresas e produzir relatórios M-5/M-6.

## 19. Restrições contratuais e operacionais

A implementação deve considerar as condições do CPSI. Trata-se de um único piloto experimental, com uma única solução selecionada, prazo estimado de seis a doze meses e valor máximo de R$ 60.000,00, incluindo todas as despesas necessárias. O serviço é especial e não comum; não há regime de dedicação exclusiva de mão de obra. A contratada controla a distribuição, supervisão e alocação de seus recursos, sem subordinação direta à Administração [1] [2].

O Município não garante contratação futura em escala. Portanto, a solução deve ser executável dentro do piloto e não pode depender de uma receita posterior para concluir as entregas. A proposta deve explicar suporte, manutenção, continuidade, encerramento e reversibilidade mesmo se não houver contratação futura.

A titularidade da solução inovadora permanece com a contratada, enquanto o Município deve receber direitos de uso e aproveitamento dos dados, relatórios, indicadores e resultados do projeto. O contrato e o Plano de Trabalho devem transformar essa divisão em regras práticas de acesso, exportação, documentação, armazenamento e devolução dos dados [2].

## 20. Checklist de implementação e de submissão

| Item | Pergunta de controle | Evidência esperada |
|---|---|---|
| Escopo | O sistema cobre portal público, empreendedor e gestão municipal? | Fluxos publicados e casos de uso. |
| PoC/MVP | Há uma versão funcional fora do `localStorage`? | URL, arquitetura, credenciais de teste e relatório de execução. |
| Base | O modelo suporta centenas de empresas e milhares de registros? | Teste de carga e relatório de qualidade. |
| Busca | A busca encontra nome, catálogo, descrição, tags, categoria e CNAE? | Suíte de consultas e explicação do resultado. |
| Demandas | As tags digitadas são salvas e cruzadas com fornecedores? | Caso de teste de demanda com match verificável. |
| Mapa | Coordenadas e áreas protegidas funcionam? | Teste urbano/rural e regra de privacidade. |
| Validação | Há aprovação, rejeição, ajuste e publicação? | Estados, permissões, justificativas e histórico. |
| Segurança | Há autenticação, RBAC, logs, TLS, backup e restauração? | Relatórios de teste, política e evidências. |
| LGPD | Há minimização, retenção, proteção e anonimização? | Aviso de privacidade, inventário e controles revisados. |
| Exportação | CSV/JSON/GeoJSON geram arquivos reais e reimportáveis? | Arquivos, dicionário de dados e teste de reversibilidade. |
| Desempenho | Atinge 95% de disponibilidade e consulta média abaixo de 5 segundos? | Monitoramento e teste de desempenho. |
| Completude | A taxa de registros completos supera 90%? | Fórmula, relatório e plano de correção. |
| Piloto | Existe estratégia para 30% de cada porte e 10–20 servidores? | Plano de mobilização, treinamento e lista de participantes. |
| Métricas | Há T0, metas, fórmula, fonte, período e responsável? | Plano de medição e relatório intermediário/final. |
| Equipe | Os responsáveis por M-1 a M-6 têm experiência comprovada? | CVs, portfólio, atestados e dedicação. |
| Economia | O orçamento fecha em R$ 60.000 e cada marco possui entregável? | Planilha, premissas e cronograma financeiro. |
| Habilitação | A pessoa física/jurídica possui a documentação exigida? | Documentos jurídicos, fiscais, trabalhistas e cadastrais conforme o caso. |
| Proposta | O texto deixa claro o que é demo, PoC e piloto? | Proposta técnica e vídeo sem alegações não comprovadas. |

## 21. Referências

[1]: `pasted_content.txt` — Termo de Referência do Desafio 01, especialmente itens 1.1–1.6, 2.3, 3.1–3.3, 4.1–4.1.8, 5.1–5.5, 6, 7.4–7.10 e matriz de julgamento.
[2]: `pasted_content_3.txt` — Estudo Técnico Preliminar do Desafio 01, especialmente itens 3.1–3.4, 4.1–4.5, 5.1–5.2, 6.1–6.5, 7.1–7.3, 9.1–9.3 e 10.
[3]: `analise_vitryx.md` — Avaliação anterior do protótipo VITRYX e testes funcionais realizados.
[4]: `pasted_content_2.txt` — Código, interface, dados demonstrativos e lógica JavaScript do protótipo VITRYX.
