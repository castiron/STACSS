# STACSS
STACSS is a flexible CSS architecture built for projects with a high volume of both reusable and standalone components. At the same time, STACSS is bendy enough for small custom projects where you don't want to use an existing design framework, but still need some helpful mixins/patterns to get started.
This repo serves as a jumping off point for sites and applications that use this architecture, along with some helpful patterns and linting configuration.

## What is STACSS for?
If you want to build an Hypertext type web experiment and don't really want to build styles, or need a set of mostly designed UI tools/patterns to get your styles going, there are a [number](http://getskeleton.com/) of [helpful](http://getbootstrap.com/) [frameworks](http://ionicframework.com/) you can drop-in to start creating styled markup right away. STACSS is not this kind of thing.

Let's say that you have an ambitious design that you know is going to need that type of componentized framework, but with primarily custom styles and structure. SCSS might help you manage and maintain that process. It's also great for building small sites where you want the backup of helpful mixins and patterns for things like cross-browser unstyled buttons and media-queries, but don't want to use or override a pre-designed framework.

### Such Features ###
The key tenant of STACSS is its architecture, which informs its name. Abstracted style presets (and in some cases, entire classes) are grouped into three files:
- Structure
- Typography
- Appearance

In that order. The goal of this organization is twofold:    
1. To separate utility classes that are unrelated from a design perspective.    
_Example:_ `.container` goes in structure, and `.heading-primary` goes in typography).    
2. To provide a clear abstraction layer for shared style patterns that sits above components.    
_Example:_ `.avatar-list` might use a grid layout that is definted in *Structure*, heading classes from *Typography*, and a shared background-color/border-style mixin that is in *Appearance*. This makes it a very specific component, but with a clear pathway back to all of its shared properties.

More thorough examples and documentation will be added to the project wiki soon.

### Many Buildings
STACSS encourages the use of making components (and component partials) that are as specific as is needed. Go ahead and make a partial for that one list module: It probably has its own view in the app anyhow. If its not clear what components will be reused at first, don't stress about it: The location of abstracted style-patterns is clear, and just granular enough that you can build away on singletons and then pull shared styles into a relevent partial when you see a repeating pattern.

### Stop Worrying about Order and Keep Everything in Order
Along with the greater structural goals above, STACSS has some suggestions about specificity and nested component classes that will help you avoid source-order conflics and, in some cases, stop worrying about order altogether. There's also this nifty z-index partial where you can keep track of the z-stacking of all components in one place: we think you'll like the sanity imparted by this idea.

### Production Tested Pattern Library
Included in this repo is a few base mixins and utility classes that have been used oh so many web times that it's just easier to start out with them there: Stuff like convenience mixins for media queries, unstled lists, buttons, and the like. There's also a responsive grid system that we use a lot, and some instructions on how to customize it to your liking...

### Forget Everything you Just Read
If you want. STACSS is pretty modular. Delete what you don't want and say goodbye forever. Urr, I mean fork it and tell us what you changed for the betterment of us all!

## Set up that stack
This repo has two top-level scss manifests, one "rte" that is helpful for websites with RTE/MCE in-browser editor components, and one "styles" that pulls in everything.
There is no special setup requirecd beyond pulling the stylesheets folder into your product and compiling it with your favorite build utility (or not, intrepid asset-pipeline-on-the-server type user!).

## Lint out of the Box
To lint the styles included in the repo, install [SCSS-Lint](https://github.com/brigade/scss-lint) with a little `gem install scss-lint` and run this in the project directory: 

`scss-lint stylesheets/ -c .scss-lint.yml`

We've bundled our current SCSS-Lint configuration in this repo to make it easy to share across projects. This repo should always pass the linter using the bundled config. We think these are some pretty good rules so far, but you probably shouldn't just throw them into your project without checking it over. SCSS-Lint has plugins/integrations for plenty of editors, so you can easily test different configs as you work.
