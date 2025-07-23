# How We Built CloudBliss: A Developer's Journey
*By Inflate Team - July 2025*

---

## The Beginning of Another Dream

It was either February 2nd or 3rd, 2025 (honestly, I don't remember the exact date), on an evening Discord call when my friend Abhinav and I decided to give another shot at building a startup. This wasn't our first rodeo – we'd tried several ventures before, each teaching us something valuable.

---

## Our Previous Adventures (2019-2024)

### The Discord Empire Days (2019-2021)
Our first real attempt started with Discord server creation. I teamed up with my Discord friends – b--e, m--x, te--y, and others – forming a 6-7 person team. We actually built 3-4 scam Nitro gift servers (yeah, not proud of that), but everything crashed when our accounts got suspended by Discord for hacking involvement. The funny part? We got scammed by a fake zg--ng ourselves – karma, right?

### The Bot Development Service (2022)
Our second venture was a Discord bot development service. It taught us a lot about client management and technical delivery, but didn't quite take off the way we hoped.

### The Minecraft Server That Almost Was (2023)
This one hurt. We were 60-70% completed with a Minecraft server, and even got Triggered Insaan invited to join! But internal conflicts led to me leaving the team and, well... I might have crashed the whole server since I was paying for those heavy AWS instances. Expensive lesson learned.

### The Role-Play Revolution (2023)
Our fourth attempt was a Discord-based role-play server – the most complex project at that time. Multiple bots, intricate systems, the works. But again, team dynamics got in the way.

### Lasthub: The Cloud Service Attempt (2024)
Named after my previous friend "Last" (nis--t), this was a cloud/VM service I ran with my partner (ps--ys). We actually got 5 customers and earned money! But insufficient starting funds killed it. We had to refund everyone. The service still exists as "Sokuwe" today.

---

## The Birth of Inflate & CloudBliss

### The Midnight Eureka (February 3, 2025)
After our long discussion about what to do next, inspiration struck at midnight (as it often does). I told Abhi about my idea: a freelancing agency platform built on Discord. The concept was simple but powerful – help new freelancers learn the market by giving them our Fiverr projects, taking a 40% cut while they kept 60%.

### The Foundation
- **Name**: "Inflate" (Abhi's ChatGPT suggestion)
- **Logo**: 100% AI-generated (and we still haven't changed it!)
- **Domain**: inflate.live (got it free for a year from GitHub Student Developer Pack)
- **Launch Date**: April 10, 2025

We completed the Discord server foundation in just 2 days, but customer acquisition proved challenging. Free marketing and friend invitations didn't generate the traction we needed.

---

## The Pivot to Innovation

### Expanding the Vision
Instead of abandoning the project, I suggested turning Inflate into a parent company with multiple sub-projects. Abhi loved the idea. Using ChatGPT (100% usage, let's be honest), we conceptualized four projects:

1. **Freelancing Agency** (original idea)
2. **InflateStorage** (now CloudBliss)
3. **InflateVM** (Sokuwe)
4. **IBM** (Inflate Backend Management - later discontinued)

---

## CloudBliss: From Concept to Reality

### The Problem That Changed Everything (March 27, 2025)
My Google Drive was completely choked – 37GB used out of 30GB limit after my premium expired. I couldn't even receive emails! This personal pain point sparked the evolution of InflateStorage from a simple file-sharing platform into something revolutionary.

**The Vision**: Decentralized storage with literally unlimited capacity.

### The Challenge
Abhi questioned the feasibility: "How will you provide unlimited storage?" The solution came from my Minecraft server experience – using private established servers (currently over 100 servers with 100TB+ capacity) working like server jars where multiple players can join.

---

## Technical Development Journey

### UI/UX Development
The entire interface was built using Lovable-dev (formerly GPT-Engineer). It worked beautifully, but we soon realized we needed something more.

### The Security Awakening (April 5, 2025)
Privacy and security concerns led us to research encryption solutions. Using ChatGPT and other AI agents, we developed a comprehensive security strategy. This wasn't just about storage anymore – we were building the world's most secure cloud storage service.

### RES54: The Encryption Beast
Between April 6-8, 2025, I developed RES54 – currently the world's best encryption and decryption model featuring:
- **AES256+GCM encryption**
- **Block splitting technology**
- **Split file obfuscation**
- **97+ commits** just for this system alone

### The Rebrand (April 8, 2025)
Late evening on April 8th, we decided to change from "InflateStorage" to "CloudBliss" – which had actually been our internal project name all along. InflateStorage felt too old-school.

---

## Launch and Evolution

### Beta Launch (April 10, 2025)
CloudBliss launched in beta alongside Luupz (LearningLoops) and Sokuwe. The beta version (v1.5) only had basic file uploading and downloading features.

### Version 2 (May 10, 2025)
The first major update brought:
- Dedicated storage file system
- Improved UI/UX
- Parallel downloading/uploading
- Settings tab
- Enhanced RES54 (200 file requests per second)
- Additional security layers

### Version 5 (July 6, 2025) - The Game Changer
Our biggest update included:
- **Working file sharing system**
- **Admin system**
- **Dedicated Security Guardian v1**
- **Service Worker v5**
- **Instant file viewing**
- **Multiple upload methods**
- **File info system**
- **About tab**
- **Developer Program v1** (API keys)
- **Archive manager**
- **Improved auth handler** (Google login, password reset, MFA)

---

## How CloudBliss Actually Works

### The Architecture
CloudBliss is entirely server-side focused, designed for privacy-conscious users. Our team of 3 has built something truly unique.

### Upload Process
When you upload a file (let's say `bill.jpg`, 10MB):

1. **Client Service Worker** receives the request
2. **Connection established** with Server Service Worker
3. **Metadata sent** to Supabase database
4. **File encryption** with obfuscation (`bill.jpg` becomes `ckcjddi432`)
5. **Edge function** processes the encrypted file
6. **Secondary encryption** with RES54's AES256+GCM
7. **File splitting** (splits into n² parts, 1-1000 random segments)
8. **Metadata storage** in Supabase
9. **Random distribution** across storage devices/repositories

### Download Process
When you download `bill.jpg`:

1. **Request sent** through Client Service Worker → Server Service Worker → RES54
2. **File ID collection** from database
3. **CB_MFS indexing** (custom indexer matching metadata ID)
4. **Combulator Module** combines and decrypts all segments
5. **File delivered** to user's download

**Average processing time**: 2-3 seconds (varies with file size)

### Decryption Model
The most complex part involves:
- **Dual key system** (server-side + client-side encryption keys)
- **Reverse engineering process** for decryption
- **Service Worker coordination** for key management

---

## Challenges and Resilience

### The Great Outage (June 21, 2025)
Supabase faced unhandleable traffic, affecting our app severely. Server-side workers experienced:
- **Extended response times**
- **Frequent crashes**
- **Timeout issues**
- **1,283ms ping problems**

This taught us the importance of redundancy and alternative infrastructure planning.

---

## Current Statistics (July 23, 2025)

As we write this, CloudBliss has achieved:
- **45+ active users**
- **400+ files uploaded**
- **753+ files downloaded**
- **20+ GB storage consumed**

### What's Next?
We're preparing CloudBliss v6.1 for August 10, 2025, featuring:
- **Bug fixes** from v5
- **Dedicated Security Guardian v2**
- **Enhanced stability**
- **Performance optimizations**

---

## Conclusion

Building CloudBliss has been an incredible journey of technical innovation, problem-solving, and persistence. From a simple Discord call to a revolutionary cloud storage platform, we've learned that the best solutions often come from solving your own problems.

Thank you to everyone who has supported us on this journey! The future of secure, unlimited cloud storage is here, and it's called CloudBliss.

*Special thanks to our amazing users, the AI tools that helped us innovate, and the countless hours of debugging that made this dream a reality.*

---

**Team Inflate**  
*Building the future, one innovation at a time*