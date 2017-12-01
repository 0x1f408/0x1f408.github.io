source "https://rubygems.org"

# Hello! This is where you manage which Jekyll version is used to run.
# When you want to use a different version, change it below, save the
# file and run `bundle install`. Run Jekyll with `bundle exec`, like so:
#
#     bundle exec jekyll serve
#
# This will help ensure the proper Jekyll version is running.
# Happy Jekylling!

# Using this for GitHub Pages; to upgrade, run `bundle update github-pages`.
# Uncomment `gem 'jekyll'` & remove `gem 'github-pages'` for other uses
gem "github-pages", group: :jekyll_plugins
# gem 'jekyll', '3.5.2'

# If you have any plugins, put them here!
group :jekyll_plugins do

end

group :development do
  gem "jekyll-livereload"  # enable livereload in development
end

# Windows-specific:
if Gem.win_platform?
  # Windows does not include zoneinfo files, so bundle the tzinfo-data gem
  gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]

  # Avoid polling for changes (Windows)
  gem 'wdm', '>= 0.1.0'
end

