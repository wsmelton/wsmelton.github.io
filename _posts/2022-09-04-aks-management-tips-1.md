---
layout: post
title: AKS Management - Tip 1
---

## AKS Management

This is the start of a series of posts as I come across tips and tricks for managing the Azure Kubernetes Service. These may be scripts, utilities (CLI or apps), and other various things that come across my keyboard as I work with AKS.

### K9s

<img src="https://k9scli.io/assets/k9s.png" width="200"/>

[K9s](https://k9scli.io/) is a utility that is a great for helping you get around and discover resources in a Kubernetes cluster through a terminal interface. It takes care of interacting with `kubectl` command for you so your cluster could run on-premises or in Azure.

### Get Started

You can find the [install instructions](https://k9scli.io/topics/install/) offer multiple methods based on your OS and preference. To install this using Chocolatey:

```console

choco install k9s -y

```

You can verify the installation after that by running:

```console

k9s version

```

You will see output similar to:

<img src="https://user-images.githubusercontent.com/11204251/188331976-c0cf444c-2796-41e3-af96-dfac6de8886b.png" />

### Use

You can run the command with various flags to control what scope it runs for a cluster. If you just run `k9s` with no flags, it will open the command-line graphic to the whole cluster.

<img src="https://user-images.githubusercontent.com/11204251/188332127-0cb5db69-9623-46d8-b41e-b20f01ca1bcc.png"/>

After you have the application running, there are a few keyboard shortcuts that are useful to help get around. Every screen you will have these quick keys accessible. They are visible on the screen at all times:

<img src="https://user-images.githubusercontent.com/11204251/188332335-1deeb7b4-1342-4e54-847e-2b05adffabf4.png"/>

Others to be aware of starting out:

- <kbd>ESCAPE</kbd> -- Escape key is used to go back to the previous screen

- <kbd>CTRL</kbd>+`c` -- Used to quit the application.

- <kbd>:</kbd> -- (colon) will bring a command prompt up where you can type an alias to move around to different areas of the cluster. You can start typing a few characters and intellisense/tab completion will be available.

    <img src="https://user-images.githubusercontent.com/11204251/188332978-96714bab-e3da-4c52-a014-0587b12e48ab.png" />

- <kbd>CTRL</kbd>+`a` -- this will bring up a complete list of all the alias that you can use in the prompt

- <kbd>SHIFT</kbd>+`f` -- this bring up a prompt for configuring port-forwarding on the selected pod or container (dependent upon what context your view is on at the time)

    <img src="https://user-images.githubusercontent.com/11204251/188332582-bdd2aabb-3b2c-4bf5-8020-e94921f3ac5d.png"/>

- <kbd>:</kbd>+`ctx` -- the alais `ctx` allows you to change context of the current cluster. A big time saver when things are busy.

    <img src="https://user-images.githubusercontent.com/11204251/188332828-16b7a789-d595-4886-9103-aedde3155f19.png"/>

## Closing

The terminal interaction that K9s offers is extremely useful for those still learning how to get around a cluster using `kubectl`. As well, even if you are already familiar with `kubectl` it saves a lot typing when you manage several clusters.
