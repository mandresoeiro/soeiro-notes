# 🧱 Views Genéricas Simples no Django

## 🧬 `View`

```python
from django.views import View
from django.http import HttpResponse

class HelloWorldView(View):
    def get(self, request):
        return HttpResponse("Olá mundo!")  # sobrescrevendo o método GET
```

✅ View base mais pura — usada quando você quer controle total sobre GET/POST sem mágica.

---

## 🖼️ `TemplateView`

```python
from django.views.generic import TemplateView

class HomePageView(TemplateView):
    template_name = "home.html"  # Apenas renderiza o template
```

✅ Útil para páginas estáticas ou com contexto simples via `get_context_data()`.

---

## 🔀 `RedirectView`

```python
from django.views.generic.base import RedirectView
from django.urls import reverse_lazy

class RedirectToHome(RedirectView):
    url = reverse_lazy("home")  # redireciona para outra URL
```

✅ Usado para redirecionar de uma rota antiga para uma nova.
