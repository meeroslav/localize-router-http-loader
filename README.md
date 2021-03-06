# localize-router-http-loader
[![Build Status](https://travis-ci.org/Greentube/localize-router-http-loader.svg?branch=master)](https://travis-ci.org/Greentube/localize-router-http-loader)
[![npm version](https://img.shields.io/npm/v/localize-router-http-loader.svg)](https://www.npmjs.com/package/localize-router-http-loader)
> A loader for [localize-router](https://github.com/Greentube/localize-router) that loads config using Http

> This package is built for angular version >=4.3. If you are still using old Angular please use `localize-router-http-loader` version <1.0.0

- [Installation](#installation)
- [Usage](#usage)
  - [Parameters](#parameters)
  - [Config file](#config-file)
- [License](#license)

## Installation

```
npm install --save localize-router-http-loader
```

## Usage

In order to load `localize-router` config via http, you must initialize LocalizeRouterModule with LocalizeRouterHttpLoader:

```ts
// Required for AoT
export function HttpLoaderFactory(translate: TranslateService, location: Location, settings: LocalizeRouterSettings, http: HttpClient) {
  return new LocalizeRouterHttpLoader(translate, location, settings, http);
}

LocalizeRouterModule.forRoot(routes, {
    parser: {
        provide: LocalizeParser,
        useFactory: HttpLoaderFactory,
        deps: [TranslateService, Location, LocalizeRouterSettings, HttpClient]
    }
})
```

### Parameters

`LocalizeRouterHttpLoader` has one optional parameter `path` which points to json config file. Default value is `assets/locales.json`.

```ts
export function HttpLoaderFactory(translate: TranslateService, location: Location, settings: LocalizeRouterSettings, http: HttpClient) {
  return new LocalizeRouterHttpLoader(translate, location, settings, http, 'my/custom/url/to/file.json');
}
```

### Config file

JSON config file has following structure:
```
{
    "locales": ["en", "de", ...],
    "prefix": "MY_PREFIX"
}
```

```ts
interface ILocalizeRouterParserConfig {
    locales: Array<string>;
    prefix?: string;
}
```

Prefix field is not mandatory and default value is empty string.

## License
Licensed under MIT
