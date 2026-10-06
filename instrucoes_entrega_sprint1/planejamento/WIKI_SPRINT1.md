# CAMAAR — Sprint 1 (Grupo XX)

**Projeto:** CAMAAR, Sistema para avaliação de atividades acadêmicas remotas do CIC
**Disciplina:** Engenharia de Software (CIC/UnB)
**Repositório do grupo:** https://github.com/Luisserra99/CAMAAR (branch de entrega: `sprint-1`)

| Integrante | Matrícula |
|---|---|
| Daniel Dezan Baby | 232046097 |
| Leonardo Tome Sampaio | 222005448 |
| Luis Eduardo Curi Serra | 251033574 |
| Tarsila Marques de Oliveira Alves | 242012029 |
| Weldo Gonçalves da Silva Junior | 222014133 |

## Escopo do projeto

O CAMAAR é uma aplicação Ruby on Rails para a avaliação das turmas do CIC:

- **Administrador:**
  - importa do SIGAA as turmas, matérias e participantes;
  - cria templates de formulário;
  - envia formulários de avaliação para as turmas escolhidas;
  - acompanha os resultados e baixa as respostas em CSV.
- **Participantes (discentes e docentes):**
  - definem a senha pelo link recebido por e-mail;
  - entram no sistema e respondem os formulários pendentes das suas turmas.

Nesta sprint o grupo:
- estudou as 16 histórias de usuário (issues #98 a #113 do EngSwCIC/CAMAAR);
- entregou o relatório do modelo entidade-relacionamento;
- especificou em BDD (Cucumber) as 16 histórias, com cenários felizes e tristes.

Nada foi implementado ainda.

## Papéis

| Papel | Integrante |
|---|---|
| Scrum Master | Luis Eduardo Curi Serra |
| Product Owner | Weldo Gonçalves da Silva Junior |

## Funcionalidades, responsáveis e pontos

Pontos na escala de Fibonacci, estimando o esforço de implementar cada história (com testes) nas próximas sprints.

| Issue | Funcionalidade | Rótulo | Responsável | Pontos | Arquivo BDD |
|---|---|---|---|:-:|---|
| #98 | Importar dados do SIGAA | — | Weldo | 5 | `features/sigaa/importar_dados_sigaa.feature` |
| #100 | Cadastrar usuários do sistema | — | Weldo | 3 | `features/sigaa/cadastro_usuarios.feature` |
| #108 | Atualizar base de dados com os dados do SIGAA | — | Weldo | 3 | `features/sigaa/atualizar_dados_sigaa.feature` |
| #104 | Sistema de login | MVP | Luis | 3 | `features/autenticacao/login.feature` |
| #105 | Sistema de definição de senha | — | Luis | 3 | `features/autenticacao/definicao_senha.feature` |
| #107 | Redefinição de senha | Bônus | Luis | 3 | `features/autenticacao/redefinicao_senha.feature` |
| #102 | Criar template de formulário | MVP | Daniel | 5 | `features/templates/criar_template.feature` |
| #111 | Visualização dos templates criados | MVP | Daniel | 2 | `features/templates/visualizar_templates.feature` |
| #112 | Edição e deleção de templates | MVP | Daniel | 3 | `features/templates/editar_deletar_template.feature` |
| #103 | Criar formulário de avaliação | MVP | Leonardo | 3 | `features/formularios/criar_formulario.feature` |
| #106 | Gerenciamento por departamento | Bônus | Leonardo | 5 | cenários `@issue-106` em `criar_formulario` e `visualizar_resultados` |
| #110 | Visualização de resultados dos formulários | — | Leonardo | 2 | `features/formularios/visualizar_resultados.feature` |
| #113 | Formulário para docentes ou discentes | Bônus | Leonardo | 2 | `features/formularios/formulario_publico_alvo.feature` |
| #99 | Responder formulário | MVP | Tarsila | 5 | `features/avaliacoes/responder_formulario.feature` |
| #101 | Gerar relatório do administrador (CSV) | MVP | Tarsila | 3 | `features/avaliacoes/relatorio_csv.feature` |
| #109 | Visualização de formulários para responder | MVP | Tarsila | 2 | `features/avaliacoes/formularios_pendentes.feature` |
| | **Total** | | | **52** | |

### Velocity

| Sprint | Objetivo | Pontos planejados | Pontos concluídos |
|---|---|:-:|:-:|
| 1 | Modelo ER + especificação BDD das 16 histórias | — (sprint de especificação) | — |
| 2 | *a definir no planejamento da Sprint 2* | | |
| 3 | *a definir* | | |

Consideramos uma história concluída quando ela está implementada e os cenários BDD dela passam. Por isso a velocity começa a ser medida na Sprint 2. O backlog total é de **52 pontos**:
- **MVP:** 26 pontos;
- **sem rótulo:** 16 pontos;
- **bônus:** 10 pontos.

## Regras de negócio por funcionalidade

A numeração é a mesma das histórias e dos cenários BDD.

**#98 Importar dados do SIGAA**
- RN01: Só administradores importam dados. O botão "Importar dados" fica na página "Gerenciamento".
- RN02: Os dados vêm de `classes.json` (matérias e turmas) e `class_members.json` (participantes), no formato do SIGAA.
- RN03: Nada é duplicado:
  - matéria: identificada pelo código;
  - turma: pela matéria + código da turma + semestre;
  - usuário: pela matrícula (discente) ou pelo usuário do SIGAA (docente).
- RN04: A importação é "tudo ou nada". Com um arquivo mal formatado, um campo obrigatório faltando ou um participante de turma inexistente, nada é gravado e o sistema mostra o motivo.
- RN05: O departamento da matéria é o departamento do docente da turma.

**#100 Cadastrar usuários do sistema**
- RN10: O cadastro acontece na importação. Quem é novo é criado sem senha e recebe um e-mail com o link para definir a senha. Não existe tela de "cadastre-se".
- RN11: Quem já está cadastrado não recebe o e-mail de novo.
- RN12: O cadastro só é efetivado depois que o usuário define a senha. Antes disso ele não entra no sistema.

**#108 Atualizar base de dados com os dados do SIGAA**
- RN36: A atualização usa o mesmo botão "Importar dados".
  - O que mudou no SIGAA (nome, e-mail, horário, participantes novos) é atualizado sem duplicar.
  - Um arquivo com erro não altera nada.

**#104 Sistema de login**
- RN26: O login é feito com e-mail ou matrícula (para docentes, o usuário do SIGAA) e a senha.
- RN27: Os dois campos são obrigatórios. Quando o login falha, a mensagem é genérica e não diz qual dado está errado.
- RN28: A opção "Gerenciamento" só aparece no menu lateral para administradores, e as páginas de gerenciamento só abrem para eles.

**#105 Sistema de definição de senha**
- RN29: O link do e-mail vale por 48 horas e só pode ser usado uma vez.
- RN30: A senha tem no mínimo 8 caracteres, e a confirmação precisa ser igual.
- RN31: Não é preciso estar logado nem digitar o e-mail, porque o link identifica o usuário.

**#107 Redefinição de senha (bônus)**
- RN34: "Esqueci minha senha", na tela de login, envia um link de redefinição para o e-mail, com as mesmas regras de RN29 e RN30.
- RN35: A mensagem é a mesma para e-mail cadastrado ou não. Um e-mail em formato inválido é recusado.

**#102 Criar template de formulário**
- RN16: Só administradores criam templates.
- RN17: O nome é obrigatório, tem até 100 caracteres e não pode se repetir entre os templates do mesmo administrador.
- RN18: Toda questão tem um tipo (Radio ou Texto) e um texto.
- RN19: Uma questão Radio precisa de pelo menos 2 opções.
- RN20: O template pode ser salvo sem questões, mas assim não pode ser usado para criar formulário.

**#111 Visualização dos templates criados**
- RN41: A lista mostra só os templates do administrador logado, com as opções "Editar" e "Excluir".
- RN42: Sem templates, o sistema avisa e mostra a opção "Novo template".

**#112 Edição e deleção de templates**
- RN43: O administrador só edita ou exclui os templates que ele criou, com as mesmas validações da criação.
- RN44: Editar ou excluir um template não altera os formulários já criados com ele, porque as questões são copiadas para o formulário no envio.
- RN45: O template excluído some da lista e do envio de formulários.

**#103 Criar formulário de avaliação**
- RN21: O administrador escolhe o template, marca as turmas e clica em "Enviar". Não há campos para digitar.
- RN22: É criado um formulário por turma marcada, com uma cópia das questões do template.
- RN23: Template e pelo menos uma turma são obrigatórios.
- RN24: Um template sem questões não pode ser usado.
- RN25: Só aparecem as turmas do semestre atual, que é o mais recente importado.

**#106 Gerenciamento por departamento (bônus)**

Esta funcionalidade acrescenta regras às features de envio e de resultados.
- RN32: Um administrador que pertence a um departamento só vê e só envia formulários para turmas desse departamento.
- RN33: Ele também só vê os resultados das turmas do seu departamento.

**#113 Formulário para docentes ou discentes (bônus)**
- RN46: No envio, o administrador escolhe o público-alvo: "Discentes" (padrão) ou "Docentes".
- RN47: Só os participantes da turma com esse papel veem e respondem o formulário.

**#110 Visualização de resultados dos formulários**
- RN39: A página de resultados lista os formulários criados, com turma, semestre e quantidade de respostas.
- RN40: Sem formulários, o sistema avisa.

**#99 Responder formulário**
- RN06: Só responde quem participa da turma com o papel do público-alvo.
- RN07: Cada participante responde cada formulário uma única vez, sem poder alterar depois.
- RN08: As questões obrigatórias precisam ser respondidas.
- RN09: Respostas de texto têm no máximo 1000 caracteres.

**#109 Visualização de formulários para responder**
- RN37: A página "Avaliações" mostra só os formulários não respondidos das turmas do participante (e do seu papel), com matéria e semestre.
- RN38: Sem pendências, o sistema avisa.

**#101 Gerar relatório do administrador (CSV)**
- RN13: O CSV tem uma linha por resposta e uma coluna por questão, com separador `;`.
- RN14: O CSV não identifica quem respondeu.
- RN15: Um formulário sem respostas não gera CSV, e o sistema avisa.

## Política de branching

```
EngSwCIC/CAMAAR:main  ◄── PR único do grupo (Grupo XX - Sprint 1)
        ▲
Luisserra99/CAMAAR
  main ............ espelho do main do upstream (ninguém commita direto)
  sprint-1 ........ branch de entrega da sprint; recebe os merges das branches de tema
    ├─ feature/autenticacao   (Luis)
    ├─ feature/sigaa          (Weldo)
    ├─ feature/templates      (Daniel)
    ├─ feature/formularios    (Leonardo)
    └─ feature/avaliacoes     (Tarsila)
```

1. **Branch por integrante:** cada um cria `feature/<tema>` a partir da `sprint-1` e commita **os próprios** arquivos `.feature`.
2. **PR interno:** cada branch de tema volta para a `sprint-1` por um Pull Request **dentro do fork**, revisado por outro integrante. O merge é feito com *merge commit*, sem squash, para preservar a autoria de cada commit.
3. **PR de entrega:** com tudo na `sprint-1`, abrimos um único PR `Luisserra99/CAMAAR:sprint-1` → `EngSwCIC/CAMAAR:main`. A partir daí a `sprint-1` **não recebe mais commits**.
4. **Próximas sprints:** as branches `sprint-2` e `sprint-3` são criadas a partir da sprint anterior, com o mesmo fluxo.
5. **Mensagens de commit:** curtas, em português, citando a issue. Exemplo: `test(bdd): adiciona cenários de login (#104)`.

## Links

- Relatório do modelo ER: entregue no Aprender (`relatorio_sprint1.pdf`)
- Pull Request da Sprint 1: *(link do PR)*
- Histórias de usuário originais: https://github.com/EngSwCIC/CAMAAR/issues
