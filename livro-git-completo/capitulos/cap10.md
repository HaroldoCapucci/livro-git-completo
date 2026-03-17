
# Git e GitHub: Do Iniciante ao Profissional com VS Code

**Autor: Haroldo Capucci**

---

## Capítulo 10: Gerenciamento de Projetos no GitHub

**Páginas estimadas:** 28  
**Tempo de leitura:** 70–90 minutos  
**Objetivos do capítulo:**  
- Compreender as ferramentas de gerenciamento de projetos oferecidas pelo GitHub  
- Utilizar Issues para rastrear tarefas, bugs e melhorias  
- Criar e gerenciar milestones para agrupar issues  
- Organizar o trabalho com labels e assignees  
- Utilizar Projects (quadros Kanban) para visualizar o fluxo de trabalho  
- Configurar automações para mover cards automaticamente  
- Criar e manter wikis para documentação extensa  
- Gerenciar releases e tags para versionamento  
- Explorar GitHub Discussions para comunicação assíncrona  

---

## 10.1 Introdução

O GitHub é muito mais do que um hospedeiro de código. Ele oferece um conjunto integrado de ferramentas de **gerenciamento de projetos** que ajudam equipes a planejar, acompanhar e entregar software de forma eficiente. Essas ferramentas são nativas da plataforma e se integram perfeitamente com o fluxo Git.

Dominar esses recursos permite:
- Organizar o trabalho de forma transparente  
- Facilitar a comunicação entre membros da equipe  
- Automatizar partes do fluxo de trabalho  
- Manter a documentação próxima ao código  
- Entregar versões com qualidade e rastreabilidade  

Neste capítulo, exploraremos cada uma dessas ferramentas, desde o básico até configurações avançadas.

---

## 10.2 Utilizando Issues para Gerenciar Tarefas e Bugs

**Issues** são a unidade fundamental de trabalho no GitHub. Elas podem representar:
- Relatos de bugs  
- Solicitações de novas funcionalidades  
- Tarefas técnicas  
- Discussões  

### 10.2.1 Criando uma Issue

1. No repositório, clique na aba **"Issues"**.  
2. Clique no botão verde **"New issue"**.  
3. Escolha um template (se houver) ou comece do zero.  
4. Preencha:
   - **Title:** descrição concisa  
   - **Comment:** detalhamento, podendo usar Markdown  
5. Opcionalmente, adicione **labels**, **assignees**, **projects**, **milestone**.  
6. Clique em **"Submit new issue"**.

### 10.2.2 Estruturando uma Issue

Uma issue bem escrita aumenta a produtividade. Exemplo de issue para bug:

```markdown
## Descrição
O botão "Salvar" não responde ao clique.

## Passos para reproduzir
1. Acesse a página de edição de perfil.
2. Altere o campo "Nome".
3. Clique em "Salvar".

## Comportamento esperado
Uma mensagem de sucesso deve aparecer.

## Ambiente
- SO: Windows 10
- Navegador: Chrome 98

## Logs
```

Erro no console: Uncaught TypeError: Cannot read property 'save' of undefined

```
```

Para uma nova funcionalidade:

```markdown
## Problema
Atualmente não há como recuperar a senha.

## Solução proposta
Adicionar um link "Esqueci minha senha" na tela de login, que envia um e‑mail com instruções.

## Critérios de aceitação
- [ ] Link visível na tela de login
- [ ] Envio de e‑mail funcional
- [ ] Token expira em 1 hora
```

10.2.3 Templates de Issues

Repositórios podem ter templates padronizados para bugs, features, etc. Eles ficam na pasta .github/ISSUE_TEMPLATE/ e são escritos em Markdown ou YAML.

Exemplo de template (simples) em .github/ISSUE_TEMPLATE/bug_report.md:

```markdown
---
name: Relatório de bug
about: Crie um relatório para nos ajudar a melhorar
title: "[BUG] "
labels: bug
assignees: ''

---

**Descrição do bug**
Uma descrição clara e concisa do bug.

**Para reproduzir**
Passos:
1. Vá para '...'
2. Clique em '...'
3. Role até '...'
4. Veja o erro

**Comportamento esperado**
Descrição clara do que deveria acontecer.

**Screenshots**
Se aplicável, adicione imagens.

**Ambiente:**
 - SO: [ex: Windows, macOS]
 - Navegador: [ex: Chrome, Safari]
 - Versão: [ex: 22]

**Contexto adicional**
Qualquer outra informação.
```

10.2.4 Labels (Rótulos)

Labels categorizam issues. O GitHub fornece algumas padrão (bug, enhancement, question, etc.), mas você pode criar as suas.

Criando labels: Vá em Issues → Labels → New label.

Exemplos úteis:

· bug – algo não funciona
· enhancement – nova funcionalidade
· documentation – melhoria na documentação
· good first issue – ideal para novos contribuidores
· help wanted – precisa de ajuda
· priority: high – prioridade alta
· status: blocked – aguardando algo

10.2.5 Milestones (Marcos)

Milestones agrupam issues com um objetivo comum e uma data alvo. Eles ajudam a planejar releases ou sprints.

Criando um milestone:

1. Em Issues → Milestones → New milestone.
2. Defina título, descrição e data de entrega.
3. Associe issues ao milestone (ao editar a issue, escolha o milestone).

10.2.6 Assignees (Responsáveis)

Atribuir uma issue a uma pessoa deixa claro quem está trabalhando nela. Uma issue pode ter vários assignees.

10.2.7 Exercício prático 10.1

No seu repositório de testes (ou no repositório do livro), crie:

· Duas labels personalizadas (ex: documentation, good first issue).
· Um milestone chamado "Versão 1.0" com data futura.
· Três issues: um bug, uma melhoria e uma tarefa de documentação. Atribua labels, milestone e assignees adequadamente.

---

10.3 Projetos: Kanban Integrado (GitHub Projects)

Projects são quadros estilo Kanban que permitem visualizar o fluxo de trabalho. Eles podem ser vinculados a um repositório ou a uma organização.

10.3.1 Tipos de Projects

O GitHub oferece dois tipos principais:

· Projects (clássico): o modelo antigo, baseado em colunas e cards.
· Projects (beta – novo): mais flexível, com campos personalizados, visualizações e automações robustas. Neste capítulo, focaremos no novo Projects (acessível em Projects na barra superior do repositório/organização).

10.3.2 Criando um Project

1. No repositório, clique na aba "Projects" (ou no perfil da organização).
2. Clique em "New project".
3. Escolha um template (Board, Roadmap, etc.) ou comece do zero.
4. Dê um nome (ex: "Desenvolvimento do Livro").
5. Defina a visibilidade (privado/público).
6. Clique em "Create".

10.3.3 Estrutura do Project (beta)

O novo Projects é como uma planilha/database. Você pode ter visualizações diferentes:

· Board view: colunas (como Kanban).
· Table view: lista tabular.
· Roadmap: cronograma.

As colunas no Board view são baseadas em um campo (ex: "Status") com opções (To do, In progress, Done).

10.3.4 Adicionando issues ao Project

· Dentro do Project, clique em "Add item" e digite # para buscar issues do repositório.
· Ou, na própria issue, no painel lateral direito, há a seção "Projects" para adicioná-la a um projeto.

10.3.5 Personalizando campos

Você pode adicionar campos personalizados:

· Texto
· Número
· Data
· Seleção única (dropdown)
· Iteração (sprints)

Exemplo: campo "Prioridade" com valores Alta, Média, Baixa.

10.3.6 Automações (Workflows)

No Projects, você pode criar automações para mover cards automaticamente. Exemplos:

· Quando uma issue é aberta, mover para "To do".
· Quando um PR é aberto, mover para "In review".
· Quando a issue é fechada, mover para "Done".

Para criar automações:

1. No Project, clique no menu do projeto (três pontos) e escolha "Workflows".
2. Crie um novo workflow com gatilhos e ações.

10.3.7 Vinculando Projects a repositórios

Projects podem ser organizacionais (visíveis em todos os repositórios da org) ou vinculados a um repositório específico. No novo Projects, você escolhe ao criar.

10.3.8 Exercício prático 10.2

1. Crie um Project (beta) no seu repositório chamado "Meu Kanban".
2. Configure a visualização Board com colunas: To do, In progress, Done.
3. Adicione as três issues criadas anteriormente ao Project.
4. Crie uma automação que mova issues para "In progress" quando um PR for aberto (simule com um PR de teste).
5. Experimente mudar a visualização para Table e Roadmap.

---

10.4 Discussões e Wikis: Documentação Colaborativa

10.4.1 GitHub Discussions

Discussions é um fórum integrado ao repositório, ideal para:

· Perguntas e respostas
· Anúncios
· Ideias
· Conversas que não se encaixam em issues (muito abertas)

Ativando Discussions:
Nas configurações do repositório, marque a opção "Discussions".

Categorias: você pode criar categorias (ex: Q&A, Ideas, Show and tell) para organizar as conversas.

Diferença entre Issues e Discussions: Issues são para trabalho rastreável (bugs, tarefas). Discussions são para conversas e ideias que podem ou não se transformar em issues.

10.4.2 Wikis

Wiki é um espaço de documentação livre, versionado em um repositório Git separado (com extensão .wiki.git). Você pode criar páginas interligadas, em Markdown.

Ativando Wiki: nas configurações do repositório, habilite Wikis.

Editando a Wiki: Você pode clonar o repositório da wiki e editar localmente, ou editar diretamente pelo site.

Exemplo de uso: documentação detalhada do projeto, guias de contribuição, FAQs.

10.4.3 Boas práticas para Wikis

· Mantenha uma página inicial (Home.md) com índice.
· Use links relativos entre páginas.
· Organize por categorias (ex: Instalação, Uso, API).
· Mantenha atualizada – assim como o código, a wiki precisa de manutenção.

10.4.4 Exercício prático 10.3

1. Ative Discussions no seu repositório e crie uma categoria "Dúvidas".
2. Inicie uma discussão perguntando algo sobre o livro (ex: "Qual capítulo você achou mais difícil?").
3. Ative a Wiki e crie uma página "Guia de Contribuição" com Markdown.
4. Na página inicial da Wiki, adicione um link para essa página.

---

10.5 Gerenciando Releases e Tags no GitHub

Releases são versões empacotadas do seu projeto, geralmente associadas a tags. Elas permitem disponibilizar arquivos binários (.zip, .exe) e notas de versão.

10.5.1 Criando uma tag

Tags são referências a commits, geralmente usadas para marcar versões (v1.0, v2.1.3). No Git:

```bash
git tag -a v1.0 -m "Versão 1.0 - Lançamento inicial"
git push origin v1.0
```

10.5.2 Criando uma Release pelo site

1. No repositório, vá em "Releases" (na aba Code).
2. Clique em "Create a new release" ou "Draft a new release".
3. Escolha a tag existente ou crie uma nova.
4. Preencha:
   · Release title: título amigável (ex: "Versão 1.0 – Estável")
   · Description: notas de versão em Markdown (destaque novas funcionalidades, correções, breaking changes)
5. Anexe arquivos binários (opcional).
6. Marque como pré‑release se não for estável.
7. Clique em "Publish release".

10.5.3 Notas de versão (Release Notes)

Boas notas de versão incluem:

· Resumo das principais mudanças
· Lista de novas funcionalidades
· Correções de bugs
· Mudanças que quebram compatibilidade (se houver)
· Agradecimentos a contribuidores

O GitHub pode gerar notas automaticamente a partir dos commits desde a última tag, mas é melhor personalizar.

10.5.4 Automatizando releases com GitHub Actions

É possível criar workflows que geram releases automaticamente quando uma tag é criada (capítulo 14).

10.5.5 Exercício prático 10.4

1. Crie uma tag v0.1.0 no seu repositório.
2. Crie uma release associada a essa tag, com notas de versão descrevendo os primeiros capítulos do livro.
3. Publique a release e verifique como ela aparece na página do repositório.

---

10.6 Integrando com VS Code

O VS Code oferece suporte a algumas dessas funcionalidades via extensões.

10.6.1 Visualizando Issues e PRs

Com a extensão "GitHub Pull Requests and Issues", você pode:

· Listar issues atribuídas a você
· Criar issues diretamente do editor
· Comentar e revisar PRs
· Gerenciar labels e assignees

10.6.2 Acessando Projects

A extensão não tem suporte direto a Projects, mas você pode abrir o navegador rapidamente com o comando Ctrl+Shift+P → "GitHub: Open on GitHub".

10.6.3 Editando a Wiki localmente

Você pode clonar o repositório da wiki:

```bash
git clone https://github.com/HaroldoCapucci/livro-git-completo.wiki.git
```

Edite os arquivos .md localmente e faça push. O VS Code funciona perfeitamente para isso.

---

10.7 Boas Práticas de Gerenciamento

1. Mantenha issues atômicas: cada issue deve representar uma unidade de trabalho pequena.
2. Use milestones para planejar entregas.
3. Defina um fluxo de trabalho claro (ex: To do → In progress → Review → Done).
4. Automatize o que for possível: automações reduzem trabalho manual.
5. Revise e feche issues antigas periodicamente.
6. Documente no wiki decisões arquiteturais e guias.
7. Use releases para comunicar mudanças aos usuários.

---

10.8 Exercícios de Fixação

1. Qual a diferença entre uma Issue e uma Discussion?
2. Como você cria um template de issue para relatar bugs?
3. O que é um milestone e como ele ajuda no planejamento?
4. Descreva como um quadro Kanban (Project) pode ser usado no desenvolvimento de um livro.
5. Como você adiciona uma issue existente a um Project?
6. Quais são os tipos de automação possíveis no Projects (beta)?
7. Para que serve uma Wiki e como ela se diferencia do README?
8. Como criar uma tag e uma release no GitHub?
9. Qual extensão do VS Code ajuda a gerenciar issues e PRs?
10. (Desafio) Configure um Project no seu repositório com automações e use‑o para gerenciar a escrita dos próximos capítulos do seu livro.

---

10.9 Resumo do Capítulo

· Issues são a base do rastreamento de trabalho: bugs, tarefas, melhorias.
· Labels, milestones e assignees organizam e priorizam as issues.
· Projects oferecem quadros Kanban flexíveis com automações.
· Discussions são fóruns para conversas abertas.
· Wikis fornecem documentação extensa versionada.
· Releases empacotam versões do projeto com notas.
· O VS Code, com extensões, integra-se a essas ferramentas.

Agora você tem todas as ferramentas para gerenciar projetos complexos diretamente no GitHub. No próximo capítulo, mergulharemos em tópicos avançados do Git: rebase interativo, stash, reflog e boas práticas.

---

10.10 Referências

· GitHub Docs: "About issues"
· GitHub Docs: "About projects"
· GitHub Docs: "About discussions"
· GitHub Docs: "About wikis"
· GitHub Docs: "Managing releases in a repository"
· Blog do GitHub: "Projects – the new way to plan and track your work"
· Extensão "GitHub Pull Requests and Issues" – documentação

```

---
