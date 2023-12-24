## Site list
{% assign doclist = site.pages | sort: 'url'  %}
{% for doc in doclist %}
       {% if doc.name contains '.md' or doc.name contains '.html' %}
              ["{{ doc.name }}"](https://tdd.1024ping.xyz{{ doc.url }})
       {% endif %}
{% endfor %}
