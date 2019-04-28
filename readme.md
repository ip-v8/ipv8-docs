# IPv8 documentation

[![Build Status](https://travis-ci.org/dsluijk/ipv8-docs.svg?branch=master)](https://travis-ci.org/dsluijk/ipv8-docs)

This repo tries to document the IPv8 application for reimplementation in other programming languages.

## Prerequisites

To to get started with this you have install mdbook:

```
cargo install mdbook
```

## Building

You can build the documentation with:

```
mdbook build
```

The output is now in the folder `./out`.

## Development

You can start the development server with:

```
mdbook watch
```

You can open the file `./out/index.html` in your browser to see the changes you have made.
