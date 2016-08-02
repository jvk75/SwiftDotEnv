# SwiftDotEnv

Swift 3 library that loads environment variables from `.env` into the environment inspired by the [Ruby dotenv][1] and [PHP dotenv][2] projects.

[1]: https://github.com/bkeepers/dotenv
[2]: https://github.com/vlucas/phpdotenv

## Why?

Storing [configuration in the environment](http://12factor.net/config) is one of the tenets of a [twelve-factor app](http://12factor.net). Anything that is likely to change between deployment environments–such as resource handles for databases or credentials for external services–should be extracted from the code into environment variables.

But it is not always practical to set environment variables on development machines or continuous integration servers where multiple projects are run. SwiftDotEnv loads variables from a `.env` file into `ENV` when the environment is bootstrapped.

## Installation

Install using [Swift Package Manager](https://swift.org/package-manager/).


## Usage

```swift
import DotEnv

let env = DotEnv(withFile: ".env")

let host = env.get("DB_HOST") ?? "localhost"
let port = env.getInt("DB_PORT") ?? 3306
let isEnabled = env.getBool("IS_ENABLED") ?? true
```

There are three getter methods: 

* `get()` returns a `String?`
* `getInt()` returns an `Int?`
* `getBool()` returns a `Bool?` where case-insensitive `"true"`, `"yes"` and `"1"` evaluate to `true`

You can also use subscript access to retrieve the string version:

```swift
let host = env["DB_HOST"] ?? "localhost"
```

As a convenience, you can use `env.all()` to retrieve all environment variables.


## Caveats

Currently has a very naive parser of the `.env` file and so doesn't support multi-line values.


## Contribute

Contributions welcome! Please put your changes in a separate branch from master and raise a PR.
