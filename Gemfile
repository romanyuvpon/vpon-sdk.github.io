#
source "https://rubygems.org"
gem "jekyll", "~> 3.0.3"
#gem 'pygments.rb'
#gem "kramdown", "~> 1.3.0"


# github page
require 'json'
require 'open-uri'
versions = JSON.parse(open('https://pages.github.com/versions.json').read)
#gem 'github-pages', versions['github-pages']
gem 'github-pages', "~>72"

group :jekyll_plugins do
    gem 'jekyll-commonmark-ghpages'
  end