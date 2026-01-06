---
layout: post
title: Removing Image Transparency - No need for a webservice 
---

When downloading AI-generated images from tools like ChatGPT, Gemini, or Google's latest models, it's common to find that what looks like a transparent background (checkerboard) is actually a flat part of the image, or it might just be a solid white background despite the `.png` extension.

### Quick Transparency Check

The fastest way to verify if an image is actually transparent is to download it and **drag it into your browser**. If the image has a real transparent background, it will take on your browser's default background color (or system theme color). If you still see a white background or a static checkerboard, it's not transparent.

### Removing the Background

If you find that your image has a solid background (like white) that you want to remove, you can use ImageMagick. If you have it installed, you can use the following command to make the background transparent based on the color of the top-left pixel:

```bash
magick input.png -fuzz 15% -transparent "%[pixel:p{0,0}]" output.png
```

This command uses a 15% fuzz factor to account for slight color variations and sets the color found at coordinate `0,0` (the top-left corner) to transparent.

Tested with ImageMagick 7.1.1-47 self compiled.

This post was in part written by Google Gemini - I don't mind it's a reference for my future self.
