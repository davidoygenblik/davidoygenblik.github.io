---
title: 'FIRA Accepted to USENIX 2026'
date: 2025-12-17 00:00:00
featured_image: /images/USENIX_2026/venue.png
excerpt: Our work FIRA will appear in the proceedings of the 2026 USENIX Security Symposium!
---
<!--- include above for other works if better ims: featured_image
: '/images/demo/demo-square.jpg' 
use_image_in_home: True if want to display image in home screen--->

![](/images/USENIX_2026/logo.png)

Our paper, *FIRA: Enabling Automatic Forensic Investigation of Unmanned Aerial Vehicles* has been accepted to the 35th USENIX Security Symposium.

Here is a synopsis of it, more to come in a future blog post with the link to the presentation and paper:

FIRA is a novel forensic framework designed to investigate crashes of Unmanned Aerial Vehicles (UAVs) that use online learning to adapt to dynamic environments. As UAVs are often deployed in inaccessible areas with very limited bandwidth to send data back to base, in the case of a drone crash (or the drone is taken) investigators would be unable to determine if an attack on the drone's machine learning model was the cause of the failure. To bridge this gap, FIRA establishes a causal chain from sensor inputs, through the internal layers of the DL model, to the actual motor commands. It achieves this by first mapping out how software modules interact with specific groups of neurons before flight, then transmitting only the most important model updates during the mission to overcome bandwidth limits, and finally tracing the root cause backward from the time of the mission failure to find the model decision that triggered the crash. In rigorous tests across 48 real-world scenarios on both PX4 and ArduPilot platforms, FIRA correctly identified the cause of accidents with 95.8% accuracy, providing a way to secure the future of autonomous UAV missions.

[**Thank you CyFI Lab!!**](https://cyfi.ece.gatech.edu/)


