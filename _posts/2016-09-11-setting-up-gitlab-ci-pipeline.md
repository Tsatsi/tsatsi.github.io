---
layout: post
title:  "Setting up Gitlab-CI pipeline"
date:   2016-09-11 03:27:23 +0200
categories: devops update
hero: "assets/img/gitlab.png"
overlay: orange
---
So I recently had to set setup up a gitlab CI pipeline for a small React JS project I’m currently working on.
In this post I will go over the steps I took in setting it up .
{: .lead}
<!–-break-–>

## Install Gitlab
The first thing to do is to setup gitlab. I installed git lab using digital ocean’s [one click][one-click] install and deploy.
 It is fairly straight forward and only requires following the setup wizard steps. 
 Another alternative is to use an instance hosted on [gitlab.com][gitlab] which has free options.


## Create Repo
Once gitlab was  up and running I created a React JS repo using [Create React App][create-react-app]. Create React App 
is a tool that let’s you start building your React JS app fast without having to worry much about the configurations.

To start using it, we first need to install it globally:

{% highlight ruby %}

npm install -g create-react-app

{% endhighlight %}


When we are done installing create-react-app, we can create our new app by running :

{% highlight ruby %}

create-react-app new-app

{% endhighlight %}


We can then run our project in development mode by running the following commands inside the project folder:
{% highlight ruby %}
npm start
{% endhighlight %}
To verify that all is fine, our project should be accessible on http://localhost:3000

## Create CI pipeline
The first step in creating a gitlab Continuous Integration pipeline is to add .gitlab-ci.yml file and save it in the root of the project directory.

The .gitlab-ci.yml file defines what the CI does with the project. In the example gitlab-ci.yml file below we have one job which is testing.
{% highlight ruby %}

before_script:
  - 'which ssh-agent || ( apt-get update -y && apt-get install openssh-client -y )'
  - eval $(ssh-agent -s)
  - ssh-add <(echo "$SSH_PRIVATE_KEY")
  - mkdir -p ~/.ssh
  - '[[ -f /.dockerenv ]] && echo -e "Host *\n\tStrictHostKeyChecking no\n\n" > ~/.ssh/config'

testing:
  stage: test
  script:
    - npm install
    - npm test
    - npm run build
    - scp  -r build/*  root@example:/var/www/new-app
  cache:
    paths:
    - node_modules/

{% endhighlight %}

The second step is to create a runner. A gitlab runner executes the commands defined in the .gitlab-ci.yml file. 
It could be a docker container, a virtual machine, or a bare metal machine. 
If the runner is successfully setup it should be visible on the runners page.

[one-click]: https://www.digitalocean.com/products/one-click-apps/gitlab/
[gitlab]: https://about.gitlab.com
[create-react-app]:  https://github.com/facebookincubator/create-react-app