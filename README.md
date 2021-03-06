[![GitHub release](https://img.shields.io/github/release/sismics/play-evolve.svg?style=flat-square)](https://github.com/sismics/play-evolve/releases/latest)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

# play-evolve plugin

This plugin provides a way to track and organize your database schema evolutions in Play! Framework 1 applications.

# Features

Same features as the evolutions Play plugin, with the following modifications:

* Always run automatically the evolutions, even in Production mode (fits better with Devops style)
* Can filter evolutions based on the driver: prefix the SQL line with !H2!, !MYSQL!, !POSTGRESQL!...

# How to use

#### Add the dependency to your `dependencies.yml` file

```
require:
    - evolve -> evolve 1.1.0

repositories:
    - sismicsNexusRaw:
        type: http
        artifact: "https://nexus.sismics.com/repository/sismics/[module]-[revision].zip"
        contains:
            - evolve -> *

```
#### Run the `play deps` command
#### Add the evolution scripts to the `db/evolutions` directory

### Tweaking SQL statements
Add to your `application.conf`:
```
# Evolve plugin
# ~~~~~
evolve.onExecuteStatement=play.plugins.evolve.OnExecuteStatement
````

Create a class `OnExecuteStatement` that implements `Function<String,String>` to transform single SQL statements:
```
public class OnExecuteStatement implements Function<String, String> {
    @Override
    public String apply(String sql) {
        if (Db.isDriverPostgresql()) {
            sql = sql.replaceAll("VARCHAR\\(36\\)", "UUID");
        }
        return sql;
    }
}
```
# License

This software is released under the terms of the Apache License, Version 2.0. See `LICENSE` for more
information or see <https://opensource.org/licenses/Apache-2.0>.
