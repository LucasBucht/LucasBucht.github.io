# lucasbucht.github.io
 
Personal portfolio and blog. Site is built with Jekyll and hosted on GitHub Pages. Below are the
requirements and instructions to create your own portfolio website. Template is free to use under the [Apache License](LICENSE). If you find any issues while trying to run the project yourself, please create 
an issue on this repo.


## Initial Requirements
Before you start, you will need 3 things:
- Ruby Installation (3.3.x)
- GitHub Repo (websitename.github.io format)
- Code Editor with Git Integration (like VSCode)


### Ruby Install
One important note about the Ruby installation is that Jekyll works best on older versions, 
namely the 3.3.x version, since Ruby stopped bundling key stdlib gems around the 3.4.x era. 
This means you will need to download and older (and almost EOL) version of Ruby. There are 
alternative options where you can manually populate the gems in the GEMFILE, 
but this method is the easiest.

Step 1: Open **PowerShell** as Administrator and type in the following command:
```bash
winget install RubyInstallerTeam.RubyInstaller.3.3
```

Step 2: Ruby on Windows requires MSYS2 to compile native C extensions (gems like `psych` or `sqlite3`). Once `winget` finishes, a seperate command prompt or terminal window should display a menu of `1`, `2`, or `3`. Press `1` and hit **Enter** to install the base MSYS2 system components.

Step 3:  Once completed, rerun the installer or type `3` to sync the MSYS2 development toolchain system.

Step 4: Restart **PowerShell** and verify your installation (`ruby 3.3.x`) with the following command:
```bash
ruby -v
```


### GitHub Repo Setup
Now that Ruby is installed, it's time to set up the GitHub repo for your portfolio site. GitHub has 
a few special types of repos, and one of them is the `.github.io` repository. This suffix tells GitHub
that it should assume a GitHub Pages format. 

Step 1: Go to [github.com](https://github.com/) and sign in.

Step 2: Click the **Create New (+)** button and select **New Repository**.

Step 3: Under **Repository name**, type whatever you want your website name to be, followed by `.github.io`. For example:
```bash
WebsiteName.github.io
```

Step 4: Make sure **Visibility** is set to `Public` and leave everything else as default. 


### VSCode Integration
Now that we have our repository set up, we can start working on the code integration portion 
of our website. Make sure you log into VSCode with the same GitHub account you used to create
the repository so that you can commit directly from the Source Control. 

Step 1: Start by making sure `git` is installed on your device by opening **PowerShell** as Administrator and typing:
```bash
winget install git.git
```

Step 2: Once you have `git` installed, you'll want to clone the repo you created to your system:
```bash
git clone https://github.com/UserName/WebsiteName.github.io.git
```

Step 3: Now that you've cloned the repo, you'll want to open **VSCode**, click `File`, then `Open Folder...`, 
and then find your folder and click **Select Folder**.

You have now sucessfully set up the initial requirements for building and maintaining your own GitHub Pages site with Jekyll.

---

## How to Build a Portfolio Website with Jekyll

### Breakdown of Site Features

Making a portfolio webside with Jekyll is fairly easy. There are a few key folders and files to keep in mind when building a site, 
each of which will be discussed here. Within my template site, there are six main folders: [/_data/](#_data), 
[/_includes/](#_includes), [/_layouts/](#_layouts), [/_posts/](#_posts), [/_site/](#_site), and [/assets/](#assets). 
Outside of those main six folders are a few important files: [_config.yml](#_config.yml), [blog.html](#blog.html), 
[index.html](#index.html), [projects.html](#projects.html), and [Gemfile](#gemfile). 

#### /_data/
The `_data` folder contains two files: certifications.yml and projects.yml. Each of these files follow a similar format
of storing configuration data for site certifications and projects. 

The certifications file follows this format:
```yaml
- name: "Name of Certification"
  issuer: "Name of Certification Issuer"
  date: Year of Certification
  url: "Link to Certificaiton"
```
Each certification is very simple, with `name` and `issuer` accepting strings, `date` accepting an integer value for the year
the certification was recieved, and `url` is the link to the certification. To add another certification, all you need to do is
copy the template certification and put it on top of the current list of certification and it will appear on the home page under
"Certifications."

The projects file follows this format:
```yaml
- name: "Name of Project"
  category: "Category of Project"
  featured: True or False
  description: "Description"
  tags: [Tag1, Tag2, ...]
  repo: "Link to GitHub Repository"
  demo: "Link to Demonstration"
  image: "Filepath of Image"
  writeup: "Link to Writeup Document"
  year: Year of Project Completion
```
The projects are a little bit more complicated, with nine fields instead of four. The `name` field acts the same way as the 
certification accepting a string value for the project name. `category` expects a string with the category of the project,
which will sort the project into a group on the home page and projects page. `featured` tells the site whether or not to 
display this project on the home page, accepting a boolean value. `description` gives a description of the project to display 
under the project. `tags` adds a tag under the project to highlight a specific aspect of the project and to allow for sorting 
by tag on the projects page. `repo` accepts a link to a GitHub repository and `demo` accepts a link to a published video showing
off the project (YouTube, Vimeo, etc.). `image` sets the project cover image, linking a file from the `assets/img/` folder.
`writeup` links the project to a blog post and adds a hotlink to the project showing that there is a writeup associated with the project. `year`, like with certifications, accepts an integer value for the year the project was completed.

#### /_includes/

The `_includes` folder contains the .html files for the header, footer, and project grid. These are small, reusable snippets 
that get pulled into your pages wherever they're needed, instead of repeating the same HTML on every single page.
 
`header.html` builds the top navigation bar: your name/logo on the left, linking back to the homepage, and a row of nav links on 
the right (Home, Projects, Writing, GitHub, Resume). The GitHub and Resume links point to `site.author.github` and a PDF file 
path respectively, both of which you set elsewhere (`_config.yml` and `assets/`). Each nav link also checks the current page 
against its own URL and adds an `active` class if they match, which is what highlights the current tab.
 
`footer.html` builds the bottom bar: a copyright line with the current year (pulled automatically, no need to update it yearly) 
and a row of links, GitHub, LinkedIn, Email, and an RSS feed link. The LinkedIn and Email links only render at all if you've 
actually filled in those fields in `_config.yml`, leave them blank and they disappear cleanly rather than showing a broken link.
 
`project-grid.html` is the template used to render project cards, both the full list on the Projects page and the smaller featured 
set on the homepage. It loops through whatever list of projects it's given, and for each one builds a card with an optional image, 
a colored category dot, the name, year, description, tags, and any of `repo`/`demo`/`write-up` links that are actually filled in. 
Fields left blank in `projects.yml` just don't render their corresponding piece, there's no need to delete unused lines.
 
#### /_layouts/
 
The `_layouts` folder contains the page templates: `default.html`, `home.html`, `page.html`, and `post.html`. Every page 
on your site is built by combining its own content with one of these layouts.
 
`default.html` is the base template every other layout builds on top of. It sets up the `<head>` (fonts, stylesheet, SEO tags) 
and wraps the page in the header and footer from `_includes`. Any layout that wants the header/footer to show up needs 
`layout: default` in its own front matter, pointing back to this file, without that line, a page renders standalone with 
no nav or footer at all.
 
`home.html` is the homepage layout: banner image, headshot, name, tagline, bio, and then your featured projects and recent 
posts pulled in automatically from `_data/projects.yml` and `_posts/`.
 
`page.html` is a generic layout for simple pages, just a title and whatever content you put below it. The Projects and Writing 
pages both use this layout.
 
`post.html` is the layout used for every blog post, it adds the post's title and date automatically above your Markdown content.
 
#### /_posts/
 
The `_posts` folder holds your blog entries. Jekyll has one strict rule here: every file must be named exactly like this:
 
```
YYYY-MM-DD-post-title.md
```

Each post needs front matter with at least a title:
 
```markdown
---
title: "Post Title"
---

Normal markdown body text
```
 
Posts show up automatically on the Writing page and in the homepage's featured list, newest first, no extra configuration needed.

#### /_site/
 
`_site` is not something you edit, ever. It's the fully-built version of your site, the actual HTML, CSS, and content Jekyll 
generates by combining everything in your other folders. It gets regenerated every time you run `jekyll serve` or every time 
GitHub Pages builds your site after a push. If you're testing locally and something looks wrong, deleting this folder and 
letting it rebuild from scratch is a common fix for stale-looking changes.

#### /assets/
 
The `assets` folder holds everything that isn't a template or a page, images, your stylesheet, video, and your resume PDF.
 
`assets/css/style.scss` is your entire visual design: colors, fonts, spacing, layout rules for every component on the site. 
Jekyll compiles this into the `style.css` your pages actually load.
 
`assets/img/` holds your photos, your headshot, banner image, and project/post images. There's no required folder structure 
beyond this, some projects nest their images into their own subfolder (for example, keeping all the photos for one blog post 
together) purely for organization, Jekyll doesn't care where under `assets/img/` a file lives as long as the path in your 
YAML or Markdown matches.
 
`assets/video/` holds any video files you embed directly in a post (see the video embed note below).
 
Your resume PDF can live directly in `assets/`, referenced by the Resume link in `header.html`.

#### _config.yml
 
This is your site's control panel, settings that apply everywhere, rather than to one specific page. This is where you set 
your site title, tagline, author info (name, GitHub username, LinkedIn, email), your banner and headshot image paths, and 
a few Jekyll-specific settings (plugins, permalink format, which files to exclude from the build).
 
Two things worth knowing:
- **Changes here require a full server restart.** Unlike editing a post or a project, Jekyll's local server doesn't pick 
up `_config.yml` changes automatically, stop it (`Ctrl+C`) and run `jekyll serve` again.
- Leaving `linkedin` or `email` as `""` cleanly hides those links in the footer, rather than showing a broken one.


#### blog.html
 
This builds the Writing page (`/blog/`). It's short, just a loop through every post in `_posts/`, listing each one's date 
and title. No per-post configuration needed here, add a post and it appears automatically.

#### index.html
 
This is the homepage, and it's intentionally almost empty:
 
```yaml
---
layout: home
title: Home
---
```
 
All of the actual homepage content lives in `_layouts/home.html`, this file just tells Jekyll which layout to use.

#### projects.html
 
This builds the Projects page (`/projects/`), including the tag filter bar. A couple of things worth understanding if 
you're customizing this:
 
- The categories are currently hardcoded to `hardware` and `software` (
  `{% assign hardware = site.data.projects | where: "category", "hardware" %}`, and similarly for software). If you 
  want different categories, you'll need to edit this file directly, and also `_layouts/home.html` where the same 
  split happens for the featured section, plus add a matching `.dot--yourcategory` color rule in `style.scss`. The 
  system expects exactly two categories by default; adding a third means adjusting both the Liquid logic and the CSS, 
  not just the data file.
- The tag filter bar only shows tags that appear on **more than one project**. This is deliberate, a filter that only ever 
narrows down to a single result isn't very useful, so one-off tags are automatically left out of the filter row (though they 
still display normally on the project's own card).

#### Gemfile
 
This lists the Ruby gems your site depends on to build locally. You generally won't need to touch this unless you hit a 
dependency error. The `csv`, `logger`, `base64`, `bigdecimal`, `abbrev`, and `ostruct` lines exist specifically to patch a 
Ruby-version mismatch, newer Ruby versions stopped bundling these by default, but the Jekyll version GitHub Pages uses still 
expects them. If you're following the Ruby 3.3.x install instructions above, you shouldn't run into this, but if you ever 
upgrade your local Ruby version and start seeing `cannot load such file` errors, this is the file to check.

---
 
## Running Locally
Now that the site is assembled and ready to test, the best practice is to view the site on a localhost before pushing the 
site to GitHub. Start by opening **PowerShell** and follow these steps:

Check Ruby Installation (3.3.x):
 
```bash
ruby -v
```

Setup from the repo:
 
```bash
cd ~/GitHub/WebsiteName.github.io
gem install bundler
bundle install
```
 
Start local instance:
 
```bash
bundle exec jekyll serve
```
 
Open `http://localhost:4000`. Leave the terminal running while editing. 
Jekyll rebuilds automatically on file save. `Ctrl+C` to stop it.
 
Now you have access to a live updating version of your site. Every time you edit a file and save it, Jekyll will update 
that localhost instance and show you what your changes did, all without ever pushing anything to GitHub. Once you're 
ready, save everything and push to GitHub to watch your completed site appear on the `.github.io` link you chose. 

## Indexing Your Site on Google

But wait, when you search the internet, your site doesn't show up! This is a common feature on sites that end in common 
suffixes like `.github.io`, since Google doesn't know the difference between your GitHub site and anyone elses, so it 
doesn't see the need to index your individual site. There is, however, an easy fix to index your site and see the analytics
through Google. 

Step 1: Go to the [Google Search Console](search.google.com/search-console) and log in with your Google account.

Step 2: Click the **Add property** label and select **Add a website**.

Step 3: Under **URL Prefix**, enter your website URL as `https://WebsiteName.github.io` and click continue.

Step 4: After it verifies the URL exists, it will ask you to download an HTML file starting with `google...`. Download this 
file and verify it contains the text `google-site-verification:` followed by the HTML file name.

Step 5: Once you have verified that the file looks correct, upload it to the root of your GitHub repository and push the 
change. 

Step 6: Once the changes appear on GitHub, go back to the Google Search Console and click **Verify**. This should load for
a minute while it verifies the site has the proper verification file and once it's verified, it will unlock the console
and let you see the analytics, indexing results, and performance staticstics. 

Step 7: Now that Google knows your site exits, you still have to request to be crawled. On the left side of the console, 
click the tab that says **URL inspection**. In the bar at the top, type in `https://WebsiteName.github.io` and hit enter. 
Once inside of the URL Indexing page, there will be a button that says **REQUEST INDEXING**. Click that button.

Step 8: Once Google tests that your URL can be indexed, you will have successfully requested indexing for your website. 
Now, whenever someone looks up your site name, Google can point them to your website without having to search your site up 
manually.

That's it! Now Google will take between 1-3 weeks to fully index your site and start recommending it to people. You have 
successfully built, customized, and indexed your very own portfolio website. Good luck and God bless. 