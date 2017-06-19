

# Lesson on automated IDE (PyCharm) and testing

Compiled by Jyry Suvilehto based on existing work by Radovan Bast and Nikolai
Denisov.

- [Website](https://coderefinery.github.io/IDEs/)
- [Credit and license](https://coderefinery.github.io/IDEs-testing/license/)

## Local development

The following Gemfile will permit you to run jekyll locally

        source 'https://rubygems.org'
        gem 'github-pages', group: :jekyll_plugins
        gem 'github-linguist'
        gem 'rouge', '~>1.11.1'

Write it as Gemfile under the repository root.

        $ export GEM_HOME=$HOME/.gem
        $ export PATH=$PATH:$HOME/.gem/bin
        $ bundler install
        $ bundle exec jekyll serve

