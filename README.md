<!-- markdownlint-disable MD041 -->
<p align="center">
    <a href="https://github.com/php-forge/actions" target="_blank">
    <img
        alt="PHPForge Logo"
        height="100px"
        src="https://avatars.githubusercontent.com/u/103309199?s=400&u=ca3561c692f53ed7eb290d3bb226a2828741606f&v=4"
    >
    </a>
    <h1 align="center">PHPForge - Reusable GitHub Actions</h1>
    <br>
</p>
<!-- markdownlint-enable MD041 -->

A comprehensive collection of reusable GitHub Actions and workflows specifically designed for PHP projects. Streamline
your CI/CD pipeline with battle-tested, configurable workflows for testing, static analysis, and code quality checks.

## Features

- ✅ **Code Quality** - Easy Coding Standard (ECS) for consistent code formatting.
- ✅ **Complete Testing Suite** - PHPUnit, Codeception, and mutation testing with Infection.
- ✅ **Database Testing** - Multi-database support (MySQL, PostgreSQL, SQLite, etc.).
- ✅ **Dependency Management** - Composer require checker for dependency validation.
- ✅ **Static Analysis** - PHPStan integration.
- ✅ **Zero Configuration** - Sensible defaults with extensive customization options.

## Available Workflows

### Testing Workflows

- [`codeception.yml`](https://github.com/php-forge/actions/blob/main/.github/workflows/codeception.yml) - Codeception testing framework.
- [`infection.yml`](https://github.com/php-forge/actions/blob/main/.github/workflows/infection.yml) - Mutation testing with Infection.
- [`phpunit-database.yml`](https://github.com/php-forge/actions/blob/main/.github/workflows/phpunit-database.yml) - PHPUnit with database services.
- [`phpunit.yml`](https://github.com/php-forge/actions/blob/main/.github/workflows/phpunit.yml) - PHPUnit testing with coverage.

### Quality Assurance Workflows

- [`composer-require-checker.yml`](https://github.com/php-forge/actions/blob/main/.github/workflows/composer-require-checker.yml) - Dependency validation.
- [`ecs.yml`](https://github.com/php-forge/actions/blob/main/.github/workflows/ecs.yml) - Easy Coding Standard.
- [`phpstan.yml`](https://github.com/php-forge/actions/blob/main/.github/workflows/phpstan.yml) - Static analysis.

### Utility Actions

- [`php-setup`](https://github.com/php-forge/actions/blob/main/actions/php-setup/action.yml) - PHP environment setup.
- [`phpunit-runner`](https://github.com/php-forge/actions/blob/main/actions/phpunit/action.yml) - Advanced PHPUnit execution.

## Quick start

### Composer Require Checker

```yaml
---
on:
    pull_request:
        paths-ignore:
            - "docs/**"
            - "README.md"
            - "CHANGELOG.md"
            - ".gitignore"
            - ".gitattributes"

    push:
        paths-ignore:
            - "docs/**"
            - "README.md"
            - "CHANGELOG.md"
            - ".gitignore"
            - ".gitattributes"

name: composer-require-checker

jobs:
    dependency-check:
        uses: php-forge/actions/.github/workflows/composer-require-checker.yml@v1
        with:
            command-options: "--config-file=.composer-require-checker.json"
```

### Easy Coding Standard

```yaml
---
on:
  pull_request:
    paths-ignore:
      - "docs/**"
      - "README.md"
      - "CHANGELOG.md"
      - ".gitignore"
      - ".gitattributes"

  push:
    paths-ignore:
      - "docs/**"
      - "README.md"
      - "CHANGELOG.md"
      - ".gitignore"
      - ".gitattributes"

name: easy-coding-standards

jobs:
  coding-standards:
    uses: php-forge/actions/.github/workflows/ecs.yml@v1
    with:
      command-options: "check --ansi --no-progress-bar"
      php-version: '["8.4"]'
```

### Infection Mutation Testing {#infection}

```yaml
---
on:
    pull_request:
        paths-ignore:
            - "docs/**"
            - "README.md"
            - "CHANGELOG.md"
            - ".gitignore"
            - ".gitattributes"

    push:
        paths-ignore:
            - "docs/**"
            - "README.md"
            - "CHANGELOG.md"
            - ".gitignore"
            - ".gitattributes"

name: mutation-testing

jobs:
    mutation-testing:
        uses: php-forge/actions/.github/workflows/reusable-infection.yml@v2
        secrets:
            STRYKER_DASHBOARD_API_KEY: ${{ secrets.STRYKER_DASHBOARD_API_KEY }}
        with:
            # Infection configuration
            command-options: "--threads=4 --min-msi=80"
            command-coverage-options: --with-uncovered

            # PHPStan integration
            phpstan: true
```

### Linting with Super-Linter

```yaml
---
on:
    pull_request:
        paths-ignore:
            - "docs/**"
            - "README.md"
            - "CHANGELOG.md"
            - ".gitignore"
            - ".gitattributes"

    push:
        paths-ignore:
            - "docs/**"
            - "README.md"
            - "CHANGELOG.md"
            - ".gitignore"
            - ".gitattributes"

name: linter

jobs:
    linter:
        uses: php-forge/actions/.github/workflows/reusable-linter.yml@main
        secrets:
            AUTH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### PHPUnit

```yaml
---
on:
    pull_request:
        paths-ignore:
            - "docs/**"
            - "README.md"
            - "CHANGELOG.md"
            - ".gitignore"
            - ".gitattributes"

    push:
        paths-ignore:
            - "docs/**"
            - "README.md"
            - "CHANGELOG.md"
            - ".gitignore"
            - ".gitattributes"

name: build

jobs:
    phpunit:
        uses: php-forge/actions/.github/workflows/phpunit.yml@v1
        secrets:
            AUTH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
            CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}
        with:
            # Composer settings
            composer-command: composer install --prefer-dist --no-progress

            # Coverage settings
            coverage-driver: pcov
            coverage-format: clover

            # PHP configuration
            extensions: mbstring, intl, pdo_sqlite
            ini-values: date.timezone='UTC', memory_limit=-1

            # Operating systems
            os: '["ubuntu-latest", "windows-2022"]'

            # PHP versions to test
            php-version: '["8.1", "8.2", "8.3", "8.4"]'

            # PHPUnit configuration
            phpunit-configuration: phpunit.xml
            phpunit-exclude-group: integration
            phpunit-group: unit
```

### PHPUnit with Database

```yaml
---
on:
    pull_request:
        paths-ignore:
            - "docs/**"
            - "README.md"
            - "CHANGELOG.md"
            - ".gitignore"
            - ".gitattributes"

    push:
        paths-ignore:
            - "docs/**"
            - "README.md"
            - "CHANGELOG.md"
            - ".gitignore"
            - ".gitattributes"

name: build-mysql

jobs:
    database-tests:
        uses: php-forge/actions/.github/workflows/phpunit-database.yml@v1
        secrets:
            CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}
        with:
            # Database configuration
            database-env: |
                {
                    "MYSQL_ROOT_PASSWORD": "root",
                    "MYSQL_DATABASE": "test"
                }
            database-health-cmd: "mysqladmin ping"
            database-health-retries: 3
            database-image: mysql
            database-port: 3306
            database-type: mysql
            database-versions: '["8.0", "8.4", "latest"]'
            extensions: pdo, pdo_mysql
            php-version: '["8.4"]'
            phpunit-group: mysql
```

### PHPStan Static Analysis

```yaml
---
on:
    pull_request:
        paths-ignore:
            - "docs/**"
            - "README.md"
            - "CHANGELOG.md"
            - ".gitignore"
            - ".gitattributes"

    push:
        paths-ignore:
            - "docs/**"
            - "README.md"
            - "CHANGELOG.md"
            - ".gitignore"
            - ".gitattributes"

name: static-analysis

jobs:
    static-analysis:
        uses: php-forge/actions/.github/workflows/phpstan.yml@v1
        with:
            # PHPStan configuration
            configuration: phpstan.neon
            command-options: "analyse --error-format=checkstyle | cs2pr"

            # Environment
            php-version: '["8.4"]'
            tools: cs2pr
```

**Supported Databases:**

| Database   | Docker Image                     | Default Port | Health Check Command     |
| ---------- | -------------------------------- | ------------ | ------------------------ |
| MySQL      | `mysql`                          | 3306         | `mysqladmin ping`        |
| PostgreSQL | `postgres`                       | 5432         | `pg_isready`             |
| SQL Server | `mcr.microsoft.com/mssql/server` | 1433         | `sqlcmd -Q "SELECT 1"`   |
| Oracle     | `gvenzl/oracle-xe`               | 1521         | `sqlplus -S / as sysdba` |

## Package information

[![GitHub Release](https://img.shields.io/github/v/release/php-forge/actions?style=for-the-badge&logo=git&logoColor=white&label=Release)](https://github.com/php-forge/actions/releases)

## Quality code

[![Super-Linter](https://img.shields.io/github/actions/workflow/status/php-forge/actions/linter.yml?style=for-the-badge&label=Super-Linter&logo=github)](https://github.com/php-forge/actions/actions/workflows/linter.yml)

## Our social networks

[![Follow on X](https://img.shields.io/badge/-Follow%20on%20X-1DA1F2.svg?style=for-the-badge&logo=x&logoColor=white&labelColor=000000)](https://x.com/Terabytesoftw)

## License

[![License](https://img.shields.io/github/license/yii2-extensions/psr-bridge?style=for-the-badge&logo=opensourceinitiative&logoColor=white&labelColor=333333)](LICENSE)
