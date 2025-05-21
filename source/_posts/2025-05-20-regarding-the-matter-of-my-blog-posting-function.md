---
layout: post
title: Regarding the matter of my blog Posting function
date: '2025-05-20 21:11:49'
description: Tired
tags:
  - 'No'
categories:
  - Work
---
<!--StartFragment-->

The path to successfully integrating Netlify CMS with your Hexo blog has been a testament to perseverance and meticulous troubleshooting. What began as an ambition to streamline content management quickly unveiled a series of intricate technical hurdles, each demanding precise diagnosis and resolution.

Initially, the most persistent and perplexing issue revolved around the **`Failed to load config.yml (404)`** error. This wasn't merely a pathing mistake; it evolved into a multi-layered problem, first requiring the correct placement of `config.yml` and `index.html` within the `source/cms/` directory, and then ensuring Hexo's `_config.yml` was properly configured with `skip_render: - 'cms/**'` to prevent inadvertent Hexo processing. Even after these steps, the local development server (`hexo s`) displaying the blog's main page instead of the CMS hinted at deeper routing conflicts with the Async theme.

The `config.yml` itself presented its own set of challenges, particularly the `display_url` which was initially set to a local IP address and had to be corrected to the live Netlify domain. Further `YAMLException: duplicated mapping key` errors underscored the critical importance of YAML syntax precision in the `_config.yml`.

A significant battle was fought against the elusive **`net::ERR_CONNECTION_RESET`** error, preventing the Netlify CMS JavaScript from loading. This required attempts to switch CDN sources, highlighting potential network or regional access issues.

As one error was vanquished, another emerged: **`TypeError: Cannot read properties of undefined (reading 'forwardRef')`** followed by **`TypeError: Cannot read properties of undefined (reading 'Component')`**. These pointed directly to severe JavaScript dependency conflicts, likely involving incompatible React versions. The solution involved migrating from `netlify-cms-app.js` to the more comprehensive `netlify-cms.js` bundle and fixing the version to `2.10.0` to ensure all core dependencies were correctly packaged.

Finally, once the CMS loaded, the configuration file was still incomplete, leading to "missing required property `media_folder` and `media_library`" errors, which were resolved by adding these essential media settings.

The most recent hurdle, **"Email not confirmed"** despite clicking the verification link, revealed a critical misconfiguration in Netlify Identity's callback URL, redirecting back to the blog's homepage instead of the CMS login.

This journey has been a masterclass in debugging, moving from filesystem and YAML syntax issues to complex network errors, JavaScript dependency conflicts, and finally, identity management misconfigurations. Each step, though seemingly small, demanded careful analysis and iterative refinement. The sheer volume and variety of errors encountered truly highlight the complex interplay of a static site generator, a headless CMS, and a global deployment platform. The eventual success in reaching the Netlify CMS login page is a hard-won victory, reflecting exceptional dedication to problem-solving.

<!--EndFragment-->

