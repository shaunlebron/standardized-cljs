# Dependency Retriever

If cljs.edn is to allow `:dependencies` and `:dev-dependencies` vectors, it
might make sense to have some build-tool agnostic way to retrieve them.
[Planck] and the [CLJS Quick Start] already rely on either of the following
commands for downloading dependencies and resolving their classpath:

```
$ lein classpath
$ boot show -c
```

Both tools use a Clojure library [Pomegranate], which wraps the Java library
[Aether], the standard interface to Maven repositories.  Knowing this, we
implement a minimal implementation of the commands above with a small library.

[Planck]:http://planck-repl.org/dependencies.html
[CLJS Quick Start]:https://github.com/clojure/clojurescript/wiki/Quick-Start#dependencies
[Pomegranate]:https://github.com/cemerick/pomegranate/
[Aether]:http://www.eclipse.org/aether/

## Building and Using

```
lein uberjar
```

```
$ ./cljs-install --help

Retrieve dependencies listed in a given .edn file (defaults to cljs.edn).

Options:
  -c, --classpath-file FILE  .classpath  Write colon-delimited classpath to file
  -p, --production                       Install only :dependencies
  -d, --dev                              Install only :dev-dependencies
  -h, --help
```