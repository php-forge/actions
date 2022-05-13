<p align="center">
    <a href="https://github.com/php-forge/reusable-actions" target="_blank">
        <img src="https://avatars.githubusercontent.com/u/103309199?s=400&u=ca3561c692f53ed7eb290d3bb226a2828741606f&v=4" height="100px">
    </a>
    <h1 align="center">PHP Forge - Reusable actions</h1>
    <br>
</p>

## Requerimientos

- PHP.

## Uso

### Ejemplo de uso de la acción [PHPUnit](https://github.com/sebastianbergmann/phpunit)

```yml
on:
  - pull_request
  - push
  
name: build

jobs:
  phpunit:
    uses: php-forge/reusable-actions/.github/workflows/phpunit.yml@main
    with:
      # coverage: pcov / coverage: xdebug / coverage: xdebug2 / coverage: none 
      # extensions: pdo, pdo_pgsql
      # ini-values: date.timezone='UTC'      
      os: >-
        ['ubuntu-latest', 'windows-latest']
      php: >-
        ['8.0', '8.1']
      #tools: composer:v2 
    secrets:
      CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}
```

### Ejemplo de uso de la acción [PSALM](https://github.com/vimeo/psalm)

```yml
on:
  - pull_request
  - push

name: static analysis

jobs:
  psalm:
    uses: php-forge/reusable-actions/.github/workflows/psalm.yml@main
    with:
      os: >-
        ['ubuntu-latest']
      php: >-
        ['7.4', '8.0', '8.1']
```

### Ejemplo de uso de la acción [ROAVE-INFECTION](https://github.com/roave/infection-static-analysis-plugin)

```yml
on:
  - pull_request
  - push

name: mutation test

jobs:
  mutation:
    uses: php-forge/reusable-actions/.github/workflows/roave-infection.yml@main
    with:
      os: >-
        ['ubuntu-latest']
      php: >-
        ['8.1']
    secrets:
      STRYKER_DASHBOARD_API_KEY: ${{ secrets.STRYKER_DASHBOARD_API_KEY }}
```

## Licencia

El paquete `php-forge/reusable-actions` es software libre. Se publica bajo los términos de la Licencia BSD.
Consulte [`LICENSE`](./LICENSE.md) para obtener más información.

Mantenido por [Terabytesoftw](https://github.com/terabytesoftw).

## Nuestras redes sociales

[![Twitter](https://img.shields.io/badge/twitter-follow-1DA1F2?logo=twitter&logoColor=1DA1F2&labelColor=555555?style=flat)](https://twitter.com/PhpForge)
