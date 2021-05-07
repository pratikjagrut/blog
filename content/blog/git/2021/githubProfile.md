---
title: "Transforming pedestrian Github profile into dynamic portfolio"
description: ""
date: 2021-05-06T20:57:06+05:30
draft: false
author: "Pratik Jagrut"
layout: "blog"
images:
  - src: "img/git/github.png"
    alt: "github banner"
    stretch: ""
    removeBlur: true
categories:
  - "git"
tags:
  - "2021"
  - "git"
  - "programming"
---
Today Github is the behemoth platform for opensource projects.
There would not be a single person in the opensource community who don't use GitHub.
And there could be a very little or minuscule number of the developer who doesn't have GitHub profile.
Github is not only the home for best opensource projects but also a place where developers could showcase their talent via a panoply of projects.

Below is the default GitHub profile page that shows the name, contact information and some repositories.

![GitHub default profile page](/img/git/ghRegProf.png)

A few months back, Github launched a new feature that lets us customize our profile page using the README file.
README is a repository or project level file used for documenting the project. 
README.md is written in `Markdown(lightweight markup language)` that converts text to HTML.

#### In this blog post, I will show how I customized my mundane Github profile using the README file.

[![GitHub default profile page](/img/git/ghNewProf.png)](https://github.com/pratikjagrut)

## Create a new repository with the username

```
1. Make sure your repository name matches the Github username.
2. Make a public repository.
3. Add README.md to it.
```
![Create repo](/img/git/repoC.png)

## Adding a banner image

When someone opens my profile, I wanted to greet them with a good banner. 
I created a banner on ***<a href="https://www.canva.com/" style="color:#2eb8ac" target="_blank">canva.com</a>***. 
They have a good collection of free templates.

![Create repo](/img/git/ghbanner.png)

I'm keeping this image in the `img` directory.
Now I want it to be at the top, so I put the link to the banner image on the first line of my README file.

To add an image in the README file, use the following syntax.
```dockerfile
![Pratik's GitHub Banner](./img/banner1.png)
```

If you want to make an image, a link that will open your blog or some other sites, use the following syntax.
```dockerfile
[![Pratik's GitHub Banner](./img/banner1.png)](https://pratikjagrut.dev)
```

## Add a bio

GitHub initializes README with a few bullet points. I used the same template to add my bio.

README file is highly customizable, we can use Markdown to add more creative bio. 
This is the ***<a href="https://www.markdownguide.org/basic-syntax/" style="color:#2eb8ac" target="_blank">Markdown syntax guide</a>***

![Create repo](/img/git/bio.png)

I've added some badges under look me up bullet point, which I created using ***<a href="http://shields.io/" style="color:#2eb8ac" target="_blank">shields.io</a>***. They lets us design customize badges with the links or without links. I used badges from ***<a href="https://shields.io/category/social" style="color:#2eb8ac" target="_blank">social category</a>***.

Once we've got the badge, we can then put it anywhere we want.
```dockerfile
[![Linkedin Badge](https://img.shields.io/badge/-pratikjagrut-0e76a8?style=flat&labelColor=0e76a8&logo=linkedin&logoColor=white)][linkedin]
```

## Listing latest blog posts

***<a href="https://github.com/gautamkrishnar" style="color:#2eb8ac" target="_blank">Gautam krishna R</a>*** created a Github action workflow which lets us show our latest blog, latest, youtube video, latest StackOverflow activity and many other things. ***<a href="https://github.com/gautamkrishnar/blog-post-workflow" style="color:#2eb8ac" target="_blank">Follow the documentation</a>***. 

![Blogs lists](/img/git/blogs.png)

## Showing GitHub statistics

***<a href="https://github.com/anuraghazra/github-readme-stats" style="color:#2eb8ac" target="_blank">Github Readme stats</a>*** shows the statistics of our profile in various beautiful cards. 

![Github stats](/img/git/stats.png)e


##### <span style="color:green"> There are tone of customization we can do with GitHub profile using README, not everything is not covered in this. Below are some useful resources which will help to add some advanced elements.</span>.

- ***[My Github profile README](https://github.com/pratikjagrut/pratikjagrut)***
- ***[Create badges: shields.io](https://shields.io/)***
- ***[Awesome github profile readme templates](https://github.com/abhisheknaiidu/awesome-github-profile-readme)***
- ***[Next Level GitHub Profile README by codeSTACKr](https://www.youtube.com/watch?v=ECuqb5Tv9qI&t=716s)***
- ***[UPDATE: Next Level GitHub Profile README (NEW) | GitHub Actions | Vercel | Spotify by codeSTACKr](https://www.youtube.com/watch?v=n6d4KHSKqGk&t=181s)***

<b style="color:#cc3300"><i>***I hope you found this blog helpful and thank you for reading it please give your feedback in the comment section below.***</i></b>

<hr>
