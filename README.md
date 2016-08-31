# play-evolve plugin

This plugin provides a way to track and organize your database schema evolutions in Play! Framework 1 applications.

# Features

Same features as the evolutions Play plugin, with the following modifications:

* Plays automatically the evolutions, even in Production mode
* Plays evolutions selectively based on the driver: prefix the SQL line with !H2!, !MYSQL!, !POSTGRESQL!...

# How to use

####  Add the dependency to your `dependencies.yml` file

```
require:
    - evolve -> evolve 0.1

repositories:
    - sismics:
        type:       http
        artifact:   "http://release.sismics.com/repo/play/[module]-[revision].zip"
        contains:
            - evolve -> *

```
####  Run the `play deps` command
####  Add the evolution scripts to the `db/evolutions` directory

# License

This software is released under the terms of the Apache License, Version 2.0. See `LICENSE` for more
information or see <https://opensource.org/licenses/Apache-2.0>.
