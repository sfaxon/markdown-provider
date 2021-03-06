# Markdown Provider

[![Language](https://img.shields.io/badge/Swift-3.1-brightgreen.svg)](http://swift.org)
[![Build Status](https://travis-ci.org/vapor-community/markdown-provider.svg?branch=master)](https://travis-ci.org/vapor-community/markdown-provider)
[![codecov](https://codecov.io/gh/vapor-community/markdown-provider/branch/master/graph/badge.svg)](https://codecov.io/gh/vapor-community/mmarkdown-provider)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/vapor-community/markdown-provider/master/LICENSE)

A Markdown renderer for Vapor and Leaf. This uses the [Vapor Markdown](https://github.com/vapor/markdown) package to wrap [cmark](https://github.com/jgm/cmark) (though a [fork](https://github.com/brokenhandsio/cmark-gfm) is used to make it work with Swift PM), so it understands [Common Mark](http://commonmark.org). A quick reference guide for Common Mark can be found [here](http://commonmark.org/help/). It also support [Github Flavored Markdown](https://guides.github.com/features/mastering-markdown/)

## Use

Once set up, you can use it in your Leaf template files like any other tag:

```swift
#markdown(myMarkdown)
```

Where you have passed `myMarkdown` into the view as something like:

```markdown
# Hey #

Check out my *awesome* markdown! It is easy to use in `tags`
```

## Setup

### Add as dependency

Add Markdown Provider as a dependency in your `Package.swift` file:

```swift
    dependencies: [
        ...,
        .Package(url: "https://github.com/vapor-community/markdown-provider.git", majorVersion: 1)
    ]
```

### Add the Provider

You can add a provider to you `Config`, which will do all of the setup for you and register your tag. Just add it as so:

```swift
let config = try Config()
try config.addProvider(MarkdownProvider.Provider.self)
let drop = try Droplet(config)
```


### Register with Leaf

Alternatively, you can also directly add the Tag onto your `LeafRenderer` if desired. During your setup (for example, in `main.swift`), register your tag as so:

```swift
if let leaf = drop.view as? LeafRenderer {
    leaf.stem.register(Markdown())
}
```

Don't forget to import MarkdownProvider in the file you register the tag or add the provider in with `import MarkdownProvider`
