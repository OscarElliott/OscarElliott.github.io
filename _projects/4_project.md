---
layout: page
title: AI Course Showcase
description: Explore my journey in the field of Artificial Intelligence through three captivating assignments showcased in my GitHub repository.
img:
importance: 1
category: uni
---

    This repository contains three seperate smaller projects relating to topics covered in the course

    Pathfinding with A* Search Algorithm:
    Unveil the intricacies of my implementation of A* Search for pathfinding. This assignment demonstrates my ability to apply efficient algorithms to real world problems.

    KD Tree for Wine Quality Assessment:
    Dive into the world of machine learning as I present my assignment on utilizing a KD tree for assessing wine quality. Witness how this data structure enhances the efficiency of wine quality predictions. This project reflects my understanding of machine learning concepts as I apply k-NN search a non-paramatic supervised learning technique. It further demonstrates my practical skills needed for building & training models that contribute to decision-making processes.

    Viterbi Forward Algorithm for Robot Localization:
    Embark on a fascinating journey through the realm of robotics with my implementation of the Viterbi Forward Algorithm. This assignment showcases my proficiency in applying advanced algorithms for robot localization. Delve into the details of how this algorithm predicts the position of a robot, highlighting my grasp of AI concepts in the context of robotics.


### GitHub Repository

If you'd like to explore these little projects further the code is publically avalible on my github


{% if site.data.repositories.github_repos %}
<div class="text-center">
  <div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-center align-items-center">
    {% for repo in site.data.repositories.AI %}
      {% include repository/repo.html repository=repo %}
    {% endfor %}
  </div>
</div>
{% endif %}
