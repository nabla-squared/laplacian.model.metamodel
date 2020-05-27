<!-- @head-content@ -->
# laplacian/metamodel

This model is a model for defining a model, i.e. a metamodel.
In this model, you can define a model with the following structure

- attribute
- relationship
- aggregation
- inheritance
- mixin


*Read this in other languages*: [[日本語](README_ja.md)] [[简体中文](README_zh.md)]
<!-- @head-content@ -->

<!-- @toc@ -->
## Table of contents
- [Overview](#overview)

  * [Model overview](#model-overview)

- [Usage](#usage)

- [Index](#index)

  * [Entity list](#entity-list)

  * [Script List](#script-list)

  * [Source code list](#source-code-list)



<!-- @toc@ -->

<!-- @main-content@ -->
## Overview


### Model overview


The following diagram explains the entities included in this module and the relationship
between them.
![](./doc/image/model-diagram.svg)

## Usage

To apply this Model module, add the following entry to your project definition.
```yaml
project:
  models:
  - group: laplacian
    name: metamodel
    version: 1.0.0
```

You can run the following command to see a list of resources affected by the application of this module and their contents.
```console
$ ./script/generate --dry-run

diff --color -r PROJECT_HOME/.NEXT/somewhere/something.md PROJECT_HOME/somewhere/something.md
1,26c1,10
< content: OLD CONTENT
---
> content: NEW CONTENT
```

If there is no problem, execute the following command to reflect the change.
```console
$ ./script/generate

```


## Index


### Entity list


- [**Entity**](<./doc/entities/Entity.md>)
エンティティ
- [**Property**](<./doc/entities/Property.md>)
property
- [**PropertyMapping**](<./doc/entities/PropertyMapping.md>)
property_mapping
- [**Query**](<./doc/entities/Query.md>)
The queries from which all navigation originates.
- [**Relationship**](<./doc/entities/Relationship.md>)
relationship
- [**ValueDomainType**](<./doc/entities/ValueDomainType.md>)
value_domain_type
- [**ValueDomain**](<./doc/entities/ValueDomain.md>)
value_domain
- [**ValueItem**](<./doc/entities/ValueItem.md>)
value_item
### Script List


- [./script/do-each-subproject.sh](<./scripts/do-each-subproject.sh>)

  Executes the command specified by the argument for each subproject.

  Example:
  ```console
  $ ./scripts/null -c git status
  ```

  > Usage: do-each-subproject.sh [OPTION]...
  >
  > -h, --help
  >
  >   Displays how to use this command.
  >   
  > -v, --verbose
  >
  >   Displays more detailed command execution information.
  >   
  > -c, --continue-on-error
  >
  >   Even if the given command fails in a subproject in the middle, executes it for the remaining subprojects.
  >   
- [./script/generate-all.sh](<./scripts/generate-all.sh>)

  Generates resources in the project, including subprojects.

  > Usage: generate-all.sh [OPTION]...
  >
  > -h, --help
  >
  >   Displays how to use this command.
  >   
  > -v, --verbose
  >
  >   Displays more detailed command execution information.
  >   
  > -c, --continue-on-error
  >
  >   Even if the given command fails in a subproject in the middle, executes it for the remaining subprojects.
  >   
- [./script/generate-metamodel-plugin.sh](<./scripts/generate-metamodel-plugin.sh>)

  Generates the [laplacian/metamodel-plugin](<null>) project as a subproject in the following directory.
  ```
  subprojects/laplacian.metamodel-plugin
  ```
  If the subproject already exists, the content of the subproject is updated.

  > Usage: generate-metamodel-plugin.sh [OPTION]...
  >
  > -h, --help
  >
  >   Displays how to use this command.
  >   
  > -v, --verbose
  >
  >   Displays more detailed command execution information.
  >   
  > -c, --clean
  >
  >   Delete all local resources of the subproject and regenerate them.
  >   
- [./script/generate.sh](<./scripts/generate.sh>)

  Generates the resources in each directory of `src/` `model/` `template/` in this project.
  The results are reflected in each directory of `dest/` `doc/` `script/`.

  *Generator input files*

  - `src/`
    Stores static resources that are not processed the generator.
    The contents of this directory are copied directly into the `dest/` directory.

  - `model/`
    Stores the static model data files written in *YAML* or *JSON* format used for the generation.

  - `template/`
    This directory contains the template files used for the generation.
    Files with a extension `.hbs` will be handled as templates. All other files are copied as is.

    - `template/dest` `template/doc` `template/scripts`
      Each of these directories contains the template files of the resource to be output
      in the directory `dest/` `doc/` `scripts`.

    - `template/model` `template/template`
      These directories store template files updating the contents of `template/` and `model/` used for the generation.
      If the content of `template/` `model/` is updated as a result of the generation,
      the generation process is executed recursively.
      The changes to `template/` `model/` that occur during the above process are treated as an intermediate state
      and will be lost after the completion of the process.
      Use the *--dry-run* option to check these intermediate files.

  *Generator output files*

  - `dest/`
    Outputs the source files of applications and modules created as the result of
    the generation process.

  - `doc/`
    Outputs the project documentation.

  - `scripts/`
    Outputs various scripts used in development and operation.

  > Usage: generate.sh [OPTION]...
  >
  > -h, --help
  >
  >   Displays how to use this command.
  >   
  > -v, --verbose
  >
  >   Displays more detailed command execution information.
  >   
  > -d, --dry-run
  >
  >   After this command is processed, the generated files are output to the `.NEXT` directory
  >   without reflecting to the folders of `dest/` `doc/` `scripts/`.
  >   In addition, the difference between the contents of the `.NEXT` directory and the current files.
  >   This directory also contains any intermediate files created during the generation.
  >   
  > -r, --max-recursion [VALUE]
  >
  >   The upper limit of the number of times to execute recursively
  >   when the contents of the `model/` `template/` directory are updated
  >   during the generation process.
  >    (Default: 10)
- [./script/git-each-subproject.sh](<./scripts/git-each-subproject.sh>)

  Executes the git sub-command specified by the argument for each subproject.

  Example:
  ```console
  $ ./scripts/null -c status
  ```

  > Usage: git-each-subproject.sh [OPTION]...
  >
  > -h, --help
  >
  >   Displays how to use this command.
  >   
  > -v, --verbose
  >
  >   Displays more detailed command execution information.
  >   
  > -c, --continue-on-error
  >
  >   Even if the given command fails in a subproject in the middle, executes it for the remaining subprojects.
  >   
- [./script/publish-local.sh](<./scripts/publish-local.sh>)

  After the resources in the project are generated,
  the resources in the `./dest` directory are built as a model module
  and registered in the local repository.

  > Usage: publish-local.sh [OPTION]...
  >
  > -h, --help
  >
  >   Displays how to use this command.
  >   
  > -v, --verbose
  >
  >   Displays more detailed command execution information.
  >   
  > -r, --max-recursion [VALUE]
  >
  >   This option is the same as the option of the same name in [generate.sh](<./scripts/generate.sh>).
  >    (Default: 10)
  > , --skip-generation
  >
  >   This option is the same as the option of the same name in [generate.sh](<./scripts/generate.sh>).
  >   
- [./script/publish-local-metamodel-plugin.sh](<./scripts/publish-local-metamodel-plugin.sh>)

  Generates resources for the [laplacian/metamodel-plugin](<null>) subproject.

  > Usage: publish-local-metamodel-plugin.sh [OPTION]...
  >
  > -h, --help
  >
  >   Displays how to use this command.
  >   
  > -v, --verbose
  >
  >   Displays more detailed command execution information.
  >   
### Source code list


- [model/project.yaml](<./model/project.yaml>)
- [src/entities/entity/example.yaml](<./src/entities/entity/example.yaml>)
- [src/entities/entity.yaml](<./src/entities/entity.yaml>)
- [src/entities/property_mapping.yaml](<./src/entities/property_mapping.yaml>)
- [src/entities/property.yaml](<./src/entities/property.yaml>)
- [src/entities/query.yaml](<./src/entities/query.yaml>)
- [src/entities/relationship.yaml](<./src/entities/relationship.yaml>)
- [src/entities/value_domain.yaml](<./src/entities/value_domain.yaml>)
- [src/value_domain_types/basic_type.yml](<./src/value_domain_types/basic_type.yml>)
- [src/value_domain_types/identifier.yml](<./src/value_domain_types/identifier.yml>)
- [src/value_domain_types/namespace.yml](<./src/value_domain_types/namespace.yml>)


<!-- @main-content@ -->