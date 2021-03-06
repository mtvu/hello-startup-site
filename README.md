Hello, Startup Website
==================

This is the website and mobile app for [Hello, Startup: A Programmer's Guide to
Building Products, Technologies, and Teams](http://www.hello-startup.net), an
O'Reilly book by [Yevgeniy Brikman](http://www.ybrikman.com).

Status
==================

* The *Hello, Startup* website is available at http://www.hello-startup.net.
* Contributions, especially to the list of
  [Startup Resources](http://www.hello-startup.net/#resources), are welcome via
  pull request (see instructions below).
* The mobile app version is currently on pause as the market doesn't seem big
  enough for it.

Running the website
==================

1. Install [grunt.js](http://gruntjs.com/)
2. Install [jekyll](http://jekyllrb.com/)
3. `npm start`
4. http://localhost:4000

The `grunt` command runs `grunt watch`, which will watch for changes in the
background and recompile everything as necessary. Jekyll is a bit slow, so it
can take ~5 seconds for your changes to be visible.

Running with Docker
==================

As an alternative to installing Ruby, Jekyll, and Grunt, if you're a user of
[Docker](https://www.docker.com/) and [Docker
Compose](https://docs.docker.com/compose/), you can run a Docker image of
hello-startup-site that has all the dependencies already setup for you.

On Linux:

1. `git clone` this repo
2. `docker-compose up`
3. Go to `http://localhost:4000` to test

On OS X, using the [docker-osx-dev](https://github.com/brikis98/docker-osx-dev)
project:

1. `git clone` this repo
2. `docker-osx-dev`
3. `docker-compose up`
4. Go to `http://dockerhost:4000` to test

Architecture
==================

* [jekyll](http://jekyllrb.com/): used to assemble static HTML from the HTML
  fragments in `_layouts`, `_includes`, `_resources`, and `_data`.
* [grunt.js](http://gruntjs.com/): used to concatenate and minify CSS and
  JavaScript.
* [PhoneGap](http://phonegap.com/): used to package up the static HTML as
  iOS and Android apps.
* [GitHub Pages](https://pages.github.com/): for hosting the website.
* [Bootstrap](http://getbootstrap.com/): for CSS, layout, general theme.
* [Font Awesome](http://fortawesome.github.io/Font-Awesome/): for icons.

The Startup Resources
==================

The [Startup Resources](http://www.hello-startup.net/#resources) are generated
from [YAML](http://www.yaml.org/) data files in the `_data` folder (see the
[Jekyll Data Files](http://jekyllrb.com/docs/datafiles/) documentation for
more info). These resources are a work in progress and I welcome contributions
via [pull request](https://help.github.com/articles/using-pull-requests/).

Each YAML file contains the information for one type of resource. For example,
`deployment.yml` contains all the resources related to deploying code.

The basic format is:

```yaml
name: "Name for this resource"
description: "Brief description of this resource."
icon: "The name of one of the Font Awesome icons to represent this resource."
type: "one of: products, technologies, or teams"
categories:
  - id: "a-unique-id-for-this-category"
    name: "Human readable name for the category"
    sites: # List of websites for this category
      - name: "Website #1"
        url: "https://www.website-number-one.com/"
        image: "screenshot1.jpg" # 800x400 screenshot under images/resources
        description: "A brief description of website #1"
      - name: "Website #2"
        url: "https://www.website-number-two.com/"
        image: "screenshot2.jpg" # 800x400 screenshot under images/resources
        description: "A brief description of website #2"
```

See the `_data` folder for lots of examples.

Running the mobile app
==================

*Note: mobile app development has been put on pause and may not work any more*

1. Install [PhoneGap](http://phonegap.com/)
2. Install the [PhoneGap Developer App](http://app.phonegap.com/) on your
   computer and the mobile app for your phone.
3. Run `grunt` as explained in the "Running the website" instructions. This will
   assemble all of the HTML.
4. Add a new project to the PhoneGap Developer App by adding the `mobile`
   folder (which has `config.xml`).
5. At the bottom of the PhoneGap Developer App, it should tell you that the
   project is running and the URL. Connect to this URL in the PhoneGap mobile
   app on your phone.
6. If you want to build the app for real, use
   [PhoneGap Build](https://build.phonegap.com).

Making PhoneGap and Jekyll work together
==================

Both PhoneGap and Jekyll require a specific folder structure, and those are not
mutually compatible. To make this all work using the same content in the same
repo, I've used a bit of a hack with symlinks:

1. PhoneGap's `config.xml` and `index.html` are in the `mobile` folder.
2. Everything else is in the normal Jekyll locations (e.g. `_includes`, `_layouts`,
   `javascripts`, `stylesheets`). All of these files get compiled into the normal
   Jekyll output folder (`_site`).
3. I've added symlinks from the `mobile/www` folder to `_site`. Therefore, if
   you point PhoneGap at the `mobile` folder, it will see the folder structure
   it expects.
4. Since `_site` is normally generated by the Jekyll build process, you don't
   usually check it in. However, I had to in this case, or the symlinks won't
   work, which causes an error when GitHub Pages tries to build the site.
   Therefore, I've checked in a few placeholder files that ensure the folders
   we symlink to exist.

