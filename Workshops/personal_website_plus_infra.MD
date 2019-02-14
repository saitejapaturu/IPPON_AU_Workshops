# A personal website hosted on Google with Cloudflare (CDN) and modern cloud features

## Pre-setup
- Registrations
  - namecheap.com (Domain provider)
  - cloudflare.com (CDN)
  - cloud.google.com (Cloud provider)
- An IDE
- Credit Card for Sign ups

# Domain Setup

- What is a domain and why do we have it?
- A domain points to an IP using (DNS)
- DNS allows us to resolve specific routing features within the internet
- We will register bob.com
- bob.com needs to point to our hosting provider
- a hosting provider provides the server or virtual machines to hold our website (In this case we are using Google)

# Email Setup

- We want to sent emails to our new domain how do we do that?
- We setup an MX record in Namecheap this then forwards our address to the standard gmail.com domain

# Cloud Setup

- There are numerous ways to setup our website
- This might be static and managed (eg. No control of server only blob storage)
- Or fully managed like a custom server that we have access to which may even be running in Sydney/Melbourne

# Cloudflare (A CDN - Content Delivery Network)

- What does it do?
- A CDN caches copies of your data on servers globally to reduce time taken to download these copies
- Updating

# Managing our website

- Upload to S3 using command line
- Edit in Github.com
- Upload then run simple CI/CD process

# How can we extend this?
- Serverless
- Media hosting
- Extra subdomains and features
- Hosting on EC2 instead of S3
- Dynamic Content (databaes and libraries)