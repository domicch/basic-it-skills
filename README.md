# Digital Safety Course Website

A Jekyll-based static website for teaching computer and mobile phone safety.

## Quick Start

### Prerequisites

- **Ruby 3.0+** (Ruby 4.0+ recommended)
- **Bundler** (Ruby gem manager)
- **Git** (for version control)

### Installation

1. **Install Homebrew Ruby** (if you don't have Ruby 3.0+):
   ```bash
   brew install ruby
   ```

2. **Set up Ruby path in your shell** (add to `~/.zshrc` or `~/.bash_profile`):
   ```bash
   export PATH="/opt/homebrew/opt/ruby/bin:$PATH"
   ```

3. **Install dependencies**:
   ```bash
   cd /Users/dominic/workspace/online-security-website
   bundle install
   ```

## Building the Website

### Development Server (Recommended)

Run the local development server and automatically rebuild on file changes:

```bash
export PATH="/opt/homebrew/opt/ruby/bin:$PATH"
bundle exec jekyll serve
```

The website will be available at **http://localhost:4000**

### Static Build

Build the static HTML files (output in `_site/` folder):

```bash
export PATH="/opt/homebrew/opt/ruby/bin:$PATH"
bundle exec jekyll build
```

### Build Options

- **Incremental build** (faster for large sites):
  ```bash
  bundle exec jekyll serve --incremental
  ```

- **Verbose output** (for debugging):
  ```bash
  bundle exec jekyll serve --verbose
  ```

- **Clean build** (remove old files):
  ```bash
  bundle exec jekyll clean
  bundle exec jekyll build
  ```

## Project Structure

```
online-security-website/
├── _courses/                    # Course markdown files
│   └── phishing-scams.md
├── _data/
│   └── courses.yml             # Course metadata (title, icon, description)
├── _layouts/
│   ├── default.html            # Main site layout (header, footer, nav)
│   └── course.html             # Course page layout
├── _site/                       # Built static HTML (generated)
├── assets/
│   ├── css/
│   │   └── style.css           # Custom CSS styling
│   └── main.scss               # Minima theme styles
├── _config.yml                 # Jekyll configuration
├── index.md                    # Homepage
├── courses.md                  # Courses listing page
├── Gemfile                     # Ruby dependencies
└── Gemfile.lock                # Locked dependency versions
```

## Adding New Courses

### Create a New Course File

1. Create a new markdown file in `_courses/`:
   ```bash
   touch _courses/password-security.md
   ```

2. Add the course content with front matter:
   ```markdown
   ---
   title: "Password Security"
   description: "Create strong passwords and manage them safely"
   ---

   ## Course Content

   Your course content here...
   ```

3. **Important**: Make sure the course is also defined in `_data/courses.yml` with metadata:
   ```yaml
   - id: password-security
     title: "Password Security"
     order: 2
     icon: "🔐"
     description: "Create strong passwords and manage them safely"
   ```

4. The course will automatically appear on the courses page at `/courses/password-security/`

### Course Front Matter Options

- `title`: Course title (required)
- `description`: Short course description (required)
- `layout`: Always set to `course` (auto-set by `_config.yml`)

## Customization

### Site Title and Description

Edit `_config.yml`:
```yaml
title: Digital Safety Course
description: Learn essential skills to stay safe online and on mobile devices.
```

### Colors and Styling

Edit `assets/css/style.css`:
- Header background: `#2c3e50`
- Primary button color: `#3498db`
- Text color: `#333`
- Background: `#f9f9f9`

### Navigation

Edit `_layouts/default.html` to add/remove navigation links.

## Deployment

The `_site/` folder contains the complete static website ready to deploy:

### Deploy to GitHub Pages

1. Push to GitHub:
   ```bash
   git push origin main
   ```

2. Enable GitHub Pages in repository settings

### Deploy to Other Hosting

Upload the contents of `_site/` to any web server:
- Netlify
- Vercel
- AWS S3
- Traditional web hosting (FTP/SFTP)

## Troubleshooting

### "command not found: jekyll"
Make sure Ruby path is set:
```bash
export PATH="/opt/homebrew/opt/ruby/bin:$PATH"
which jekyll
```

### "Gem::FilePermissionError"
System Ruby permissions issue. Use Homebrew Ruby instead:
```bash
brew install ruby
# Then add to PATH as shown in Installation section
```

### Port 4000 already in use
Use a different port:
```bash
bundle exec jekyll serve --port 4001
```

### Changes not showing
1. Stop the server (Ctrl+C)
2. Clear cache and rebuild:
   ```bash
   bundle exec jekyll clean
   bundle exec jekyll serve
   ```

### Gemfile.lock conflicts
Update dependencies:
```bash
bundle update
```

## File Descriptions

| File | Purpose |
|------|---------|
| `_config.yml` | Jekyll configuration, collections setup, site metadata |
| `_layouts/default.html` | Main site template with header, footer, navigation |
| `_layouts/course.html` | Course page template |
| `_data/courses.yml` | Course metadata (title, description, icon, order) |
| `assets/css/style.css` | Custom CSS for site styling |
| `index.md` | Homepage content |
| `courses.md` | Courses listing page template |
| `Gemfile` | Ruby dependencies (Jekyll, minima theme, etc.) |

## Useful Commands

```bash
# Start local server
bundle exec jekyll serve

# Build static site
bundle exec jekyll build

# Clean generated files
bundle exec jekyll clean

# Check for broken links
bundle exec jekyll doctor

# Update dependencies
bundle update
```

## License

This project is open source and available for educational purposes.

## Support

For issues or questions about Jekyll, visit:
- [Jekyll Official Docs](https://jekyllrb.com/docs/)
- [Jekyll GitHub Issues](https://github.com/jekyll/jekyll/issues)
