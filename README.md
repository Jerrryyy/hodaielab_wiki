## Local development

For local development, it is useful to be able to visualize the website w/o having to push or commit.
The following instructions describe the setup of the Jekyll server and the launch command.

Alternatively, there is a nice overview of gh-pages and jekyll [here](https://www.aleksandrhovhannisyan.com/blog/getting-started-with-jekyll-and-github-pages).

### Setup Jekyll

```
# 1. setup 'Ruby Version Management' tool
sudo apt-get install gnupg2
curl -sSL https://rvm.io/mpapis.asc | gpg --import -
curl -sSL https://rvm.io/pkuczynski.asc | gpg --import -
curl -sSL https://get.rvm.io | bash -s stable

source ~/.bashrc  # to make the installation of 'rvm' available in the current session

# 2. install ruby 3.0.0
rvm install 3.0.0
rvm --default use 3.0.0

# 3. install gems locally for the user
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# 4. setup the ruby environment for gh-pages
gem install bundler

cd <path_to_lab_wiki_root>
bundle init
bundle add jekyll --version "~> 3.9.2"
bundle add webrick
echo "" >> Gemfile
echo "gem 'github-pages', group: :jekyll_plugins" >> Gemfile

bundle install
```

### Serve gh-pages website with Jekyll

```
# launch the Jekyll website locally
bundle exec jekyll serve
```
