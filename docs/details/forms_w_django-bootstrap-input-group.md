# How to use forms with django-bootstrap-input-group  
<a href="https://pypi.org/project/django-bootstrap-input-group/" target="_blank">pypi.org</a> | <a href="https://github.com/Actionb/django-bootstrap-input-group" target="_blank">github</a>  

## Define Field_group in FormClass

``` py title="forms.py" hl_lines="54-61"
class RideForm(ModelForm): 

    class Meta:
        model = Activity
        exclude = (
            ...
        ) 
    
    timestamp = forms.DateTimeField(
        required=True,
        widget=DateTimePickerInput(
            attrs={"class": "form-control"},
            options={
                "format": "MM/DD/YYYY hh:mm A",
                "showClose": True,
                "showClear": True,
            },
        ),
    )
    ride_name = forms.CharField(
        label="Ride Name",
        max_length=200,
        required=True,
    )
    distance = forms.FloatField(
        label="Distance",
        min_value=0,
        required=True,
    )
    unit_distance = forms.ChoiceField(
        choices=[("kilometers", "kilometers"), ("miles", "miles")],
        label="Unit of Measurement",
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
    unit_elevation = forms.ChoiceField(
        choices=[("meters", "meters"), ("feet", "feet")], label="Unit of Measurement"
    )
    calories = forms.IntegerField(
        label="Calories",
        min_value=0,
        required=False,
    )

    # define fields to be used and their order and their grouping
    field_groups = [
        "timestamp",
        "ride_name",
        ("Distance", ("distance", "unit_distance")),
        "duration",
        ("Elevation", ("elevation", "unit_elevation")),
        "calories",
    ]

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

``` html title="template/dj_bs_input_group.html" hl_lines="3 9 14"
{% extends "include/base.html" %}
<!-- load extra input_group template tags in additon -->
{% load django_bootstrap5 django_bootstrap_input_group %}

{% block content %}
<div class="container">
    <h2>Your Form</h2>

    {{ form.media }}

    <form method="post">
        {% csrf_token %}

        {% bootstrap_grouped_form form layout=layout %}

        <button type="submit">Save Changes</button>
    </form>
</div>

{% endblock content %}
```