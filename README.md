# Convertendo LaTeX em Word (.tex em .docx) com github actions

## Primeiro Passo - Conectando o Overleaf com o Github

Crie uma conta em Overleaf.com e github.com

Agora entre no overleaf e dê permissões para o github, conectando as duas contas

Depois, basta criar um projeto no Github e importar ele para o Overleaf, ou vice-versa.
Mais informações, [aqui](https://www.overleaf.com/learn/how-to/Using_Git_and_GitHub#Overleaf_GitHub_Synchronization)


## Segundo Passo - Criando o action

No github, acesse o diretório do projeto e clique em `Actions`.

Lá você irá criar um arquivo .yml com o nome do projeto e copiar o seguinte código:

```actions
name: Compila o LaTeX e converte para Word
on: [push]
jobs:
build_latex:
runs-on: ubuntu-latest
steps:
- name: Set up Git repository
uses: actions/checkout@v1
- name: Compile LaTeX document
uses: xu-cheng/latex-action@master
with:
root_file: artigo.tex
convert_via_pandoc:
runs-on: ubuntu-latest
steps:
- uses: actions/checkout@v2
- run: mkdir output
- uses: docker://pandoc/core:2.9
with:
args: >-
-s comutation-manuscript.tex
-f latex
-t docx
-o output/comutation-manuscript.docx
--bibliography referencias/referencias.bib
--csl fearp.csl
- uses: actions/upload-artifact@master
with:
name: manuscript
path: output
```
Então, fará as alterações necessárias:
 - nome dos arquivos .tex, .bib
 - etc

AINDA NÃO FUNCIONA, ESTOU CRIANDO!

Aceito dicas, rs


## Referências

[r-bloggers - Joshua Cook (2020)](https://www.r-bloggers.com/2020/03/github-actions-for-compiling-and-converting-latex/) 
