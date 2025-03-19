1. sbys: step by step in jekyll website.
2. docs: done by following github pages.
3. myblog: use Minimal Mistakes Jekyll theme



github建站攻略：
1. 安装 ruby，gem，bundle
2. 安装jekyll
3. jekyll init . 初始化项目，改Gemfile中github page，config中模版
4. Bundle add webrick
5. Bundle exec Jekyll serve —live reload 
6. 解决token问题 https://idratherbewriting.com/documentation-theme-jekyll/mydoc_install_jekyll_on_mac.html#githuberror

Note: Jekyll 3.3 overrides this value with url: http://localhost:4000 when running jekyll serve locally in development. If you want to avoid this behavior set JEKYLL_ENV=production to force the environment to production.

Note: Comments are disabled by default in development. To enable when testing/building locally be sure to set JEKYLL_ENV=production to force the environment to production.


