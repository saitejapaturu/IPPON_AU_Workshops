# 🎓 Ippon Australia Tech Workshop Collection

## What is this?
Tech workshops to further your understanding of real world software development workflows.

## Why?
As a student of Computer Science I was constantly expanding my knowledge in areas including Discrete Math, Algorithms/Data structures, Complexity Theory, Networking protocols and all that other fun stuff! However, there was a lack of teaching real world concepts especially ones related to higher level design, systems integration, testing and how all these amazing pieces of technologies are stitched together to really create something valuable.

## Structure
Each workshop will follow a similar structure including an introduction, steps through to complete the workshop, challenge and final solution/hints. It will be difficult and not all information will be given to you so some of this you need to figure out on your own! Some solutions and hints will be given as extras/solutions as below:

Send a new POST request using `curl` to test your login API and make sure it responds with the correct format.

<details>
<summary>Solution</summary>
<p>

```bash
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{"username":"admin","password":"admin"}' \
  http://localhost:3000/api/login
```

</p>
</details>

## Prerequisites
- Developer environment (IDE, Terminal, Admin privileges)
- Knowledge of a one programming language (eg. Java, C#, JavaScript)
- Website development knowledge including HTML, CSS and Networking/Internet theory
- Credit/Debit card for Cloud sign ups! (Don't worry GCP won't charge you)
- Git and GitHub understanding (git clone, navigating)
- Run `git clone` or fork this repo for future use
- An awesome attitude 💪

# Workshops

## 1️⃣ Building an end-to-end website on the Cloud  for free (almost!)
In this workshop you will be creating a personal blog hosted on Google Cloud Platform, you will be required to register your domain, configure DNS settings, upload files to GCP and manage hosting setup. This will be integrated with CircleCI for a CI/CD pipeline and automatic deployment. Finally you will be enabling a Cloudflare Content Delivery Network to accelerate your website and provide HTTPS.

✅ [Get Started!](Workshop_1_Website.MD)

## 2️⃣ Setting up your JavaScript build environment and getting ready for production
In this workshop you will be modifying your previous website and optimising content for production using common JavaScript build tools, packagers and test tools. We will look at SEO optimisations, compression, headers and general config.

⏳ [Coming Soon!](Workshop_2_JS_ENV.MD)

## 3️⃣ Securing your site, understanding security essentials, cookies, sessions and common attack vectors

In this workshop you will be adding more features to your website and hacking into it! Some parts of your website will be dynamic and need to be secured. We will be testing locally due the potential issues of actual hackers messing with your website! Once these are secured you can deploy to production.

⏳ [Coming Soon!](Workshop_3_Security.MD)

# 🤔 Something wrong?
Check out our contributions guide and feel free make a pull request and edit this guide ❤️

# Acknowledgements and Inspiration
https://github.com/node-girls and all their amazing work!  
https://github.com/DjangoGirls

# Need some extra help?
- Feel free to get in touch with me at bedridge at ippon.tech
- If you do have any other suggestions of other workshop ideas please let me know