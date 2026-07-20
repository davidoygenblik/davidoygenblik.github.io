---
title: 'FAULT Accepted to CCS 26'
date: 2026-07-20 00:00:00
featured_image: /images/CCS26/hague.jpg
excerpt: My paper, 'Finding FAULTs in Architectural Backdoors Why Trigger Detection Fails Under Real-World Conditions', has been accepted to CCS26!
---
<!--- include above for other works if better ims: featured_image
: '/images/demo/demo-square.jpg' 
use_image_in_home: True if want to display image in home screen--->

![](/images/CCS26/logo.png)

I am very excited to present my work, *Finding FAULTs in Architectural Backdoors: Why Trigger Detection Fails Under Real-World Conditions* at the 33rd ACM Conference on Computer and Communications Security (CCS) in The Hague, Netherlands!

Here is a synopsis of it, more to come in a future blog post with the link to the presentation and paper:

Architectural backdoors (ABs) hide malicious logic inside a deep learning model's *inference code* rather than its weights, letting them slip past every technique that vets a model's parameters. This paper asks whether that threat survives real-world deployment, and shows that it does not. Our key insight is that every existing AB detector reduces to the same operation: scoring how closely an input region matches a fixed trigger pattern, then thresholding that score. From this we formalize three fundamental limitations. First, the input transformations routinely applied before inference (cropping, contrast, noise, denoising) corrupt the trigger before it is ever detected. Second, turning sensitivity back up to recover attack success inflates false positives and visibly degrades benign accuracy. Third, more complex triggers only widen the space of benign inputs that falsely fire the detector. We build FAULT, a framework that traces the full attack-success, accuracy, and false-positive trade-off for any AB under any preprocessing. Across the GTSRB, CIFAR10, and Mapillary datasets, no sensitivity setting yields both a meaningful attack success rate and benign accuracy near baseline, capping an optimally tuned attacker at a roughly 10 to 20 percent success ceiling. As currently constructed, architectural backdoors cannot be both effective and stealthy in realistic deployments.

[**Thank you CyFI Lab!!**](https://cyfi.ece.gatech.edu/)


