---
title: Linux and Server Administration
excerpt: Some information about my servers, and the ways I use Linux.
collection: projects
---
This project doesn't really fit the time frame of a normal project. For starters, it's been a part of my life since 2017. It also isn't ending anytime soon, probably ever. Because of this, I won't go over the timeline from start to end like I normally would. Instead, I'll detail a few of my favourite parts.
## Basics
### Linux
With the exception of my first ever Network Attached Storage server (It ran FreeBSD), all of my servers run Linux. I was first exposed to Linux when my parents got me a Raspberry Pi 3 in 6th grade. Instantly, I was hooked. I did a presentation on it that year for my class, and I began experimenting with it more and more. Currently, I daily-drive Linux on every device that I use (assuming that Android counts as Linux). Since even Microsoft uses Linux to run their cloud-hosting platform Azure, I probably don't need to espouse the benefits of Linux for hosting servers. In terms of daily use, I like Linux because it respects your privacy and is a lot lighter compared to Windows. I also enjoy the customisability of it. I don't play many video games these days, but game compatibility is now quite good thanks to Valve. Software compatibility is generally only an issue if you play multiplayer games with invasive anticheat, or use software from certain companies like Adobe.
### Docker
I have been using Docker since 2019 and it is the backbone of all the servers that I have run since. Docker is *containerization* software. Put simply, it isolates apps running from the system they're running on. This allows them to be managed without me having to install any of their dependencies, or manage conflicts with other software. It also increases security somewhat; if an app I was running had weak security and was taken over, the attacker would first have to escape the container before doing any real damage (It should be noted that Docker alone is not a sufficient firewall, but an added step of security). It also provides a convenient way of specifying how you want your containers to run (called Docker Compose) and a repository that stores a whole bunch of different images.
### Caddy
I use Caddy to reverse proxy nearly all of my services to my domain, jwillb.net. Caddy makes things really simple because all you need to do is add a line or two to the Caddyfile (The file that dictates how Caddy behaves) to add a domain. It even manages HTTPS by itself! As an example, you could do a quick reverse proxy from example.jwillb.net to the port 3000 on your local machine like this: `reverse_proxy example.jwillb.net {127.0.0.1:3000}`. This is much simpler than the GUI-based NginX Proxy Manager, which I was running previously.
## Services
### Jellyfin
This is probably the most used software on any of my servers, probably ever. Jellyfin is a free and open source media server. What this allows somebody to do is provide a nice interface for browsing your media collection, which can be movies, TV shows, music, or even home videos. My family and I use this to watch Blu-Ray movies and TV that we find at thrift stores because it provides a convenient way to watch your media on any device that supports it, and you don't have to be tech-savvy. I deploy it using their official Docker container. Docker does make it slightly harder to set up hardware transcoding on Nvidia GPUs, but it's worth the hassle. I host this on my local server because media takes up storage and local streaming is a lot faster than streaming from a VPS.
### Vikunja
Probably the most important service I am currently running. It's a to-do list/reminder app with tons of features that suits my needs and helps me remember that I have stuff to do.
### Vaultwarden
Vaultwarden is a server for the Bitwarden password manager rewritten in Rust. It is also a lot simpler to set up. It doesn't do much by itself, but it becomes an amazing password manager when combined with the Bitwarden apps/browser extensions.
### Joplin
Joplin is similar to Vaultwarden in that it's just a server, but it shines when combined with its companion app. I run the sync server on my VPS and I use their desktop app to take notes for school and other stuff.
