# Reuse/Release Equivalence Principle

> The granule of reuse is the granule of release.

## Principle

Classes and modules that are grouped into a component should be *releasable* together.

The fact that they share the same version number and the same release tracking, and are included under the same release documentation, should make sense both to the author and to the users.

## Background

People who want to reuse software components cannot, and will not, do so unless those components are tracked through a release process and are given release numbers.

This is not simply because, without release numbers, there would be no way to ensure that all the reused components are compatible with each other. Rather, it also reflects the fact that software developers need to know when new releases are coming, and which changes those new releases will bring.

Therefore the release process must produce the appropriate notificatiosn and release documentation so that users can make informed decisions about when and whether to integrate the new release.