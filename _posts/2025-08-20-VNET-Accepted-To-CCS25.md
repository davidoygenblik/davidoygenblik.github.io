---
title: 'VillainNet Accepted to CCS 25'
date: 2025-08-20 00:00:00
featured_image: /images/CCS25/paper.png
excerpt: My paper, 'VillainNet Targeted Poisoning Attacks Against SuperNets Along the Accuracy-Latency Pareto Frontier', has been accepted to CCS25!
---
<!--- include above for other works if better ims: featured_image
: '/images/demo/demo-square.jpg' 
use_image_in_home: True if want to display image in home screen--->

![](/images/CCS25/logo.png)

I am very excited to present my work, *VillainNet: Targeted Poisoning Attacks Against SuperNets Along the Accuracy-Latency Pareto Frontier* at the 32nd ACM Conference on Computer and Communications Security (CCS)! 

Here is a synopsis of it, more to come in a future blog post with the link to the presentation and paper:

State-of-the-art SuperNets improve AI adaptability by dynamically activating different subnetworks. This dynamism is a double-edged sword as it makes AI deployment more flexible, but also creates a wider attack surface. This paper introduces VillainNet (VNET), a novel poisoning attack that allows an adversary to implant a stealthy backdoor that activates only within specific, attacker-chosen subnetworks, while remaining dormant across billions of other configurations. VNET achieves this precision by using novel distance metrics—based on architectural and computational similarity—to confine the backdoor's effects exclusively to targeted subnetworks during the training process. The method is highly effective, achieving a ~99% attack success rate in targeted subnetworks while increasing the cost of detection for defenders, requiring them to sample on average 66 different subnetworks to detect the attack.

[**Thank you CyFI Lab!!**](https://cyfi.ece.gatech.edu/)



