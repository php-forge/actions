<p align="center">
    <a href="https://github.com/php-forge/reusable-actions" target="_blank">
        <img src="https://avatars.githubusercontent.com/u/103309199?s=400&u=ca3561c692f53ed7eb290d3bb226a2828741606f&v=4" height="100px">
    </a>
    <h1 align="center">PHPForge - actions reusable</h1>
    <br>
</p>

## Requeriments

- PHP.

## Usage

### Example of using the [Dependency check](https://github.com/maglnet/ComposerRequireChecker)

```yml
on:
  pull_request:
    paths-ignore:
      - 'docs/**'
      - 'README.md'
      - 'CHANGELOG.md'
      - '.gitignore'
      - '.gitattributes'
      - 'infection.json.dist'
      - 'phpunit.xml.dist'
      - 'psalm.xml'

  push:
    branches: ['main']
    paths-ignore:
      - 'docs/**'
      - 'README.md'
      - 'CHANGELOG.md'
      - '.gitignore'
      - '.gitattributes'
      - 'infection.json.dist'
      - 'phpunit.xml.dist'
      - 'psalm.xml'

name: dependency-check

jobs:
  composer-require-checker:
    uses: php-forge/actions/.github/workflows/composer-require-checker.yml@main
    secrets:
      AUTH_TOKEN: ${{ secrets.AUTH_TOKEN }} # for repository private
    with:
      os: >-
        ['ubuntu-latest']
      php: >-
        ['8.1', '8.2']
```

### Example of using the [Easy Coding Standard](https://github.com/easy-coding-standard/easy-coding-standard)

```yml
on:
  pull_request:
    paths-ignore:
      - 'docs/**'
      - 'README.md'
      - 'CHANGELOG.md'
      - '.gitignore'
      - '.gitattributes'
      - 'infection.json.dist'
      - 'phpunit.xml.dist'

  push:
    branches: ['main']
    paths-ignore:
      - 'docs/**'
      - 'README.md'
      - 'CHANGELOG.md'
      - '.gitignore'
      - '.gitattributes'
      - 'infection.json.dist'
      - 'phpunit.xml.dist'

name: ecs

jobs:
  easy-coding-standard:
    uses: php-forge/actions/.github/workflows/ecs.yml@main
    secrets:
      AUTH_TOKEN: ${{ secrets.AUTH_TOKEN }} # for repository private
    with:
      os: >-
        ['ubuntu-latest']
      php: >-
        ['8.1', '8.2']
```

### Example of using the [PHPUnit](https://github.com/sebastianbergmann/phpunit) action.

```yml
on:
  pull_request:
    paths-ignore:
      - 'docs/**'
      - 'README.md'
      - 'CHANGELOG.md'
      - '.gitignore'
      - '.gitattributes'
      - 'infection.json.dist'
      - 'psalm.xml'

  push:
    branches: ['main']
    paths-ignore:
      - 'docs/**'
      - 'README.md'
      - 'CHANGELOG.md'
      - '.gitignore'
      - '.gitattributes'
      - 'infection.json.dist'
      - 'psalm.xml'
  
name: build

jobs:
  phpunit:
    uses: php-forge/actions/.github/workflows/phpunit.yml@main
    secrets:
      AUTH_TOKEN: ${{ secrets.AUTH_TOKEN }} # for repository private
      CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}
    with:
      # coverage: pcov / coverage: xdebug / coverage: xdebug2 / coverage: none 
      # extensions: ext-php 
      # ini-values: date.timezone='UTC'      
      os: >-
        ['ubuntu-latest', 'windows-latest']
      php: >-
        ['8.0', '8.1']
      #tools: composer:v2 
```

### Example of using the [PSALM](https://github.com/vimeo/psalm) action.

```yml
on:
  pull_request:
    paths-ignore:
      - 'docs/**'
      - 'README.md'
      - 'CHANGELOG.md'
      - '.gitignore'
      - '.gitattributes'
      - 'infection.json.dist'
      - 'psalm.xml'

  push:
    branches: ['main']
    paths-ignore:
      - 'docs/**'
      - 'README.md'
      - 'CHANGELOG.md'
      - '.gitignore'
      - '.gitattributes'
      - 'infection.json.dist'
      - 'psalm.xml'

name: static analysis

jobs:
  psalm:
    uses: php-forge/actions/.github/workflows/psalm.yml@main
    secrets:
      AUTH_TOKEN: ${{ secrets.AUTH_TOKEN }} # for repository private   
    with:
      # extensions: ext-php 
      # ini-values: date.timezone='UTC'       
      os: >-
        ['ubuntu-latest']
      php: >-
        ['7.4', '8.0', '8.1']
      #tools: composer:v2, cs2pr 
```

### Example of using the [ROAVE-INFECTION](https://github.com/roave/infection-static-analysis-plugin) action.

```yml
on:
  pull_request:
    paths-ignore:
      - 'docs/**'
      - 'README.md'
      - 'CHANGELOG.md'
      - '.gitignore'
      - '.gitattributes'
      - 'infection.json.dist'
      - 'psalm.xml'

  push:
    branches: ['main']
    paths-ignore:
      - 'docs/**'
      - 'README.md'
      - 'CHANGELOG.md'
      - '.gitignore'
      - '.gitattributes'
      - 'infection.json.dist'
      - 'psalm.xml'

name: mutation test

jobs:
  mutation:
    uses: php-forge/actions/.github/workflows/roave-infection.yml@main
    secrets:
      AUTH_TOKEN: ${{ secrets.AUTH_TOKEN }} # for repository private
      STRYKER_DASHBOARD_API_KEY: ${{ secrets.STRYKER_DASHBOARD_API_KEY }}    
    with:
      # coverage: pcov / coverage: xdebug / coverage: xdebug2 / coverage: none 
      # extensions: ext-php
      # ini-values: date.timezone='UTC'   
      os: >-
        ['ubuntu-latest']
      php: >-
        ['8.1']
      #tools: composer:v2        
```

## Our social networks

[![Twitter](https://img.shields.io/badge/twitter-follow-1DA1F2?logo=twitter&logoColor=1DA1F2&labelColor=555555?style=flat)](https://twitter.com/Terabytesoftw)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
