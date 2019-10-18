# Dart/Flutter package analyzer

This action uses the [pana (Package ANAlysis) package](https://pub.dev/packages/pana) to compute the score that your Dart or Flutter package will have on the [Pub site](https://pub.dev/help), and annotates your code, with suggestions for improvements. 

This package, amongst other things:
* checks code formatting with [`dartfmt`](https://dart.dev/tools/dartfmt) or [`flutter format`](https://flutter.dev/docs/development/tools/formatting#automatically-formatting-code-with-the-flutter-command) (detected automatically),
* validates the code by performing static analysis with [dartanalyzer](https://dart.dev/tools/dartanalyzer),
* checks for outdated dependencies,
* validates the `pubscpec.yaml` file (dependencies, description's length...),
* checks for required files (`CHANGELOG`, `README`, `example` folder...)
* ...

## Usage

You must include the `actions/checkout` step in your workflow. Here's an example:
```yml
name: Workflow example
on: [push, pull_request]

jobs:
  package-analysis:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v1 # required
      - uses: axel-op/dart_package_analyzer@stable
        with:
          # Required:
          githubToken: ${{ secrets.GITHUB_TOKEN }}
          # Optional:
          relativePath: 'packages/mypackage/'
          minAnnotationLevel: info
```

* `githubToken` input is required to post a comment on GitHub. **Note:** this secret is already provided by GitHub and you don't have to set it up yourself. 
* If your package isn't at the root of the repository, use `relativePath` to indicate its location.
* If you only want to see annotations for important errors, try to change the `minAnnotationLevel` parameter to another value. Accepted values are `info`, `warning` and `error`. Defaults to `info` that posts all the annotations. 

## Example

![](example.png)

