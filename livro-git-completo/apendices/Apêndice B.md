``````markdown'''
# Git e GitHub: Do Iniciante ao Profissional com VS Code

**Autor: Haroldo Capucci**

---

## Apêndice B: Cheat Sheet de Comandos Git

**Páginas estimadas:** 8  
**Objetivo:** Consulta rápida com os principais comandos Git organizados por categoria.

---

### B.1 Configuração Inicial

| Comando | Descrição |
|---------|-----------|
| `git config --global user.name "Seu Nome"` | Configura nome do autor |
| `git config --global user.email "seu@email.com"` | Configura e-mail do autor |
| `git config --global core.editor "code --wait"` | Define VS Code como editor padrão |
| `git config --global init.defaultBranch main` | Define branch padrão como main |
| `git config --global alias.s status` | Cria atalho `git s` para status |
| `git config --global --list` | Lista todas as configurações |
| `git config --global credential.helper cache` | Cache de credenciais (15 min padrão) |

---

### B.2 Criando e Clonando Repositórios

| Comando | Descrição |
|---------|-----------|
| `git init` | Inicializa repositório local |
| `git init -b main` | Inicializa com branch main |
| `git clone <url>` | Clona repositório remoto |
| `git clone --depth 1 <url>` | Clona apenas o último commit (shallow clone) |

---

### B.3 Operações Básicas (Add, Commit, Status)

| Comando | Descrição |
|---------|-----------|
| `git status` | Mostra estado dos arquivos |
| `git status -s` | Versão resumida |
| `git add <arquivo>` | Adiciona arquivo ao staging |
| `git add .` | Adiciona todos os arquivos (cuidado) |
| `git add -p` | Adiciona interativamente por partes (hunks) |
| `git commit -m "mensagem"` | Cria commit com mensagem |
| `git commit -a -m "msg"` | Adiciona e commita em um passo (apenas arquivos rastreados) |
| `git commit --amend -m "nova msg"` | Altera último commit (mensagem ou inclusão) |
| `git rm <arquivo>` | Remove arquivo e prepara remoção |
| `git mv <origem> <destino>` | Move ou renomeia arquivo |

---

### B.4 Histórico e Navegação

| Comando | Descrição |
|---------|-----------|
| `git log` | Exibe histórico completo |
| `git log --oneline` | Histórico resumido (um commit por linha) |
| `git log --graph --oneline --all` | Gráfico de todas as branches |
| `git log --author="nome"` | Filtra por autor |
| `git log --grep="palavra"` | Busca na mensagem |
| `git log -- <arquivo>` | Histórico de um arquivo específico |
| `git show <commit>` | Detalhes de um commit |
| `git show <commit>:<arquivo>` | Conteúdo de um arquivo em um commit específico |
| `git diff` | Compara working directory com staging |
| `git diff --staged` | Compara staging com último commit |
| `git diff <commit1> <commit2>` | Compara dois commits |
| `git diff <branch1>..<branch2>` | Compara duas branches |

---

### B.5 Branches

| Comando | Descrição |
|---------|-----------|
| `git branch` | Lista branches locais |
| `git branch -a` | Lista todas (locais e remotas) |
| `git branch <nome>` | Cria nova branch (sem mudar) |
| `git switch <branch>` | Troca para branch existente |
| `git switch -c <branch>` | Cria e troca para nova branch |
| `git checkout -b <branch>` | Alternativa antiga para criar e trocar |
| `git branch -m <novo-nome>` | Renomeia branch atual |
| `git branch -d <branch>` | Deleta branch (se mesclada) |
| `git branch -D <branch>` | Força deleção (mesmo não mesclada) |
| `git merge <branch>` | Mescla branch na atual |
| `git merge --abort` | Aborta merge com conflito |
| `git rebase <branch>` | Reaplica commits da branch atual sobre outra |
| `git rebase -i HEAD~n` | Rebase interativo dos últimos n commits |
| `git rebase --continue` | Continua rebase após resolver conflitos |
| `git rebase --abort` | Aborta rebase |

---

### B.6 Stash (Trabalho Temporário)

| Comando | Descrição |
|---------|-----------|
| `git stash` | Guarda alterações não commitadas |
| `git stash push -m "mensagem"` | Stash com descrição |
| `git stash list` | Lista stashes |
| `git stash apply` | Aplica último stash (mantém na lista) |
| `git stash pop` | Aplica e remove da lista |
| `git stash drop` | Remove último stash |
| `git stash clear` | Remove todos os stashes |
| `git stash branch <branch>` | Cria branch a partir de stash |

---

### B.7 Repositórios Remotos

| Comando | Descrição |
|---------|-----------|
| `git remote -v` | Lista remotos com URLs |
| `git remote add <nome> <url>` | Adiciona novo remote |
| `git remote rename <antigo> <novo>` | Renomeia remote |
| `git remote remove <nome>` | Remove remote |
| `git push -u <remote> <branch>` | Envia branch e define upstream |
| `git push` | Envia para upstream configurado |
| `git push --force` | Força push (cuidado!) |
| `git push --force-with-lease` | Força push mais seguro |
| `git push origin --delete <branch>` | Deleta branch remota |
| `git pull` | Busca e mescla (fetch + merge) |
| `git pull --rebase` | Busca e faz rebase em vez de merge |
| `git fetch` | Busca referências sem mesclar |
| `git fetch --all` | Busca de todos os remotos |
| `git remote show <remote>` | Informações detalhadas do remote |

---

### B.8 Tags

| Comando | Descrição |
|---------|-----------|
| `git tag` | Lista tags |
| `git tag -a v1.0 -m "mensagem"` | Cria tag anotada |
| `git tag v1.0` | Cria tag leve |
| `git show v1.0` | Mostra detalhes da tag |
| `git push origin v1.0` | Envia tag específica para remoto |
| `git push origin --tags` | Envia todas as tags |
| `git tag -d v1.0` | Deleta tag local |
| `git push origin --delete v1.0` | Deleta tag remota |

---

### B.9 Desfazendo e Recuperando

| Comando | Descrição |
|---------|-----------|
| `git restore <arquivo>` | Descarta alterações no working directory |
| `git restore --staged <arquivo>` | Remove arquivo do staging |
| `git reset HEAD~1` | Remove último commit (mantém alterações) |
| `git reset --hard HEAD~1` | Remove último commit e alterações (perigoso) |
| `git revert <commit>` | Cria novo commit desfazendo o especificado |
| `git reflog` | Mostra movimentações do HEAD (para recuperar commits perdidos) |
| `git checkout <hash>` | Vai para commit específico (detached HEAD) |
| `git checkout <hash> -- <arquivo>` | Restaura arquivo de um commit antigo |

---

### B.10 Busca Binária (Bisect)

| Comando | Descrição |
|---------|-----------|
| `git bisect start` | Inicia sessão bisect |
| `git bisect good <commit>` | Marca commit como bom |
| `git bisect bad <commit>` | Marca commit como ruim |
| `git bisect reset` | Finaliza bisect |
| `git bisect run <script>` | Automatiza com script de teste |

---

### B.11 Submódulos

| Comando | Descrição |
|---------|-----------|
| `git submodule add <url> <caminho>` | Adiciona submódulo |
| `git submodule update --init --recursive` | Inicializa e atualiza submódulos após clone |
| `git submodule update --remote` | Atualiza submódulos para último commit |
| `git submodule foreach git pull` | Executa comando em cada submódulo |

---

### B.12 Git LFS (Large File Storage)

| Comando | Descrição |
|---------|-----------|
| `git lfs install` | Inicializa LFS no repositório |
| `git lfs track "*.psd"` | Rastreia arquivos .psd com LFS |
| `git lfs track` | Lista padrões rastreados |
| `git lfs ls-files` | Lista arquivos rastreados pelo LFS |

---

### B.13 GitHub CLI (gh)

| Comando | Descrição |
|---------|-----------|
| `gh auth login` | Autentica no GitHub |
| `gh repo create <nome>` | Cria repositório remoto |
| `gh repo clone <nome>` | Clona repositório |
| `gh pr create` | Cria Pull Request |
| `gh pr list` | Lista PRs |
| `gh pr checkout <numero>` | Checkout de PR localmente |
| `gh issue list` | Lista issues |
| `gh release create v1.0` | Cria release |

---

### B.14 VS Code Atalhos para Git

| Atalho | Ação |
|--------|------|
| `Ctrl+Shift+G` | Abre Source Control |
| `Ctrl+Enter` | Faz commit (com mensagem) |
| `Ctrl+Shift+G` seguido de `Ctrl+P` | Abre paleta de comandos Git |
| Clique na branch na barra inferior | Trocar/criar branch |
| Ícone de sincronização na barra inferior | Pull + Push |
| `Ctrl+Shift+V` | Preview Markdown |

---

### B.15 Resumo de Fluxo Diário

```bash
# Atualizar branch main
git switch main
git pull

# Criar branch para nova funcionalidade
git switch -c feature/nova

# Trabalhar, commitar, testar
git add .
git commit -m "feat: implementa nova funcionalidade"

# Enviar para remoto
git push -u origin feature/nova

# Abrir Pull Request (via GitHub ou gh)
gh pr create --fill

# Após merge, deletar branch local e remota
git switch main
git pull
git branch -d feature/nova
git push origin --delete feature/nova
```

---

B.16 Comandos Menos Usados, mas Úteis

Comando Descrição
git shortlog -sn Lista contribuidores e número de commits
git blame <arquivo> Mostra quem modificou cada linha e quando
git grep "palavra" Busca texto no repositório
git clean -fd Remove arquivos não rastreados (cuidado!)
git archive --format=zip HEAD > projeto.zip Cria arquivo zip do repositório
git cherry-pick <commit> Aplica um commit específico na branch atual

---

Dica: Use git help <comando> para acessar a documentação completa de qualquer comando diretamente no terminal.

```
