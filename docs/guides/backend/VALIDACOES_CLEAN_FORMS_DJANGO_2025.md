# 🧼 Lista Profissional de Validações para `clean()` e `clean_<field>()` em Forms — Django 2025

Guia visual e prático com validações **mais comuns** que você pode (e deve!) aplicar em `forms.Form` e `forms.ModelForm`.

---

## 🔠 1) Campo obrigatório com strip

> Remover espaços e impedir string vazia.

```python
from django import forms
from django.core.exceptions import ValidationError

class MyForm(forms.Form):
    nome = forms.CharField(required=True)

    def clean_nome(self):
        nome = self.cleaned_data.get('nome', '').strip()
        if not nome:
            raise ValidationError("Nome não pode ficar vazio.")
        return nome
```

---

## 🔡 2) Comprimento mínimo e máximo

> Pode usar `min_length` no campo ou validar manualmente.

```python
class MyForm(forms.Form):
    resumo = forms.CharField(min_length=10, max_length=500)

    def clean_resumo(self):
        resumo = self.cleaned_data['resumo']
        if len(resumo) < 10:
            raise ValidationError("Resumo precisa ter pelo menos 10 caracteres.")
        return resumo
```

---

## 🔢 3) Validação com Regex (ex.: CPF)

```python
from django.core.validators import RegexValidator

cpf_validator = RegexValidator(r'^\d{11}$', "CPF deve ter 11 dígitos numéricos.")

class MyForm(forms.Form):
    cpf = forms.CharField(validators=[cpf_validator])
```

---

## 📧 4) Email com domínio restrito

```python
class MyForm(forms.Form):
    email = forms.EmailField()

    def clean_email(self):
        email = self.cleaned_data['email'].lower()
        if email.endswith('@temporal.com'):
            raise ValidationError("Domínio não permitido.")
        return email
```

---

## 🔢 5) Validação numérica com limites

```python
class MyForm(forms.Form):
    idade = forms.IntegerField()

    def clean_idade(self):
        idade = self.cleaned_data['idade']
        if not (0 <= idade <= 120):
            raise ValidationError("Idade inválida.")
        return idade
```

---

## 🔁 6) Verificar unicidade no banco

```python
from django.forms import ModelForm
from .models import Usuario

class UsuarioForm(ModelForm):
    class Meta:
        model = Usuario
        fields = ['email', 'username']

    def clean_email(self):
        email = self.cleaned_data['email'].lower()
        qs = Usuario.objects.filter(email=email)
        if self.instance.pk:
            qs = qs.exclude(pk=self.instance.pk)
        if qs.exists():
            raise ValidationError("Este e-mail já está em uso.")
        return email
```

---

## 🔒 7) Campos relacionados (ex.: senhas)

```python
class RegistroForm(forms.Form):
    senha = forms.CharField(widget=forms.PasswordInput)
    senha_confirm = forms.CharField(widget=forms.PasswordInput)

    def clean(self):
        cleaned = super().clean()
        if cleaned.get('senha') != cleaned.get('senha_confirm'):
            raise ValidationError("As senhas não coincidem.")
        return cleaned
```

---

## 🖼️ 8) Arquivo: tamanho, tipo e dimensões

```python
from PIL import Image

class UploadForm(forms.Form):
    imagem = forms.ImageField()

    def clean_imagem(self):
        imagem = self.cleaned_data['imagem']
        if imagem.size > 2*1024*1024:
            raise ValidationError("Imagem maior que 2MB.")
        if imagem.content_type not in ('image/jpeg', 'image/png'):
            raise ValidationError("Formato inválido. Use JPG ou PNG.")
        w, h = Image.open(imagem).size
        if w < 800 or h < 600:
            raise ValidationError("Resolução mínima 800x600.")
        return imagem
```

---

## 📅 9) Datas (intervalos válidos)

```python
from django.utils import timezone

class EventoForm(forms.Form):
    data_inicio = forms.DateField()
    data_fim = forms.DateField()

    def clean(self):
        cleaned = super().clean()
        inicio, fim = cleaned.get('data_inicio'), cleaned.get('data_fim')
        if inicio and fim:
            if fim < inicio:
                raise ValidationError("Data de fim deve ser depois do início.")
            if inicio < timezone.now().date():
                raise ValidationError("Data de início no passado.")
        return cleaned
```

---

## ✅ 10) Validar ChoiceField

```python
class PedidoForm(forms.Form):
    metodo_pagamento = forms.ChoiceField(choices=[('cc','Cartão'),('boleto','Boleto')])

    def clean_metodo_pagamento(self):
        val = self.cleaned_data['metodo_pagamento']
        return val
```

---

## 🔀 11) Campo condicional

```python
class ExemploForm(forms.Form):
    tipo = forms.ChoiceField(choices=[('A','A'),('B','B')])
    detalhe = forms.CharField(required=False)

    def clean(self):
        cleaned = super().clean()
        if cleaned.get('tipo') == 'B' and not cleaned.get('detalhe'):
            raise ValidationError({'detalhe': "Detalhe é obrigatório quando tipo = B."})
        return cleaned
```

---

## 🔁 12) Lista de valores sem duplicata

```python
class TagsForm(forms.Form):
    tags = forms.CharField()

    def clean_tags(self):
        tags = [t.strip() for t in self.cleaned_data['tags'].split(',') if t.strip()]
        if len(tags) != len(set(tags)):
            raise ValidationError("Tags duplicadas detectadas.")
        return tags
```

---

## ♻️ 13) Validators reutilizáveis

```python
def validar_positivo(value):
    if value <= 0:
        raise ValidationError("Valor deve ser positivo.")

class ProdutoForm(forms.Form):
    preco = forms.DecimalField(validators=[validar_positivo], error_messages={'invalid': 'Preço inválido.'})
```

---

## 🚧 14) Campo vs erro geral

```python
# raise ValidationError({'campo': "Erro do campo"})
# raise ValidationError("Erro geral do formulário")
```

---

## 🧩 15) Validação em Formsets

```python
from django.forms import BaseFormSet, formset_factory

class BaseItemFormSet(BaseFormSet):
    def clean(self):
        if any(self.errors): return
        nomes = []
        for form in self.forms:
            nome = form.cleaned_data.get('nome')
            if nome in nomes:
                raise ValidationError("Itens duplicados.")
            nomes.append(nome)
```

---

## 🧼 16) Sanitização (acentos, case...)

```python
import unicodedata

def remover_acentos(s):
    return ''.join(c for c in unicodedata.normalize('NFKD', s) if not unicodedata.combining(c))

class NomeForm(forms.Form):
    nome = forms.CharField()

    def clean_nome(self):
        nome = remover_acentos(self.cleaned_data['nome'].strip()).title()
        return nome
```

---

## 🌐 17) Integração com API externa (ex.: CEP)

```python
import requests

def validar_cep_via_api(cep):
    r = requests.get(f'https://viacep.com.br/ws/{cep}/json/', timeout=5)
    if r.status_code != 200 or 'erro' in r.json():
        raise ValidationError("CEP inválido ou não encontrado.")
    return r.json()

class EnderecoForm(forms.Form):
    cep = forms.CharField()

    def clean_cep(self):
        return validar_cep_via_api(self.cleaned_data['cep'])
```

---

## 🧠 18) Boas práticas

- ✅ Sempre chame `super().clean()`
- ✅ Retorne valor em `clean_<field>()`
- ♻️ Reuse validadores onde possível
- 🌍 Use `gettext_lazy` para mensagens se multilíngue
- 📦 Validações pesadas? Use Celery ou background
- 🔄 Separe lógica complexa em services/testáveis

---

Checklist para Forms limpos, seguros e escaláveis ✅
