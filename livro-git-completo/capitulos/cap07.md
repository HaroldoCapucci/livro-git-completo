```markdown
# Git e GitHub: Do Iniciante ao Profissional com VS Code

**Autor: Haroldo Capucci**

---

## Capítulo 7: Markdown para Documentação

**Páginas estimadas:** 24  
**Tempo de leitura:** 60–80 minutos  
**Objetivos do capítulo:**  
- Compreender a importância da documentação em projetos de software  
- Aprender a sintaxe básica e avançada do Markdown  
- Criar arquivos README.md atraentes e informativos  
- Utilizar o VS Code para escrever e visualizar Markdown  
- Aplicar boas práticas de documentação em repositórios Git  

---

## 7.1 Introdução

De que adianta ter um código brilhante se ninguém sabe como usá‑lo, instalá‑lo ou contribuir com ele? A documentação é a ponte entre o desenvolvedor e os usuários (incluindo você mesmo no futuro).

No universo Git/GitHub, o formato padrão para documentação é o **Markdown**. Ele é simples, legível mesmo em texto puro e se converte facilmente em HTML bonito no site do GitHub. Todo repositório que se preze tem um arquivo `README.md` na raiz – é a porta de entrada do projeto.

Neste capítulo, você aprenderá a dominar o Markdown e a criar documentações profissionais que farão seus projetos se destacarem.

---

## 7.2 O que é Markdown?

Markdown é uma linguagem de marcação leve criada por John Gruber em 2004. O objetivo é ser fácil de ler e fácil de escrever, mesmo em texto plano, e poder ser convertida para HTML (e outros formatos) de maneira simples.

### 7.2.1 Por que usar Markdown?

- **Simplicidade:** a sintaxe é intuitiva e rápida de aprender.  
- **Legibilidade:** mesmo sem processamento, o texto é claro.  
- **Versatilidade:** GitHub, GitLab, Bitbucket, fóruns, sites estáticos (Jekyll, Hugo) – todos aceitam Markdown.  
- **Versionamento:** por ser texto puro, o Git pode mostrar diffs das alterações na documentação.  

### 7.2.2 Onde o Markdown é usado no ecossistema Git

- `README.md` – apresentação do projeto  
- `CONTRIBUTING.md` – guia para contribuidores  
- `LICENSE.md` – texto da licença  
- Issues e Pull Requests (comentários podem usar Markdown)  
- Wikis do GitHub  

---

## 7.3 Sintaxe Básica do Markdown

Vamos explorar os elementos mais comuns. Em todos os exemplos, mostramos a sintaxe e a saída esperada.

### 7.3.1 Títulos

Use `#` para títulos. Quanto mais `#`, menor o nível.

```markdown
# Título nível 1 (equivalente a <h1>)
## Título nível 2 (<h2>)
### Título nível 3 (<h3>)
#### Título nível 4 (<h4>)
##### Título nível 5 (<h5>)
###### Título nível 6 (<h6>)
```

7.3.2 Ênfase (itálico e negrito)

```markdown
*itálico* ou _itálico_
**negrito** ou __negrito__
***itálico e negrito*** ou **_combinação_**
```

7.3.3 Listas

Não ordenadas: use -, * ou +

```markdown
- Item 1
- Item 2
  - Subitem 2.1 (dois espaços antes do traço)
  - Subitem 2.2
* Item com asterisco
+ Item com mais
```

Ordenadas: use números seguidos de ponto

```markdown
1. Primeiro
2. Segundo
   1. Subitem (com 4 espaços)
   2. Outro subitem
3. Terceiro
```

7.3.4 Links

```markdown
[Texto do link](https://exemplo.com)
[Link com título](https://exemplo.com "Título opcional")
```

Links relativos dentro do repositório:

```markdown
[Veja o código](src/index.js)
[Leia a licença](LICENSE.md)
```

7.3.5 Imagens

Sintaxe similar aos links, mas com ! na frente:

```markdown
![Texto alternativo](caminho/para/imagem.jpg)
![Logo do projeto](images/logo.png "Título opcional")
```

No GitHub, você pode usar imagens hospedadas ou relativas ao repositório.

7.3.6 Citações em bloco

Use > no início da linha:

```markdown
> Esta é uma citação.
> Pode ter várias linhas.
>> E até citações aninhadas.
```

7.3.7 Linhas horizontais

Três ou mais hífens, asteriscos ou underscores:

```markdown
---
***
___
```

7.3.8 Código

Código inline: envolva com crases  ` 

```markdown
O comando `git status` mostra o estado do repositório.
```

Bloco de código: use três crases antes e depois, opcionalmente com a linguagem para syntax highlighting:

```markdown
```javascript
function saudacao(nome) {
  return `Olá, ${nome}!`;
}
```
```

Para um bloco genérico (sem destaque):

```markdown
```
Isso é um bloco de código simples.
```
```

7.3.9 Exercício prático 7.1

Crie um arquivo teste.md no seu repositório de estudos e escreva nele:

· Um título principal e dois subtítulos
· Uma lista de compras (não ordenada)
· Uma lista de passos (ordenada)
· Um link para o Google
· Uma imagem qualquer (pode ser um placeholder tipo https://via.placeholder.com/150)
· Um bloco de código em JavaScript com uma função simples

Visualize o resultado no VS Code (veja seção 7.6).

---

7.4 Sintaxe Avançada

O Markdown básico é suficiente para a maioria dos casos, mas alguns recursos extras são suportados por muitas plataformas (incluindo GitHub).

7.4.1 Tabelas

Use pipes (|) e hífens para separar cabeçalho e linhas:

```markdown
| Comando | Descrição |
|---------|-----------|
| `git status` | Mostra o estado dos arquivos |
| `git add` | Adiciona arquivos ao staging |
| `git commit` | Cria um novo commit |
```

Você pode alinhar colunas com dois pontos:

```markdown
| Esquerda | Centro | Direita |
|:---------|:------:|--------:|
| Texto    | Texto  | Texto   |
```

7.4.2 Listas de tarefas (task lists)

No GitHub, você pode criar checkboxes:

```markdown
- [x] Tarefa concluída
- [ ] Tarefa pendente
- [ ] Outra pendente
```

7.4.3 Menções a usuários e equipes

Use @usuario para notificar alguém em issues/comentários. No README, apenas mostra o link para o perfil.

7.4.4 Emojis

O GitHub suporta códigos de emoji como :smile: ou :rocket:. Lista completa em https://www.webfx.com/tools/emoji-cheat-sheet/.

Exemplo: :octocat: vira o mascote do GitHub.

7.4.5 Notas de rodapé

Alguns processadores suportam notas de rodapé:

```markdown
Texto com nota[^1].

[^1]: Explicação da nota.
```

7.4.6 Escapando caracteres especiais

Se quiser mostrar um caractere que tem significado especial (como * ou #), use barra invertida:

```markdown
\*Isto não será itálico\*
```

7.4.7 Exercício prático 7.2

No mesmo arquivo teste.md, adicione:

· Uma tabela comparando Git e SVN (pelo menos 3 linhas)
· Uma lista de tarefas com dois itens concluídos e um pendente
· Uma menção ao seu próprio usuário do GitHub (ex: @HaroldoCapucci)
· Um emoji (por exemplo, :tada:)

---

7.5 Criando um README Profissional

O arquivo README.md é o cartão de visitas do seu projeto. Um bom README responde a perguntas como:

· O que é este projeto?
· Para que serve?
· Como instalar?
· Como usar?
· Onde obter ajuda?
· Quem mantém?
· Como contribuir?

7.5.1 Estrutura recomendada

```markdown
# Nome do Projeto

Breve descrição (1-2 frases) do que o projeto faz.

## Índice

- [Instalação](#instalação)
- [Uso](#uso)
- [Contribuição](#contribuição)
- [Licença](#licença)

## Instalação

Passo a passo para instalar e configurar o ambiente.

```bash
comando de instalação
```

Uso

Exemplos de como utilizar o projeto, com código e prints.

```javascript
exemplo de código
```

Contribuição

Instruções para quem quiser contribuir (pull requests, issues). Mencione o arquivo CONTRIBUTING.md se houver.

Licença

Informe a licença (ex: MIT, GPL-3.0).

```

### 7.5.2 Boas práticas

- Use badges (emblemas) para mostrar status: build passing, cobertura de testes, versão, licença. Exemplo:  
  `![Build Status](https://img.shields.io/...)`  
- Inclua uma tabela de conteúdos para READMEs longos.  
- Mantenha a linguagem clara e direta.  
- Atualize sempre que houver mudanças significativas.  
- Use exemplos reais de código.  

### 7.5.3 Badges (emblemas)

Serviços como [Shields.io](https://shields.io) geram badges personalizáveis. Exemplos:

```markdown
![GitHub license](https://img.shields.io/github/license/HaroldoCapucci/livro-git-completo)
![GitHub last commit](https://img.shields.io/github/last-commit/HaroldoCapucci/livro-git-completo)
```

7.5.4 Exercício prático 7.3

Crie um README.md para o repositório do seu livro (ou para um projeto fictício) seguindo a estrutura acima. Inclua pelo menos:

· Título e descrição
· Índice com links funcionais
· Seção de instalação (pode ser fictícia)
· Seção de uso com um exemplo de código
· Pelo menos dois badges (licença e último commit)

---

7.6 Preview de Markdown no VS Code

O VS Code tem excelente suporte a Markdown nativamente.

7.6.1 Abrindo o preview

· Abra um arquivo .md.
· Clique no ícone de "Abrir visualização" no canto superior direito (ou Ctrl+Shift+V).
· O preview é atualizado em tempo real conforme você digita.

7.6.2 Atalhos úteis

· Ctrl+K V – abre preview ao lado (split view).
· Ctrl+Shift+P e digite "Markdown: Open Preview" – mesma coisa.

7.6.3 Extensões recomendadas

· Markdown All in One (yzhang.markdown-all-in-one): atalhos, auto-completar, TOC automático, formatação.
· markdownlint (DavidAnson.vscode-markdownlint): alerta sobre más práticas na sintaxe.
· GitHub Markdown Preview (bierner.github-markdown-preview): preview idêntico ao do GitHub.

7.6.4 Customizando o preview

Você pode escrever CSS customizado para o preview nas configurações do VS Code, se desejar.

7.6.5 Exportando Markdown

Com extensões como "Markdown PDF", você pode exportar seus arquivos .md para PDF, HTML, etc. Isso é útil para gerar documentação em outros formatos.

---

7.7 Markdown em Issues e Pull Requests

Ao abrir uma issue ou pull request no GitHub, você pode usar Markdown na descrição e nos comentários. Isso ajuda a estruturar informações:

· Listas de verificação (task lists) para acompanhar progresso.
· Blocos de código com syntax highlighting.
· Menções a usuários.
· Referências a outros issues/PRs com #numero.

7.7.1 Exemplo de issue bem formatada

```markdown
## Descrição do bug
Ao clicar no botão "Salvar", nada acontece.

## Passos para reproduzir
1. Acesse a página de perfil
2. Preencha o campo "Nome"
3. Clique em "Salvar"

## Comportamento esperado
Uma mensagem de sucesso deve aparecer.

## Ambiente
- SO: Windows 10
- Navegador: Chrome 98

## Logs
```

Erro: Cannot read property 'save' of undefined

```
```

7.7.2 Exercício prático 7.4

No seu repositório de testes, abra uma issue fictícia descrevendo um problema qualquer (pode ser inventado). Use Markdown para formatar bem a descrição.

---

7.8 Documentação Além do README

Projetos maiores podem precisar de mais páginas. O GitHub oferece Wikis (repositórios Git separados) que também usam Markdown. Você pode criar páginas interligadas.

Além disso, muitos projetos mantêm uma pasta docs/ na raiz com vários arquivos .md. Ferramentas como MkDocs ou Docusaurus podem gerar sites completos a partir desses arquivos.

7.8.1 Exemplo de estrutura de documentação

```
docs/
├── index.md
├── instalacao.md
├── uso/
│   ├── comandos.md
│   └── exemplos.md
└── contribuicao.md
```

---

7.9 Boas Práticas de Documentação

1. Mantenha a documentação próxima ao código – no mesmo repositório.
2. Atualize junto com o código – quando muda o comportamento, atualize os docs.
3. Seja conciso, mas completo – nem muito prolixo, nem muito superficial.
4. Use exemplos reais – código que realmente funciona.
5. Peça feedback – se alguém tiver dificuldade, sua documentação pode melhorar.
6. Revise a ortografia e gramática – erros passam má impressão.

---

7.10 Exercícios de Fixação

1. Qual a extensão padrão de arquivos Markdown?
2. Como se faz um título de nível 2 em Markdown?
3. Escreva a sintaxe para uma lista ordenada com três itens.
4. Como inserir um link para o Google com o texto "Clique aqui"?
5. Qual a diferença entre código inline e bloco de código?
6. Crie uma tabela com duas colunas (Comando e Descrição) e três linhas de exemplos Git.
7. O que são badges e onde encontrá-las?
8. No VS Code, qual atalho abre o preview do Markdown?
9. Por que é importante manter a documentação atualizada?
10. (Desafio) Pesquise sobre o formato AsciiDoc e compare com Markdown. Em que situações ele pode ser preferível?

---

7.11 Resumo do Capítulo

· Markdown é a linguagem padrão para documentação em repositórios Git.
· A sintaxe básica inclui títulos, listas, ênfase, links, imagens, blocos de código.
· Recursos avançados (tabelas, task lists, emojis) são suportados no GitHub.
· Um bom README segue uma estrutura clara e inclui badges.
· O VS Code oferece preview em tempo real e extensões que facilitam a escrita.
· Issues e pull requests também se beneficiam do Markdown para comunicação eficaz.
· Manter a documentação atualizada é uma prática essencial de profissionalismo.

No próximo capítulo, voltaremos ao Git com foco em repositórios remotos, aprendendo a sincronizar seu trabalho com o GitHub.

---

7.12 Referências

· Markdown Guide
· GitHub Flavored Markdown Spec
· Shields.io – Badges
· Mastering Markdown – GitHub Guides
· Documentação da extensão "Markdown All in One"
· "Writing on GitHub" – GitHub Docs

```
