# Jekyll Static Safety Course Website Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a modular Jekyll website for teaching computer and mobile phone safety, organized by 6 courses with consistent layout and easy content management.

**Architecture:** Jekyll project with a `_courses/` data structure, reusable Liquid templates, and course pages. Each course is a separate collection with its own layout, navigation, and content structure. Site uses a simple CSS framework for responsive design.

**Tech Stack:** Jekyll 4.x, Liquid templating, YAML front matter, CSS/HTML, Markdown for content

---

### Task 1: Initialize Git Repository and Jekyll Project

**Files:**
- Create: `/Users/dominic/workspace/online-security-website/` (entire project)

**Step 1: Initialize git and create Jekyll project**

Run:
```bash
cd /Users/dominic/workspace/online-security-website
git init
jekyll new . --force
```

Expected: Jekyll creates `_config.yml`, `_posts/`, `_layouts/`, `assets/`, `Gemfile`, and other Jekyll defaults.

**Step 2: Verify Jekyll installs correctly**

Run:
```bash
bundle install
```

Expected: Gemfile dependencies install successfully.

**Step 3: Test Jekyll local server**

Run:
```bash
bundle exec jekyll serve
```

Expected: Server starts on `http://localhost:4000` with the default welcome post visible.

**Step 4: Stop the server and commit**

Run:
```bash
git add .
git commit -m "init: set up Jekyll project structure"
```

Expected: Git commit succeeds with initial Jekyll files.

---

### Task 2: Create Course Collection and Data Structure

**Files:**
- Create: `/Users/dominic/workspace/online-security-website/_courses/` (directory)
- Create: `/Users/dominic/workspace/online-security-website/_data/courses.yml`
- Modify: `/Users/dominic/workspace/online-security-website/_config.yml`

**Step 1: Update Jekyll config to add courses collection**

Read the current `_config.yml`, then add this under the main config:

```yaml
collections:
  courses:
    output: true
    permalink: /courses/:name/

defaults:
  - scope:
      path: ""
      type: "courses"
    values:
      layout: "course"
```

Expected: Config file updated with courses collection configuration.

**Step 2: Create courses data file**

Create `/Users/dominic/workspace/online-security-website/_data/courses.yml`:

```yaml
courses:
  - id: phishing-scams
    title: "Phishing & Scams"
    order: 1
    icon: "🎣"
    description: "Learn to identify and avoid phishing emails and online scams"

  - id: password-security
    title: "Password Security"
    order: 2
    icon: "🔐"
    description: "Create strong passwords and manage them safely"

  - id: malware-prevention
    title: "Malware Prevention"
    order: 3
    icon: "🛡️"
    description: "Protect your devices from viruses and malware"

  - id: social-media-safety
    title: "Social Media Safety"
    order: 4
    icon: "👥"
    description: "Stay safe on social media platforms"

  - id: mobile-security
    title: "Mobile Phone Security"
    order: 5
    icon: "📱"
    description: "Secure your smartphone and tablets"

  - id: online-shopping
    title: "Online Shopping Security"
    order: 6
    icon: "🛒"
    description: "Shop safely online and protect your financial information"
```

Expected: File created with all 6 courses defined.

**Step 3: Create _courses directory**

Run:
```bash
mkdir -p /Users/dominic/workspace/online-security-website/_courses
```

Expected: Directory created.

**Step 4: Commit changes**

Run:
```bash
git add _config.yml _data/courses.yml
git commit -m "feat: configure Jekyll courses collection and course metadata"
```

Expected: Git commit succeeds.

---

### Task 3: Create Base Course Layout Template

**Files:**
- Create: `/Users/dominic/workspace/online-security-website/_layouts/course.html`
- Modify: `/Users/dominic/workspace/online-security-website/_layouts/default.html`

**Step 1: Create course layout**

Create `/Users/dominic/workspace/online-security-website/_layouts/course.html`:

```html
---
layout: default
---

<div class="course-container">
  <div class="course-header">
    <h1>{{ page.title }}</h1>
    <p class="course-description">{{ page.description }}</p>
  </div>

  <div class="course-content">
    {{ content }}
  </div>

  <div class="course-navigation">
    <a href="/courses/" class="btn btn-back">← Back to Courses</a>
  </div>
</div>
```

Expected: File created with course layout structure.

**Step 2: Update default layout with basic styling**

Read the existing `_layouts/default.html` and wrap it with a simple header and footer:

```html
---
---
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>{{ page.title }} - Computer & Mobile Safety Course</title>
    <link rel="stylesheet" href="{{ '/assets/css/style.css' | relative_url }}">
  </head>
  <body>
    <header class="site-header">
      <nav class="site-nav">
        <a href="/" class="site-title">Digital Safety Course</a>
        <ul>
          <li><a href="/courses/">All Courses</a></li>
          <li><a href="/">Home</a></li>
        </ul>
      </nav>
    </header>

    <main class="site-content">
      {{ content }}
    </main>

    <footer class="site-footer">
      <p>&copy; 2026 Digital Safety Course. Created for safer computing.</p>
    </footer>
  </body>
</html>
```

Expected: Default layout updated with header, nav, and footer structure.

**Step 3: Commit changes**

Run:
```bash
git add _layouts/course.html _layouts/default.html
git commit -m "feat: create course and default layout templates"
```

Expected: Git commit succeeds.

---

### Task 4: Create Courses Index Page

**Files:**
- Create: `/Users/dominic/workspace/online-security-website/courses.md`

**Step 1: Create courses index page**

Create `/Users/dominic/workspace/online-security-website/courses.md`:

```markdown
---
layout: default
title: Safety Courses
permalink: /courses/
---

# Safety Courses

Learn essential skills to stay safe online and on mobile devices.

<div class="courses-grid">
{% assign sorted_courses = site.data.courses.courses | sort: "order" %}
{% for course in sorted_courses %}
  <div class="course-card">
    <div class="course-icon">{{ course.icon }}</div>
    <h2>{{ course.title }}</h2>
    <p>{{ course.description }}</p>
    <a href="/courses/{{ course.id }}/" class="btn btn-primary">Start Course</a>
  </div>
{% endfor %}
</div>
```

Expected: Page created with course listing template.

**Step 2: Commit changes**

Run:
```bash
git add courses.md
git commit -m "feat: create courses index page"
```

Expected: Git commit succeeds.

---

### Task 5: Create Basic CSS Styling

**Files:**
- Create: `/Users/dominic/workspace/online-security-website/assets/css/style.css`

**Step 1: Create CSS file with base styling**

Create `/Users/dominic/workspace/online-security-website/assets/css/style.css`:

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, sans-serif;
  line-height: 1.6;
  color: #333;
  background-color: #f9f9f9;
}

.site-header {
  background: #2c3e50;
  color: white;
  padding: 1rem 0;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.site-nav {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.site-title {
  font-size: 1.5rem;
  font-weight: bold;
  text-decoration: none;
  color: white;
}

.site-nav ul {
  list-style: none;
  display: flex;
  gap: 2rem;
}

.site-nav a {
  color: white;
  text-decoration: none;
  transition: opacity 0.2s;
}

.site-nav a:hover {
  opacity: 0.8;
}

.site-content {
  max-width: 1200px;
  margin: 2rem auto;
  padding: 0 2rem;
}

.courses-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin: 2rem 0;
}

.course-card {
  background: white;
  border-radius: 8px;
  padding: 2rem;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition: transform 0.2s, box-shadow 0.2s;
}

.course-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
}

.course-icon {
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.course-card h2 {
  margin-bottom: 0.5rem;
  color: #2c3e50;
}

.course-card p {
  color: #666;
  margin-bottom: 1.5rem;
}

.btn {
  display: inline-block;
  padding: 0.75rem 1.5rem;
  border-radius: 4px;
  text-decoration: none;
  transition: background-color 0.2s;
  border: none;
  cursor: pointer;
  font-size: 1rem;
}

.btn-primary {
  background-color: #3498db;
  color: white;
}

.btn-primary:hover {
  background-color: #2980b9;
}

.btn-back {
  background-color: #95a5a6;
  color: white;
}

.btn-back:hover {
  background-color: #7f8c8d;
}

.course-header {
  background: white;
  padding: 2rem;
  border-radius: 8px;
  margin-bottom: 2rem;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.course-header h1 {
  color: #2c3e50;
  margin-bottom: 0.5rem;
}

.course-description {
  color: #666;
  font-size: 1.1rem;
}

.course-content {
  background: white;
  padding: 2rem;
  border-radius: 8px;
  margin-bottom: 2rem;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.course-content h2 {
  margin-top: 2rem;
  margin-bottom: 1rem;
  color: #2c3e50;
  border-bottom: 2px solid #3498db;
  padding-bottom: 0.5rem;
}

.course-content h3 {
  margin-top: 1.5rem;
  margin-bottom: 0.5rem;
  color: #34495e;
}

.course-content ul, .course-content ol {
  margin-left: 1.5rem;
  margin-bottom: 1rem;
}

.course-content li {
  margin-bottom: 0.5rem;
}

.site-footer {
  background: #2c3e50;
  color: white;
  text-align: center;
  padding: 2rem;
  margin-top: 3rem;
}

@media (max-width: 768px) {
  .site-nav {
    flex-direction: column;
    gap: 1rem;
  }

  .courses-grid {
    grid-template-columns: 1fr;
  }

  .site-content {
    padding: 0 1rem;
  }
}
```

Expected: CSS file created with comprehensive styling.

**Step 2: Commit changes**

Run:
```bash
git add assets/css/style.css
git commit -m "style: add base CSS styling for courses and layouts"
```

Expected: Git commit succeeds.

---

### Task 6: Create First Course - Phishing & Scams

**Files:**
- Create: `/Users/dominic/workspace/online-security-website/_courses/phishing-scams.md`

**Step 1: Create first course content**

Create `/Users/dominic/workspace/online-security-website/_courses/phishing-scams.md`:

```markdown
---
title: "Phishing & Scams"
description: "Learn to identify and avoid phishing emails and online scams"
---

## What is Phishing?

Phishing is when criminals send fake emails that look like they're from legitimate companies to trick you into:
- Giving them your password or personal information
- Clicking malicious links
- Downloading harmful attachments

## How to Spot a Phishing Email

### Red Flags:
- **Sender's email address looks suspicious** - Not the official company domain
- **Urgent language** - "Act now!" "Verify immediately!" "Account will be closed!"
- **Requests for passwords** - Real companies never ask for passwords via email
- **Generic greetings** - "Dear Customer" instead of your name
- **Suspicious links** - Hover over links to see the real URL (often mismatched)
- **Poor grammar/spelling** - Professional companies proofread
- **Unusual requests** - Ask for wire transfer, gift cards, or unusual payment

## What NOT to Do:
- ❌ Don't click links in suspicious emails
- ❌ Don't download attachments from unknown senders
- ❌ Don't reply with personal information
- ❌ Don't call phone numbers in the email

## What TO Do:
- ✅ Contact the company directly using a number from their official website
- ✅ Report the phishing email to the company
- ✅ Delete the email
- ✅ If you already clicked, change your password immediately
- ✅ Check your accounts for unauthorized activity

## Example Phishing Email

**Subject:** "URGENT: Confirm Your Banking Details"

This is a classic phishing attempt because:
- Uses urgent language
- Requests sensitive information
- Email address isn't from the real bank domain

## Practice Tip

When in doubt, go to the company's official website directly and log in there instead of clicking email links. This is the safest way to access your accounts.
```

Expected: Course content file created with comprehensive lesson.

**Step 2: Test the Jekyll build**

Run:
```bash
bundle exec jekyll build
```

Expected: Site builds successfully with the new course visible.

**Step 3: Verify the course displays**

Run:
```bash
bundle exec jekyll serve
```

Then open `http://localhost:4000/courses/phishing-scams/` in a browser.

Expected: Course page displays correctly with formatting.

**Step 4: Stop server and commit**

Run:
```bash
git add _courses/phishing-scams.md
git commit -m "content: add phishing & scams course"
```

Expected: Git commit succeeds.

---

### Task 7: Create Home Page

**Files:**
- Create: `/Users/dominic/workspace/online-security-website/index.md`

**Step 1: Create homepage**

Create or replace `/Users/dominic/workspace/online-security-website/index.md`:

```markdown
---
layout: default
title: Home
---

# Digital Safety Course

Welcome to the comprehensive guide for staying safe with computers and mobile devices.

## Why This Course?

In today's digital world, knowing how to protect yourself online is essential. This course covers:
- How to recognize and avoid scams
- Creating and managing secure passwords
- Protecting your devices from malware
- Staying safe on social media
- Securing your mobile phone
- Shopping safely online

## How to Use This Course

1. Start with any course that interests you
2. Read through all the lessons
3. Practice the safety tips in your daily digital life
4. Come back anytime you need a refresher

**Ready to learn?** [View All Courses](/courses/)

---

*Last Updated: February 2026*
```

Expected: Homepage created with welcome content.

**Step 2: Verify homepage displays**

Run:
```bash
bundle exec jekyll serve
```

Then open `http://localhost:4000/` in a browser.

Expected: Homepage displays correctly.

**Step 3: Stop server and commit**

Run:
```bash
git add index.md
git commit -m "content: add homepage"
```

Expected: Git commit succeeds.

---

## Summary

**7 Tasks Total:**
1. Initialize Git Repository and Jekyll Project
2. Create Course Collection and Data Structure
3. Create Base Course Layout Template
4. Create Courses Index Page
5. Create Basic CSS Styling
6. Create First Course - Phishing & Scams
7. Create Home Page

Each task has clear steps, expected outputs, and git commits for easy tracking.
