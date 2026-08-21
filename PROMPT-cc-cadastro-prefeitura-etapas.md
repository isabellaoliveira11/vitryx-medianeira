# Prompt Claude Code — Cadastro de empresa pela Prefeitura (por etapas)

> Cole no Claude Code, na pasta do `vitryx.html`.

---

Trabalhe no `vitryx.html`. Leia o arquivo antes de editar. Faça este trabalho **por etapas**, e deixe qualquer correção de divergência/inconsistência para o **final**, em um único passo de varredura, para economizar tokens — não vá corrigindo coisas soltas no meio.

## Objetivo

Adicionar um fluxo em que **o gestor (Prefeitura) cadastra uma empresa manualmente** na base econômica. O Termo de Referência (item 4.1.5) diz que a coleta de dados é responsabilidade da Prefeitura — preciso demonstrar isso no vídeo. Reaproveite o modal de cadastro que já existe (`modal-onboarding`) sempre que possível, em vez de criar um novo.

**Não** chame nenhuma API externa. Tudo é simulado em `localStorage`, como o resto do protótipo.

## Etapas

**Etapa 1 — Botão de acesso.** Na tela **Base Econômica** do gestor, adicione um botão **"+ Cadastrar Empresa"**, no mesmo estilo visual do botão "+ Cadastrar Demanda" que já existe nessa área.

**Etapa 2 — Formulário.** Ao clicar, abra um formulário de cadastro contendo apenas os campos que a Prefeitura preencheria de uma base administrativa: **nome, CNAE, porte, categoria/segmento, endereço e telefone (opcional)**. Não peça catálogo, descrição pública, horários nem tags de vitrine — um registro importado pela Prefeitura ainda não tem vitrine. Se der para reutilizar o `modal-onboarding` em um "modo Prefeitura" que oculta os campos de vitrine, prefira isso; se ficar mais limpo um modal próprio enxuto, pode criar.

**Etapa 3 — Gravação do registro.** Ao salvar, a empresa entra na base com:
- origem = "Base Importada" (o mesmo rótulo dos importados atuais),
- `hasVitrine: false`,
- `validationStatus: "validado"` (é dado oficial da Prefeitura),
- sem catálogo, sem tags de vitrine, views/contatos zerados,
igual aos registros importados que já existem no seed.

**Etapa 4 — Feedback e coerência.** Após salvar: toast "Empresa cadastrada na base econômica municipal."; a empresa aparece na tabela da Base Econômica com a etiqueta "Sem vitrine"; o cadastro é registrado na trilha de auditoria (ação "Cadastro pela Prefeitura"); e os indicadores do painel recalculam sozinhos (total de empresas, com/sem vitrine).

**Etapa 5 — Varredura final (só agora corrija divergências).** Confirme e corrija de uma vez:
- a nova empresa NÃO vaza para a busca pública (por ter `hasVitrine: false`);
- os contadores e gráficos do gestor batem com a nova contagem;
- nenhum id órfão, nenhuma div desbalanceada, nada quebrado no fluxo existente de onboarding/reivindicação.

## Ao final

Relate em poucas linhas: (a) reusou o modal existente ou criou novo; (b) o que foi corrigido na varredura; (c) qualquer efeito colateral.

Comece lendo o `modal-onboarding` e a tela de Base Econômica.
