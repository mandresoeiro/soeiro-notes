# Guia de Uso: Home & Work

Este guia explica como utilizar este repositório tanto em casa (home) quanto no trabalho (work), além de como configurar GitHub Actions e publicar o conteúdo com GitHub Pages.

## 1. Introdução

Este repositório contém anotações, guias e materiais de referência para uso pessoal e profissional. O objetivo é facilitar o acesso e a atualização dos conteúdos em diferentes ambientes.

## 2. Como usar em casa (home)

- Clone o repositório normalmente:
  ```sh
  git clone https://github.com/mandresoeiro/soeiro-notes.git
  ```
- Instale dependências, se necessário (ex: Python, mkdocs):
  ```sh
  pip install -r docs/requirements.txt
  ```
- Edite e adicione novos conteúdos conforme sua necessidade.

## 3. Como usar no trabalho (work)

- Repita o processo de clonagem e instalação acima.
- Mantenha as anotações sincronizadas usando `git pull` e `git push`.
- Utilize branches para separar conteúdos sensíveis, se necessário.

## 4. GitHub Actions

- O repositório pode usar GitHub Actions para automatizar tarefas, como build e deploy do site.
- Exemplo de workflow (em `.github/workflows/gh-pages.yml`):
  ```yaml
  name: Deploy to GitHub Pages
  on:
    push:
      branches: [main]
  jobs:
    deploy:
      runs-on: ubuntu-latest
      steps:
        - uses: actions/checkout@v4
        - uses: actions/setup-python@v5
          with:
            python-version: '3.x'
        - run: pip install mkdocs mkdocs-material
        - run: mkdocs gh-deploy --force
  ```

## 5. Publicando com GitHub Pages

- O conteúdo do repositório pode ser publicado automaticamente usando o comando:
  ```sh
  mkdocs gh-deploy --force
  ```
- O site ficará disponível em: `https://mandresoeiro.github.io/soeiro-notes/`

---

Mantenha este guia atualizado conforme novas necessidades surgirem.
