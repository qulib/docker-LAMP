This project is used as a local development server for working on the QUL website. It does its best to mirror the stack we have in production.

Getting Started
---------------

1. Pull this repo and enter the root dir
2. run 'docker-compose up -d --build'
3. navigate to 'localhost'

At this point you'll need add some content to the `www` folder; to serve up the QUL website:

1. Make sure you're still in the root dir of this project
2. Pull the [qul-site](https://gitlab.com/quladmin/qul-site) repo (note: you can simlink to the repo if you've already cloned it elsewhere)
3. Replace the missing files from the repo (`settings.local.php`, the entire `files` directory, `main-bg.jpg` in the theme)
4. Connect to the local database container (e.g. via Sequel Pro) and load today's data
5. Rename the folder from 'qul-site' to 'www'

Notes
-----
Make sure your settings.local.php file database connection settings match those from `docker-compose.yml`.

**IMPORTANT**: Instead of `localhost` for the database and memcache servers, you need to use the name of the container. Here is what my `/www/sites/default/settings.local.php` file looks like:

```
<?php

$databases['default']['default'] = array(
  'database' => 'qul_d7_db',
  'username' => 'drupal',
  'password' => 'drupal',
  'host' => 'database',
  'port' => '3306',
  'driver' => 'mysql',
  'prefix' => '',
);

$conf['workbench_moderation_per_node_type'] = TRUE;
$conf['memcache_servers'] = array('memcached:11211' => 'default');
$conf['cache_backends'][] = 'sites/all/modules/contrib/memcache/memcache.inc';
$conf['cache_default_class'] = 'MemCacheDrupal';
$conf['cache_class_cache_form'] = 'DrupalDatabaseCache';
$conf['page_cache_without_database'] = TRUE;
$conf['page_cache_invoke_hooks'] = FALSE;

```

Drush
----
Drush 8.1.18 included.
Call drush outside docker web container as `docker exec -it web /drush/drush cc all`.

PHP
----
Installing from PHP 7.2-apache package.

Memcache
----
Installing memcached version 3.1.3.

Todo
----
- Add [docker-sync](http://docker-sync.io/)
