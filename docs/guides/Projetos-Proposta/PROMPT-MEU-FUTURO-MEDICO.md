📄 PROMPT-MEU-FUTURO-MEDICO.md

(copie tudo abaixo e salve como PROMPT-MEU-FUTURO-MEDICO.md)

# 🚀 Meu Futuro Médico — Super Prompt para Gerar o Projeto Completo
Versão profissional para iniciar um sistema Django + DRF + Tailwind com Dashboard, Sidebar, Cards Interativos e Simulador de Chances de Medicina.

## 🎯 Objetivo Geral
Gerar um projeto profissional completo chamado **meu-futuro-medico**, com backend em Django + DRF e frontend HTML/Tailwind (ou React no futuro), contendo:

- Dashboard com cards das fases do caminho médico  
- Sidebar profissional  
- Sistema de perfil com foto  
- Sistema de trilhas, rotas e progresso  
- Cards interativos (não arrastáveis ainda)  
- Simulador de chances (frontend + API base)  
- Dados mockados de faculdades, notas ENEM e estados  
- Autenticação completa (login, registro, JWT opcional)  
- Estrutura modular para crescer sem precisar refazer  
- Scripts automáticos  
- Documentação MkDocs  

---

# 📦 Estrutura do Projeto (que o modelo deve gerar)



meu-futuro-medico/
│
├── backend/
│ ├── core/
│ │ ├── settings/
│ │ │ ├── base.py
│ │ │ ├── dev.py
│ │ │ ├── prod.py
│ │ ├── urls.py
│ │ ├── wsgi.py
│ │ ├── asgi.py
│ │
│ ├── apps/
│ │ ├── accounts/
│ │ ├── dashboard/
│ │ ├── simulation/
│ │ ├── colleges/
│ │ └── progress/
│ │
│ ├── manage.py
│ ├── pyproject.toml (Poetry)
│ ├── scripts/
│ │ ├── bootstrap.sh
│ │ └── create_admin.py
│ └── docs/
│ ├── index.md
│ └── arquitetura.md
│
└── frontend/ (HTML + Tailwind ou React se ativado)
├── templates/
├── static/
└── components/


---

## 🧱 Módulos que devem ser criados

### 1. **accounts/**
- Modelo User com foto de perfil  
- Registro, login, logout  
- API para perfil  
- Painel do usuário  

### 2. **dashboard/**
Tela principal contendo:

- 📘 Conhecimento Base  
- 📚 Conteúdos por estado  
- 📊 Análise de chances  
- 🧠 Rotina personalizada  
- 🎯 Checklists  
- 🧬 Trilha médica (passo a passo)  

### 3. **simulation/**  
Simulador de chances ENEM Medicina:

- Registrar notas  
- Comparar estado  
- Gerar % de chance  
- Recomendações automáticas  
- API para consultas  

### 4. **colleges/**  
Base mockada com:

- Nome da faculdade  
- Estado  
- Nota de corte  
- Modalidades (Ampla, Cota, ProUni)  

### 5. **progress/**  
Registrar:

- Conclusão de cards  
- Fases concluídas  
- Último acesso  
- Checklist pessoal  

---

# 🎨 Layout que o modelo deve gerar

### Sidebar
- Ícones alinhados à esquerda  
- Tema escuro e claro  
- Foto do usuário no topo  
- Navegação:



🏠 Dashboard
🧬 Jornada Médica
📊 Simulador
🎯 Progresso
🎓 Faculdades
⚙️ Configurações


---

# 🖥️ Dashboard (cards iniciais)

- "O Caminho para Medicina"  
- "Notas de Corte 2025"  
- "Simular Minhas Chances"  
- "Estados e Universidades"  
- "Plano de Estudo Inteligente"  
- "Comparação Nacional"  
- "Metas Semanais"  
- "Checklist da Aprovação"  

Cada card deve ter:
- Título  
- Descrição  
- Botão de acesso  
- Estado de conclusão (0%, 50%, 100%)  

---

# 🧠 Regras para o Backend

1. Usar Django + DRF  
2. Criar APIs REST organizadas por app  
3. Rotas com versionamento: `/api/v1/...`  
4. Incluir documentação automática com **drf-spectacular**  
5. Incluir autenticação (session + JWT opcional)  
6. Usar Poetry como gerenciador  
7. Usar Tailwind para estilização  
8. Preparar migração futura para React  

---

# 📚 Documentação MkDocs

Criar arquivo:



docs/index.md
docs/arquitetura.md
docs/rotas.md


Tema: **mkdocs-material**

---

# 💬 Comando final do prompt

**Gerar agora o projeto completo Meu Futuro Médico com tudo acima, incluindo:**

- Código em Python/Django  
- Templates HTML + Tailwind  
- APIs DRF  
- Estrutura de pastas  
- Scripts  
- Mock de dados  
- Documentação  
- Comentários explicativos  
- ZIP final pronto para download  

> **IMPORTANTE:** Não resuma, não simplifique. Gere tudo completo e funcional.  