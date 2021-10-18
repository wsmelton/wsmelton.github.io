---
layout: post
title: GitHub Issue Forms Beta
---

## Forms are Finally Here!!!

June 23, GitHub announced [Issue Forms beta for public repositories](https://github.blog/changelog/2021-06-23-issues-forms-beta-for-public-repositories/). If you are a maintainer of an open-source project on GitHub, issues are the lifeblood of your project for your userbase to interact and report bugs and features. [Discussions](https://docs.github.com/en/discussions) is also an option but most generally stick with using GitHub Issues.

GitHub uses YAML for GitHub Actions and various other features in repositories that let you define what you want in code rather than using a UI. Issue Forms uses this and a change from the markdown style that we use up to this point.

The use of Issue Forms allows you more control over what users can input on a specific issue. In the markdown style, all we can do is provide comments or suggestions, and as users submit them, we hope for the best. If you get many users that simply select all text and remove it, then your template serves no purpose. Issue Forms helps with all of this and gives you the control of at least asking them for specific details in a given text box, drop-down, or checkbox.

An example drop-down option, where you can also see the red `*` that means a selection has to be done before the issue can be submitted.

![image](https://user-images.githubusercontent.com/11204251/126049353-0d3421af-a362-404b-a710-4883c7844311.png)

The only requirement for using this feature currently is the repository has to be public. I created a public repository, [wsmelton/testing-issue-templates](https://github.com/wsmelton/testing-issue-templates/tree/main/.github/ISSUE_TEMPLATE) if you would like to see a few live and interact with them.

I've also implemented them for the following projects I am a maintainer for as well:

- [dbatools](https://github.com/sqlcollaborative/dbatools)
- [Thycotic.SecretServer](https://github.com/thycotic-ps/thycotic.secretserver)

## More Information

More details on the Issue Forms:

- [Configuring Issue Templates](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository)
- [YAML Syntax Issue Forms](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-issue-forms)
- [Issue Forms Feedback](https://github.com/github/feedback/discussions/categories/issues-feedback)
