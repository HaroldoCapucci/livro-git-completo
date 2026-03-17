
# Capítulo 4: Primeiros Passos com Repositórios

**Páginas estimadas: 28**  
**Tempo de leitura:** 60-90 minutos  
**Pré-requisitos:** Git instalado, VS Code configurado (Capítulos 2 e 3)

---

## 4.1 Introdução: O Coração do Git

Imagine que você está construindo uma casa. Você não começa levantando paredes sem antes preparar o terreno e fazer a fundação, certo? No universo do Git, o **repositório** é exatamente isso: a fundação de todo o projeto.

Um repositório Git (ou "repo") é como um "escritório mágico" que fica vigiando todas as pastas e arquivos do seu projeto. Ele não apenas guarda os arquivos, mas **registra cada alteração feita ao longo do tempo**, permitindo que você volte a qualquer momento anterior como se fosse uma máquina do tempo.

Neste capítulo, você vai aprender a criar esse "escritório mágico" de duas formas:
1. **Criando do zero** (`git init`) - quando você está começando um projeto novo
2. **Clonando um existente** (`git clone`) - quando quer trabalhar em algo que já existe (no GitHub, por exemplo)

Vamos também explorar o ciclo de vida dos arquivos dentro desse repositório e os comandos fundamentais que você usará centenas de vezes: `status`, `add` e `commit`.

---

## 4.2 Criando um Repositório do Zero: `git init`

### 4.2.1 O Comando Mágico

O comando `git init` é o ponto de partida. Ele transforma uma pasta comum do seu computador em um repositório Git. É como dizer: "A partir de agora, quero que o Git monitore tudo o que acontecer aqui dentro".

**Sintaxe básica:**
```bash
git init
```

4.2.2 Mão na Massa: Seu Primeiro Repositório

Vamos criar nosso primeiro projeto. Siga cada passo no seu computador:

Passo 1: Abra o terminal (ou Git Bash no Windows)

Passo 2: Crie uma pasta para o projeto e entre nela:

```bash
mkdir meu-primeiro-repo
cd meu-primeiro-repo
```

Passo 3: Inicialize o repositório:

```bash
git init
```

Resposta esperada:

```
Initialized empty Git repository in /caminho/para/meu-primeiro-repo/.git/
```

Passo 4: Veja o que aconteceu:

```bash
ls -la
```

Você notará uma pasta nova chamada .git. Ela é o "coração" do repositório. Nunca mexa nela manualmente a menos que saiba exatamente o que está fazendo. É lá que o Git guarda todo o histórico, configurações e metadados.

4.2.3 O que Acontece nos Bastidores?

Quando você executa git init, o Git:

1. Cria a subpasta .git
2. Dentro dela, prepara estruturas para:
   · objects/ – Onde os arquivos e commits são armazenados
   · refs/ – Onde as branches e tags são registradas
   · HEAD – Um arquivo que indica em qual branch você está
   · config – Configurações específicas deste repositório
   · description – Usado apenas por programas gráficos

Curiosidade: Você pode ter repositórios Git dentro de outras pastas que também são repositórios? Sim, mas isso é avançado (submódulos) e veremos em capítulos futuros.

4.2.4 Inicializando com Nome da Branch Diferente

Desde outubro de 2020, o GitHub mudou o nome padrão da branch principal de master para main. Se você quiser que seu repositório local já comece com main:

```bash
git init -b main
```

Ou, se já inicializou, pode renomear depois:

```bash
git branch -m master main
```

4.2.5 Exercício Prático 4.1

Crie três pastas diferentes (projeto-a, projeto-b, projeto-c) e inicialize repositórios em cada uma. Em seguida, liste o conteúdo de cada pasta para ver a pasta .git. Depois, remova os repositórios com rm -rf .git dentro de cada pasta (cuidado: isso apaga todo o histórico, mas mantém os arquivos).

---

4.3 Clonando um Repositório Existente: git clone

4.3.1 Quando Usar o Clone

O git clone é usado quando você quer copiar um repositório que já existe – geralmente em um servidor remoto como GitHub, GitLab ou Bitbucket – para o seu computador.

É como "baixar" o projeto, mas com um superpoder: você baixa tudo, inclusive todo o histórico de versões, todas as branches, todas as tags.

4.3.2 O Comando na Prática

Sintaxe:

```bash
git clone <url-do-repositorio>
```

Exemplo clonando um repositório real do GitHub:

```bash
git clone https://github.com/facebook/react.git
```

Isso criará uma pasta chamada react com todo o código fonte, histórico e configurações.

4.3.3 Clonando com Nome Diferente

Se quiser que a pasta local tenha um nome diferente do repositório original:

```bash
git clone https://github.com/facebook/react.git meu-react
```

Agora a pasta será meu-react, não react.

4.3.4 Protocolos de Clone: HTTPS vs. SSH

Você pode clonar usando dois protocolos principais:

Protocolo Exemplo Autenticação
HTTPS https://github.com/usuario/repo.git Usuário/senha ou token
SSH git@github.com:usuario/repo.git Chave SSH (mais seguro)

Recomendação: Use SSH se já configurou chaves (Capítulo 3). É mais seguro e você não precisa digitar senha toda vez.

4.3.5 O que Realmente Acontece num Clone?

Quando você executa git clone, o Git:

1. Cria uma nova pasta com o nome do repositório
2. Inicializa um repositório Git vazio dentro dela (git init)
3. Adiciona o repositório original como "remote" chamado origin
4. Busca (fetch) todos os objetos (commits, branches, tags) do remoto
5. Cria uma branch local apontando para a branch padrão do remoto (geralmente main ou master)
6. Dá checkout nessa branch, ou seja, baixa os arquivos para sua área de trabalho

4.3.6 Clonando Apenas o Último Commit (Shallow Clone)

Para repositórios enormes (como o Linux, com milhões de commits), você pode querer clonar apenas o histórico recente para economizar tempo e espaço:

```bash
git clone --depth 1 https://github.com/torvalds/linux.git
```

Isso baixa apenas o último commit. Mas atenção: você perde a capacidade de ver o histórico completo ou voltar a versões antigas.

4.3.7 Exercício Prático 4.2

1. Clone o repositório https://github.com/jlord/git-it-electron.git (um tutorial interativo de Git)
2. Entre na pasta clonada
3. Execute git log para ver o histórico
4. Execute git branch -a para ver todas as branches (locais e remotas)
5. Crie um clone raso (--depth 1) do mesmo repositório em outra pasta e compare o tamanho das pastas com du -sh

---

4.4 Entendendo a Área de Trabalho: Os Três Estados do Git

Um dos conceitos mais importantes – e que mais confunde iniciantes – é que o Git gerencia seus arquivos em três áreas principais. Visualize assim:

```
[Working Directory] <--> [Staging Area] <--> [Repositório Local]
      (sua pasta)          (index/área de preparo)    (.git/commits)
```

4.4.1 Working Directory (Árvore de Trabalho)

É simplesmente sua pasta do projeto, onde você edita arquivos, cria pastas, deleta coisas. É o que você vê no Explorer/Finder e no VS Code.

Estado: Os arquivos aqui podem estar "modificados" mas ainda não marcados para commit.

4.4.2 Staging Area (Área de Preparo / Index)

É uma área intermediária, como um "rascunho" do próximo commit. Aqui você seleciona quais alterações vão entrar no próximo snapshot.

Pense nisso como um palco: os artistas (arquivos modificados) ficam nos bastidores (working directory). Você escolhe quais sobem ao palco (staging area) para a apresentação (commit).

4.4.3 Repositório Local (Histórico / .git)

É onde o Git armazena permanentemente os commits. Cada commit é um snapshot completo do projeto naquele momento, com metadados (autor, data, mensagem).

4.4.4 Por Que Três Áreas?

Essa separação dá um poder imenso: você pode trabalhar em várias alterações diferentes, mas só commitar aquelas que estão prontas. Por exemplo:

· Você modificou 10 arquivos
· 5 são correções de bugs importantes
· 5 são experimentos ainda não testados

Com o staging, você pode adicionar apenas os 5 primeiros, commitar, e depois decidir o que fazer com os outros.

4.4.5 Fluxo Básico de Trabalho

1. Você modifica arquivos no Working Directory
2. Você adiciona alguns ao Staging Area
3. Você commita o que está no Staging para o Repositório Local

---

4.5 O Ciclo de Vida dos Arquivos

Cada arquivo no seu repositório pode estar em um de quatro estados:

```
                   +-------------+
                   |  Untracked  |
                   +-------------+
                          |
                          | (git add)
                          v
+-------------+     +-------------+     +-------------+
|  Unmodified | <--> |  Modified   | <--> |   Staged    |
+-------------+     +-------------+     +-------------+
      ^                                              |
      |              (commit)                        |
      +----------------------------------------------+
```

4.5.1 Untracked (Não Rastreado)

Arquivos que o Git não está monitorando. São novos na pasta e o Git não sabe se você quer versioná-los ou não.

Exemplo: Você acabou de criar README.md e o Git mostra como "untracked".

4.5.2 Unmodified (Não Modificado)

Arquivos que já estão no repositório e não foram alterados desde o último commit.

Exemplo: index.html depois que você fez commit e não tocou nele.

4.5.3 Modified (Modificado)

Arquivos rastreados que foram alterados, mas ainda não foram marcados para commit.

Exemplo: Você editou style.css mas não executou git add.

4.5.4 Staged (Preparado)

Arquivos modificados que você marcou para entrar no próximo commit.

Exemplo: Você executou git add style.css e agora ele aguarda o commit.

---

4.6 Comandos Essenciais: status, add, commit

Vamos colocar a mão na massa com os três comandos que você usará em 90% do tempo.

4.6.1 git status – O "Radar" do Git

O comando mais importante para iniciantes. Ele mostra exatamente:

· Em qual branch você está
· Quais arquivos foram modificados
· Quais estão no staging
· Quais não são rastreados

Crie um cenário prático:

```bash
# Dentro do seu repositório (meu-primeiro-repo)
echo "# Meu Projeto" > README.md
echo "console.log('Olá')" > app.js
git status
```

Saída esperada:

```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md
        app.js

nothing added to commit but untracked files present (use "git add" to track)
```

O Git está dizendo: "Olha, tem dois arquivos novos aqui, mas ainda não estou rastreando eles. Se quiser que eu comece a rastrear, use git add."

4.6.2 git add – Movendo para o Staging

O comando git add tem várias funções:

· Começar a rastrear arquivos untracked
· Marcar arquivos modified como staged
· Marcar arquivos removidos para o próximo commit

Sintaxes comuns:

```bash
# Adicionar um arquivo específico
git add README.md

# Adicionar vários arquivos
git add app.js style.css

# Adicionar todos os arquivos (cuidado!)
git add .

# Adicionar todos os arquivos .js
git add *.js

# Adicionar tudo (versão mais explícita)
git add -A
```

Aplique no nosso exemplo:

```bash
git add README.md
git status
```

Saída:

```
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        app.js
```

Agora README.md está "staged" (pronto para commit) e app.js continua untracked.

4.6.3 git commit – Tirando o Snapshot

O commit é o coração do Git. É como tirar uma foto do projeto naquele momento.

Sintaxe básica:

```bash
git commit -m "mensagem descritiva"
```

A mensagem é obrigatória e deve ser clara. Uma boa mensagem responde: "O que este commit faz?"

Exemplo:

```bash
git commit -m "Adiciona README inicial com título do projeto"
```

Saída:

```
[main (root-commit) a1b2c3d] Adiciona README inicial com título do projeto
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

Vamos analisar a saída:

· main – branch onde o commit foi feito
· a1b2c3d – os primeiros 7 caracteres do hash do commit (identificador único)
· 1 file changed, 1 insertion(+) – estatística: 1 arquivo alterado, 1 linha adicionada

Agora execute git status novamente:

```
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        app.js

nothing added to commit but untracked files present
```

O README.md sumiu da lista? Ele está "unmodified" agora, pois foi salvo no último commit.

4.6.4 Commit com Mensagem Multilinha

Para mensagens mais longas, use o comando sem -m para abrir o editor configurado:

```bash
git commit
```

Isso abre o editor (Vim, Nano, VS Code) onde você pode escrever:

· Primeira linha: título (até 50 caracteres)
· Linha em branco
· Corpo da mensagem (descrição detalhada)

4.6.5 Boas Práticas para Mensagens de Commit

Uma boa mensagem de commit segue convenções:

```
Tipo: Resumo curto (até 50 caracteres)

Corpo opcional explicando o que foi feito e por que, não como.
Pode ter várias linhas, com quebra de linha em 72 caracteres.
```

Tipos comuns:

· feat: – nova funcionalidade
· fix: – correção de bug
· docs: – documentação
· style: – formatação (espaços, ponto-e-vírgula, etc)
· refactor: – refatoração de código
· test: – testes
· chore: – tarefas de manutenção

Exemplo ruim:

```
git commit -m "alteracoes"
```

Exemplo bom:

```
git commit -m "feat: adiciona validação de email no formulário de cadastro"
```

4.6.6 Exercício Prático 4.3

1. No repositório meu-primeiro-repo, crie mais um arquivo: style.css com qualquer conteúdo
2. Use git status para ver os untracked files
3. Adicione app.js e style.css ao staging (git add app.js style.css)
4. Faça um commit com a mensagem "feat: adiciona scripts e estilos iniciais"
5. Modifique README.md (adicione uma linha, por exemplo)
6. Execute git status – agora README.md aparece como "modified"
7. Adicione a modificação ao staging e faça um novo commit

---

4.7 Visualizando Tudo no VS Code

O VS Code tem uma integração fantástica com Git. Você pode fazer quase tudo sem digitar comandos.

4.7.1 A Guia Controle de Código Fonte

Clique no ícone de branch na barra lateral esquerda (ou Ctrl+Shift+G).

Lá você verá:

· Changes – Arquivos modificados (working directory)
· Staged Changes – Arquivos preparados para commit

4.7.2 Fazendo Tudo pelo VS Code

Para adicionar ao staging: Passe o mouse sobre o arquivo e clique no "+" que aparece.

Para commitar: Digite a mensagem no campo superior e clique no "✔" (check) ou pressione Ctrl+Enter.

Para ver o status: Tudo é mostrado visualmente.

4.7.3 O Editor de Diff

Clique duas vezes em um arquivo modificado. O VS Code abre uma visualização "diff":

· Lado esquerdo: versão antiga (último commit)
· Lado direito: versão atual
· Linhas vermelhas: removidas
· Linhas verdes: adicionadas

4.7.4 Desfazendo Ações no VS Code

· Desfazer staging: clique no "-" ao lado do arquivo na área "Staged Changes"
· Descartar alterações: clique no ícone de "desfazer" (seta curvada) ao lado do arquivo em "Changes"

Atenção: Descartar alterações é permanente! Use com cuidado.

---

4.8 Ignorando Arquivos com .gitignore

4.8.1 Por que Ignorar Arquivos?

Nem tudo deve ser versionado:

· Arquivos de configuração local (com senhas)
· Pastas node_modules (podem ser recriadas com npm install)
· Arquivos compilados (.exe, .class, .pyc)
· Logs, caches, arquivos temporários
· Arquivos do sistema (.DS_Store no Mac)

4.8.2 Criando um .gitignore

Crie um arquivo chamado .gitignore na raiz do repositório. Dentro, liste padrões de arquivos/pastas a ignorar.

Exemplo básico:

```
# Dependências
node_modules/

# Arquivos compilados
*.exe
*.dll
*.so
*.dylib
*.class
*.pyc

# Logs e caches
logs/
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Sistema operacional
.DS_Store
Thumbs.db

# Ambiente
.env
.vscode/
```

4.8.3 Como Funciona?

· node_modules/ – ignora a pasta inteira
· *.log – ignora todos os arquivos terminados em .log
· !important.log – exclamação significa "não ignore este" (exceção)

4.8.4 Git Ignore Templates Prontos

O GitHub mantém uma coleção de templates para diferentes linguagens:
https://github.com/github/gitignore

Para um projeto Node.js, por exemplo, você pode baixar o template específico.

4.8.5 Verificando o que está sendo ignorado

```bash
git status --ignored
```

Mostra todos os arquivos ignorados.

4.8.6 Exercício Prático 4.4

1. No seu repositório, crie uma pasta logs/ e dentro dela um arquivo app.log
2. Crie um arquivo .gitignore com logs/ dentro
3. Execute git status – note que a pasta logs não aparece mais
4. Execute git status --ignored – agora você vê logs/ como ignorado
5. Commit o .gitignore

---

4.9 Removendo e Movendo Arquivos

4.9.1 Removendo Arquivos (git rm)

Se você simplesmente deletar um arquivo com rm arquivo.txt, o Git percebe a remoção, mas ela fica como "modified" (deleted). Você precisa adicionar essa remoção ao staging.

Forma correta de remover:

```bash
# Remove do sistema de arquivos e do staging
git rm arquivo.txt

# Se já tiver modificado e quiser remover mesmo assim (forçar)
git rm -f arquivo.txt

# Remove apenas do staging, mantendo o arquivo local (útil para .gitignore)
git rm --cached arquivo.txt
```

4.9.2 Movendo/Renomeando (git mv)

```bash
# Renomear
git mv antigo.txt novo.txt

# Mover para pasta
git mv arquivo.txt pasta/
```

Isso é equivalente a:

```bash
mv antigo.txt novo.txt
git add -A
```

4.9.3 Exercício Prático 4.5

1. Crie um arquivo teste.txt
2. Adicione e commite
3. Use git rm teste.txt
4. Execute git status – veja a remoção staged
5. Commit a remoção com git commit -m "remove arquivo teste"

---

4.10 Histórico de Comandos: Recap e Dicas

4.10.1 Comandos Aprendidos

Comando Função Uso comum
git init Cria repositório git init ou git init -b main
git clone Copia repositório remoto git clone URL
git status Mostra situação atual git status -s (resumido)
git add Prepara arquivos git add . ou git add arquivo
git commit Salva snapshot git commit -m "msg"
git rm Remove arquivos git rm arquivo
git mv Move/renomeia gitmv velho novo

4.10.2 Atalhos e Configurações Úteis

Crie atalhos (aliases) para comandos frequentes:

```bash
git config --global alias.s status
git config --global alias.c "commit -m"
git config --global alias.a "add ."
```

Agora você pode usar:

```bash
git s          # ao invés de git status
git c "mensagem"  # ao invés de git commit -m "mensagem"
git a          # ao invés de git add .
```

4.10.3 Flags Úteis para status

```bash
# Versão resumida (mais limpa)
git status -s

# Mostrar arquivos ignorados
git status --ignored

# Mostrar branch e informações curtas
git status -sb
```

4.10.4 Flags Úteis para commit

```bash
# Adiciona todos os arquivos modificados e já abre o editor
git commit -a

# Adiciona tudo e já passa a mensagem
git commit -am "mensagem"

# Altera o último commit (amend)
git commit --amend -m "nova mensagem"
```

Cuidado com --amend: Ele reescreve o histórico. Use apenas em commits que ainda não foram enviados para o remoto.

---

4.11 Problemas Comuns e Soluções

4.11.1 "fatal: not a git repository"

Você está tentando executar um comando Git fora de um repositório. Entre na pasta correta ou execute git init.

4.11.2 "nothing added to commit but untracked files present"

Você tem arquivos novos, mas não os adicionou ao staging. Use git add primeiro.

4.11.3 Esqueci de adicionar um arquivo no último commit

```bash
git add arquivo-esquecido.txt
git commit --amend --no-edit
```

Isso adiciona o arquivo ao commit anterior sem alterar a mensagem.

4.11.4 Quero desfazer o staging de um arquivo

```bash
git restore --staged arquivo.txt
```

Antes do Git 2.23, usava-se git reset HEAD arquivo.txt.

4.11.5 Quero desfazer as alterações de um arquivo (voltar ao último commit)

```bash
git restore arquivo.txt
```

Cuidado: Isso perde as alterações permanentemente.

4.11.6 Mensagem de commit errada

```bash
git commit --amend -m "mensagem correta"
```

4.11.7 Adicionei arquivos grandes demais

Se você acidentalmente adicionou um arquivo muito grande (e ainda não fez push), você pode removê-lo do histórico com git rm --cached e depois adicioná-lo ao .gitignore.

Para remover completamente do histórico (mais avançado), use git filter-branch ou a ferramenta BFG Repo-Cleaner.

---

4.12 Resumo do Capítulo

Neste capítulo, você aprendeu:

1. Criar repositórios com git init e git clone
2. Os três estados do Git: Working Directory, Staging Area, Repositório Local
3. O ciclo de vida dos arquivos: untracked, unmodified, modified, staged
4. Comandos essenciais: status, add, commit
5. Usar o VS Code para gerenciar versionamento visualmente
6. Ignorar arquivos com .gitignore
7. Remover e mover arquivos com git rm e git mv
8. Resolver problemas comuns do dia a dia

Você agora tem uma base sólida para começar a versionar seus projetos. No próximo capítulo, aprenderemos a navegar pelo histórico, comparar versões e viajar no tempo com git log, git diff, git checkout e outros comandos poderosos.

---

4.13 Exercícios de Fixação (Respostas no Apêndice D)

1. Qual comando transforma uma pasta comum em um repositório Git?
2. Explique a diferença entre Working Directory, Staging Area e Repositório Local.
3. O que significa um arquivo estar "untracked"?
4. Como você adiciona todos os arquivos .js ao staging?
5. Qual a diferença entre git commit -m e git commit sem a flag?
6. Por que é importante usar um arquivo .gitignore?
7. Como você desfaz o staging de um arquivo sem perder as alterações?
8. Qual comando baixa um repositório remoto para seu computador?
9. Como você vê arquivos ignorados pelo Git?
10. O que faz git commit --amend?

---

4.14 Referências e Leitura Recomendada

· Pro Git Book (2ª edição) - Capítulo 2: Git Basics
· Documentação oficial: git help init, git help clone
· GitHub Guides: "Getting started with Git"
· Visual Git Reference: https://marklodato.github.io/visual-git-guide/

```



