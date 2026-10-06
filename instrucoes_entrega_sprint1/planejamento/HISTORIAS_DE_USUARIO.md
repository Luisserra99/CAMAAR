# Histórias de Usuário — CAMAAR (Sprint 1)

**Grupo XX** · Engenharia de Software · CIC/UnB

As histórias abaixo são as issues **#98 a #113** do repositório [EngSwCIC/CAMAAR](https://github.com/EngSwCIC/CAMAAR/issues). Reescrevemos cada uma no padrão Connextra (*Como… / Quero… / Para que…*) e acrescentamos:

- as **regras de negócio (RN)** que o grupo combinou;
- os **critérios de aceitação**;
- os **pontos** usados no cálculo da velocity.

As RNs têm o mesmo número aqui, no `ESPECIFICACOES_BDD.md` e na Wiki. Se alguém mudar uma regra, precisa mudar nos três lugares.

★ = feature especificada de forma completa no BDD (as outras são enxutas: 1 cenário feliz e 1–2 tristes).

---

## Resumo do backlog

| Issue | História | Rótulo | Pontos | Responsável | Arquivo `.feature` |
|---|---|---|:-:|---|---|
| [#98](https://github.com/EngSwCIC/CAMAAR/issues/98) | Importar dados do SIGAA ★ | — | 5 | Weldo | `features/sigaa/importar_dados_sigaa.feature` |
| [#99](https://github.com/EngSwCIC/CAMAAR/issues/99) | Responder formulário ★ | MVP | 5 | Tarsila | `features/avaliacoes/responder_formulario.feature` |
| [#100](https://github.com/EngSwCIC/CAMAAR/issues/100) | Cadastrar usuários do sistema | — | 3 | Weldo | `features/sigaa/cadastro_usuarios.feature` |
| [#101](https://github.com/EngSwCIC/CAMAAR/issues/101) | Gerar relatório do administrador (CSV) | MVP | 3 | Tarsila | `features/avaliacoes/relatorio_csv.feature` |
| [#102](https://github.com/EngSwCIC/CAMAAR/issues/102) | Criar template de formulário ★ | MVP | 5 | Daniel | `features/templates/criar_template.feature` |
| [#103](https://github.com/EngSwCIC/CAMAAR/issues/103) | Criar formulário de avaliação ★ | MVP | 3 | Leonardo | `features/formularios/criar_formulario.feature` |
| [#104](https://github.com/EngSwCIC/CAMAAR/issues/104) | Sistema de login ★ | MVP | 3 | Luis | `features/autenticacao/login.feature` |
| [#105](https://github.com/EngSwCIC/CAMAAR/issues/105) | Sistema de definição de senha | — | 3 | Luis | `features/autenticacao/definicao_senha.feature` |
| [#106](https://github.com/EngSwCIC/CAMAAR/issues/106) | Gerenciamento por departamento | Bônus | 5 | Leonardo | cenários `@issue-106` em `criar_formulario.feature` e `visualizar_resultados.feature` |
| [#107](https://github.com/EngSwCIC/CAMAAR/issues/107) | Redefinição de senha | Bônus | 3 | Luis | `features/autenticacao/redefinicao_senha.feature` |
| [#108](https://github.com/EngSwCIC/CAMAAR/issues/108) | Atualizar base de dados com os dados do SIGAA | — | 3 | Weldo | `features/sigaa/atualizar_dados_sigaa.feature` |
| [#109](https://github.com/EngSwCIC/CAMAAR/issues/109) | Visualização de formulários para responder | MVP | 2 | Tarsila | `features/avaliacoes/formularios_pendentes.feature` |
| [#110](https://github.com/EngSwCIC/CAMAAR/issues/110) | Visualização de resultados dos formulários | — | 2 | Leonardo | `features/formularios/visualizar_resultados.feature` |
| [#111](https://github.com/EngSwCIC/CAMAAR/issues/111) | Visualização dos templates criados | MVP | 2 | Daniel | `features/templates/visualizar_templates.feature` |
| [#112](https://github.com/EngSwCIC/CAMAAR/issues/112) | Edição e deleção de templates | MVP | 3 | Daniel | `features/templates/editar_deletar_template.feature` |
| [#113](https://github.com/EngSwCIC/CAMAAR/issues/113) | Formulário para docentes ou discentes | Bônus | 2 | Leonardo | `features/formularios/formulario_publico_alvo.feature` |
| | **Total** | | **52** | | |

Pontos por rótulo:
- **MVP:** 26 pontos.
- **Sem rótulo:** 16 pontos.
- **Bônus:** 10 pontos.

Pontos por pessoa:
- **Leonardo:** 12.
- **Weldo:** 11.
- **Daniel:** 10.
- **Tarsila:** 10.
- **Luis:** 9.

### Como pontuamos

Usamos a escala de Fibonacci. O ponto mede o esforço relativo para **implementar** a história, com testes, nas Sprints 2 e 3, e não o esforço de escrever o BDD.

| Pontos | Significado | Exemplo |
|:-:|---|---|
| 1 | trivial | — |
| 2 | uma tela simples ou uma listagem | ver templates, ver formulários pendentes |
| 3 | um formulário com validações ou um fluxo curto | login, definir senha, enviar formulário |
| 5 | um fluxo com várias partes ou uma regra que afeta outras telas | importação do SIGAA, criar template com questões dinâmicas, responder formulário, regra de departamento |
| 8 | grande demais: deve ser quebrada antes de entrar na sprint | — |

### Como cadastrar as histórias no GitHub

1. No fork, crie **uma issue por história**, com o título `[#98] Importar dados do SIGAA`. Use sempre o número da issue do **upstream**, porque é ele que vai nas tags `@issue-98`, no PR e na Wiki.
2. No corpo, cole a seção da história (história, RNs e critérios) e o bloco Gherkin correspondente do `ESPECIFICACOES_BDD.md`.
3. Crie as labels:
   - `MVP`, `Bônus`;
   - `1 ponto`, `2 pontos`, `3 pontos`, `5 pontos`;
   - `sprint-1`.
4. Atribua a issue ao responsável.
5. Se quiserem acompanhar o andamento, criem um GitHub Project (quadro) com as colunas *A fazer / Em andamento / Em revisão / Pronto*.

---

## Tema: Dados do SIGAA (responsável: Weldo)

### #98 — Importar dados do SIGAA ★
**5 pontos** · sem rótulo · `features/sigaa/importar_dados_sigaa.feature`

**Como** administrador,
**quero** importar do SIGAA os dados de turmas, matérias e participantes que ainda não existem na base,
**para que** a base de dados do CAMAAR seja alimentada sem eu ter que cadastrar tudo à mão.

**Regras de negócio**
- **RN01:** Só administradores importam dados. O botão "Importar dados" fica na página "Gerenciamento".
- **RN02:** Os dados vêm de dois arquivos JSON no formato do SIGAA, iguais aos que estão no repositório:
  - `classes.json`: matérias e turmas;
  - `class_members.json`: discentes e docente de cada turma.
- **RN03:** Nada é duplicado. Cada registro é identificado assim:
  - matéria: pelo código (ex.: CIC0097);
  - turma: pela matéria + código da turma + semestre;
  - usuário: pela matrícula (discente) ou pelo usuário do SIGAA (docente).
- **RN04:** A importação é "tudo ou nada". Se um arquivo estiver mal formatado, faltar um campo obrigatório ou um participante for de uma turma que não está no `classes.json`, nada é gravado e o sistema mostra o motivo.
- **RN05:** O departamento da matéria é o departamento do docente da turma, porque o `classes.json` não traz departamento.

**Critérios de aceitação**
- [ ] Com a base vazia, importar os JSONs do repositório cria as 3 turmas de 2021.2. A turma CIC0097-TA fica com 44 discentes e 1 docente.
- [ ] Importar os mesmos arquivos de novo não cria nenhuma turma, matéria ou usuário repetido.
- [ ] Com um arquivo inválido, nenhuma turma é criada e aparece uma mensagem dizendo qual arquivo tem problema e qual é o problema.
- [ ] A matéria CIC0097 fica no "DEPTO CIÊNCIAS DA COMPUTAÇÃO".

### #100 — Cadastrar usuários do sistema
**3 pontos** · sem rótulo · `features/sigaa/cadastro_usuarios.feature`

**Como** administrador,
**quero** que os participantes novos sejam cadastrados quando eu importo os dados do SIGAA,
**para que** eles recebam o link para definir a senha e consigam acessar o CAMAAR.

> Comentário do mantenedor na issue: "o que é feito é a solicitação da definição da senha do usuário. O cadastro do aluno/professor como usuário só é realmente efetivado após a definição da senha." Por isso **não existe tela de "cadastre-se"**.

**Regras de negócio**
- **RN10:** O cadastro acontece durante a importação. Quem ainda não existe é criado **sem senha** e recebe um e-mail com o link para definir a senha.
- **RN11:** Quem já está cadastrado não recebe o e-mail de novo.
- **RN12:** O cadastro só é efetivado quando o usuário define a senha. Antes disso ele não consegue entrar no sistema.

**Critérios de aceitação**
- [ ] Na primeira importação, os 45 participantes da turma CIC0097-TA são criados sem senha e cada um recebe um e-mail com o link.
- [ ] Um participante que já estava cadastrado não recebe outro e-mail.
- [ ] Se a importação falhar (RN04), nenhum e-mail é enviado.

### #108 — Atualizar base de dados com os dados do SIGAA
**3 pontos** · sem rótulo · `features/sigaa/atualizar_dados_sigaa.feature`

**Como** administrador,
**quero** atualizar a base de dados que já existe com os dados atuais do SIGAA,
**para que** a base de dados do sistema fique correta.

**Regras de negócio**
- **RN36:** A atualização usa **o mesmo botão "Importar dados"**, como o monitor pediu.
  - O que mudou no SIGAA é atualizado nos registros que já existem, sem duplicar (RN03): nome, e-mail, horário e participantes novos.
  - Um arquivo com erro não altera nada (RN04).

**Critérios de aceitação**
- [ ] Se o horário de uma turma mudou no SIGAA, depois de clicar em "Importar dados" a turma aparece com o horário novo.
- [ ] Um discente novo na turma passa a fazer parte dela e recebe o e-mail de definição de senha (RN10).
- [ ] Com um arquivo inválido, os dados antigos continuam iguais.

---

## Tema: Autenticação (responsável: Luis)

### #104 — Sistema de login ★
**3 pontos** · MVP · `features/autenticacao/login.feature`

**Como** usuário do sistema,
**quero** entrar no CAMAAR com meu e-mail ou minha matrícula e a senha que eu cadastrei,
**para que** eu possa responder formulários ou gerenciar o sistema.

**Regras de negócio**
- **RN26:** O login aceita e-mail **ou** matrícula, mais a senha. Para docentes, a "matrícula" é o usuário do SIGAA.
- **RN27:** Os dois campos são obrigatórios. Se o login falhar, a mensagem é genérica ("E-mail/matrícula ou senha inválidos") e não diz qual dos dois está errado.
- **RN28:** A opção "Gerenciamento" só aparece no menu lateral para administradores, e as páginas de gerenciamento só abrem para eles. Esta é a regra da observação da issue.
- Vale também a **RN12**: quem ainda não definiu a senha não entra.

**Critérios de aceitação**
- [ ] Discente entra com e-mail e senha e cai na página "Avaliações".
- [ ] Docente entra com o usuário do SIGAA e a senha.
- [ ] O administrador vê "Gerenciamento" no menu lateral; discentes e docentes não veem.
- [ ] Um participante que tenta abrir a página "Gerenciamento" pelo endereço volta para "Avaliações" com o aviso "Acesso restrito a administradores".
- [ ] Senha errada, usuário inexistente ou campo vazio mantêm o usuário na página de login, com mensagem.
- [ ] Um usuário importado que ainda não definiu a senha recebe o aviso para usar o link do e-mail.

> Para não repetir cenário, a restrição de acesso à área de gerenciamento é testada **só aqui** (RN28) e vale para as RN01 e RN16.

### #105 — Sistema de definição de senha
**3 pontos** · sem rótulo · `features/autenticacao/definicao_senha.feature`

**Como** usuário importado do SIGAA,
**quero** definir a minha senha a partir do e-mail de solicitação de cadastro,
**para que** eu consiga acessar o sistema.

**Regras de negócio**
- **RN29:** O link enviado por e-mail vale por **48 horas** e só pode ser usado **uma vez**.
- **RN30:** A senha precisa ter **no mínimo 8 caracteres**, e a confirmação precisa ser igual à senha.
- **RN31:** Para definir a senha não é preciso estar logado nem digitar o e-mail, porque o link já identifica o usuário.

**Critérios de aceitação**
- [ ] Pelo link, preenchendo "Nova senha" e "Confirmar senha" iguais (≥ 8 caracteres), a senha é salva e o usuário consegue entrar.
- [ ] Senhas diferentes, senha com 7 caracteres ou campos vazios mostram erro e não salvam nada.
- [ ] Um link com mais de 48 horas, ou que já foi usado, mostra "Este link não é mais válido" e não deixa definir a senha.

### #107 — Redefinição de senha (bônus)
**3 pontos** · Bônus · `features/autenticacao/redefinicao_senha.feature`

**Como** usuário,
**quero** redefinir a minha senha a partir de um link recebido por e-mail depois de pedir a troca de senha,
**para que** eu recupere o meu acesso ao sistema.

**Regras de negócio**
- **RN34:** Na tela de login, "Esqueci minha senha" pede o e-mail e envia um link de redefinição. Valem as mesmas regras da RN29 e da RN30.
- **RN35:** A mensagem depois do pedido é a mesma para e-mail cadastrado ou não, para não revelar quem tem conta. Um e-mail em formato inválido é recusado.

**Critérios de aceitação**
- [ ] Pedir a troca com um e-mail cadastrado envia o link. Depois de salvar a nova senha, a senha antiga para de funcionar.
- [ ] Um e-mail não cadastrado mostra a mesma mensagem, mas nenhum e-mail é enviado.
- [ ] Um e-mail em formato inválido (ex.: `ana.souza`) mostra "Informe um e-mail válido".

---

## Tema: Templates (responsável: Daniel)

### #102 — Criar template de formulário ★
**5 pontos** · MVP · `features/templates/criar_template.feature`

**Como** administrador,
**quero** criar um template de formulário com as questões do formulário,
**para que** eu possa gerar formulários de avaliação do desempenho das turmas.

**Regras de negócio**
- **RN16:** Só administradores criam templates. A restrição de acesso é testada no login (RN28).
- **RN17:** O nome do template é obrigatório, tem no máximo **100 caracteres** e não pode se repetir entre os templates do mesmo administrador.
- **RN18:** Toda questão tem um **tipo** ("Radio" ou "Texto", os dois tipos do Figma) e um **texto** (o enunciado).
- **RN19:** Uma questão do tipo Radio precisa de **pelo menos 2 opções**. No campo "Opções" elas são digitadas separadas por ponto e vírgula.
- **RN20:** O template pode ser salvo **sem questões**, como rascunho, mas não pode ser usado para criar formulário enquanto estiver vazio (RN24).

**Critérios de aceitação**
- [ ] Em "Gerenciamento - Templates", clicando em "Novo template", dá para dar um nome, adicionar uma questão Radio (com opções) e uma questão Texto e clicar em "Criar". O template aparece na lista com 2 questões.
- [ ] Um nome vazio, com 101 caracteres ou repetido mostra erro e o template não é criado. Um nome com exatamente 100 caracteres é aceito.
- [ ] Uma questão sem texto, ou uma questão Radio com 0 ou 1 opção, mostra erro dizendo qual questão está errada.

### #111 — Visualização dos templates criados
**2 pontos** · MVP · `features/templates/visualizar_templates.feature`

**Como** administrador,
**quero** visualizar os templates criados,
**para que** eu possa editar ou deletar um template que eu criei.

**Regras de negócio**
- **RN41:** A página "Gerenciamento - Templates" mostra **só os templates criados pelo administrador logado**, cada um com as opções "Editar" e "Excluir".
- **RN42:** Se o administrador ainda não criou nenhum template, o sistema avisa e mostra a opção "Novo template".

**Critérios de aceitação**
- [ ] Clicando em "Editar Templates" no Gerenciamento, aparecem os meus templates e não aparecem os de outro administrador.
- [ ] Sem templates, aparece "Você ainda não criou nenhum template".

### #112 — Edição e deleção de templates
**3 pontos** · MVP · `features/templates/editar_deletar_template.feature`

**Como** administrador,
**quero** editar ou deletar um template que eu criei, sem afetar os formulários já criados,
**para que** eu mantenha os templates organizados.

**Regras de negócio**
- **RN43:** O administrador só edita ou exclui templates que ele criou. A edição segue as mesmas regras da criação (RN17 a RN19).
- **RN44:** Editar ou excluir um template **não altera os formulários já criados** com ele. As questões foram copiadas para o formulário no envio (ver o modelo ER).
- **RN45:** Depois de excluído, o template **some da lista** e não pode mais ser escolhido em "Enviar Formulários".

**Critérios de aceitação**
- [ ] Depois de editar o texto de uma questão, o template mostra o texto novo e o formulário já enviado continua com o texto antigo.
- [ ] Depois de excluir, o template não aparece mais na lista e o formulário já enviado continua disponível.
- [ ] Salvar a edição com o nome vazio mostra erro e não altera o template.
- [ ] Tentar editar um template de outro administrador é bloqueado.

---

## Tema: Formulários do administrador (responsável: Leonardo)

### #103 — Criar formulário de avaliação ★
**3 pontos** · MVP · `features/formularios/criar_formulario.feature`

**Como** administrador,
**quero** criar um formulário baseado em um template para as turmas que eu escolher,
**para que** eu avalie o desempenho das turmas no semestre atual.

**Regras de negócio**
- **RN21:** O administrador escolhe o template, marca as turmas e clica em "Enviar". Não há campo para digitar, como o monitor apontou.
- **RN22:** É criado **um formulário por turma marcada**, com uma **cópia das questões** do template.
- **RN23:** É obrigatório escolher um template e marcar **pelo menos uma turma**.
- **RN24:** Um template sem questões não pode ser usado.
- **RN25:** Só aparecem para envio as turmas do **semestre atual**, que é o semestre mais recente importado.

**Critérios de aceitação**
- [ ] Escolhendo o template e marcando 2 turmas, são criados 2 formulários com as mesmas questões do template, e a turma não marcada não recebe nada.
- [ ] Sem turma marcada, sem template escolhido ou com um template vazio, aparece uma mensagem e nenhum formulário é criado.
- [ ] Uma turma de 2021.1 não aparece na lista quando o semestre atual é 2021.2.

### #106 — Sistema de gerenciamento por departamento (bônus)
**5 pontos** · Bônus · cenários `@issue-106` em `criar_formulario.feature` e `visualizar_resultados.feature`

**Como** administrador,
**quero** gerenciar somente as turmas do departamento ao qual eu pertenço,
**para que** eu avalie o desempenho das turmas do meu departamento no semestre atual.

> O monitor comentou em 2024.1 que essa funcionalidade "não deveria ser completamente segregada das outras, ela é uma funcionalidade a qual deveria adicionar regras de negócio em outras features". Por isso ela não tem `.feature` próprio: os cenários dela ficam dentro das features de envio e de resultados.

**Regras de negócio**
- **RN32:** Um administrador que pertence a um departamento só vê e só envia formulários para turmas de matérias desse departamento.
- **RN33:** Esse administrador também só vê os resultados dos formulários das turmas do seu departamento.

**Critérios de aceitação**
- [ ] Um administrador do "DEPTO CIÊNCIAS DA COMPUTAÇÃO" não vê a turma MAT0025-TA (DEPTO MATEMÁTICA) em "Enviar Formulários".
- [ ] Ele também não consegue enviar formulário para essa turma pelo endereço.
- [ ] Ele não vê em "Resultados" os formulários dessa turma.

### #113 — Criação de formulário para docentes ou discentes (bônus)
**2 pontos** · Bônus · `features/formularios/formulario_publico_alvo.feature`

**Como** administrador,
**quero** escolher se o formulário é para os docentes ou para os discentes de uma turma,
**para que** eu avalie o desempenho de uma matéria pelos dois lados.

**Regras de negócio**
- **RN46:** No envio, o administrador escolhe o **público-alvo**: "Discentes" (padrão) ou "Docentes".
- **RN47:** Só os participantes da turma com o papel escolhido veem e respondem o formulário.

**Critérios de aceitação**
- [ ] Um formulário enviado para "Docentes" aparece para o docente da turma e não aparece para os discentes.
- [ ] Um discente que tenta abrir esse formulário pelo endereço é bloqueado.

### #110 — Visualização de resultados dos formulários
**2 pontos** · sem rótulo · `features/formularios/visualizar_resultados.feature`

**Como** administrador,
**quero** visualizar os formulários criados,
**para que** eu possa gerar um relatório a partir das respostas.

**Regras de negócio**
- **RN39:** A página "Gerenciamento - Resultados" lista os formulários criados, com template, turma, semestre e quantidade de respostas.
- **RN40:** Se nenhum formulário foi criado, o sistema avisa.
- Vale também a **RN33** (bônus #106).

**Critérios de aceitação**
- [ ] Clicando em "Resultados" no Gerenciamento, cada formulário aparece com a sua quantidade de respostas, inclusive os que têm 0.
- [ ] Sem formulários, aparece "Nenhum formulário foi criado ainda".

---

## Tema: Participante e relatório (responsável: Tarsila)

### #99 — Responder formulário ★
**5 pontos** · MVP · `features/avaliacoes/responder_formulario.feature`

**Como** participante de uma turma,
**quero** responder o questionário sobre a turma em que estou matriculado,
**para que** eu envie a minha avaliação da turma.

**Regras de negócio**
- **RN06:** Só responde quem participa da turma do formulário com o papel do público-alvo (RN47).
- **RN07:** Cada participante responde cada formulário **uma única vez**. Depois de enviada, a resposta não pode ser alterada.
- **RN08:** As questões obrigatórias precisam estar respondidas para o envio ser aceito.
- **RN09:** Respostas de texto têm **no máximo 1000 caracteres**.

**Critérios de aceitação**
- [ ] Respondendo a questão Radio e a de texto e clicando em "Enviar", aparece "Avaliação enviada com sucesso. Obrigado!" e o formulário sai da lista de pendentes.
- [ ] Uma questão que não é obrigatória pode ficar em branco.
- [ ] Sem a obrigatória, o envio é recusado e nada é gravado.
- [ ] Um texto com 1000 caracteres é aceito; com 1001, é recusado.
- [ ] Abrir de novo um formulário já respondido, ou um formulário de uma turma em que não estou matriculado, é bloqueado.

### #109 — Visualização de formulários para responder
**2 pontos** · MVP · `features/avaliacoes/formularios_pendentes.feature`

**Como** participante de uma turma,
**quero** visualizar os formulários não respondidos das turmas em que estou matriculado,
**para que** eu possa escolher qual vou responder.

**Regras de negócio**
- **RN37:** A página "Avaliações" mostra **só os formulários ainda não respondidos** das turmas do participante e do seu papel na turma, em cards com a matéria e o semestre (como no Figma).
- **RN38:** Se não houver nada pendente, o sistema avisa.

**Critérios de aceitação**
- [ ] Só aparecem os formulários pendentes das minhas turmas. Os já respondidos e os de turmas de que não participo não aparecem.
- [ ] Com tudo respondido, aparece "Você não tem avaliações pendentes".

### #101 — Gerar relatório do administrador (CSV)
**3 pontos** · MVP · `features/avaliacoes/relatorio_csv.feature`

**Como** administrador,
**quero** baixar um arquivo CSV com os resultados de um formulário,
**para que** eu avalie o desempenho das turmas.

**Regras de negócio**
- **RN13:** O CSV é gerado por formulário: uma linha por resposta enviada e uma coluna por questão, com separador `;`.
- **RN14:** O CSV **não identifica quem respondeu**; a avaliação é anônima.
- **RN15:** Um formulário sem respostas não gera CSV, e o sistema avisa.

**Critérios de aceitação**
- [ ] Em "Gerenciamento - Resultados", "Baixar CSV" de um formulário com 2 respostas gera um arquivo com o cabeçalho das questões e 2 linhas.
- [ ] O arquivo não tem nome nem matrícula de quem respondeu.
- [ ] Um formulário sem respostas mostra "Este formulário ainda não tem respostas" e não baixa nada.

---

## Índice das regras de negócio

| RN | Issue | Regra (resumo) |
|---|---|---|
| RN01 | #98 | só admin importa |
| RN02 | #98 | dados vêm de `classes.json` e `class_members.json` |
| RN03 | #98 | nada duplicado (chaves: código da matéria; matéria+turma+semestre; matrícula/usuário) |
| RN04 | #98 | importação "tudo ou nada", com motivo do erro |
| RN05 | #98 | departamento da matéria = departamento do docente |
| RN06 | #99 | só responde participante da turma com o papel do público-alvo |
| RN07 | #99 | responde uma vez só; não altera depois |
| RN08 | #99 | obrigatórias precisam ser respondidas |
| RN09 | #99 | texto até 1000 caracteres |
| RN10 | #100 | novo participante: criado sem senha + e-mail com link |
| RN11 | #100 | já cadastrado não recebe e-mail de novo |
| RN12 | #100 | só entra depois de definir a senha |
| RN13 | #101 | CSV: linha por resposta, coluna por questão, `;` |
| RN14 | #101 | CSV anônimo |
| RN15 | #101 | sem respostas não gera CSV |
| RN16 | #102 | só admin cria template |
| RN17 | #102 | nome obrigatório, até 100 caracteres, sem repetir (por admin) |
| RN18 | #102 | questão tem tipo (Radio/Texto) e texto |
| RN19 | #102 | Radio com pelo menos 2 opções |
| RN20 | #102 | template pode ficar sem questões (rascunho) |
| RN21 | #103 | admin escolhe template + turmas e clica em "Enviar" |
| RN22 | #103 | um formulário por turma, com cópia das questões |
| RN23 | #103 | template e ≥ 1 turma obrigatórios |
| RN24 | #103 | template vazio não pode ser usado |
| RN25 | #103 | só turmas do semestre atual |
| RN26 | #104 | login com e-mail ou matrícula + senha |
| RN27 | #104 | campos obrigatórios; erro genérico |
| RN28 | #104 | "Gerenciamento" só para admin (menu e páginas) |
| RN29 | #105 | link vale 48 h e uma vez |
| RN30 | #105 | senha ≥ 8 caracteres e confirmação igual |
| RN31 | #105 | não precisa estar logado nem digitar e-mail |
| RN32 | #106 | admin de departamento só envia para turmas do departamento |
| RN33 | #106 | admin de departamento só vê resultados do departamento |
| RN34 | #107 | "Esqueci minha senha" envia link (RN29, RN30) |
| RN35 | #107 | mesma mensagem para e-mail cadastrado ou não; formato inválido recusado |
| RN36 | #108 | atualização pelo mesmo botão, sem duplicar; erro não altera nada |
| RN37 | #109 | "Avaliações" mostra só pendentes das minhas turmas e do meu papel |
| RN38 | #109 | aviso quando não há pendentes |
| RN39 | #110 | "Resultados" lista formulários com quantidade de respostas |
| RN40 | #110 | aviso quando não há formulários |
| RN41 | #111 | lista só os templates do admin logado, com Editar/Excluir |
| RN42 | #111 | aviso quando o admin não tem templates |
| RN43 | #112 | só edita/exclui os próprios; mesmas validações da criação |
| RN44 | #112 | editar/excluir não altera formulários já criados |
| RN45 | #112 | template excluído some da lista e do envio |
| RN46 | #113 | público-alvo: Discentes (padrão) ou Docentes |
| RN47 | #113 | só quem tem o papel escolhido vê e responde |
