# How to use forms with django-bootstrap5
<a href="https://github.com/zostera/django-bootstrap5" target="_blank">github</a> | <a href="https://django-bootstrap5.readthedocs.io/en/stable/" target="_blank">readthedocs</a>

## Simple Form with django-bootstrap5

``` py title="forms.py"
class SimpleForm(forms.Form)
    """Simple Form or ModelForm field displayed as defined in this class"""

    timestamp = forms.DateTimeField(
        required=True,
        widget=DateTimePickerInput(attrs={"class": "form-control"}),
    )
    ride_title = forms.CharField(
        label="Ride Title",
        max_length=200,
        required=False,
    )
    distance = forms.FloatField(
        label="Distance",
        min_value=0,
        required=True,
    )
    duration = forms.DurationField(
        label="Ride Duration",
        help_text="h:m:s",
        required=True,
    )
    elevation = forms.IntegerField(
        label="Elevation Gained",
        min_value=0,
        required=False,
    )
    calories = forms.IntegerField(
        label="Calories",
        min_value=0,
        required=False,
    )
```

``` py title="view.py"
class SimpleCreateView(LoginRequiredMixin, CreateView)
    """Simple CreateView.  Do your normal stuff here"""

    model = Doc
    success_url = reverse_lazy("habits:list")
    form_class = HabitForm
    template_name = "template/dj_bs5.html"

    ...
    ...
```

``` html title="template/dj_bs5.html" hl_lines="2 8 13"
{% extends "include/base.html" %}
{% load django_bootstrap5 %}

{% block content %}
<div class="container">
    <h2>Your Form</h2>

    {{ form.media }}

    <form method="post">
        {% csrf_token %}

        {% bootstrap_form form %} <!--displays all fields as defined in forms.py-->

        <button type="submit">Save Changes</button>
    </form>
</div>
{% endblock content}
```

## Custom Form with django-bootstrap5

``` html title="template/define_each_field.html" hl_lines="2 8 13-17"
{% extends "include/base.html" %}
{% load django_bootstrap5 %}

{% block content %}
<div class="container">
    <h2>Your Form</h2>

    {{ form.media }}

    <form method="post">
        {% csrf_token %}

        {% bootstrap_form_errors form %}
        {% bootstrap_field form.username %}
        {% bootstrap_field form.email %}
        {% bootstrap_field form.password1 addon_after="<i class='bi bi-eye-slash' id='togglePassword1' onclick='togglePassword1()''></i>" %}
        {% bootstrap_field form.password2 addon_after="<i class='bi bi-eye-slash' id='togglePassword2' onclick='togglePassword2()''></i>" %}

        <button type="submit">Save Changes</button>

    </form>
</div>
{% endblock content}
```
