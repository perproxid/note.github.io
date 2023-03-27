---
title: image_demo
date: 2023-03-26 22:24:12 +0800
categories: [demo, image]
tags: [jekyll, markdown]     # TAG names should always be lowercase
toc: true
math: true
mermaid: true
pin: false  # pin one or more posts to the top of the home page and the fixed posts are sorted in reverse order according to their release date
img_path: /assets/demo/
image: Lighthouse 1200_630.png
---

Abstract: This post is to show Markdown images rendering on [**Chirpy**](https://github.com/cotes2020/jekyll-theme-chirpy/fork), you can also use it as an example of writing.  
Now, let's start looking at the [**imaging style**].

## caption & size & shadow
  
![the phone number](windows.png){: width="200" height="50" }{: .shadow }
_caption here_  

## position

![the phone](windows.png)
_By default, the image is centered_  
  
![the phone](windows.png){: .normal }
_Image will be left aligned_  
  
![the phone](windows.png){: .left }
_Float to the left_  
- this style make photo on the left, and words on the right.  
- one can adjust the width & height of the photo to adapt the lenghth of the sentences.  
- xxxxxxx
- xxxxxxx
- xxxxxxx
- XXXXXXX

![the phone](windows.png){: .right }
_Float to the right_  
- this style make photo on the right, and words on the left.  
- one can adjust the width & height of the photo to adapt the lenghth of the sentences.  
- xxxxxxx
- xxxxxxx
- xxxxxxx
- XXXXXXX 
  
## add an image at the top of the post

- provide an image with a resolution of `1200 x 630`.   
- Please note that if the image aspect ratio does not meet `1.91 : 1`, the image will be scaled and cropped.  
- setting the image’s attribute:
```yaml
image:
  path: /path/to/image
  alt: image alternative text
```
For simple use, you can also just use `image: /path/to/image` to define the path.
