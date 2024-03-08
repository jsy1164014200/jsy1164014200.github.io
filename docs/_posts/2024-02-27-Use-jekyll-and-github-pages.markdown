---
layout: single
title:  "Use Jekyll and Github Pages to build the website"
date:   2024-02-27 13:26:36 +0800
categories: Miscellaneous
---
In this article, you will learn how to build your own website by utilizing the Github Pages and Jekyll. 

# 1. Preliminary 

Before continuing, you should google the following concepts and have a breif understanding:
- github pages
- ruby, gem
- bundler, Gemfile
- jekyll

Then, you can locally build a static website by following the step by step tutorial in [Jekyll website][jek-sbys]. 
The next step is reading the [document of github pages][doc-github-pages]. This way, you can deploy the static website on Github Pages. 

# 2. Use Theme

You may choose one theme from the [Jekyll Theme][jek-the] and read the document of the corresponding theme. I will take the Minimal Mistakes theme as a example. 

First step: 
{% highlight ruby %}
jekyll init . 
{% endhighlight %}
This way, you init the project by the default theme of jekyll.

Second step: 
Change some configures in Gemfile. 
{% highlight ruby %}
gem "github-pages", group: :jekyll_plugins
gem "minimal-mistakes-jekyll"
{% endhighlight %}

Third step:
Revise the _config.yml. Just copy [this file][config-file] into _config.yml. 

Fourth step:
Fix some bugs.
{% highlight ruby %}
Bundle add webrick
{% endhighlight %} 
If you see some warnings about the Token Api, see this [link][token].

Last step: 
Test the website locally.
{% highlight ruby %}
Bundle exec Jekyll serve —livereload
{% endhighlight %} 

> Remeber to set `JEKYLL_ENV=production` to force the environment to production.



<!-- Note: Jekyll 3.3 overrides this value with url: http://localhost:4000 when running jekyll serve locally in development. If you want to avoid this behavior set JEKYLL_ENV=production to force the environment to production.

Note: Comments are disabled by default in development. To enable when testing/building locally be sure to set JEKYLL_ENV=production to force the environment to production. -->


[jek-sbys]: https://jekyllrb.com/docs/step-by-step/01-setup/
[doc-github-pages]: https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll
[jek-the]: https://jekyllrb.com/docs/themes/
[config-file]: https://github.com/mmistakes/minimal-mistakes/blob/master/_config.yml
[token]: https://idratherbewriting.com/documentation-theme-jekyll/mydoc_install_jekyll_on_mac.html#githuberror