# Use Case Experiments

Example use-case for experimenting with various formats for specifying architecture rules.

This assumes we want to allow two distinct rule sets: defining what projects may use which other projects, and a more granular set of rules based on package names specifying what classes should use other classes (things like a DB layer not being called directly from a web service, etc)

The system implicitly knows about projects (from the build system, etc). API layers must be defined by the user

## Scenario 1

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

## Scenario 2

Same as scenario 1, but now in addition each layer has a sub-set of files in an "impl" package which are internal - no other layer should be accessing them directly
