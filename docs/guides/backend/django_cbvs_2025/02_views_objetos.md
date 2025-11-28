# 📦 Views Baseadas em Objetos (CRUD com Modelos)

## 🔎 `DetailView`

```python
from django.views.generic import DetailView
from .models import Produto

class ProdutoDetailView(DetailView):
    model = Produto
    template_name = "produto_detalhe.html"
```

✅ Exibe os detalhes de um único objeto via `pk` ou `slug`.

---

## 📋 `ListView`

```python
from django.views.generic import ListView
from .models import Produto

class ProdutoListView(ListView):
    model = Produto
    paginate_by = 10  # Paginação automática
```

✅ Lista registros automaticamente com paginação, filtro e ordenação.

---

## ➕ `CreateView`

```python
from django.views.generic.edit import CreateView
from .models import Produto

class ProdutoCreateView(CreateView):
    model = Produto
    fields = ['nome', 'preco']
    success_url = "/produtos/"
```

✅ Cria objetos do model usando um formulário gerado automaticamente.

---

## ✏️ `UpdateView`

```python
from django.views.generic.edit import UpdateView
from .models import Produto

class ProdutoUpdateView(UpdateView):
    model = Produto
    fields = ['nome', 'preco']
    success_url = "/produtos/"
```

✅ Exibe formulário preenchido para editar um objeto existente.

---

## ❌ `DeleteView`

```python
from django.views.generic.edit import DeleteView
from .models import Produto
from django.urls import reverse_lazy

class ProdutoDeleteView(DeleteView):
    model = Produto
    success_url = reverse_lazy("produtos_lista")
```

✅ Mostra página de confirmação e apaga o objeto após confirmação.

---

## 🧾 `FormView`

```python
from django.views.generic.edit import FormView
from .forms import ContatoForm

class ContatoFormView(FormView):
    form_class = ContatoForm
    template_name = "contato.html"
    success_url = "/obrigado/"

    def form_valid(self, form):
        form.enviar_email()
        return super().form_valid(form)
```

✅ Exibe/processa forms customizados **sem ligação com models**.
