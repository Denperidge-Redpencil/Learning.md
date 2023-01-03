# Semantic.works

## Docker-Ember
### Install
A way to install [docker-ember](https://github.com/madnificent/docker-ember) without having to change your path, compliant with Linux directory standards (I think), and having it all neatly tucked away.
```bash
cd /usr/local/lib/
git clone https://github.com/madnificent/docker-ember.git
cd ../bin/
ln -s ../lib/docker-ember/bin/* .
```
Usually symbolic links are made using absolute paths, but in /usr/local/ it's not unheard of to use relative (npm, for example, does this).

### Uninstall
```bash
cd /usr/local/bin/
rm ed edi edl eds
cd ../lib/
rm -rf docker-ember/
```


## Kaleidos diagram recreation
```mermaid
graph TD
    Frontend===Identifier
    subgraph Identify & dispatch
        Identifier===Dispatcher
    end
    subgraph Core and shared
        Migrations
        subgraph Login
            Dispatcher===acm[ACM/IDM login]
            sink---acm
        end
        subgraph Resource
            Dispatcher---Cache
            Cache---cl-resources
        end
        Dispatcher---File
        subgraph Search
            Dispatcher---mu-search
            mu-search---el[(Elastic Search)]
        end
    end

    subgraph Custom services
        Dispatcher---range-file
        subgraph Access distribution
            meeting[Meeting distribution]
            userinfo[User info distribution]
        end
    end

    subgraph SEAS

        File o--o filesystem[(filesystem)]
        mu-search o--o filesystem
        range-file o--o filesystem

        acm===auth
        File---auth
        mu-search---auth
        cl-resources---auth
        meeting===auth
        userinfo===auth
        range-file---auth


        meeting-.-delta-notifier
        userinfo-.-delta-notifier
        cl-resources-.-delta-notifier
        mu-search-.-delta-notifier

        auth[mu-authorization]---Virtuoso[(Virtuoso)]
        Migrations===Virtuoso
        
        auth---delta-notifier
    end
```