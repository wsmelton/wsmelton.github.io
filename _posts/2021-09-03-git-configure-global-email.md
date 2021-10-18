---
layout: post
title: Git - Configure Global Email
---

If you work with GitHub or other hosted version control systems they all work with Git. One of the things Git does when you first try and push (or write) to a hosted Git repository is prompt you to login. GitHub when you do this by default will link all of your commits made to the default email address you have configured on your profile.

## What Email is used?

Under your profile settings in GitHub you can identify what email address(es) is configured by looking under the `Emails` section:

![image](https://user-images.githubusercontent.com/11204251/132080102-d02ee008-afa2-41c2-8312-3af369f5feae.png)

You can configure multiple but a default, primary will be configured as the first email you used to create your account. As you add additional emails you can then change when address is your primary.

## Secure Your Email Address

If you are not aware, a common practice these days is companies are trolling contributors and maintainers of open-source projects. I have personally had it happen a few times, and had one company tell me they got my eamil from the commit history of dbatools.

A method that can help you keep this from happening is enabling the two settings below under the Emails section of your profile on GitHub:

![image](https://user-images.githubusercontent.com/11204251/132080178-4071c473-901d-4cae-954c-32808ba556dc.png)

When you enable the `Keep my email address private` you will see a no-reply email address is generated and provided. The email name is generated from your username on GitHub, prefixed with a randomly generated 8-digit number.

In addition, you can check the box for blocking commits that are using your private email from being pushed to GitHub's site.

## Configure Git Global Email

Once you have installed Git client on your machine you can configure the global setting for your email to be set to that no-reply address. Setting this globally prevents the need of setting it on each local repository.

Easiest way to do this is using the Git UI that comes with the client.

After you open the Git Gui, you first need to open an existing repository on your machine. You can then go to **Edit > Options** and will see on the right side the Global settings.

![image](https://user-images.githubusercontent.com/11204251/132080419-a5a5be0d-1d1c-45cc-9fd4-1f4aed796b23.png)

Replace the current email address with your no-reply, and then **click Save** at the bottom of the window.

I have added this as a setup step on any new machine I setup now.
