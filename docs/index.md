## Site list
{% assign doclist = site.pages | sort: 'url'  %}
{% for doc in doclist %}
       {% if doc.name contains '.md' or doc.name contains '.html' %}
              - ["{{ doc.name }}"](tdd.1024ping.xyz/{{ doc.name }})
       {% endif %}
{% endfor %}
