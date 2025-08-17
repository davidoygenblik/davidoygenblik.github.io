---
title: 'ZEN Accepted to NDSS 26'
date: 2024-08-11 00:00:00
featured_image: images/initial_photos/profile_pic.JPG
excerpt: My paper, 'Achieving Zen Combining Mathematical and Programmatic Deep Learning Model Representations for Attribution and Reuse', has been accepted to NDSS26!
---
<!--- include above for other works if better ims: featured_image
: '/images/demo/demo-square.jpg' 
use_image_in_home: True if want to display image in home screen--->

![](/images/NDSS26/ndss_26.png)

My paper, *Achieving Zen Combining Mathematical and Programmatic Deep Learning Model Representations for Attribution and Reuse* has been accepted to the
the 33rd Network and Distributed System Security (NDSS) Symposium.

Here is a synopsis of it, more to come in a future blog post with the link to the presentation and paper:

Existing techniques for recovering and analyzing AI models from black-box systems are insufficient for practical use as  they only extract the model's weights, layers, and structure while ignoring the underlying code that actually defines *how* the model uses those recovered components. This paper introduces ZEN, a novel framework that bridges this gap by recovering a model's "unified representation", essentially a unique fingerprint combining both its mathematical structure (weights, layers, graph structure, etc.) and its programmatic implementation (code) from a memory image. Using this fingerprint, ZEN automatically attributes an unknown black-box model to a known open-source base model and generates code patches to replicate the black-box model's custom functionality. In evaluations across 21  models, ZEN successfully attributed every custom model to its correct base with 100% accuracy, enabling full model reuse for white-box analysis.

[**Thank you CyFI Lab!!**](https://cyfi.ece.gatech.edu/)



