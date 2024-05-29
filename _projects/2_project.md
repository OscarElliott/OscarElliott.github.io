---
layout: page
title: Purpose Project
description: A project to help students identify potential future prospects based on a fun conversation.
img: assets/img/purpose.png
importance: 1
category: fun
---

Purpose Project is an innovative tool designed to assist students in discovering potential future career paths through an engaging and interactive process. The core idea is to provide students with insights into their strengths and areas of interest by evaluating their responses to a set of questions.


### [Try it Online here](https://oscarelliott.pythonanywhere.com/)


### Features

- Interactive Assessment: Students answer a series of questions related to various skills and attributes.
- AI-Powered Evaluation: Utilizing OpenAI's advanced language model, each answer is scored across multiple metrics, offering a detailed analysis of the student's capabilities.
- KD-Tree Algorithm: The project employs a K-dimensional tree (KD-Tree) algorithm to match students' scores with the most suitable career paths from a predefined dataset.
- Career Path Suggestions: Based on the closest match from a nearest neighbour search, students receive personalized career recommendations, helping them to explore and consider various professions that align with their strengths and interests.


### GitHub Repository

If you'd like to explore this little project further the code is publically avalible on my github

{% if site.data.repositories.github_repos %}
<div class="text-center">
  <div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-center align-items-center">
    {% for repo in site.data.repositories.PurposeProject %}
      {% include repository/repo.html repository=repo %}
    {% endfor %}
  </div>
</div>
{% endif %}
