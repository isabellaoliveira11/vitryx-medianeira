# Prompt Claude Code — Cadastro pela Prefeitura + Tags de Demanda (localStorage)

> Cole no Claude Code, na pasta do `vitryx.html`. Duas entregas no mesmo trabalho. Tudo em `localStorage` — **não crie backend, banco, API ou autenticação de servidor.** É um protótipo demonstrativo.

---

Trabalhe no `vitryx.html`. Leia o arquivo antes de editar. Faça **por etapas** e deixe as correções de divergência para uma **varredura única no final**, para economizar tokens.

Regra geral: **tudo é simulado em `localStorage`**, como o resto do protótipo. Onde a lógica ideal pediria backend/banco/API, implemente o equivalente demonstrativo em memória/localStorage. Não construa backend.

## ENTREGA 1 — Cadastro de empresa pela Prefeitura

Contexto: o Termo de Referência (4.1.5) diz que a coleta de dados é da Prefeitura. Preciso demonstrar isso: o gestor cadastrando uma empresa na base econômica.

- **Etapa 1.1** — Na tela **Base Econômica** do gestor, adicione um botão **"+ Cadastrar Empresa"**, no mesmo estilo do botão de cadastrar demanda que já existe.
- **Etapa 1.2** — Ao clicar, abra um formulário com apenas: **nome, CNAE, porte, categoria/segmento, endereço e telefone (opcional)**. Sem catálogo, descrição pública, horários ou tags de vitrine (um registro importado ainda não tem vitrine). Reutilize o `modal-onboarding` em "modo Prefeitura" se ficar limpo; senão, um modal próprio enxuto.
- **Etapa 1.3** — Ao salvar, a empresa entra na base com: origem = "Base Importada"; `hasVitrine: false`; `validationStatus: "validado"`; sem catálogo, sem tags de vitrine, views/contatos zerados — igual aos importados que já existem no seed.
- **Etapa 1.4** — Após salvar: toast "Empresa cadastrada na base econômica municipal."; aparece na tabela com etiqueta "Sem vitrine"; registra na trilha de auditoria (ação "Cadastro pela Prefeitura"); indicadores do painel recalculam sozinhos.

## ENTREGA 2 — Corrigir tags de demanda pública (RF-051)

Contexto: hoje, quando o gestor cria uma demanda pública e digita palavras-chave/tags, essas tags **não são usadas de verdade no cruzamento com as empresas** — o match ignora as tags digitadas. É um bug conhecido. Quero que a demanda cruze com os negócios **usando as tags que o gestor digitou**.

- **Etapa 2.1** — Garanta que as tags digitadas no campo de tags da demanda (`dem-tags` / `dem-tags-container`) sejam **persistidas** no objeto da demanda ao salvar.
- **Etapa 2.2** — Ajuste a lógica de cruzamento (a que alimenta "Demandas com Oferta Local" e "Negócios Locais Aptos a Atender") para considerar **as tags da demanda** ao procurar empresas compatíveis — cruzando as tags/palavras-chave da demanda com nome, catálogo, tags, descrição e categoria dos negócios. Mantenha o que já funciona (cruzamento por categoria/CNAE) e **some** o cruzamento por tags.
- **Etapa 2.3** — Ao exibir os fornecedores relacionados a uma demanda, se já houver essa tela/lista, mostre-os; se não houver, ao menos garanta que o **contador** de "aptos a atender" reflita o novo cruzamento. Não crie tela nova complexa — só faça o número/lista existente ficar correto.
- **Regra de segurança do domínio:** o cruzamento é **informativo** — não deve sugerir contratação nem direcionar fornecedor. Se houver algum texto próximo, mantenha o aviso de que é apoio à pesquisa de mercado.

## ENTREGA 3 — Varredura final (só agora corrija divergências)

Confirme e corrija de uma vez:
- a empresa cadastrada pela Prefeitura NÃO vaza para a busca pública (`hasVitrine: false`);
- os contadores e gráficos do gestor batem com a nova contagem de empresas;
- a demanda com tags realmente muda o número de fornecedores aptos (teste: criar demanda com uma tag que existe em algum negócio e ver o match aparecer);
- nenhum id órfão, nenhuma div desbalanceada, nada quebrado no onboarding/reivindicação existente.

## Ao final

Relate em poucas linhas: (a) reusou o modal existente ou criou novo; (b) como o cruzamento por tags ficou e um exemplo testado (demanda X → negócios Y); (c) o que foi corrigido na varredura; (d) qualquer efeito colateral.

Comece lendo o `modal-onboarding`, a tela de Base Econômica, o modal de cadastro de demanda e a função de cruzamento demanda×empresa. Me mostre um plano curto antes de editar.
