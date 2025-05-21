---
layout: post
title: All things is done
date: '2025-05-21 11:15:29'
description: Happy
tags:
  - NuLL
categories:
  - Work
---
<!--StartFragment-->

We embarked on a journey to integrate a music player into a Hexo blog using the `hexo-theme-async` theme. The initial approach involved creating a custom EJS widget file (`music_player.ejs`) within `source/_data/async_widgets/` and configuring it in `_config.async.yml` under the `widgets` section.

The first hurdle encountered was a `ReferenceError: theme is not defined` within `music_player.ejs` when attempting to access `theme.music_player.url`. This indicated that the `theme` variable was not correctly passed to the custom widget template. Subsequent attempts to resolve this involved trying `config.music_player.url` and `site.data.async.music_player.url`, but these also failed.

Further investigation into the theme's structure revealed that existing widgets, like `about-card.ejs` within `node_modules/hexo-theme-async/layout/_widget/`, were successfully using `theme.about.title`. This suggested that the `theme` variable *should* be available.

Despite this, even hardcoding the music player's HTML and URL directly into `music_player.ejs` and even into a known working theme file like `about-card.ejs` in `node_modules` did not make the music player appear on the sidebar. This led to the conclusion that the issue might be deeper, possibly related to Hexo's caching, the theme's specific rendering pipeline, or environmental factors.

Concurrently, a separate issue arose: an "Error loading the CMS configuration" with the message `'collections[0].fields[6].required' should be boolean`. This error was traced to the `config.yml` file of the Netlify CMS, specifically within the `body` field of the "posts" collection. The problem was identified as an incorrectly formatted `default` value for the `body` field, where a JavaScript `<script>` tag was directly embedded, causing a YAML parsing error.

The solution for the CMS error involved removing the `<script>` tag from the `default` value in `config.yml` and instead integrating the comment system (initially considered Utterances.es) directly into the Hexo theme's EJS template for comments (`source/layout/_third-party/comment/index.ejs`).

However, the user then indicated a preference for **Giscus**, which the `hexo-theme-async` theme natively supports. This shifted the focus to correctly configuring Giscus within `_config.async.yml`. The key steps involved obtaining the `repo`, `repo-id`, `category`, and `category-id` from the Giscus app on GitHub. A specific error was identified where `reactions-enabled` was set to `"中文回答"` instead of a boolean or numeric value (`1` or `0`).

The current phase involves ensuring all Giscus parameters are correctly populated in `_config.async.yml` and then performing `hexo clean`, `hexo generate`, and `hexo s` to apply the changes locally. Finally, the user needs to commit these local changes using `git add .`, `git commit -m "..."`, and `git push origin master/main` to update the GitHub repository and potentially trigger a blog redeployment. The persistent music player issue remains unresolved, suggesting a deeper problem beyond standard configuration.

<!--EndFragment-->
