---
title: "Building Your Blog with Hugo and GitHub Pages: A Step-by-Step Guide"
date: 2024-02-24T03:24:01+01:00
draft: false
---

**Title: Building Your Blog with Hugo and GitHub Pages: A Step-by-Step Guide**

Are you looking to create your own blog but don't want the hassle of managing servers or paying for hosting? With Hugo and GitHub Pages, you can quickly set up a sleek and professional-looking blog without spending a dime. In this tutorial, we'll walk through the process of setting up your blog using Hugo, a static site generator, and GitHub Pages, a free hosting service provided by GitHub.

### Step 1: Install Hugo
The first step is to install Hugo on your system. If you're using Fedora, you can easily install it using the terminal:
```bash
sudo dnf install hugo
```
For other operating systems, you can refer to the official installation guide on the [Hugo website](https://gohugo.io/installation/).

### Step 2: Create a New Hugo Site
Once Hugo is installed, create a new Hugo site using the following command:
```bash
hugo new site blog -f yml
```
This will generate a basic Hugo site structure with default directories.

### Step 3: Choose a Theme
Next, download a theme for your blog. In this tutorial, we'll use the "paper" theme:
```bash
git submodule add https://github.com/nanxiaobei/hugo-paper themes/paper
```
After adding the theme, update the configuration file (`config.yml`) to set the theme to "paper".

### Step 4: Create a Demo Post
Create a demo post to test your setup:
```bash
hugo new posts/test.md
```

### Step 5: Set Up GitHub Repository
Create a new repository on GitHub with the name "blog". Then, initialize the local repository and push the files to GitHub:
```bash
echo "# blog" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/<your-github-username>/blog.git
git push -u origin main
```

### Step 6: Configure GitHub Pages
Go to the settings of your GitHub repository and navigate to the "Pages" tab. Choose GitHub Actions as the build and deployment method, and select Hugo as the workflow. This will generate a `hugo.yml` file.

### Step 7: Update Configuration
Update the `baseURL` in the `config.yml` file to reflect your GitHub Pages URL.

### Step 8: Sync Local and Remote Repositories
Before making any further changes locally, synchronize your local repository with the remote one by running `git pull`.

### Step 9: Publish Your Blog
Now you're ready to start adding content to your blog! You can create new posts using `hugo new posts/<filename>.md` and continue building your blog.

By following these steps, you can easily create and host your own blog using Hugo and GitHub Pages, allowing you to focus on creating content without worrying about the technical details of hosting. Happy blogging!

