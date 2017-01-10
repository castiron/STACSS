# STACSS
STACSS is a flexible CSS architecture built for projects with a high volume of both reusable and standalone components. At the same time, STACSS is bendy enough for small custom projects where you don't want to use an existing design framework, but still need some helpful mixins/patterns to get started.
This repo serves as a jumping off point for sites and applications that use this architecture, along with some helpful patterns and linting configuration.

## What is STACSS for?
If you want to build an Hypertext type web experiment and don't really want to build styles, or need a set of mostly designed UI tools/patterns to get your styles going, there are a [number](http://getskeleton.com/) of [helpful](http://getbootstrap.com/) [frameworks](http://ionicframework.com/) you can drop-in to start creating styled markup right away. STACSS is not this kind of thing.

Let's say that you have an ambitious design that you know is going to need that a componentized style framework, but with primarily custom styles and structure. STACSS might help you manage and maintain that build.
It's also great for making small sites where you want the backup of helpful mixins and patterns for things like cross-browser unstyled buttons and media-queries, but don't want to use or override a pre-designed framework.  

We built STACSS with two key development stages in mind: Building a project front-end with most (but maybe not all) of a design in hand, and coming back to a completed site to add new features. STACSS can also be a good
"Design in the browser" architecture because it allows you to build fast without worrying much about abstraction until you know which styles will be shared. It may seem technically simple at first, because it is! The difficulty is learning to
let STACSS be your guide to a more maintainable, team-friendly architecture.

## Such Features ###
The key tenant of STACSS is its architecture, which informs its name. Abstracted style presets (mixins) are primarily grouped into three files:
- Structure
- Typography
- Appearance

The goals of this organization are:
1. To provide a clear abstraction layer for shared style patterns that sits above components.
_Example:_ A component `.avatar-list` might use a grid layout that is defined in *Structure*, heading that uses styles from *Typography*, and a shared background-color/border-style mixin that is in *Appearance*. This makes it a very specific component, but with a clear pathway back to all of its shared properties.
2. To make it clearer how and which styles are shared: It is difficult enough to track down which classes are used across multiple pages and components. STACSS lets you draw explicit lines between components and the styles they share with other classes.
3. To help structure less global CSS. If there is a repeating style that is _really_ global, it goes in the above three files, otherwise it can live along side a smaller, partialed component without cluttering the global files.
 This can be particularly helpful in an app architecture like Rails or React, where you might have individual SCSS/CSS files within component folders, that only depend on some of the globally abstracted styles, and may have variables/mixins of their own.

### Many Buildings
STACSS encourages the use of making components (and component partial files) that are as specific as is needed. Go ahead and make a partial for that one list module: It probably has its own view in the app anyhow. If it's not clear what components will be reused at first, don't stress about it: The location of abstracted style-patterns is clear, and just granular enough that you can build away on singletons and then pull shared styles into a relevent partial when you see a repeating pattern.

### Stop Worrying about Order and Keep Everything in Order
Along with the greater structural goals above, STACSS has some suggestions about specificity and nested component classes that will help you avoid source-order conflics and, in some cases, stop worrying about order altogether. There's also this nifty z-index partial where you can keep track of the z-stacking of all components in one place: we think you'll like the sanity imparted by this idea.

### Production Tested Pattern Library
Included in this repo is a few base mixins and utility classes that have been used oh so many web times that it's just easier to start out with them there: Stuff like convenience mixins for media queries, unstyled lists, buttons, and the like. We include normalize!

### Forget Everything you Just Read
If you want. STACSS is pretty modular. Delete what you don't want and say goodbye forever. Urr, I mean fork it and tell us what you changed for the betterment of us all!


## How to STACSS
This readme gives an overview for the features that make STACSS magical and the seasoned frontendo may be able to take this and run with it, but 
the demo (forthcoming) provides a more thorough overview on how to build and customize components in this architecture. It is recommended that you [get Sassy](http://sass-lang.com/guide) in order to take advantage of what STACSS has to offer.

As mentioned above, global abstracted style presets (mixins) are primarily grouped into three files:
- Structure (Spacing, layout related styles)
- Typography (Font sizes, text decoration, letter-spacing, etc)
- Appearance (Colors, borders, shadows, texture!)

There are also optional files to store presets that won't change frequently:
- Variables (global use only)
- Fonts
- Icons
- Mixins (base, media, project, vendor)
- Libs (we put normalize in here, and external libraries would go in here too)

More information about how each file is used, and what is defined by "Structure, Typography, and Appearance" are available as comments in the files themselves. A thorough demo page is also on the way.

### Let's make a class now, please
Note that the files above are the only files within STACSS where import order matters, because for instance, mixins in 'Appearance' can use declarations that already exist in 'Typography' or 'Structure.'
Also note that none of these files contain actual CSS classes! Those go in the components folder, in as specific a partial as you can make.
For example, say there is a section heading that uses a few typography conventions that are used across the site, and also might contain an icon above it.  Here's the markup without any class names yet:
```
<header>
  <figure>
    <img src="section-logo.png" alt="Description of section logo" />
  </figure>
  <h3>I named this section myself!</h3>
  <p>It's got a tagline and everything</p>
</header>
```

### STACSS naming and scope
A single component partial can be made for this in `components>_section-header-primary.scss`
We like to start small component partials with a top level class name that is descriptive of the classes function, and use [SCSS nesting](http://sass-lang.com/guide) for pretty much everything inside of it. That way, a team of developers can use concise,
generic, readable class names within the component without fear of namespace conflict or source-order issues. Don't like nesting? Don't do it. STACSS doesn't care, it's just a suggestion to keep the global space worry-free, geez.  

Let's add those class names then!
```
<header class="section-header-primary">
  <figure class="icon">
    <img src="section-logo.png" alt="Description of section logo" />
  </figure>
  <h3 class="title">I named this section myself!</h3>
  <p class="subtitle">It's got a tagline and everything</p>
</header>
```

Why add `-primary`? In case there is more than one! In STACSS, it's often good to start as specific as possible, so that it's immediately obvious how to add a new "section-header" if needed.  
In this case, the SCSS would look like this:
```
  .section-header-primary {
    @include boxPrimary; // This might be a mixin in STACSS>_appearance.scss that has padding, background color, borders, shadow, etc.
    $iconWidth: 125px; // This variable can be as generic a name as you want, it's scoped to a class so it's all yours!
    text-align: center;
    
    icon {
      display: inline-block;
      padding-bottom: 18px;
      
      img {
        width: 100%;
        max-width: $iconWidth;
      }
    }
    
    .title {
      @include headerSecondary; // This might be a mixin in STACSS>_typography.scss
      padding-bottom: 28px; // This might be an override of something in the mixin
    }
    
    .subtitle {
      @include copySecondary; // This might be a mixin in STACSS>_typography.scss
    }
  }
```

### Local Artisinal Small Batch Component
This component can take advantage of both local and global mixins/variables, the usage of which is clearly defined by STACSS architecture. `boxPrimary` and `headingSecondary` are global abstracted styles,
`$iconWidth` is local to this component only, and actually can't be used outside of this file unless it's also declared globally. Did you know you can define local mixins this way too? Objectacular! Can you still define a 
global mixin or variable in this partial? Sur - I mean DON'T!! Component partials should *only* contain styles for the component. If it turns out this style is used in multiple places, it should be abstracted as a mixin inside of the
higher level 'STACSS' folder.

Groups of components (Maybe something like Backend, Dashboard, or Footer styles) should be grouped! Not within a monolithic file, but inside an aptly named folder (with an _index.scss for easy importing).

It's also worth noting that in a Rails or React/Redux like app structure, SCSS component files might live in individual folders alongside controllers or views. Depending on how you compile these, they may not have access to global STACSS mixins, but
as long as these mixin partials *only* contain mixins and variables, they can be pulled in within the component SCSS via an @import without including any redundant styles on the front-end. In addition, this structure makes it a lot clearer to 
developers which global dependencies are required for individual components.

### What about utility classes and tiny shared components?
In a utopic front-end development situation, you might be able to get away with having only top-level classes with concise, semantic nested classes that include mixins that live in the global space. Probably though, some other 
developer is going to show up and be all "How do I get this standard button and/or header!!" and they just want to write some markup without making a SCSS partial. This is understandable. STACSS has a convention for that too:
Just put them in `structure`, `typography`, and `appearance`.
For instance, STACSS ships with a `screenReaderText()` mixin in `STACSS>_appearance.scss`. If you want to make a utility class for that, just put `.screen-reader-text` inside `STACSS>_appearance.scss`.
If your utility class deals with more than just structure, typography, or appearance, it probably isn't a utility class, and the STACSS convention is to make a reusable component for that. That's kind of the 
STACSS test right there.
*Note:* If you are using a Rails or React/Redux structure like the one noted above, you may not want to put classes inside any of the files inside `STACSS` because you have to include them many times in one app. 
If this is the case for you, you might want to make additional "Structure," "Typography," and "Appearance" partials inside components that only use utility classes.

Sometimes there might be a tiny component that shows up all over the place, like a button that uses some styles from typography, appearance, and maybe contains some of its own layout and/or icon sauce. Most of the time, you should still make a partial for this,
but if it's really tiny and used all over the place, it might make sense to throw into a partial like `components>_shared.scss` just so it's easy to find. Beware! A file such as this is in danger of the dreaded clutterblorp. Don't make STACSS sad by 
just putting a bunch of classes in a "shared" partial. Keeping partials with like components in folders will help with this.

Conveniently, you can always scope these utility classes inside of partials with top-level classes if you need to make tweaks to them in context. Remember: the order doesn't matter!

### Z-Stack*
There is one partial in the STACSS top level that's a little different. It's your global z-stack! This is a little speakeasy where you can talk about specific components and their global z-indeces (and nothing else) without
any other declarations to bother you. This file should look a little something like this:

```
.dropdown {
   z-index: 5;
}

.fixed-header {
  z-index: 10;
}

.modal-overlay {
  z-index: 20;
}
```

Note that in this example, all of the classes above should also be declared somewhere in `components` with the rest of their styles. This file is just to keep all your z-index parameters in one place, so as to avoid the slippery slope of
forgetting where all these components stack up (you *know* this happens).

*not an actual nick name for Cast Iron Tech-Chief Zach Davis


## Set up that stack
This repo has two top-level scss manifests, one that is helpful for websites with RTE/MCE in-browser editor components (rte.scss), and one that pulls in everything (styles.scss). STACSS doesn't have anything to say about how to pre-compile these
files except that you probably should.
There is no special setup required beyond pulling the stylesheets folder into your product and compiling it with your favorite build utility (or not, intrepid asset-pipeline-on-the-server type user!).

### Lint out of the Box
To lint the styles included in the repo, install [SCSS-Lint](https://github.com/brigade/scss-lint) with a little `gem install scss-lint` and run this in the project directory: 

`scss-lint stylesheets/ -c .scss-lint.yml`

We've bundled our current SCSS-Lint configuration in this repo to make it easy to share across projects. This repo should always pass the linter using the bundled config. We think these are some pretty good rules so far, but you probably shouldn't just throw them into your project without checking it over. SCSS-Lint has plugins/integrations for plenty of editors, so you can easily test different configs as you work.
