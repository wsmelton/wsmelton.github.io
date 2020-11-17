---
layout: post
title: VS Code New Window Size
categories: azure, vscode
---

If you use [VS Code](https://code.visualstudio.com/), you may have found that when you have a current workspace open and want to open a new one, it may be sized extremely small. Mine would always open to around 300x500 and be positioned in the center of the screen.

Windows has support for saving the window size by holding the `Shift` key down while closing the window (click the `x`). I tried this with no result; the window continued to open up smaller than the original window.

I decided to check the user settings of Code. I searched for `window size` and found the setting that controls that new window sizing:

```
window.newWindowDimensions
```

Each option controls what size and position you get for the window:

| Setting | Description |
| ------------ | ------------- |
| default | Open new windows in the center of the screen |
| inherit | Open new windows with same dimensions as last active one |
| offset | Open new windows with same dimensions as last active one with an offset position|
| maximized | Open new windows maximized |
| fullscreen | Open new windows in full screen mode |

So fix for that small screen being opened is merely adjusting the setting. I  am using `offset` for now, and it works like a charm. 
