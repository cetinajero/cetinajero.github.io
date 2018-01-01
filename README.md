# cetinajero.github.io
My personal website

## Table of contents

  1. [Setup the source branch](#1-setup-the-source-branch)
  2. [Setup the master branch](#2-setup-the-master-branch)
  3. [Checkout the master branch in *_site* directory](#3-checkout-the-master-branch-in-_site-directory)
  4. [Disable jekyll build on github](#4-disable-jekyll-build-on-github)
  5. [Setup yarn](#5-Setup-yarn)
  6. [The deploy task](#6-the-deploy-task)
  7. [Conclusion](#7-conclusion)
  8. [License](#8-license)
  9. [Credits](#9-credits)

## Setup the source branch

Generate the website:
```bash
jekyll new cetinajero.github.io
```

Init git:
```bash
cd cetinajero.github.io
git init
git checkout --orphan source
git add .
git commit -m "Initial commit (jekyll new cetinajero.github.io)"
```

Push `source` to github:
```bash
git remote add origin git@github.com:cetinajero/cetinajero.github.io.git
git push -u origin source
```

## Setup the master branch

Create an orphan `master` branch:
```bash
git checkout --orphan master
git reset .
rm -r * .gitignore
echo 'Coming soon' > index.html
git add index.html
git commit -m "Initial commit (Coming soon)"
```

Push `master` to github:
```bash
git push -u origin master
```

## Checkout the master branch in *_site* directory

Let's work in `source` branch:
```bash
git checkout source
```

Checkout the `master` branch into `_site` directory:
```bash
git clone git@github.com:cetinajero/cetinajero.github.io.git -b master _site
```

Push the generated site on github:
```bash
bundle exec jekyll build
cd _site
git add .
git commit -m "First generation (bundle exec jekyll build)"
git push
```

## Disable jekyll build on github

To be sure that jekyll generation is not triggered on github, you must add an empty `.nojekyll` file:
```bash
cd ..
touch .nojekyll
```

Then edit the `_config.yml` file and set:
```
include:
  - .nojekyll
```

Commit the changes:
```bash
git add .
git commit -m "Added .nojekyll flag to avoid generation on _site"
git push
```

## Setup yarn

Init yarn:
```bash
yarn init
```

To exclude yarn files from jekyll build, edit the `_config.yml` file and adds:
```
exclude:
  - node_modules
  - package.json
```

Make git ignore yarn packages by adding that line to `.gitignore` file:
```
node_modules
```

Commit the changes:
```bash
git add .
git commit -m "Added package.json to support node.js dependencies"
git push
```

## The deploy task

Create a `Rakefile` file:
- You can use this [Rakefile](/Rakefile)

Exclude `Rakefile` from jekyll build, by editing the `_config.yml` file and adding:
```
exclude:
- Rakefile
```

Commit the changes:
```
git add .
git commit -m "Added rake tasks and excluded Rakefile on _config.yml"
git push
```

## Conclusion

With that setup, you only have two commands to run:

- `rake serve` while developing, with live reload support
- `rake deploy` to deploy the site in production

## License

Copyright (c) 2018

Licensed under the [MIT License](/LICENSE)

## Credits

Thanks to [aymerick](http://www.aymerick.com) for his awesome [blog post](http://www.aymerick.com/2014/07/22/jekyll-github-pages-bower-bootstrap.html)!
