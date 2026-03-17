```markdown'''
# Git e GitHub: Do Iniciante ao Profissional com VS Code

**Autor: Haroldo Capucci**

---

## Capítulo 15: Projeto Prático 1 – Gerenciando um TCC ou Artigo Científico com Git

**Páginas estimadas:** 22  
**Tempo de leitura:** 60–75 minutos  
**Objetivos do capítulo:**  
- Aplicar os conceitos de Git e GitHub no contexto acadêmico  
- Configurar um repositório para um trabalho de conclusão de curso (TCC)  
- Utilizar branches para organizar versões (rascunho, revisão, final)  
- Colaborar com orientadores e colegas usando Issues e Pull Requests  
- Gerenciar referências bibliográficas com Git  
- Automatizar a geração do PDF do trabalho  
- Versionar documentos do Office (Word, Excel) com Git LFS  
- Publicar o trabalho final no GitHub Pages  

---

## 15.1 Introdução

O Trabalho de Conclusão de Curso (TCC) é um dos maiores desafios acadêmicos. Envolve pesquisa, escrita, revisões, formatação e, muitas vezes, colaboração com orientador e colegas. Tradicionalmente, isso é feito com dezenas de arquivos `versao_final.docx`, `versao_revisada.docx`, `versao_final_mesmo.docx`, enviados por e-mail – um pesadelo de versionamento.

O Git, combinado com o GitHub, pode transformar esse processo em algo organizado, rastreável e seguro. Neste capítulo, você aprenderá a aplicar todo o conhecimento adquirido para gerenciar um TCC (ou qualquer artigo científico) de forma profissional.

---

## 15.2 Configurando o Repositório para um Trabalho Acadêmico

### 15.2.1 Estrutura de pastas sugerida

Antes de mais nada, defina uma estrutura organizada. Exemplo:

```

tcc/
├── README.md
├── .gitignore
├── texto/
│   ├── capitulos/
│   │   ├── 01-introducao.md
│   │   ├── 02-revisao.md
│   │   ├── 03-metodologia.md
│   │   ├── 04-resultados.md
│   │   └── 05-conclusao.md
│   ├── pre-textuais/
│   │   ├── resumo.md
│   │   ├── abstract.md
│   │   └── sumario.md
│   ├── pos-textuais/
│   │   ├── apendices.md
│   │   └── anexos.md
│   └── referencias.bib
├── imagens/
│   ├── figura1.png
│   └── figura2.svg
├── dados/
│   └── planilha-resultados.xlsx
├── scripts/
│   └── analise.R
└── output/
└── tcc.pdf (gerado automaticamente)

```

### 15.2.2 Criando o repositório

```bash
mkdir tcc
cd tcc
git init
git branch -m main
```

Crie os arquivos iniciais (README.md, .gitignore) e faça o primeiro commit:

```bash
echo "# Meu TCC" > README.md
git add README.md
git commit -m "docs: adiciona README inicial"
```

15.2.3 Configurando o .gitignore

Para um TCC, você pode querer ignorar arquivos temporários e de output:

```
# Arquivos temporários
*.bak
*.swp
*.tmp

# PDFs gerados (se forem sempre gerados por script)
/output/

# Dados sensíveis (se houver)
/dados/privado/

# Arquivos do sistema
.DS_Store
Thumbs.db
```

15.2.4 Criando a estrutura de pastas

```bash
mkdir -p texto/capitulos texto/pre-textuais texto/pos-textuais imagens dados scripts output
```

Adicione arquivos placeholder para cada capítulo (opcional). Depois, commit:

```bash
git add .
git commit -m "chore: adiciona estrutura inicial do TCC"
```

---

15.3 Usando Branches para Revisões e Versões

No desenvolvimento de um TCC, você terá diferentes estágios:

· Rascunho: primeira versão, ainda bruta.
· Revisão: após feedback do orientador.
· Final: versão entregue.
· Banca: versão com correções pós-banca.

Você pode usar branches para organizar isso.

15.3.1 Branch principal: main (versão final)

A branch main conterá a versão mais atualizada e aprovada do trabalho. Inicialmente, pode estar vazia ou com a estrutura.

15.3.2 Branch de desenvolvimento: dev (rascunho)

Crie uma branch dev para trabalhar nos rascunhos:

```bash
git switch -c dev
```

Agora você pode escrever à vontade, fazer commits frequentes, sem medo de "quebrar" a versão estável.

15.3.3 Branches para revisões específicas

Quando receber feedback do orientador, crie uma branch para aquela revisão:

```bash
git switch -c revisao-orientador-2025-03-20
```

Isso permite que você experimente as correções sem afetar o fluxo principal da dev.

15.3.4 Mesclando após aprovação

Quando uma revisão for aprovada, mescle-a na dev e depois, quando estiver pronto para uma versão "quase final", mescle na main e crie uma tag.

```bash
git switch dev
git merge revisao-orientador-2025-03-20
git tag -a v0.9 -m "Versão pré-banca"
git switch main
git merge dev
git tag -a v1.0 -m "Versão final para banca"
```

15.3.5 Exercício prático 15.1

Crie as branches dev e revisao1 no seu repositório de TCC. Faça algumas alterações em cada uma e pratique os merges. Use git log --graph --oneline para visualizar o histórico.

---

15.4 Colaboração com Orientadores e Colegas

O GitHub facilita a colaboração com orientadores e colegas, mesmo que eles não conheçam Git profundamente (eles podem usar a interface web).

15.4.1 Convidando colaboradores

No repositório do GitHub, vá em Settings → Collaborators and teams → Add people. Adicione o e-mail do seu orientador. Ele receberá um convite e poderá acessar o repositório (se for privado, precisa de conta GitHub).

15.4.2 Orientador revisando via Issues

O orientador pode abrir Issues apontando problemas ou sugestões. Exemplo:

Título: Revisão do Capítulo 2
Descrição: Na seção 2.3, a explicação sobre metodologia ficou confusa. Sugiro reescrever focando nos passos práticos. Veja o artigo X como referência.

Você pode responder, marcar como resolvida quando corrigir.

15.4.3 Pull Requests para revisões formais

Se o orientador quiser revisar alterações, ele pode fazer um fork (se não for colaborador) ou vocês podem usar Pull Requests. Você cria uma branch com as alterações, abre um PR e o orientador comenta diretamente nas linhas do código (texto). Isso é extremamente útil para revisões detalhadas.

15.4.4 Usando GitHub Discussions para debates

Para discussões mais amplas (escolha do tema, metodologia), ative as Discussions no repositório. É um fórum integrado.

15.4.5 Exercício prático 15.2

Convide um colega para colaborar em um repositório de teste. Peça que ele abra uma issue sugerindo uma melhoria. Depois, crie uma branch, implemente a melhoria e abra um Pull Request. Simule o processo de revisão com comentários.

---

15.5 Gerenciando Referências Bibliográficas

Referências são parte crucial de um TCC. O formato mais adequado para versionamento é o BibTeX (arquivo .bib).

15.5.1 Criando um arquivo referencias.bib

Exemplo de entrada:

```bibtex
@article{knuth1984,
  author  = {Donald E. Knuth},
  title   = {Literate Programming},
  journal = {The Computer Journal},
  year    = {1984},
  volume  = {27},
  number  = {2},
  pages   = {97--111}
}
```

15.5.2 Versionando o .bib

O arquivo .bib é texto puro, perfeito para Git. Cada vez que você adiciona uma referência, faz um commit. O histórico mostra exatamente quando e por que cada referência foi incluída.

15.5.3 Usando referências no texto

Se você escreve em Markdown/LaTeX, pode citar as referências com @knuth1984 e depois usar o Pandoc + filtro pandoc-citeproc para gerar a bibliografia formatada (ABNT, APA, etc.). Veremos isso na automação.

15.5.4 Ferramentas auxiliares

· Zotero ou Mendeley podem exportar em BibTeX. Mantenha o arquivo .bib sincronizado com o repositório.
· JabRef é um gerenciador de referências open source que trabalha diretamente com .bib.

15.5.5 Exercício prático 15.3

Crie um arquivo referencias.bib com três referências de artigos ou livros da sua área. Adicione ao repositório e faça commit.

---

15.6 Automatizando a Geração do PDF

Um dos maiores ganhos de produtividade é gerar o PDF automaticamente sempre que você faz uma alteração, usando GitHub Actions.

15.6.1 Pré-requisitos

· Os capítulos em Markdown (ou LaTeX).
· Um arquivo mestre que os combine (ex: tcc.md que inclui os capítulos via !include ou simplesmente concatenando).
· Pandoc e LaTeX disponíveis (usaremos container).

15.6.2 Workflow de geração

Já vimos um exemplo similar no capítulo 14. Vamos adaptar para o TCC:

```yaml
name: Gerar PDF do TCC

on:
  push:
    branches: [ main ]
    paths:
      - 'texto/**'
      - 'referencias.bib'
  workflow_dispatch:

jobs:
  build-pdf:
    runs-on: ubuntu-latest
    container:
      image: pandoc/latex:latest

    steps:
      - uses: actions/checkout@v4

      - name: Concatenar capítulos
        run: |
          cat texto/pre-textuais/*.md > tcc-completo.md
          cat texto/capitulos/*.md >> tcc-completo.md
          cat texto/pos-textuais/*.md >> tcc-completo.md

      - name: Gerar PDF
        run: |
          pandoc tcc-completo.md \
            --from markdown \
            --to pdf \
            --output tcc.pdf \
            --pdf-engine=xelatex \
            --bibliography=referencias.bib \
            --citeproc \
            --csl=abnt.csl  # se tiver um arquivo de estilo ABNT

      - name: Upload do PDF
        uses: actions/upload-artifact@v4
        with:
          name: tcc-pdf
          path: tcc.pdf
```

15.6.3 Adicionando estilo ABNT

Você precisa de um arquivo CSL (Citation Style Language) para o formato ABNT. Baixe de https://github.com/citation-style-language/styles (procure por abnt.csl) e coloque na raiz do repositório. No workflow, referencie com --csl=abnt.csl.

15.6.4 Gerando release com PDF

Assim como no capítulo 14, você pode adicionar um step que cria uma release e anexa o PDF quando uma tag é criada.

15.6.5 Exercício prático 15.4

Implemente o workflow acima no seu repositório de TCC (ou teste em um repositório separado). Faça um push na branch main e veja o PDF ser gerado e disponibilizado como artefato.

---

15.7 Versionando Documentos do Office (com Git LFS)

Arquivos binários como .docx, .xlsx, .pptx não são ideais para o Git, pois não permitem diff e incham o repositório. Mas às vezes são necessários (ex: planilha de dados, questionários).

A solução é o Git Large File Storage (LFS) , que substitui os arquivos por ponteiros e armazena o conteúdo em um servidor separado.

15.7.1 Instalando Git LFS

· Windows: Baixe o instalador em https://git-lfs.com.
· macOS: brew install git-lfs
· Linux: Use o gerenciador de pacotes (ex: sudo apt install git-lfs).

Depois, em cada repositório, inicie:

```bash
git lfs install
```

15.7.2 Rastreando arquivos com LFS

```bash
git lfs track "*.docx"
git lfs track "*.xlsx"
git lfs track "*.pdf"
```

Isso cria/atualiza o arquivo .gitattributes. Adicione e commit:

```bash
git add .gitattributes
git commit -m "chore: configura Git LFS para documentos Office"
```

Agora, ao adicionar arquivos .docx, eles serão gerenciados pelo LFS.

15.7.3 Limitações

· O GitHub oferece 1 GB de armazenamento LFS gratuito e 1 GB de largura de banda mensal. Para TCCs, é suficiente.
· Colaboradores também precisam ter Git LFS instalado para clonar corretamente.

15.7.4 Alternativa: converter para Markdown

Sempre que possível, prefira formatos texto. Por exemplo, planilhas podem ser exportadas para CSV. Isso evita o LFS.

15.7.5 Exercício prático 15.5

Crie um arquivo .docx de teste, configure o Git LFS no repositório, adicione o arquivo e faça push. Depois, clone o repositório em outra pasta e verifique se o arquivo foi baixado corretamente.

---

15.8 Publicando o Trabalho com GitHub Pages

Você pode publicar uma versão web do seu TCC (HTML) usando GitHub Pages . Isso é ótimo para compartilhar com a banca ou como portfólio.

15.8.1 Convertendo para HTML

Com Pandoc, você pode gerar HTML em vez de PDF:

```bash
pandoc tcc-completo.md --to html --output docs/index.html --bibliografia referencias.bib --citeproc --csl=abnt.csl
```

15.8.2 Configurando o Pages

1. Crie uma pasta docs/ na raiz.
2. Coloque o index.html e os recursos (CSS, imagens) lá.
3. No GitHub, vá em Settings → Pages.
4. Em "Branch", selecione main e a pasta /docs.
5. Salve. Seu site estará disponível em https://haroldocapucci.github.io/nome-do-repo/.

15.8.3 Automatizando com Actions

Você pode criar um workflow que gera o HTML e publica no Pages automaticamente. O GitHub tem uma action própria: peaceiris/actions-gh-pages.

```yaml
- name: Deploy para GitHub Pages
  uses: peaceiris/actions-gh-pages@v4
  with:
    github_token: ${{ secrets.GITHUB_TOKEN }}
    publish_dir: ./docs
    publish_branch: gh-pages
```

15.8.4 Exercício prático 15.6

Crie uma versão HTML simples do seu TCC (pode ser apenas o resumo) e publique no GitHub Pages. Compartilhe o link.

---

15.9 Dicas Extras para TCC com Git

15.9.1 Commits semânticos

Use Conventional Commits para manter o histórico organizado:

· docs: adiciona introdução
· fix: corrige erro na seção 3.2
· refactor: reorganiza capítulo 4
· feat: adiciona gráfico de resultados

15.9.2 Backup automático

Com o GitHub, seu TCC já está backupado na nuvem. Mas você pode fazer push automático periódico com um cron job (não recomendado para evitar conflitos).

15.9.3 Trabalhando offline

O Git é distribuído: você pode trabalhar no metrô, fazer commits, e depois sincronizar. Perfeito para quem não tem internet sempre.

15.9.4 Controle de versão de imagens

Imagens também são binárias. Considere usar LFS para pastas de imagens, mas prefira formatos leves (SVG, PNG otimizado).

15.9.5 Template de TCC

Crie um template com a estrutura e compartilhe com colegas. Você pode fazer um fork do template e adaptar.

---

15.10 Exercícios de Fixação

1. Como você organizaria as branches para um TCC com versões: rascunho, revisão orientador, versão banca, versão final?
2. Qual a vantagem de usar Issues para comunicação com o orientador?
3. Por que o formato BibTeX é mais adequado para versionamento do que um arquivo do Word com referências?
4. Descreva um workflow do GitHub Actions que gere o PDF do TCC automaticamente.
5. O que é Git LFS e quando usá-lo em um TCC?
6. Como você publicaria seu TCC em formato web usando GitHub Pages?
7. Crie um exemplo de mensagem de commit seguindo o padrão Conventional Commits para a adição de um novo capítulo.
8. (Desafio) Configure um repositório completo para um TCC fictício, incluindo estrutura de pastas, branches, um workflow de PDF e um script simples de análise de dados em R ou Python.

---

15.11 Resumo do Capítulo

· Um repositório Git bem estruturado é ideal para gerenciar TCCs.
· Branches permitem organizar rascunhos, revisões e versões finais.
· Issues e Pull Requests facilitam a colaboração com orientadores.
· Referências em BibTeX são versionáveis e integráveis à geração de PDF.
· GitHub Actions automatiza a compilação do PDF a cada alteração.
· Git LFS resolve o problema de arquivos binários grandes.
· GitHub Pages oferece uma versão web do trabalho.

Agora você pode aplicar esses conceitos ao seu próprio TCC e impressionar a banca com a organização e profissionalismo. No próximo capítulo, veremos como contribuir com projetos open source, outro grande uso do Git e GitHub.

---

15.12 Referências

· Pro Git Book – Capítulos sobre Git LFS e GitHub
· GitHub Docs: "Git Large File Storage"
· GitHub Docs: "GitHub Pages"
· Pandoc User Guide
· Citation Style Language (CSL) – abnt.csl
· Conventional Commits

```
