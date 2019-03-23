# Building an end-to-end website on the Cloud ☁️ for Free 💰 (almost!)

![alt text](media/Workshop1/website.png "Screenshot of final design")

# Introduction

## Why?
Why end-to-end? I couldn't think of a better way to describe it. This workshop will help guide you through a full production cloud deployment of your own personal blog plus domain name. yourawesomename.com you might have automatic deployment, secure HTTPS and awesome performance depending on how far you get!

## What are we building?

- Today you will be using a static site generator `hugo` to deliver and manage your content
- a static site generator based on the JAM Stack a relatively new concept
- There are a number of open source static site generators
- What do they give us: Flexibility, open APIs, requires programming skills to setup. Focused on blogs, personal websites and informational websites that do not require heavy backends and primarily deliver information but do not accept input.
- A static site generator allows us to more easily write/author content then generate relevant routes, pages and templates according to our content writen.
- Hugo gives us an easy way to write templates in markdown, style them then generate posts/pages via Markdown formatting. Markdown is a **Markup** authoring syntax to author text files. This file is written in github.com flavour of Markdown

## 📚 Resources
https://jamstack.wtf/  
https://www.staticgen.com/  
https://headlesscms.org/

## Prerequisites 
Complete this before the workshop if you can, it will save time! Some of these instructions may differ depending on operating system.

- Credit/Debit Card
- Registrations:
  - [NameCheap](namecheap.com) Domain provider
  - [Cloudflare](cloudflare.com) CDN & Extra DNS provider
  - [Google Cloud Platform](https://console.cloud.google.com/freetrial) (Credit/Debit card required)
  - [GitHub](github.com) (Hosting & building your website content)
- Download and install:
  - [Hugo](https://gohugo.io/getting-started/installing) a static site generator with markdown syntax 
  - [NodeJS](https://nodejs.org/en/download/)
  -  [Google Cloud SDK including `gcloud`](https://cloud.google.com/sdk/install)
  - [Git](https://git-scm.com/downloads) (managing github.com repositories and tracking code)

# Contents
- The Code!
  - Website template and pages
  - Features
  - Dynamic features
  - Make some changes
- Deployment
  - Google Cloud Tools
  - Upload to Bucket
  - Manage settings
  - Testing
  - Setting up our CDN
- Domains, DNS & CDN Config
  - [Domain Registration and Setup](#Domain-Setup)
  - Email Setup and Forwarding
  - DNS settings
  - Final Testing


# 💻 Static websites

## Why do we want a static website?
- A static website is primarily HTML, CSS and JS and are fully interactive on the client side
- This may include routing, local state etc.
- However we do not store state, manage sessions or authorisations

### To host and run a website we have a number of options:
- Run a server ourselves (A bit vintage but fun!)
- Upload your website content to another server managed elsewhere
- Use a fully managed solution such as Wordpress
- Use a static hosting solution (No server side scripting or code!)

Today we are primarily looking a more static website oh... boring but the main focus here is end-end deployment 
and we will focus less focus on programming aspects but architectural decision making and understanding how to piece everything together!

## Getting started
Based on: https://gohugo.io/getting-started/quick-start/

Once you have the `hugo` static site generator up and running you should run through the quick start.

1. Create our new website `hugo new site myblog`
2. Enter the new directory where you created blog `cd myblog`
3. Find a theme you like! Currently we are using https://github.com/olOwOlo/hugo-theme-even if you don't like this you can find another.
4. Add a theme we will be using `git clone https://github.com/olOwOlo/hugo-theme-even themes/even`
5. Copy over the config from our theme `cp themes/even/exampleSite/config.toml  config.toml`
6. Create a new blog post page `hugo new post/i_like_static_sites.md`
7. Edit your post eg `code content/post/i_like_static_sites.md`
8. Test! in the myblog dir run `hugo server -D` Your server will now be running check it out at: http://localhost:1313
9. Make some changes to your post and see the changes (it should have hot reloading!)
10. Create a new blog post and pages relevant to your wishes or skip if you wish to get to the nitty gritty deployment
11. Run `hugo -D` you will build all your assets including files marked as drafts
12. check the `public` directory to see you HTML

**Be careful you may need configure the base url correctly**

# ☁️ Google Cloud Platform - Cloud Hosting Provider

![alt text](media/Workshop1/bucket_creation.png "Screenshot of final design")

There are numerous ways to setup and host our website. This might be static or dynamic solution. Managed or unmanaged solution. Or fully managed like a custom server that we have access to which may even be running in Sydney/Melbourne on someones Raspberry Pi.

- To get started with Google Cloud Platform we should login to the console.google.com with our Google account. Once this has been setup we will have access to Google's services.
- It may take some time so get acquanted with the UI and material style of things
- Once things have loaded check out the **Google Cloud Storage** this is Google's offering for "bucket" storage (many cloud offerings have a similar service) this is simply a static file storage. Just like Google drive but for developers! 
- We will be using GCS to host our static files generated by the static site generator in the first part of this tutorial
- Once your code works locally we need to upload it
  
To upload to GCS we can use `gcloud` tool or the web interface. `gcloud` is a command line interface allowing us submit a number of powerful commands to GCP and manage infrastructure.

## It's GCP time
1. Enable billing
2. Set billing alerts for say $10 just so you don't waste that free credit!
3. Create a bucket under storage with a name like: `bens-website-dev`
4. Create another bucket under storage with your domain if you have one `example.com`
5. Upload all files in `public` generated by hugo
6. Select `permissions` and update permissions to public this will allow anyone access to this bucket Add new permission for `allUsers` and give the role `Storage Object Viewer` this means anyone can access the content of the bucket. Be careful what you upload!
7. Browse your `http` site
8. http://storage.googleapis.com/bucketname where bucketname is the chosen name of your bucket

## Editing our config.toml

To deploy on a domain other than locally we need to configure hugo via the `config.toml` file. Update the changes as below:

```
baseUrl = "https://<your domain>"  
title = "Choose and awesome title"
```

To submit your static files to GCP
```
gcloud /dist <bucket-name>

```

We now need to build our site with hugo
1. `hugo`
2. Now check the `myblog/public/` you will see all your generated static site content is here!
3. Open the index.html
4. Boom! Website done
5. Now time to upload to GCP
6. `gsutil rsync -R local-dir gs://www.example.com`

Now navigate to your bucket, have a look and see if you can access your site. It should be available at: gcs.googleaapis.com/my-bucket/index.html

## 🔥 Extra:
- Keep exploring the GCP console
- Look at alternative static site generators
- Keep digging into hugo

# Managing our website

- Upload to Google using command line gcloud tool
- Edit in Github.com
- Upload then run simple CI/CD process in github or Google Cloud

# 🌎 Domain Setup

- Maybe I gave you a free domain, maybe you have one, if not I highly recommend you get one! Perfect for experimentation and all manner of fun!
- What is a domain and why do we have it?
- A domain points to an IP using (DNS)
- DNS allows us to resolve specific routing features within the internet
- Register yourawesomedomain.com or whatever
- This domain will need to point to our hosting provider (Google)
- A hosting provider provides the server or virtual machines to store our website content (In this case we are using Google)

1. Put a `cname` entry in for `c.storage.googleapis.com` point to our custom domain this will be used at a later stage to point to our google hosted website!

## 🔥 Extra:
- Explore some of the other DNS options
- Maybe you can add some other interesting things here
- Look at [subdomains](subdomains) or redirections
- Read into DMARC email validation

# ✉️ Email Setup

We now have our nice shiny domain pointing to our website but what about emails? I want to receive emails @ myawesomedomain.com!

- To set this up we need to go back to namecheap.com and enable email forwarding, of course we could run our own email server or use a paid service but we want FREE!
- We setup a forwarding MX record in Namecheap this then forwards our address to our gmail.com domain or whatever email you prefer
- Email being sent won't be sent as this email but that can be done here as [well](well)
- Now add this new email to your blog/website if you wish and test it out
- You should be able to send any email to: `<anything>@mydomain.com`

## 🔥 Extra:
- Read into DMARC email validation with DNS
- Setup your own email forwarding on AWS using SES
- Setup free sender emailing service so you can send emails from your domain eg. Received from me@awesomedomain.com rather than forwarding to your gmail.com email.

# ⚡ Cloudflare - Content Delivery Network (CDN)
We have finished our website, it's up and running on our new domain but we want speed. We did a test on [cdnplanet](https://www.cdnplanet.com/tools/cdnperfcheck) and our friends in the Philippines are getting slow response times 😢
To speed up content delivery we need to cache files closer to our end users. This is what a Content Delivery Network does! A CDN caches files on servers closer to the end user. The server might be located in Australia but we can cache globally over a large network. A CDN will intelligently route traffic to those edge locations so users can reduce latency.

**This will give us https**

## 🔥 Extra:
- Explore some of the other DNS options
- Maybe you can add some other interesting things here
- Look at [subdomains](subdomains) or redirections
- Read into DMARC email validation

# Automatic Deployment

## What if we could do all of this ourselves?

We can make use of github as our CI/CD toolkit, there are other options but we will keep it simple.

https://developer.github.com/webhooks/

## Github auto deployment

1. Fork this repository or create your own
2. First setup github.com hooks for when you make changes to your repository
3. A hook is basically a request made by github.com to an endpoint of your choice
4. Our endpoint will be a serverless function that reads in our github repository from the repo, runs hugo, builds and then pulls in the release updating our Google Cloud Storage

## 🔥 Extra:
- Look into open source CI/CD platforms
- gitlab.com providers some great features utilising containerisation
- Setup your own more complicated CI/CD pipeline


# 🔥 Additional Features
- Dynamic content
  - 3rd party (form submissions, comment sections)
  - Serverless mailer function for contact form
- Extra subdomains and features eg. help.yourdomain.com
- Switching the host to Amazon?
- Check out another static site generator or headless CMS

# Acknowledgements
https://github.com/olOwOlo/hugo-theme-even
