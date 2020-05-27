---
layout: post
title:  "Splunk Sandbox The Easy Way"
description: "Setting up a Splunk sandbox on a local machine has never been easier."
image: "/assets/images/p101.jpg"
---
<img class="w-100" src="{{ page.image }}" alt="{{ page.title }}">

[Splunk](https://www.splunk.com){:target="_blank"} is a powerful operational intelligence & log monitoring tool. As a Splunk administrator and developer, I always want to test or try out new ideas - quick and dirty. However, the cumbersome process to set up a Splunk sandbox makes me lose motivation.

For example, to set up a Splunk sandbox on my laptop,
- I need to download the latest version from splunk.com
- Before installing the newer version, I might first need to get rid of an already installed obsolete version. 
- For getting rid of it, I need to carefully evaluate and take a backup of any app or knowledge objects it already had.
- Thanks to my laziness, if I still decide to continue with the already installed version, the enterprise trial license would have expired or I might have forgotten the old Splunk admin password. Phew!

To overcome this, I decided to shift my Splunk sandbox setup to [Docker](https://www.docker.com){:target="_blank"}. 

The shift to docker sandbox saved a considerable amount of time. However, I now faced new challenges. 
- The list of docker run command arguments required to start a new Splunk instance (docker container) is quite hard to remember. 
- I love to work on [Visual Studio Code](https://code.visualstudio.com/){:target="_blank"} to edit Splunk conf files. Setting up sync or copying conf files or app directory from my laptop (local filesystem) to the docker container, after every edit is not as easy as said. 
- Also, the same goes for backing up apps or knowledge objects from the docker container to the local filesystem.

After reading a [Splunk blog post](https://www.splunk.com/en_us/blog/tips-and-tricks/hands-on-lab-sandboxing-with-splunk-with-docker.html){:target="_blank"}, I was inspired and developed a simple solution to address the problems I had in building and managing my Splunk sandbox.

I call it my [Docker Splunk Minion](https://github.com/dmanojbaba/docker-splunk-minion){:target="_blank"}.

Here is how I do it now,
- Open `docker-splunk-minion` directory on Visual Studio Code
- Run: `./minion run` in the terminal to start the Splunk instance *(this always pulls the latest docker tag)*
- As required, I add/edit conf files in `sandbox-app`
- To restart the Splunk instance, I use the Splunk web interface or run: `./minion restart`
- See my Splunk app in action at http://localhost:8000/app/sandbox-app/
- Iterate until done
- Once done, to stop the sandbox, I run: `./minion stop`
- To remove the docker container and docker image, I run: `./minion rm && ./minion rmi`

I no longer go to splunk.com every time to download and install the latest version. I do not worry about taking manual backups of knowledge objects before killing the sandbox. Last but not the least, I can now continue to work my new ideas on my favorite code editor and see it in action instantly. 

You don't have to be a docker expert. This minion makes Splunk Sandbox The Easy Way. 

Try it today! 

Source Code: [https://github.com/dmanojbaba/docker-splunk-minion](https://github.com/dmanojbaba/docker-splunk-minion){:target="_blank"}

---