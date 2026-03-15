```markdown
# Git e GitHub: Do Iniciante ao Profissional com VS Code

**Autor: Haroldo Capucci**

---

## Apêndice A: Glossário Completo de Termos Git/GitHub

**Páginas estimadas:** 12  
**Objetivo:** Consulta rápida de todos os termos técnicos utilizados no livro, com definições claras e objetivas.

---

### A.1 Termos Gerais

**Branch (Ramificação)**
: Linha independente de desenvolvimento. Permite trabalhar em funcionalidades isoladas sem afetar a branch principal. Criar uma branch é instantâneo, pois é apenas um ponteiro para um commit.

**Clone**
: Cópia local de um repositório remoto. Inclui todo o histórico, branches e tags. Comando: `git clone <url>`.

**Commit**
: Snapshot do projeto em um determinado momento. Cada commit possui um hash único, autor, data e mensagem descritiva. É a unidade fundamental do histórico.

**Conflito (Conflict)**
: Ocorre quando duas branches alteram a mesma parte do mesmo arquivo de maneiras diferentes e o Git não consegue decidir automaticamente qual versão manter. Exige resolução manual.

**Detached HEAD**
: Estado em que o ponteiro HEAD não está em nenhuma branch, mas sim em um commit específico. Ocorre ao fazer checkout de um commit antigo. Alterações feitas nesse estado podem ser perdidas se não forem salvas em uma nova branch.

**Diff**
: Visualização das diferenças entre versões de arquivos. Pode comparar working directory, staging area, commits ou branches. Comando: `git diff`.

**Fork**
: Cópia de um repositório alheio para sua conta no GitHub. Permite modificar o código livremente e depois propor contribuições via Pull Request.

**HEAD**
: Ponteiro que indica onde você está no momento (qual commit ou branch está ativo). Geralmente aponta para a branch atual.

**Issue**
: Unidade de trabalho no GitHub, usada para relatar bugs, sugerir melhorias ou tarefas. Pode ser associada a labels, milestones e projetos.

**Merge**
: Integração de duas branches. Pode ser fast-forward (avanço linear) ou gerar um commit de merge (quando há divergência). Comando: `git merge <branch>`.

**Pull Request (PR)**
: Solicitação para que um mantenedor incorpore suas alterações (de um fork ou branch) ao repositório principal. Inclui discussão, revisão e, eventualmente, merge.

**Rebase**
: Reescreve a história aplicando commits de uma branch sobre outra, criando um histórico linear. Útil localmente, mas perigoso em branches compartilhadas.

**Reflog**
: Registro de todas as movimentações do HEAD no repositório local. Permite recuperar commits "perdidos" após operações destrutivas. Comando: `git reflog`.

**Remote (Remoto)**
: Repositório hospedado em outro local (ex: GitHub). Nomes comuns: `origin` (principal) e `upstream` (original, em forks).

**Repository (Repositório)**
: Pasta especial (contém subpasta `.git`) que armazena todos os arquivos, histórico e configurações do projeto versionado.

**Staging Area (Index)**
: Área intermediária onde os arquivos são preparados antes do commit. Permite escolher quais alterações farão parte do próximo snapshot. Comando: `git add`.

**Stash**
: Área temporária que guarda alterações não commitadas, permitindo mudar de branch ou limpar o working directory temporariamente. Comando: `git stash`.

**Tag**
: Marcador estático que aponta para um commit específico, usado geralmente para versões (v1.0, v2.1). Diferente de branch, não se move.

**Upstream**
: Termo usado para o repositório original em um fluxo de fork. Ex: `git remote add upstream <url-do-original>`.

**Working Directory (Árvore de Trabalho)**
: Diretório onde você edita os arquivos. É uma das três áreas do Git (junto com staging e repositório).

---

### A.2 Comandos Git (Resumo)

| Comando | Descrição |
|---------|-----------|
| `git init` | Inicializa um novo repositório local |
| `git clone <url>` | Clona um repositório remoto |
| `git status` | Mostra o estado dos arquivos (modificados, staged, etc.) |
| `git add <arquivo>` | Adiciona arquivo ao staging |
| `git commit -m "msg"` | Cria um commit com a mensagem fornecida |
| `git log` | Exibe o histórico de commits |
| `git log --oneline --graph` | Histórico resumido com gráfico |
| `git diff` | Mostra diferenças não staged |
| `git diff --staged` | Mostra diferenças entre staging e último commit |
| `git branch` | Lista branches locais |
| `git branch <nome>` | Cria nova branch |
| `git switch <branch>` | Troca para a branch especificada |
| `git switch -c <branch>` | Cria e troca para nova branch |
| `git merge <branch>` | Mescla a branch especificada na atual |
| `git rebase <branch>` | Reaplica commits da branch atual sobre outra |
| `git rebase -i HEAD~n` | Rebase interativo dos últimos n commits |
| `git remote add <nome> <url>` | Adiciona um repositório remoto |
| `git push <remote> <branch>` | Envia commits para o remoto |
| `git pull <remote> <branch>` | Baixa e integra alterações do remoto |
| `git fetch <remote>` | Baixa referências do remoto sem integrar |
| `git stash` | Guarda alterações temporariamente |
| `git stash pop` | Aplica e remove o stash mais recente |
| `git stash list` | Lista stashes salvos |
| `git tag <nome>` | Cria uma tag leve |
| `git tag -a <nome> -m "msg"` | Cria uma tag anotada |
| `git restore <arquivo>` | Descarta alterações no working directory |
| `git restore --staged <arquivo>` | Remove arquivo do staging |
| `git reset <commit>` | Move a branch para um commit anterior (modos: --soft, --mixed, --hard) |
| `git revert <commit>` | Cria um novo commit que desfaz as alterações de um commit anterior |
| `git bisect` | Busca binária para encontrar commit que introduziu bug |
| `git reflog` | Mostra o histórico de movimentações do HEAD |

---

### A.3 Termos GitHub

**Actions**
: Serviço de CI/CD integrado ao GitHub. Permite automatizar workflows (testes, deploy, etc.) baseados em eventos.

**Code Spaces**
: Ambiente de desenvolvimento na nuvem, integrado ao GitHub.

**Discussions**
: Fórum integrado ao repositório para conversas, perguntas e anúncios.

**Gist**
: Trechos de código ou notas versionadas, podendo ser públicos ou secretos.

**GitHub CLI (`gh`)**
: Ferramenta de linha de comando para interagir com o GitHub sem sair do terminal.

**GitHub Pages**
: Serviço de hospedagem de sites estáticos diretamente a partir de um repositório.

**Git LFS (Large File Storage)**
: Extensão para versionar arquivos grandes (vídeos, imagens, binários) de forma eficiente.

**Label**
: Rótulo usado para categorizar issues e pull requests (ex: bug, enhancement, good first issue).

**Milestone**
: Marco que agrupa issues e pull requests com um objetivo comum e data alvo.

**Organization**
: Conta corporativa que agrupa vários repositórios e membros, com permissões centralizadas.

**Project**
: Quadro Kanban integrado para planejamento e acompanhamento de tarefas.

**Release**
: Versão empacotada do projeto, associada a uma tag, com notas de versão e arquivos para download.

**Secret**
: Variável criptografada usada em Actions para armazenar senhas, tokens, etc.

**Sponsors**
: Programa de financiamento de desenvolvedores e projetos open source.

**Template**
: Modelo pré-definido para issues, pull requests ou até repositórios inteiros.

**Wiki**
: Espaço de documentação versionado, separado do código principal.

---

### A.4 Termos do VS Code para Git

| Termo | Descrição |
|-------|-----------|
| **Source Control** | Guia do VS Code que integra operações Git |
| **Timeline** | Painel que mostra eventos (commits, salvamentos) de um arquivo |
| **GitLens** | Extensão que amplia funcionalidades Git: blame inline, explorador, etc. |
| **Git Graph** | Extensão que exibe gráfico interativo de commits |
| **GitHub Pull Requests** | Extensão oficial para revisar PRs dentro do editor |
| **Inline Blame** | Anotação ao lado de cada linha mostrando quem modificou por último |

---

### A.5 Convenções e Padrões

**Conventional Commits**
: Padrão para mensagens de commit. Formato: `<tipo>(escopo): <descrição>` (ex: `feat: adiciona botão de login`). Tipos comuns: feat, fix, docs, style, refactor, test, chore.

**Git Flow**
: Fluxo de trabalho com branches específicas: `main`, `develop`, `feature/*`, `release/*`, `hotfix/*`.

**GitHub Flow**
: Fluxo simplificado: branch `main` sempre pronta para deploy; branches de feature; Pull Requests; merge.

**Semantic Versioning (SemVer)**
: Versionamento semântico: `vMAIOR.MENOR.PATCH` (ex: v2.1.3). MAIOR para mudanças incompatíveis, MENOR para novas funcionalidades compatíveis, PATCH para correções.

---

### A.6 Termos Relacionados a Autenticação

**HTTPS**
: Protocolo de autenticação que exige usuário e token (senha não é mais aceita no terminal do GitHub). Requer token pessoal.

**SSH**
: Protocolo seguro baseado em chaves pública/privada. Mais prático e seguro. Chave pública adicionada ao GitHub; chave privada fica no computador.

**Personal Access Token (PAT)**
: Token gerado no GitHub para autenticação via HTTPS. Substitui a senha. Pode ter escopos limitados.

**GPG Key**
: Chave usada para assinar commits, garantindo autenticidade. Commits assinados mostram selo "Verified" no GitHub.

---

### A.7 Termos de Colaboração

**Assignee**
: Pessoa responsável por uma issue ou pull request.

**Reviewer**
: Pessoa designada para revisar um Pull Request.

**Code Review**
: Processo de análise do código proposto em um PR, com comentários e sugestões.

**Merge Conflict**
: Ver "Conflito".

**Squash**
: Ação de combinar múltiplos commits em um só durante o merge de um PR.

**Upstream**
: Em forks, repositório original. Em outros contextos, repositório de origem.

---

### A.8 Exercícios de Fixação do Glossário

1. Defina, com suas palavras: branch, commit, merge e rebase.  
2. Qual a diferença entre `git fetch` e `git pull`?  
3. O que é um fork e em que contexto ele é usado?  
4. Explique o que significa "detached HEAD" e como sair desse estado.  
5. Qual a função do `git stash`? Dê um exemplo prático.  
6. O que são GitHub Actions e para que servem?  
7. Cite três tipos de labels comuns em issues.  
8. O que é um milestone?  
9. Qual a diferença entre HTTPS e SSH para autenticação no GitHub?  
10. O que significa o selo "Verified" em um commit?

---

### A.9 Referências do Glossário

- Pro Git Book (2ª edição) – Glossário oficial  
- GitHub Docs – Glossary  
- Conventional Commits – Site oficial  
- SemVer.org
```