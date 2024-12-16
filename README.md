# gen

[![bb compatible](https://raw.githubusercontent.com/babashka/babashka/master/logo/badge.svg)](https://babashka.org)
[![Clojars Project](https://img.shields.io/clojars/v/baby.pat/gen.svg)](https://clojars.org/baby.pat/gen)   
Simple macro for easy context-sensitive clojure.spec generators

___
[<img src="resources/twins.png" alt="fw" width="200px">](https://gen.pat.baby)
A thin layer around [the Genman library](https://github.com/athos/genman) by notable Japanese Clojurian [Athos]. It's just a wrapper around a wrapper around spec to make fun generators that are simple to read and reason about.

## Installation

```clojure
baby.pat/gen {:mvn/version "0.0.2"}
```
## Usage

```clojure
(require '[clojure.spec.alpha :as s])
(require '[baby.pat.gen :as g])
(s/def ::love integer?)
(g/def ::love :home #(and (< % 10000) (< % 50) (pos-int? %)))
(g/def ::love :away #(and (< % 10000) (> % 50)))
(g/gen ::love :home)
(g/sample ::love :away 20)
```
## Usage Notes
The `g/def` macro already includes the spec id as an `and` argument to help generators work without too much fiddling. I errored on the side of fiddling by the user in place of getting clever, so if at first you cannot generate, get more specific as you would with a `clojure.spec/and` normal generators.
