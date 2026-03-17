
# Git e GitHub: Do Iniciante ao Profissional com VS Code

**Autor: Haroldo Capucci**

---

## Capítulo 2: Instalação e Configuração Inicial

**Páginas estimadas:** 28  
**Tempo de leitura:** 70–90 minutos  
**Objetivos do capítulo:**  
- Instalar o Git nos sistemas Windows, macOS e Linux  
- Instalar e configurar o Visual Studio Code  
- Realizar as configurações iniciais do Git (identidade, editor, etc.)  
- Compreender o Git Bash e o terminal integrado do VS Code  
- Configurar ferramentas de diff e merge  

---

## 2.1 Introdução

Antes de começar a usar o Git, é preciso preparar o ambiente de trabalho. Neste capítulo, você aprenderá a instalar o Git no seu sistema operacional, configurá-lo corretamente e integrá-lo ao Visual Studio Code, o editor que utilizaremos ao longo de todo o livro.

Uma boa configuração inicial evita dores de cabeça futuras e torna o fluxo de trabalho mais produtivo. Ao final deste capítulo, você terá um ambiente totalmente preparado para versionar seus projetos com Git e colaborar usando o GitHub.

---

## 2.2 Instalando o Git

### 2.2.1 Verificando se o Git já está instalado

Abra um terminal (Prompt de Comando, PowerShell, Terminal do Linux ou macOS) e digite:

```bash
git --version
```

Se o Git estiver instalado, a saída será algo como:

```
git version 2.40.0
```

Caso contrário, você receberá uma mensagem de comando não encontrado. Siga as instruções abaixo para seu sistema operacional.

2.2.2 Instalação no Windows

Método 1: Instalador oficial

1. Acesse https://git-scm.com/download/win
2. O download do instalador será iniciado automaticamente (versão de 64 bits).
3. Execute o arquivo baixado.
4. Durante a instalação, preste atenção nas seguintes telas:
   · Selecionar componentes: mantenha as opções padrão, mas recomenda‑se marcar "Git Bash Here" e "Git GUI Here" para facilitar o acesso.
   · Escolher o editor padrão: selecione "Use Visual Studio Code as Git's default editor" se já tiver o VS Code instalado (caso contrário, instale o VS Code primeiro ou escolha outro editor como Nano ou Vim).
   · Ajustar o PATH: escolha "Git from the command line and also from 3rd-party software" (recomendado).
   · Usar OpenSSL: mantenha a opção padrão.
   · Configurar terminais: escolha "Use MinTTY" (terminal mais amigável).
   · Opções extras: mantenha as padrões.
5. Conclua a instalação.

Método 2: via winget (Windows Package Manager)

Se você utiliza o Windows 10/11 com o gerenciador winget, abra o PowerShell como administrador e execute:

```bash
winget install --id Git.Git -e --source winget
```

Método 3: via Chocolatey

Caso utilize o Chocolatey:

```bash
choco install git
```

Após a instalação, reinicie o terminal e confirme com git --version.

2.2.3 Instalação no macOS

Método 1: Instalador oficial

1. Acesse https://git-scm.com/download/mac
2. Baixe o instalador apropriado para sua versão do macOS.
3. Abra o arquivo .dmg e execute o instalador .pkg.
4. Siga as instruções.

Método 2: via Homebrew (recomendado)

Se você tem o Homebrew instalado, basta:

```bash
brew install git
```

Método 3: via Xcode Command Line Tools

Em versões recentes do macOS, ao tentar usar git no terminal, o sistema pode oferecer a instalação automática das ferramentas de linha de comando. Aceite e aguarde.

2.2.4 Instalação no Linux

A instalação no Linux varia conforme a distribuição. Use o gerenciador de pacotes correspondente.

Debian/Ubuntu (apt)

```bash
sudo apt update
sudo apt install git
```

Fedora/RHEL (dnf)

```bash
sudo dnf install git
```

openSUSE (zypper)

```bash
sudo zypper install git
```

Arch Linux (pacman)

```bash
sudo pacman -S git
```

Após a instalação, confirme com git --version.

2.2.5 Instalação via código-fonte (avançado)

Caso precise de uma versão específica ou queira compilar manualmente, consulte a documentação oficial em https://git-scm.com/book/en/v2/Getting-Started-Installing-Git. Para a grande maioria dos usuários, os métodos acima são suficientes.

---

2.3 Instalando e Configurando o Visual Studio Code

2.3.1 Instalação do VS Code

Windows

1. Acesse https://code.visualstudio.com/download
2. Escolha a versão para Windows (User Installer ou System Installer – recomendamos o System Installer para todos os usuários).
3. Execute o instalador e siga os passos, marcando as opções:
   · Adicionar ação "Abrir com Code" ao menu de contexto de arquivo
   · Adicionar ação "Abrir com Code" ao menu de contexto de diretório
   · Registrar Code como editor para tipos de arquivo suportados
   · Adicionar ao PATH (essencial para usar o comando code no terminal)

macOS

1. Baixe o arquivo .zip do site oficial.
2. Extraia e arraste o aplicativo "Visual Studio Code" para a pasta "Aplicativos".
3. Abra o VS Code, pressione Cmd+Shift+P e digite "shell command" para instalar o comando code no PATH (isso permitirá abrir arquivos do terminal com code .).

Linux

· Debian/Ubuntu: baixe o arquivo .deb do site e instale com sudo dpkg -i <arquivo>.deb ou use o repositório da Microsoft.
· Fedora: baixe o arquivo .rpm e instale com sudo rpm -i <arquivo>.rpm ou via repositório.
· Outras distribuições: utilize o gerenciador de pacotes ou o pacote .tar.gz.

Após a instalação, abra o terminal e teste:

```bash
code --version
```

2.3.2 Extensões essenciais para Git

O VS Code já possui integração nativa com Git, mas algumas extensões tornam a experiência ainda mais produtiva. Recomendo instalar:

· GitLens — Git supercharged (eamodio.gitlens): amplia as funcionalidades do Git, mostrando blame, histórico, explorers, etc.
· Git History (donjayamanne.githistory): visualiza e navega pelo histórico de commits.
· Git Graph (mhutchie.git-graph): exibe um gráfico interativo dos commits e branches.
· Markdown All in One (yzhang.markdown-all-in-one): útil para escrever a documentação do livro.

Para instalar, clique no ícone de extensões na barra lateral (Ctrl+Shift+X) e pesquise pelos nomes.

2.3.3 Configurando o terminal integrado

O VS Code possui um terminal integrado que pode ser aberto com  Ctrl+`  (acento grave). Por padrão, ele usa o shell do sistema. Você pode alterar para o Git Bash no Windows:

1. Abra as configurações (Ctrl+,).
2. Pesquise por "terminal integrated shell windows".
3. Em Terminal > Integrated > Automation Shell: Windows, defina o caminho para o Git Bash (ex: C:\Program Files\Git\bin\bash.exe).

No macOS/Linux, o terminal padrão (bash ou zsh) já funciona perfeitamente.

---

2.4 Configuração Inicial do Git

O Git precisa de algumas informações básicas para registrar quem faz os commits. Essas configurações podem ser feitas em três níveis:

· Sistema (--system): afeta todos os usuários da máquina.
· Global (--global): afeta o usuário atual em todos os repositórios.
· Local (--local): afeta apenas o repositório atual (padrão).

Na maioria dos casos, configuramos o nível global.

2.4.1 Configurando nome e e-mail

```bash
git config --global user.name "Haroldo Capucci"
git config --global user.email "joseharoldocapucci@gmail.com"
```

Importante: Este e‑mail deve ser o mesmo que você utilizará para criar sua conta no GitHub (capítulo 3). Isso garante que seus commits sejam corretamente atribuídos a você nas plataformas de hospedagem.

Para verificar as configurações atuais:

```bash
git config --global --list
```

2.4.2 Configurando o editor padrão

O Git pode abrir um editor de texto para você digitar mensagens de commit (quando não usa a opção -m). Defina o VS Code como editor padrão:

```bash
git config --global core.editor "code --wait"
```

No Windows, pode ser necessário usar o caminho completo ou garantir que o comando code esteja no PATH. A flag --wait faz com que o terminal aguarde até que você feche o arquivo no VS Code.

Outros editores comuns:

· Nano: git config --global core.editor "nano"
· Vim: git config --global core.editor "vim"
· Emacs: git config --global core.editor "emacs"

2.4.3 Configurando ferramentas de diff e merge

Para facilitar a resolução de conflitos, você pode definir uma ferramenta visual de diff e merge. Por exemplo, para usar o próprio VS Code:

```bash
git config --global diff.tool vscode
git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd "code --wait $MERGED"
```

Existem ferramentas especializadas como Beyond Compare, Meld, KDiff3. A configuração varia, mas o princípio é o mesmo.

2.4.4 Configurando o nome da branch padrão

Desde outubro de 2020, o GitHub usa main como nome padrão da branch principal. Para alinhar seu ambiente local:

```bash
git config --global init.defaultBranch main
```

2.4.5 Configurando aliases (atalhos)

Aliases são apelidos para comandos longos. Exemplos úteis:

```bash
git config --global alias.s status
git config --global alias.c commit
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.l "log --oneline --graph"
```

Agora, em vez de git status, você pode usar git s. O alias git l mostra um log resumido e graficamente bonito.

2.4.6 Cache de credenciais

Para não precisar digitar usuário e senha a cada interação com o remoto (via HTTPS), configure o cache:

```bash
git config --global credential.helper cache
```

No Windows, o Git pode usar o Gerenciador de Credenciais do Windows. Durante a instalação, há uma opção para isso. No macOS, o helper padrão é o keychain.

---

2.5 Git Bash e Terminal Integrado

2.5.1 O que é Git Bash?

No Windows, ao instalar o Git, você ganha o Git Bash, um terminal que emula o ambiente Bash do Linux. Ele permite usar comandos Unix-like (como ls, pwd, grep) no Windows, o que é muito útil para quem está acostumado com Linux/macOS e para seguir os exemplos deste livro.

2.5.2 Abrindo o Git Bash

· Pelo menu Iniciar: "Git Bash".
· Clique com o botão direito em uma pasta e escolha "Git Bash Here".

Dentro do Git Bash, você pode executar comandos Git e também comandos do shell.

2.5.3 Terminal integrado do VS Code

No VS Code, abra o terminal integrado ( Ctrl+` ). Se você configurou o VS Code para usar o Git Bash (conforme 2.3.3), terá um ambiente Unix-like diretamente no editor. Isso facilita a execução de comandos sem sair do contexto de edição.

2.5.4 Primeiros comandos no terminal

Vamos testar se tudo está funcionando:

```bash
git version
code --version
pwd            # mostra diretório atual (no Git Bash)
ls -la         # lista arquivos
```

Se todos os comandos forem reconhecidos, seu ambiente está pronto.

---

2.6 Escolhendo o Editor Padrão e Ferramentas de Diff

2.6.1 Editores de texto para mensagens de commit

Quando você executa git commit sem -m, o Git abre o editor configurado. A escolha do editor é pessoal, mas para iniciantes recomendamos o VS Code por sua interface amigável e integração com Git.

2.6.2 Ferramentas de diff

O comando git diff mostra as diferenças entre versões de arquivos. Se você preferir uma visualização gráfica, pode usar o git difftool com a ferramenta configurada. Com a configuração acima, basta digitar:

```bash
git difftool
```

E o VS Code abrirá uma janela de comparação lado a lado.

---

2.7 Verificando a Configuração

Para ter certeza de que tudo foi configurado corretamente, execute:

```bash
git config --global --list
```

A saída deve incluir:

```
user.name=Haroldo Capucci
user.email=joseharoldocapucci@gmail.com
core.editor=code --wait
init.defaultBranch=main
alias.s=status
...
```

Se algo estiver faltando, repita os comandos da seção correspondente.

---

2.8 Exercícios de Fixação

1. Qual comando você usa para verificar a versão do Git instalada?
2. Instale o Git no seu sistema operacional (se ainda não o fez) e confirme com git --version.
3. Configure seu nome e e-mail globalmente, substituindo pelos seus dados reais.
4. Defina o VS Code como editor padrão do Git.
5. Crie um alias git hist que mostre o log em uma linha com gráfico (dica: use log --oneline --graph).
6. Abra o terminal integrado do VS Code e execute git config --global --list para confirmar as configurações.
7. (Desafio) Pesquise como configurar o Beyond Compare ou Meld como ferramenta de diff e tente configurá-lo.

---

2.9 Resumo do Capítulo

· Aprendemos a instalar o Git nos principais sistemas operacionais.
· Instalamos o Visual Studio Code e as extensões recomendadas para Git.
· Configuramos a identidade do usuário (nome e e-mail), essencial para os commits.
· Definimos o VS Code como editor padrão e configuramos ferramentas de diff/merge.
· Conhecemos o Git Bash e o terminal integrado do VS Code.
· Criamos aliases para agilizar comandos comuns.

Agora seu ambiente está pronto. No próximo capítulo, você criará uma conta no GitHub e configurará a autenticação segura (SSH) para conectar seu computador aos repositórios remotos.

---

2.10 Referências

· Documentação oficial do Git: https://git-scm.com/doc
· Documentação do Visual Studio Code: https://code.visualstudio.com/docs
· Pro Git Book (2ª edição) - Capítulo 1: "Getting Started"
· GitHub Docs: "Setting your commit email address"

```
