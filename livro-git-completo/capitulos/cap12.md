
# Git e GitHub: Do Iniciante ao Profissional com VS Code

**Autor: Haroldo Capucci**

---

## Capítulo 12: Git Inside VS Code – A Interface Gráfica

**Páginas estimadas:** 26  
**Tempo de leitura:** 65–85 minutos  
**Objetivos do capítulo:**  
- Conhecer a integração nativa do Git no VS Code  
- Navegar pela guia Controle de Código Fonte (Source Control)  
- Realizar operações comuns (commit, pull, push, branch) sem usar o terminal  
- Utilizar o editor de merge integrado para resolver conflitos visualmente  
- Explorar extensões que potencializam o Git (GitLens, Git History, Git Graph)  
- Configurar o VS Code para um fluxo Git eficiente  
- Aprender atalhos de teclado e dicas de produtividade  

---

## 12.1 Introdução

O Visual Studio Code se tornou um dos editores mais populares entre desenvolvedores, e uma das razões é sua excelente integração com Git. Embora o terminal seja poderoso, a interface gráfica do VS Code oferece uma maneira mais intuitiva e rápida de executar tarefas cotidianas, especialmente para quem está começando.

Neste capítulo, você aprenderá a usar todas as funcionalidades Git diretamente da interface do VS Code, desde o básico até operações mais avançadas, além de conhecer extensões que transformam o editor em uma verdadeira central de controle de versionamento.

---

## 12.2 Visão Geral da Guia Controle de Código Fonte

### 12.2.1 Acessando a guia

A guia **Source Control** (Controle de Código Fonte) é o coração da integração Git no VS Code. Você pode abri-la de três formas:

- Clique no ícone de branch na barra lateral esquerda (terceiro ícone, geralmente).  
- Use o atalho `Ctrl+Shift+G` (Windows/Linux) ou `Cmd+Shift+G` (macOS).  
- Através da paleta de comandos (`Ctrl+Shift+P`), digite "View: Show Source Control".

### 12.2.2 Layout da guia

A guia é dividida em seções:

1. **Changes (Alterações):** arquivos modificados no working directory (ainda não adicionados ao staging).  
2. **Staged Changes (Alterações preparadas):** arquivos que já foram adicionados (`git add`) e estão prontos para commit.  
3. **Merge Changes (Alterações de merge):** aparece apenas durante conflitos, listando os arquivos com conflitos.  
4. **Timeline (linha do tempo):** na parte inferior do explorador, mostra eventos como commits e salvamentos (não exclusivo do Git).

Cada arquivo listado pode ter ações representadas por ícones:

- `+` (ou `U`): adicionar ao staging (ou começar a rastrear).  
- `-` (ou `R`): remover do staging (reverter para modified).  
- `↩` (desfazer): descartar alterações no arquivo (cuidado!).  
- `D` (diff): abrir o editor de comparação.

### 12.2.3 Mensagem de commit

Na parte superior da guia, há um campo de texto para digitar a mensagem do commit. Abaixo dele, um botão com ícone de "check" (`✔`) confirma o commit. Ao lado, um botão com "..." abre um menu com opções adicionais (pull, push, branch, etc.).

---

## 12.3 Realizando Commits, Pulls e Pushes pela Interface

### 12.3.1 Fazendo um commit

Passos:
1. Modifique ou crie arquivos no seu projeto.  
2. Na guia Source Control, os arquivos aparecem em "Changes".  
3. Passe o mouse sobre um arquivo e clique no `+` para adicioná-lo ao staging. Você pode adicionar todos de uma vez clicando no `+` que aparece ao lado de "Changes".  
4. Digite uma mensagem de commit no campo superior.  
5. Clique no ícone de "check" (`✔`) ou pressione `Ctrl+Enter` (Windows/Linux) / `Cmd+Enter` (macOS).  
6. O commit é criado localmente.

**Dica:** Se você quitar fazer um commit direto (sem staging explícito), pode usar a opção "Commit" no menu de três pontos, que faz o commit de todas as alterações (equivalente a `git commit -a`). Mas cuidado: isso inclui todos os arquivos modificados, mesmo os que você não quer.

### 12.3.2 Sincronizando com o remoto (pull/push)

No canto inferior esquerdo da janela do VS Code, há uma barra de status que mostra a branch atual e ícones de sincronização:

- Ícone de setas circulares: sincronizar (pull + push).  
- Ícone de nuvem com seta para baixo: pull.  
- Ícone de nuvem com seta para cima: push.

Você também pode acessar essas ações pelo menu de três pontos na guia Source Control:  
- **Pull, Push** – comandos individuais.  
- **Sync** – executa pull seguido de push.

**Importante:** Se houver conflitos durante o pull, o VS Code notificará e você precisará resolvê-los antes de continuar.

### 12.3.3 Publicando um repositório local

Se você tem um repositório local sem remote, o VS Code oferece a opção "Publish to GitHub" no menu de três pontos. Ele cria um repositório no GitHub (público ou privado) e faz o push inicial. Você precisa estar autenticado no GitHub (extensão GitHub Authentication).

### 12.3.4 Clonando um repositório

Na tela inicial do VS Code, há a opção "Clone Git Repository". Basta colar a URL e escolher uma pasta. O VS Code abrirá o repositório automaticamente.

### 12.3.5 Exercício prático 12.1

1. Crie um novo projeto local (ou use um existente).  
2. Faça algumas alterações e commit usando apenas a interface do VS Code.  
3. Adicione um remote (se não tiver) via menu de três pontos → "Remote" → "Add Remote".  
4. Faça um push.  
5. Simule uma alteração no GitHub (edite um arquivo diretamente pelo site) e depois faça pull no VS Code.

---

## 12.4 Gerenciando Branches Visualmente

### 12.4.1 Visualizando branches

Clique no nome da branch na barra inferior esquerda (ex: `main`). Uma lista suspensa aparece mostrando:

- **Branches locais**  
- **Branches remotas** (precedidas por `origin/`)  
- Opção para criar nova branch

### 12.4.2 Criando e trocando de branch

- Para criar uma nova branch a partir da atual, clique em "Create new branch..." na lista e dê um nome.  
- Para trocar, clique no nome da branch desejada na lista.  
- Se houver alterações não commitadas, o VS Code perguntará o que fazer (stash, commit, descartar).

### 12.4.3 Publicando uma branch

Quando você cria uma branch local e tenta fazer push, o VS Code pergunta se deseja publicá-la (configurar upstream). Basta confirmar.

### 12.4.4 Excluindo branches

No menu de três pontos da guia Source Control, escolha "Branch" → "Delete Branch...". Selecione a branch a ser deletada. O VS Code impede a exclusão da branch atual.

### 12.4.5 Fazendo merge

Para mesclar uma branch na atual:

1. Certifique-se de estar na branch de destino (ex: `main`).  
2. Menu de três pontos → "Branch" → "Merge Branch...".  
3. Escolha a branch a ser mesclada.  
4. Se houver conflitos, o VS Code entra em modo de resolução (ver seção 12.5).

### 12.4.6 Exercício prático 12.2

1. Crie uma branch `feature/nova` a partir da `main`.  
2. Faça um commit nela.  
3. Publique a branch no GitHub.  
4. Volte para `main`, faça uma alteração diferente e commit.  
5. Mescle `feature/nova` na `main` usando a interface. Resolva conflitos se necessário.

---

## 12.5 Resolvendo Conflitos com o Editor de Merge Integrado

### 12.5.1 Identificando conflitos

Quando um merge ou pull resulta em conflitos, o VS Code:

- Exibe um alerta.  
- Na guia Source Control, aparece a seção **Merge Changes** listando os arquivos conflitantes.  
- Os arquivos também são marcados no explorador com um ícone de alerta.

### 12.5.2 Abrindo o editor de merge

Clique duas vezes em um arquivo conflitante. O VS Code abre uma visualização dividida em três partes:

- **Esquerda:** versão atual (HEAD) – a sua branch.  
- **Direita:** versão de entrada (incoming) – a branch que está sendo mesclada.  
- **Centro:** resultado da mesclagem (onde você edita).

Acima do centro, há botões para aceitar:

- **Accept Current Change** – mantém a versão da esquerda.  
- **Accept Incoming Change** – mantém a da direita.  
- **Accept Both Changes** – combina as duas (cada uma em sua linha).  
- **Compare Changes** – visualiza as diferenças.

### 12.5.3 Resolvendo manualmente

Você também pode editar diretamente a área central, removendo os marcadores de conflito (`<<<<<<<`, `=======`, `>>>>>>>`) e deixando o código desejado.

### 12.5.4 Finalizando a resolução

Após resolver todos os conflitos em todos os arquivos, você deve:

1. Adicionar os arquivos resolvidos ao staging (clique no `+` ao lado de cada arquivo em "Merge Changes" ou no `+` geral).  
2. Digitar uma mensagem de commit (geralmente o VS Code já preenche uma padrão).  
3. Clicar no ícone de "check" para concluir o merge.

### 12.5.5 Abortando um merge

Se a confusão for grande, você pode abortar o merge: menu de três pontos → "Merge" → "Abort Merge".

### 12.5.6 Exercício prático 12.3

1. Provocando um conflito (como no capítulo 6).  
2. Use o editor de merge do VS Code para resolver.  
3. Finalize o merge e commit.

---

## 12.6 Visualizando Histórico com Extensões

O VS Code nativo mostra o histórico de forma limitada (apenas o último commit via Timeline). Para uma experiência rica, precisamos de extensões.

### 12.6.1 GitLens — Git supercharged

**GitLens** é a extensão mais popular para Git no VS Code. Ela adiciona uma infinidade de funcionalidades:

- **Blame inline:** mostra, ao lado de cada linha, quem a modificou pela última vez e quando.  
- **Explorador de commits:** uma nova guia na barra lateral com histórico, branches, stashes, etc.  
- **Navegação:** links para commits, autores, repositórios remotos.  
- **Comparação fácil:** selecione um trecho e veja sua evolução.  
- **GitLens Inspect:** painel detalhado do commit atual.

**Instalação:** procure por "GitLens" na guia de extensões.

### 12.6.2 Git History

Essa extensão (de donjayamanne) adiciona uma visualização gráfica do histórico. Para usá-la:

1. Abra a paleta de comandos (`Ctrl+Shift+P`).  
2. Digite "Git: View History" ou "Git: View File History".  
3. Uma nova aba mostra o gráfico de commits, permitindo filtrar por autor, branch, etc.

### 12.6.3 Git Graph

Outra extensão muito boa: **Git Graph** (de mhutchie). Ela exibe um gráfico interativo de commits no estilo `git log --graph`. Você pode:

- Clicar em commits para ver detalhes.  
- Criar branches, tags, fazer merge, checkout, etc. diretamente do gráfico.  
- Ver os commits de todas as branches.

### 12.6.4 Git Blame

Extensão mais leve que o GitLens, focada apenas em blame inline. Se você quer algo simples, pode ser suficiente.

### 12.6.5 Exercício prático 12.4

1. Instale GitLens e Git Graph.  
2. Explore o blame inline: abra um arquivo e veja as anotações.  
3. Abra o Git Graph e navegue pelo histórico do seu repositório.  
4. Use o GitLens para comparar duas versões de um arquivo.

---

## 12.7 Outras Extensões Úteis

### 12.7.1 GitHub Pull Requests and Issues

Extensão oficial da Microsoft que integra PRs e issues do GitHub. Permite:

- Listar, revisar e mergear PRs.  
- Criar issues.  
- Comentar e aprovar revisões.  
- Checkout de PRs localmente.

### 12.7.2 Remote Repositories

Outra extensão oficial que permite abrir repositórios remotos (GitHub, Azure) diretamente no VS Code, sem clonar localmente. Útil para revisões rápidas.

### 12.7.3 GitLens (já mencionado)

Vale reforçar que o GitLens também integra funcionalidades de PRs e issues.

### 12.7.4 Gitmoji

Para quem gosta de usar emojis em commits, a extensão Gitmoji facilita a inserção de emojis padronizados.

---

## 12.8 Configurações do VS Code para Melhorar a Experiência Git

### 12.8.1 Editor de diff

O VS Code tem um excelente editor de diff. Você pode configurar para que ele seja a ferramenta padrão de diff do Git (como visto no capítulo 2). Além disso, pode ajustar:

- `git.enableSmartCommit`: se verdadeiro, permite commit sem staging explícito (equivale a `git commit -a`). Cuidado!  
- `git.autofetch`: faz fetch automático periodicamente.  
- `git.confirmSync`: pede confirmação antes de sincronizar.  
- `git.untrackedChanges`: como exibir mudanças em arquivos não rastreados.

### 12.8.2 Atalhos de teclado

- `Ctrl+Shift+G` – abre Source Control.  
- `Ctrl+Enter` – faz commit (com mensagem).  
- `Ctrl+Shift+G` seguido de `Ctrl+P` – abre paleta de comandos Git.  
- `Alt+Shift+F` – formata documento (útil para Markdown).  

Você pode personalizar atalhos em File → Preferences → Keyboard Shortcuts.

### 12.8.3 Configurando o Git Bash como terminal padrão

Para ter uma experiência consistente, configure o terminal integrado para usar Git Bash (Windows) ou bash padrão (Linux/macOS). Isso permite executar comandos Git no terminal do VS Code com o mesmo ambiente.

---

## 12.9 Dicas de Produtividade

1. **Use a barra de status:** ela mostra branch, sincronização, e você pode clicar para ações rápidas.  
2. **Stage hunk (parte de um arquivo):** no diff, você pode clicar com botão direito em um trecho e escolher "Stage Selected Ranges" para adicionar apenas parte das alterações ao staging.  
3. **Desfazer staging rapidamente:** clique no `-` ao lado do arquivo em Staged Changes.  
4. **Compare arquivos:** no explorador, selecione um arquivo, clique com botão direito e "Select for Compare", depois escolha outro arquivo e "Compare with Selected".  
5. **Abra o repositório no GitHub:** com a extensão GitHub, você pode usar o comando "GitHub: Open on GitHub" para abrir rapidamente o repositório no navegador.  
6. **Use snippets de commit:** se você usa Conventional Commits, crie snippets no VS Code para agilizar.  

---

## 12.10 Exercícios de Fixação

1. Qual atalho abre a guia Source Control no VS Code?  
2. Como você adiciona um arquivo ao staging usando a interface?  
3. Explique como resolver um conflito de merge usando o editor de merge do VS Code.  
4. Cite três extensões que melhoram a experiência Git no VS Code e suas principais funções.  
5. Como você publica uma branch local no GitHub pelo VS Code?  
6. O que é GitLens e qual sua funcionalidade mais marcante?  
7. Qual a diferença entre as extensões Git History e Git Graph?  
8. Como você pode visualizar o histórico de um arquivo específico no VS Code?  
9. O que faz a configuração `git.enableSmartCommit`?  
10. (Desafio) Instale a extensão "GitHub Pull Requests and Issues", autentique-se e tente revisar um PR de um repositório público (ou crie um PR fictício no seu repositório e revise-o).

---

## 12.11 Resumo do Capítulo

- O VS Code oferece integração Git nativa através da guia Source Control.  
- É possível realizar todas as operações básicas (commit, pull, push, branch) sem terminal.  
- O editor de merge integrado simplifica a resolução de conflitos.  
- Extensões como GitLens, Git Graph e Git History potencializam a visualização do histórico e outras funcionalidades.  
- Configurações e atalhos adequados aumentam a produtividade.  

Agora você pode trabalhar com Git diretamente do seu editor favorito, combinando o poder do terminal com a conveniência da interface gráfica. No próximo capítulo, exploraremos o GitHub Copilot, o assistente de IA que pode gerar código e documentação, integrado ao VS Code.

---

## 12.12 Referências

- VS Code Docs: "Using Git source control"  
- GitLens Documentation: [https://gitlens.amod.io](https://gitlens.amod.io)  
- Git Graph – Visual Studio Marketplace  
- GitHub Pull Requests and Issues – Visual Studio Marketplace  
- "Visual Studio Code: End-to-End Git Integration" – blog da Microsoft
```

---
