---
layout: default
title: Implementations
nav_order: 3
has_children: false
---

<style>
  .zoom {
    transition: transform .2s;
    margin: auto;
  }
  .zoom:hover {
    transform: scale(1.2);
  }
  .slide-in {
    opacity: 0;
    animation-name: fade-in-top;
    animation-duration: 1s;
    animation-timing-function: ease;
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
  }
  @keyframes fade-in-top {
    0%{
      -webkit-transform: translateY(-50px);
      transform: translateY(-50px);
      opacity: 0;
    }
    100%{
      -webkit-transform: translateY(0);
      transform: translateY(0);
      opacity: 1;
    }
  }
</style>

# Implementations

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

Skiylia Implementations are listed below, grouped into language categories.

(Click on the images to visit that github repo)

### Python

<div style="display:flex; overflow: initial;">
  <a href="https://github.com/Skiylia-Lang/PySkiylia" style="width: 50%;" class="zoom slide-in">
    <img src="https://repository-images.githubusercontent.com/349156513/8620e100-9423-11eb-830a-858a39150e2c"/>
  </a>
  <div style="width: 40%">
    <p class="slide-in" style="animation-delay: .25s;">
      <a href="https://github.com/SK1Y101">
        <img src="https://img.shields.io/badge/Author-SK1Y101-lightgrey?style=for-the-badge"/>
      </a>
    </p>
    <p class="slide-in" style="animation-delay: .2s;">
      <img src="https://badges.pufler.dev/updated/Skiylia-Lang/PySkiylia?style=for-the-badge"/>
    </p>
    <p class="slide-in" style="animation-delay: .15s;">
      <img src="https://img.shields.io/github/v/release/Skiylia-Lang/PySkiylia?include_prereleases&style=for-the-badge"/>
    </p>
    <p class="slide-in" style="animation-delay: .1s;">
      <img src="https://img.shields.io/github/license/Skiylia-Lang/PySkiylia?style=for-the-badge"/>
    </p>
  </div>
</div>
