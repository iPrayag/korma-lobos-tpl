# korma-lobos-tpl

A template integrating Korma and Lobos.

## Usage

Create a MySQL db and provide details in `src/korma_lobos_tpl/secret.clj` in the form of dynamic bindings of all the required names used in `lobos.config` and `korma-lobos-tpl.entities.connection`.

```
(ns korma-lobos-tpl.secret)
(def ^:dynamic *db-name* "tpl")
(def ^:dynamic *db-user* "root")
(def ^:dynamic *db-password* "mysql55")
(def ^:dynamic *db-host* "127.0.0.1")
(def ^:dynamic *db-port* 3306)
```



```bash
lein deps
lein repl
```

Once in the REPL:
```clojure
(use 'lobos.core 'lobos.connectivity 'lobos.migration 'lobos.config 'lobos.migrations)
(open-global sqldb)
(migrate)
(use 'korma-lobos-tpl.entities.users)
(create-new-user "Aberforth")
```


After the migration, check the database

```
mysql> use tpl;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> show tables;
+------------------+
| Tables_in_tpl    |
+------------------+
| lobos_migrations |
| users            |
+------------------+
2 rows in set (0.00 sec)


mysql> select * from users;
+-----------+
| username  |
+-----------+
| Aberforth |
+-----------+
1 row in set (0.00 sec)
```

## License

No Copyright.

Distributed under the Eclipse Public License, the same as Clojure.
