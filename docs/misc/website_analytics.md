# Website Analytics with Umami

![umami](../assets/icons/umami.png){: width="25%"}

- <a href="https://umami.is/" target="_blank">https://umami.is/</a>
- <a href="https://us.umami.is/dashboard" target="_blank">https://us.umami.is/dashboard</a>
- <a href="https://umami.is/docs" target="_blank">https://umami.is/docs</a>

``` python title="include/_head.html"
<!-- Analytics -->
{% if ENVIRONMENT_NAME == "Production" %}
    <script defer src="https://cloud.umami.is/script.js" data-website-id="********************"></script>
{% endif %}
```

**Script is only enabled for production environment*
