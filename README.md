# WP LPT Environment
Lando development environment for [WordPress/wp-lpt theme](https://github.com/diva-dev/wp-lpt).
## Requirements

* [Lando](https://lando.dev/)

## Installation

### Enviroment installation

Install project with the following steps:

**1. Start lando**
```bash
  lando start
```

**2. Install WordPress core**
```bash
  lando install:wordpress
```
    
**3. Install the WP-LPT theme**
```bash
  lando install:theme
```

**4. Install the plugins theme**
```bash
  lando install:plugins
```

### Theme setup

**1. Download and install DB from staging**
```bash
  # ssh into staging
  ssh divastaging.co.uk

  # go to subdomain
  cd lpt.divastaging.co.uk

  # create database
  wp db export

  # scp the database
  scp divastaging.co.uk:lpt.divastaging.co.uk/divastag_lpt-*.sql ./

  # import the database into lando db
  ## {project_root}/wordpress
  lando wp db import divastag_lpt-*.sql

  # Update the url
  ## {project_root}/wordpress
  lando wp search-replace --all-tables --verbose 'lpt.divastaging.co.uk' 'lpt.test'
  lando wp search-replace --all-tables --verbose 'http://lpt.test' 'https://lpt.test'
```

**2. Rsync the media files from staging**
```bash
  # Rsync the uploads folder
  ## {project_root}/wordpress/wp-content/uploads
  rsync -chavzP --stats divastaging.co.uk:~/lpt.divastaging.co.uk/wp-content/uploads/ ./
```

**3. Build node modules**
```bash
  # Install node_modules
  ## {project_root}/wordpress/wp-content/themes/wp-lpt
  lando yarn

  # Install bower packages
  ## {project_root}/wordpress/wp-content/themes/wp-lpt
  lando bower install
```

**4. Build assets**
```bash
  # Dev mode
  ## {project_root}/wordpress/wp-content/themes/wp-lpt
  lando yarn start

  # Build assets
  ## {project_root}/wordpress/wp-content/themes/wp-lpt
  lando yarn build
```
# childrens-commissioner-lando-environment
