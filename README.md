# Nag

> The mother-in-law of linters

A microservice to nag you about code quality; [Pronto](https://github.com/mmozuras/pronto)-as-a-Service.

## Getting Started

1. Clone the project:

	```shell
	$ git clone git@github.com:wombatsecurity/nag.git
	$ cd nag
	```

2. Install dependencies:

  ```shell
  $ mix deps.get
  ```

3. Build and run:

  ```shell
  $ GITHUB_ACCESS_TOKEN= mix run --no-halt
  ```

## Getting Started (with Docker)

1. Install Docker

2. Build and run container:

	```shell
	$ docker build -t wombatsecurity/nag .
	$ docker run -d -p 4000:4000 -v -e GITHUB_ACCESS_TOKEN= wombatsecurity/nag
	```

	If you've made changes and docker isn't picking them up, use the `--no-cache` flag when building:

	```shell
	$ docker build --no-cache -t wombatsecurity/nag .
	```

## Lifecycle

![Life cycle](lifecycle.png)

## Current Support

The following is a list of currently support languages and runners supported by each:

- Ruby — Brakeman, Fasterer, Flay, Rails Best Practices, Reek, Rubocop
- JavaScript — JSLint
- CoffeeScript — CoffeeLint
- Elixir — Credo

Pronto does not yet support Java but that's something we can contribute! Pronto runners wrap any CLI tool and normalize the output, there are three tools to consider for future incorporation:

- [Findbugs](http://findbugs.sourceforge.net) — Identify existing bugs.
- [PMD](https://pmd.github.io) — Code quality, anti-patterns, error prone code.
- [Checkstyle](http://checkstyle.sourceforge.net) — Styleguide enforcement.

## Running Locally

As it stands today, Nag relies on GitHub webhooks to know when and what to analyze.  During local development [Postman](https://getpostman.com) (or any REST  client) can be used to fake webhook requests to our local Nag server.  Local requests should target [localhost:4000/webhook](http://localhost:4000/webhook).

There are only a handful of fields required by Nag so a minimal request without those values will suffice:

```json
{
  "action": "opened",
  "pull_request": {
    "number": 1,
    "state": "open",
    "head": {
      "ref": "branch-name",
      "repo": {
        "full_name": "wombatsecurity/repo-name"
      }
    }
  }
}
```
