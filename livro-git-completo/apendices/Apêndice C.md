```markdown
# Git e GitHub: Do Iniciante ao Profissional com VS Code

**Autor: Haroldo Capucci**

---

## Apêndice C: Guia de Boas Práticas para Nomes de Branches e Commits

**Páginas estimadas:** 6  
**Objetivo:** Estabelecer convenções e boas práticas para manter a organização e legibilidade do histórico, facilitando o trabalho em equipe e a revisão de código.

---

### C.1 Por que padronizar?

Em projetos colaborativos, a consistência é fundamental. Quando todos seguem as mesmas convenções para nomear branches e escrever mensagens de commit, o histórico se torna autoexplicativo, a navegação fica mais fácil e a integração com ferramentas automáticas (como geradores de changelog) é simplificada.

---

### C.2 Nomes de Branches

#### C.2.1 Estrutura recomendada

Uma branch deve ter um nome descritivo, curto e que indique seu propósito. Formatos comuns:

```

<tipo>/<descrição-curta>
<id-da-issue>-<descrição-curta>
<iniciais-do-autor>/<descrição>

```

**Tipos comuns:**
- `feature/` – nova funcionalidade  
- `bugfix/` – correção de bug  
- `hotfix/` – correção urgente em produção  
- `release/` – preparação de release  
- `docs/` – alterações na documentação  
- `refactor/` – refatoração de código  
- `test/` – adição ou correção de testes  
- `chore/` – tarefas de manutenção (build, dependências, etc.)

**Exemplos:**
- `feature/autenticacao-google`
- `bugfix/correcao-login-123`
- `hotfix/critical-security-patch`
- `docs/atualiza-readme`
- `refactor/otimiza-consultas`

#### C.2.2 Boas práticas

- Use letras minúsculas e hífens para separar palavras (kebab-case).  
- Seja conciso, mas claro: `feature/adiciona-botao` em vez de `feature/abc`.  
- Inclua o número da issue quando relevante: `bugfix/123-corrige-login`.  
- Evite caracteres especiais como `@`, `#`, `$`, `%`.  
- Após mesclar a branch, delete-a (local e remotamente) para manter o repositório limpo.

#### C.2.3 Exemplos de nomes ruins e bons

| Ruim | Bom |
|------|-----|
| `minhas-alteracoes` | `feature/novo-cabecalho` |
| `fix` | `bugfix/123-corrige-erro-validacao` |
| `nova-branch` | `hotfix/seguranca-sql-injection` |
| `teste123` | `test/adiciona-tests-unitarios` |

---

### C.3 Mensagens de Commit

#### C.3.1 O padrão Conventional Commits

O formato mais aceito atualmente é o **Conventional Commits** , que estrutura a mensagem em:

```

<tipo>(escopo opcional): <descrição curta>

[corpo opcional]

[rodapé opcional]

```

**Tipos principais:**
- `feat`: nova funcionalidade  
- `fix`: correção de bug  
- `docs`: documentação  
- `style`: formatação (espaços, ponto-e-vírgula, etc.) – não altera código  
- `refactor`: refatoração sem mudar comportamento  
- `perf`: melhoria de performance  
- `test`: adiciona ou corrige testes  
- `chore`: tarefas de build, dependências, etc.

**Escopo opcional:** indica o módulo afetado (ex: `feat(auth): adiciona validação de token`).

**Descrição:** deve ser curta (até 50 caracteres), em imperativo, começando com letra minúscula e sem ponto final.

**Exemplos:**
```

feat: adiciona botão de login na página inicial
fix(api): corrige timeout na requisição de dados
docs: atualiza README com instruções de instalação
style: remove espaços extras no arquivo CSS
refactor: extrai função de validação para módulo separado
test: adiciona testes para o componente de formulário
chore: atualiza dependências do projeto

```

#### C.3.2 Corpo da mensagem

Quando necessário, o corpo deve explicar o **porquê** da mudança, não o **como** (o código já mostra o como). Use quebras de linha a cada 72 caracteres.

Exemplo:
```

fix: corrige erro ao salvar usuário sem email

O erro ocorria porque o campo email estava sendo validado
mesmo quando não era obrigatório. Agora a validação só ocorre
se o email for fornecido.

Closes #123

```

#### C.3.3 Rodapé

Pode conter referências a issues (`Closes #123`, `Fixes #456`) ou notas de breaking change (`BREAKING CHANGE: a API de login foi modificada`).

#### C.3.4 Regras de ouro

1. **Primeira linha até 50 caracteres.**  
2. **Maiúscula?** Não, a primeira palavra deve ser minúscula (exceto se for um nome próprio).  
3. **Ponto final?** Não, a primeira linha não deve ter ponto final.  
4. **Imperativo:** "Adiciona" em vez de "Adicionado" ou "Adicionando".  
5. **Separe o corpo da primeira linha com uma linha em branco.**  

#### C.3.5 Exemplos de commits ruins e bons

| Ruim | Bom |
|------|-----|
| `alteracoes no codigo` | `feat: adiciona validação de email no cadastro` |
| `corrigi bug` | `fix: resolve erro 500 ao logar com senha inválida` |
| `atualiza docs` | `docs: adiciona exemplo de uso da API no README` |
| `mudancas` | `refactor: simplifica lógica do loop de iteração` |

#### C.3.6 Commit atômico

Cada commit deve representar uma **única mudança lógica**. Evite misturar correções de bug com novas funcionalidades no mesmo commit. Isso facilita o entendimento, o revert e a revisão.

---

### C.4 Convenções para Pull Requests

#### C.4.1 Título do PR

Siga o mesmo padrão dos commits: um título claro que resuma a contribuição.

#### C.4.2 Descrição do PR

Use um template, se disponível. Inclua:

- **Motivação:** por que a mudança é necessária?  
- **O que foi feito:** resumo das alterações.  
- **Como testar:** passos para validar.  
- **Checklist:** confirmação de que as diretrizes foram seguidas.  
- **Issues relacionadas:** `Closes #123`, `Relacionado a #456`.

#### C.4.3 Exemplo

```markdown
## Descrição
Adiciona a funcionalidade de recuperação de senha via e-mail.

## Motivação
Usuários estavam sem conseguir redefinir a senha quando esqueciam.

## Como testar
1. Acesse a página de login.
2. Clique em "Esqueci minha senha".
3. Informe um e-mail cadastrado.
4. Verifique se o e-mail de recuperação é enviado.

## Checklist
- [x] Testes unitários passando
- [x] Documentação atualizada
- [x] Código segue as diretrizes do projeto

Closes #789
```

---

C.5 Versionamento Semântico (SemVer)

Use tags para marcar versões seguindo o padrão vMAIOR.MENOR.PATCH:

· MAIOR: quando há mudanças incompatíveis (breaking changes).
· MENOR: quando há novas funcionalidades compatíveis.
· PATCH: quando há correções de bugs compatíveis.

Exemplos: v1.0.0, v1.2.3, v2.1.0.

---

C.6 Git Flow e GitHub Flow

C.6.1 Git Flow

Branches principais: main (produção), develop (integração).
Branches de suporte: feature/*, release/*, hotfix/*.

C.6.2 GitHub Flow

Mais simples: branch main sempre pronta para deploy. Para cada nova funcionalidade, crie uma branch descritiva, faça PR, após aprovação mescle em main.

Escolha o que se adapta à sua equipe.

---

C.7 Boas Práticas Gerais

· Proteja a branch main: exija revisão de PR e status checks.
· Não force push em branches compartilhadas: use --force-with-lease se estritamente necessário.
· Sincronize seu fork regularmente com o upstream.
· Use .gitignore adequado para evitar commitar arquivos desnecessários.
· Prefira rebase em branches locais para manter histórico limpo, mas merge em branches públicas.
· Documente as convenções no arquivo CONTRIBUTING.md do repositório.

---

C.8 Checklist de Boas Práticas

· Nome da branch segue o padrão tipo/descrição.
· Mensagem de commit segue Conventional Commits.
· Commit é atômico (uma mudança lógica).
· Testes passam localmente.
· Código segue o estilo do projeto (linters).
· Documentação atualizada (README, wiki, etc.).
· PR tem título e descrição claros.
· PR referencia a issue correspondente.
· Branch foi deletada após merge.

---

C.9 Exercícios de Fixação

1. Qual o formato recomendado para nomes de branches? Dê três exemplos.
2. Escreva uma mensagem de commit seguindo o padrão Conventional Commits para a adição de uma nova rota na API.
3. Por que é importante manter commits atômicos?
4. O que deve constar na descrição de um Pull Request?
5. Qual a diferença entre feat, fix e docs nos tipos de commit?
6. Crie um exemplo de rodapé de commit que fecha uma issue de número 456.
7. O que significa v2.1.3 em versionamento semântico?
8. Liste três coisas que você deve evitar ao nomear uma branch.
9. (Desafio) No seu repositório do livro, crie um arquivo CONTRIBUTING.md com as diretrizes de boas práticas que você aprendeu.

---

C.10 Referências

· Conventional Commits: https://www.conventionalcommits.org
· Semantic Versioning: https://semver.org
· Git Flow: https://nvie.com/posts/a-successful-git-branching-model/
· GitHub Flow: https://guides.github.com/introduction/flow/
· Pro Git Book – Capítulo sobre contribuição

```