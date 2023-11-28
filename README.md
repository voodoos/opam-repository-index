# opam-repository

This repository is a package repository for the [opam package
manager](https://opam.ocaml.org).

It contains a development version of the tools required to provide project-wide occurrences to ocaml developers.
These tools include: the compiler, dune, a new indexing binary and updated merlin / ocaml-lsp.

```sh
# Add the repository:
opam repo add ocaml-index https://github.com/voodoos/opam-repository-index.git

# Create a (local or global) switch with that repository:
opam switch create --repositories=default,ocaml-index . 4.14.2+index

# Install all tools with the virtual package:
opam install indexing-tools
```


