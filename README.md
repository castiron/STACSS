# STACSS
STACSS is a flexible CSS architecture for projects with a high volume of reusable and independant components. At the same time, STACSS is bendy enough for small custom projects where you don't want to use an existing design framework, but still need some helpful mixins/patterns to get started.
This repo serves as a jumping off point for sites and applications that use this architecture, along with some helpful patterns and linting configuration.

## What is STACSS for?
If you want to build an Hypertext type web experiment and need a set of mostly designed UI tools/patterns to get your styles going, there are a [number](http://getskeleton.com/) of [helpful](http://getbootstrap.com/) [frameworks](http://ionicframework.com/) you can drop-in to start creating styled markup right away. STACSS is not this kind of thing.

Let's say that you have an ambitious design that you know is going to need that type of componentized framework, but with primarily custom styles and structure. SCSS might help you manage and maintain that process. It's also great for building small sites where you want the backup of helpful mixins and patterns for things like cross-browser unstyled buttons and media-queries, but don't want to use or override a pre-designed framework.

The key tenant of STACSS is its architecture, which informs its name. Abstracted style presets (and in some cases, entire classes) are grouped into three files:
- Structure
- Typography
- Appearance

In that order. The goal of this organization is to separate out style patterns that are unrelated from a design perspective, so that they can be combined in a blocky and maintainable way as a style (or in somecases) style framework is built.

Standard example to be provided soon, and more details will be built out in the project wiki.

## Set up that stack
This repo has two top-level scss manifests, one "rte" that is helpful for websites with RTE/MCE in-browser editor components, and one "styles" that pulls in everything.
There is no special setup requirecd beyond pulling the stylesheets folder into your product and compiling it with your favorite build utility (or not, intrepid asset-pipeline-on-the-server type user!).

## Lint out of the box
To lint the styles included in the repo, install [SCSS-Lint](https://github.com/brigade/scss-lint) with a little `gem install scss-lint` and run this in the project directory: 

`scss-lint stylesheets/ -c .scss-lint.yml`

We've bundled our current SCSS-Lint configuration in this repo to make it easy to share across projects. This repo should always pass the linter using the bundled config. We think these are some pretty good rules so far, but you probably shouldn't just throw them into your project without checking it over. SCSS-Lint has plugins/integrations for plenty of editors, so you can easily test different configs as you work.
