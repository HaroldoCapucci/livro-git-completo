```markdown
# Git e GitHub: Do Iniciante ao Profissional com VS Code

**Autor: Haroldo Capucci**

---

## Capítulo 9: Colaboração com Forks e Pull Requests

**Páginas estimadas:** 30  
**Tempo de leitura:** 75–95 minutos  
**Objetivos do capítulo:**  
- Compreender o modelo de colaboração baseado em forks e pull requests  
- Aprender a fazer um fork de um repositório no GitHub  
- Configurar o repositório local para trabalhar com o fork e o original  
- Criar uma branch para sua contribuição e enviar alterações  
- Abrir um Pull Request (PR) e descrevê‑lo adequadamente  
- Participar do processo de revisão de código  
- Manter o fork sincronizado com o repositório original  
- Utilizar o VS Code e GitHub CLI para agilizar o fluxo  

---

## 9.1 Introdução

O GitHub não é apenas um lugar para guardar código; é uma plataforma social de colaboração. Milhares de projetos open source vivem no GitHub e recebem contribuições de pessoas do mundo todo. Mas como alguém que não tem permissão de escrita em um repositório pode contribuir? A resposta é o modelo **fork + pull request**.

- **Fork:** uma cópia do repositório original para a sua conta no GitHub. Você tem total liberdade para modificar esse fork.  
- **Pull Request (PR):** uma solicitação para que o mantenedor do projeto original incorpore as alterações que você fez no seu fork.

Esse fluxo é a espinha dorsal da colaboração open source e também é amplamente usado em empresas para revisão de código antes de integrar mudanças à branch principal.

Neste capítulo, você aprenderá na prática como contribuir com projetos alheios e também como receber contribuições nos seus próprios projetos.

---

## 9.2 O Modelo de Colaboração: Fork e Pull Request

### 9.2.1 Fluxo básico

1. **Fork** o repositório desejado para sua conta.  
2. **Clone** seu fork para o computador local.  
3. **Adicione o repositório original como remote** (upstream) para manter-se sincronizado.  
4. **Crie uma branch** para sua contribuição (ex: `feature/minha-mudanca`).  
5. Faça as alterações, **commits** e **push** para o seu fork.  
6. No GitHub, **abra um Pull Request** comparando sua branch com a branch principal do original.  
7. Participe da **revisão**: discuta, faça ajustes se necessário.  
8. Quando aprovado, o mantenedor **faz o merge** (ou você, se tiver permissão).  
9. Após o merge, você pode **sincronizar seu fork** com o original e deletar a branch usada.

### 9.2.2 Por que esse modelo?

- **Segurança:** contribuidores não têm acesso direto ao repositório principal.  
- **Qualidade:** todo código passa por revisão antes de ser integrado.  
- **Rastreabilidade:** fica claro quem fez o quê e por quê.  
- **Transparência:** discussões ficam públicas e documentadas.

---

## 9.3 Fazendo um Fork de um Projeto

### 9.3.1 Escolhendo um projeto

Para este capítulo, usaremos um repositório de exemplo: `octocat/Hello-World` (um repositório público criado pelo GitHub para testes). Você pode usar qualquer repositório público que desejar.

### 9.3.2 Executando o fork

1. Acesse o repositório no GitHub: `https://github.com/octocat/Hello-World`  
2. No canto superior direito, clique no botão **"Fork"**.  
3. Escolha sua conta pessoal como destino (se houver mais de uma).  
4. Aguarde – o GitHub criará uma cópia exata do repositório em `https://github.com/seu-usuario/Hello-World`.

Agora você tem seu próprio fork. Ele contém todo o histórico, branches e tags do original.

### 9.3.3 Verificando o fork

No seu fork, você verá uma mensagem "forked from octocat/Hello-World" abaixo do nome do repositório, indicando a origem.

---

## 9.4 Clonando o Fork e Configurando o Upstream

### 9.4.1 Clonando o fork para o computador

```bash
git clone https://github.com/HaroldoCapucci/Hello-World.git
cd Hello-World
```

9.4.2 Adicionando o repositório original como remote upstream

```bash
git remote add upstream https://github.com/octocat/Hello-World.git
```

Verifique os remotos:

```bash
git remote -v
```

Saída esperada:

```
origin    https://github.com/HaroldoCapucci/Hello-World.git (fetch)
origin    https://github.com/HaroldoCapucci/Hello-World.git (push)
upstream  https://github.com/octocat/Hello-World.git (fetch)
upstream  https://github.com/octocat/Hello-World.git (push)
```

Agora você tem dois remotos:

· origin: seu fork (onde você tem permissão de escrita).
· upstream: o repositório original (somente leitura para você).

9.4.3 Importância do upstream

Manter o upstream configurado permite que você sincronize seu fork com as atualizações do projeto original, evitando que sua cópia fique desatualizada.

---

9.5 Criando uma Branch para a Contribuição

Nunca trabalhe diretamente na branch main do seu fork. Crie uma branch descritiva para sua contribuição.

9.5.1 Atualize sua main local com a upstream

Antes de criar a branch, certifique-se de que sua main local está igual à do projeto original:

```bash
git switch main
git pull upstream main
git push origin main   # opcional: atualizar seu fork no GitHub
```

9.5.2 Crie e mude para a nova branch

```bash
git switch -c minha-contribuicao
```

Use um nome que identifique o propósito, como fix/typo-readme, feature/adiciona-botao, docs/atualiza-exemplo.

---

9.6 Fazendo as Alterações e Commit

9.6.1 Edite os arquivos necessários

Por exemplo, vamos corrigir um pequeno erro no README do repositório Hello-World.

Abra o arquivo README (pode ser README.md) e faça uma alteração simples (adicione uma linha, corrija um typo).

9.6.2 Commit das alterações

```bash
git add README.md
git commit -m "docs: corrige pequeno erro de digitação no README"
```

Lembre-se das boas práticas de mensagens de commit (capítulo 5).

9.6.3 Push para o seu fork

```bash
git push origin minha-contribuicao
```

Se for o primeiro push dessa branch, use -u para configurar upstream:

```bash
git push -u origin minha-contribuicao
```

Agora sua branch está no seu fork no GitHub.

---

9.7 Abrindo um Pull Request (PR)

9.7.1 Pelo site do GitHub

1. Acesse seu fork no GitHub: https://github.com/HaroldoCapucci/Hello-World
2. O GitHub geralmente mostra um banner sugerindo "minha-contribuicao had recent pushes" com um botão "Compare & pull request". Clique nele.
   · Se não aparecer, vá até a aba "Pull requests" e clique no botão verde "New pull request".
3. Na página de comparação, verifique:
   · base repository: octocat/Hello-World (o original)
   · base: main (a branch do original que receberá as mudanças)
   · head repository: HaroldoCapucci/Hello-World (seu fork)
   · compare: minha-contribuicao (sua branch)
4. O GitHub mostrará um diff das alterações. Confira se está tudo correto.
5. Clique em "Create pull request".
6. Preencha o título e a descrição do PR (veja seção 9.8).
7. Clique novamente em "Create pull request".

Pronto! Seu PR está aberto e visível para os mantenedores do projeto original.

9.7.2 Pelo GitHub CLI

Se você tem o GitHub CLI instalado (capítulo 3), pode abrir o PR diretamente do terminal:

```bash
gh pr create --base main --head minha-contribuicao --title "docs: corrige typo no README" --body "Correção de um pequeno erro de digitação."
```

O comando interativo também pode ser usado: gh pr create e siga as instruções.

9.7.3 Pelo VS Code

Com a extensão "GitHub Pull Requests and Issues" instalada, você pode abrir PRs diretamente do editor:

1. Abra a guia "Source Control".
2. Clique nos três pontos e escolha "Pull Request" → "Create Pull Request".
3. Preencha os campos na interface.

---

9.8 Escrevendo uma Boa Descrição de Pull Request

Uma descrição clara ajuda os revisores a entenderem sua contribuição e acelera o processo.

9.8.1 Estrutura recomendada

```markdown
## Descrição
Breve explicação do que este PR faz. Se for uma correção de bug, descreva o problema. Se for uma nova funcionalidade, explique o motivo e o comportamento esperado.

## Tipo de mudança
- [ ] Correção de bug
- [x] Nova funcionalidade
- [ ] Documentação
- [ ] Refatoração
- [ ] Outro (especifique)

## Como testar
Passos para testar as alterações:
1. Acesse a página X
2. Clique no botão Y
3. Verifique se Z aparece

## Checklist
- [x] Meu código segue as diretrizes do projeto
- [x] Eu testei minhas alterações
- [ ] Atualizei a documentação, se necessário
- [ ] Adicionei testes, quando aplicável

## Issues relacionadas
Closes #123 (se este PR resolve uma issue)
```

9.8.2 Dicas

· Seja educado e grato.
· Referencie issues usando #numero.
· Use listas e cabeçalhos para organizar.
· Inclua prints ou GIFs se a mudança for visual.

---

9.9 Revisando Código: Comentários, Sugestões e Aprovações

Após abrir o PR, os mantenedores (e outros contribuidores) podem revisar seu código.

9.9.1 Tipos de comentários no GitHub

· Comentário geral: no topo do PR, sobre o conjunto.
· Comentário em linha: em uma linha específica do código (passe o mouse sobre a linha e clique no ícone de +).
· Sugestão: o revisor pode propor uma alteração usando o bloco de sugestão (suggestion), que você pode aceitar com um clique.

9.9.2 Respondendo a revisões

· Seja receptivo a críticas construtivas.
· Faça os ajustes solicitados na mesma branch, faça novos commits e push – o PR será atualizado automaticamente.
· Marque os comentários como resolvidos após implementar.
· Se discordar de algo, explique educadamente o motivo.

9.9.3 Aprovação e merge

Quando o revisor estiver satisfeito, ele aprovará o PR (botão "Approve"). O mantenedor então fará o merge (ou você, se tiver permissão). Existem opções de merge:

· Create a merge commit: mantém histórico completo.
· Squash and merge: combina todos os commits em um só.
· Rebase and merge: reescreve os commits na base.

---

9.10 Mantendo seu Fork Sincronizado

Enquanto seu PR está aberto, o projeto original pode receber outras contribuições. É importante manter seu fork atualizado para evitar conflitos.

9.10.1 Sincronização manual

```bash
git switch main
git pull upstream main
git push origin main
```

Se você ainda está trabalhando na branch de contribuição, pode mesclar as atualizações da main nela:

```bash
git switch minha-contribuicao
git merge main   # ou git rebase main
# resolva conflitos, se houver
git push origin minha-contribuicao
```

9.10.2 Sincronização pelo GitHub

O GitHub oferece um botão "Fetch upstream" no seu fork, que permite atualizar a branch main diretamente pelo site. Após usar, você precisará dar pull localmente.

9.10.3 Automatizando com GitHub Actions

É possível configurar um workflow que mantém seu fork sincronizado automaticamente (tópico avançado, veremos no capítulo 14).

---

9.11 Boas Práticas para Contribuições

1. Comunique-se antes: se a mudança for grande, abra uma issue primeiro para discutir.
2. Siga as diretrizes do projeto: muitos têm CONTRIBUTING.md.
3. Faça commits atômicos: cada commit deve fazer uma única mudança lógica.
4. Escreva mensagens de commit claras.
5. Teste suas alterações.
6. Mantenha o foco: um PR deve resolver um problema ou adicionar uma funcionalidade, não várias ao mesmo tempo.
7. Seja paciente: mantenedores são voluntários e podem demorar a responder.

---

9.12 Recebendo Pull Requests no Seu Próprio Repositório

Se você mantém um projeto, receberá PRs de outras pessoas. O fluxo como revisor:

1. Analise o código, teste localmente se possível.
2. Use comentários e sugestões para pedir melhorias.
3. Quando estiver satisfeito, faça o merge.
4. Agradeça ao contribuidor.

9.12.1 Testando PRs localmente

Para testar um PR de outra pessoa, você pode fazer fetch da branch dela:

```bash
git fetch origin pull/ID/head:nome-local
git switch nome-local
```

Ou usar o GitHub CLI: gh pr checkout ID.

---

9.13 Exemplo Completo com VS Code e GitHub CLI

Vamos simular uma contribuição real usando as ferramentas.

9.13.1 Cenário

Repositório original: HaroldoCapucci/livro-git-completo (seu próprio livro).
Você quer corrigir um typo no capítulo 1.

9.13.2 Passos

1. Fork o repositório (se for seu, você já tem acesso, mas para treino, use outro).
2. Clone o fork:
   ```bash
   gh repo clone HaroldoCapucci/livro-git-completo   # se tiver gh
   ```
3. Adicione upstream:
   ```bash
   git remote add upstream https://github.com/HaroldoCapucci/livro-git-completo.git
   ```
4. Crie branch:
   ```bash
   git switch -c fix/typo-cap1
   ```
5. Edite capitulos/cap01.md, corrija o typo.
6. Commit:
   ```bash
   git add capitulos/cap01.md
   git commit -m "fix: corrige pequeno erro de digitação no capítulo 1"
   ```
7. Push:
   ```bash
   git push -u origin fix/typo-cap1
   ```
8. Abra PR (pelo gh):
   ```bash
   gh pr create --base main --head fix/typo-cap1 --title "Correção de typo no capítulo 1" --body "Corrige um pequeno erro de digitação."
   ```
9. Acompanhe no navegador ou com gh pr status.

---

9.14 Exercícios de Fixação

1. O que é um fork e qual sua finalidade no modelo de colaboração do GitHub?
2. Explique a diferença entre os remotos origin e upstream em um fork clonado.
3. Por que é recomendável criar uma branch separada para cada contribuição?
4. Descreva o processo para abrir um Pull Request após fazer alterações no fork.
5. Quais informações devem constar em uma boa descrição de Pull Request?
6. Como você responde a um comentário de revisão que pede alterações?
7. Como manter seu fork sincronizado com o repositório original?
8. Utilizando o GitHub CLI, qual comando abre um novo Pull Request?
9. No VS Code, como você pode testar um PR de outra pessoa localmente?
10. (Desafio) Encontre um projeto open source no GitHub com issues marcadas como "good first issue" e tente fazer uma contribuição seguindo o fluxo aprendido.

---

9.15 Resumo do Capítulo

· O modelo fork + pull request é a base da colaboração no GitHub.
· Fork é uma cópia do repositório para sua conta; você pode modificá‑la livremente.
· Após clonar o fork, adicione o repositório original como remote upstream.
· Crie branches específicas para cada contribuição.
· Abra Pull Requests com descrições claras e detalhadas.
· A revisão de código é uma etapa fundamental: discuta, ajuste, aprenda.
· Mantenha seu fork sincronizado para evitar conflitos.
· Ferramentas como GitHub CLI e VS Code integram-se perfeitamente a esse fluxo.

Agora você está pronto para contribuir com projetos open source e também para gerenciar contribuições nos seus próprios projetos. No próximo capítulo, veremos como usar as ferramentas de gerenciamento de projetos do GitHub: issues, projetos, wikis e muito mais.

---

9.16 Referências

· GitHub Docs: "Fork a repo"
· GitHub Docs: "About pull requests"
· GitHub CLI manual: gh pr --help
· "Open Source Guide": https://opensource.guide
· "How to Contribute to Open Source" – freeCodeCamp
· VS Code Docs: "GitHub Pull Requests and Issues" extension

```
