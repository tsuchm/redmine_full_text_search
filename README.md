# Full text search plugin

This plugin provides the following features:

* Fast and rich full text search to Redmine
* Display similar issues on an issue page

## Requirements

* [Mroonga](http://mroonga.org/) or
  [PGroonga](https://pgroonga.github.io/): RDBMS plugins for full text search.

If you're using MySQL or MariaDB, you need Mroonga 9.03 or later.

If you're using PostgreSQL, you need PGroonga 2.2.0 or later.

Mroonga and PGroonga uses Groonga as full text search engine. You need
Groonga 9.0.3 or later.

### Optional requirements

* ChupaText server: Text extractor server.

## How to use

### Install PGroonga or Mroonga

See [PGroonga document](https://pgroonga.github.io/install/)

See [Mroonga document](http://mroonga.org/docs/install.html)

### Install ChupaText server (optional)

You can choose one of them to install ChupaText:

1. Use [chupa-text-docker](https://github.com/ranguba/chupa-text-docker)
2. Use [chupa-text-vagrant](https://github.com/ranguba/chupa-text-vagrant)
3. Use [chupa-text-http-server](https://github.com/ranguba/chupa-text-http-server)

chupa-text-docker is recommended. See [chupa-text-docker
document](https://github.com/ranguba/chupa-text-docker/blob/master/README.md)
to install chupa-text-docker.

See [chupa-text-vagrant
document](https://github.com/ranguba/chupa-text-vagrant/blob/master/README.md)
to install chupa-text-vagrant.

chupa-text-http-server is a normal [Ruby on
Rails](https://rubyonrails.org/) application like Redmine itself. You
can deploy chupa-text-http-server as a normal Ruby on Rails
application.

### Install this plugin

```text
$ cd redmine
$ git clone https://github.com/clear-code/redmine_full_text_search.git plugins/full_text_search
$ RAILS_ENV=production bin/rails redmine:plugins:migrate
```

Restart Redmine.

**NOTE** for PGroonga:

If you use normal user for Redmine. You must run the following query
as a super user before run `RAILS_ENV=production bin/rails
redmine:plugins:migrate`:

```sql
CREATE EXTENSION IF NOT EXISTS pgroonga;
```

### Configure this plugin

Open https://YOUR_REDMINE_SERVER/settings/plugin/full_text_search and
configure items in the page. If you install ChupaText server, you must
configure "ChupaText server URL". If you install your ChupaText server
by chupa-text-docker or chupa-text-vagrant on the same host, it's
`http://127.0.0.1:20080/extraction.json`.

### Synchronize data

You need to create index for existing data. You need to run
`full_text_search:synchronize` task until no more synchronize target
data.

```text
$ cd redmine
$ RAILS_ENV=production bin/rails full_text_search:synchronize
$ RAILS_ENV=production bin/rails full_text_search:synchronize
$ RAILS_ENV=production bin/rails full_text_search:synchronize
...
```

## Authors

  * Kenji Okimoto

  * Sutou Kouhei `<kou@clear-code.com>`

  * Shimadzu Corporation

## License

The MIT License. See [LICENSE](LICENSE) for details.

### Exceptions

  * `asserts/stylesheets/fontawesome*/**/*`
    * Author: [@fontawesome](https://fontawesome.com/)
    * Fonts: SIL OFL 1.1 License
    * Codes: MIT License
    * See `asserts/stylesheets/fontawesome*/LICENSE.txt` for details

## Contributing

1. Fork it ( http://github.com/clear-code/redmine_full_text_search/fork )
1. Create your feature branch (`git checkout -b my-new-feature`)
1. Commit your changes (`git commit -am 'Add some feature'`)
1. Push to the branch (`git push origin my-new-feature`)
1. Create new Pull Request
