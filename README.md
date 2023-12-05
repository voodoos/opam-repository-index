# opam-repository

This repository is a package repository for the [opam package
manager](https://opam.ocaml.org).

It contains a development version of the tools required to provide project-wide
occurrences to ocaml developers. These tools include: the compiler, dune, a new
indexing binary and updated merlin / ocaml-lsp servers.

# What the feature does...

✅ Every usages of types, values, constructors and labels in *ml files* in the entire workspace

✅ Usages of modules (like `M` in `include M`) in *ml* files

✅ Can be called on any such usage or on the *definition* itself

# ...what is does not cover yet:

❌ Usages of types and modules in *mli* files

❌ *Declarations* related to definitions in both *ml* and *mli* files.

❌ Occurrences of modules appearing in paths: like `M` and `N` in `M.N.P`

# How-to

## 1. Install the switch and tools

```sh
# Add the repository:
opam repo add index https://github.com/voodoos/opam-repository-index.git

# Create a (local or global) switch with that repository:
opam switch create --repositories=default,index . 4.14.2+index

# Install all tools with the virtual package:
opam install indexing-tools
```

## 2. Generate the index for your project

To index your project you need to build the `@ocaml-index` target in addition to
your project's targets. Running dune in watch mode is recommended to always keep
the index up-to-date. For example:

```
dune build @ocaml-index @install --watch
```

When the index is built and up-to-date `references` queries should return value
usages in all the project's sources.

## 3. Query

In vscode, or another editor using lsp, place the cursor on a definition or usage of a type, value, constructor or label and trigger the `find all references` commands.

https://github.com/voodoos/opam-repository-index/assets/5031221/c715f180-d3f7-4e09-b29b-e43872465511


# Current limitations

- Project using PPXes might show unexpected behavior, please open an issue if this happens!
- Declarations are not considered. Only the definition and usages of a type,
  value or module can be used as a starting point to perform a query. The result
  of the query will show all the usages along with its definition but not the
  declarations associated with that definition.
- We only provide Dune rules to orchestrate the index generation. However the
  indexing tool itself is agnostic and can be used by other build systems.

# Reporting issues
Please report any issue you encounter with the feature in [this
repository](https://github.com/voodoos/opam-repository-index). Dune projects can
have very complex rules  and indexing might fail in some corner cases. Please
report any such case you might encounter so that we can fix them.
