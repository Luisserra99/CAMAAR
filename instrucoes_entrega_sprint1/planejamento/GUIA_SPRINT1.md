# Guia da Sprint 1 — CAMAAR (Grupo XX)

Este guia junta tudo o que o grupo precisa fazer na Sprint 1: o que o professor pediu, quem faz o quê, o passo a passo no Git/GitHub e os erros que outros grupos já cometeram. Ele foi montado a partir de três fontes:
- o PDF da entrega;
- as issues #98–#113;
- os PRs e as Wikis dos grupos de 2024.1, 2025.2 e 2026.1 no EngSwCIC/CAMAAR, incluindo o feedback dos monitores.

Arquivos que acompanham este guia:

| Arquivo | Para quê |
|---|---|
| `HISTORIAS_DE_USUARIO.md` | as 16 histórias no padrão Connextra, com regras de negócio (RN01–RN47), critérios de aceitação e pontos |
| `ESPECIFICACOES_BDD.md` | os 15 arquivos `.feature` prontos, cada um com dono e caminho |
| `WIKI_SPRINT1.md` | rascunho da página da Wiki do fork |
| `entrega_sprint1.txt` | o `.txt` que vai para o Aprender |
| `../relatorio_revisado/` | o relatório ER revisado (`.tex` + `.pdf`), o diagrama (`.drawio` + `.pdf`) e a avaliação do relatório preliminar |

---

## 1. Resumo rápido

- **Etapa 1 (50%), prazo D1:**
  - entregar no Aprender o **PDF do modelo ER** seguindo o template LaTeX. A versão revisada já está pronta: falta o grupo revisar e entregar;
  - o fork já existe: https://github.com/Luisserra99/CAMAAR. Falta adicionar todo mundo como colaborador.
- **Etapa 2 (50%), prazo D2:**
  - cada um commita os **seus** `.feature` na **sua** branch;
  - juntamos tudo na `sprint-1` e abrimos **um** PR para o EngSwCIC/CAMAAR;
  - entregamos o `.txt` no Aprender e publicamos a **Wiki**.
- **Não implementamos nada nesta sprint.** Só especificação.

> **Prazos:** o PDF diz **19/05/2026** (etapa 1) e **26/05/2026** (etapa 2), mas essas datas parecem ser do semestre passado. **Confirmem no Aprender.** Neste guia, **D1** = prazo da etapa 1 e **D2** = prazo da etapa 2.

---

## 2. O que o professor pediu (checklist)

### Etapa 1

| # | Item | Onde entrega | Dono | Situação |
|---|---|---|---|---|
| 1.1 | Estudar as histórias das issues #98–#113 | — | todos | ler `HISTORIAS_DE_USUARIO.md` |
| 1.2 | Fork do CAMAAR com todos os membros | GitHub (Settings → Collaborators) | Luis | fork pronto; falta convidar os 4 |
| 1.3 | Relatório em PDF explicando o modelo ER, **seguindo o template LaTeX** | Aprender | Daniel (texto) + Leonardo (diagrama) | versão revisada pronta em `relatorio_revisado/` |
| 1.4 | Spike de como fazer as views em Rails a partir do Figma | não é entregue | Tarsila (+ todos leem) | seção 9 deste guia. O grupo decidiu **não** colocar no relatório |

### Etapa 2

| # | Item | Onde entrega | Dono | Situação |
|---|---|---|---|---|
| 2.1 | Cenários BDD das histórias com Cucumber (≥1 feliz e ≥1 triste por feature) | branch `sprint-1` do fork | cada um, os seus | prontos em `ESPECIFICACOES_BDD.md` |
| 2.2 | **Um** PR com os testes de aceitação para o EngSwCIC/CAMAAR | GitHub | Luis | depois dos merges internos |
| 2.3 | `.txt` com o link do repositório e os nomes e matrículas | Aprender | Luis | `entrega_sprint1.txt` (falta o nº do grupo e o link do PR) |
| 2.4 | Página da Wiki no fork com as informações da Sprint 1 | Wiki do fork | Weldo (conteúdo) + Luis (publica) | `WIKI_SPRINT1.md` |

---

## 3. Divisão de tarefas

Cada pessoa fica com **um tema** (3 issues, sendo uma delas completa ★) e **uma tarefa transversal**. A divisão por tema facilita a Sprint 2, porque quem especificou a feature implementa a mesma feature.

| Membro | Papel | Tema e issues | Arquivos `.feature` | Tarefa transversal | Pontos |
|---|---|---|---|---|:-:|
| **Luis** Eduardo Curi Serra (251033574) | Scrum Master | Autenticação: ★#104, #105, #107 | `autenticacao/login`, `definicao_senha`, `redefinicao_senha` | convidar colaboradores, criar branches, revisar PRs internos, abrir o PR final, publicar a Wiki, entregar o `.txt` | 9 |
| **Weldo** Gonçalves da Silva Junior (222014133) | Product Owner | SIGAA: ★#98, #100, #108 | `sigaa/importar_dados_sigaa`, `cadastro_usuarios`, `atualizar_dados_sigaa` | backlog no fork (issues, labels, pontos), dono das regras de negócio, conteúdo da Wiki | 11 |
| **Daniel** Dezan Baby (232046097) | Dev | Templates: ★#102, #111, #112 | `templates/criar_template`, `visualizar_templates`, `editar_deletar_template` | relatório final: revisar o `.tex`, compilar, entregar o PDF | 10 |
| **Leonardo** Tome Sampaio (222005448) | Dev | Formulários: ★#103 (+ #106), #113, #110 | `formularios/criar_formulario`, `formulario_publico_alvo`, `visualizar_resultados` | diagrama: revisar o `.drawio`, ajustar e exportar o PDF | 12 |
| **Tarsila** Marques de Oliveira Alves (242012029) | Dev | Participante: ★#99, #109, #101 | `avaliacoes/responder_formulario`, `formularios_pendentes`, `relatorio_csv` | revisão cruzada dos `.feature` (passos iguais, rótulos do Figma) e dona do spike | 10 |

- A divisão (inclusive SM e PO) é uma **sugestão**. Se o grupo trocar algo, atualizem esta tabela, as `HISTORIAS_DE_USUARIO.md` e a Wiki.
- Se quem fez o relatório preliminar não for o Daniel, essa pessoa assume a revisão do relatório e o Daniel fica com a tarefa dela.

**O que o SM e o PO fazem nesta sprint:**
- **Scrum Master (Luis):**
  - destrava o grupo e cobra os prazos internos da seção 4;
  - cuida do repositório: branches, PRs, `sprint-1` congelada depois do PR;
  - garante que cada um commitou o próprio trabalho.
- **Product Owner (Weldo):**
  - é o "dono" das histórias: mantém as RNs coerentes entre histórias, BDD e Wiki, e decide as dúvidas de regra de negócio;
  - cadastra as issues no fork com os pontos.

---

## 4. Cronograma interno

Datas relativas aos prazos: "D1−3" = três dias antes do prazo da etapa 1.

| Quando | O quê | Quem |
|---|---|---|
| Hoje | Ler este guia e as histórias. Aceitar o convite do fork | todos |
| Hoje | Convidar os 4 como colaboradores do fork | Luis |
| D1−4 | Ler o relatório revisado e o `AVALIACAO_RELATORIO.md`; mandar ajustes no grupo | todos |
| D1−2 | Fechar o texto (Daniel) e o diagrama (Leonardo); compilar e conferir o PDF | Daniel, Leonardo |
| D1−1 | **Entregar o PDF no Aprender** | Daniel |
| D2−6 | Cadastrar as 16 issues no fork, com labels e pontos | Weldo |
| D2−5 | Cada um cria a sua branch, cria os `.feature` e faz o **próprio** commit | todos |
| D2−4 | Abrir o PR interno (`feature/<tema>` → `sprint-1`, **base no fork**) | todos |
| D2−3 | Revisão cruzada: passos iguais, rótulos, tags. Corrigir e dar merge | Tarsila + todos |
| D2−2 | Publicar a Wiki | Weldo + Luis |
| D2−1 | **Abrir o PR para o EngSwCIC/CAMAAR** e **entregar o `.txt`** com o link do PR | Luis |
| D2 | Conferência final. A partir do PR, **ninguém mais commita na `sprint-1`** | todos |

---

## 5. Regras que valem nota

1. **Cada aluno faz o commit das próprias modificações.** O monitor confere a autoria dos commits.
   - Ninguém commita o arquivo de outra pessoa.
   - Confira se o seu git está com o **mesmo e-mail da sua conta do GitHub**, senão o commit não aparece no seu nome:
     ```bash
     git config user.name   # seu nome
     git config user.email  # o mesmo e-mail da sua conta do GitHub
     ```
2. **Nomes e matrículas** de todos vão no **corpo do PR** e na **Wiki**. Um monitor já escreveu, num PR de outro grupo: "do contrario não consigo atribuir a nota ao aluno".
3. **Um único PR por grupo**, da branch `sprint-1` do fork para o `main` do EngSwCIC/CAMAAR.
4. **Depois de abrir o PR, a `sprint-1` não recebe mais commits.** Um PR aberto se atualiza a cada push: dois grupos de 2026.1 mudaram a branch depois do prazo.
5. **As features não são implementadas.** Só os `.feature`: sem step definitions e sem `rails new` agora.
6. **Toda feature tem pelo menos um cenário feliz e um triste.**
7. **As histórias seguem o padrão Connextra** (Como… / Quero… / Para que…).
8. **Os pontos estão atribuídos** às histórias (Fibonacci), para a velocity. Estão no `HISTORIAS_DE_USUARIO.md` e na Wiki.

---

## 6. Passo a passo no Git e no GitHub

### 6.1 Uma vez só (cada integrante)

```bash
git clone git@github.com:Luisserra99/CAMAAR.git
cd CAMAAR
git remote add upstream git@github.com:EngSwCIC/CAMAAR.git   # o repositório do professor
git fetch --all
git switch sprint-1
```

### 6.2 Criar a sua branch e os seus arquivos

```bash
git switch sprint-1 && git pull
git switch -c feature/autenticacao      # sigaa | templates | formularios | avaliacoes
mkdir -p features/autenticacao
# crie cada arquivo e cole o bloco Gherkin correspondente do ESPECIFICACOES_BDD.md
git add features/autenticacao/login.feature
git commit -m "test(bdd): adiciona cenários de login (#104)"
# repita para cada arquivo (um commit por feature fica mais fácil de revisar)
git push -u origin feature/autenticacao
```

- **Só adicionem os `.feature`.** Nada de `git add .`: a pasta `instrucoes_entrega_sprint1/` tem o PDF do professor e documentos internos, e não pode ir para o PR.
- Se quiserem que o git ignore essa pasta só na máquina de vocês, sem mudar o repositório, coloquem o nome dela em `.git/info/exclude`.

### 6.3 Pull Request interno (para a `sprint-1` do fork)

1. No GitHub, clique em **Compare & pull request** na sua branch.
2. **Atenção:** o GitHub sugere como base o repositório do professor. Troque para **base repository: `Luisserra99/CAMAAR`, base: `sprint-1`**. Vários grupos abriram PRs internos no repositório do professor por engano.
3. No título, cite as issues. Exemplo: `Autenticação: #104, #105, #107 (BDD)`.
4. Peça revisão de outro integrante. A Tarsila faz a revisão cruzada dos passos.
5. Merge com **"Create a merge commit"**, para preservar a autoria dos seus commits. **Não usem squash.**

### 6.4 Pull Request final (para o professor), feito pelo Luis

- **Quando:** depois dos 5 merges internos. Antes, confira que a `sprint-1` só tem `features/**/*.feature` além do que já estava no `main`.
- **Onde:** GitHub do fork → branch `sprint-1` → **New pull request**:
  - **base repository:** `EngSwCIC/CAMAAR`, **base:** `main`;
  - **head repository:** `Luisserra99/CAMAAR`, **compare:** `sprint-1`.
- **Título:** `Grupo XX - Sprint 1 (#98 a #113)`. O exemplo do PDF é `Grupo 01 - #47 Refatorar Questionários`. Como entregamos todas as issues, citamos o intervalo, e a lista completa vai no corpo.
- **Corpo:**

```markdown
## Grupo XX - Sprint 1: especificação BDD (Cucumber) das histórias #98 a #113

| Integrante | Matrícula | Issues | Arquivos |
|---|---|---|---|
| Luis Eduardo Curi Serra | 251033574 | #104, #105, #107 | features/autenticacao/*.feature |
| Weldo Gonçalves da Silva Junior | 222014133 | #98, #100, #108 | features/sigaa/*.feature |
| Daniel Dezan Baby | 232046097 | #102, #111, #112 | features/templates/*.feature |
| Leonardo Tome Sampaio | 222005448 | #103, #106, #110, #113 | features/formularios/*.feature |
| Tarsila Marques de Oliveira Alves | 242012029 | #99, #101, #109 | features/avaliacoes/*.feature |

- Responsáveis pela branch `sprint-1`: Luis Eduardo Curi Serra (251033574), Scrum Master
- Cenários em português (`# language: pt`), com `@issue-NN` em cada feature e `@feliz`/`@triste` em cada cenário
- O #106 (bônus) foi especificado como regras dentro de `criar_formulario.feature` e `visualizar_resultados.feature`
- Wiki da Sprint 1: https://github.com/Luisserra99/CAMAAR/wiki
```

- **Depois de abrir:**
  - coloque o link do PR no `.txt` e na Wiki;
  - entregue o `.txt` no Aprender;
  - **não faça mais commits na `sprint-1`**.

### 6.5 Wiki

1. No fork, abra a aba **Wiki** → **Create the first page**.
2. Cole o conteúdo do `WIKI_SPRINT1.md`.
3. Troque "Grupo XX", o link do PR e o que mais mudar. A página inicial (Home) precisa responder:
   - quem foi SM e quem foi PO;
   - as funcionalidades e as regras de negócio de cada uma;
   - quem é responsável por cada funcionalidade;
   - a política de branching;
   - os pontos de cada história.

### 6.6 Cadastrar as histórias como issues no fork (PO)

O passo a passo está no começo do `HISTORIAS_DE_USUARIO.md`. O título de cada issue leva o número do upstream, por exemplo `[#104] Sistema de login`. Também é o número do upstream que usamos nas tags e no PR, não o número da issue no fork.

---

## 7. Como escrever (e conferir) os cenários

- **Convenções:** tudo está no começo do `ESPECIFICACOES_BDD.md`. O mais importante:
  - `# language: pt` na **primeira linha** (nunca `pt-br`);
  - `@issue-NN` na Funcionalidade e `@feliz`/`@triste` nos cenários;
  - os passos comuns escritos **exatamente iguais** em todos os arquivos.
- **Técnica do professor para o caminho triste:** testar um valor abaixo do limite, um dentro, um acima, um em formato errado e um que quebre uma regra de negócio. Exemplos que já estão nas nossas features:
  - nome do template com 100 caracteres (passa) e com 101 (falha);
  - comentário com 1000 caracteres (passa) e com 1001 (falha);
  - senha com 7 caracteres;
  - link de senha com 49 horas;
  - JSON mal formatado;
  - turma que não existe no `classes.json`;
  - template sem questões.
- **O que os monitores cobraram de outros grupos:**
  - dizer em que tela o usuário está e quais campos preenche;
  - deixar claro o resultado do caminho triste;
  - Contexto curto, só com `Dado`;
  - não repetir cenário entre features;
  - não criar tela de cadastro (#100);
  - importação e atualização no mesmo botão;
  - template vazio não gera formulário;
  - depois de excluir, o template some da lista.
- **Conferir a sintaxe** (opcional; não precisa do Rails). Com Ruby instalado:
  ```bash
  gem install cucumber
  cucumber --dry-run features/
  ```
  Os passos vão aparecer como *undefined*, o que é normal porque não implementamos nada. O importante é **não aparecer erro de parse**. Nós já validamos os 15 arquivos com o parser oficial do Gherkin: 55 cenários e 70 execuções, contando as linhas de `Exemplos`.

---

## 8. Definition of Done da Sprint 1

- [ ] PDF do modelo ER entregue no Aprender, com a estrutura do template e o diagrama aparecendo.
- [ ] Os 5 integrantes são colaboradores do fork.
- [ ] As 16 issues foram cadastradas no fork, com pontos e responsáveis.
- [ ] Os 15 `.feature` estão na `sprint-1`, cada um commitado pelo seu dono, com `# language: pt`, tags e ≥1 feliz + ≥1 triste.
- [ ] O PR para o EngSwCIC/CAMAAR está aberto, com título no padrão e nomes e matrículas no corpo.
- [ ] A Wiki está publicada, respondendo às perguntas do PDF.
- [ ] O `.txt` foi entregue no Aprender, com o link do repositório, nomes e matrículas.
- [ ] A `sprint-1` não recebeu nenhum commit depois do PR.

---

## 9. Spike: views em Rails a partir do Figma (interno, prepara a Sprint 2)

O PDF pede essa investigação, mas ela **não é entregue**. Decidimos não colocá-la no relatório. Esta seção serve para a Sprint 2 começar rápido.

### 9.1 Acesso ao Figma

- Link: https://www.figma.com/design/5GVzfaJSBbcXmGvuvAi7WF/Camaar-2024.1. É o arquivo "Camaar 2024.1"; o protótipo começa no frame `2:2471`.
- A API do Figma exige login, então montamos o inventário pela miniatura do arquivo e pelas views que grupos anteriores fizeram a partir dele.
- **Alguém do grupo precisa abrir o arquivo logado** e conferir as cores e os tamanhos exatos no *Inspect*/*Dev Mode*.
- O arquivo tem dois fluxos:
  - **"Fluxo do Usuário":** usuário sem acesso ao gerenciamento;
  - **"Fluxo do Admin":** admin com acesso ao gerenciamento.

### 9.2 Telas

| Tela | Quem vê | Elementos principais | Issues |
|---|---|---|---|
| Login | visitante | card "LOGIN" com "Email" e "Senha", botão verde "Entrar"; painel roxo "Bem vindo ao Camaar" | #104 |
| Layout logado | todos | header (☰, título da página, busca, avatar com "Sair"); menu lateral com "Avaliações" e, **só para admin**, "Gerenciamento" | #104 |
| Avaliações | participante (e admin) | grade de cards (matéria, semestre, professor) dos formulários pendentes | #109 |
| Responder | participante | uma caixa por questão (radio ou texto) e botão roxo redondo de enviar | #99 |
| Gerenciamento | admin | painel com 4 botões verdes: "Importar dados", "Editar Templates", "Enviar Formularios", "Resultados" | #98, #108, #102, #103, #110 |
| Templates | admin | cards dos templates com lápis e lixeira, e um card "+" | #111, #112 |
| Criar/editar template (modal) | admin | "Nome do template", e para cada questão "Tipo" (Radio/Texto), "Texto" e "Opções"; botão "+" e botão "Criar" | #102, #112 |
| Enviar formulários (modal) | admin | "Template" (select), tabela de turmas com checkbox (Nome, Semestre, Código), botão "Enviar". **Público-alvo (#113) não está no Figma**: precisamos acrescentar | #103, #113 |
| Resultados | admin | cards ou lista dos formulários, com "Baixar CSV" | #110, #101 |
| Definir/redefinir senha | usuário | **não está no Figma**: reaproveitar o layout do login (Nova senha, Confirmar senha, Salvar senha) | #105, #107 |

**Tokens visuais** (valores que outros grupos copiaram do Figma; conferir no Inspect):

| Elemento | Valor |
|---|---|
| Roxo | `#6C2365` |
| Verde dos botões | `#22C55E` |
| Verde claro do Gerenciamento | `#86EFAC` |
| Fundo | `#DBDBDB` |
| Bordas | `#D9D9D9` |
| Texto cinza | `#8E8E8E` |
| Fonte | Roboto |
| Menu lateral | 257 px |
| Header | 60 px |
| Card | 278×130 px |

### 9.3 Stack sugerida

- **Base:**
  - Ruby 3.4 + Rails 8.1, que é o padrão da maioria dos grupos de 2026.1: importmap, Turbo, Stimulus, Propshaft e SQLite;
  - no Ruby 3.4, o CSV precisa de `gem "csv"` no Gemfile.
- **Autenticação:** `has_secure_password` (bcrypt), com sessão própria. 9 de 11 grupos fizeram assim, e o Devise só complica o "login por e-mail **ou** matrícula".
- **Testes:** `cucumber-rails` (`require: false`), `capybara`, `rspec-rails`, `database_cleaner-active_record`, `simplecov`.
- **Desenvolvimento:** `letter_opener`, para ver os e-mails no navegador.
- **CSS:** CSS puro com variáveis para os tokens (sem etapa de build), ou `tailwindcss-rails` v4 se alguém do grupo já usa Tailwind.

### 9.4 Telas → rotas, controllers e views

```ruby
# config/routes.rb (proposta)
root "evaluations#index"                                   # Avaliações (#109)
get    "login",  to: "sessions#new"
post   "login",  to: "sessions#create"
delete "logout", to: "sessions#destroy"                    # #104
resources :password_setups, only: %i[edit update], param: :token            # #105
resources :password_resets, only: %i[new create edit update], param: :token # #107
resources :forms, only: :show do                           # Responder (#99)
  resource :submission, only: :create
end
namespace :admin do
  root "dashboard#index"                                   # Gerenciamento (#104)
  resource  :sigaa_import, only: :create                   # Importar dados (#98, #100, #108)
  resources :form_templates, except: :show                 # Templates (#102, #111, #112)
  resources :forms, only: %i[index new create] do          # Enviar (#103, #113) e Resultados (#110)
    get :results, on: :member                              # Baixar CSV (#101)
  end
end
```

**Organização das views:**
- **`layouts/auth.html.erb`:** login, definir senha e esqueci minha senha (card branco + painel roxo).
- **`layouts/application.html.erb`:** usa os partials `shared/_header`, `shared/_sidebar` e `shared/_flash`. O título de cada página vem de `content_for :title`.
  - No `_sidebar`, o item "Gerenciamento" fica dentro de `if current_user.admin?`.
  - A proteção de verdade fica num `Admin::BaseController` com `before_action :require_admin`.
- **Componentes repetidos viram partials:** card de avaliação, card de template, campos de questão (`_question_fields`).
- **Modais:** usar Turbo Frame. Sem JavaScript (como no Capybara com rack_test), o link abre a página inteira e o teste continua funcionando.

### 9.5 Dicas técnicas

- **Questões dinâmicas no template:** `accepts_nested_attributes_for :questions, allow_destroy: true` + `fields_for`, mais um controller Stimulus que clona um `<template>` para "Adicionar questão" e mostra "Opções" só quando o tipo é Radio.
- **#112 (cópia das questões):** um service, por exemplo `FormDispatcher`, que numa transação:
  - cria um `Form` por turma;
  - duplica as `Question`/`Option` do template com `form_id`;
  - usa `has_many :forms, dependent: :nullify` no `FormTemplate`.
- **Excluir:** use `button_to … method: :delete, form: { data: { turbo_confirm: "…" } }`.
  - `link_to … data: { turbo_method: :delete }` não funciona sem JavaScript (quebrou o Cucumber de outros grupos).
  - `data-confirm` é a sintaxe antiga e o Turbo ignora.
- **Botões só com ícone** ("+", lápis, lixeira, enviar): coloquem `aria-label` com o mesmo texto usado no BDD ("Novo template", "Adicionar questão", "Editar", "Excluir", "Enviar").
- **Usuário importado sem senha:**
  - `has_secure_password` exige o digest preenchido. Usem `has_secure_password validations: false` e validem a senha (≥ 8) e a confirmação no fluxo de definir senha;
  - **não** gravem uma senha aleatória no lugar do hash: um grupo fez isso e o login quebrou.
- **Token do e-mail:** gerar com `SecureRandom.urlsafe_base64`, guardar só o digest (`token_digest`) com `token_expires_at = 48.hours.from_now` e limpar depois do uso, que é o que o modelo ER descreve. O Rails 8 tem `generates_token_for`, mas o padrão dele é 15 minutos.
- **Importação:**
  - um service `SigaaImporter` idempotente, dentro de `ActiveRecord::Base.transaction`, usando `find_or_initialize_by` pelas chaves naturais;
  - converter `dicente`/`docente` para `student`/`teacher`;
  - e-mail em minúsculas;
  - aceitar upload dos dois JSONs e, sem upload, ler os do repositório (foi a solução mais robusta entre os grupos);
  - novos usuários recebem `UserMailer.password_setup` (#100).
- **CSV:** `CSV.generate(col_sep: ";")` + `send_data`, com o cabeçalho = enunciados das questões, **sem** nome ou matrícula (RN14).
- **Mensagens em português:** a gem `rails-i18n` e `config.i18n.default_locale = :"pt-BR"`.

### 9.6 O que deu errado em outros grupos

- **Layout e views:**
  - header e menu copiados em cada view, em vez de usar o layout;
  - dados fixos no HTML ("2024.2", "CS101", avatar "U");
  - views com o texto padrão do gerador ("Find me in app/views/…");
  - rotas duplicadas.
- **Importação:**
  - controller chamando o service com o número errado de argumentos (a importação sempre falhava);
  - caminho de arquivo frágil (`Rails.root.join('..','..','classes.json')`).
- **E-mail:**
  - "e-mails" gravados em arquivo de log, em vez do ActionMailer;
  - API externa chamada direto, com URL fixa (impossível de testar);
  - senha enviada em texto puro.
- **Escopo:**
  - tela pública de cadastro (contradiz a #100);
  - CSV sem as respostas;
  - editar template apagando as questões.
- **Repositório:** `vendor/bundle`, `.DS_Store`, `tmp/` e `log/` commitados; app dentro de subpasta, em vez da raiz do repositório.

---

## 10. Pendências do grupo

- [ ] **Número do grupo.** Trocar "Grupo XX" no PR, no `.txt`, na Wiki e nas histórias.
- [ ] **Prazos reais** da etapa 1 e da etapa 2 (confirmar no Aprender).
- [ ] Confirmar **SM e PO** (sugestão: Luis e Weldo).
- [ ] Confirmar quem revisa o relatório: o autor do preliminar ou o Daniel.
- [ ] Alguém abrir o Figma logado e conferir os rótulos e as cores (seção 9.1).
