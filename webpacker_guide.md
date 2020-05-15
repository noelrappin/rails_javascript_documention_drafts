# Webpacker

This guide will show you how to install and use Webpacker to package JavaScript, CSS, and other assets for the client-side of your Rails application.

After reading this guide, you will know:

* What Webpacker does and why it is different from Sprockets.
* How to install Webpacker and integrate it with your framework of choice.
* How to use Webpacker for JavaScript assets.
* How to use Webpacker for CSS assets.
* How to use Webpacker for static assets.
* How to deploy a site that uses Webpacker.
* How to use Webpacker in alternate Rails contexts, such as engines or Docker containers.

## What Is Webpacker?

Webpacker is a Rails wrapper around the [webpack](https://webpack.js.org) build system that provides a standard webpack configuration and reasonable defaults.

### What is webpack?

The goal of webpack, or any front-end build system, is to allow you to write your front-end code in a way that is convenient for developers and then package that code in a way that is convenient for browsers. With webpack, you can manage JavaScript, CSS, and static assets like files or fonts. Webpack will allow you to write your code, reference other code in your application, transform you code, and combine your code into easily downloadable packs.

## How is Webpacker Different from Sprockets?

Rails also ships with Sprockets, an asset-packaging tool whose features overlap with Webpacker. Both tools will compile your JavaScript into into browser-friendly files, and minify and fingerprint them in production. Both tools allow you to incrementally change files in development.

Sprockets, which was designed to be used with Rails, is somewhat simpler to integrate. In particular, code can be added to Sprockets via a Ruby gem. However, webpack is better at integrating with more current JavaScript tools and NPM packages, and allows for a wider range of integration.

You should choose webpacker over Sprockets on a new project, if you want to use NPM packages, and if you want access to the most current JavaScript features and tools. You should choose Sprockets over Webpacker for legacy applications where migration might be costly, if you want to integrate using Gems, or if you have a very small amount of code to package.

If you are familiar with Sprockets, the following guide might give you some idea of how to translate. Please note that each tool has a slightly different structure, and the concepts don't directly map onto each other

|Task              | Sprockets         | Webpacker         |
|------------------|-------------------|-------------------|
|Attach JavaScript |javascript_link_tag|javascript_pack_tag|
|Attach CSS        |stylesheet_link_tag|stylesheet_pack_tag|
|Link to an image  |image_url          |image_pack_tag     |
|Link to an asset  |asset_url          |asset_pack_tag     |
|Require a script  |//= require        |require or include |

## Installing Webpacker

In order to use Webpacker you must be using the Yarn package manager, version 1.x or up, and you must have Node.js installed, version 10.13.0 and up.

Webpacker is installed by default in Rails 6.0 and up. In an older version, you can install it when a new project is created by adding `--webpack` to a `rails new` command. In an existing project, Webpacker can be added by installing `bundle exec rails webpacker:install`. This installation command creates local files:

* The Webpacker configuration at `config/webpacker.yml`
* Environment-specific webpack configuration files in `config/webpack/`
* Configuration files for Babel, PostCSS, and Browserslist
* A place for your front-end source at `app/javascript`

The installation also calls the `yarn` package manager, creates a `package.json` file with a basic set of packages listed, and uses Yarn to install these dependencies.

### Integrating Frameworks with Webpacker

Webpacker also contains support for many popular JavaScript frameworks and tools. Typically, these are installed either when the application is created with something like `rails new myapp --webpack=whatever` or with a separate command line task, like `rails:install:whatever`.

These integrations typically install the set of NPM packages needed to get started with the framework or tool, a "hello world" page to show that it works, and any other webpack loaders or transformations needed to compile the tool. The supported frameworks and tools are (use the tool name in all lowercase in the installation command):

* Angular (also installs TypeScript)
* CoffeeScript
* Elm
* ERB
* React
* Stimulus
* Svelte
* TypeScript
* Vue

## Using Webpacker for JavaScript

With Webpacker installed, by default any JavaScript file in the `app/javascripts/packs` directory will get compiled to its own pack file.

Given a file called `app/javascript/packs/application.js`, Webpacker will create a pack called `application`. You can render a script tag that references the url for this pack with the code `<%= javascript_pack_tag "application" %>` in a Rails view template, such as the application layout. With that in place, in development, Rails will re-compile the `application.js` file every time it changes and you load a page that uses that pack. Typically, the file in the actual `packs` directory will be a manifest that mostly loads other files, but it can also have arbitrary JavaScript code.

The default pack created for you by Webpacker will link to Rails default JavaScript packages if they have been included in the project:

```
require("@rails/ujs").start()
require("turbolinks").start()
require("@rails/activestorage").start()
require("channels")
```

You'll need to include a pack that requires these packages to use them in your Rails application.

### Where to Place Files

### Linking Files

### Babel and TypeScript

## Using Webpacker for CSS

## Using Webpacker for Static Assets

## Webpacker in Rails Engines

## Running Webpacker in Development

## Webpacker in Production

### Deploying Webpacker

### Webpacker and Docker

## Extending and Customizing Webpacker

## Troubleshooting Common Problems

## Upgrading Webpacker

## Credits

* [Webpacker Documentation](https://github.com/rails/webpacker)
* Noel Rappin
* Niklas Häusele
* [The React-Rails Sprockets or Webpacker Page](https://github.com/reactjs/react-rails/wiki/Choosing-Sprockets-or-Webpacker), edited by Greg Myers, was useful.
