# Aviator

Aviator is a small CLI tool to run genereic **Aviator** Concourse pipelines.

## Installation (Mac Only)

comming soon ...

## Prereqs

- [Spruce](https://github.com/geofffranks/spruce) CLI Tool
- [Fly](https://github.com/concourse/fly) CLI Tool

## Aviator Properties

**aviator.yml**

Example:

```
spruce:
- base: base.yml
  prune:
  - meta
  with:
    files:
    - another.yml
    - yet-another.yml
  to: result.yml
- base: result.yml
  for_each_in: path/to/dir/
  regexp: match-string
  to_dir: path/to/destination/
- base: another-base.yml
  walk_through: will/walt/through/subdirs
  to_dir: path/to/destiantion/

fly:
 config: pipeline.yml
 vars:
 - credentials.yml
 - personal.yml
```

### Spruce

- **base (string):** This is the base yml file you want to spruce into.

- **prune (array):** Here you can list all properties you want to prune.

- **with (array):**

    - **files** List specific files you want to spruce on top of the base.
    - **in_dir** (optional) If specified, each file in `files` will be prefixed with this string. This allows to specify specific file in a directory.


- **with_in (string):** You can also include all files within a dir to the spruce command by using this property.

- **to (string):** Filename you want to save the spruced file to.

- **to_dir (string):** Path you want to save the spruced files to. Use this property only in combination with `for_each`, `for_each_in`, and `walk_through`.

- **for_each (array):** List all files which need to be spruced with a base file seperately.

- **for_each_in (string):** Specify a dir which contains all files a base needs to be spruced with.

- **walk_through (string):** Same as `for_each_in`, but it walks through all subdirectories.

  - **for_all (string):** Adds an outer-loop to the walk_through loop
  - **enable_matching (bool):**
  - **copy_parents (bool):** parent directories will be copied to destination


- **regexp (string):** will include only files matching the regexp.

### Fly (Optional)

- **config (string):** the pipeline config file (yml)
- **vars (array):** List of all property files (-l)

## Usage

make sure to have the `aviator.yml` in your directory. Then execute aviator:

**Spruce only**

```
$ aviator
```

**With Fly**

```
$ aviator -t <target> -p <pipeline-name>
```
