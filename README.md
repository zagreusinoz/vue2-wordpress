# vue2-wordpress

## Introduction
A Vue2 and Quasar Framework starter project for building an app which front-ends a WordPress blog.

## Features

- View post list.
- Read the full list.
- iOS or Material designs.

## Installation

First, install the [Quasar Framework](http://quasar-framework.org/) cli. 

```shell
npm i -g quasar-cli
```

And then install the project dependencies.

```shell
npm i
```

Update the environment variables in `config/prod.env.js`
* WP_BASE: The base URL of your blog (e.g. http://myblog.com)
* BLOG_NAME: The title of your blog (e.g. My Blog)

You can run the client with quasar tools:

```shell
# Run the application with material design
quasar dev

# Run the application with iOS design
quasar dev ios
```

## Cordova Builds

You can use the [Quasar Framework wrappers](http://quasar-framework.org/guide/cordova-wrapper.html) to build this project for iOS or Android. 

## Contributing

Contributions are encouraged.  Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Alternatives

*Not found.*

*Feel free to add more alternatives as Pull Request.*

## License

- `Laravel Eloquent Flag` package is open-sourced software licensed under the [GPLv3](LICENSE).
