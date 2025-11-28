# 🧩 Mixins Essenciais para Views Genéricas

## 📦 `SingleObjectMixin`

Usado para recuperar um objeto único baseado em `pk` ou `slug`.

```python
from django.views.generic.detail import SingleObjectMixin
```

---

## 🧾 `SingleObjectTemplateResponseMixin`

Adiciona suporte de renderização de template com um objeto único.

---

## 📚 `MultipleObjectMixin`

Usado por `ListView` para fornecer queryset múltiplo.

---

## 🔐 `PermissionRequiredMixin`

```python
from django.contrib.auth.mixins import PermissionRequiredMixin

class AdminView(PermissionRequiredMixin, View):
    permission_required = 'app.view_secret'
```

✅ Requer permissão específica para acessar a view.

---

## 🔐 `LoginRequiredMixin`

```python
from django.contrib.auth.mixins import LoginRequiredMixin

class PainelView(LoginRequiredMixin, TemplateView):
    template_name = "painel.html"
```

✅ Redireciona para login se o usuário não estiver autenticado.

---

## 🔎 `UserPassesTestMixin`

```python
from django.contrib.auth.mixins import UserPassesTestMixin

class SuperUserOnlyView(UserPassesTestMixin, View):
    def test_func(self):
        return self.request.user.is_superuser
```

✅ Permite lógica customizada para controlar acesso.
