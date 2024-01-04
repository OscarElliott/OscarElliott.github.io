---
layout: page
title: Linux Shell
description: a simple UNIX shell implemented in C
img:
importance: 4
category: fun
---

This repository hosts a standard implementation of a Linux Shell, written in C. A minimalist yet powerful command-line interface, this Shell is designed to provide users with a replicated experience of basic functionality of a linux terminal following POSIX API.


### Features
- **Command Execution:** Execute commands in the shell, including external commands and built-in commands like `cd`.


- **Background Execution:** Run commands in the background with threads using the `&` symbol.

- **File Operations:**
  - `rm`: Delete a file or directory.
  - `mv`: Rename a file or directory.
  - `cp`: Copy a file or directory.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/Example_Shell.png" title="example_shell image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A series of commands showcasing a range of shells capabilities.
</div>

### GitHub Repository

If you'd like to explore this little project further the code is publically avalible on my github


{% if site.data.repositories.github_repos %}
<div class="text-center">
  <div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-center align-items-center">
    {% for repo in site.data.repositories.Linux_Shell %}
      {% include repository/repo.html repository=repo %}
    {% endfor %}
  </div>
</div>
{% endif %}
