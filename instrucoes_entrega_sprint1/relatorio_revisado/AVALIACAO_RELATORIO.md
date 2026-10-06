# Avaliação do relatório preliminar do modelo ER

**Arquivos avaliados:**
- `instrucoes_entrega_sprint1/relatorio_preliminar.tex` (223 linhas) e o PDF compilado (8 páginas);
- `instrucoes_entrega_sprint1/er-camaar.pdf`.

**Referências usadas na avaliação:**
- o template obrigatório `TemplateRelatorioSprint1_1/ER-MyRottenPotatoes.tex`;
- o PDF da entrega;
- as issues #98 a #113;
- os arquivos `classes.json` e `class_members.json`.

**Arquivos da versão revisada, nesta pasta:**
- `relatorio_sprint1.tex` e `relatorio_sprint1.pdf`: 7 páginas, já compilados;
- `er-camaar-v2.drawio`: diagrama editável no draw.io;
- `er-camaar-v2.pdf`: o diagrama que entra no LaTeX.

## Resumo

A base do relatório é boa. O grupo achou as 11 entidades certas, usou bem os dados reais do SIGAA e pensou em pontos importantes, como as chaves naturais para a importação e a separação entre template e formulário.

Mesmo assim, ele **não pode ser entregue como está**, por três motivos:

1. **O PDF não tem o diagrama.** No lugar da figura aparece uma caixa com o texto "er-camaar.pdf" (ver item 1).
2. **A estrutura foge do template.** Há duas seções a mais e uma página em paisagem, e a entrega pede para seguir o template.
3. **O modelo não atende duas histórias** (#112 e #113), mas as Considerações Finais dizem que "cobre as histórias de usuário".

A versão revisada já corrige tudo isso e aplica três decisões que o grupo tomou:
- nomes em inglês, com a tradução entre parênteses, como no `Movie (Filme)` do template;
- as questões são copiadas para o formulário (resolve a #112);
- só os tipos de questão Radio e Texto, que são os do Figma.

---

## 1. Problema crítico: o PDF compilado não tem o diagrama

- O `relatorio_preliminar.pdf` foi gerado às **09:44:01**, e o `er-camaar.pdf` só foi salvo às **09:47:01**.
- Na hora da compilação a figura não existia. O LaTeX avisou "File `er-camaar.pdf' not found: using draft setting" e desenhou uma caixa com o nome do arquivo.
- Como a figura estava numa página em paisagem com `width=\linewidth`, essa caixa ficou com uns 698 pt de altura e passou da página.
- No PDF de 8 páginas:
  - **página 5:** só a seção "Decisões de Modelagem", com uns 70% em branco (o `landscape` força quebra de página);
  - **página 6:** só o título "Modelo Relacional UML" e a frase;
  - **página 7:** apenas a caixa "er-camaar.pdf".

**Lição para as próximas entregas:**
- Sempre recompilar **depois** de exportar a figura.
- Procurar "not found" e "Overfull" no `.log`.
- Abrir o PDF antes de enviar.

## 2. Conformidade com o template (obrigatório)

O template tem só quatro seções, nesta ordem:

**Introdução → Entidades Principais → Modelo Relacional UML → Considerações Finais**

Cada entidade é um `\subsection*{N. Nome (Tradução)}` com um `itemize` de atributos e uma frase "Relacionamento: …".

| Linhas do preliminar | Problema | O que fizemos na versão revisada |
|---|---|---|
| 173–179 | Seção "Decisões de Modelagem" não existe no template | Removida. As decisões foram para as Considerações Finais e para o texto das entidades |
| 194–217 | Seção "Mapeamento para Rails" não existe no template. Também não é o spike: o ponto extra é para o spike das **views**. Além disso, a tabela tinha erros (ver item 5) | Removida |
| 8, 181, 192 | Página em paisagem (`pdflscape`). O template põe a figura em retrato. Foi isso que causou o problema do item 1 | Figura em retrato com `width=\textwidth`. O diagrama foi redesenhado para caber em pé |
| 9–10 | `booktabs` e `array` só serviam à tabela Rails | Removidos |
| 38 | Parágrafo sobre "três blocos" de entidades, que não existe no template. Ele ainda contradiz a linha 184, que fala em quatro cores | Removido. O diagrama novo não usa cores |
| 40, 59, 68, … 161 | Títulos sem a tradução entre parênteses (o template usa `1. Movie (Filme)`) | `1. User (Usuário)`, `2. Department (Departamento)`, … |
| 57 | Parágrafo "Observação" solto (o template só tem itemize + Relacionamento) | O conteúdo foi para o atributo `password_digest` |
| 93 | Parágrafo antes do itemize de Participação | Foi para a frase de Relacionamento |
| 55, 66, 77, … 171 | As frases de Relacionamento começam com minúscula e algumas não falam de cardinalidade. A 171 descreve a Resposta, e não o ItemResposta | Todas reescritas no estilo do template ("Relacionamento: Um/Cada…"), com "nenhum ou vários" |
| 4, 13 | Pacotes e comandos fora do template | Ficaram só `fontenc[T1]` e `babel[brazilian]`. Sem o babel o PDF hifenizava em inglês ("reg-istradas", "nen-huma", "atual-ização"), e ele também já traduz "Figure" para "Figura", então o `\renewcommand{\figurename}` saiu |

Também acrescentamos um `\clearpage` antes de "Modelo Relacional UML", para que a seção e a figura fiquem juntas numa página, como no template. Ele não muda a estrutura.

## 3. Correção em relação às issues e aos dados (obrigatório)

### 3.1 Cobertura das 16 histórias

| Issue | No preliminar | Na versão revisada |
|---|---|---|
| #98 Importar SIGAA | Sim (chaves naturais), mas a matéria não tinha de onde tirar o departamento | Sim. O departamento da matéria vem do docente da turma |
| #99 Responder formulário | Sim, mas **nunca citada** | Sim (`Submission`/`Answer`), citada |
| #100 Cadastrar usuários | Sim (senha nula até definir) | Sim |
| #101 Relatório CSV | Sim, mas instável: editar o template mudava o sentido das respostas | Sim |
| #102 Criar template | Sim, mas o tipo "múltipla escolha" não cabia em um `opcao_id` por item | Sim, com tipos `radio`/`text` (os do Figma) |
| #103 Criar formulário | Sim | Sim, com cópia das questões |
| #104 Login | Sim, mas um docente não podia ser admin (`papel` exclusivo) | Sim, com `admin : Boolean` |
| #105 Definir senha | Parcial: token sem validade | Sim (`token_expires_at`, 48 h) |
| #106 Departamento (bônus) | Parcial: o admin não tinha departamento e a matéria não tinha origem | Sim |
| #107 Redefinir senha (bônus) | Parcial e **nunca citada** | Sim, citada |
| #108 Atualizar base | Sim | Sim |
| #109 Formulários pendentes | Sim, mas sem filtrar pelo público-alvo | Sim |
| #110 Ver formulários criados | Sim, mas citada como se fosse o CSV | Sim, citada em `Form` |
| #111 Ver templates | Sim | Sim |
| #112 Editar/excluir template | **Não atende** | **Sim**, pela cópia das questões |
| #113 Público-alvo (bônus) | **Não atende** | **Sim** (`target_audience`) |

### 3.2 Problemas de modelagem

- **#112 "sem afetar os formulários já criados" (linhas 113, 142, 166, 177).** As questões pertenciam só ao Template; o Formulário apontava para o template e o `ItemResposta` para a questão do template. Isso causava três problemas:
  - editar uma questão mudava todos os formulários já enviados e o significado das respostas;
  - excluir uma questão quebrava a FK das respostas, ou apagava as respostas, com cascata;
  - excluir o template quebrava `Formulario.template_id`, que era obrigatório.

  **Correção:**
  - no envio, as questões e as opções são **copiadas** para o formulário (`Question.form_id`);
  - as respostas apontam para essas cópias;
  - `Form.form_template_id` passa a ser opcional e fica nulo se o template for excluído;
  - `Form.title` guarda o nome do template.
- **#113 sem suporte.** Faltava o público-alvo do formulário. Foi criado `Form.target_audience` (`students`/`teachers`). As histórias #109 e #99 passam a filtrar por ele.
- **Departamento (linhas 52 e 74).**
  - A #106 é sobre o departamento do **administrador**, não só do docente.
  - O `classes.json` não traz departamento: só o docente do `class_members.json` tem. Por isso o departamento da matéria virou opcional e é preenchido na importação com o departamento do docente.
- **`papel` duplicado (linhas 48 e 99).** O papel docente/discente estava no usuário **e** na participação. Isso podia gerar divergência e impedia um docente de ser admin. Agora o usuário tem só `admin : Boolean`, e o papel na turma fica em `Participation.role`.
- **Múltipla escolha (linhas 121 e 167–171).** Um item por questão com um único `opcao_id` não representa múltipla escolha. Como o Figma só tem Radio e Texto, ficamos com esses dois tipos e com "no máximo um item por questão".
- **Token sem validade (linha 51).** Agora há `token_expires_at` (48 h), e o token é guardado criptografado (`token_digest`).
- **Anonimato (linha 178).** O texto dizia "se o grupo decidir". Decidimos: a resposta guarda o participante só para impedir respostas repetidas e para listar os pendentes, e o CSV não exporta quem respondeu.

### 3.3 Citações e afirmações

- **#107** nunca era citada. A linha 51 falava em redefinição sem citar a issue.
- **#99** nunca era citada.
- **#113** só aparecia no intervalo "#98 a #113".
- **#110** era tratada como CSV (linha 171). Na verdade ela é "visualizar os formulários criados".
- **#100** aparecia duas vezes na mesma frase (linha 57).
- **Linha 113:** "Suporta… #112" era falso no modelo antigo.
- **Linha 177:** "Alterar um template não deve alterar respostas" era um desejo que o modelo não garantia.
- **Linha 221:** três afirmações sem base:
  - "cobre as histórias de usuário" (#112 e #113 não eram atendidas);
  - "mantém o histórico… quando os templates são editados";
  - "importação periódica" (nenhuma issue fala nisso; a #108 é uma atualização manual).

## 4. Diagrama

**Problemas no `er-camaar.pdf`:**
- Faltavam duas ligações de FK: `Formulario.criado_por_id → Usuario` e `ItemResposta.opcao_id → Opcao`.
- FKs opcionais apareciam como "1" no lado do pai, em "lota" e "oferta"; o certo é 0..1.
- Não havia tipos nos atributos, notação pé-de-galinha nem legenda. O `example-er.png` do template tem os três (`id : Int`, `title : String`).
- Havia rótulos sobrepostos ("possui0..*", "oferece0..*", "lota"/"0..*", "recebe"/"0..*", "itens"/"1..*") e cruzamentos ambíguos ("avaliada em" × "participa").
- Com 1377 pt de largura, o texto ficava com uns 3–4 pt no PDF.
- As cores não batiam com o texto: o texto fala em 3 blocos, a legenda em 4 cores, e o Departamento aparecia como "acesso".

**O que tem o `er-camaar-v2`:**
- O mesmo estilo do `example-er.png`: caixas com cabeçalho, `nome : Tipo`, pés de galinha e uma legenda com "Um e somente um", "Zero ou um", "Um ou muitos", "Zero ou muitos", PK, FK e UQ.
- 17 FKs ↔ 17 linhas, conferidas por script, com as cardinalidades certas:
  - FKs opcionais com "zero ou um" no lado do pai;
  - `Form → Question` com "um ou muitos";
  - `Submission → Answer` com "um ou muitos".
- Layout em pé (3 colunas × 4 linhas), com linhas ortogonais e só 2 cruzamentos (marcados com "pulo"), sem rótulos sobrepostos.
- Na página, a 15,9 cm de largura, o texto dos atributos fica com uns 6,6 pt, um pouco maior que o do exemplo do template.

## 5. Sobre a tabela "Mapeamento para Rails"

Mesmo fora do relatório, vale registrar para a Sprint 2. Com nomes em português, o inflector padrão do Rails erra os plurais:
- `"questao".pluralize` dá `questaos`;
- `has_many :questoes` procura uma classe `Questo`;
- `:opcoes` vira `Opco` e `:itens_resposta` vira `ItensRespostum`.

Ou seja, as associações da tabela não funcionariam sem um `config/initializers/inflections.rb` cheio de regras. Esse foi mais um motivo para usar nomes em inglês. No modelo novo também evitamos duas palavras reservadas:
- `Class`, por isso `SchoolClass`;
- a coluna `type`, por isso `question_type`, já que o Rails usa `type` para herança (STI).

## 6. Antes → depois

| Preliminar | Revisado | O que mudou |
|---|---|---|
| Usuario (nome, email, matricula, senha_digest, papel, curso, formacao, token_senha, departamento_id) | User (name, email, registration, password_digest, **admin**, course, education_level, **token_digest**, **token_expires_at**, department_id) | `papel` → `admin`; token criptografado e com validade |
| Departamento (nome) | Department (name) | — |
| Materia (codigo, nome, departamento_id) | Subject (code, name, department_id) | FK opcional, com a origem explicada |
| Turma (materia_id, codigo_turma, semestre, horario) | SchoolClass (subject_id, code, semester, schedule) | — |
| Participacao (usuario_id, turma_id, papel) | Participation (user_id, school_class_id, role) | `role` = `student`/`teacher` (vem de `dicente`/`docente`) |
| Template (titulo, criado_por_id, created_at) | FormTemplate (title, creator_id, created_at) | pode ter 0 questões (rascunho) |
| Questao (template_id, enunciado, tipo, ordem, obrigatoria) | Question (form_template_id, **form_id**, statement, question_type, position, required) | pertence ao template **ou** ao formulário (cópia) |
| Opcao (questao_id, texto) | Option (question_id, text, **position**) | ordem das opções |
| Formulario (template_id, turma_id, criado_por_id, created_at) | Form (form_template_id *opcional*, school_class_id, creator_id, **title**, **target_audience**, created_at) | #112 e #113 |
| Resposta (formulario_id, usuario_id, submetida_em) | Submission (form_id, user_id, submitted_at) | — |
| ItemResposta (resposta_id, questao_id, opcao_id, valor_texto) | Answer (submission_id, question_id, option_id, text_value) | no máximo 1 item por questão |

## 7. O que mantivemos do preliminar

- As 11 entidades e a divisão entre estrutura acadêmica, templates e avaliação.
- A Participação como entidade associativa, que vem do `class_members.json`.
- As chaves naturais para importar e atualizar sem duplicar (#98, #108).
- Template e formulário separados, com um formulário por turma.
- A unicidade (formulário, participante) na resposta e a definição de "formulário pendente" (#109).
- O CSV gerado sob demanda, sem virar entidade.
- O uso de dados reais nos exemplos (CIC0097, 2021.2, 35T45, DEPTO CIÊNCIAS DA COMPUTAÇÃO).

## 8. Como fechar a entrega (Daniel + Leonardo)

1. Ler o `relatorio_sprint1.tex` e ajustar o que o grupo quiser no texto. A ordem dos autores é a mesma do preliminar.
2. **Diagrama** (só se for mexer):
   1. Abra o `er-camaar-v2.drawio` em https://app.diagrams.net (Arquivo → Abrir).
   2. Ajuste o que precisar.
   3. Exporte em Arquivo → Exportar como → PDF, marcando "Recortar" (Crop).
   4. Salve por cima de `er-camaar-v2.pdf`, nesta mesma pasta.
3. **Compilar:** rode `pdflatex relatorio_sprint1.tex` duas vezes, ou suba o `.tex` e o `er-camaar-v2.pdf` no Overleaf. No `.log` não pode aparecer "not found".
4. Abrir o PDF e conferir a página da figura.
5. Entregar o PDF no Aprender até o prazo da etapa 1.
