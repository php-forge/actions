<p align="center">
    <a href="https://github.com/php-forge/reusable-actions" target="_blank">
        <img src="https://avatars.githubusercontent.com/u/103309199?s=400&u=ca3561c692f53ed7eb290d3bb226a2828741606f&v=4" height="100px">
    </a>
    <h1 align="center">PHPForge - Reusable GitHub Actions</h1>
    <br>
</p>

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

| Workflow | Description | Use Case |
|----------|-------------|----------|
| [`codeception.yml`](#codeception) | Codeception testing framework | Acceptance and functional tests |
| [`infection.yml`](#infection) | Mutation testing | Code quality validation |
| [`phpunit-database.yml`](#phpunit-database) | PHPUnit with database services | Database-dependent tests |
| [`phpunit.yml`](#phpunit) | PHPUnit testing with coverage | Unit and integration tests |

### Quality Assurance Workflows

| Workflow | Description | Use Case |
|----------|-------------|----------|
| [`composer-require-checker.yml`](#composer-require-checker) | Dependency validation | Ensure proper dependencies |
| [`ecs.yml`](#ecs) | Easy Coding Standard | Code formatting and style |
| [`phpstan.yml`](#phpstan) | Static analysis | Type checking and bug detection |

### ⚙️ Utility Actions

| Action | Description | Use Case |
|--------|-------------|----------|
| [`php-setup`](#php-setup) | PHP environment setup | Prepare PHP with extensions |
| [`phpunit-runner`](#phpunit-runner) | Advanced PHPUnit execution | Custom test execution |

## Quick start

### Basic PHPUnit Testing

```yaml
on:
  pull_request:
    paths-ignore:
      - 'docs/**'
      - 'README.md'
      - 'CHANGELOG.md'
      - '.gitignore'
      - '.gitattributes'

  push:
    paths-ignore:
      - 'docs/**'
      - 'README.md'
      - 'CHANGELOG.md'
      - '.gitignore'
      - '.gitattributes'

name: tests

jobs:
  tests:
    uses: php-forge/actions/.github/workflows/phpunit.yml@v1
    secrets:
      CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}
    with:
      os: '["ubuntu-latest", "windows-latest"]'
      php-version: '["8.1", "8.2", "8.3", "8.4"]'
```

### Complete Quality Pipeline

```yaml
on:
  pull_request:
    paths-ignore:
      - 'docs/**'
      - 'README.md'
      - 'CHANGELOG.md'
      - '.gitignore'
      - '.gitattributes'

  push:
    paths-ignore:
      - 'docs/**'
      - 'README.md'
      - 'CHANGELOG.md'
      - '.gitignore'
      - '.gitattributes'
      
name: quality

jobs:
  static-analysis:
    uses: php-forge/actions/.github/workflows/phpstan.yml@v1
    
  coding-standards:
    uses: php-forge/actions/.github/workflows/ecs.yml@v1
    
  dependency-check:
    uses: php-forge/actions/.github/workflows/composer-require-checker.yml@v1
    
  mutation-testing:
    uses: php-forge/actions/.github/workflows/infection.yml@v1
    secrets:
      STRYKER_DASHBOARD_API_KEY: ${{ secrets.STRYKER_DASHBOARD_API_KEY }}
```

## Our social networks

[![X](https://img.shields.io/badge/follow-@terabytesoftw-1DA1F2?logo=x&logoColor=1DA1F2&labelColor=555555&style=flat)](https://x.com/Terabytesoftw)

## License

[![License](https://img.shields.io/github/license/yii2-extensions/nested-sets-behavior)](LICENSE.md)
