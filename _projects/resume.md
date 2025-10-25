---
title: CI/CD for my Resume!
excerpt: An explanation of my resume pipeline, and switching to Typst
collection: projects
---

## Background
When I first created my resume, I used Google Docs. This was fine for the first few years that I was working. By the second year of university I realised I needed something that was more deterministic to use, and I learned that many people used LaTeX for their resumes. I found this exciting because it was a way to declare your resume and know exactly how it was set up. With a WYSIWYG (What you see is what you get) editor, there is a lot of dragging and dropping and cursing when your columns don't like up. Not so with LaTeX: It is a markup language for declaring your documents! I instantly knew I wanted my resume in this format. The unfortunate thing is that the most popular editor for LaTeX, Overleaf, is proprietary, online only software. I decided to use TeXMaker instead, which allowed me to edit locally. This was a good workflow. The final issue was a simple one on the surface: How do I get my resume into a central place, with revision history to see what changes I've made? If you know about Git, then you know it is the right choice.

## Versioning with Git
For those who don't know, Git is a distributed version control system for writing software, Essentially, it allows you to track changes made to files, and pretty much all developers use it today. Another benefit of using Git was that I could use GitHub for hosting my resume, which would make it easy to access without me worrying about hosting it.

## GitHub Actions!
GitHub Actions is a Continuous Integration service that GitHub offers. It normally allows software to be immediately deployed after certain conditions are met (e.g. An app gets compiled after a branch has been merged to `main`). I realised that I could use this for my resume! The action itself is available on my GitHub repo, but all it does is compile my resume and publish a release for it. The release portion is critical: I set each new release as the latest release, so I can compile my resume with each new release, and always have a link to the latest version; This will be important later.

## Typst
I had been using my resume workflow for a while and it had been working well. I would make a change to my resume, push a new commit, and it would automatically build it and make a release. Unfortunately, I had grown tired of LaTeX. It had an unwieldy syntax and the editor was bulky and inconvenient. I had put up with it because I thought there was no other option. But then, I learned about Typst.

Typst is an alternative to LaTeX for declaring PDF files in code. Its syntax is WAY nicer than LaTeX and it also has more pleasant tools. They're also fully open source, and a lot easier to set up! The only road block was learning a new syntax. Luckily, it only took a few hours, and the reward was absolutely worth it. The language is a lot more fun to use and it's actually a full programming language, unlike LaTeX.

Updating the GitHub Action was also easy. It was very easy to find a straightforward GitHub Action on the Marketplace, so after updating the workflow and adding the fonts for Font Awesome, my resume compiles and releases, fully in Typst!

I used the Google Drive PDF viewer to have it viewable on my website without downloading it first. This is the current iteration of my resume: I commit my changes, it builds a release, and the latest version is viewable right on my website.
