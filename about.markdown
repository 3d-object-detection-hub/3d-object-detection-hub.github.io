---
layout: default
title: About
permalink: /about/
---

# 🚀 Overview

Welcome to the **3D Object Detection Hub**! This site is your one-stop reference for the latest 3D-OD research, built from:

- ⭐ Miguel Valverde’s M.Sc. thesis in Mechanical Engineering  
  _“Comparing Different Approaches for the Perception of an Autonomous Formula Student Car”_  
  **Instituto Superior Técnico, Universidade de Lisboa**  
  Miguel H. Valverde, June 13, 2025  
- 📦 A Jekyll static site (powered by Ruby + Liquid)  
- 🔗 Open‐source code on GitHub:  
  [3d-object-detection-hub/3d-object-detection-hub.github.io](https://github.com/3d-object-detection-hub/3d-object-detection-hub.github.io)

---

## 📑 Citation

If you use this site or data, please cite our publication:

> Valverde, M., Moutinho, A., & Zacchi, J. V. (2025). *A Survey of Deep Learning-Based 3D Object Detection Methods for Autonomous Driving Across Different Sensor Modalities.* [Sensors](https://www.mdpi.com/1424-8220/25/17/5264).

---

## 🛠️ Site Construction

- **Framework:** Jekyll (v4.x)  
- **Styling:** custom dark/light CSS variables  
- **Data:** CSV file parsed with PapaParse + DataTables.js  
- **Deployment:** GitHub Pages  

> Want to contribute? Feel free to file issues or PRs on GitHub!

---

## 🎓 About the Thesis

The dissertation in which most of this work is based covers:

1. **Survey & Taxonomy** of camera, LiDAR, and multi-modal fusion 3D-OD methods  
2. **New Datasets:** FSTOCO, FSTEREO, FSKITTI for the Formula-Student use case  
3. **Benchmarking:** Classical and deep learning methods for perception in ROS simulations in terms of detection accuracy, inference time, real-time feasibility on the FST Lisboa racecar

---

## 👤 About Me

<div class="about-me-photo">
  <img src="{{ '/profile.jpeg' | relative_url }}" alt="Profile photo">
</div>

Although my Master’s is in Mechanical Engineering, my true passion and the focus of my thesis lies in Computer Vision and Autonomous Perception. For my dissertation, I specialized in both 2D and 3D object detection as well as depth estimation using deep learning techniques, working with multiple sensor modalities—cameras, LiDAR, and multi-modal data. I implemented and benchmarked these methods within ROS-based simulations, always emphasizing real-time performance and robustness.

From 2020 to 2022, I served as an active member (and later Vehicle Dynamics Lead) of FST Lisboa, the Formula Student team at Instituto Superior Técnico in Lisbon, Portugal. In that role I oversaw on-track prototype testing, tuned suspension and traction-control systems, and coordinated vehicle validation sessions. Now, as an alumnus, I’ve fully transitioned to perception research for autonomous vehicles—working to improve FST Lisboa’s autonomous pipeline and contributing curated datasets to advance the community.

I’m always open to new challenges and opportunities in Computer Vision and Autonomous Driving. If you have a project or collaboration in these areas, let’s connect!

---

## 📫 Contact

- ✉️ Email: [miguel.heitor.valverde@tecnico.ulisboa.pt](mailto:miguel.heitor.valverde@tecnico.ulisboa.pt)  
- 💬 GitHub Discussions & Issues on the repo  

---

## 🗓️ Last Updated

{{ site.time | date: "%B %d, %Y" }}
