# Use Case Experiments

Example use-case for experimenting with various formats for specifying architecture rules.

This assumes we want to allow two distinct rule sets: defining what projects may use which other projects, and a more granular set of rules based on package names specifying what classes should use other classes (things like a DB layer not being called directly from a web service, etc)

A user has the following projects:

- product.core
- product.io
- product.db
- product.rest

They wish to specify that product.rest may use any project, product.io and product.db may use product.core, and product.core should not depend on any other projects. Each project's packages start with com.(project name)

In addition, within/across these projects, there are 3 layers: 
- persistence
- domain
- api

api should only use domain, and domain should only use persistence. These are structured within the projects by the name of the layer being within the package name for classes which are part of that layer.

## Scenario 1

The system does not know anything implicitly - projects must be fully defined by the user by providing antMatcher-style patterns to determine which classes are part of which projects, same for API layers

## Scenario 2

The system implicitly knows about projects (from the build system, etc). API layers must still be defined by the user
