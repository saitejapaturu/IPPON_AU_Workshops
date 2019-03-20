# 1️⃣ Building a website end-to-end on the Cloud ☁️ for Free 💰 (almost!)

Why end-to-end? I couldn't think of a better way to describe it. This tutorial will go 
through the a whole production example of a build

# What are we building?

**Bling Bling**
> Insert Amazing image here

# Prerequisites 
Complete these before the workshop if you can, it will save time!
Some of these instructions may differ depending on operating system.

- Credit/Debit Card for registrations
- Register:
  - namecheap.com (Domain provider)
  - cloudflare.com (CDN & Extra DNS provider)
  - cloud.google.com (Cloud provider)
  - github.com (For hosting & building your website content)
- Download and install:
  - gcloud tool for Google Cloud
  - git (managing github.com repositories and tracking code)
  - hugo our static site generator (https://gohugo.io/getting-started/installing)
  - NodeJS and npm (JavaScript woo!)

# Workshop Content
- The Code!
  - Website template
  - Pages
  - Features
  - Dynamic features
- Deployment
  - Google Cloud Tools
  - Upload to Bucket
  - Manage settings
  - Test
  - CDN
- Domains, DNS & CDN
  - [Domain Registration and Setup](#Domain-Setup)
  - Email Setup and Forwarding
  - DNS settings

# 💻 The Code

To host and run a website we have a number of options:
- Run a server ourselves (A little bit vintage but fun!)
- Upload your website/data to someone another server
- Use Wordpress (many of you may have done this)
- Use a static hosting solution (No server side scripting or code!)

Today we are choosing a more static website (you might think oh... boring but the main focus here is end-end deployment 
and we will focus less focus on programming aspects but architectural decision making and understanding how to piece everything together!

## Static websites
- A static website is primarily HTML, CSS and JS and is fully interactive on the client side
- This may include routing, local state etc.
- However we do not store state, manage sessions or authorisations

## What are we building?

- Today you will be using a static site generator plus a CMS to deliver and manage your content
- There are a number of open source static site generators
- What do they give us: Flexibility, open APIs, requires programming skills to setup. Focused on blogs, personal websites and informational websites that do not heavy backends and primary deliver information but do not accept input.

## We will be using a static site generator
- A static site generator allows us to more easily write/author content then generate relevant routes, pages and templates according to our content writen.
- Today we will be using [Hexo]() a static site generator based on the JAM Stack a relatively new concept
- Hexo gives us an easy way to write templates in HTML, style them then generate posts/pages via Markdown formatting. Markdown is a **Markup** authoring syntax to author text files. Take a look at this repo Readme.md file it's markdown!

## Getting started
Once you have the `hugo` static site generator up and running you should run through the quick start.

1. Create our new website `hugo new site myblog`
2. Enter the new directory where you created blog `cd myblog`
3. Add a theme we will be using `git clone https://github.com/olOwOlo/hugo-theme-even themes/even`
4. Copy over the config from our theme `cp themes/even/exampleSite/config.toml  config.toml`
5. **SHOULD EDIT ABOVE??**
6. Create a new blog post page `hugo new post/i_like_static_sites.md`
7. Edit your post eg `code content/post/i_like_static_sites.md`
8. Test! in the myblog dir run `hugo server -D` Your server will now be running check it out at: http://localhost:1313
9. Make some changes to your post and see the changes **Hot Update!**

https://gohugo.io/getting-started/quick-start/

# Testing locally -> then the Cloud

# 🏗️ Infrastructure

# 🌐 Domain Setup

- What is a domain and why do we have it?
- A domain points to an IP using (DNS)
- DNS allows us to resolve specific routing features within the internet
- We will register bob.com
- bob.com needs to point to our hosting provider
- a hosting provider provides the server or virtual machines to hold our website (In this case we are using Google)


1. Put a `cname` entry in for `c.storage.googleapis.com` point to our custom domain this will be used at a later stage to point to our google hosted website!

### Extra:
- Explore some of the other DNS options
- Maybe you can add some other interesting things here
- Look at [subdomains](subdomains) or redirections

# ✉️ Email Setup - Email Forwarding

We now have our nice shiny domain pointing to our website but what about emails? I want to receive emails @ myawesomedomain.com!

- To set this up we need to go back to namecheap.com and enable email forwarding, of course we could run our own email server or use a paid service but we want FREE!
- We setup a forwarding MX record in Namecheap this then forwards our address to our gmail.com domain or whatever email you prefer
- Email being sent won't be sent as this email but that can be done here as [well](well)
- Now add this new email to your blog/website if you wish and test it out
- You should be able to send any email to: `<anything>@mydomain.com`

# ☁️ Google Cloud Platform - Cloud Hosting Provider

[img](gcp.jpg)

There are numerous ways to setup and host our website. This might be static or dynamic solution. Managed or unmanaged solution. Or fully managed like a custom server that we have access to which may even be running in Sydney/Melbourne on someones Raspberry Pi.

- To get started with Google Cloud Platform we should login to the console.google.com with our Google account. Once this has been setup we will have access to Google's services.
- It may take some time so get acquanted with the UI and material style of things
- Once things have loaded check out the **Google Cloud Storage** this is Google's offering for "bucket" storage (many cloud offerings have a similar service) this is simply a static file storage. Just like Google drive but for developers! 
- We will be using GCS to host our static files generated by the static site generator in the first part of this tutorial
- Once your code works locally we need to upload it
  
To upload to GCS we can use `gcloud` tool or the web interface. `gcloud` is a command line interface allowing us submit a number of powerful commands to GCP and manage infrastructure.

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

## GCP time
1. Enable billing
2. Set billing alerts for say $10
3. Create bucket under storage
4. Upload all files in `public` generated by hugo
5. Select `permissions` and update permissions to public this will allow anyone access to this bucket
6. Add new permission for `allUsers` and give the role `Storage Object Viewer` this means anyone can access the content of the bucket. Be careful what you  upload!
7. Browse your `http` site
8. `storage.googleapis.com/yourdomainname`

Now navigate to your bucket, have a look and see if you can access your site. It should be available at: gcs.googleaapis.com/my-bucket/index.html

# ⚡ Cloudflare - Content Delivery Network (CDN)
We have finished our website, it's up and running on our new domain but we want speed. We did a test on [cdnplanet](https://www.cdnplanet.com/tools/cdnperfcheck) and our friends in the Philippines are getting slow response times 😢

To speed up content delivery times we need to cache files closer to our end users. This is what a Content Delivery Network does! A CDN caches files on servers closer to the end user. The server might be located in Australia but we can cache globally over a large network. A CDN will intelligently route traffic to those edge locations so users can reduce latency.

**This will give us https**

# Managing our website

- Upload to Google using command line gcloud tool
- Edit in Github.com
- Upload then run simple CI/CD process in github or Google Cloud

# 🔥 How can we extend this?
- Serverless
- Media hosting
- Extra subdomains and features eg. help.yourdomain.com
- Hosting on EC2 instead of S3, running your own server
- Dynamic Content (databases and libraries)
- Use another static site generator
- Attach a CMS
- Or just code your own!

# Acknowledgements

https://github.com/olOwOlo/hugo-theme-even
