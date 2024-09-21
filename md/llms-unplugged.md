---
marp: true
paginate: true
transition: dissolve 400ms
theme: uncover
class: invert
size: 16:9
style: |
  img {background-color: transparent!important;}
  a:hover, a:active, a:focus {text-decoration: none;}
  header a {color: #148ec8 !important; font-size: 24px;}
  footer {color: #148ec8;}
  /* ⬇️ Mark the image of "1" in every pages as morphable image named as "one" ⬇️ */
  img[alt="1"] {
    view-transition-name: one;
    contain: layout; /* required */
  }
  
  img[alt="2"] {
    view-transition-name: two;
    contain: layout; /* required */
  }

  /* Generic image styling for number icons */
  img:is([alt="1"], [alt="2"], [alt="3"]) {
    height: 64px;
    position: relative;
    top: -0.1em;
    vertical-align: middle;
    width: 64px;
  }
  
  @keyframes marp-transition-dissolve {
      from {
        opacity: 1;
      }
      to {
        opacity: 0;
      }
  }
header: '[LLMs Unplugged](#1 " ") / [Atyantik DevHub](https://atyantik.com)'
footer: 'Slides by [Mayur](https://www.linkedin.com/in/mayur-gohil-b9858b12a/) and [Hardip](https://hardippatel.com)'
---

# LLMs Unplugged
## Everyday Hacks and Cool bots creation!

---
## Slides

http://present.hardippatel.com/llms-unplugged.html

![bg right w:512 h:512](https://d3gh5bvik1zjmo.cloudfront.net/hardipstatics/presentations.jpg)

---

# Mayur Gohil
![1 w:256 h:256](https://media.licdn.com/dms/image/v2/D4D03AQHmJ-fgCEz-TA/profile-displayphoto-shrink_400_400/profile-displayphoto-shrink_400_400/0/1720707306887?e=1732147200&v=beta&t=AtUZqGaTI00s2UElfDviwsvyadh0TGozCpZe_YXIxBo)

Software Engineering @ [Atyantik Technologies](https://atyantik.com)

---

![1 w:128 h:128](https://media.licdn.com/dms/image/v2/D4D03AQHmJ-fgCEz-TA/profile-displayphoto-shrink_400_400/profile-displayphoto-shrink_400_400/0/1720707306887?e=1732147200&v=beta&t=AtUZqGaTI00s2UElfDviwsvyadh0TGozCpZe_YXIxBo)

### ❤️
Driving Innovation with AI | Machine Learning | NLP | Deep Learning Specialist

---

![1 w:256 h:256](https://d3gh5bvik1zjmo.cloudfront.net/hardipstatics/hardip.png)

#### [HardipPatel.com](https://hardippatel.com)
Developer @ [Atyantik Technologies](https://atyantik.com)

---

![1 w:128 h:128](https://d3gh5bvik1zjmo.cloudfront.net/hardipstatics/hardip.png)

### ❤️ 
Indie Hacking | Anime | Novels | Music | Running
...and I have endless curiosity!

---

### Let's start with -
![1](https://icongr.am/material/numeric-1-circle.svg?color=148ec8) What is AI?

![2](https://icongr.am/material/numeric-2-circle.svg?color=148ec8) What is ML?

![3](https://icongr.am/material/numeric-3-circle.svg?color=148ec8) What is DL?


---
### ![1](https://icongr.am/material/numeric-1-circle.svg?color=148ec8) What is AI?
> Artificial intelligence (AI) involves using computers to do things that traditionally require human intelligence.

---
### ![1](https://icongr.am/material/numeric-2-circle.svg?color=148ec8) What is ML?
> A subfield of AI where computer started to do things human can do

---
### ![1](https://icongr.am/material/numeric-3-circle.svg?color=148ec8) What is DL?
> A sub field  ML which help to process large amount of data. Deep learning mimics the workings of our brains. These neural networks can outperform humans at intelligent tasks like speech recognition or playing chess!

---

### How is AI working?

--- 

### Chart of AI, ML, DL
-  Research Papers
-  Ongoing Development

---

## Types of Applied AI/ML
![1](https://icongr.am/material/numeric-1-circle.svg?color=148ec8) Generative AI
![2](https://icongr.am/material/numeric-2-circle.svg?color=148ec8) Predictive/Analytical AI

---

![1](https://icongr.am/material/numeric-1-circle.svg?color=148ec8) Generative AI
   1. Single Modal (Text/Image/Video/Audio)
   2. Multi Modal

--- 

![1](https://icongr.am/material/numeric-2-circle.svg?color=148ec8) Predictive/Analytical AI
> Predictive AI blends statistical analysis with machine learning algorithms to find data patterns and forecast future outcomes. It extracts insights from historical data to make accurate predictions about the most likely upcoming event, result or trend.
 
---
![1](https://icongr.am/material/numeric-2-circle.svg?color=148ec8) Predictive/Analytical AI

- TimeSeries Forecast

---

## Coolbots!
![1](https://icongr.am/material/numeric-1-circle.svg?color=148ec8) Cursor AI (IDE)
![2](https://icongr.am/material/numeric-2-circle.svg?color=148ec8) ChatGPT assistants

---
![2](https://icongr.am/material/numeric-2-circle.svg?color=148ec8) ChatGPT assistants
- [Integrate Easy](https://chatgpt.com/g/g-vr4IpsqGM-integrateeasy)
- [Clean your code](https://chatgpt.com/g/g-29jiCjHfj-make-the-code-clean)
- [Chat with your code](https://chatgpt.com/g/g-34wthuFSb-chat-with-code)
- [Linkedin Roaster](https://chatgpt.com/g/g-Ll9hk3dPu-social-roaster)
---

## Coolbots!
![1](https://icongr.am/material/numeric-1-circle.svg?color=148ec8) Anything LLM
![2](https://icongr.am/material/numeric-2-circle.svg?color=148ec8) Groq
![3](https://icongr.am/material/numeric-3-circle.svg?color=148ec8) ComfyUI

---

# Google Colab
<!-- _class: invert lead -->
![1 w:400 h:200](https://storage.googleapis.com/gweb-uniblog-publish-prod/images/Colab_Hero.width-1600.format-webp.webp)

* [Intro](https://colab.research.google.com/drive/1nVBN1fVQwFqL-9D7pzOxso7kPA_6vcv4?usp=sharing)
* [LLM inference](https://colab.research.google.com/drive/1qTiH51xgA_6GZDqS0b2ASfPwKMWQhJ9t?usp=sharing)
* [LLM inference 2](https://colab.research.google.com/drive/1q-FHd5aKUTdRF0G4p1ijzWI0Sf27uO-t?usp=sharing)
* [LLM with finetuning](https://colab.research.google.com/drive/1tU3_k3-o_AAg-ZkK93H9TfMCmPg86wD3?usp=sharing)

---

# Can we make a quick UI for this?

---

# Yes!

---

# Can we make a quick API out of this?

---

# Yes!

---

1. How to work with constantly updating data?
    1. What is RAG?
    2. Why is RAG?
    3. How to RAG?
    4. Example for RAG?
       1.  Cross-platform api integration bot

---

![1 w:700 h:300](https://d3gh5bvik1zjmo.cloudfront.net/hardipstatics/rag_1.png)

---
![2 w:700 h:300](https://d3gh5bvik1zjmo.cloudfront.net/hardipstatics/rag_2.png)

---
![3 w:700 h:300](https://d3gh5bvik1zjmo.cloudfront.net/hardipstatics/rag_3.png)

---

When to use Prompting vs Finetuning vs RAG

![4 w:700 h:400](https://d3gh5bvik1zjmo.cloudfront.net/hardipstatics/ragvspromptingvsfinetuning.png)

---

<!-- _class: invert lead -->
# Questions

---

<!-- _class: invert lead -->
# More questions?

---

<!-- _class: invert lead -->
# Thank you for your time!

---

<!-- _class: invert lead -->
# Thank you for your time 
# ...and money!