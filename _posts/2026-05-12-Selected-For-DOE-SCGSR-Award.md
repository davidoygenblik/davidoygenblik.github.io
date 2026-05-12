---
title: 'Selected for the DOE Office of Science Graduate Student Research (SCGSR) Award'
date: 2026-05-12 00:00:00
featured_image: /images/NLR/picture_of_NLR.png
excerpt: I have been selected as one of 75 PhD students nationwide to receive the Department of Energy Office of Science Graduate Student Research (SCGSR) Award. I will be conducting research at the National Lab of the Rockies (NLR) with my collaborating scientist Dr. Shuva Paul.
---

<div style="display: flex; align-items: center; justify-content: center; gap: 40px; margin-bottom: 30px;">
  <img src="/images/NLR/DOE_logo.png" alt="Department of Energy" style="max-height: 100px;">
  <img src="/images/NLR/NLR_logo.png" alt="National Lab of the Rockies" style="max-height: 100px;">
</div>

I am thrilled to share that I have been selected for the **Department of Energy (DOE) Office of Science Graduate Student Research (SCGSR) Award**! I am one of 75 PhD students selected from 55 universities across 27 states for this prestigious fellowship. The full announcement can be found [here](https://www.energy.gov/science/articles/outstanding-us-graduate-students-selected-department-energy-office-science).

The SCGSR program prepares doctoral candidates for careers critical to the DOE Office of Science's mission by providing hands-on training and access to world-class National Laboratory facilities. I will be conducting my thesis research at the **National Lab of the Rockies (NLR)**, working alongside my collaborating scientist, **Dr. Shuva Paul**.

## The Research: AEGIS

My proposed research introduces **AEGIS** (**A**I **E**xamination and **G**uarding through **I**mplementation **S**crutinization), an automated pipeline for the analysis and live behavioral monitoring of black-box AI systems deployed in mission-critical energy infrastructure.

NLR increasingly leverages AI for applications vital to national energy security, from real-time grid stability prediction to sensor data analysis. This reliance, however, introduces significant security risks: adversarial inputs, backdoors, code-based attacks, prompt injections, and large-scale data poisoning can cause AI systems to silently misbehave, with potentially catastrophic consequences for the power grid and public safety.

AEGIS addresses this threat through three interconnected tasks:

**Task I — Model Recovery:** Starting from CPU/GPU memory snapshots of a deployed black-box AI system, AEGIS recovers a model's weights, topology, and inference code to produce an instrumentable white-box instance. This builds directly on my prior published work ([AiP, USENIX Security '24](https://www.usenix.org/conference/usenixsecurity24/presentation/oygenblik) and [ZEN, NDSS '26](https://www.ndss-symposium.org/ndss-paper/achieving-zen-combining-mathematical-and-programmatic-deep-learning-model-representations-for-attribution-and-reuse/)), which demonstrated recovery across diverse model families, from YOLOv5 variants to Llama 2.

**Task II — Security Evaluation:** Using the recovered white-box model, AEGIS generates code-level Control and Data Flow Graphs (CDFGs) to establish behavioral signatures of normal inference. It then identifies weights and execution paths that are sensitive to small input perturbations (capable of causing model misclassifications when changed) detecting weight-based backdoors, architectural backdoors, and novel hybridized attacks. This profiling produces boundary constraints used in Task III.

**Task III — Continuous Monitoring:** AEGIS instruments the model's inference code with the constraints derived in Task II, enabling real-time anomaly detection during deployment. An LLM agent interfaces with human operators, summarizing anomalous layer activations and unexpected execution path changes, and generating actionable health reports.

## Application to NLR

NLR's centers — including the Energy Security, Resilience and Integration (ESRI) group and the Cybersecurity Research Center (CRC) — are already working to understand and mitigate AI security threats within critical infrastructure. AEGIS is designed to directly complement these efforts.

Consider an AI system at NLR analyzing real-time sensor data to predict grid instability. If an adversary has implanted a backdoor into the model's code or training data, it could recommend control actions that exacerbate instability under adversary-specified trigger conditions, leading to cascading grid failures. AEGIS enables NLR scientists and engineers to continuously monitor such systems at runtime — catching these attacks before they cause real-world harm.

The 12-month research plan kicks off in June 2026, beginning with applying my AI model recovery and attribution techniques to NLR-relevant models, followed by security evaluation and live monitoring in NLR's simulated environments, and culminating in application to real NLR systems and demos for NLR engineers.

I am incredibly grateful to the DOE for this opportunity, to my advisor Professor Brendan Saltaformaggio and the [CyFI Lab](https://cyfi.ece.gatech.edu/) for their continued support, and to Dr. Shuva Paul at NLR for agreeing to collaborate on this work. I look forward to what this year will bring!
