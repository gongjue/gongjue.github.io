source "https://rubygems.org"

# GitHub Pages compatibility (includes Jekyll 3.9.5)
gem "github-pages", "~> 231", group: :jekyll_plugins

# GitHub Pages supported plugins (automatically included)
# jekyll-feed, jekyll-sitemap, jekyll-seo-tag are included with github-pages gem

# Development tools
group :development do
  gem "webrick", "~> 1.8"
end

# Windows and JRuby compatibility
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]