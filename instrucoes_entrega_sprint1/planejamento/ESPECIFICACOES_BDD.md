# Especificações BDD — CAMAAR (Sprint 1)

**Grupo XX** · Engenharia de Software · CIC/UnB

São 15 arquivos `.feature` com 55 cenários (70 execuções, contando cada linha de `Exemplos`) cobrindo as 16 issues (#98 a #113). A #106 não tem arquivo próprio; os cenários dela ficam dentro de duas outras features. As histórias e as regras de negócio (RNxx) citadas aqui estão em `HISTORIAS_DE_USUARIO.md`.

★ = feature completa; as outras são enxutas (1 cenário feliz e 1–2 tristes, às vezes mais).

## Como usar este arquivo

1. **Cada um commita o próprio arquivo.** O PDF diz que "cada aluno deve fazer o commit de suas próprias modificações". Por isso ninguém copia a feature do outro:
   - na sua branch (`feature/<tema>`), crie o arquivo no caminho indicado;
   - cole o bloco Gherkin;
   - faça o commit e o push.
2. **Para cadastrar no GitHub:** cole a seção da feature (cabeçalho + bloco) no corpo da issue correspondente do fork. O passo a passo das issues está no `HISTORIAS_DE_USUARIO.md`.
3. **Não implementamos nada nesta sprint.** Só os arquivos `.feature` vão para o PR, sem step definitions e sem app Rails.
4. **Se mudar um texto de passo, avise no grupo.** Os passos comuns (lista abaixo) precisam continuar idênticos em todos os arquivos, senão na Sprint 2 vamos ter que escrever a mesma step definition várias vezes.

## Convenções que seguimos

- **Cabeçalho e palavras-chave:**
  - A 1ª linha de todo arquivo é `# language: pt`. Não use `pt-br`: esse código não existe no Gherkin e o arquivo não é lido.
  - Palavras-chave em português: `Funcionalidade`, `Contexto`, `Cenário`, `Esquema do Cenário`, `Exemplos`, `Dado`, `Quando`, `Então`, `E`, `Mas`.
- **Tags:**
  - Na Funcionalidade, `@issue-NN` com o número da issue do **upstream**.
  - Em cada cenário, `@feliz` ou `@triste`.
  - Nos cenários do bônus de departamento, também `@issue-106`.
  - Num "Esquema do Cenário" que mistura casos válidos e inválidos, a tag fica em cada bloco de `Exemplos`.
- **Caminho feliz e triste** seguem a técnica do PDF do professor: valor dentro do limite (feliz); valor vazio, acima do limite, em formato errado ou que quebra uma regra de negócio (triste). Exemplos:
  - nome do template com 100 e 101 caracteres;
  - resposta de texto com 1000 e 1001 caracteres;
  - senha com 7 caracteres;
  - link com 49 horas.
- **O que os monitores cobraram de outros grupos** (feedback real em PRs de semestres anteriores):
  - Dizer **em que tela** o usuário está, **quais campos** ele preenche e em que ordem.
  - Todo caminho triste tem resultado claro: a mensagem e o que **não** mudou ("nenhum formulário deve ser criado").
  - O `Contexto` só contextualiza (passos `Dado`). Nada de ação ou verificação nele.
  - Não repetir o mesmo cenário em duas features. Por isso a restrição "só administrador acessa o Gerenciamento" é testada uma vez só, em `login.feature` (RN28).
  - Cadastro de usuário (#100) é feito pela importação e pelo e-mail com link. **Não existe tela de "cadastre-se".**
  - Importação e atualização do SIGAA usam **o mesmo botão** "Importar dados".
  - No envio de formulário, o administrador só escolhe o template e as turmas. Template vazio não gera formulário.
  - Depois de excluir um template, ele **não aparece mais** na lista.
  - A definição de senha não exige estar logado nem digitar o e-mail.
- **Rótulos** iguais aos do protótipo do Figma: "Avaliações", "Gerenciamento", "Importar dados", "Editar Templates", "Enviar Formulários", "Resultados", "Nome do template", "Tipo" (Radio/Texto), "Texto", "Opções", "Criar", "Enviar".
  - O que não aparece no Figma ganhou nome nosso: "Novo template", "Adicionar questão", "Editar", "Excluir", "Público-alvo", "Baixar CSV", "Esqueci minha senha", "Nova senha", "Confirmar senha", "Salvar senha".
  - **Botões que no Figma são só ícone** ("+", lápis, lixeira, o botão roxo de enviar) vão precisar, na Sprint 2, de um `aria-label` com esse mesmo texto para o Capybara achar.
- **Campo de login:** no Figma o rótulo é "Email", mas a #104 pede e-mail **ou** matrícula. Usamos "E-mail ou matrícula".
- **Pessoas são fictícias.** Os JSONs do repositório têm nomes e e-mails reais de alunos. Usamos deles só os dados das turmas (códigos, nomes das matérias, semestre, horário, departamento) e as contagens (44 discentes + 1 docente).

## Passos comuns (escrever exatamente assim)

| Passo | Onde aparece |
|---|---|
| `Dado que estou logado como administrador` | importação, envio, templates, resultados, CSV |
| `Dado que estou logado como o administrador "<nome>"` | templates (#111, #112) |
| `estou logado como a discente "<nome>"` | login, avaliações, público-alvo |
| `estou na página "<página>"` | quase todas |
| `clico em "<botão ou link>"` | todas |
| `preencho "<campo>" com "<valor>"` | login, senha, templates |
| `seleciono "<opção>" em "<campo>"` | templates, envio |
| `acesso a página "<página>"` | quando o usuário digita o endereço da página |
| `devo ver a mensagem "<mensagem>"` | todas |
| `devo ser redirecionado para a página "<página>"` | depois de uma ação que muda de página |
| `devo continuar na página "<página>"` | quando a ação falha |
| `devo estar na página "<página>"` | depois de navegar pelo menu |
| `nenhum formulário deve ser criado` / `nenhum e-mail deve ser enviado` | caminhos tristes |

Páginas citadas: "Login", "Avaliações", "Gerenciamento", "Gerenciamento - Templates", "Gerenciamento - Resultados", "Definir senha", "Esqueci minha senha".

> **Dica para a Sprint 2:** o mesmo passo às vezes aparece como `Dado que estou na página …` e às vezes como `E estou na página …`. Na step definition, usem a parte opcional do Cucumber Expression: `Given('(que )estou na página {string}')`.

## Dados de teste (fictícios)

| Pessoa | Perfil | E-mail | Matrícula / usuário SIGAA | Senha |
|---|---|---|---|---|
| Ana Souza | discente | ana.souza@aluno.unb.br | 200012345 | senha12345 |
| Bruno Alves | discente importado, sem senha | bruno.alves@aluno.unb.br | 211055000 | — |
| Carlos Lima | docente | carlos.lima@unb.br | 10293847566 | docente2026 |
| Beatriz Rocha | administradora | beatriz.rocha@unb.br | 100200300 | admin2026! |
| Marcos Teixeira | outro administrador | — | — | — |
| Pedro Nunes | discente novo no SIGAA (#108) | — | 231000111 | — |

Turmas dos JSONs do repositório, todas do semestre 2021.2 e do "DEPTO CIÊNCIAS DA COMPUTAÇÃO":

| Turma | Matéria | Horário | Observação |
|---|---|---|---|
| CIC0097 - TA | BANCOS DE DADOS | 35T45 | 44 discentes + 1 docente |
| CIC0105 - TA | ENGENHARIA DE SOFTWARE | 35M12 | |
| CIC0202 - TA | PROGRAMAÇÃO CONCORRENTE | 35M34 | |

Nos cenários de departamento entra também a turma fictícia **MAT0025 - TA** (CÁLCULO 1, "DEPTO MATEMÁTICA").

## Índice

| Issue | Arquivo | Responsável | Cenários (execuções) |
|---|---|---|---|
| #104 ★ | `features/autenticacao/login.feature` | Luis | 6 (11) |
| #105 | `features/autenticacao/definicao_senha.feature` | Luis | 3 (6) |
| #107 | `features/autenticacao/redefinicao_senha.feature` | Luis | 4 (4) |
| #98 ★ | `features/sigaa/importar_dados_sigaa.feature` | Weldo | 3 (6) |
| #100 | `features/sigaa/cadastro_usuarios.feature` | Weldo | 3 (3) |
| #108 | `features/sigaa/atualizar_dados_sigaa.feature` | Weldo | 2 (2) |
| #102 ★ | `features/templates/criar_template.feature` | Daniel | 6 (9) |
| #111 | `features/templates/visualizar_templates.feature` | Daniel | 2 (2) |
| #112 | `features/templates/editar_deletar_template.feature` | Daniel | 4 (4) |
| #103 ★ + #106 | `features/formularios/criar_formulario.feature` | Leonardo | 7 (7), 2 deles `@issue-106` |
| #113 | `features/formularios/formulario_publico_alvo.feature` | Leonardo | 2 (2) |
| #110 + #106 | `features/formularios/visualizar_resultados.feature` | Leonardo | 3 (3), 1 deles `@issue-106` |
| #99 ★ | `features/avaliacoes/responder_formulario.feature` | Tarsila | 6 (7) |
| #109 | `features/avaliacoes/formularios_pendentes.feature` | Tarsila | 2 (2) |
| #101 | `features/avaliacoes/relatorio_csv.feature` | Tarsila | 2 (2) |

---

## Tema: Autenticação (Luis)

### #104 — Sistema de login ★

- **Arquivo:** `features/autenticacao/login.feature`
- **Pontos:** 3
- **Regras cobertas:** RN26, RN27, RN28, RN12

```gherkin
# language: pt
@issue-104
Funcionalidade: Login no sistema
  Como usuário do CAMAAR
  Quero entrar no sistema com meu e-mail ou minha matrícula e a senha que eu cadastrei
  Para que eu possa responder os formulários ou gerenciar o sistema

  Contexto:
    Dado que existem os seguintes usuários com senha definida:
      | nome          | email                  | matrícula   | senha       | perfil        |
      | Ana Souza     | ana.souza@aluno.unb.br | 200012345   | senha12345  | discente      |
      | Carlos Lima   | carlos.lima@unb.br     | 10293847566 | docente2026 | docente       |
      | Beatriz Rocha | beatriz.rocha@unb.br   | 100200300   | admin2026!  | administrador |
    E estou na página "Login"

  @feliz
  Cenário: Discente entra com e-mail e senha
    Quando preencho "E-mail ou matrícula" com "ana.souza@aluno.unb.br"
    E preencho "Senha" com "senha12345"
    E clico em "Entrar"
    Então devo ser redirecionado para a página "Avaliações"
    E devo ver "Avaliações" no menu lateral
    Mas não devo ver "Gerenciamento" no menu lateral

  @feliz
  Cenário: Docente entra com o usuário do SIGAA e a senha
    Quando preencho "E-mail ou matrícula" com "10293847566"
    E preencho "Senha" com "docente2026"
    E clico em "Entrar"
    Então devo ser redirecionado para a página "Avaliações"
    Mas não devo ver "Gerenciamento" no menu lateral

  @feliz
  Cenário: Administrador entra e vê a opção de gerenciamento no menu lateral
    Quando preencho "E-mail ou matrícula" com "100200300"
    E preencho "Senha" com "admin2026!"
    E clico em "Entrar"
    Então devo ser redirecionado para a página "Avaliações"
    E devo ver "Gerenciamento" no menu lateral

  @triste
  Esquema do Cenário: Login com dados inválidos
    Quando preencho "E-mail ou matrícula" com "<login>"
    E preencho "Senha" com "<senha>"
    E clico em "Entrar"
    Então devo continuar na página "Login"
    E devo ver a mensagem "<mensagem>"

    Exemplos:
      | login                  | senha       | mensagem                                   |
      | ana.souza@aluno.unb.br | senhaerrada | E-mail/matrícula ou senha inválidos        |
      | 200012345              | senhaerrada | E-mail/matrícula ou senha inválidos        |
      | naoexiste@unb.br       | senha12345  | E-mail/matrícula ou senha inválidos        |
      | 999999999              | senha12345  | E-mail/matrícula ou senha inválidos        |
      |                        | senha12345  | Preencha o e-mail ou a matrícula e a senha |
      | ana.souza@aluno.unb.br |             | Preencha o e-mail ou a matrícula e a senha |

  @triste
  Cenário: Usuário importado do SIGAA que ainda não definiu a senha
    Dado que o discente "Bruno Alves" com matrícula "211055000" foi importado do SIGAA e ainda não definiu a senha
    Quando preencho "E-mail ou matrícula" com "211055000"
    E preencho "Senha" com "qualquersenha"
    E clico em "Entrar"
    Então devo continuar na página "Login"
    E devo ver a mensagem "Você ainda não definiu sua senha. Use o link enviado para o seu e-mail."

  @triste
  Cenário: Participante tenta abrir a página de gerenciamento pelo endereço
    Dado que estou logado como a discente "Ana Souza"
    Quando acesso a página "Gerenciamento"
    Então devo ser redirecionado para a página "Avaliações"
    E devo ver a mensagem "Acesso restrito a administradores"
```

### #105 — Sistema de definição de senha

- **Arquivo:** `features/autenticacao/definicao_senha.feature`
- **Pontos:** 3
- **Regras cobertas:** RN29, RN30, RN31

```gherkin
# language: pt
@issue-105
Funcionalidade: Definição de senha no primeiro acesso
  Como usuário importado do SIGAA
  Quero definir a minha senha pelo link que recebi por e-mail
  Para que eu consiga acessar o CAMAAR

  Contexto:
    Dado que o discente "Bruno Alves" com e-mail "bruno.alves@aluno.unb.br" foi importado do SIGAA e ainda não definiu a senha
    E ele recebeu o e-mail com o link para definir a senha

  @feliz
  Cenário: Definir a senha pelo link do e-mail, sem precisar estar logado
    Quando abro o link de definição de senha recebido por "bruno.alves@aluno.unb.br"
    E preencho "Nova senha" com "minhasenha1"
    E preencho "Confirmar senha" com "minhasenha1"
    E clico em "Salvar senha"
    Então devo ser redirecionado para a página "Login"
    E devo ver a mensagem "Senha definida com sucesso. Faça o login."
    E devo conseguir entrar com "bruno.alves@aluno.unb.br" e a senha "minhasenha1"

  @triste
  Esquema do Cenário: Senha que não segue as regras
    Quando abro o link de definição de senha recebido por "bruno.alves@aluno.unb.br"
    E preencho "Nova senha" com "<senha>"
    E preencho "Confirmar senha" com "<confirmação>"
    E clico em "Salvar senha"
    Então devo continuar na página "Definir senha"
    E devo ver a mensagem "<mensagem>"
    E "Bruno Alves" ainda não deve conseguir entrar no sistema

    Exemplos:
      | senha       | confirmação | mensagem                                 |
      | minhasenha1 | outrasenha1 | A confirmação não confere com a senha    |
      | abc1234     | abc1234     | A senha deve ter pelo menos 8 caracteres |
      |             |             | A senha deve ter pelo menos 8 caracteres |

  @triste
  Esquema do Cenário: Link que não vale mais
    Dado que o link de definição de senha <situação>
    Quando abro o link de definição de senha recebido por "bruno.alves@aluno.unb.br"
    Então devo ver a mensagem "Este link não é mais válido. Peça um novo em Esqueci minha senha."
    E não devo ver o campo "Nova senha"

    Exemplos:
      | situação                |
      | foi enviado há 49 horas |
      | já foi usado uma vez    |
```

### #107 — Redefinição de senha (bônus)

- **Arquivo:** `features/autenticacao/redefinicao_senha.feature`
- **Pontos:** 3
- **Regras cobertas:** RN34, RN35 (mais RN29 e RN30)

```gherkin
# language: pt
@issue-107
Funcionalidade: Redefinição de senha
  Como usuário do CAMAAR
  Quero redefinir a minha senha por um link enviado para o meu e-mail
  Para que eu recupere o acesso ao sistema quando esquecer a senha

  Contexto:
    Dado que existe o usuário "Ana Souza" com e-mail "ana.souza@aluno.unb.br" e senha "senha12345"
    E estou na página "Login"

  @feliz
  Cenário: Pedir o link de redefinição
    Quando clico em "Esqueci minha senha"
    E preencho "E-mail" com "ana.souza@aluno.unb.br"
    E clico em "Enviar link"
    Então devo ver a mensagem "Se o e-mail estiver cadastrado, você vai receber um link para redefinir a senha."
    E "ana.souza@aluno.unb.br" deve receber um e-mail com o link de redefinição de senha

  @feliz
  Cenário: Cadastrar a nova senha pelo link
    Dado que "ana.souza@aluno.unb.br" pediu a redefinição de senha e recebeu o link
    Quando abro o link de redefinição de senha recebido por "ana.souza@aluno.unb.br"
    E preencho "Nova senha" com "novasenha99"
    E preencho "Confirmar senha" com "novasenha99"
    E clico em "Salvar senha"
    Então devo ser redirecionado para a página "Login"
    E devo conseguir entrar com "ana.souza@aluno.unb.br" e a senha "novasenha99"
    Mas não devo conseguir entrar com "ana.souza@aluno.unb.br" e a senha "senha12345"

  @triste
  Cenário: Pedir o link com um e-mail que não está cadastrado
    Quando clico em "Esqueci minha senha"
    E preencho "E-mail" com "ninguem@unb.br"
    E clico em "Enviar link"
    Então devo ver a mensagem "Se o e-mail estiver cadastrado, você vai receber um link para redefinir a senha."
    E nenhum e-mail deve ser enviado

  @triste
  Cenário: Pedir o link com um e-mail em formato inválido
    Quando clico em "Esqueci minha senha"
    E preencho "E-mail" com "ana.souza"
    E clico em "Enviar link"
    Então devo continuar na página "Esqueci minha senha"
    E devo ver a mensagem "Informe um e-mail válido"
    E nenhum e-mail deve ser enviado
```

---

## Tema: Dados do SIGAA (Weldo)

### #98 — Importar dados do SIGAA ★

- **Arquivo:** `features/sigaa/importar_dados_sigaa.feature`
- **Pontos:** 5
- **Regras cobertas:** RN02, RN03, RN04, RN05 (a RN01 é testada em `login.feature`)

```gherkin
# language: pt
@issue-98
Funcionalidade: Importar dados do SIGAA
  Como administrador
  Quero importar as turmas, matérias e participantes do SIGAA
  Para que a base de dados do CAMAAR seja alimentada sem eu precisar cadastrar tudo à mão

  Contexto:
    Dado que estou logado como administrador
    E estou na página "Gerenciamento"

  @feliz
  Cenário: Primeira importação com a base vazia
    Dado que não existe nenhuma turma cadastrada
    E os arquivos do SIGAA são os arquivos "classes.json" e "class_members.json" do repositório
    Quando clico em "Importar dados"
    Então devo ver a mensagem "Dados do SIGAA importados com sucesso"
    E devem existir as seguintes turmas cadastradas:
      | matéria | nome                    | turma | semestre | horário |
      | CIC0097 | BANCOS DE DADOS         | TA    | 2021.2   | 35T45   |
      | CIC0105 | ENGENHARIA DE SOFTWARE  | TA    | 2021.2   | 35M12   |
      | CIC0202 | PROGRAMAÇÃO CONCORRENTE | TA    | 2021.2   | 35M34   |
    E a turma "CIC0097 - TA" deve ter 44 discentes e 1 docente
    E a matéria "CIC0097" deve pertencer ao departamento "DEPTO CIÊNCIAS DA COMPUTAÇÃO"

  @feliz
  Cenário: Importar de novo os mesmos arquivos não duplica nada
    Dado que os arquivos "classes.json" e "class_members.json" do repositório já foram importados
    Quando clico em "Importar dados"
    Então devo ver a mensagem "Dados do SIGAA importados com sucesso"
    E devem existir 3 turmas cadastradas
    E devem existir 45 usuários importados do SIGAA

  @triste
  Esquema do Cenário: Arquivo do SIGAA com problema não importa nada
    Dado que não existe nenhuma turma cadastrada
    E o arquivo "<arquivo>" do SIGAA <problema>
    Quando clico em "Importar dados"
    Então devo ver a mensagem "<mensagem>"
    E não deve existir nenhuma turma cadastrada

    Exemplos:
      | arquivo            | problema                                  | mensagem                                                                         |
      | classes.json       | não é um JSON válido                      | Não foi possível importar: classes.json não é um JSON válido                     |
      | classes.json       | tem uma turma sem o campo "code"          | Não foi possível importar: classes.json tem turma sem o campo code               |
      | class_members.json | tem um discente sem o campo "email"       | Não foi possível importar: class_members.json tem participante sem o campo email |
      | class_members.json | tem participantes da turma "CIC9999 - TA" | Não foi possível importar: a turma CIC9999 - TA não existe em classes.json       |
```

### #100 — Cadastrar usuários do sistema

- **Arquivo:** `features/sigaa/cadastro_usuarios.feature`
- **Pontos:** 3
- **Regras cobertas:** RN10, RN11 (a RN12 é testada em `login.feature`)

```gherkin
# language: pt
@issue-100
Funcionalidade: Cadastro dos participantes pela importação do SIGAA
  Como administrador
  Quero que os participantes novos sejam cadastrados quando eu importo os dados do SIGAA
  Para que eles recebam o link para definir a senha e consigam acessar o CAMAAR

  Contexto:
    Dado que estou logado como administrador
    E estou na página "Gerenciamento"

  @feliz
  Cenário: Participantes novos são cadastrados sem senha e recebem o e-mail
    Dado que nenhum participante da turma "CIC0097 - TA" está cadastrado
    Quando clico em "Importar dados"
    Então os 45 participantes da turma "CIC0097 - TA" devem estar cadastrados sem senha
    E cada um deles deve receber um e-mail com o link para definir a senha

  @triste
  Cenário: Participante que já tem cadastro não recebe outro e-mail
    Dado que um dos discentes da turma "CIC0097 - TA" já está cadastrado e já definiu a senha
    Quando clico em "Importar dados"
    Então esse discente não deve receber um novo e-mail
    E os outros 44 participantes da turma devem receber o e-mail para definir a senha

  @triste
  Cenário: Importação com erro não cadastra ninguém nem envia e-mail
    Dado que nenhum participante da turma "CIC0097 - TA" está cadastrado
    Mas o arquivo "class_members.json" do SIGAA não é um JSON válido
    Quando clico em "Importar dados"
    Então nenhum usuário deve ser cadastrado
    E nenhum e-mail deve ser enviado
```

### #108 — Atualizar base de dados com os dados do SIGAA

- **Arquivo:** `features/sigaa/atualizar_dados_sigaa.feature`
- **Pontos:** 3
- **Regras cobertas:** RN36 (mais RN03 e RN04)

```gherkin
# language: pt
@issue-108
Funcionalidade: Atualizar a base de dados com os dados atuais do SIGAA
  Como administrador
  Quero atualizar os dados já importados com o que está atualmente no SIGAA
  Para que a base de dados do CAMAAR fique correta

  Contexto:
    Dado que estou logado como administrador
    E os arquivos "classes.json" e "class_members.json" do repositório já foram importados
    E estou na página "Gerenciamento"

  @feliz
  Cenário: O mesmo botão de importação atualiza o que mudou no SIGAA
    Dado que no SIGAA o horário da turma "CIC0105 - TA" mudou para "24M34"
    E no SIGAA a turma "CIC0097 - TA" ganhou o discente "Pedro Nunes" com matrícula "231000111"
    Quando clico em "Importar dados"
    Então devo ver a mensagem "Dados do SIGAA importados com sucesso"
    E a turma "CIC0105 - TA" deve ter o horário "24M34"
    E a turma "CIC0097 - TA" deve ter 45 discentes e 1 docente
    E devem existir 3 turmas cadastradas

  @triste
  Cenário: Atualização com arquivo inválido não altera a base
    Dado que no SIGAA o horário da turma "CIC0105 - TA" mudou para "24M34"
    Mas o arquivo "class_members.json" do SIGAA não é um JSON válido
    Quando clico em "Importar dados"
    Então devo ver a mensagem "Não foi possível importar: class_members.json não é um JSON válido"
    E a turma "CIC0105 - TA" deve continuar com o horário "35M12"
```

---

## Tema: Templates (Daniel)

### #102 — Criar template de formulário ★

- **Arquivo:** `features/templates/criar_template.feature`
- **Pontos:** 5
- **Regras cobertas:** RN17, RN18, RN19, RN20 (a RN16 é testada em `login.feature`)

```gherkin
# language: pt
@issue-102
Funcionalidade: Criar template de formulário
  Como administrador
  Quero criar um template com as questões que vão estar no formulário
  Para que eu possa gerar formulários de avaliação das turmas a partir dele

  Contexto:
    Dado que estou logado como administrador
    E estou na página "Gerenciamento - Templates"

  @feliz
  Cenário: Criar um template com uma questão Radio e uma questão Texto
    Quando clico em "Novo template"
    E preencho "Nome do template" com "Avaliação de Disciplina 2021.2"
    E clico em "Adicionar questão"
    E seleciono "Radio" em "Tipo" da questão 1
    E preencho "Texto" da questão 1 com "O professor explicou bem o conteúdo?"
    E preencho "Opções" da questão 1 com "Concordo; Não concordo nem discordo; Discordo"
    E clico em "Adicionar questão"
    E seleciono "Texto" em "Tipo" da questão 2
    E preencho "Texto" da questão 2 com "Deixe um comentário sobre a disciplina"
    E clico em "Criar"
    Então devo ver a mensagem "Template criado com sucesso"
    E devo ver o template "Avaliação de Disciplina 2021.2" na lista de templates
    E o template "Avaliação de Disciplina 2021.2" deve ter 2 questões

  @feliz
  Cenário: Criar um template sem questões para completar depois
    Quando clico em "Novo template"
    E preencho "Nome do template" com "Rascunho de avaliação"
    E clico em "Criar"
    Então devo ver a mensagem "Template criado com sucesso"
    E devo ver o template "Rascunho de avaliação" na lista de templates

  Esquema do Cenário: Limite de tamanho do nome do template
    Quando clico em "Novo template"
    E preencho "Nome do template" com um texto de <tamanho> caracteres
    E clico em "Criar"
    Então devo ver a mensagem "<mensagem>"

    @feliz
    Exemplos: No limite
      | tamanho | mensagem                    |
      | 100     | Template criado com sucesso |

    @triste
    Exemplos: Acima do limite
      | tamanho | mensagem                                             |
      | 101     | O nome do template deve ter no máximo 100 caracteres |

  @triste
  Esquema do Cenário: Nome do template vazio ou repetido
    Dado que existe o template "Avaliação de Disciplina 2021.2" criado por mim
    Quando clico em "Novo template"
    E preencho "Nome do template" com "<nome>"
    E clico em "Criar"
    Então devo ver a mensagem "<mensagem>"
    E deve existir só 1 template criado por mim

    Exemplos:
      | nome                           | mensagem                            |
      |                                | O nome do template é obrigatório    |
      | Avaliação de Disciplina 2021.2 | Já existe um template com esse nome |

  @triste
  Cenário: Questão sem texto
    Quando clico em "Novo template"
    E preencho "Nome do template" com "Avaliação de Disciplina 2021.2"
    E clico em "Adicionar questão"
    E seleciono "Texto" em "Tipo" da questão 1
    E clico em "Criar"
    Então devo ver a mensagem "A questão 1 precisa de um texto"
    E o template "Avaliação de Disciplina 2021.2" não deve ser criado

  @triste
  Esquema do Cenário: Questão Radio com menos de 2 opções
    Quando clico em "Novo template"
    E preencho "Nome do template" com "Avaliação de Disciplina 2021.2"
    E clico em "Adicionar questão"
    E seleciono "Radio" em "Tipo" da questão 1
    E preencho "Texto" da questão 1 com "O professor foi pontual?"
    E preencho "Opções" da questão 1 com "<opções>"
    E clico em "Criar"
    Então devo ver a mensagem "A questão 1 precisa de pelo menos 2 opções"
    E o template "Avaliação de Disciplina 2021.2" não deve ser criado

    Exemplos:
      | opções |
      |        |
      | Sim    |
```

### #111 — Visualização dos templates criados

- **Arquivo:** `features/templates/visualizar_templates.feature`
- **Pontos:** 2
- **Regras cobertas:** RN41, RN42

```gherkin
# language: pt
@issue-111
Funcionalidade: Visualizar os templates criados
  Como administrador
  Quero ver os templates que eu criei
  Para que eu possa escolher qual editar ou excluir

  Contexto:
    Dado que estou logado como o administrador "Beatriz Rocha"

  @feliz
  Cenário: Ver a lista dos meus templates a partir do Gerenciamento
    Dado que existem os templates:
      | nome                           | criado por      |
      | Avaliação de Disciplina 2021.2 | Beatriz Rocha   |
      | Avaliação Docente 2021.2       | Beatriz Rocha   |
      | Template do outro admin        | Marcos Teixeira |
    E estou na página "Gerenciamento"
    Quando clico em "Editar Templates"
    Então devo estar na página "Gerenciamento - Templates"
    E devo ver o template "Avaliação de Disciplina 2021.2" na lista de templates
    E devo ver o template "Avaliação Docente 2021.2" na lista de templates
    Mas não devo ver o template "Template do outro admin" na lista de templates
    E cada template da lista deve ter as opções "Editar" e "Excluir"

  @triste
  Cenário: Administrador que ainda não criou nenhum template
    Dado que "Beatriz Rocha" ainda não criou nenhum template
    Quando acesso a página "Gerenciamento - Templates"
    Então devo ver a mensagem "Você ainda não criou nenhum template"
    E devo ver a opção "Novo template"
```

### #112 — Edição e deleção de templates

- **Arquivo:** `features/templates/editar_deletar_template.feature`
- **Pontos:** 3
- **Regras cobertas:** RN43, RN44, RN45

```gherkin
# language: pt
@issue-112
Funcionalidade: Editar e excluir templates
  Como administrador
  Quero editar ou excluir um template que eu criei sem mexer nos formulários que já foram enviados
  Para que eu mantenha os templates organizados

  Contexto:
    Dado que estou logado como o administrador "Beatriz Rocha"
    E existe o template "Avaliação de Disciplina 2021.2" criado por "Beatriz Rocha" com a questão "Deixe um comentário sobre a disciplina"
    E a turma "CIC0097 - TA" recebeu o formulário "Avaliação de Disciplina 2021.2"
    E estou na página "Gerenciamento - Templates"

  @feliz
  Cenário: Editar o template não altera o formulário já enviado
    Quando clico em "Editar" no template "Avaliação de Disciplina 2021.2"
    E preencho "Texto" da questão 1 com "O que você mudaria na disciplina?"
    E clico em "Salvar"
    Então devo ver a mensagem "Template atualizado com sucesso"
    E o template "Avaliação de Disciplina 2021.2" deve ter a questão "O que você mudaria na disciplina?"
    Mas o formulário da turma "CIC0097 - TA" deve continuar com a questão "Deixe um comentário sobre a disciplina"

  @feliz
  Cenário: Excluir o template
    Quando clico em "Excluir" no template "Avaliação de Disciplina 2021.2"
    E confirmo a exclusão
    Então devo ver a mensagem "Template excluído com sucesso"
    E não devo ver o template "Avaliação de Disciplina 2021.2" na lista de templates
    Mas o formulário da turma "CIC0097 - TA" deve continuar disponível para os participantes

  @triste
  Cenário: Salvar a edição com o nome em branco
    Quando clico em "Editar" no template "Avaliação de Disciplina 2021.2"
    E preencho "Nome do template" com ""
    E clico em "Salvar"
    Então devo ver a mensagem "O nome do template é obrigatório"
    E o template "Avaliação de Disciplina 2021.2" não deve ter sido alterado

  @triste
  Cenário: Tentar editar um template criado por outro administrador
    Dado que existe o template "Template do outro admin" criado por "Marcos Teixeira"
    Quando acesso a página de edição do template "Template do outro admin"
    Então devo ser redirecionado para a página "Gerenciamento - Templates"
    E devo ver a mensagem "Você só pode alterar templates criados por você"
```

---

## Tema: Formulários do administrador (Leonardo)

### #103 — Criar formulário de avaliação ★ (com os cenários do bônus #106)

- **Arquivo:** `features/formularios/criar_formulario.feature`
- **Pontos:** 3 (#103) + 5 (#106)
- **Regras cobertas:** RN21, RN22, RN23, RN24, RN25, RN32

```gherkin
# language: pt
@issue-103
Funcionalidade: Criar formulário de avaliação a partir de um template
  Como administrador
  Quero criar formulários a partir de um template para as turmas que eu escolher
  Para que eu avalie o desempenho das turmas no semestre atual

  Contexto:
    Dado que estou logado como administrador
    E existem as seguintes turmas cadastradas:
      | matéria | nome                    | turma | semestre | departamento                 |
      | CIC0097 | BANCOS DE DADOS         | TA    | 2021.2   | DEPTO CIÊNCIAS DA COMPUTAÇÃO |
      | CIC0105 | ENGENHARIA DE SOFTWARE  | TA    | 2021.2   | DEPTO CIÊNCIAS DA COMPUTAÇÃO |
      | CIC0202 | PROGRAMAÇÃO CONCORRENTE | TA    | 2021.2   | DEPTO CIÊNCIAS DA COMPUTAÇÃO |
    E existe o template "Avaliação de Disciplina 2021.2" com 2 questões
    E estou na página "Gerenciamento"

  @feliz
  Cenário: Enviar o formulário para duas turmas
    Quando clico em "Enviar Formulários"
    E seleciono "Avaliação de Disciplina 2021.2" em "Template"
    E marco a turma "CIC0097 - TA"
    E marco a turma "CIC0105 - TA"
    E clico em "Enviar"
    Então devo ver a mensagem "Formulário enviado para 2 turmas"
    E as turmas "CIC0097 - TA" e "CIC0105 - TA" devem ter um formulário "Avaliação de Disciplina 2021.2" cada
    E cada formulário deve ter uma cópia das 2 questões do template
    Mas a turma "CIC0202 - TA" não deve ter formulário

  @triste
  Cenário: Enviar sem marcar nenhuma turma
    Quando clico em "Enviar Formulários"
    E seleciono "Avaliação de Disciplina 2021.2" em "Template"
    E clico em "Enviar"
    Então devo ver a mensagem "Selecione pelo menos uma turma"
    E nenhum formulário deve ser criado

  @triste
  Cenário: Enviar sem escolher o template
    Quando clico em "Enviar Formulários"
    E marco a turma "CIC0097 - TA"
    E clico em "Enviar"
    Então devo ver a mensagem "Selecione um template"
    E nenhum formulário deve ser criado

  @triste
  Cenário: Template sem questões não pode ser usado
    Dado que existe o template "Rascunho de avaliação" sem questões
    Quando clico em "Enviar Formulários"
    E seleciono "Rascunho de avaliação" em "Template"
    E marco a turma "CIC0097 - TA"
    E clico em "Enviar"
    Então devo ver a mensagem "O template escolhido não tem questões"
    E nenhum formulário deve ser criado

  @triste
  Cenário: Turma de semestre anterior não aparece para envio
    Dado que existe a turma "CIC0097 - TB" de "BANCOS DE DADOS" no semestre "2021.1"
    Quando clico em "Enviar Formulários"
    Então devo ver a turma "CIC0097 - TA" na lista de turmas
    Mas não devo ver a turma "CIC0097 - TB" na lista de turmas

  @issue-106 @feliz
  Cenário: Administrador de departamento só vê as turmas do seu departamento
    Dado que pertenço ao departamento "DEPTO CIÊNCIAS DA COMPUTAÇÃO"
    E existe a turma "MAT0025 - TA" de "CÁLCULO 1" do departamento "DEPTO MATEMÁTICA" no semestre "2021.2"
    Quando clico em "Enviar Formulários"
    Então devo ver a turma "CIC0097 - TA" na lista de turmas
    Mas não devo ver a turma "MAT0025 - TA" na lista de turmas

  @issue-106 @triste
  Cenário: Administrador de departamento tenta enviar para turma de outro departamento
    Dado que pertenço ao departamento "DEPTO CIÊNCIAS DA COMPUTAÇÃO"
    E existe a turma "MAT0025 - TA" de "CÁLCULO 1" do departamento "DEPTO MATEMÁTICA" no semestre "2021.2"
    Quando tento enviar o template "Avaliação de Disciplina 2021.2" para a turma "MAT0025 - TA" pelo endereço
    Então devo ver a mensagem "Você só pode enviar formulários para turmas do seu departamento"
    E nenhum formulário deve ser criado
```

### #113 — Criação de formulário para docentes ou discentes (bônus)

- **Arquivo:** `features/formularios/formulario_publico_alvo.feature`
- **Pontos:** 2
- **Regras cobertas:** RN46, RN47

```gherkin
# language: pt
@issue-113
Funcionalidade: Escolher o público-alvo do formulário
  Como administrador
  Quero escolher se o formulário é para os docentes ou para os discentes da turma
  Para que eu consiga avaliar a matéria pelos dois lados

  Contexto:
    Dado que a turma "CIC0097 - TA" tem o docente "Carlos Lima" e a discente "Ana Souza"
    E existe o template "Avaliação Docente 2021.2" com 2 questões

  @feliz
  Cenário: Enviar um formulário só para os docentes da turma
    Dado que estou logado como administrador
    E estou na página "Gerenciamento"
    Quando clico em "Enviar Formulários"
    E seleciono "Avaliação Docente 2021.2" em "Template"
    E seleciono "Docentes" em "Público-alvo"
    E marco a turma "CIC0097 - TA"
    E clico em "Enviar"
    Então devo ver a mensagem "Formulário enviado para 1 turma"
    E o formulário "Avaliação Docente 2021.2" da turma "CIC0097 - TA" deve aparecer em "Avaliações" para "Carlos Lima"
    Mas o formulário "Avaliação Docente 2021.2" da turma "CIC0097 - TA" não deve aparecer em "Avaliações" para "Ana Souza"

  @triste
  Cenário: Discente tenta abrir um formulário feito para os docentes
    Dado que a turma "CIC0097 - TA" recebeu o formulário "Avaliação Docente 2021.2" para os docentes
    E estou logado como a discente "Ana Souza"
    Quando acesso o formulário "Avaliação Docente 2021.2" da turma "CIC0097 - TA" pelo endereço
    Então devo ser redirecionado para a página "Avaliações"
    E devo ver a mensagem "Este formulário não está disponível para você"
```

### #110 — Visualização de resultados dos formulários (com cenário do bônus #106)

- **Arquivo:** `features/formularios/visualizar_resultados.feature`
- **Pontos:** 2
- **Regras cobertas:** RN39, RN40, RN33

```gherkin
# language: pt
@issue-110
Funcionalidade: Visualizar os formulários criados
  Como administrador
  Quero ver a lista dos formulários que foram criados
  Para que eu possa escolher de qual vou gerar o relatório das respostas

  Contexto:
    Dado que estou logado como administrador

  @feliz
  Cenário: Ver os formulários enviados e quantas respostas cada um tem
    Dado que foram enviados os formulários:
      | template                       | turma        | semestre | respostas |
      | Avaliação de Disciplina 2021.2 | CIC0097 - TA | 2021.2   | 12        |
      | Avaliação de Disciplina 2021.2 | CIC0105 - TA | 2021.2   | 0         |
    E estou na página "Gerenciamento"
    Quando clico em "Resultados"
    Então devo estar na página "Gerenciamento - Resultados"
    E devo ver o formulário "Avaliação de Disciplina 2021.2" da turma "CIC0097 - TA" com 12 respostas
    E devo ver o formulário "Avaliação de Disciplina 2021.2" da turma "CIC0105 - TA" com 0 respostas

  @triste
  Cenário: Nenhum formulário foi criado ainda
    Dado que nenhum formulário foi enviado
    Quando acesso a página "Gerenciamento - Resultados"
    Então devo ver a mensagem "Nenhum formulário foi criado ainda"

  @issue-106 @triste
  Cenário: Administrador de departamento não vê resultados de outro departamento
    Dado que pertenço ao departamento "DEPTO CIÊNCIAS DA COMPUTAÇÃO"
    E a turma "MAT0025 - TA" é do departamento "DEPTO MATEMÁTICA"
    E foram enviados os formulários:
      | template                       | turma        | semestre | respostas |
      | Avaliação de Disciplina 2021.2 | CIC0097 - TA | 2021.2   | 12        |
      | Avaliação de Disciplina 2021.2 | MAT0025 - TA | 2021.2   | 30        |
    Quando acesso a página "Gerenciamento - Resultados"
    Então devo ver o formulário "Avaliação de Disciplina 2021.2" da turma "CIC0097 - TA" com 12 respostas
    Mas não devo ver o formulário "Avaliação de Disciplina 2021.2" da turma "MAT0025 - TA"
```

---

## Tema: Participante e relatório (Tarsila)

### #99 — Responder formulário ★

- **Arquivo:** `features/avaliacoes/responder_formulario.feature`
- **Pontos:** 5
- **Regras cobertas:** RN06, RN07, RN08, RN09

```gherkin
# language: pt
@issue-99
Funcionalidade: Responder formulário de avaliação
  Como participante de uma turma
  Quero responder o formulário de avaliação da turma em que estou matriculado
  Para que a minha avaliação da turma seja registrada

  Contexto:
    Dado que a discente "Ana Souza" está matriculada na turma "CIC0097 - TA"
    E a turma "CIC0097 - TA" recebeu o formulário "Avaliação de Disciplina 2021.2" com as questões:
      | número | tipo  | texto                                  | opções                     | obrigatória |
      | 1      | Radio | O professor explicou bem o conteúdo?   | Concordo; Neutro; Discordo | sim         |
      | 2      | Texto | Deixe um comentário sobre a disciplina |                            | não         |
    E estou logado como a discente "Ana Souza"
    E estou na página "Avaliações"

  @feliz
  Cenário: Responder todas as questões e enviar
    Quando clico no formulário "Avaliação de Disciplina 2021.2" da turma "CIC0097 - TA"
    E escolho "Concordo" na questão 1
    E preencho a questão 2 com "Gostei muito das aulas práticas"
    E clico em "Enviar"
    Então devo ser redirecionado para a página "Avaliações"
    E devo ver a mensagem "Avaliação enviada com sucesso. Obrigado!"
    E não devo ver o formulário "Avaliação de Disciplina 2021.2" da turma "CIC0097 - TA"

  @feliz
  Cenário: Enviar deixando em branco a questão que não é obrigatória
    Quando clico no formulário "Avaliação de Disciplina 2021.2" da turma "CIC0097 - TA"
    E escolho "Neutro" na questão 1
    E clico em "Enviar"
    Então devo ver a mensagem "Avaliação enviada com sucesso. Obrigado!"

  @triste
  Cenário: Enviar sem responder a questão obrigatória
    Quando clico no formulário "Avaliação de Disciplina 2021.2" da turma "CIC0097 - TA"
    E preencho a questão 2 com "Comentário qualquer"
    E clico em "Enviar"
    Então devo continuar na página do formulário "Avaliação de Disciplina 2021.2"
    E devo ver a mensagem "Responda as questões obrigatórias: 1"
    E nenhuma resposta deve ser registrada

  Esquema do Cenário: Limite de tamanho da resposta de texto
    Quando clico no formulário "Avaliação de Disciplina 2021.2" da turma "CIC0097 - TA"
    E escolho "Concordo" na questão 1
    E preencho a questão 2 com um texto de <tamanho> caracteres
    E clico em "Enviar"
    Então devo ver a mensagem "<mensagem>"

    @feliz
    Exemplos: No limite
      | tamanho | mensagem                                 |
      | 1000    | Avaliação enviada com sucesso. Obrigado! |

    @triste
    Exemplos: Acima do limite
      | tamanho | mensagem                                                   |
      | 1001    | A resposta da questão 2 pode ter no máximo 1000 caracteres |

  @triste
  Cenário: Tentar responder de novo um formulário já respondido
    Dado que já respondi o formulário "Avaliação de Disciplina 2021.2" da turma "CIC0097 - TA"
    Quando acesso o formulário "Avaliação de Disciplina 2021.2" da turma "CIC0097 - TA" pelo endereço
    Então devo ser redirecionado para a página "Avaliações"
    E devo ver a mensagem "Você já respondeu este formulário"

  @triste
  Cenário: Tentar responder o formulário de uma turma em que não estou matriculada
    Dado que a turma "CIC0105 - TA" recebeu o formulário "Avaliação de Disciplina 2021.2"
    Quando acesso o formulário "Avaliação de Disciplina 2021.2" da turma "CIC0105 - TA" pelo endereço
    Então devo ser redirecionado para a página "Avaliações"
    E devo ver a mensagem "Você não participa desta turma"
```

### #109 — Visualização de formulários para responder

- **Arquivo:** `features/avaliacoes/formularios_pendentes.feature`
- **Pontos:** 2
- **Regras cobertas:** RN37, RN38

```gherkin
# language: pt
@issue-109
Funcionalidade: Ver os formulários que ainda não respondi
  Como participante de uma turma
  Quero ver os formulários que ainda não respondi nas turmas em que estou matriculado
  Para que eu possa escolher qual vou responder

  Contexto:
    Dado que a discente "Ana Souza" está matriculada nas turmas "CIC0097 - TA" e "CIC0105 - TA"
    E estou logado como a discente "Ana Souza"

  @feliz
  Cenário: Ver só os formulários pendentes das minhas turmas
    Dado que as turmas "CIC0097 - TA", "CIC0105 - TA" e "CIC0202 - TA" receberam o formulário "Avaliação de Disciplina 2021.2"
    E já respondi o formulário "Avaliação de Disciplina 2021.2" da turma "CIC0105 - TA"
    Quando acesso a página "Avaliações"
    Então devo ver 1 formulário pendente
    E devo ver o card do formulário da turma "CIC0097 - TA" com a matéria "BANCOS DE DADOS" e o semestre "2021.2"
    Mas não devo ver o formulário "Avaliação de Disciplina 2021.2" da turma "CIC0105 - TA"
    E não devo ver o formulário "Avaliação de Disciplina 2021.2" da turma "CIC0202 - TA"

  @triste
  Cenário: Nenhum formulário pendente
    Dado que já respondi todos os formulários das minhas turmas
    Quando acesso a página "Avaliações"
    Então devo ver a mensagem "Você não tem avaliações pendentes"
```

### #101 — Gerar relatório do administrador (CSV)

- **Arquivo:** `features/avaliacoes/relatorio_csv.feature`
- **Pontos:** 3
- **Regras cobertas:** RN13, RN14, RN15

```gherkin
# language: pt
@issue-101
Funcionalidade: Baixar o relatório de respostas em CSV
  Como administrador
  Quero baixar um arquivo CSV com as respostas de um formulário
  Para que eu consiga avaliar o desempenho das turmas

  Contexto:
    Dado que estou logado como administrador
    E a turma "CIC0097 - TA" recebeu o formulário "Avaliação de Disciplina 2021.2" com as questões:
      | número | tipo  | texto                                  | opções                     | obrigatória |
      | 1      | Radio | O professor explicou bem o conteúdo?   | Concordo; Neutro; Discordo | sim         |
      | 2      | Texto | Deixe um comentário sobre a disciplina |                            | não         |

  @feliz
  Cenário: Baixar o CSV de um formulário com respostas
    Dado que o formulário da turma "CIC0097 - TA" recebeu as respostas:
      | questão 1 | questão 2        |
      | Concordo  | Aulas muito boas |
      | Discordo  |                  |
    E estou na página "Gerenciamento - Resultados"
    Quando clico em "Baixar CSV" no formulário da turma "CIC0097 - TA"
    Então devo receber um arquivo CSV com o cabeçalho "O professor explicou bem o conteúdo?;Deixe um comentário sobre a disciplina"
    E o arquivo deve ter 2 linhas de respostas
    E o arquivo não deve ter o nome nem a matrícula de quem respondeu

  @triste
  Cenário: Tentar baixar o CSV de um formulário sem respostas
    Dado que o formulário da turma "CIC0097 - TA" ainda não recebeu respostas
    E estou na página "Gerenciamento - Resultados"
    Quando clico em "Baixar CSV" no formulário da turma "CIC0097 - TA"
    Então devo ver a mensagem "Este formulário ainda não tem respostas"
    E nenhum arquivo deve ser baixado
```
