---
title: Easily Deploy Your Apps with Coolify
date: 2025-05-22
draft: false
tags:
  - deployment
---

Hey there! If you're a developer, a small business owner, or just someone who loves building cool stuff, you know that feeling when your app is finally ready. Awesome, right? But then comes the tricky part: **deployment**. For a lot of us, that's where the fun can turn into a major headache. Cloud hosting platforms promise to make things easy, but they often hit you with tricky learning curves, bills that keep climbing, and that annoying feeling that you're not really in charge of your own stuff.

**Are you totally over complicated deployment steps, crazy high hosting costs, or just struggling to get your apps live without a fuss?** What if you could get that super smooth, modern deployment experience, but with all the control and budget-friendliness of hosting things on your own server?

Well, say hello to **Coolify** – an open-source solution that you can host yourself, designed specifically to make deploying your apps, databases, and services ridiculously easy, even if you're just starting out!

When I first used Coolify, I was really confused with how little steps you have to do before having a setup up and running. Before showing you how to use it, let's see what it can do for you, and if you want to use it or not.

## So, What Exactly IS Coolify?

At its core, Coolify is an **open-source, self-hostable alternative to those big Platform-as-a-Service (PaaS) companies**. Picture this: you get your very own cloud management dashboard that you set up and run right on your own server. Instead of paying some big company to handle your infrastructure and deploy your apps, Coolify puts the power back in _your_ hands. You get to do it yourself, on hardware you totally control!

It's built to simplify all those tricky bits that usually come with self-hosting. You just need to provide the server – maybe a super affordable Virtual Private Server (VPS) from places like Hetzner or DigitalOcean, a powerful machine you own, a tiny Raspberry Pi, or even an old laptop you've got lying around. Coolify then gives you this awesome, easy-to-use interface and all the automation you need to effortlessly deploy and manage your digital projects.

## How Coolify Works Its Magic for Super Easy Deployment

The real genius of Coolify is how it takes all the confusing technical stuff about server operations and presents it in a friendly, simple web interface. Here's how it makes deployment a breeze:

### Use your own server
First things first, you'll need a server with SSH access. This is where Coolify will live and where your apps will run. Just remember, Coolify doesn't _give_ you the server; it's the powerful software that manages everything _on_ it.

### Installation
Getting Coolify up and running on your chosen server is surprisingly simple. Usually, it's just one command, and boom! All the necessary bits for its dashboard and deployment powers are set up.
    
### Manage multiple VPS at once
Once Coolify's installed, you hop onto its web dashboard. From there, you securely link your server(s) to Coolify using SSH keys. This secure connection is what lets Coolify automate tasks and deploy your apps with incredible ease.

### Dockerised applications
Coolify uses Docker containers for all your deployments. This is a HUGE win for simplicity! It means your apps and services run in their own little isolated, portable environments. You don't need to be a Docker wizard; Coolify handles all the tricky orchestration for you, whether you're deploying a basic website, a complex database, or something totally custom.
    
### Simplified deployment and CI/CD
- **Git Integration (Push-to-Deploy!):** You can link up your Git repositories (from GitHub, GitLab, Bitbucket, Gitea, etc). Then, Coolify can automatically build and deploy your app every single time you push new code to a specific branch. No more logging into servers manually or messing with complicated scripts – just push your code, and Coolify does the rest!
- **One-Click Services:** For popular apps and databases (like WordPress, PostgreSQL, Redis, MongoDB, etc.), Coolify offers "one-click" deployment options. Seriously, you can get a fully configured service running in minutes, without any head-scratching manual setup.
- **Custom Docker Images:** Got a specific Docker image for your app? Just give Coolify the image name, and it'll pull it down and run it for you. Easy peasy!

Services can be a single component, or be rather complex, such as the self-hosted version of supabase that need 7 or 8 different containers to work correctly. With coolify, setting up supabase only takes a few click

### Automated Essentials
Coolify handles all those crucial tasks that often trip up beginners:
- **Free SSL Certificates:** It automatically grabs and renews those important Let's Encrypt SSL certificates for your custom domains. That means secure HTTPS connections without you lifting a finger!
- **Domain Management:** You can easily assign your custom domain names to your deployed apps right from the Coolify dashboard.
- **Automatic Backups:** Set up automatic backups for your databases to S3-compatible storage. Hello, peace of mind! Your data is safe.
- **Monitoring:** Get basic checks on your server's resources and how healthy your apps are, with options for alerts if something goes sideways.

This super streamlined, automated approach means you spend way less time on boring server configuration and way more time on what you actually love: building and making your projects even better!

## Example: Getting a Minecraft Server Up with Coolify
Let's dive into a real-world example that truly shows off how easy Coolify is: setting up a Minecraft server! You'll see how effortlessly you can get even complex services running.

### What you'll need
- A server (a VPS, a dedicated machine, etc.) with Coolify already installed and ready to go.
- SSH access to your server (you'll need this for the initial Coolify setup, but less so for daily deployments).
- A domain name (optional, but it makes connecting way easier to remember!).

> I personnaly recommend using [hostinger](https://hostinger.fr?REFERRALCODE=AG8ROTOURI3W) as vps provider. Solid machines, no problems whatsoever after more than a year using their services.
    

### Here are the steps
**Log in to Your Coolify Dashboard**
Just open your web browser and go to your Coolify instance's URL (like http://your-server-ip:8000). Pop in your admin details and you're in
!![Image Description](/images/Pasted%20image%2020250522102419.png)

**Create a New Project (please stay organized.)**    
In Coolify, projects help you organize your stuff. Click on "Projects" in the sidebar, then "Add New Project." Give it a name, then create it and select the production environment.

**Add a New Resource**    
Head over to your new project (or the default one if you skipped the last step). Click "Add New Resource."    
Choose "Service" and search for "Minecraft"
!![Image Description](/images/Pasted%20image%2020250522102454.png)
    
**Configure Environment Variables**    
Minecraft servers need a few specific settings to work right. Under the "Environment Variables" section, you'll add these:
    
- `EULA`: Add this one and set it to `true`. This automatically accepts the Minecraft End User License Agreement when the server starts up.
- `MINECRAFT_MAX_MEMORY`: Decide how much RAM you want to give your server, e.g., `2G` for 2 Gigabytes. Adjust this based on your server's power and how many friends will be joining!
- `MINECRAFT_VERSION`: Pick the exact Minecraft version you want, like `1.21.1`.
- You can even add other variables here to tweak server properties, and potentially setup mods if you want to. Check the docs !
	
**Set Up Persistent Storage**
This step is SUPER important! You definitely want your Minecraft world data (all your builds, player progress, everything!) to stick around even if the server restarts or updates. Under the "Volumes" section, add a new volume.

> Wait... Actually Coolify already made the volumes for us. Nothing to do here !

**Configure Ports**
Minecraft servers usually uses port 25565. I would not recommend changing this if you're not used to configuring port mapping.
    
**Assign a Domain (Optional, but way easier to remember):**
Under the "General > Services" section, you can add your own custom domain or a subdomain (like minecraft.yourdomain.com). Coolify will automatically handle the SSL certificate for this domain, keeping it secure and making it super easy for players to remember how to join. If you don't have a domain, no worries, players can still connect using your server's IP address and port.
    
**Deploy Your Minecraft Server**    
Once everything looks good, hit that "Deploy" button! Coolify will then handle everything: pulling the Docker image, setting up the container with all your chosen settings, and firing up the Minecraft server. You can even watch the deployment logs right there in the Coolify dashboard.
    
**Connect to Your Server (Time to Play!)**
After a successful deployment, your Minecraft server will be live! Your friends can connect using your fancy domain (e.g., minecraft.yourdomain.com) or your server's IP address followed by the port (e.g., your-server-ip:25565).