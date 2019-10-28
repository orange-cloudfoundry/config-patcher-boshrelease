# config-patcher-boshrelease

Boshrelease to use [config-patcher](https://github.com/orange-cloudfoundry/config-patcher).

## Usage

1. Deploy boshrelease as bosh addons with manifest [/manifest/add-addons-config-patcher.yml](/manifest/add-addons-config-patcher.yml)
2. Now you can create config patch file in your jobs by writing yaml file in a new directory inside your job **config-patcher**

Example in a spec file in your job:

```yaml
---
name: my-patch

templates:
  my-patch.yml: config-patcher/my-patch.yml
```

## Patch format

```yaml
- config_file: <config-file> # config file in input which will be patched
  config_type: <json | yaml | toml> # this is actually not mandatory but you could need to set explicitly type of your config file
  patches:
    - op: <add | remove | replace | move | copy | test>
      from: <source-path> # only valid for the 'move' and 'copy' operations
      path: <target-path> # always mandatory
      value: <any-yaml-structure> # only valid for 'add', 'replace' and 'test' operations
```