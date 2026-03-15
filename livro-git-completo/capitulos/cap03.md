 ```markdown
# Git e GitHub: Do Iniciante ao Profissional com VS Code

**Autor: Haroldo Capucci**

---

## Capítulo 3: Autenticação Segura com GitHub

**Páginas estimadas:** 26  
**Tempo de leitura:** 65–85 minutos  
**Objetivos do capítulo:**  
- Criar uma conta no GitHub  
- Entender as diferenças entre autenticação HTTPS e SSH  
- Gerar e configurar chaves SSH no Windows, macOS e Linux  
- Adicionar a chave pública à sua conta do GitHub  
- Configurar o GitHub CLI (opcional)  
- Gerenciar múltiplas contas e chaves  

---

## 3.1 Introdução

No capítulo anterior, você preparou seu ambiente local com Git e VS Code. Agora é hora de conectar esse ambiente ao **GitHub**, a plataforma que hospedará seus repositórios e permitirá a colaboração com outros desenvolvedores.

Para que a comunicação entre seu computador e o GitHub seja segura, existem duas formas principais de autenticação: **HTTPS** (com usuário/senha ou token) e **SSH** (com chaves criptográficas). Neste capítulo, você aprenderá ambas, com ênfase no SSH por ser mais seguro e prático após a configuração inicial.

Ao final, você estará apto a clonar, enviar e receber alterações de repositórios remotos sem digitar senha a cada operação.

---

## 3.2 Criando uma Conta no GitHub

### 3.2.1 Passo a passo

1. Acesse [https://github.com](https://github.com)
2. Clique no botão **"Sign up"** (Inscrever‑se)
3. Preencha os campos:
   - **Email:** use o mesmo que você configurou no Git (`joseharoldocapucci@gmail.com`). Isso facilitará a atribuição dos commits.
   - **Password:** crie uma senha forte (mínimo 8 caracteres, com letras, números e símbolos)
   - **Username:** escolha um nome de usuário único. Exemplos: `haroldocapucci`, `josecapucci`, `hcapucci`. Esse nome aparecerá na URL do seu perfil: `github.com/seu-usuario`
   - **Email preferences:** opte por receber ou não atualizações (recomendamos desmarcar se não quiser spam)
4. Complete o desafio de verificação (quebra-cabeça ou código enviado por e‑mail)
5. Clique em **"Create account"**
6. Verifique seu e‑mail com o código enviado pelo GitHub

### 3.2.2 Escolhendo o plano

Após a verificação, o GitHub perguntará se você deseja o plano **Free** ou **Team**. Escolha **Free** (gratuito). Ele já oferece repositórios públicos e privados ilimitados, com até 3 colaboradores em repositórios privados (suficiente para a maioria dos usuários individuais).

### 3.2.3 Confirmando o e‑mail no Git local

Lembre‑se de que você configurou o Git com o e‑mail `joseharoldocapucci@gmail.com`. Para garantir que seus commits fiquem associados à sua conta do GitHub, verifique novamente:

```bash
git config --global user.email
```

A saída deve ser <joseharoldocapucci@gmail.com>. Se não for, corrija:

```bash
git config --global user.email "joseharoldocapucci@gmail.com"
```

---

3.3 Autenticação via HTTPS vs. SSH

3.3.1 HTTPS (Hypertext Transfer Protocol Secure)

Como funciona:

· Você se autentica com seu nome de usuário e senha (ou token) do GitHub.
· Para cada operação que exija autenticação (push, pull de repositório privado), o Git pede suas credenciais.
· Desde agosto de 2021, o GitHub não aceita mais senhas comuns no terminal; você deve usar um token de acesso pessoal (PAT – Personal Access Token).

Vantagens:

· Mais simples para iniciantes (não requer criação de chaves).
· Funciona em qualquer rede (porta 443 geralmente aberta).

Desvantagens:

· Precisa digitar usuário/token a cada operação (a menos que use cache de credenciais).
· Token tem validade e pode expirar, exigindo renovação.

3.3.2 SSH (Secure Shell)

Como funciona:

· Você gera um par de chaves: uma pública (que você coloca no GitHub) e uma privada (que fica no seu computador, jamais compartilhada).
· A comunicação é criptografada e autenticada automaticamente.
· Não é necessário digitar senha/token a cada operação.

Vantagens:

· Mais seguro (chave privada nunca trafega na rede).
· Mais prático (após configurado, não pede credenciais).
· Recomendado para uso frequente.

Desvantagens:

· Configuração inicial um pouco mais complexa.
· Pode ser bloqueado em redes corporativas muito restritivas.

3.3.3 Qual escolher?

Para o dia a dia, SSH é a melhor opção. Neste capítulo, focaremos nela, mas também explicaremos como gerar um token HTTPS para quem precisar.

---

3.4 Passo a Passo Detalhado: Gerando e Configurando Chaves SSH

3.4.1 Verificando se você já possui chaves SSH

Abra o terminal e execute:

```bash
ls -al ~/.ssh
```

Se você já tiver chaves SSH, verá arquivos como id_rsa (privada) e id_rsa.pub (pública), ou id_ed25519/id_ed25519.pub. Caso existam, você pode usá‑las ou gerar novas. Se não houver, siga os próximos passos.

3.4.2 Gerando uma nova chave SSH (recomendado: ed25519)

O algoritmo Ed25519 é mais moderno e seguro que o RSA. Use o comando:

```bash
ssh-keygen -t ed25519 -C "joseharoldocapucci@gmail.com"
```

Explicação:

· -t ed25519: tipo de chave
· -C "email": comentário (geralmente seu e‑mail, para identificar a chave)

Se seu sistema não suportar Ed25519 (muito raro), use RSA:

```bash
ssh-keygen -t rsa -b 4096 -C "joseharoldocapucci@gmail.com"
```

Durante a execução, o comando perguntará:

```
Enter file in which to save the key (/home/você/.ssh/id_ed25519):
```

Pressione Enter para aceitar o local padrão.

Em seguida, solicitará uma frase secreta (passphrase):

```
Enter passphrase (empty for no passphrase):
```

Você pode deixar em branco (apenas Enter) ou definir uma frase. Uma frase secreta adiciona uma camada extra de segurança: mesmo que alguém obtenha sua chave privada, precisará da frase para usá‑la. A desvantagem é que você precisará digitá‑la sempre que usar a chave (a menos que use um agente SSH). Para a maioria dos usuários domésticos, deixar em branco é aceitável.

3.4.3 Adicionando a chave ao agente SSH (opcional, mas recomendado)

O agente SSH gerencia suas chaves e evita que você digite a frase secreta repetidamente.

No Linux/macOS:

```bash
# Inicie o agente em segundo plano
eval "$(ssh-agent -s)"

# Adicione a chave privada
ssh-add ~/.ssh/id_ed25519
```

No Windows (Git Bash):

```bash
# Inicie o agente
eval $(ssh-agent -s)

# Adicione a chave
ssh-add ~/.ssh/id_ed25519
```

Se você definiu uma frase secreta, ela será solicitada agora.

3.4.4 Exibindo a chave pública

A chave pública é o arquivo com extensão .pub. Para vê‑la e copiá‑la:

```bash
cat ~/.ssh/id_ed25519.pub
```

A saída será algo como:

```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIG1yR3b5... joseharoldocapucci@gmail.com
```

Selecione todo o conteúdo (inclusive o ssh-ed25519 no início e o e‑mail no final) e copie para a área de transferência.

---

3.5 Adicionando a Chave SSH à Sua Conta do GitHub

1. Faça login no GitHub.
2. No canto superior direito, clique na sua foto de perfil e escolha "Settings".
3. Na barra lateral esquerda, clique em "SSH and GPG keys".
4. Clique no botão verde "New SSH key".
5. No campo "Title", dê um nome descritivo para identificar a chave (ex: "Meu notebook pessoal").
6. No campo "Key", cole a chave pública que você copiou.
7. Clique em "Add SSH key".
8. Confirme sua senha do GitHub, se solicitado.

Pronto! Agora seu computador está autorizado a se comunicar com o GitHub via SSH.

---

3.6 Testando a Conexão SSH

Para verificar se tudo funcionou:

```bash
ssh -T git@github.com
```

A primeira vez que você conectar, verá uma mensagem como:

```
The authenticity of host 'github.com (140.82.113.4)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
Are you sure you want to continue connecting (yes/no)?
```

Digite yes e pressione Enter. Em seguida, se tudo estiver correto, você verá:

```
Hi HaroldoCapucci! You've successfully authenticated, but GitHub does not provide shell access.
```

(Substitua HaroldoCapucci pelo seu nome de usuário.)

Caso receba uma mensagem de permissão negada, revise os passos anteriores.

---

3.7 Configurando o GitHub CLI (opcional)

O GitHub CLI (gh) é uma ferramenta de linha de comando que permite interagir com o GitHub sem sair do terminal: criar repositórios, abrir pull requests, ver issues, etc.

3.7.1 Instalação

· Windows: winget install --id GitHub.cli ou baixe o instalador em <https://cli.github.com>
· macOS: brew install gh
· Linux: siga as instruções para sua distribuição em <https://github.com/cli/cli#installation>

3.7.2 Autenticação

Após instalar, execute:

```bash
gh auth login
```

O assistente perguntará:

· Qual protocolo usar: escolha SSH.
· Se deseja usar suas chaves SSH existentes: escolha yes.
· Ele fará o teste de conexão e autenticará.

Pronto! Agora você pode usar comandos como gh repo create, gh pr list, etc.

---

3.8 Gerenciando Múltiplas Contas e Chaves

Se você trabalha com contas diferentes (ex: pessoal e empresarial), pode precisar de chaves SSH distintas e configurar o Git para usar a chave correta em cada repositório.

3.8.1 Criando chaves específicas por conta

Gere uma chave com nome diferente:

```bash
ssh-keygen -t ed25519 -C "pessoal@email.com" -f ~/.ssh/id_ed25519_pessoal
ssh-keygen -t ed25519 -C "empresa@email.com" -f ~/.ssh/id_ed25519_empresa
```

3.8.2 Configurando o arquivo ~/.ssh/config

Crie (ou edite) o arquivo ~/.ssh/config com blocos como:

```
# Conta pessoal
Host github.com-pessoal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_pessoal

# Conta empresarial
Host github.com-empresa
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_empresa
```

Agora, ao clonar um repositório da conta pessoal, você usará o host github.com-pessoal:

```bash
git clone git@github.com-pessoal:usuario-pessoal/repo.git
```

3.8.3 Configurando o Git localmente por repositório

Dentro de cada repositório, você pode configurar o nome e e‑mail específicos:

```bash
git config user.name "Haroldo Pessoal"
git config user.email "pessoal@email.com"
```

Isso sobrescreve a configuração global apenas naquele repositório.

---

3.9 Autenticação via HTTPS com Token

Caso prefira ou precise usar HTTPS, siga estes passos:

3.9.1 Gerando um token de acesso pessoal

1. No GitHub, vá para Settings → Developer settings → Personal access tokens → Tokens (classic).
2. Clique em "Generate new token" → "Generate new token (classic)".
3. Dê um nome (ex: "Meu computador").
4. Selecione os escopos (permissões). Para operações básicas de repositório, marque repo (acesso total a repositórios). Se for apenas para clonar repositórios públicos, pode marcar apenas public_repo.
5. Clique em "Generate token".
6. Copie o token imediatamente (ele não será mostrado novamente).

3.9.2 Usando o token

Ao clonar com HTTPS, você usará o token como senha:

```bash
git clone https://github.com/usuario/repo.git
# Quando pedir usuário, digite seu nome de usuário
# Quando pedir senha, cole o token (não sua senha do GitHub)
```

Para não precisar digitar toda vez, configure o cache:

```bash
git config --global credential.helper cache
# ou no Windows: git config --global credential.helper manager-core
```

---

3.10 Exercícios de Fixação

1. Crie sua conta no GitHub com o e‑mail <joseharoldocapucci@gmail.com>.
2. Gere um par de chaves SSH (Ed25519) e adicione a chave pública à sua conta.
3. Teste a conexão com ssh -T <git@github.com>.
4. (Opcional) Instale o GitHub CLI e faça a autenticação.
5. Crie um repositório teste no GitHub (pode ser via web) e clone‑o usando SSH.
6. Dentro do repositório clonado, crie um arquivo README.md, faça commit e push.
7. Configure um alias no Git para git s (status) e git l (log oneline).
8. (Desafio) Se você tiver duas contas, configure o arquivo ~/.ssh/config para usar chaves diferentes e clone um repositório de cada conta.

---

3.11 Resumo do Capítulo

· Criamos uma conta no GitHub com o e‑mail configurado no Git.
· Entendemos as diferenças entre HTTPS (com token) e SSH (com chaves).
· Geramos chaves SSH (Ed25519) e adicionamos a chave pública ao GitHub.
· Testamos a conexão SSH com sucesso.
· Conhecemos o GitHub CLI e como gerenciar múltiplas contas.
· Aprendemos a gerar tokens HTTPS para quem precisar.

Agora seu ambiente está completamente integrado com o GitHub. No próximo capítulo, começaremos a trabalhar com repositórios locais e remotos, aplicando na prática tudo o que configuramos.

---

3.12 Referências

· Documentação GitHub: "Connecting to GitHub with SSH"
· Documentação GitHub: "Creating a personal access token"
· man ssh-keygen
· man ssh-agent
· GitHub CLI manual: gh help

```
