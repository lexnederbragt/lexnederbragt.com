# My personal website

Repository for my personal website [lexnederbragt.com](https://lexnederbragt.com).

Based on the rroxford.github.io website


### Render and view the site

```
mkdir -p vendor

docker run --platform=linux/amd64 \
  -v "$PWD":/srv/jekyll \
  -v "$PWD/_site":/srv/jekyll/_site \
  -w /srv/jekyll \
  jekyll/builder:3.8 \
  bash -c "bundle install --path vendor/bundle && JEKYLL_ENV=production bundle exec jekyll build --future"
```

Add ` --watch` to render changes after each save.

# view the site
cd _site && python3 -m http.server 4000
# view at http://localhost:4000

