---
layout: post
title: "Moving Over to Octopress"
date: 2015-12-26 20:00:07 +0530
comments: true
categories: 
---

Hi, so I know there are a lot of resources which detail how to move your blog
over to octopress. I just did the same thing today. Since, I faced some
difficulties while doing this, I think this might be a good topic to start my
blog off with. So let’s get started with creating your blog.

## Installing Octopress

To install Octopress on your system, you need Git and Ruby installed on your
machine. Both these packages can be installed using various package managers
such as yum and apt-get. Now clone the Octopress repository from Github. Run
the following commands:

```
git clone git://github.com/imathis/octopress.git octopress
cd octopress
gem install bundler #package manager for ruby
bundle install   # installs all the dependencies for Octopress
rake install     # installs octopress
```

Some points about the above commands:

* If you get an error Net::HTTPServerException with some other messages, open the
Gemfile and replace https://rubygems.org with http://rubygems.org. This should
resolve that issue
* Don’t be root when doing bundle install. This will prohibit any other user from
using Octopress.

## Basic setup details

All the configuration information for your blog is stored in `_config.yml` file.
Here you can define the name of your blog, the url, the author, link github id
and gmail ids etc. Browse through the file once.

To create a new page (eg: About me) run

```
rake new_page[About]
```

This creates a new directory `About` inside the `source` directory. This directory
has a file named `index.markdown`. Use it to add content to your file.

```
To create your first blog post
```

To generate and preview the blog

```
rake generate
rake preview
```

Head over to `http://localhost:4000` to see your first blog!

## Deploying the blog to Github

First of all, create a repository of the form `[username].github.io` from your
Github account, where username is your Github username. For example, my github
user name is *SudShekhar*, so my github.io repository is named
`sudshekhar.github.io`.

Now inside the octopress folder (which we had cloned from remote), type

```
rake setup_github_pages
```

This will ask for the link of your github repository url
(git@github.com:SudShekhar/sudshekhar.github.io.git in my case). Just press
enter and voila! the entire setup is done. To push your code live, run the
following commands

```
rake generate
rake deploy
```
A short note about these two commands: `setup_github_pages` pushes the`_deploy`
folder to remote. The `source` folder is not pushed to remote and you need to add
it explicitly before such a step can be taken. By default, your Octopress
repository (local version) remains in `source` branch. Thus, only the *_deploy*
will be pushed to remote.

Please let me know if you face any other issues. I will be glad to help :)
