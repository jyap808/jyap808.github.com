---
layout: post
title: Using Anonymous Structs to pass data to templates in GoLang
date: 2013-09-23 22:40
---

One thing that is quite common with Python web frameworks like Django, Flask or Bottle is passing multiple objects to a view.

Something like this in Django is common where a context dictionary with multiple objects is passed back to the template for rendering:
```python
from django.shortcuts import render

def my_view(request):
        context = {'poll': p, 'error_message': "You didn't select a choice.",}
        return render(request, 'polls/detail.html', context)
```

While reading through some examples in GoLang is seemed strange that all the tutorials and examples only passed a single object back to the template.

Here is an example:
```go
package main

import (
    "html/template"
    "net/http"
    "strings"
)

type Paste struct {
    Expiration string
    Content    []byte
    UUID       string
}

func pasteHandler(w http.ResponseWriter, r *http.Request) {
    paste_id := strings.TrimPrefix(r.URL.Path, "/paste")
    paste := &Paste{UUID: paste_id}

    data := paste
    t, _ := template.ParseFiles("templates/paste.html")
    t.Execute(w, data)
}
```

Your template code would then look something like this:
```html
Expiration: {{ .Expiration }}
UUID: {{ .UUID}}
```

What if we want to pass multiple objects to the template?

A really clean solution I found was to use an "anonymous struct":http://nf.wh3rd.net/10things/#2:.

In the following example, we are now modifying the pasteHandler function in the above example to pass extra boolean flags to the template.

```go
func pasteHandler(w http.ResponseWriter, r *http.Request) {
    paste_id := strings.TrimPrefix(r.URL.Path, "/paste")
    paste := &Paste{UUID: paste_id}
    keep_alive := false
    burn_after_reading := false

    data := struct {
        Paste *Paste
        KeepAlive bool
        BurnAfterReading bool
    } {
        paste,
        keep_alive,
        burn_after_reading,
    }
    t, _ := template.ParseFiles("templates/paste.html")
    t.Execute(w, data)
}
```

We then need to modify out template code to access the objects like this:

```html
Expiration: {{ .Paste.Expiration }}
UUID: {{ .Paste.UUID}}
{{ if .BurnAfterReading }}
BurnAfterReading: True
{{ else }}
BurnAfterReading: False
{{ end }}
```

