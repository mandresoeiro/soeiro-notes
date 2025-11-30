# GitHub Copilot — Guia Completo de Configuração e Uso  
*Autor: Soeirotech*

---

## 📌 1. Introdução

Este guia ensina a configurar e usar o **GitHub Copilot Pro** de maneira profissional.  
Abrange instalação, autenticação, configuração no VS Code e controle de consumo de requisições premium.

---

## 🧩 2. Verificar o estado da assinatura

Acesse:

- https://github.com/settings/copilot

Você verá:

- Status da assinatura (Pro / Individual / Business)
- Uso de Premium Requests
- Recursos habilitados (Editor, Chat, CLI)
- Data de renovação mensal

---

## ⚙️ 3. Instalação no VS Code

### 3.1 Instalar extensões
No VS Code:

1. Pressione `Ctrl + Shift + X`
2. Instale:
   - **GitHub Copilot**
   - **GitHub Copilot Chat**

---

## 🔐 4. Autenticação

1. No canto inferior esquerdo do VS Code, clique no ícone de conta
2. Clique em **Sign in to GitHub**
3. Confirme a permissão
4. Verifique se aparece sua foto no rodapé

---

## 🧠 5. Verificar status do Copilot

Abra a paleta:

```
Ctrl + Shift + P
```

Digite:

```
Copilot: Status
```

Esperado:

```
✔️ GitHub Copilot: Enabled
```

---

## 🛠️ 6. Configurações recomendadas

**Settings → Extensions → GitHub Copilot**

Ativar:

- Inline Suggestions ✔️
- Chat in Editor ✔️
- Edit & Fix ✔️
- Suggestion Delay: 50–150ms

Desativar (se quiser economizar):

- Auto-trigger no Chat

---

## 📉 7. Controle de consumo

Copilot usa “Premium Requests”.  
Recomendações:

- Use autocomplete para tarefas pequenas
- Use Chat apenas quando necessário
- Evite pedir refatoração de projetos inteiros
- Trabalhe em blocos de código pequenos
- Evite prompts longos demais

---

## 🧪 8. Usando Copilot de forma profissional

### 8.1 Para gerar código
> “Implemente um `UserService` em Python com princípios SOLID, tipagem forte e docstrings no padrão Google.”

### 8.2 Para refatorar
> “Refatore este trecho mantendo a lógica, reduzindo complexidade e adicionando comentários concisos.”

### 8.3 Para explicar
> “Explique este algoritmo em 5 tópicos, focando em tempo de execução e possíveis gargalos.”

---

## 📚 9. Copilot Chat no GitHub.com

Permite conversar sobre:

- Pull requests
- Commits
- Códigos específicos
- Arquivos inteiros do repositório

---

## 🧰 10. Copilot CLI

Ative em:

```
npm install -g @githubnext/github-copilot-cli
```

Comandos úteis:

```
gh copilot explain "comando"
gh copilot suggest
gh copilot fix
```

---

## 🏁 11. Conclusão

Com este guia você tem:

- Configuração completa  
- Controle de consumo  
- Boas práticas de uso  
- Fluxo profissional de desenvolvimento com IA  

Soeirotech now codes faster, cleaner and sharper. 🦾🔥
