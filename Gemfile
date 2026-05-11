source "https://rubygems.org"

# Use the github-pages gem to match GitHub Pages' Jekyll environment exactly.
# Run `bundle update github-pages` periodically to stay in sync.
gem "github-pages", group: :jekyll_plugins

# Plugins (these are also whitelisted by GitHub Pages)
group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-sitemap"
  gem "jekyll-seo-tag"
end

# Windows / JRuby tzdata
gem "tzinfo-data", platforms: [:mingw, :mswin, :x64_mingw, :jruby]

# Performance booster for watching directories on Windows
gem "wdm", "~> 0.1.1", platforms: [:mingw, :mswin, :x64_mingw]

# Ruby 3.x no longer ships with webrick, but Jekyll's built-in server uses it
gem "webrick"
