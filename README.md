# sass_builder

[![Build Status](https://travis-ci.org/dart-league/sass_builder.svg?branch=master)](https://travis-ci.org/dart-league/sass_builder)

Transpile sass files using the [build][1] package and the dart implementation
of [sass][2].

[1]: https://github.com/dart-lang/build
[2]: https://github.com/sass/dart-sass

## Usage

1\. Create a `pubspec.yaml` file containing the following code:

```yaml
dependencies:
    # update to the latest version
    bootstrap_sass: any
dev_dependencies:
    # update to the latest version
    sass_builder: ^1.0.0
    build_runner: ^0.7.0
```

2\. Create `web/main.scss` containing the following code:

```scss
@import "sub";
@import "package:bootstrap_sass/scss/variables";

.a {
  color: blue;
}

.c {
  color: $body-color;
}

```

3\. Create `web/_sub.scss` containing the following code:

```scss
.b {
  color: red;
}

```

4\. Create `web/index.html` containing the following code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Sample</title>
    <link rel="stylesheet" href="main.css">
</head>
<body>
<div class="a">Some Text</div>
<div class="b">Some Text</div>
<div class="c">Some Text</div>
</body>
</html>
```

5\. Run `pub run build_runner serve` and then go to `localhost:8080` with a browser
 and check if the file `web/main.css` was generated containing:

```css
.b {
  color: red;
}

.a {
  color: blue;
}

.c {
  color: #373a3c;
}
```

## Wrapped as a Pub Transformer

To automatically generate .css files when you run `pub build` or `pub serve`
you can add sass_builder as a transformer in your package.

In your `pubspec.yaml` add the following code:

```yaml
dependencies:
  sass_builder ^1.0.0 # update for the latest version
transformers:
- sass_builder
```

By default this will generate .css files for every non-partial .scss file in your project.
 You can customize the extension of the generated files with the `outputExtension` option:

```yaml
transformers:
- sass_builder:
    outputExtension: .scss.css
```
