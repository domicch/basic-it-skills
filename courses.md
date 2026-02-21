---
layout: default
title: Safety Courses
permalink: /courses/
---

# All Courses

Master practical computer and technology skills to navigate the digital world with confidence.

<div class="courses-grid">
{% assign sorted_courses = site.data.courses.courses | sort: "order" %}
{% for course in sorted_courses %}
  <div class="course-card">
    <div class="course-icon">{{ course.icon }}</div>
    <h2>{{ course.title }}</h2>
    <p>{{ course.description }}</p>
    <a href="{{ '/courses/' | relative_url }}{{ course.id }}/" class="btn btn-primary">Start Course</a>
  </div>
{% endfor %}
</div>
