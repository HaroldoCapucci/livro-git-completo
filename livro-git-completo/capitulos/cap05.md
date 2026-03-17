```markdown'''
# Git e GitHub: Do Iniciante ao Profissional com VS Code

**Autor: Haroldo Capucci**

---

## Capítulo 5: Navegando pela História do Projeto

**Páginas estimadas:** 30  
**Tempo de leitura:** 75–95 minutos  
**Objetivos do capítulo:**  
- Visualizar o histórico de commits com `git log` e suas variações  
- Navegar entre diferentes versões do projeto usando `git checkout` e `git switch`  
- Comparar mudanças entre commits, branches e arquivos com `git diff`  
- Corrigir erros com `git commit --amend` e `git restore`  
- Utilizar a interface gráfica do VS Code para explorar o histórico  

---

## 5.1 Introdução

No capítulo anterior, você aprendeu a criar repositórios, fazer commits e entender o ciclo de vida dos arquivos. Agora é hora de explorar o **histórico** do projeto – uma das funcionalidades mais poderosas do Git.

Saber navegar pela história permite:
- Entender a evolução do código  
- Encontrar quando e por que uma determinada mudança foi feita  
- Comparar versões para depurar problemas  
- Voltar a um estado anterior caso algo dê errado  

Neste capítulo, você dominará os comandos que tornam o Git uma verdadeira "máquina do tempo".

---

## 5.2 Visualizando o Histórico com `git log`

O comando `git log` é a porta de entrada para o histórico. Ele lista os commits em ordem cronológica reversa (do mais recente para o mais antigo).

### 5.2.1 Uso básico

```bash
git log
```

A saída padrão mostra, para cada commit:

· Hash (identificador único)
· Autor
· Data
· Mensagem

Pressione espaço para rolar para baixo, q para sair.

5.2.2 Visualizando de forma resumida

```bash
git log --oneline
```

Cada commit aparece em uma única linha com o hash abreviado e a mensagem. Exemplo:

```
a1b2c3d Adiciona validação de email
e4f5g6h Corrige bug no formulário
i7j8k9l Commit inicial
```

5.2.3 Exibindo estatísticas

```bash
git log --stat
```

Mostra, além da mensagem, quais arquivos foram alterados e quantas linhas foram adicionadas/removidas.

5.2.4 Visualizando o gráfico de branches

```bash
git log --graph --oneline --all
```

Essa combinação mágica desenha um gráfico ASCII mostrando a relação entre branches e merges. É uma das visualizações mais úteis.

5.2.5 Filtros úteis

· Por autor: git log --author="Haroldo"
· Por data: git log --since="2 weeks ago" ou --until="2023-12-01"
· Por mensagem: git log --grep="bugfix" (busca na mensagem)
· Por arquivo: git log -- README.md (histórico de um arquivo específico)

5.2.6 Formatação personalizada

Você pode criar seu próprio formato com --pretty=format:

```bash
git log --pretty=format:"%h - %an, %ar : %s"
```

Os placeholders comuns:

· %h – hash abreviado
· %an – author name
· %ar – data relativa ("2 dias atrás")
· %s – assunto (mensagem)

5.2.7 Exercício prático 5.1

No repositório que você criou no capítulo anterior, faça alguns commits extras (pelo menos 5) com mensagens variadas. Depois execute:

· git log --oneline
· git log --graph --oneline
· git log --author="seu nome"
· git log --grep="feat" (se tiver usado essa palavra)

---

5.3 Navegando entre Commits com git checkout e git switch

5.3.1 Movendo o ponteiro HEAD

O Git mantém um ponteiro especial chamado HEAD que indica onde você está no momento (qual commit ou branch está "checkoutado").

Para viajar para um commit específico, use:

```bash
git checkout <hash-do-commit>
```

Exemplo:

```bash
git checkout a1b2c3d
```

Após esse comando, você entra em estado "detached HEAD" – você não está em nenhuma branch, mas sim em um commit específico. Pode explorar o projeto como estava naquele momento.

5.3.2 Retornando para a branch principal

Para voltar ao estado normal (na branch main):

```bash
git checkout main
```

Ou, se usou switch (mais moderno):

```bash
git switch main
```

5.3.3 Diferença entre checkout e switch

O comando git checkout é versátil demais: serve tanto para trocar de branch quanto para restaurar arquivos. Por isso, versões recentes do Git introduziram git switch (focado em branches) e git restore (focado em arquivos), deixando o comando mais intuitivo.

Recomendação: Use git switch para mudar de branch e git restore para manipular arquivos. Mas git checkout ainda funciona e é amplamente usado.

5.3.4 Navegação segura

Quando você navega para um commit antigo, o diretório de trabalho reflete exatamente aquele snapshot. Você pode:

· Compilar/testar o código como era na época
· Criar uma nova branch a partir dali (git switch -c nova-branch)
· Simplesmente inspecionar e voltar

Importante: Se você fizer alterações enquanto estiver em detached HEAD, elas não pertencerão a nenhuma branch. Se quiser salvá-las, crie uma nova branch antes de voltar.

5.3.5 Exercício prático 5.2

1. No seu repositório, execute git log --oneline e escolha um commit antigo (não o mais recente).
2. Use git checkout <hash> para ir até ele.
3. Execute git status – note a mensagem "detached HEAD".
4. Explore os arquivos (estão como eram naquele momento).
5. Volte para main com git switch main.

---

5.4 Comparando Mudanças com git diff

O git diff mostra as diferenças entre versões de arquivos.

5.4.1 Diferenças entre working directory e staging

```bash
git diff
```

Mostra as linhas modificadas nos arquivos que ainda não foram adicionados ao staging.

5.4.2 Diferenças entre staging e último commit

```bash
git diff --staged
```

Mostra o que será enviado no próximo commit (o que está no staging).

5.4.3 Diferenças entre dois commits

```bash
git diff <hash1> <hash2>
```

Exibe as mudanças entre dois commits específicos. A ordem importa: o que mudou de hash1 para hash2.

5.4.4 Diferenças entre branches

```bash
git diff branch1..branch2
```

Mostra o que há em branch2 que não está em branch1.

5.4.5 Diferenças em um arquivo específico

```bash
git diff -- README.md
```

Limita a comparação a um único arquivo.

5.4.6 Ferramentas visuais

Se configurou uma ferramenta de diff (como no capítulo 2), use:

```bash
git difftool
```

Isso abrirá a ferramenta visual configurada (ex: VS Code, Meld).

5.4.7 Exercício prático 5.3

1. Modifique um arquivo no seu repositório (adicione uma linha).
2. Execute git diff e veja a saída.
3. Adicione o arquivo ao staging (git add).
4. Execute git diff --staged – agora você vê as mudanças que estão prontas para commit.
5. Faça um commit.
6. Compare o commit atual com o anterior usando git diff HEAD^ HEAD (HEAD^ significa o commit anterior).

---

5.5 Corrigindo Erros: git commit --amend e git restore

5.5.1 Alterando o último commit

Às vezes você esquece de incluir um arquivo ou digita a mensagem errada. O comando --amend permite corrigir o commit mais recente.

```bash
git add arquivo-esquecido.txt
git commit --amend
```

Isso abre o editor para que você possa modificar a mensagem. Se quiser manter a mensagem original:

```bash
git commit --amend --no-edit
```

Cuidado: Só use --amend em commits que ainda não foram enviados para o remoto (push). Se já tiver enviado, reescrever o histórico pode causar problemas para quem já baixou.

5.5.2 Desfazendo alterações no working directory

Se você modificou um arquivo mas quer descartar as alterações (voltar ao estado do último commit):

```bash
git restore arquivo.txt
```

Antes do Git 2.23, usava-se git checkout -- arquivo.txt. O restore é mais explícito.

5.5.3 Removendo arquivos do staging

Se você adicionou um arquivo ao staging por engano:

```bash
git restore --staged arquivo.txt
```

O arquivo volta para modified (as alterações permanecem, mas não estão mais marcadas para commit).

5.5.4 Desfazendo commits com git reset (cuidado!)

O git reset pode mover o ponteiro da branch para trás, efetivamente "desfazendo" commits. Existem três modos:

· --soft: mantém as alterações no staging
· --mixed (padrão): mantém as alterações no working directory, mas não no staging
· --hard: descarta completamente as alterações (perigoso!)

Exemplo: voltar um commit, mantendo as alterações no working directory:

```bash
git reset HEAD~1
```

Atenção: git reset reescreve o histórico. Use apenas em commits locais (não enviados).

5.5.5 Exercício prático 5.4

1. Faça um commit com uma mensagem errada (ex: "corrige tudo").
2. Corrija a mensagem com git commit --amend -m "Mensagem correta".
3. Crie um arquivo temporário, adicione ao staging e depois desfaça o staging com git restore --staged.
4. Modifique um arquivo e depois descarte as alterações com git restore.

---

5.6 Visualizando Detalhes com git show

O comando git show exibe informações detalhadas sobre um objeto (commit, tag, árvore).

```bash
git show <hash>
```

Mostra:

· Metadados do commit (autor, data, mensagem)
· As alterações (diff) introduzidas por aquele commit

Sem argumento, git show mostra o commit atual.

Útil para inspecionar um commit específico sem precisar navegar até ele.

---

5.7 Git Inside VS Code – Navegação Visual

O VS Code oferece uma interface gráfica poderosa para explorar o histórico.

5.7.1 Abrindo a timeline

Na barra lateral, clique no ícone do Git (ou Ctrl+Shift+G). Você verá:

· Changes – arquivos modificados
· Staged Changes – arquivos prontos para commit
· Commits – histórico (se você tiver extensões como GitLens)

5.7.2 Extensão GitLens

Recomendada no capítulo 2, o GitLens adiciona:

· Blame inline: mostra quem modificou cada linha e quando
· Explorador de commits: navegue pela história com um clique
· Comparação visual: diff lado a lado de qualquer commit

5.7.3 Comparando versões no VS Code

Clique com o botão direito em um arquivo e escolha "Select for Compare" e depois "Compare with Selected" para comparar duas versões.

5.7.4 Timeline nativa

O VS Code possui uma linha do tempo integrada (Timeline) que mostra eventos como commits e salvamentos. Acesse pela guia "Timeline" na parte inferior do explorador.

---

5.8 Boas Práticas com Mensagens de Commit

Embora não seja um comando, a qualidade das mensagens de commit afeta diretamente a navegabilidade do histórico.

5.8.1 Convenção Conventional Commits

```
<tipo>[escopo opcional]: <descrição>

[corpo opcional]

[rodapé opcional]
```

Tipos comuns: feat, fix, docs, style, refactor, test, chore.

Exemplo:

```
feat(auth): adiciona validação de email no cadastro

Implementa verificação de formato de email usando regex.
Previne cadastros com emails inválidos.

Closes #123
```

5.8.2 Dicas

· Primeira linha até 50 caracteres
· Corpo com quebra de linha a cada 72 caracteres
· Use imperativo: "Adiciona" em vez de "Adicionou"
· Explique o porquê, não o como (o código já mostra o como)

---

5.9 Exercícios de Fixação

1. Qual comando mostra o histórico em uma única linha por commit?
2. Como você faz para ver as diferenças entre o staging e o último commit?
3. Explique o que é "detached HEAD" e como você entra nesse estado.
4. Qual a diferença entre git restore e git restore --staged?
5. Como você altera a mensagem do último commit sem criar um novo commit?
6. Crie um alias git lg que mostre o log com gráfico, em uma linha, com cores (log --graph --oneline --all).
7. No VS Code, usando GitLens, encontre quem modificou uma linha específica de um arquivo.
8. (Desafio) Pesquise sobre git reflog e descreva sua utilidade (veremos no capítulo 11, mas é interessante conhecer).

---

5.10 Resumo do Capítulo

· git log é a ferramenta principal para ver o histórico, com inúmeras variações (--oneline, --graph, --author, etc.).
· Navegamos entre commits com git checkout (ou git switch), entrando em detached HEAD.
· git diff compara working directory, staging e commits.
· Corrigimos erros com git commit --amend, git restore (arquivos) e git restore --staged (staging).
· git show exibe detalhes de um commit.
· O VS Code, com extensões, oferece navegação visual poderosa.

Agora você sabe viajar no tempo com Git. No próximo capítulo, mergulharemos no universo das branches – a verdadeira magia do Git.

---

5.11 Referências

· Pro Git Book – Capítulo 2: "Git Basics – Viewing the Commit History"
· Documentação oficial: git help log, git help diff, git help restore
· Conventional Commits: https://www.conventionalcommits.org
· GitLens documentation

```

---

## 📦 Status atual do livro

| Capítulo | Título | Status |
|----------|--------|--------|
| 1 | Introdução ao Controle de Versão | ✅ Concluído |
| 2 | Instalação e Configuração Inicial | ✅ Concluído |
| 3 | Autenticação Segura com GitHub | ✅ Concluído |
| 4 | Primeiros Passos com Repositórios | ✅ Concluído (entregue anteriormente) |
| 5 | Navegando pela História do Projeto | ✅ Concluído (acabou de ser entregue) |
| 6 | Trabalhando com Branches | Pendente |
| 7 | Markdown para Documentação | Pendente |
| ... | ... | ... |
