# Entry List
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; This is part of [managed list](/Plugins/List) plugin system.
</div>

Stores a copy of any entry that was added to it, and can be used in a variety of ways. 
See [managed_list](/Plugins/List/) how to use lists in general. 

### Configuration

```
entry_list: <NAME>
```

## Examples


### Digest replacement

```yaml
task:
  get-movies:
    priority: 1
    rss: ...
    accept_all: yes
    list_add:
      - entry_list: downloaded movies
    download: ...

  email-report:
    priority: 2
    entry_list: downloaded movies
    accept_all: yes
    notify:
      task:
        via:
          email: ...
```

First task `get-movies` will add all accepted entries to an `entry_list` with the name `downloaded movies`. It then later be used as an input itself in a `email-report` task. Effectively this can replace the [digest](/Plugins/digest) plugin.


### Search in entry list:

You can use `entry_list` as a [search](/Searches) plugin to use with [discover](/Plugins/discover):
```yaml
tasks:
  series_discover_task:
    series:
      - foo:
          begin: s01e01
    discover:
      release_estimations: ignore
      what:
        - next_series_episodes: yes
      from:
        - entry_list: series list
```

## Command line interface

Please see [commandline documentation](/CLI/entry-list)

## Entry List API
`entry_list` plugin has full JSON API support. See [API post](http://discuss.flexget.com/t/flexget-rest-api/) for details.