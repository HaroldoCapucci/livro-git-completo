```markdown
# Git e GitHub: Do Iniciante ao Profissional com VS Code

**Autor: Haroldo Capucci**

---

## Capítulo 6: Trabalhando com Branches (Ramificações)

**Páginas estimadas:** 32  
**Tempo de leitura:** 80–100 minutos  
**Objetivos do capítulo:**  
- Compreender o conceito de branches e sua importância  
- Criar, listar, renomear e excluir branches  
- Navegar entre branches com `git switch` e `git checkout`  
- Mesclar branches com `git merge` (fast-forward e merge de três vias)  
- Resolver conflitos de merge manualmente e com ferramentas visuais  
- Conhecer fluxos de trabalho com branches: Git Flow e GitHub Flow  
- Utilizar a interface gráfica do VS Code para gerenciar branches  

---

## 6.1 Introdução

Até agora, trabalhamos em uma linha reta do tempo: cada commit sucedia o anterior na branch `main` (ou `master`). Mas o desenvolvimento de software raramente é linear. Muitas vezes você precisa:

- Desenvolver uma nova funcionalidade sem atrapalhar o código estável  
- Corrigir um bug urgente enquanto continua trabalhando em outra tarefa  
- Experimentar uma ideia sem risco de quebrar o projeto principal  
- Colaborar com outras pessoas de forma paralela  

Para tudo isso, o Git oferece um recurso poderoso e leve: **branches** (ramificações). Uma branch é simplesmente um ponteiro móvel para um commit. Criar uma branch é instantâneo e não consome espaço extra, pois ela apenas referencia o histórico existente.

Neste capítulo, você dominará o uso de branches – a funcionalidade que torna o Git imbatível para trabalho paralelo.

---

## 6.2 O Conceito de Branches: Por que usar?

### 6.2.1 Linha do tempo alternativa

Imagine um livro sendo escrito. O autor tem a versão principal (main). Para escrever um novo capítulo experimental, ele cria uma cópia do manuscrito, trabalha nela e, se gostar, incorpora ao original. No Git, essa "cópia" é uma branch.

**Analogia com árvore:** O tronco principal é a branch `main`. Dele partem galhos (branches) que crescem independentemente. Podem dar frutos (commits) e, se desejado, ser enxertados de volta ao tronco (merge).

### 6.2.2 Vantagens

- **Isolamento:** alterações em uma branch não afetam outras.  
- **Paralelismo:** várias pessoas podem trabalhar em diferentes funcionalidades ao mesmo tempo.  
- **Experimentação:** crie uma branch para testar uma ideia; se falhar, basta deletá-la.  
- **Organização:** branches podem representar features, hotfixes, releases, etc.

---

## 6.3 Gerenciando Branches: Comandos Básicos

### 6.3.1 Listando branches

```bash
git branch
```

Mostra as branches locais. A branch atual é destacada com um asterisco (* main).

Para ver branches remotas também:

```bash
git branch -a
```

6.3.2 Criando uma nova branch

```bash
git branch nome-da-branch
```

Isso cria uma nova branch apontando para o mesmo commit onde você está. Mas você não muda para ela automaticamente.

6.3.3 Criando e mudando para a nova branch (atalho)

```bash
git switch -c nome-da-branch
```

Ou, com o comando antigo:

```bash
git checkout -b nome-da-branch
```

Esse é o modo mais comum: cria e já troca para a nova branch.

6.3.4 Trocando de branch

Com git switch (recomendado):

```bash
git switch nome-da-branch
```

Com git checkout:

```bash
git checkout nome-da-branch
```

6.3.5 Renomeando uma branch

```bash
git branch -m nome-antigo nome-novo
```

Se você já estiver na branch que quer renomear:

```bash
git branch -m nome-novo
```

6.3.6 Excluindo uma branch

```bash
git branch -d nome-da-branch
```

O Git só permite deletar se a branch já tiver sido mesclada (para não perder trabalho). Para forçar a exclusão (mesmo sem mesclar):

```bash
git branch -D nome-da-branch
```

Cuidado: branches deletadas localmente podem ser recuperadas via reflog (capítulo 11) se você tiver o hash do último commit.

---

6.4 Trocando de Branch: git switch vs. git checkout

Como vimos, git checkout é um comando sobrecarregado: serve para trocar de branch, restaurar arquivos, etc. O Git 2.23 introduziu git switch e git restore para separar essas responsabilidades.

Recomendação moderna: use git switch para branches e git restore para arquivos. Mas git checkout ainda é amplamente usado e aceito.

Exemplos comparativos:

Ação git checkout git switch
Trocar para branch existente git checkout main git switch main
Criar e trocar para nova branch git checkout -b nova git switch -c nova
Voltar ao commit anterior (detached HEAD) git checkout HEAD~1 git switch --detach HEAD~1

---

6.5 Unindo Históricos com Merge: git merge

Quando você termina o trabalho em uma branch, geralmente quer integrá-la à branch principal. O comando git merge faz isso.

6.5.1 Preparando o merge

Suponha que você criou uma branch feature/login a partir de main, fez alguns commits nela e agora quer mesclá-la de volta.

1. Vá para a branch de destino (aquela que receberá as mudanças):
   ```bash
   git switch main
   ```
2. Execute o merge:
   ```bash
   git merge feature/login
   ```

6.5.2 Tipos de merge

O Git é inteligente e tenta mesclar automaticamente. Existem dois cenários principais:

Fast-forward (avanço rápido)

Se a branch main não teve novos commits desde que feature/login foi criada, o Git simplesmente move o ponteiro de main para o commit mais recente de feature/login. É um merge linear, sem commit extra.

```
antes:   A---B---C  (main)
               \
                D---E  (feature/login)

depois:  A---B---C---D---E  (main, feature/login)
```

Merge de três vias (recursive)

Se main avançou enquanto você trabalhava na feature, o Git precisa combinar as duas linhas. Ele cria um novo commit de merge com dois pais.

```
antes:       A---B---C  (main)
               \
                D---E  (feature/login)

depois:      A---B---C---F  (main, commit de merge)
               \         /
                D-------E
```

6.5.3 Visualizando o merge

Após um merge, git log --graph --oneline mostrará o histórico entrelaçado.

6.5.4 Exercício prático 6.1

1. No seu repositório de testes, crie uma branch feature/1 e faça dois commits nela.
2. Volte para main e faça um commit diferente.
3. Agora mescle feature/1 em main. Observe o tipo de merge (deve ser merge de três vias).
4. Use git log --graph --oneline para ver o histórico.

---

6.6 Resolvendo Conflitos de Merge na Prática

Conflitos ocorrem quando duas branches alteram a mesma parte do mesmo arquivo de maneiras diferentes. O Git não sabe qual versão escolher e pede sua ajuda.

6.6.1 Simulando um conflito

1. Crie uma branch feature/a e altere a linha 1 de README.md para "A". Commit.
2. Volte para main e altere a mesma linha de README.md para "B". Commit.
3. Tente mesclar feature/a em main:
   ```bash
   git merge feature/a
   ```

Você verá:

```
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

6.6.2 Marcadores de conflito

Abra o arquivo conflitante. Ele conterá algo como:

```diff
<<<<<<< HEAD
B
=======
A
>>>>>>> feature/a
```

· <<<<<<< HEAD – sua versão atual (na branch main)
· ======= – separador
· >>>>>>> feature/a – versão da branch que está sendo mesclada

6.6.3 Resolvendo manualmente

Edite o arquivo para a versão desejada (pode ser uma combinação das duas) e remova os marcadores. Por exemplo, se quiser "A e B", deixe:

```
A e B
```

Salve o arquivo.

6.6.4 Finalizando o merge

Após resolver todos os conflitos:

```bash
git add README.md
git commit
```

O Git abrirá o editor com uma mensagem de merge pré-preenchida. Você pode aceitar ou modificar.

6.6.5 Usando ferramentas visuais

Se configurou uma ferramenta de merge (capítulo 2), use:

```bash
git mergetool
```

Ele abrirá a ferramenta (ex: VS Code) mostrando as três versões: local (HEAD), remota (feature) e mesclada (a ser salva). No VS Code, após instalar o GitLens, você tem uma interface visual para resolver conflitos.

6.6.6 Abortando um merge

Se a confusão for grande e você quiser voltar ao estado anterior:

```bash
git merge --abort
```

Isso desfaz o merge e retorna ao estado anterior.

6.6.7 Exercício prático 6.2

1. Crie uma situação de conflito propositalmente (como no exemplo).
2. Resolva manualmente, adicione e faça commit.
3. Repita o processo, mas desta vez use git mergetool (com VS Code configurado).

---

6.7 Boas Práticas com Branches: Git Flow e GitHub Flow

Existem modelos (fluxos) de como usar branches em equipe. Dois dos mais conhecidos são Git Flow e GitHub Flow.

6.7.1 Git Flow

Criado por Vincent Driessen, é um modelo mais estruturado, com branches específicas:

· main: código em produção
· develop: branch de integração, onde as features se juntam
· feature/*: branches para novas funcionalidades (partem de develop, retornam a develop)
· release/*: preparação para uma nova versão (correções finais)
· hotfix/*: correções urgentes em produção (partem de main, mesclam em main e develop)

Vantagens: organizado, previsível.
Desvantagens: complexo, pode ser exagerado para projetos pequenos.

6.7.2 GitHub Flow

Mais simples, usado por equipes que fazem deploy contínuo:

· main é sempre a versão pronta para deploy
· Para qualquer mudança, crie uma branch descritiva (ex: feature/novo-botao)
· Faça commits, abra um Pull Request (PR) para discussão
· Após revisão, faça o merge para main e faça o deploy imediatamente

Vantagens: simplicidade, integração com Pull Requests.
Desvantagens: menos adequado para releases programadas.

6.7.3 Escolhendo um fluxo

Para projetos pessoais ou pequenas equipes, o GitHub Flow é suficiente e mais fácil. Para projetos maiores com ciclos de release definidos, o Git Flow pode ser útil.

6.7.4 Exercício prático 6.3

Pesquise sobre GitLab Flow (uma variação que adiciona branches de ambiente) e compare com os dois modelos acima. Escreva um pequeno resumo.

---

6.8 Gerenciando Branches no VS Code

6.8.1 Visualizando branches

Na barra inferior esquerda do VS Code, há um indicador da branch atual (ex: main). Clique nele para abrir a paleta de comandos com opções de branches.

6.8.2 Criando e trocando branches

· Criar nova branch: clique no ícone de branch na barra inferior → "Create new branch..."
· Trocar de branch: clique no nome da branch e escolha a desejada na lista.

6.8.3 Publicando uma branch

Após criar uma branch local, você pode publicá-la no remoto com um clique (ícone de "Publicar branch" ao lado do nome).

6.8.4 Mesclando branches

Na guia "Source Control" (Ctrl+Shift+G), clique nos três pontos (...) e escolha "Branch" → "Merge Branch...". Selecione a branch a ser mesclada na atual.

6.8.5 Resolvendo conflitos visualmente

Quando ocorre um conflito, o VS Code destaca os arquivos. Abra o arquivo e você verá opções como "Accept Current Change", "Accept Incoming Change", "Accept Both Changes", ou "Compare Changes". Use os botões para resolver rapidamente.

---

6.9 Exemplo Prático: Criando uma Nova Funcionalidade com Branches

Vamos simular o desenvolvimento de uma nova funcionalidade seguindo o GitHub Flow.

1. Parta de main atualizada:
   ```bash
   git switch main
   git pull origin main
   ```
2. Crie uma branch descritiva:
   ```bash
   git switch -c feature/adiciona-contador
   ```
3. Faça as alterações necessárias (adicione um arquivo contador.js).
4. Commit:
   ```bash
   git add contador.js
   git commit -m "feat: adiciona contador de cliques"
   ```
5. Publique a branch no GitHub:
   ```bash
   git push -u origin feature/adiciona-contador
   ```
6. No GitHub, abra um Pull Request (comparando feature/adiciona-contador com main).
7. Após revisão e aprovação, faça o merge (pode ser feito pelo botão no GitHub).
8. Volte ao terminal e atualize main localmente:
   ```bash
   git switch main
   git pull origin main
   ```
9. Opcional: delete a branch local (já que foi mesclada):
   ```bash
   git branch -d feature/adiciona-contador
   ```

---

6.10 Exercícios de Fixação

1. O que é uma branch no Git e por que ela é útil?
2. Qual comando cria uma nova branch e já muda para ela?
3. Explique a diferença entre um merge fast-forward e um merge de três vias.
4. O que são marcadores de conflito (<<<<<<<, =======, >>>>>>>)?
5. Como você resolve um conflito de merge manualmente?
6. Descreva resumidamente o Git Flow e o GitHub Flow.
7. No VS Code, como você publica uma branch local no GitHub?
8. Crie um repositório de testes e simule um conflito, resolvendo-o usando o VS Code.
9. (Desafio) Pesquise sobre git rebase e como ele pode ser usado como alternativa ao merge (veremos no capítulo 11, mas tente entender a ideia).

---

6.11 Resumo do Capítulo

· Branches são ponteiros leves para commits, permitindo desenvolvimento paralelo.
· Comandos principais: git branch, git switch -c, git merge.
· Merges podem ser fast-forward (lineares) ou de três vias (com commit de merge).
· Conflitos ocorrem quando alterações incompatíveis são mescladas; devem ser resolvidos manualmente ou com ferramentas visuais.
· Existem fluxos de trabalho padronizados: Git Flow (mais estruturado) e GitHub Flow (mais simples).
· O VS Code oferece suporte gráfico completo para gerenciamento de branches.

Agora você já pode trabalhar com múltiplas linhas de desenvolvimento. No próximo capítulo, aprenderemos a documentar projetos com Markdown – essencial para criar READMEs atraentes e documentação de qualidade.

---

6.12 Referências

· Pro Git Book – Capítulo 3: "Git Branching"
· Documentação oficial: git help branch, git help merge
· "A successful Git branching model" (Git Flow) – Vincent Driessen
· GitHub Flow: https://guides.github.com/introduction/flow/
· VS Code Docs: "Using Git source control"

```
