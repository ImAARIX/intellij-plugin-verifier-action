# IntelliJ Plugin Verifier GitHub Action

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-v1.3.0-undefined.svg?logo=github&logoColor=white&style=flat)](https://github.com/marketplace/actions/intellij-plugin-verifier)

Use GitHub Actions to verify the compatibility of your IntelliJ plugin against any version of IntelliJ IDEA.

## Usage

Simply add the action to your workflow-file and specify the path to your plugin, as well as the desired versions of IntelliJ IDEA to test, as shown in the example:

```yaml
steps:
- uses: actions/checkout@master
- uses: thepieterdc/intellij-plugin-verifier-action@v1.3.0
  with:
    plugin: '/path/to/plugin.zip'
    versions: |
      181.5684.4
      2019.3.3
```

## Arguments

This action currently requires 2 arguments:

| Input  | Description | Usage |
| :---:     |     :---:   |    :---:   |
| `plugin`  | The path to the `zip`-distribution of the plugin, generated by executing `./gradlew buildPlugin` | *Required* |
| `versions`  | Releases of IntelliJ that should be used to validate against, formatted as a multi-line string as shown in the example. | *Required* |

Note that you do not need to specify the full path (with e.g. the version number) to the zip-file, as illustrated in the example.

## Example
The following example builds a plugin using Gradle, and validates it against IDEA builds `181.5684.4`, `2019.3.3` and the latest EAP version.

```yaml
name: Plugin compatibility
on: [push]
jobs:
  run:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: Setup Java
      uses: actions/setup-java@v1
      with:
        java-version: 11.x.x
    - name: Build the plugin using Gradle
      run: ./gradlew buildPlugin
    - uses: thepieterdc/intellij-plugin-verifier-action@v1.3.0
      with:
        plugin: '/home/runner/work/demo-plugin/demo-plugin/build/distributions/demo-plugin-*'
        versions: |
          181.5684.4
          2019.3.3
          LATEST-EAP-SNAPSHOT
```
## Contributing

Contributions are always appreciated in the form of pull requests/issues.

## License

The code in this project is released under the [MIT License](LICENSE).
