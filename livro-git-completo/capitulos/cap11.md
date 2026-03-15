```markdown
# Git e GitHub: Do Iniciante ao Profissional com VS Code

**Autor: Haroldo Capucci**

---

## Capítulo 11: Git Avançado e Boas Práticas

**Páginas estimadas:** 32  
**Tempo de leitura:** 80–100 minutos  
**Objetivos do capítulo:**  
- Dominar o rebase interativo para reescrever a história  
- Utilizar `git stash` para guardar trabalho temporário  
- Compreender e usar `git reflog` como rede de segurança  
- Comparar merge e rebase: quando usar cada um  
- Adotar boas práticas em mensagens de commit e organização  
- Configurar `.gitignore` avançado para diferentes cenários  
- Assinar commits com GPG para verificação de autenticidade  
- Usar `git bisect` para encontrar commits que introduziram bugs  
- Introdução a submódulos e seu gerenciamento  

---

## 11.1 Introdução

Nos capítulos anteriores, você aprendeu os comandos essenciais do Git e como colaborar com outras pessoas. Agora é hora de elevar seu nível: mergulhar em funcionalidades avançadas que tornam o Git uma ferramenta ainda mais poderosa e flexível.

Dominar esses recursos permite:
- Corrigir erros no histórico de forma elegante  
- Salvar temporariamente alterações sem commits  
- Recuperar commits "perdidos"  
- Manter um histórico limpo e compreensível  
- Garantir a autenticidade do seu código  
- Encontrar bugs de forma sistemática  

Além disso, discutiremos boas práticas que transformam um usuário comum em um profissional que respeita as convenções e facilita a vida de quem colabora com ele.

---

## 11.2 Reescrevendo a História: `git rebase` Interativo

O rebase interativo (`rebase -i`) é uma das ferramentas mais poderosas do Git. Ele permite modificar, reorganizar, combinar ou deletar commits antes de compartilhá-los.

### 11.2.1 O que é rebase?

Rebase significa "mudar a base". Em vez de mesclar (merge), que cria um commit de junção, o rebase reaplica os commits de uma branch sobre outra, criando uma história linear.

Exemplo: se você tem uma branch `feature` baseada em um commit antigo de `main`, ao fazer `git rebase main` na branch `feature`, o Git pega os commits da `feature` e os coloca após o último commit de `main`, como se tivessem sido feitos depois.

### 11.2.2 Rebase interativo

O rebase interativo permite escolher o que fazer com cada commit durante o processo.

```bash
git rebase -i HEAD~3   # últimos 3 commits
```

O editor abrirá com uma lista como:

```
pick a1b2c3d Adiciona funcionalidade X
pick e4f5g6h Corrige bug na funcionalidade X
pick i7j8k9l Adiciona testes
```

Para cada linha, você pode substituir pick por comandos:

· pick (p) – mantém o commit como está
· reword (r) – mantém o conteúdo, mas altera a mensagem
· edit (e) – para modificar o commit (conteúdo ou mensagem)
· squash (s) – combina o commit com o anterior (a mensagem é mesclada)
· fixup (f) – combina com o anterior, descartando a mensagem
· drop (d) – remove o commit

11.2.3 Exemplos práticos

Corrigir mensagem de um commit antigo:
Altere pick para reword na linha desejada, salve e feche. O Git abrirá o editor para a nova mensagem.

Combinar commits:
Suponha que os dois primeiros commits sejam muito atômicos e queira combiná-los. Altere o segundo para squash ou fixup.

```
pick a1b2c3d Adiciona funcionalidade X
squash e4f5g6h Corrige bug na funcionalidade X
pick i7j8k9l Adiciona testes
```

Ao salvar, o Git combinará os commits e pedirá uma mensagem para o novo commit único.

Remover um commit: troque pick por drop na linha.

11.2.4 Cuidados com rebase

· Nunca faça rebase em commits que já foram enviados para o remoto e compartilhados com outros. Isso reescreve a história e causa problemas para quem já tem a versão antiga.
· Use rebase localmente para organizar seu trabalho antes do push.
· Se precisar forçar o push após um rebase em uma branch que você é o único a usar, use git push --force-with-lease (mais seguro que --force).

11.2.5 Exercício prático 11.1

1. Em um repositório de testes, crie uma sequência de 4 commits com mensagens confusas.
2. Use git rebase -i HEAD~4 para:
   · Corrigir a mensagem do segundo commit
   · Combinar o terceiro e quarto commits em um só
   · Remover o primeiro commit (apenas para treino)
3. Verifique o histórico com git log --oneline.

---

11.3 Salvando Trabalho Temporário: git stash

Imagine que você está no meio de uma alteração e precisa urgentemente mudar de branch para corrigir um bug, mas não quer commitar código incompleto. O git stash é a solução.

11.3.1 Comandos básicos

· git stash – guarda as alterações atuais (working directory e staging) e reverte para o último commit.
· git stash list – lista os stashes salvos.
· git stash apply – aplica o stash mais recente, mas mantém na lista.
· git stash pop – aplica e remove da lista.
· git stash drop – remove um stash específico.
· git stash clear – remove todos os stashes.

11.3.2 Stash com nome

```bash
git stash push -m "WIP: ajustes na validação"
```

11.3.3 Stash parcial

Se quiser guardar apenas arquivos específicos:

```bash
git stash push -m "ajustes no README" README.md
```

11.3.4 Recuperando stashes

```bash
git stash apply stash@{2}   # aplica o stash de índice 2
```

11.3.5 Criando branch a partir de um stash

Se você aplicou um stash e decidiu que ele merece uma branch própria:

```bash
git stash branch nova-branch
```

11.3.6 Exercício prático 11.2

1. Em um repositório, modifique dois arquivos diferentes.
2. Use git stash para guardar as alterações.
3. Verifique que os arquivos voltaram ao estado do último commit.
4. Liste os stashes.
5. Aplique o stash com pop.
6. Repita o processo, mas desta vez crie uma branch a partir do stash.

---

11.4 Comandos de Emergência e Recuperação: git reflog

O reflog é um registro de todas as movimentações do ponteiro HEAD no seu repositório local. É a "rede de segurança" do Git: mesmo commits que parecem perdidos podem ser encontrados aqui.

11.4.1 Visualizando o reflog

```bash
git reflog
```

Saída típica:

```
a1b2c3d HEAD@{0}: commit: Adiciona funcionalidade X
e4f5g6h HEAD@{1}: rebase -i (finish): refatora histórico
i7j8k9l HEAD@{2}: commit: Corrige bug
```

Cada entrada mostra o hash do commit, a ação e uma referência tipo HEAD@{n}.

11.4.2 Recuperando um commit "perdido"

Suponha que você fez um git reset --hard e perdeu commits. No reflog, você encontra o hash do commit anterior e pode voltar:

```bash
git checkout a1b2c3d
# ou criar uma branch a partir dele
git branch recuperacao a1b2c3d
```

11.4.3 Entendendo o reflog

O reflog é local e expira após 90 dias (configurável). Ele não é compartilhado com o remoto.

11.4.4 Exercício prático 11.3

1. Faça alguns commits e depois um git reset --hard HEAD~2.
2. Use git reflog para encontrar os commits anteriores.
3. Recupere um deles criando uma nova branch.

---

11.5 Merge vs. Rebase: Quando Usar Cada Um

A discussão entre merge e rebase é clássica. Ambos integram mudanças, mas de formas diferentes.

11.5.1 Merge

· Cria um commit de merge (com dois pais).
· Preserva a história exata de quando as branches divergiram e foram unidas.
· Mais fiel à realidade temporal.
· Pode poluir o histórico com muitos commits de merge.

11.5.2 Rebase

· Reescreve a história, aplicando os commits da branch sobre a base mais recente.
· Gera uma história linear, mais fácil de ler.
· Evita commits de merge.
· Perde o contexto de quando a branch foi criada.

11.5.3 Boas práticas

· Use merge em branches compartilhadas (ex: main recebendo develop) para preservar o contexto.
· Use rebase em branches locais ou de feature antes de integrar, para manter a história limpa.
· Nunca faça rebase de branches públicas que outras pessoas podem ter usado.

11.5.4 Integração com git pull

Você pode configurar o git pull para fazer rebase em vez de merge:

```bash
git config --global pull.rebase true
```

Assim, git pull equivale a git fetch + git rebase.

11.5.5 Exercício prático 11.4

1. Crie duas branches a partir de um mesmo ponto.
2. Faça commits em ambas.
3. Em uma, faça merge da outra. Observe o histórico.
4. Na outra (recriando a situação), faça rebase. Compare os históricos com git log --graph.

---

11.6 Boas Práticas com .gitignore

Já vimos o básico do .gitignore. Agora, vamos aprofundar.

11.6.1 Padrões avançados

· **/logs – ignora qualquer pasta logs em qualquer nível.
· *.log – ignora todos os arquivos .log.
· !important.log – exclui o arquivo important.log da regra anterior (exceção).
· build/ – ignora a pasta build na raiz.
· **/__pycache__/ – ignora pastas __pycache__ em qualquer nível.

11.6.2 Ignorar arquivos já rastreados

Se um arquivo já está sendo versionado e você quer ignorá-lo a partir de agora, precisa removê-lo do índice:

```bash
git rm --cached arquivo.conf
```

Depois adicione ao .gitignore.

11.6.3 Modelos prontos

O GitHub mantém uma coleção de .gitignore templates em github/gitignore. Você pode baixar o específico para sua linguagem.

11.6.4 .gitignore global

Para ignorar arquivos em todos os repositórios (ex: .DS_Store no macOS, backups de editor), crie um arquivo global:

```bash
git config --global core.excludesfile ~/.gitignore_global
```

Nesse arquivo, coloque padrões como:

```
.DS_Store
*.swp
*.swo
Thumbs.db
```

---

11.7 Assinatura de Commits com GPG

Para garantir que um commit realmente foi feito por você (e não por alguém se passando), você pode assinar commits com GPG.

11.7.1 Gerando uma chave GPG

No Linux/macOS, instale o GPG (se necessário) e gere a chave:

```bash
gpg --full-generate-key
```

Escolha o tipo RSA (4096 bits) e preencha seu nome e e-mail (o mesmo do Git).

11.7.2 Listando chaves e obtendo o ID

```bash
gpg --list-secret-keys --keyid-format LONG
```

Saída:

```
sec   rsa4096/AAAAAAAAAAAAAAAA 2023-01-01 [SC]
      XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
uid                 [ultimate] Haroldo Capucci <joseharoldocapucci@gmail.com>
```

O ID é AAAAAAAAAAAAAAAA (após a barra).

11.7.3 Exportando a chave pública

```bash
gpg --armor --export AAAAAAAAAAAAAAAA
```

Copie a saída, incluindo as linhas -----BEGIN PGP PUBLIC KEY BLOCK----- e -----END-----.

11.7.4 Adicionando a chave pública ao GitHub

1. GitHub → Settings → SSH and GPG keys → New GPG key.
2. Cole a chave pública.
3. Adicione.

11.7.5 Configurando o Git para assinar commits

```bash
git config --global user.signingkey AAAAAAAAAAAAAAAA
git config --global commit.gpgsign true  # assina todos os commits por padrão
```

11.7.6 Assinando commits manualmente

Se não quiser assinar todos, use git commit -S para assinar um commit específico.

11.7.7 Verificando assinaturas

No GitHub, commits assinados mostram um selo "Verified". Localmente:

```bash
git log --show-signature
```

11.7.8 Exercício prático 11.5

1. Gere uma chave GPG (se não tiver).
2. Configure o Git para usá-la.
3. Faça um commit assinado e veja o selo no GitHub.
4. Verifique a assinatura localmente.

---

11.8 Encontrando Bugs com git bisect

git bisect faz uma busca binária no histórico para encontrar o commit que introduziu um bug.

11.8.1 Fluxo básico

1. Inicie o bisect: git bisect start
2. Marque um commit bom (sem o bug): git bisect good <commit>
3. Marque um commit ruim (com o bug): git bisect bad <commit>
4. O Git checkout um commit intermediário. Teste se o bug existe.
5. Informe: git bisect good ou git bisect bad
6. Repita até que o Git aponte o commit culpado.
7. Finalize: git bisect reset

11.8.2 Automatizando com script

Se você tem um script de teste que retorna 0 para sucesso e !=0 para falha:

```bash
git bisect start HEAD <commit-bom>
git bisect run npm test   # ou pytest, make test, etc.
```

11.8.3 Exercício prático 11.6

1. Em um repositório, introduza um bug em um commit antigo (ex: quebre uma função).
2. Use git bisect para encontrar o commit que introduziu o bug.
3. Após encontrar, finalize e corrija o bug.

---

11.9 Submódulos (Submodules)

Submódulos permitem incluir um repositório Git dentro de outro. Útil quando você quer usar uma biblioteca externa ou compartilhar código entre projetos.

11.9.1 Adicionando um submódulo

```bash
git submodule add https://github.com/usuario/biblioteca.git libs/biblioteca
```

Isso cria um arquivo .gitmodules e clona o repositório na pasta especificada.

11.9.2 Clonando um repositório com submódulos

```bash
git clone --recursive https://github.com/meu/projeto.git
```

Se já clonou sem --recursive, atualize:

```bash
git submodule update --init --recursive
```

11.9.3 Atualizando submódulos

Dentro da pasta do submódulo, faça git pull. Depois volte ao repositório principal e faça commit da nova referência.

11.9.4 Removendo submódulos

Remover submódulos é trabalhoso. O processo manual envolve remover do .gitmodules, da área de staging e da pasta. Consulte a documentação oficial.

11.9.5 Cuidados com submódulos

· Eles ficam em um estado "detached HEAD". É recomendável criar branches neles.
· Alterações no submódulo precisam ser commitadas e push separadamente.
· Podem complicar o fluxo para iniciantes. Considere alternativas como gerenciadores de dependência (npm, pip, etc.).

---

11.10 Boas Práticas Gerais

11.10.1 Mensagens de commit

· Use o padrão Conventional Commits.
· Primeira linha até 50 caracteres.
· Corpo explicando o porquê, não o como.
· Referencie issues com #123.

11.10.2 Tamanho dos commits

Commits devem ser atômicos: uma única mudança lógica. Evite commits gigantes que misturam várias coisas.

11.10.3 Branches

· Nomes descritivos: feature/autenticacao, bugfix/botao-quebrado, hotfix/1.2.1.
· Remova branches mescladas: git branch -d nome e git push origin --delete nome.

11.10.4 Proteção de branches

No GitHub, configure regras de proteção para a branch main:

· Exigir pull request com aprovação.
· Exigir que status checks passem.
· Impedir push direto.

11.10.5 Documentação

Mantenha README.md, CONTRIBUTING.md e LICENSE sempre atualizados.

---

11.11 Exercícios de Fixação

1. O que é rebase interativo e para que serve?
2. Como você guarda alterações temporárias sem commit?
3. Qual a utilidade do git reflog? Dê um exemplo.
4. Explique quando usar merge e quando usar rebase.
5. Como você faz um .gitignore global?
6. O que é necessário para assinar commits com GPG?
7. Descreva o fluxo do git bisect para encontrar um bug.
8. O que são submódulos e qual sua principal desvantagem?
9. Liste três boas práticas para mensagens de commit.
10. (Desafio) Simule um cenário onde você precisa usar git rebase -i para organizar uma branch de feature antes de integrá-la à main, e depois faça o merge.

---

11.12 Resumo do Capítulo

· Rebase interativo permite reescrever a história localmente.
· Stash guarda alterações temporárias.
· Reflog é a rede de segurança para recuperar commits perdidos.
· Merge preserva contexto; rebase cria histórico linear.
· .gitignore avançado e global.
· GPG garante autenticidade dos commits.
· Bisect ajuda a encontrar bugs sistematicamente.
· Submódulos integram repositórios externos, mas com complexidade.
· Boas práticas tornam o trabalho colaborativo mais eficiente.

Agora você domina o Git em nível profissional. Nos próximos capítulos, exploraremos a integração com VS Code (capítulo 12), GitHub Copilot (13), automação com Actions (14) e projetos práticos (15 e 16).

---

11.13 Referências

· Pro Git Book – Capítulos 7 e 8: "Git Tools"
· Documentação oficial: git help rebase, git help stash, git help reflog, git help bisect, git help submodule
· GitHub Docs: "About commit signature verification"
· Conventional Commits: https://www.conventionalcommits.org
· Atlassian Git Tutorials: "Merging vs. Rebasing"

```
