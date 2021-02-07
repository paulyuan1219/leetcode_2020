# Lumen5 Rendering Explained


```
(base) MacBook-Pro:docker weiyuan$ bash run_dev.sh 
Starting development cluster with image tag: latest
.env already exists - displaying...
# keep alphabetized per section when possible!
#
# for all Django containers
CELERY_PASSWORD=celery_password
CELERY_USER=celery_user
DB_HOST=pgbouncer-service
DB_PASSWORD=l5pgpass
DB_PORT=5432
DB_USER=lumen5
DEBUG=true
PYTHONUNBUFFERED=1

# rabbit
RABBITMQ_DEFAULT_PASS=l5rmqpass
RABBITMQ_DEFAULT_USER=l5user
RABBITMQ_HTTP_PASSWORD=http_password
RABBITMQ_HTTP_USERNAME=http_user

# raw postgres container (only accessible through pgbouncer, see below)
POSTGRES_PASSWORD=postgres
POSTGRES_USER=postgres

# pgbouncer config, "documented" at
# https://github.com/edoburu/docker-pgbouncer/blob/f274ab7e66c2ea43ac0b5b02fd15ab0ce8616b44/entrypoint.sh
# and https://pgbouncer.github.io/config.html
MAX_CLIENT_CONN=500
MAX_DB_CONNECTIONS=100
DEFAULT_POOL_SIZE=8
MIN_POOL_SIZE=4

# local API keys
GOOGLE_APPLICATION_CREDENTIALS=/var/certs/gcloud-dev-key.json
STRIPE_API_SECRET=sk_test_ZKedassHMbcSnR9wG8939PHc

# rendering
LUMEN5_CHROME_PORT=2623
LUMEN5_CHROME_WHITELIST=localhost
LUMEN5_CHROME_DISABLE_WHITELIST=true
LUMEN5_CHROME_DOWNLOAD_PATH=/Users/weiyuan/Documents/lumen5/rendering/docker/container-storage/chrome
LUMEN5_CHROME_PATH=
CHROME_SERVER_BASE_DIR=
CHROME_SERVER_BASE_DIR and LUMEN5_CHROME_PATH need to be set in order to render videos
ac8b76a1050e
eb6c79498a43
9186faf51ef7
ded967f00954
ce0933ca35c4
a62ff01c41ac
c5f40c175e90
d93af7e2292c
1878f7a3baba
2efd3c6daf2f
Pulling media-proxy        ... done
Pulling frontend           ... done
Pulling video-data-service ... done
Pulling db                 ... done
Pulling pgbouncer-service  ... done
Pulling elasticsearch-v3   ... done
Pulling web-service        ... done
Pulling rabbitmq-ha        ... done
Pulling base_worker        ... done
Pulling stripe-cli         ... done
Creating docker_video-data-service_1 ... done
Creating docker_frontend_1           ... done
Creating docker_elasticsearch-v3_1   ... done
Creating docker_rabbitmq-ha_1        ... done
Creating docker_stripe-cli_1         ... done
Creating docker_media-proxy_1        ... done
Creating docker_db_1                 ... done
Creating docker_pgbouncer-service_1  ... done
Creating docker_web-service_1        ... done
Creating docker_base_worker_1        ... done
Attaching to docker_video-data-service_1, docker_db_1, docker_stripe-cli_1, docker_elasticsearch-v3_1, docker_media-proxy_1, docker_rabbitmq-ha_1, docker_frontend_1, docker_pgbouncer-service_1, docker_base_worker_1, docker_web-service_1
db_1                  | 
db_1                  | PostgreSQL Database directory appears to contain a database; Skipping initialization
db_1                  | 
elasticsearch-v3_1    | File '/opt/plugins/ltr-1.1.0-es6.3.1.zip' already there; not retrieving.
elasticsearch-v3_1    | 
db_1                  | LOG:  database system was interrupted; last known up at 2020-05-08 23:01:14 UTC
pgbouncer-service_1   | grep: /etc/pgbouncer/userlist.txt: No such file or directory
db_1                  | LOG:  database system was not properly shut down; automatic recovery in progress
media-proxy_1         | Operations to perform:
media-proxy_1         |   Apply all migrations: admin, auth, contenttypes, sessions
media-proxy_1         | Running migrations:
pgbouncer-service_1   | Wrote authentication credentials to /etc/pgbouncer/userlist.txt
pgbouncer-service_1   | Create pgbouncer config in /etc/pgbouncer
stripe-cli_1          | Checking for new versions...
video-data-service_1  | VideoData Server listening on port 4000!
pgbouncer-service_1   | ################## Auto generated ##################
pgbouncer-service_1   | [databases]
pgbouncer-service_1   | * = host=db port=5432 user=lumen5
pgbouncer-service_1   | 
pgbouncer-service_1   | [pgbouncer]
pgbouncer-service_1   | listen_addr = 0.0.0.0
pgbouncer-service_1   | listen_port = 5432
pgbouncer-service_1   | unix_socket_dir =
pgbouncer-service_1   | user = postgres
pgbouncer-service_1   | auth_file = /etc/pgbouncer/userlist.txt
pgbouncer-service_1   | auth_type = md5
pgbouncer-service_1   | max_client_conn = 500
pgbouncer-service_1   | default_pool_size = 8
pgbouncer-service_1   | min_pool_size = 4
pgbouncer-service_1   | max_db_connections = 100
pgbouncer-service_1   | ignore_startup_parameters = extra_float_digits
pgbouncer-service_1   | 
pgbouncer-service_1   | # Log settings
pgbouncer-service_1   | admin_users = postgres
pgbouncer-service_1   | 
pgbouncer-service_1   | # Connection sanity checks, timeouts
pgbouncer-service_1   | 
pgbouncer-service_1   | # TLS settings
pgbouncer-service_1   | 
pgbouncer-service_1   | # Dangerous timeouts
pgbouncer-service_1   | ################## end file ##################
db_1                  | LOG:  redo starts at 0/22D4190
db_1                  | LOG:  invalid record length at 0/22D99F0: wanted 24, got 0
db_1                  | LOG:  redo done at 0/22D99C8
media-proxy_1         |   Applying contenttypes.0001_initial... OK
stripe-cli_1          | 
pgbouncer-service_1   | Starting /usr/bin/pgbouncer /etc/pgbouncer/pgbouncer.ini...
media-proxy_1         |   Applying auth.0001_initial... OK
media-proxy_1         |   Applying admin.0001_initial... OK
media-proxy_1         |   Applying admin.0002_logentry_remove_auto_add... OK
pgbouncer-service_1   | 2020-05-08 23:03:56.852 1 LOG file descriptor limit: 1048576 (H:1048576), max_client_conn: 500, max fds possible: 510
db_1                  | LOG:  last completed transaction was at log time 2020-05-08 23:02:53.103639+00
pgbouncer-service_1   | 2020-05-08 23:03:56.853 1 LOG listening on 0.0.0.0:5432
pgbouncer-service_1   | 2020-05-08 23:03:56.853 1 LOG process up: pgbouncer 1.9.0, libevent 2.1.8-stable (epoll), adns: udns 0.4, tls: LibreSSL 2.6.5
media-proxy_1         |   Applying admin.0003_logentry_add_action_flag_choices... OK
stripe-cli_1          | Getting ready...
db_1                  | LOG:  MultiXact member wraparound protections are now enabled
db_1                  | LOG:  database system is ready to accept connections
db_1                  | LOG:  autovacuum launcher started
media-proxy_1         |   Applying contenttypes.0002_remove_content_type_name... OK
stripe-cli_1          | Ready! Your webhook signing secret is whsec_vpNp3D1KO49WOVYhNTKOhoeWaQDub8NK (^C to quit)
media-proxy_1         |   Applying auth.0002_alter_permission_name_max_length... OK
media-proxy_1         |   Applying auth.0003_alter_user_email_max_length... OK
media-proxy_1         |   Applying auth.0004_alter_user_username_opts... OK
media-proxy_1         |   Applying auth.0005_alter_user_last_login_null... OK
media-proxy_1         |   Applying auth.0006_require_contenttypes_0002... OK
media-proxy_1         |   Applying auth.0007_alter_validators_add_error_messages... OK
media-proxy_1         |   Applying auth.0008_alter_user_username_max_length... OK
media-proxy_1         |   Applying auth.0009_alter_user_last_name_max_length... OK
media-proxy_1         |   Applying sessions.0001_initial... OK
media-proxy_1         | [2020-05-08 23:03:58 +0000] [10] [INFO] Starting gunicorn 19.9.0
media-proxy_1         | [2020-05-08 23:03:58 +0000] [10] [INFO] Listening at: http://0.0.0.0:7999 (10)
media-proxy_1         | [2020-05-08 23:03:58 +0000] [10] [INFO] Using worker: sync
media-proxy_1         | /usr/local/lib/python3.8/os.py:1023: RuntimeWarning: line buffering (buffering=1) isn't supported in binary mode, the default buffer size will be used
media-proxy_1         |   return io.open(fd, *args, **kwargs)
media-proxy_1         | [2020-05-08 23:03:58 +0000] [12] [INFO] Booting worker with pid: 12
elasticsearch-v3_1    | -> Downloading file:///opt/plugins/ltr-1.1.0-es6.3.1.zip
[=================================================] 100%?? 
rabbitmq-ha_1         | Waiting for pid file '/var/lib/rabbitmq/mnesia/rabbit@queue.pid' to appear
rabbitmq-ha_1         | pid is 10
rabbitmq-ha_1         | Waiting for erlang distribution on node 'rabbit@queue' while OS process '10' is running
elasticsearch-v3_1    | @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
elasticsearch-v3_1    | @     WARNING: plugin requires additional permissions     @
elasticsearch-v3_1    | @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
elasticsearch-v3_1    | * java.lang.RuntimePermission createClassLoader
elasticsearch-v3_1    | * org.elasticsearch.script.ClassPermission java.lang.Math
elasticsearch-v3_1    | * org.elasticsearch.script.ClassPermission java.lang.String
elasticsearch-v3_1    | * org.elasticsearch.script.ClassPermission org.apache.lucene.expressions.Expression
elasticsearch-v3_1    | * org.elasticsearch.script.ClassPermission org.apache.lucene.search.DoubleValues
elasticsearch-v3_1    | * org.elasticsearch.script.ClassPermission org.apache.lucene.util.MathUtil
elasticsearch-v3_1    | * org.elasticsearch.script.ClassPermission org.apache.lucene.util.SloppyMath
elasticsearch-v3_1    | See http://docs.oracle.com/javase/8/docs/technotes/guides/security/permissions.html
elasticsearch-v3_1    | for descriptions of what these permissions allow and the associated risks.
elasticsearch-v3_1    | -> Installed ltr
elasticsearch-v3_1    | OpenJDK 64-Bit Server VM warning: Option UseConcMarkSweepGC was deprecated in version 9.0 and will likely be removed in a future release.
rabbitmq-ha_1         | Waiting for applications 'rabbit_and_plugins' to start on node 'rabbit@queue'
stripe-cli_1          | 2020-05-08 23:04:03   --> payment_intent.succeeded [evt_1GgfEbHkF2NYgxfd1ZrDeCxs]
stripe-cli_1          | 2020-05-08 23:04:03            [ERROR] Failed to POST: Post http://web-service:8000/api/stripe/event/: dial tcp 172.18.0.11:8000: connect: connection refused
stripe-cli_1          | 
stripe-cli_1          | 2020-05-08 23:04:03   --> payment_intent.created [evt_1GgfEcHkF2NYgxfdJ0AfiDmZ]
stripe-cli_1          | 2020-05-08 23:04:03   --> charge.succeeded [evt_1GgfEcHkF2NYgxfd0X7Clt0s]
stripe-cli_1          | 2020-05-08 23:04:03            [ERROR] Failed to POST: Post http://web-service:8000/api/stripe/event/: dial tcp 172.18.0.11:8000: connect: connection refused
stripe-cli_1          | 
stripe-cli_1          | 2020-05-08 23:04:03            [ERROR] Failed to POST: Post http://web-service:8000/api/stripe/event/: dial tcp 172.18.0.11:8000: connect: connection refused
stripe-cli_1          | 
stripe-cli_1          | 2020-05-08 23:04:03   --> invoice.payment_succeeded [evt_1GgfEcHkF2NYgxfdqfzb0XTH]
stripe-cli_1          | 2020-05-08 23:04:03            [ERROR] Failed to POST: Post http://web-service:8000/api/stripe/event/: dial tcp 172.18.0.11:8000: connect: connection refused
stripe-cli_1          | 
stripe-cli_1          | 2020-05-08 23:04:03   --> invoice.updated [evt_1GgfEcHkF2NYgxfdGHWiwjAm]
stripe-cli_1          | 2020-05-08 23:04:03            [ERROR] Failed to POST: Post http://web-service:8000/api/stripe/event/: dial tcp 172.18.0.11:8000: connect: connection refused
stripe-cli_1          | 
stripe-cli_1          | 2020-05-08 23:04:03   --> invoice.finalized [evt_1GgfEcHkF2NYgxfd64ayvjnm]
stripe-cli_1          | 2020-05-08 23:04:03            [ERROR] Failed to POST: Post http://web-service:8000/api/stripe/event/: dial tcp 172.18.0.11:8000: connect: connection refused
stripe-cli_1          | 
elasticsearch-v3_1    | [2020-05-08T23:04:03,551][INFO ][o.e.n.Node               ] [es-node-0] initializing ...
elasticsearch-v3_1    | [2020-05-08T23:04:03,636][INFO ][o.e.e.NodeEnvironment    ] [es-node-0] using [1] data paths, mounts [[/usr/share/elasticsearch/data (/dev/sda1)]], net usable_space [79.5gb], net total_space [100.3gb], types [ext4]
elasticsearch-v3_1    | [2020-05-08T23:04:03,637][INFO ][o.e.e.NodeEnvironment    ] [es-node-0] heap size [494.9mb], compressed ordinary object pointers [true]
elasticsearch-v3_1    | [2020-05-08T23:04:03,679][INFO ][o.e.n.Node               ] [es-node-0] node name [es-node-0], node ID [fxkwWM38QLe_z_iUWnSs5Q]
elasticsearch-v3_1    | [2020-05-08T23:04:03,680][INFO ][o.e.n.Node               ] [es-node-0] version[6.3.1], pid[84], build[default/tar/eb782d0/2018-06-29T21:59:26.107521Z], OS[Linux/4.19.76-linuxkit/amd64], JVM[Oracle Corporation/OpenJDK 64-Bit Server VM/10.0.1/10.0.1+10]
elasticsearch-v3_1    | [2020-05-08T23:04:03,680][INFO ][o.e.n.Node               ] [es-node-0] JVM arguments [-Xms1g, -Xmx1g, -XX:+UseConcMarkSweepGC, -XX:CMSInitiatingOccupancyFraction=75, -XX:+UseCMSInitiatingOccupancyOnly, -XX:+AlwaysPreTouch, -Xss1m, -Djava.awt.headless=true, -Dfile.encoding=UTF-8, -Djna.nosys=true, -XX:-OmitStackTraceInFastThrow, -Dio.netty.noUnsafe=true, -Dio.netty.noKeySetOptimization=true, -Dio.netty.recycler.maxCapacityPerThread=0, -Dlog4j.shutdownHookEnabled=false, -Dlog4j2.disable.jmx=true, -Djava.io.tmpdir=/tmp/elasticsearch.RZ2GiLet, -XX:+HeapDumpOnOutOfMemoryError, -XX:HeapDumpPath=data, -XX:ErrorFile=logs/hs_err_pid%p.log, -Xlog:gc*,gc+age=trace,safepoint:file=logs/gc.log:utctime,pid,tags:filecount=32,filesize=64m, -Djava.locale.providers=COMPAT, -Des.cgroups.hierarchy.override=/, -Xms512m, -Xmx512m, -Des.path.home=/usr/share/elasticsearch, -Des.path.conf=/usr/share/elasticsearch/config, -Des.distribution.flavor=default, -Des.distribution.type=tar]
web-service_1         | [2020-05-08 23:04:06 +0000] [6] [media.apps] [INFO] setting up post_save, post_update signal handlers...
web-service_1         | [2020-05-08 23:04:06 +0000] [6] [media.apps] [INFO] setting up pre_delete, post_delete signal handlers...
web-service_1         | [2020-05-08 23:04:06 +0000] [6] [retry_dbconn] [DEBUG] retry_dbconn: monkeypatching BaseDatabaseWrapper
elasticsearch-v3_1    | [2020-05-08T23:04:06,612][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [aggs-matrix-stats]
elasticsearch-v3_1    | [2020-05-08T23:04:06,613][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [analysis-common]
elasticsearch-v3_1    | [2020-05-08T23:04:06,613][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [ingest-common]
elasticsearch-v3_1    | [2020-05-08T23:04:06,615][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [lang-expression]
elasticsearch-v3_1    | [2020-05-08T23:04:06,615][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [lang-mustache]
elasticsearch-v3_1    | [2020-05-08T23:04:06,616][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [lang-painless]
elasticsearch-v3_1    | [2020-05-08T23:04:06,616][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [mapper-extras]
elasticsearch-v3_1    | [2020-05-08T23:04:06,617][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [parent-join]
elasticsearch-v3_1    | [2020-05-08T23:04:06,618][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [percolator]
elasticsearch-v3_1    | [2020-05-08T23:04:06,618][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [rank-eval]
elasticsearch-v3_1    | [2020-05-08T23:04:06,620][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [reindex]
elasticsearch-v3_1    | [2020-05-08T23:04:06,620][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [repository-url]
elasticsearch-v3_1    | [2020-05-08T23:04:06,621][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [transport-netty4]
elasticsearch-v3_1    | [2020-05-08T23:04:06,622][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [tribe]
elasticsearch-v3_1    | [2020-05-08T23:04:06,622][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-core]
elasticsearch-v3_1    | [2020-05-08T23:04:06,623][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-deprecation]
elasticsearch-v3_1    | [2020-05-08T23:04:06,623][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-graph]
elasticsearch-v3_1    | [2020-05-08T23:04:06,625][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-logstash]
elasticsearch-v3_1    | [2020-05-08T23:04:06,625][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-ml]
elasticsearch-v3_1    | [2020-05-08T23:04:06,626][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-monitoring]
elasticsearch-v3_1    | [2020-05-08T23:04:06,627][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-rollup]
elasticsearch-v3_1    | [2020-05-08T23:04:06,627][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-security]
elasticsearch-v3_1    | [2020-05-08T23:04:06,628][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-sql]
elasticsearch-v3_1    | [2020-05-08T23:04:06,628][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-upgrade]
elasticsearch-v3_1    | [2020-05-08T23:04:06,629][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-watcher]
elasticsearch-v3_1    | [2020-05-08T23:04:06,630][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded plugin [ingest-geoip]
elasticsearch-v3_1    | [2020-05-08T23:04:06,631][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded plugin [ingest-user-agent]
elasticsearch-v3_1    | [2020-05-08T23:04:06,632][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded plugin [ltr]
web-service_1         | [2020-05-08 23:04:08 +0000] [6] [wait_for_elasticsearch] [WARNING] waiting for Elasticsearch...
rabbitmq-ha_1         | 2020-05-08 23:04:09.101 [info] <0.9.0> Feature flags: list of feature flags found:
rabbitmq-ha_1         | 2020-05-08 23:04:09.101 [info] <0.9.0> Feature flags: feature flag states written to disk: yes
elasticsearch-v3_1    | [2020-05-08T23:04:09,169][WARN ][o.e.d.c.s.Settings       ] [http.enabled] setting was deprecated in Elasticsearch and will be removed in a future release! See the breaking changes documentation for the next major version.
web-service_1         | [2020-05-08 23:04:09 +0000] [6] [wait_for_elasticsearch] [WARNING] waiting for Elasticsearch...
rabbitmq-ha_1         | 2020-05-08 23:04:09.274 [info] <0.337.0> 
rabbitmq-ha_1         |  Starting RabbitMQ 3.7.26 on Erlang 22.3.3
rabbitmq-ha_1         |  Copyright (c) 2007-2020 Pivotal Software, Inc.
rabbitmq-ha_1         |  Licensed under the MPL.  See https://www.rabbitmq.com/
rabbitmq-ha_1         | 
rabbitmq-ha_1         |   ##  ##
rabbitmq-ha_1         |   ##  ##      RabbitMQ 3.7.26. Copyright (c) 2007-2020 Pivotal Software, Inc.
rabbitmq-ha_1         |   ##########  Licensed under the MPL.  See https://www.rabbitmq.com/
rabbitmq-ha_1         |   ######  ##
rabbitmq-ha_1         |   ##########  Logs: <stdout>
rabbitmq-ha_1         | 
rabbitmq-ha_1         |               Starting broker...
rabbitmq-ha_1         | 2020-05-08 23:04:09.275 [info] <0.337.0> 
rabbitmq-ha_1         |  node           : rabbit@queue
rabbitmq-ha_1         |  home dir       : /var/lib/rabbitmq
rabbitmq-ha_1         |  config file(s) : (none)
rabbitmq-ha_1         |  cookie hash    : IdYqRLoCMQQoNmik7zqkNA==
rabbitmq-ha_1         |  log(s)         : <stdout>
rabbitmq-ha_1         |  database dir   : /var/lib/rabbitmq/mnesia/rabbit@queue
rabbitmq-ha_1         | 2020-05-08 23:04:09.294 [info] <0.337.0> Running boot step pre_boot defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.294 [info] <0.337.0> Running boot step rabbit_core_metrics defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.295 [info] <0.337.0> Running boot step rabbit_alarm defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.312 [info] <0.362.0> Memory high watermark set to 3185 MiB (3340314214 bytes) of 7963 MiB (8350785536 bytes) total
rabbitmq-ha_1         | 2020-05-08 23:04:09.324 [info] <0.388.0> Enabling free disk space monitoring
rabbitmq-ha_1         | 2020-05-08 23:04:09.325 [info] <0.388.0> Disk free limit set to 50MB
rabbitmq-ha_1         | 2020-05-08 23:04:09.331 [info] <0.337.0> Running boot step code_server_cache defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.331 [info] <0.337.0> Running boot step file_handle_cache defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.332 [info] <0.396.0> Limiting to approx 1048476 file handles (943626 sockets)
rabbitmq-ha_1         | 2020-05-08 23:04:09.333 [info] <0.397.0> FHC read buffering:  OFF
rabbitmq-ha_1         | 2020-05-08 23:04:09.333 [info] <0.397.0> FHC write buffering: ON
rabbitmq-ha_1         | 2020-05-08 23:04:09.334 [info] <0.337.0> Running boot step worker_pool defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.335 [info] <0.342.0> Will use 6 processes for default worker pool
rabbitmq-ha_1         | 2020-05-08 23:04:09.335 [info] <0.342.0> Starting worker pool 'worker_pool' with 6 processes in it
rabbitmq-ha_1         | 2020-05-08 23:04:09.336 [info] <0.337.0> Running boot step database defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.346 [info] <0.337.0> Waiting for Mnesia tables for 30000 ms, 9 retries left
rabbitmq-ha_1         | 2020-05-08 23:04:09.391 [info] <0.337.0> Waiting for Mnesia tables for 30000 ms, 9 retries left
rabbitmq-ha_1         | 2020-05-08 23:04:09.391 [info] <0.337.0> Peer discovery backend rabbit_peer_discovery_classic_config does not support registration, skipping registration.
rabbitmq-ha_1         | 2020-05-08 23:04:09.392 [info] <0.337.0> Running boot step database_sync defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.393 [info] <0.337.0> Running boot step feature_flags defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.393 [info] <0.337.0> Running boot step codec_correctness_check defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.393 [info] <0.337.0> Running boot step external_infrastructure defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.394 [info] <0.337.0> Running boot step rabbit_registry defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.394 [info] <0.337.0> Running boot step rabbit_auth_mechanism_cr_demo defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.395 [info] <0.337.0> Running boot step rabbit_queue_location_random defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.396 [info] <0.337.0> Running boot step rabbit_event defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.396 [info] <0.337.0> Running boot step rabbit_auth_mechanism_amqplain defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.397 [info] <0.337.0> Running boot step rabbit_auth_mechanism_plain defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.397 [info] <0.337.0> Running boot step rabbit_exchange_type_direct defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.398 [info] <0.337.0> Running boot step rabbit_exchange_type_fanout defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.398 [info] <0.337.0> Running boot step rabbit_exchange_type_headers defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.399 [info] <0.337.0> Running boot step rabbit_exchange_type_topic defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.399 [info] <0.337.0> Running boot step rabbit_mirror_queue_mode_all defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.400 [info] <0.337.0> Running boot step rabbit_mirror_queue_mode_exactly defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.400 [info] <0.337.0> Running boot step rabbit_mirror_queue_mode_nodes defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.401 [info] <0.337.0> Running boot step rabbit_priority_queue defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.401 [info] <0.337.0> Priority queues enabled, real BQ is rabbit_variable_queue
rabbitmq-ha_1         | 2020-05-08 23:04:09.402 [info] <0.337.0> Running boot step rabbit_queue_location_client_local defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.402 [info] <0.337.0> Running boot step rabbit_queue_location_min_masters defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.402 [info] <0.337.0> Running boot step kernel_ready defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.402 [info] <0.337.0> Running boot step rabbit_sysmon_minder defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.403 [info] <0.337.0> Running boot step rabbit_epmd_monitor defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.414 [info] <0.421.0> epmd monitor knows us, inter-node communication (distribution) port: 25672
rabbitmq-ha_1         | 2020-05-08 23:04:09.414 [info] <0.337.0> Running boot step guid_generator defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.420 [info] <0.337.0> Running boot step rabbit_node_monitor defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.420 [info] <0.427.0> Starting rabbit_node_monitor
rabbitmq-ha_1         | 2020-05-08 23:04:09.421 [info] <0.337.0> Running boot step delegate_sup defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.423 [info] <0.337.0> Running boot step rabbit_memory_monitor defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.424 [info] <0.337.0> Running boot step core_initialized defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.424 [info] <0.337.0> Running boot step upgrade_queues defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.462 [info] <0.337.0> Running boot step rabbit_connection_tracking defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.463 [info] <0.337.0> Running boot step rabbit_connection_tracking_handler defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.463 [info] <0.337.0> Running boot step rabbit_exchange_parameters defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.464 [info] <0.337.0> Running boot step rabbit_mirror_queue_misc defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.465 [info] <0.337.0> Running boot step rabbit_policies defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.467 [info] <0.337.0> Running boot step rabbit_policy defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.467 [info] <0.337.0> Running boot step rabbit_queue_location_validator defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.468 [info] <0.337.0> Running boot step rabbit_vhost_limit defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.469 [info] <0.337.0> Running boot step rabbit_mgmt_reset_handler defined by app rabbitmq_management
rabbitmq-ha_1         | 2020-05-08 23:04:09.469 [info] <0.337.0> Running boot step rabbit_mgmt_db_handler defined by app rabbitmq_management_agent
rabbitmq-ha_1         | 2020-05-08 23:04:09.470 [info] <0.337.0> Management plugin: using rates mode 'basic'
rabbitmq-ha_1         | 2020-05-08 23:04:09.471 [info] <0.337.0> Running boot step recovery defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.475 [info] <0.466.0> Making sure data directory '/var/lib/rabbitmq/mnesia/rabbit@queue/msg_stores/vhosts/628WB79CIFDYO9LJI6DKMI09L' for vhost '/' exists
rabbitmq-ha_1         | 2020-05-08 23:04:09.480 [info] <0.466.0> Starting message stores for vhost '/'
rabbitmq-ha_1         | 2020-05-08 23:04:09.481 [info] <0.470.0> Message store "628WB79CIFDYO9LJI6DKMI09L/msg_store_transient": using rabbit_msg_store_ets_index to provide index
rabbitmq-ha_1         | 2020-05-08 23:04:09.484 [info] <0.466.0> Started message store of type transient for vhost '/'
rabbitmq-ha_1         | 2020-05-08 23:04:09.485 [info] <0.473.0> Message store "628WB79CIFDYO9LJI6DKMI09L/msg_store_persistent": using rabbit_msg_store_ets_index to provide index
rabbitmq-ha_1         | 2020-05-08 23:04:09.486 [warning] <0.473.0> Message store "628WB79CIFDYO9LJI6DKMI09L/msg_store_persistent": rebuilding indices from scratch
rabbitmq-ha_1         | 2020-05-08 23:04:09.495 [info] <0.466.0> Started message store of type persistent for vhost '/'
rabbitmq-ha_1         | 2020-05-08 23:04:09.520 [info] <0.337.0> Running boot step load_definitions defined by app rabbitmq_management
rabbitmq-ha_1         | 2020-05-08 23:04:09.520 [info] <0.337.0> Running boot step empty_db_check defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.520 [info] <0.337.0> Running boot step rabbit_looking_glass defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.521 [info] <0.337.0> Running boot step rabbit_core_metrics_gc defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.522 [info] <0.337.0> Running boot step background_gc defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.523 [info] <0.337.0> Running boot step connection_tracking defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.524 [info] <0.337.0> Setting up a table for connection tracking on this node: tracked_connection_on_node_rabbit@queue
rabbitmq-ha_1         | 2020-05-08 23:04:09.525 [info] <0.337.0> Setting up a table for per-vhost connection counting on this node: tracked_connection_per_vhost_on_node_rabbit@queue
rabbitmq-ha_1         | 2020-05-08 23:04:09.526 [info] <0.337.0> Running boot step routing_ready defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.526 [info] <0.337.0> Running boot step pre_flight defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.526 [info] <0.337.0> Running boot step notify_cluster defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.527 [info] <0.337.0> Running boot step networking defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.533 [info] <0.531.0> started TCP listener on [::]:5672
rabbitmq-ha_1         | 2020-05-08 23:04:09.534 [info] <0.337.0> Running boot step cluster_name defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.535 [info] <0.337.0> Running boot step direct_client defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.535 [info] <0.337.0> Running boot step os_signal_handler defined by app rabbit
rabbitmq-ha_1         | 2020-05-08 23:04:09.536 [info] <0.533.0> Swapping OS signal event handler (erl_signal_server) for our own
rabbitmq-ha_1         | 2020-05-08 23:04:09.594 [info] <0.588.0> Management plugin: HTTP (non-TLS) listener started on port 15672
rabbitmq-ha_1         | 2020-05-08 23:04:09.594 [info] <0.694.0> Statistics database started.
rabbitmq-ha_1         | 2020-05-08 23:04:09.594 [info] <0.693.0> Starting worker pool 'management_worker_pool' with 3 processes in it
rabbitmq-ha_1         |  completed with 3 plugins.
rabbitmq-ha_1         | 2020-05-08 23:04:09.782 [info] <0.9.0> Server startup complete; 3 plugins started.
rabbitmq-ha_1         |  * rabbitmq_management
rabbitmq-ha_1         |  * rabbitmq_web_dispatch
rabbitmq-ha_1         |  * rabbitmq_management_agent
rabbitmq-ha_1         | Applications 'rabbit_and_plugins' are running on node 'rabbit@queue'
web-service_1         | [2020-05-08 23:04:10 +0000] [6] [wait_for_elasticsearch] [WARNING] waiting for Elasticsearch...
elasticsearch-v3_1    | [2020-05-08T23:04:10,664][INFO ][o.e.d.DiscoveryModule    ] [es-node-0] using discovery type [single-node]
web-service_1         | [2020-05-08 23:04:11 +0000] [6] [wait_for_elasticsearch] [WARNING] waiting for Elasticsearch...
rabbitmq-ha_1         | Adding user "l5user" ...
rabbitmq-ha_1         | 2020-05-08 23:04:11.459 [info] <0.711.0> Creating user 'l5user'
rabbitmq-ha_1         | Error:
rabbitmq-ha_1         | User "l5user" already exists
elasticsearch-v3_1    | [2020-05-08T23:04:11,609][INFO ][o.e.n.Node               ] [es-node-0] initialized
elasticsearch-v3_1    | [2020-05-08T23:04:11,609][INFO ][o.e.n.Node               ] [es-node-0] starting ...
elasticsearch-v3_1    | [2020-05-08T23:04:11,844][INFO ][o.e.t.TransportService   ] [es-node-0] publish_address {172.18.0.5:9300}, bound_addresses {0.0.0.0:9300}
elasticsearch-v3_1    | [2020-05-08T23:04:11,981][INFO ][o.e.h.n.Netty4HttpServerTransport] [es-node-0] publish_address {172.18.0.5:9200}, bound_addresses {0.0.0.0:9200}
elasticsearch-v3_1    | [2020-05-08T23:04:11,981][INFO ][o.e.n.Node               ] [es-node-0] started
web-service_1         | [2020-05-08 23:04:12 +0000] [6] [wait_for_elasticsearch] [WARNING] waiting for Elasticsearch...
rabbitmq-ha_1         | Setting permissions for user "l5user" in vhost "/" ...
rabbitmq-ha_1         | 2020-05-08 23:04:12.888 [info] <0.718.0> Setting permissions for 'l5user' in '/' to '.*', '.*', '.*'
elasticsearch-v3_1    | [2020-05-08T23:04:13,094][INFO ][o.e.l.LicenseService     ] [es-node-0] license [3f4e27ce-16dc-46e7-8e1f-5933698005d8] mode [basic] - valid
elasticsearch-v3_1    | [2020-05-08T23:04:13,104][INFO ][o.e.g.GatewayService     ] [es-node-0] recovered [12] indices into cluster_state
web-service_1         | [2020-05-08 23:04:13 +0000] [6] [wait_for_elasticsearch] [WARNING] waiting for Elasticsearch...
elasticsearch-v3_1    | [2020-05-08T23:04:14,234][INFO ][o.e.c.r.a.AllocationService] [es-node-0] Cluster health status changed from [RED] to [YELLOW] (reason: [shards started [[audio_31a7][0]] ...]).
rabbitmq-ha_1         | Adding user "celery_user" ...
rabbitmq-ha_1         | 2020-05-08 23:04:14.304 [info] <0.725.0> Creating user 'celery_user'
rabbitmq-ha_1         | Error:
rabbitmq-ha_1         | User "celery_user" already exists
web-service_1         | [2020-05-08 23:04:14 +0000] [6] [wait_for_elasticsearch] [WARNING] waiting for Elasticsearch...
rabbitmq-ha_1         | Setting permissions for user "celery_user" in vhost "/" ...
rabbitmq-ha_1         | 2020-05-08 23:04:15.315 [info] <0.732.0> Setting permissions for 'celery_user' in '/' to '.*', '.*', '.*'
rabbitmq-ha_1         | Adding user "http_user" ...
rabbitmq-ha_1         | 2020-05-08 23:04:16.298 [info] <0.739.0> Creating user 'http_user'
rabbitmq-ha_1         | Error:
rabbitmq-ha_1         | User "http_user" already exists
rabbitmq-ha_1         | Setting permissions for user "http_user" in vhost "/" ...
rabbitmq-ha_1         | 2020-05-08 23:04:17.215 [info] <0.746.0> Setting permissions for 'http_user' in '/' to '', '', '.*'
rabbitmq-ha_1         | 2020-05-08 23:04:18.342 [info] <0.753.0> Setting user tags for user 'http_user' to [management]
rabbitmq-ha_1         | Setting tags for user "http_user" to [management] ...
rabbitmq-ha_1         | *** RabbitMQ user accounts ('l5user', 'celery_user' and 'http_user') setup. ***
frontend_1            | npm WARN react-dom@16.13.1 requires a peer of react@^16.13.1 but none is installed. You must install peer dependencies yourself.
frontend_1            | npm WARN acorn-jsx@5.0.1 requires a peer of acorn@^6.0.0 but none is installed. You must install peer dependencies yourself.
frontend_1            | npm WARN babel-eslint@11.0.0-beta.2 requires a peer of eslint@>= 6.0.0 but none is installed. You must install peer dependencies yourself.
frontend_1            | npm WARN chai-immutable@1.6.0 requires a peer of chai@>= 2.0.0 < 4 but none is installed. You must install peer dependencies yourself.
frontend_1            | npm WARN karma-requirejs@1.1.0 requires a peer of requirejs@^2.1.0 but none is installed. You must install peer dependencies yourself.
frontend_1            | npm WARN The package identity-obj-proxy is included as both a dev and production dependency.
frontend_1            | npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@2.1.3 (node_modules/jest-haste-map/node_modules/fsevents):
frontend_1            | npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
frontend_1            | npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@2.1.2 (node_modules/karma/node_modules/fsevents):
frontend_1            | npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.2: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
frontend_1            | npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@2.1.3 (node_modules/mocha/node_modules/fsevents):
frontend_1            | npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
frontend_1            | npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@2.1.3 (node_modules/babel-jest/node_modules/fsevents):
frontend_1            | npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
frontend_1            | 
frontend_1            | audited 279162 packages in 22.929s
web-service_1         | [2020-05-08 23:04:21 +0000] [89] [media.apps] [INFO] setting up post_save, post_update signal handlers...
web-service_1         | [2020-05-08 23:04:21 +0000] [89] [media.apps] [INFO] setting up pre_delete, post_delete signal handlers...
web-service_1         | [2020-05-08 23:04:21 +0000] [89] [retry_dbconn] [DEBUG] retry_dbconn: monkeypatching BaseDatabaseWrapper
frontend_1            | 
frontend_1            | 57 packages are looking for funding
frontend_1            |   run `npm fund` for details
frontend_1            | 
frontend_1            | found 9631 vulnerabilities (7898 low, 9 moderate, 1724 high)
frontend_1            |   run `npm audit fix` to fix them, or `npm audit` for details
frontend_1            | 
frontend_1            | > rendering@ server /opt/app
frontend_1            | > webpack-dev-server --config webpack.config.dev.js
frontend_1            | 
base_worker_1         | [2020-05-08 23:04:24 +0000] [7] [media.apps] [INFO] setting up post_save, post_update signal handlers...
base_worker_1         | [2020-05-08 23:04:24 +0000] [7] [media.apps] [INFO] setting up pre_delete, post_delete signal handlers...
base_worker_1         | [2020-05-08 23:04:24 +0000] [7] [retry_dbconn] [DEBUG] retry_dbconn: monkeypatching BaseDatabaseWrapper
frontend_1            | ℹ ｢wds｣: Project is running at http://0.0.0.0:3000/
frontend_1            | ℹ ｢wds｣: webpack output is served from http://localhost:3000/frontend/bundles/
frontend_1            | ℹ ｢wds｣: Content not from webpack is served from /opt/app
frontend_1            | ℹ ｢wds｣: 404s will fallback to /index.html
pgbouncer-service_1   | 2020-05-08 23:04:25.452 1 LOG C-0x556cc5259cf0: (nodb)/(nouser)@172.18.0.11:40730 registered new auto-database: db=lumen5
pgbouncer-service_1   | 2020-05-08 23:04:25.452 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40730 login attempt: db=lumen5 user=lumen5 tls=no
pgbouncer-service_1   | 2020-05-08 23:04:25.453 1 LOG S-0x556cc52aa330: lumen5/lumen5@172.18.0.3:5432 new connection to server (from 172.18.0.9:46502)
web-service_1         | Operations to perform:
web-service_1         |   Apply all migrations: admin, appsumo, article, auth, authtoken, billing, contenttypes, django_celery_results, media, newspaper, search, sessions, social_django, user_events, vision, web
base_worker_1         | [2020-05-08 23:04:25 +0000] [7] [celery.bootsteps] [DEBUG] | Worker: Preparing bootsteps.
base_worker_1         | [2020-05-08 23:04:25 +0000] [7] [celery.bootsteps] [DEBUG] | Worker: Building graph...
base_worker_1         | [2020-05-08 23:04:25 +0000] [7] [celery.bootsteps] [DEBUG] | Worker: New boot order: {Beat, Timer, Hub, Pool, Autoscaler, StateDB, Consumer}
base_worker_1         | [2020-05-08 23:04:25 +0000] [7] [celery.bootsteps] [DEBUG] | Consumer: Preparing bootsteps.
base_worker_1         | [2020-05-08 23:04:25 +0000] [7] [celery.bootsteps] [DEBUG] | Consumer: Building graph...
base_worker_1         | [2020-05-08 23:04:25 +0000] [7] [celery.bootsteps] [DEBUG] | Consumer: New boot order: {Connection, Agent, Events, Mingle, Gossip, Tasks, Control, Heart, event loop}
base_worker_1         |  
base_worker_1         |  -------------- celery@ba7a2a4bc629 v4.1.1 (latentcall)
base_worker_1         | ---- **** ----- 
base_worker_1         | --- * ***  * -- Linux-4.19.76-linuxkit-x86_64-with-debian-9.11 2020-05-08 23:04:25
base_worker_1         | -- * - **** --- 
base_worker_1         | - ** ---------- [config]
base_worker_1         | - ** ---------- .> app:         web:0x7fd4cf4ec550
base_worker_1         | - ** ---------- .> transport:   amqp://celery_user:**@rabbitmq-ha:5672//
base_worker_1         | - ** ---------- .> results:     
base_worker_1         | - *** --- * --- .> concurrency: 6 (prefork)
base_worker_1         | -- ******* ---- .> task events: OFF (enable -E to monitor tasks in this worker)
base_worker_1         | --- ***** ----- 
base_worker_1         |  -------------- [queues]
base_worker_1         |                 .> default          exchange=(direct) key=task.#
base_worker_1         |                 .> media_detections exchange=(direct) key=media_detections.#
base_worker_1         |                 .> user_blocking_tasks exchange=(direct) key=user_blocking_task.#
base_worker_1         |                 .> video_template_tasks exchange=(direct) key=video_template_task.#
base_worker_1         | 
base_worker_1         | [2020-05-08 23:04:25 +0000] [7] [celery.bootsteps] [DEBUG] | Worker: Starting Hub
base_worker_1         | [2020-05-08 23:04:25 +0000] [7] [celery.bootsteps] [DEBUG] ^-- substep ok
base_worker_1         | [2020-05-08 23:04:25 +0000] [7] [celery.bootsteps] [DEBUG] | Worker: Starting Pool
pgbouncer-service_1   | 2020-05-08 23:04:25.628 1 LOG S-0x556cc52aa4c0: lumen5/lumen5@172.18.0.3:5432 new connection to server (from 172.18.0.9:46504)
web-service_1         | Running migrations:
web-service_1         |   No migrations to apply.
pgbouncer-service_1   | 2020-05-08 23:04:25.962 1 LOG S-0x556cc52aa650: lumen5/lumen5@172.18.0.3:5432 new connection to server (from 172.18.0.9:46506)
pgbouncer-service_1   | 2020-05-08 23:04:26.254 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40730 closing because: client close request (age=0)
base_worker_1         | [2020-05-08 23:04:26 +0000] [7] [celery.bootsteps] [DEBUG] ^-- substep ok
base_worker_1         | [2020-05-08 23:04:26 +0000] [7] [celery.bootsteps] [DEBUG] | Worker: Starting Consumer
base_worker_1         | [2020-05-08 23:04:26 +0000] [7] [celery.bootsteps] [DEBUG] | Consumer: Starting Connection
rabbitmq-ha_1         | 2020-05-08 23:04:26.585 [info] <0.757.0> accepting AMQP connection <0.757.0> (172.18.0.10:34418 -> 172.18.0.7:5672)
base_worker_1         | [2020-05-08 23:04:26 +0000] [7] [amqp] [DEBUG] Start from server, version: 0.9, properties: {'cluster_name': 'rabbit@queue', 'platform': 'Erlang/OTP 22.3.3', 'copyright': 'Copyright (c) 2007-2020 Pivotal Software, Inc.', 'information': 'Licensed under the MPL.  See https://www.rabbitmq.com/', 'capabilities': {'authentication_failure_close': True, 'per_consumer_qos': True, 'direct_reply_to': True, 'exchange_exchange_bindings': True, 'connection.blocked': True, 'consumer_priorities': True, 'publisher_confirms': True, 'consumer_cancel_notify': True, 'basic.nack': True}, 'version': '3.7.26', 'product': 'RabbitMQ'}, mechanisms: [b'AMQPLAIN', b'PLAIN'], locales: ['en_US']
rabbitmq-ha_1         | 2020-05-08 23:04:26.591 [info] <0.757.0> connection <0.757.0> (172.18.0.10:34418 -> 172.18.0.7:5672): user 'celery_user' authenticated and granted access to vhost '/'
base_worker_1         | [2020-05-08 23:04:26 +0000] [7] [celery.worker.consumer.connection] [INFO] Connected to amqp://celery_user:**@rabbitmq-ha:5672//
base_worker_1         | [2020-05-08 23:04:26 +0000] [7] [celery.bootsteps] [DEBUG] ^-- substep ok
base_worker_1         | [2020-05-08 23:04:26 +0000] [7] [celery.bootsteps] [DEBUG] | Consumer: Starting Events
rabbitmq-ha_1         | 2020-05-08 23:04:26.604 [info] <0.764.0> accepting AMQP connection <0.764.0> (172.18.0.10:34420 -> 172.18.0.7:5672)
base_worker_1         | [2020-05-08 23:04:26 +0000] [7] [amqp] [DEBUG] Start from server, version: 0.9, properties: {'cluster_name': 'rabbit@queue', 'platform': 'Erlang/OTP 22.3.3', 'copyright': 'Copyright (c) 2007-2020 Pivotal Software, Inc.', 'information': 'Licensed under the MPL.  See https://www.rabbitmq.com/', 'capabilities': {'authentication_failure_close': True, 'per_consumer_qos': True, 'direct_reply_to': True, 'exchange_exchange_bindings': True, 'connection.blocked': True, 'consumer_priorities': True, 'publisher_confirms': True, 'consumer_cancel_notify': True, 'basic.nack': True}, 'version': '3.7.26', 'product': 'RabbitMQ'}, mechanisms: [b'AMQPLAIN', b'PLAIN'], locales: ['en_US']
rabbitmq-ha_1         | 2020-05-08 23:04:26.607 [info] <0.764.0> connection <0.764.0> (172.18.0.10:34420 -> 172.18.0.7:5672): user 'celery_user' authenticated and granted access to vhost '/'
base_worker_1         | [2020-05-08 23:04:26 +0000] [7] [celery.bootsteps] [DEBUG] ^-- substep ok
base_worker_1         | [2020-05-08 23:04:26 +0000] [7] [celery.bootsteps] [DEBUG] | Consumer: Starting Mingle
base_worker_1         | [2020-05-08 23:04:26 +0000] [7] [celery.worker.consumer.mingle] [INFO] mingle: searching for neighbors
base_worker_1         | [2020-05-08 23:04:26 +0000] [7] [amqp] [DEBUG] using channel_id: 1
base_worker_1         | [2020-05-08 23:04:26 +0000] [7] [amqp] [DEBUG] Channel open
rabbitmq-ha_1         | 2020-05-08 23:04:26.635 [info] <0.779.0> accepting AMQP connection <0.779.0> (172.18.0.10:34422 -> 172.18.0.7:5672)
base_worker_1         | [2020-05-08 23:04:26 +0000] [7] [amqp] [DEBUG] Start from server, version: 0.9, properties: {'cluster_name': 'rabbit@queue', 'platform': 'Erlang/OTP 22.3.3', 'copyright': 'Copyright (c) 2007-2020 Pivotal Software, Inc.', 'information': 'Licensed under the MPL.  See https://www.rabbitmq.com/', 'capabilities': {'authentication_failure_close': True, 'per_consumer_qos': True, 'direct_reply_to': True, 'exchange_exchange_bindings': True, 'connection.blocked': True, 'consumer_priorities': True, 'publisher_confirms': True, 'consumer_cancel_notify': True, 'basic.nack': True}, 'version': '3.7.26', 'product': 'RabbitMQ'}, mechanisms: [b'AMQPLAIN', b'PLAIN'], locales: ['en_US']
base_worker_1         | [2020-05-08 23:04:26 +0000] [7] [amqp] [DEBUG] using channel_id: 1
rabbitmq-ha_1         | 2020-05-08 23:04:26.639 [info] <0.779.0> connection <0.779.0> (172.18.0.10:34422 -> 172.18.0.7:5672): user 'celery_user' authenticated and granted access to vhost '/'
base_worker_1         | [2020-05-08 23:04:26 +0000] [7] [amqp] [DEBUG] Channel open
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [celery.worker.consumer.mingle] [INFO] mingle: all alone
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [celery.bootsteps] [DEBUG] ^-- substep ok
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [celery.bootsteps] [DEBUG] | Consumer: Starting Gossip
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [amqp] [DEBUG] using channel_id: 2
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [amqp] [DEBUG] Channel open
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [celery.bootsteps] [DEBUG] ^-- substep ok
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [celery.bootsteps] [DEBUG] | Consumer: Starting Tasks
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [celery.bootsteps] [DEBUG] ^-- substep ok
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [celery.bootsteps] [DEBUG] | Consumer: Starting Control
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [amqp] [DEBUG] using channel_id: 3
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [amqp] [DEBUG] Channel open
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [celery.bootsteps] [DEBUG] ^-- substep ok
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [celery.bootsteps] [DEBUG] | Consumer: Starting Heart
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [amqp] [DEBUG] using channel_id: 1
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [amqp] [DEBUG] Channel open
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [celery.bootsteps] [DEBUG] ^-- substep ok
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [celery.bootsteps] [DEBUG] | Consumer: Starting event loop
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [celery.bootsteps] [DEBUG] | Worker: Hub.register Pool...
base_worker_1         | /home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/celery/fixups/django.py:200: UserWarning: Using settings.DEBUG leads to a memory leak, never use this setting in production environments!
base_worker_1         |   warnings.warn('Using settings.DEBUG leads to a memory leak, never '
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [celery.apps.worker] [INFO] celery@ba7a2a4bc629 ready.
base_worker_1         | [2020-05-08 23:04:27 +0000] [7] [kombu.common] [DEBUG] basic.qos: prefetch_count->30
web-service_1         | [2020-05-08 23:04:33 +0000] [172] [media.apps] [INFO] setting up post_save, post_update signal handlers...
web-service_1         | [2020-05-08 23:04:33 +0000] [172] [media.apps] [INFO] setting up pre_delete, post_delete signal handlers...
web-service_1         | [2020-05-08 23:04:33 +0000] [172] [retry_dbconn] [DEBUG] retry_dbconn: monkeypatching BaseDatabaseWrapper
pgbouncer-service_1   | 2020-05-08 23:04:35.320 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40752 login attempt: db=lumen5 user=lumen5 tls=no
pgbouncer-service_1   | 2020-05-08 23:04:35.325 1 LOG S-0x556cc52aa7e0: lumen5/lumen5@172.18.0.3:5432 new connection to server (from 172.18.0.9:46524)
pgbouncer-service_1   | 2020-05-08 23:04:35.336 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40752 closing because: client close request (age=0)
web-service_1         | 2020-05-08 23:04:37,532 [255] [gunicorn.error] [INFO] Starting gunicorn 20.0.4
web-service_1         | 2020-05-08 23:04:37,533 [255] [gunicorn.error] [INFO] Listening at: http://0.0.0.0:8000 (255)
web-service_1         | 2020-05-08 23:04:37,533 [255] [gunicorn.error] [INFO] Using worker: sync
web-service_1         | 2020-05-08 23:04:37,536 [264] [gunicorn.error] [INFO] Booting worker with pid: 264
web-service_1         | 2020-05-08 23:04:37,593 [265] [gunicorn.error] [INFO] Booting worker with pid: 265
web-service_1         | [2020-05-08 23:04:44 +0000] [264] [media.apps] [INFO] setting up post_save, post_update signal handlers...
web-service_1         | [2020-05-08 23:04:44 +0000] [264] [media.apps] [INFO] setting up pre_delete, post_delete signal handlers...
web-service_1         | [2020-05-08 23:04:44 +0000] [264] [retry_dbconn] [DEBUG] retry_dbconn: monkeypatching BaseDatabaseWrapper
web-service_1         | [2020-05-08 23:04:44 +0000] [265] [media.apps] [INFO] setting up post_save, post_update signal handlers...
web-service_1         | [2020-05-08 23:04:44 +0000] [265] [media.apps] [INFO] setting up pre_delete, post_delete signal handlers...
web-service_1         | [2020-05-08 23:04:44 +0000] [265] [retry_dbconn] [DEBUG] retry_dbconn: monkeypatching BaseDatabaseWrapper
pgbouncer-service_1   | 2020-05-08 23:04:44.327 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40790 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:04:44 +0000] [264] [incoming_requests] [DEBUG] {"get": {"id": "45"}, "post": {}, "time": "2020-05-08T23:04:44.335581+00:00", "path": "/app/"}
base_worker_1         | [2020-05-08 23:04:47 +0000] [7] [amqp] [DEBUG] heartbeat_tick : for connection 4b38861564db4d128568a3020245a256
base_worker_1         | [2020-05-08 23:04:47 +0000] [7] [amqp] [DEBUG] heartbeat_tick : Prev sent/recv: None/None, now - 32/59, monotonic - 109559.01130841, last_heartbeat_sent - 109559.011306948, heartbeat int. - 60 for connection 4b38861564db4d128568a3020245a256
pgbouncer-service_1   | 2020-05-08 23:04:50.287 1 LOG C-0x556cc5259e80: lumen5/lumen5@172.18.0.11:40800 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:04:50 +0000] [265] [incoming_requests] [DEBUG] {"get": {"id": "45"}, "post": {}, "time": "2020-05-08T23:04:50.297348+00:00", "path": "/app/"}
pgbouncer-service_1   | 2020-05-08 23:04:56.856 1 LOG stats: 2 xacts/s, 2 queries/s, in 504 B/s, out 1834 B/s, xact 573 us, query 573 us, wait time 105 us
base_worker_1         | [2020-05-08 23:05:07 +0000] [7] [amqp] [DEBUG] heartbeat_tick : for connection 4b38861564db4d128568a3020245a256
base_worker_1         | [2020-05-08 23:05:07 +0000] [7] [amqp] [DEBUG] heartbeat_tick : Prev sent/recv: 32/59, now - 32/90, monotonic - 109579.012773503, last_heartbeat_sent - 109559.011306948, heartbeat int. - 60 for connection 4b38861564db4d128568a3020245a256
frontend_1            | ℹ ｢wdm｣:    2320 modules
frontend_1            | ℹ ｢wdm｣: Compiled successfully.
web-service_1         | [2020-05-08 23:05:10 +0000] [265] [retry_dbconn] [DEBUG] The connection was pretty old, trying poll
web-service_1         | [2020-05-08 23:05:10 +0000] [264] [retry_dbconn] [DEBUG] The connection was pretty old, trying poll
pgbouncer-service_1   | 2020-05-08 23:05:10.851 1 LOG C-0x556cc5259e80: lumen5/lumen5@172.18.0.11:40800 closing because: client close request (age=20)
pgbouncer-service_1   | 2020-05-08 23:05:10.858 1 LOG C-0x556cc5259e80: lumen5/lumen5@172.18.0.11:40812 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:10 +0000] [265] [incoming_requests] [DEBUG] {"get": {"id": "45"}, "post": {}, "time": "2020-05-08T23:05:10.862854+00:00", "path": "/app/"}
pgbouncer-service_1   | 2020-05-08 23:05:10.986 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40790 closing because: client close request (age=26)
pgbouncer-service_1   | 2020-05-08 23:05:11.309 1 LOG C-0x556cc5259e80: lumen5/lumen5@172.18.0.11:40812 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:13.420 1 LOG C-0x556cc5259e80: lumen5/lumen5@172.18.0.11:40824 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:13 +0000] [264] [incoming_requests] [DEBUG] {"get": {"require_editable_version": "True"}, "post": {}, "time": "2020-05-08T23:05:13.423059+00:00", "path": "/api/video/45/"}
pgbouncer-service_1   | 2020-05-08 23:05:13.426 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40828 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:13 +0000] [265] [incoming_requests] [DEBUG] {"get": {}, "post": {}, "time": "2020-05-08T23:05:13.429880+00:00", "path": "/api/pricing/premium-media/"}
pgbouncer-service_1   | 2020-05-08 23:05:13.487 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40828 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:13.494 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40834 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:13 +0000] [265] [incoming_requests] [DEBUG] {"get": {}, "post": {}, "time": "2020-05-08T23:05:13.498623+00:00", "path": "/api/random-tip/"}
pgbouncer-service_1   | 2020-05-08 23:05:13.515 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40834 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:13.544 1 LOG C-0x556cc5259e80: lumen5/lumen5@172.18.0.11:40824 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:13.802 1 LOG C-0x556cc5259e80: lumen5/lumen5@172.18.0.11:40844 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:13 +0000] [264] [incoming_requests] [DEBUG] {"get": {}, "post": {}, "time": "2020-05-08T23:05:13.804927+00:00", "path": "/api/workspaces/"}
pgbouncer-service_1   | 2020-05-08 23:05:13.807 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40846 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:13 +0000] [265] [incoming_requests] [DEBUG] {"get": {}, "post": {}, "time": "2020-05-08T23:05:13.810226+00:00", "path": "/api/user/"}
pgbouncer-service_1   | 2020-05-08 23:05:13.838 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40846 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:13.844 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40864 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:13 +0000] [265] [incoming_requests] [DEBUG] {"get": {"video_id": "45"}, "post": {}, "time": "2020-05-08T23:05:13.847198+00:00", "path": "/api/article-media/"}
pgbouncer-service_1   | 2020-05-08 23:05:13.880 1 LOG C-0x556cc5259e80: lumen5/lumen5@172.18.0.11:40844 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:13.888 1 LOG C-0x556cc5259e80: lumen5/lumen5@172.18.0.11:40866 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:13 +0000] [264] [incoming_requests] [DEBUG] {"get": {}, "post": {}, "time": "2020-05-08T23:05:13.897474+00:00", "path": "/api/favorites/"}
pgbouncer-service_1   | 2020-05-08 23:05:13.931 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40864 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:13.938 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40868 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:13 +0000] [265] [incoming_requests] [DEBUG] {"get": {}, "post": {}, "time": "2020-05-08T23:05:13.942108+00:00", "path": "/api/brand-profiles/"}
pgbouncer-service_1   | 2020-05-08 23:05:13.973 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40868 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:13.982 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40872 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:13 +0000] [265] [incoming_requests] [DEBUG] {"get": {}, "post": {}, "time": "2020-05-08T23:05:13.986480+00:00", "path": "/api/font-assets/"}
pgbouncer-service_1   | 2020-05-08 23:05:14.030 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40872 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:14.037 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40882 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:14 +0000] [265] [incoming_requests] [DEBUG] {"get": {}, "post": {"video_data": "{\"slides\":[{\"text_pos\":\"bottom_right\",\"overlay_rgba\":[0,0,0,0],\"source_sentence\":null,\"background\":{\"type\":\"video\",\"video\":{\"license\":\"CC0\",\"width\":1920,\"render_url\":\"https://storage.googleapis.com/lumen5-prod-video/fixed_tmp9LebZI.mp4\",\"height\":1080,\"start_time\":null,\"stop_time\":null,\"transform\":[1,0,-0.05555555555555555,1,0,0],\"has_audio\":null,\"is_editorial\":null,\"duration\":12054,\"preview_url\":\"https://storage.googleapis.com/lumen5-prod-video/fixed_tmp9LebZI-HQhdn.mp4\",\"volume\":0,\"source\":12,\"uuid\":\"1a49d595-46b5-42cf-94ca-c21523c9afaa\",\"thumbnail_url\":\"https://storage.googleapis.com/lumen5-prod-video/thumb-fixed_tmp9LebZI-HQhdn.mp4\",\"poster_url\":\"https://storage.googleapis.com/lumen5-prod-images/tmp-placeholder-img-HCf6a.jpg\",\"attribution\":\"\",\"source_id\":\"126\"},\"image\":null},\"scene_design\":\"every_moment_B:text_5\",\"foreground_elements\":[{\"text_2\":{\"content\":\"\",\"size\":70,\"highlight_indices\":[]},\"text_1\":{\"content\":\"hello\",\"size\":150,\"highlight_indices\":[]},\"duration\":567},{\"text_2\":{\"content\":\"\",\"size\":70,\"highlight_indices\":[]},\"text_1\":{\"content\":\"\",\"size\":90,\"highlight_indices\":[]},\"duration\":567},{\"text_2\":{\"content\":\"\",\"size\":70,\"highlight_indices\":[]},\"text_1\":{\"content\":\"\",\"size\":90,\"highlight_indices\":[]},\"duration\":567},{\"text_2\":{\"content\":\"\",\"size\":70,\"highlight_indices\":[]},\"text_1\":{\"content\":\"\",\"size\":90,\"highlight_indices\":[]},\"duration\":567},{\"text_2\":{\"content\":\"\",\"size\":70,\"highlight_indices\":[]},\"text_1\":{\"content\":\"\",\"size\":90,\"highlight_indices\":[]},\"duration\":567},{\"text_2\":{\"content\":\"\",\"size\":70,\"highlight_indices\":[]},\"text_1\":{\"content\":\"\",\"size\":90,\"highlight_indices\":[]},\"duration\":567}],\"background_animation\":\"none\",\"duration\":3400,\"transition\":\"None\",\"slide_number\":1,\"type\":\"text_slide\",\"id\":\"a36540da-5bdd-60ac-804f-5e7deeed6dc8\",\"transition_duration\":0},{\"text_pos\":\"top_center\",\"overlay_rgba\":[0,0,0,0],\"source_sentence\":null,\"background\":{\"type\":\"image\",\"video\":null,\"image\":{\"license\":\"CC0\",\"width\":500,\"render_url\":\"https://storage.googleapis.com/lumen5-prod-images/invisible.png\",\"height\":500,\"transform\":[1,0,0,1,0,0],\"is_editorial\":false,\"preview_url\":\"https://storage.googleapis.com/lumen5-prod-images/invisible.png\",\"source\":0,\"uuid\":\"bb529f5f-6b8e-0802-cd78-3890a892188e\",\"thumbnail_url\":\"https://storage.googleapis.com/lumen5-prod-images/invisible.png\",\"attribution\":null,\"source_id\":null}},\"scene_design\":\"every_moment_B:text_5\",\"foreground_elements\":[{\"text_2\":{\"content\":\"\",\"size\":70,\"highlight_indices\":[]},\"text_1\":{\"content\":\"\",\"size\":90,\"highlight_indices\":[]},\"duration\":4500}],\"background_animation\":\"none\",\"duration\":4500,\"transition\":\"Slide down\",\"slide_number\":2,\"type\":\"text_slide\",\"id\":\"498a0e99-2cb1-5b65-7438-357992824516\",\"transition_duration\":200}],\"watermark\":null,\"aspect_ratio\":\"square\",\"watermark_position\":\"top_right\",\"theme\":{\"transitions_enabled\":true,\"text_1\":{\"accent_rgba\":[255,255,255,100],\"text_rgba\":[25,29,38,100],\"font_url\":\"https://storage.googleapis.com/lumen5-site-css/Uni-Sans-Heavy.otf\",\"highlight_rgba\":[221,52,15,100]},\"text_2\":{\"accent_rgba\":[0,0,0,100],\"text_rgba\":[255,255,255,100],\"font_url\":\"https://storage.googleapis.com/lumen5-site-css/Montserrat-Bold.ttf\",\"highlight_rgba\":[221,52,15,100]},\"background_2_rgba\":[34,34,34,100],\"slide_transition_set\":\"clean\",\"background_1_rgba\":[255,255,255,100]},\"render_output\":\"render_output_single_video\",\"video_height\":720,\"text_direction\":\"ltr\",\"pace_multiplier\":100,\"watermark_opacity\":40,\"theme_reference\":\"every_moment_B\",\"capabilities\":{\"render_1080p\":false,\"allow_no_slides\":false,\"no_branding\":true,\"render_720p\":true,\"custom_watermark\":false},\"audio\":null,\"format\":\"facebook_post_square\",\"version\":\"9.47.0\"}"}, "time": "2020-05-08T23:05:14.040551+00:00", "path": "/api/premium-media-credit-check/"}
pgbouncer-service_1   | 2020-05-08 23:05:14.063 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40882 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:14.071 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40892 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:14 +0000] [265] [incoming_requests] [DEBUG] {"get": {}, "post": {}, "time": "2020-05-08T23:05:14.073551+00:00", "path": "/api/recommend-search-terms/"}
web-service_1         | [2020-05-08 23:05:14 +0000] [264] [elasticsearch] [INFO] POST http://elasticsearch-v3:9200/media_history/_msearch?filter_path=responses.status%2Cresponses.hits.hits._source.type%2Cresponses.hits.hits._source.uuid%2Cresponses.hits.hits.matched_queries%2Cresponses.hits.hits.fields [status:200 request:0.273s]
web-service_1         | [2020-05-08 23:05:14 +0000] [264] [elasticsearch] [DEBUG] > {"index": "media_history"}
web-service_1         | {"from": 0, "query": {"bool": {"filter": [{"match": {"path": "favorites/1"}}], "must_not": []}}, "size": 1000, "sort": [{"last_updated": {"order": "desc"}}]}
web-service_1         | 
web-service_1         | [2020-05-08 23:05:14 +0000] [264] [elasticsearch] [DEBUG] < {"responses":[{"status":200}]}
pgbouncer-service_1   | 2020-05-08 23:05:14.221 1 LOG C-0x556cc5259e80: lumen5/lumen5@172.18.0.11:40866 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:14.239 1 LOG C-0x556cc5259e80: lumen5/lumen5@172.18.0.11:40894 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:14 +0000] [264] [incoming_requests] [DEBUG] {"get": {"theme": "every_moment_B", "recommend_overlay": "true", "highlight_rgba[]": "100", "asset_type": "video", "y_offset": "0", "asset_uuid": "1a49d595-46b5-42cf-94ca-c21523c9afaa", "aspect_ratio": "square", "recommend_scene_design": "false", "x_offset": "-0.05555555555555555", "auto_crop": "true"}, "post": {}, "time": "2020-05-08T23:05:14.244125+00:00", "path": "/api/scene-attributes/"}
pgbouncer-service_1   | 2020-05-08 23:05:15.055 1 LOG C-0x556cc5259e80: lumen5/lumen5@172.18.0.11:40894 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:15.061 1 LOG C-0x556cc5259e80: lumen5/lumen5@172.18.0.11:40908 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:15 +0000] [264] [incoming_requests] [DEBUG] {"get": {"theme": "every_moment_B", "recommend_overlay": "true", "highlight_rgba[]": "100", "asset_type": "image", "y_offset": "0", "asset_uuid": "bb529f5f-6b8e-0802-cd78-3890a892188e", "aspect_ratio": "square", "recommend_scene_design": "false", "x_offset": "0", "auto_crop": "true"}, "post": {}, "time": "2020-05-08T23:05:15.063925+00:00", "path": "/api/scene-attributes/"}
pgbouncer-service_1   | 2020-05-08 23:05:15.381 1 LOG C-0x556cc5259e80: lumen5/lumen5@172.18.0.11:40908 closing because: client close request (age=0)
web-service_1         | [2020-05-08 23:05:18 +0000] [265] [web_parsing.topic_parser] [DEBUG] CACHE MISS: web_parsing.topic_parser get_article_labels
web-service_1         | [2020-05-08 23:05:18 +0000] [265] [web_parsing.external_util] [ERROR] HTTPConnectionPool(host='summarization-service', port=8002): Max retries exceeded with url: /multi-label-classify (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7fccbc4c2320>: Failed to establish a new connection: [Errno -2] Name or service not known',))
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connection.py", line 159, in _new_conn
web-service_1         |     (self._dns_host, self.port), self.timeout, **extra_kw)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/util/connection.py", line 57, in create_connection
web-service_1         |     for res in socket.getaddrinfo(host, port, family, socket.SOCK_STREAM):
web-service_1         |   File "/usr/lib/python3.5/socket.py", line 733, in getaddrinfo
web-service_1         |     for res in _socket.getaddrinfo(host, port, family, type, proto, flags):
web-service_1         | socket.gaierror: [Errno -2] Name or service not known
web-service_1         | 
web-service_1         | During handling of the above exception, another exception occurred:
web-service_1         | 
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connectionpool.py", line 600, in urlopen
web-service_1         |     chunked=chunked)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connectionpool.py", line 354, in _make_request
web-service_1         |     conn.request(method, url, **httplib_request_kw)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 1107, in request
web-service_1         |     self._send_request(method, url, body, headers)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 1152, in _send_request
web-service_1         |     self.endheaders(body)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 1103, in endheaders
web-service_1         |     self._send_output(message_body)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 934, in _send_output
web-service_1         |     self.send(msg)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 877, in send
web-service_1         |     self.connect()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connection.py", line 181, in connect
web-service_1         |     conn = self._new_conn()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connection.py", line 168, in _new_conn
web-service_1         |     self, "Failed to establish a new connection: %s" % e)
web-service_1         | urllib3.exceptions.NewConnectionError: <urllib3.connection.HTTPConnection object at 0x7fccbc4c2320>: Failed to establish a new connection: [Errno -2] Name or service not known
web-service_1         | 
web-service_1         | During handling of the above exception, another exception occurred:
web-service_1         | 
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/adapters.py", line 449, in send
web-service_1         |     timeout=timeout
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connectionpool.py", line 638, in urlopen
web-service_1         |     _stacktrace=sys.exc_info()[2])
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/util/retry.py", line 399, in increment
web-service_1         |     raise MaxRetryError(_pool, url, error or ResponseError(cause))
web-service_1         | urllib3.exceptions.MaxRetryError: HTTPConnectionPool(host='summarization-service', port=8002): Max retries exceeded with url: /multi-label-classify (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7fccbc4c2320>: Failed to establish a new connection: [Errno -2] Name or service not known',))
web-service_1         | 
web-service_1         | During handling of the above exception, another exception occurred:
web-service_1         | 
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/opt/app/web_parsing/external_util.py", line 394, in multi_label_classify
web-service_1         |     'max_depth': max_depth
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/api.py", line 116, in post
web-service_1         |     return request('post', url, data=data, json=json, **kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/api.py", line 60, in request
web-service_1         |     return session.request(method=method, url=url, **kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/sessions.py", line 533, in request
web-service_1         |     resp = self.send(prep, **send_kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/sessions.py", line 646, in send
web-service_1         |     r = adapter.send(request, **kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/adapters.py", line 516, in send
web-service_1         |     raise ConnectionError(e, request=request)
web-service_1         | requests.exceptions.ConnectionError: HTTPConnectionPool(host='summarization-service', port=8002): Max retries exceeded with url: /multi-label-classify (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7fccbc4c2320>: Failed to establish a new connection: [Errno -2] Name or service not known',))
web-service_1         | [2020-05-08 23:05:18 +0000] [265] [web_parsing.topic_parser] [DEBUG] CACHE MISS: web_parsing.topic_parser get_article_labels
web-service_1         | [2020-05-08 23:05:18 +0000] [265] [web_parsing.external_util] [ERROR] HTTPConnectionPool(host='summarization-service', port=8002): Max retries exceeded with url: /multi-label-classify (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7fccbc4c2cc0>: Failed to establish a new connection: [Errno -2] Name or service not known',))
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connection.py", line 159, in _new_conn
web-service_1         |     (self._dns_host, self.port), self.timeout, **extra_kw)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/util/connection.py", line 57, in create_connection
web-service_1         |     for res in socket.getaddrinfo(host, port, family, socket.SOCK_STREAM):
web-service_1         |   File "/usr/lib/python3.5/socket.py", line 733, in getaddrinfo
web-service_1         |     for res in _socket.getaddrinfo(host, port, family, type, proto, flags):
web-service_1         | socket.gaierror: [Errno -2] Name or service not known
web-service_1         | 
web-service_1         | During handling of the above exception, another exception occurred:
web-service_1         | 
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connectionpool.py", line 600, in urlopen
web-service_1         |     chunked=chunked)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connectionpool.py", line 354, in _make_request
web-service_1         |     conn.request(method, url, **httplib_request_kw)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 1107, in request
web-service_1         |     self._send_request(method, url, body, headers)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 1152, in _send_request
web-service_1         |     self.endheaders(body)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 1103, in endheaders
web-service_1         |     self._send_output(message_body)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 934, in _send_output
web-service_1         |     self.send(msg)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 877, in send
web-service_1         |     self.connect()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connection.py", line 181, in connect
web-service_1         |     conn = self._new_conn()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connection.py", line 168, in _new_conn
web-service_1         |     self, "Failed to establish a new connection: %s" % e)
web-service_1         | urllib3.exceptions.NewConnectionError: <urllib3.connection.HTTPConnection object at 0x7fccbc4c2cc0>: Failed to establish a new connection: [Errno -2] Name or service not known
web-service_1         | 
web-service_1         | During handling of the above exception, another exception occurred:
web-service_1         | 
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/adapters.py", line 449, in send
web-service_1         |     timeout=timeout
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connectionpool.py", line 638, in urlopen
web-service_1         |     _stacktrace=sys.exc_info()[2])
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/util/retry.py", line 399, in increment
web-service_1         |     raise MaxRetryError(_pool, url, error or ResponseError(cause))
web-service_1         | urllib3.exceptions.MaxRetryError: HTTPConnectionPool(host='summarization-service', port=8002): Max retries exceeded with url: /multi-label-classify (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7fccbc4c2cc0>: Failed to establish a new connection: [Errno -2] Name or service not known',))
web-service_1         | 
web-service_1         | During handling of the above exception, another exception occurred:
web-service_1         | 
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/opt/app/web_parsing/external_util.py", line 394, in multi_label_classify
web-service_1         |     'max_depth': max_depth
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/api.py", line 116, in post
web-service_1         |     return request('post', url, data=data, json=json, **kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/api.py", line 60, in request
web-service_1         |     return session.request(method=method, url=url, **kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/sessions.py", line 533, in request
web-service_1         |     resp = self.send(prep, **send_kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/sessions.py", line 646, in send
web-service_1         |     r = adapter.send(request, **kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/adapters.py", line 516, in send
web-service_1         |     raise ConnectionError(e, request=request)
web-service_1         | requests.exceptions.ConnectionError: HTTPConnectionPool(host='summarization-service', port=8002): Max retries exceeded with url: /multi-label-classify (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7fccbc4c2cc0>: Failed to establish a new connection: [Errno -2] Name or service not known',))
web-service_1         | [2020-05-08 23:05:18 +0000] [265] [web_parsing.topic_parser] [DEBUG] CACHE MISS: web_parsing.topic_parser get_article_labels
web-service_1         | [2020-05-08 23:05:18 +0000] [265] [web_parsing.external_util] [ERROR] HTTPConnectionPool(host='summarization-service', port=8002): Max retries exceeded with url: /multi-label-classify (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7fccbc4c25f8>: Failed to establish a new connection: [Errno -2] Name or service not known',))
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connection.py", line 159, in _new_conn
web-service_1         |     (self._dns_host, self.port), self.timeout, **extra_kw)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/util/connection.py", line 57, in create_connection
web-service_1         |     for res in socket.getaddrinfo(host, port, family, socket.SOCK_STREAM):
web-service_1         |   File "/usr/lib/python3.5/socket.py", line 733, in getaddrinfo
web-service_1         |     for res in _socket.getaddrinfo(host, port, family, type, proto, flags):
web-service_1         | socket.gaierror: [Errno -2] Name or service not known
web-service_1         | 
web-service_1         | During handling of the above exception, another exception occurred:
web-service_1         | 
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connectionpool.py", line 600, in urlopen
web-service_1         |     chunked=chunked)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connectionpool.py", line 354, in _make_request
web-service_1         |     conn.request(method, url, **httplib_request_kw)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 1107, in request
web-service_1         |     self._send_request(method, url, body, headers)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 1152, in _send_request
web-service_1         |     self.endheaders(body)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 1103, in endheaders
web-service_1         |     self._send_output(message_body)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 934, in _send_output
web-service_1         |     self.send(msg)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 877, in send
web-service_1         |     self.connect()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connection.py", line 181, in connect
web-service_1         |     conn = self._new_conn()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connection.py", line 168, in _new_conn
web-service_1         |     self, "Failed to establish a new connection: %s" % e)
web-service_1         | urllib3.exceptions.NewConnectionError: <urllib3.connection.HTTPConnection object at 0x7fccbc4c25f8>: Failed to establish a new connection: [Errno -2] Name or service not known
web-service_1         | 
web-service_1         | During handling of the above exception, another exception occurred:
web-service_1         | 
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/adapters.py", line 449, in send
web-service_1         |     timeout=timeout
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connectionpool.py", line 638, in urlopen
web-service_1         |     _stacktrace=sys.exc_info()[2])
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/util/retry.py", line 399, in increment
web-service_1         |     raise MaxRetryError(_pool, url, error or ResponseError(cause))
web-service_1         | urllib3.exceptions.MaxRetryError: HTTPConnectionPool(host='summarization-service', port=8002): Max retries exceeded with url: /multi-label-classify (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7fccbc4c25f8>: Failed to establish a new connection: [Errno -2] Name or service not known',))
web-service_1         | 
web-service_1         | During handling of the above exception, another exception occurred:
web-service_1         | 
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/opt/app/web_parsing/external_util.py", line 394, in multi_label_classify
web-service_1         |     'max_depth': max_depth
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/api.py", line 116, in post
web-service_1         |     return request('post', url, data=data, json=json, **kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/api.py", line 60, in request
web-service_1         |     return session.request(method=method, url=url, **kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/sessions.py", line 533, in request
web-service_1         |     resp = self.send(prep, **send_kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/sessions.py", line 646, in send
web-service_1         |     r = adapter.send(request, **kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/adapters.py", line 516, in send
web-service_1         |     raise ConnectionError(e, request=request)
web-service_1         | requests.exceptions.ConnectionError: HTTPConnectionPool(host='summarization-service', port=8002): Max retries exceeded with url: /multi-label-classify (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7fccbc4c25f8>: Failed to establish a new connection: [Errno -2] Name or service not known',))
web-service_1         | [2020-05-08 23:05:18 +0000] [265] [web_parsing.topic_parser] [DEBUG] CACHE MISS: web_parsing.topic_parser get_named_entities
web-service_1         | [2020-05-08 23:05:18 +0000] [265] [web_parsing.topic_parser] [DEBUG] entities: []
web-service_1         | [2020-05-08 23:05:18 +0000] [265] [web_parsing.topic_parser] [DEBUG] CACHE MISS: web_parsing.topic_parser get_topics
web-service_1         | [2020-05-08 23:05:18 +0000] [265] [web_parsing.topic_parser] [DEBUG] CACHE MISS: web_parsing.topic_parser get_article_labels
web-service_1         | [2020-05-08 23:05:18 +0000] [265] [web_parsing.external_util] [ERROR] HTTPConnectionPool(host='summarization-service', port=8002): Max retries exceeded with url: /multi-label-classify (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7fccbc2a7fd0>: Failed to establish a new connection: [Errno -2] Name or service not known',))
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connection.py", line 159, in _new_conn
web-service_1         |     (self._dns_host, self.port), self.timeout, **extra_kw)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/util/connection.py", line 57, in create_connection
web-service_1         |     for res in socket.getaddrinfo(host, port, family, socket.SOCK_STREAM):
web-service_1         |   File "/usr/lib/python3.5/socket.py", line 733, in getaddrinfo
web-service_1         |     for res in _socket.getaddrinfo(host, port, family, type, proto, flags):
web-service_1         | socket.gaierror: [Errno -2] Name or service not known
web-service_1         | 
web-service_1         | During handling of the above exception, another exception occurred:
web-service_1         | 
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connectionpool.py", line 600, in urlopen
web-service_1         |     chunked=chunked)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connectionpool.py", line 354, in _make_request
web-service_1         |     conn.request(method, url, **httplib_request_kw)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 1107, in request
web-service_1         |     self._send_request(method, url, body, headers)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 1152, in _send_request
web-service_1         |     self.endheaders(body)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 1103, in endheaders
web-service_1         |     self._send_output(message_body)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 934, in _send_output
web-service_1         |     self.send(msg)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 877, in send
web-service_1         |     self.connect()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connection.py", line 181, in connect
web-service_1         |     conn = self._new_conn()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connection.py", line 168, in _new_conn
web-service_1         |     self, "Failed to establish a new connection: %s" % e)
web-service_1         | urllib3.exceptions.NewConnectionError: <urllib3.connection.HTTPConnection object at 0x7fccbc2a7fd0>: Failed to establish a new connection: [Errno -2] Name or service not known
web-service_1         | 
web-service_1         | During handling of the above exception, another exception occurred:
web-service_1         | 
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/adapters.py", line 449, in send
web-service_1         |     timeout=timeout
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connectionpool.py", line 638, in urlopen
web-service_1         |     _stacktrace=sys.exc_info()[2])
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/util/retry.py", line 399, in increment
web-service_1         |     raise MaxRetryError(_pool, url, error or ResponseError(cause))
web-service_1         | urllib3.exceptions.MaxRetryError: HTTPConnectionPool(host='summarization-service', port=8002): Max retries exceeded with url: /multi-label-classify (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7fccbc2a7fd0>: Failed to establish a new connection: [Errno -2] Name or service not known',))
web-service_1         | 
web-service_1         | During handling of the above exception, another exception occurred:
web-service_1         | 
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/opt/app/web_parsing/external_util.py", line 394, in multi_label_classify
web-service_1         |     'max_depth': max_depth
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/api.py", line 116, in post
web-service_1         |     return request('post', url, data=data, json=json, **kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/api.py", line 60, in request
web-service_1         |     return session.request(method=method, url=url, **kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/sessions.py", line 533, in request
web-service_1         |     resp = self.send(prep, **send_kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/sessions.py", line 646, in send
web-service_1         |     r = adapter.send(request, **kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/adapters.py", line 516, in send
web-service_1         |     raise ConnectionError(e, request=request)
web-service_1         | requests.exceptions.ConnectionError: HTTPConnectionPool(host='summarization-service', port=8002): Max retries exceeded with url: /multi-label-classify (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7fccbc2a7fd0>: Failed to establish a new connection: [Errno -2] Name or service not known',))
web-service_1         | [2020-05-08 23:05:18 +0000] [265] [web_parsing.topic_parser] [DEBUG] CACHE MISS: web_parsing.topic_parser get_named_entities
web-service_1         | [2020-05-08 23:05:18 +0000] [265] [web_parsing.topic_parser] [DEBUG] entities: []
web-service_1         | [2020-05-08 23:05:18 +0000] [265] [web_parsing.topic_parser] [DEBUG] CACHE MISS: web_parsing.topic_parser get_topics
web-service_1         | [2020-05-08 23:05:18 +0000] [265] [web_parsing.topic_parser] [DEBUG] CACHE MISS: web_parsing.topic_parser get_article_labels
web-service_1         | [2020-05-08 23:05:18 +0000] [265] [web_parsing.external_util] [ERROR] HTTPConnectionPool(host='summarization-service', port=8002): Max retries exceeded with url: /multi-label-classify (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7fccbc2a7b38>: Failed to establish a new connection: [Errno -2] Name or service not known',))
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connection.py", line 159, in _new_conn
web-service_1         |     (self._dns_host, self.port), self.timeout, **extra_kw)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/util/connection.py", line 57, in create_connection
web-service_1         |     for res in socket.getaddrinfo(host, port, family, socket.SOCK_STREAM):
web-service_1         |   File "/usr/lib/python3.5/socket.py", line 733, in getaddrinfo
web-service_1         |     for res in _socket.getaddrinfo(host, port, family, type, proto, flags):
web-service_1         | socket.gaierror: [Errno -2] Name or service not known
web-service_1         | 
web-service_1         | During handling of the above exception, another exception occurred:
web-service_1         | 
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connectionpool.py", line 600, in urlopen
web-service_1         |     chunked=chunked)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connectionpool.py", line 354, in _make_request
web-service_1         |     conn.request(method, url, **httplib_request_kw)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 1107, in request
web-service_1         |     self._send_request(method, url, body, headers)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 1152, in _send_request
web-service_1         |     self.endheaders(body)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 1103, in endheaders
web-service_1         |     self._send_output(message_body)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 934, in _send_output
web-service_1         |     self.send(msg)
web-service_1         |   File "/usr/lib/python3.5/http/client.py", line 877, in send
web-service_1         |     self.connect()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connection.py", line 181, in connect
web-service_1         |     conn = self._new_conn()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connection.py", line 168, in _new_conn
web-service_1         |     self, "Failed to establish a new connection: %s" % e)
web-service_1         | urllib3.exceptions.NewConnectionError: <urllib3.connection.HTTPConnection object at 0x7fccbc2a7b38>: Failed to establish a new connection: [Errno -2] Name or service not known
web-service_1         | 
web-service_1         | During handling of the above exception, another exception occurred:
web-service_1         | 
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/adapters.py", line 449, in send
web-service_1         |     timeout=timeout
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/connectionpool.py", line 638, in urlopen
web-service_1         |     _stacktrace=sys.exc_info()[2])
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/urllib3/util/retry.py", line 399, in increment
web-service_1         |     raise MaxRetryError(_pool, url, error or ResponseError(cause))
web-service_1         | urllib3.exceptions.MaxRetryError: HTTPConnectionPool(host='summarization-service', port=8002): Max retries exceeded with url: /multi-label-classify (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7fccbc2a7b38>: Failed to establish a new connection: [Errno -2] Name or service not known',))
web-service_1         | 
web-service_1         | During handling of the above exception, another exception occurred:
web-service_1         | 
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/opt/app/web_parsing/external_util.py", line 394, in multi_label_classify
web-service_1         |     'max_depth': max_depth
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/api.py", line 116, in post
web-service_1         |     return request('post', url, data=data, json=json, **kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/api.py", line 60, in request
web-service_1         |     return session.request(method=method, url=url, **kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/sessions.py", line 533, in request
web-service_1         |     resp = self.send(prep, **send_kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/sessions.py", line 646, in send
web-service_1         |     r = adapter.send(request, **kwargs)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/requests/adapters.py", line 516, in send
web-service_1         |     raise ConnectionError(e, request=request)
web-service_1         | requests.exceptions.ConnectionError: HTTPConnectionPool(host='summarization-service', port=8002): Max retries exceeded with url: /multi-label-classify (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0x7fccbc2a7b38>: Failed to establish a new connection: [Errno -2] Name or service not known',))
pgbouncer-service_1   | 2020-05-08 23:05:18.430 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40892 closing because: client close request (age=4)
base_worker_1         | [2020-05-08 23:05:27 +0000] [7] [amqp] [DEBUG] heartbeat_tick : for connection 4b38861564db4d128568a3020245a256
base_worker_1         | [2020-05-08 23:05:27 +0000] [7] [amqp] [DEBUG] heartbeat_tick : Prev sent/recv: 32/90, now - 32/120, monotonic - 109599.014267652, last_heartbeat_sent - 109559.011306948, heartbeat int. - 60 for connection 4b38861564db4d128568a3020245a256
pgbouncer-service_1   | 2020-05-08 23:05:33.990 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40916 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:33 +0000] [265] [incoming_requests] [DEBUG] {"get": {}, "post": {}, "time": "2020-05-08T23:05:33.992242+00:00", "path": "/api/video/45/"}
web-service_1         | [2020-05-08 23:05:34 +0000] [265] [web.api_views] [DEBUG] Video with ID: 45 just saved
pgbouncer-service_1   | 2020-05-08 23:05:34.027 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40916 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:41.593 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40922 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:41 +0000] [265] [incoming_requests] [DEBUG] {"get": {"filter": "videos,photos,editorial", "source": "recommended", "q": "", "autocorrect": "false", "video_duration": "7", "boost_terms": "[]", "page": "1", "sort": "", "did_you_mean": "false"}, "post": {}, "time": "2020-05-08T23:05:41.595600+00:00", "path": "/api/background-assets/"}
web-service_1         | [2020-05-08 23:05:41 +0000] [265] [elasticsearch] [INFO] POST http://elasticsearch-v3:9200/media_43tc/_msearch?filter_path=responses.status%2Cresponses.hits.hits._id%2Cresponses.hits.hits._source.type%2Cresponses.hits.hits.matched_queries%2Cresponses.hits.hits.fields%2Cresponses.suggest%2Cresponses.hits.hits._source.query [status:200 request:0.060s]
web-service_1         | [2020-05-08 23:05:41 +0000] [265] [elasticsearch] [DEBUG] > {"index": "media_43tc"}
web-service_1         | {"from": 0, "query": {"bool": {"filter": [], "must_not": [{"term": {"src": 0}}, {"term": {"src": 1}}, {"term": {"src": 2}}, {"term": {"src": 3}}, {"term": {"src": 26}}, {"term": {"license": "user_private"}}, {"bool": {"must": [{"term": {"src": 16}}, {"bool": {"must_not": {"terms": {"getty_collection_code": ["NEW", "SPO", "ENT", "ARP", "AFP", "AFE", "GIEF", "WIV", "GIS", "SKP", "CRV", "ISF", "VTV"]}}}}]}}, {"term": {"src": 23}}, {"term": {"src": 24}}, {"term": {"src": 16}}, {"term": {"src": 25}}, {"term": {"src": 26}}, {"term": {"editorial": true}}, {"term": {"src": 16}}, {"term": {"src": 25}}, {"term": {"src": 26}}], "should": [{"term": {"type": {"value": "VideoAsset", "boost": 2}}}], "must": [{"query_string": {"default_field": "jam", "query": "", "minimum_should_match": "50%"}}]}}, "size": 1000}
web-service_1         | {"index": "media_43tc"}
web-service_1         | {"from": 0, "query": {"bool": {"filter": [], "must_not": [{"term": {"src": 0}}, {"term": {"src": 1}}, {"term": {"src": 2}}, {"term": {"src": 3}}, {"term": {"src": 26}}, {"term": {"license": "user_private"}}, {"bool": {"must": [{"term": {"src": 16}}, {"bool": {"must_not": {"terms": {"getty_collection_code": ["NEW", "SPO", "ENT", "ARP", "AFP", "AFE", "GIEF", "WIV", "GIS", "SKP", "CRV", "ISF", "VTV"]}}}}]}}, {"term": {"src": 0}}, {"term": {"src": 1}}, {"term": {"src": 2}}, {"term": {"src": 3}}, {"term": {"src": 4}}, {"term": {"src": 5}}, {"term": {"src": 6}}, {"term": {"src": 7}}, {"term": {"src": 8}}, {"term": {"src": 9}}, {"term": {"src": 10}}, {"term": {"src": 11}}, {"term": {"src": 12}}, {"term": {"src": 13}}, {"term": {"src": 14}}, {"term": {"src": 15}}, {"term": {"src": 17}}, {"term": {"src": 18}}, {"term": {"src": 19}}, {"term": {"src": 20}}, {"term": {"src": 21}}, {"term": {"src": 22}}, {"term": {"editorial": true}}], "should": [{"term": {"type": {"value": "VideoAsset", "boost": 2}}}], "must": [{"query_string": {"default_field": "jam", "query": "", "minimum_should_match": "50%"}}]}}, "size": 2}
web-service_1         | {"index": "popular_query_index"}
web-service_1         | {"from": 0, "query": {"bool": {"filter": {"range": {"last_updated": {"gte": "2020-05-07"}}}, "must": {"match_phrase": {"query": ""}}}}, "sort": [{"freq": {"order": "desc"}}], "size": 6}
web-service_1         | 
web-service_1         | [2020-05-08 23:05:41 +0000] [265] [elasticsearch] [DEBUG] < {"responses":[{"status":200},{"status":200},{"status":200}]}
web-service_1         | [2020-05-08 23:05:41 +0000] [265] [web.model_search] [DEBUG] results: {'responses': [{'status': 200}, {'status': 200}, {'status': 200}]}
pgbouncer-service_1   | 2020-05-08 23:05:41.678 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40922 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:41.689 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40930 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:41 +0000] [265] [incoming_requests] [DEBUG] {"get": {}, "post": {}, "time": "2020-05-08T23:05:41.690949+00:00", "path": "/api/clicklogsrecommendation/"}
web-service_1         | {"severity": "INFO", "textPayload": {"user": 1, "time": "2020-05-08T23:05:41.696541Z", "video_id": 45, "log_name": "media_recommendations_v1", "action": "R", "query": [], "page": 1, "strategy": "recommended", "results": [], "results_shape": [-1, 2], "language": "en", "filter": {"marketplace_enabled": true}}, "name": "click_logs"}
pgbouncer-service_1   | 2020-05-08 23:05:41.701 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40930 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:46.853 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40938 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:46 +0000] [265] [incoming_requests] [DEBUG] {"get": {"filter": "videos,photos,editorial", "source": "recommended", "q": "Nature", "autocorrect": "true", "video_duration": "7", "boost_terms": "[]", "page": "1", "sort": "", "did_you_mean": "true"}, "post": {}, "time": "2020-05-08T23:05:46.856847+00:00", "path": "/api/background-assets/"}
web-service_1         | 
web-service_1         | [2020-05-08 23:05:47 +0000] [265] [elasticsearch] [INFO] POST http://elasticsearch-v3:9200/media_43tc/_msearch?filter_path=responses.status%2Cresponses.hits.hits._id%2Cresponses.hits.hits._source.type%2Cresponses.hits.hits.matched_queries%2Cresponses.hits.hits.fields%2Cresponses.suggest%2Cresponses.hits.hits._source.query [status:200 request:0.139s]
web-service_1         | [2020-05-08 23:05:47 +0000] [265] [elasticsearch] [DEBUG] > {"index": "media_43tc"}
web-service_1         | {"from": 0, "query": {"bool": {"filter": [], "must_not": [{"term": {"src": 0}}, {"term": {"src": 1}}, {"term": {"src": 2}}, {"term": {"src": 3}}, {"term": {"src": 26}}, {"term": {"license": "user_private"}}, {"bool": {"must": [{"term": {"src": 16}}, {"bool": {"must_not": {"terms": {"getty_collection_code": ["NEW", "SPO", "ENT", "ARP", "AFP", "AFE", "GIEF", "WIV", "GIS", "SKP", "CRV", "ISF", "VTV"]}}}}]}}, {"term": {"src": 23}}, {"term": {"src": 24}}, {"term": {"src": 16}}, {"term": {"src": 25}}, {"term": {"src": 26}}, {"term": {"editorial": true}}, {"term": {"src": 16}}, {"term": {"src": 25}}, {"term": {"src": 26}}], "should": [{"term": {"type": {"value": "VideoAsset", "boost": 2}}}], "must": [{"query_string": {"default_field": "jam", "query": "Nature", "minimum_should_match": "50%"}}]}}, "suggest": {"did_you_mean": {"phrase": {"highlight": {"post_tag": "</em>", "pre_tag": "<em>"}, "field": "did_you_mean", "direct_generator": [{"field": "did_you_mean", "suggest_mode": "missing", "min_word_length": 5}], "gram_size": 3, "size": 1}}, "text": "Nature", "autocorrect": {"term": {"field": "tags", "suggest_mode": "missing", "sort": "frequency"}}}, "size": 1000}
web-service_1         | {"index": "media_43tc"}
web-service_1         | {"from": 0, "query": {"bool": {"filter": [], "must_not": [{"term": {"src": 0}}, {"term": {"src": 1}}, {"term": {"src": 2}}, {"term": {"src": 3}}, {"term": {"src": 26}}, {"term": {"license": "user_private"}}, {"bool": {"must": [{"term": {"src": 16}}, {"bool": {"must_not": {"terms": {"getty_collection_code": ["NEW", "SPO", "ENT", "ARP", "AFP", "AFE", "GIEF", "WIV", "GIS", "SKP", "CRV", "ISF", "VTV"]}}}}]}}, {"term": {"src": 0}}, {"term": {"src": 1}}, {"term": {"src": 2}}, {"term": {"src": 3}}, {"term": {"src": 4}}, {"term": {"src": 5}}, {"term": {"src": 6}}, {"term": {"src": 7}}, {"term": {"src": 8}}, {"term": {"src": 9}}, {"term": {"src": 10}}, {"term": {"src": 11}}, {"term": {"src": 12}}, {"term": {"src": 13}}, {"term": {"src": 14}}, {"term": {"src": 15}}, {"term": {"src": 17}}, {"term": {"src": 18}}, {"term": {"src": 19}}, {"term": {"src": 20}}, {"term": {"src": 21}}, {"term": {"src": 22}}, {"term": {"editorial": true}}], "should": [{"term": {"type": {"value": "VideoAsset", "boost": 2}}}], "must": [{"query_string": {"default_field": "jam", "query": "Nature", "minimum_should_match": "50%"}}]}}, "size": 2}
web-service_1         | {"index": "popular_query_index"}
web-service_1         | {"from": 0, "query": {"bool": {"filter": {"range": {"last_updated": {"gte": "2020-05-07"}}}, "must": {"match_phrase": {"query": "Nature"}}}}, "sort": [{"freq": {"order": "desc"}}], "size": 6}
web-service_1         | 
web-service_1         | [2020-05-08 23:05:47 +0000] [265] [elasticsearch] [DEBUG] < {"responses":[{"hits":{"hits":[{"_id":"72c208df-4fad-49f6-bf28-a1ae7c4682db","_source":{"type":"VideoAsset"}},{"_id":"b2fa31bf-1b8e-41e4-b7e2-dda646171c08","_source":{"type":"VideoAsset"}},{"_id":"1a49d595-46b5-42cf-94ca-c21523c9afaa","_source":{"type":"VideoAsset"}},{"_id":"723084f5-0d54-4f55-8098-9b40eabc7c2e","_source":{"type":"VideoAsset"}},{"_id":"bd9f9de4-1b9e-4840-8c25-2a7acb300497","_source":{"type":"VideoAsset"}},{"_id":"13f53d83-4a4d-41c1-a9a1-175bf10c3821","_source":{"type":"VideoAsset"}},{"_id":"8956ec13-f0ad-47a3-a36f-cfae0b1be9d2","_source":{"type":"VideoAsset"}},{"_id":"4451c02a-11ec-457e-a78d-4f6bae0d7113","_source":{"type":"VideoAsset"}},{"_id":"07b100e3-9e1a-4ce3-bb20-09da7aec5e3c","_source":{"type":"VideoAsset"}},{"_id":"8a6f424c-dffb-4a52-897d-f385ac2334fe","_source":{"type":"VideoAsset"}},{"_id":"f10fcda5-3532-49d6-8690-50ec108ee05e","_source":{"type":"VideoAsset"}},{"_id":"0b6e7df0-95aa-4145-b50f-cc76a7098354","_source":{"type":"VideoAsset"}},{"_id":"b2c09d7d-d8cd-4a11-907a-b0561bf6a34e","_source":{"type":"VideoAsset"}},{"_id":"e02c4379-0f7f-41a0-92dc-210f1022f3c4","_source":{"type":"VideoAsset"}},{"_id":"aabe81d9-7882-4d91-9012-191e4a526edc","_source":{"type":"VideoAsset"}},{"_id":"5610e39f-479d-4a39-b67d-c05de86bd8d3","_source":{"type":"VideoAsset"}},{"_id":"9b8d66c4-7197-4a04-a645-5e4e7da7b311","_source":{"type":"VideoAsset"}},{"_id":"205ee663-4a5c-45ae-94c9-fe26e23aff62","_source":{"type":"VideoAsset"}},{"_id":"d80fdf6e-0531-46c1-b5e4-1a515c9a1fe1","_source":{"type":"VideoAsset"}},{"_id":"cd091a7f-a244-411a-8b03-ff771e631fa5","_source":{"type":"VideoAsset"}},{"_id":"e58e458b-d144-44c3-b851-fd28df60b6f7","_source":{"type":"VideoAsset"}},{"_id":"b4488ab0-c818-49ff-9325-cf3e1a0a7800","_source":{"type":"VideoAsset"}},{"_id":"e907e8fc-f929-4450-aa37-9dadd4062d5f","_source":{"type":"VideoAsset"}},{"_id":"8fbcbfbd-8748-4459-b11d-e63f6cce4b99","_source":{"type":"VideoAsset"}},{"_id":"837323ea-d664-49a0-aa16-b954184405c9","_source":{"type":"VideoAsset"}},{"_id":"65bd495e-f207-4c73-800e-92c600c870e9","_source":{"type":"VideoAsset"}},{"_id":"22acb077-b854-448e-a775-9704e66879fa","_source":{"type":"VideoAsset"}},{"_id":"745b1022-583b-4b47-b28f-64eeb3eba573","_source":{"type":"ImageAsset"}},{"_id":"35909c80-26e7-46cf-b030-73ac437bd0bf","_source":{"type":"ImageAsset"}},{"_id":"0074129d-708d-430b-85f9-fdfca96aab33","_source":{"type":"ImageAsset"}},{"_id":"9cc0fdee-cdbe-458c-8436-ebc1d25d15d1","_source":{"type":"ImageAsset"}},{"_id":"bd1d0e2e-178b-4a0d-b5d8-36992b4bb5a0","_source":{"type":"ImageAsset"}},{"_id":"b81d9ad3-c679-4b60-a349-b438ed63b710","_source":{"type":"ImageAsset"}},{"_id":"5b12e32b-e12a-4d75-9128-3701a91fde9a","_source":{"type":"ImageAsset"}},{"_id":"7305c340-d9c3-4e52-be27-87d50b85164c","_source":{"type":"ImageAsset"}},{"_id":"d7cb3ecf-b26c-4359-953e-3bc8b57588c5","_source":{"type":"ImageAsset"}},{"_id":"7574823d-c2cf-43e4-b035-cac1f3408fad","_source":{"type":"ImageAsset"}},{"_id":"09906a35-0668-4f70-a57c-6e5215716393","_source":{"type":"ImageAsset"}},{"_id":"6dcb1afb-8984-48eb-b489-39fb6bac9f83","_source":{"type":"ImageAsset"}},{"_id":"21ba7594-7a16-4009-86bc-c406131ccb32","_source":{"type":"ImageAsset"}},{"_id":"c22c16ef-6692-4396-93de-34a2e7b8f951","_source":{"type":"ImageAsset"}},{"_id":"db6f78e3-3772-49f5-b12f-cc3df99c9e53","_source":{"type":"ImageAsset"}},{"_id":"7ef41d9f-1a95-434f-a395-60a6e1df168c","_source":{"type":"ImageAsset"}},{"_id":"07afc347-5cec-4aa3-81a5-671ef2359b32","_source":{"type":"ImageAsset"}},{"_id":"4d6fd831-edde-4895-80a6-5780b64829ec","_source":{"type":"ImageAsset"}},{"_id":"fb4375c6-cd63-4a4e-befd-b171f1d7b95e","_source":{"type":"ImageAsset"}},{"_id":"734ceadf-4e7f-4c9a-83a2-da51d81212eb","_source":{"type":"ImageAsset"}},{"_id":"b0c9f884-6b0d-4a8b-b2f5-25ebc28dfe32","_source":{"type":"ImageAsset"}},{"_id":"b27bbec1-f8b8-4fbf-89da-f1ebdf96524b","_source":{"type":"ImageAsset"}},{"_id":"ae009c0a-3090-4b29-beaf-535fac7e0446","_source":{"type":"ImageAsset"}},{"_id":"5f0db89a-7fca-45d6-9703-a6cded757f0b","_source":{"type":"ImageAsset"}},{"_id":"1a2c060a-f1a2-41f4-a245-76d50752b98f","_source":{"type":"ImageAsset"}},{"_id":"f4833b8d-0f09-442f-a88e-e5b657c0d6c2","_source":{"type":"ImageAsset"}},{"_id":"9a9943c0-a65e-4f59-959c-e9013eba57fd","_source":{"type":"ImageAsset"}},{"_id":"3e530120-c6f8-471b-abd8-1cd817beb5e9","_source":{"type":"ImageAsset"}},{"_id":"e3ee386d-49e0-4dae-8497-9958a210d4bf","_source":{"type":"ImageAsset"}},{"_id":"931fea3e-1dba-41f4-802e-67731eaf066e","_source":{"type":"ImageAsset"}},{"_id":"dec8db7c-ecff-41a0-8a2b-534d808ce331","_source":{"type":"ImageAsset"}},{"_id":"527f8b52-92f9-4888-9c11-87ea8e71c5e3","_source":{"type":"ImageAsset"}},{"_id":"ce2cb77d-cec9-4e0a-9c89-b4fa12899fbd","_source":{"type":"ImageAsset"}},{"_id":"1aaa4fb6-811e-472b-a019-96984744390c","_source":{"type":"ImageAsset"}},{"_id":"87a146b2-8a8d-4d68-9636-f18299e0c8fe","_source":{"type":"ImageAsset"}},{"_id":"1a63688c-daf7-4cc7-bcbf-2dd51d6f98e9","_source":{"type":"ImageAsset"}},{"_id":"99e7026b-4435-4ab1-963b-206229930214","_source":{"type":"ImageAsset"}},{"_id":"c502c598-8610-418a-9d10-e0575d3e31b3","_source":{"type":"ImageAsset"}},{"_id":"c2e9b4ef-0418-489c-8ffe-921f403b81db","_source":{"type":"ImageAsset"}},{"_id":"214aecfc-d5aa-41c4-9f87-d0c857062b4a","_source":{"type":"ImageAsset"}},{"_id":"64773c74-4096-4d96-9b36-984e5dcbf432","_source":{"type":"ImageAsset"}},{"_id":"20b2ae93-c2a1-4657-a5d9-c56fba1c8392","_source":{"type":"ImageAsset"}},{"_id":"645b97f1-3755-4702-b44b-7647b47bb65b","_source":{"type":"ImageAsset"}},{"_id":"531d331e-28cc-40ba-bdc5-22f694f4a77c","_source":{"type":"ImageAsset"}},{"_id":"c2d64bcf-c5c5-4b23-bf21-040252f9f605","_source":{"type":"ImageAsset"}},{"_id":"c35e45c1-0a10-4309-9111-0f8059c1d491","_source":{"type":"ImageAsset"}},{"_id":"0c9bff7f-9524-4d9e-b6a7-b1491ad8bf1f","_source":{"type":"ImageAsset"}},{"_id":"4a302de2-2c6e-43ff-ad5a-b9b7ab45032e","_source":{"type":"ImageAsset"}},{"_id":"98e0c3e0-cea2-4174-99e1-d2cbf10f7b00","_source":{"type":"ImageAsset"}},{"_id":"c1e8eefd-5e3a-4f8f-8a95-1fdcc24fc473","_source":{"type":"ImageAsset"}},{"_id":"10b2a298-69e0-422c-bbc8-acca14e9a14e","_source":{"type":"ImageAsset"}},{"_id":"23f6f3cb-fca9-4b11-9181-9224da1514bb","_source":{"type":"ImageAsset"}},{"_id":"2f338a4e-3cc5-4f9a-b9d4-d2c6d9299c63","_source":{"type":"ImageAsset"}},{"_id":"5e577863-ea30-46a7-b92b-ceeea6253bd4","_source":{"type":"ImageAsset"}},{"_id":"329a4fbb-4189-45b7-974e-edfbd4804625","_source":{"type":"ImageAsset"}},{"_id":"708433cf-223f-4251-a624-e8ddf5df35ac","_source":{"type":"ImageAsset"}},{"_id":"c6b7f38b-8319-4acc-b24c-782b880a2d1c","_source":{"type":"ImageAsset"}},{"_id":"9a9f7c0b-b5ca-49ec-8a75-cea0e40ab30f","_source":{"type":"ImageAsset"}},{"_id":"c10fd639-a543-483e-9454-88ff8306800b","_source":{"type":"ImageAsset"}},{"_id":"94d16b64-b724-4a85-bf4c-c44fe3cddfaf","_source":{"type":"ImageAsset"}},{"_id":"625c2c04-6c14-400b-a1e1-c6cacb2d315f","_source":{"type":"ImageAsset"}},{"_id":"5f16bcdd-4a76-4078-82bd-20f000fd257e","_source":{"type":"ImageAsset"}},{"_id":"b5c3f4b2-cb01-4c02-869b-1048ebcab322","_source":{"type":"ImageAsset"}},{"_id":"14fd36a0-4613-468b-9bd0-ff0dc1772d1d","_source":{"type":"ImageAsset"}},{"_id":"f59ba4bc-8bf5-4385-9b9d-6861b5d5909a","_source":{"type":"ImageAsset"}},{"_id":"7b8ffff5-739e-4a2a-ae61-30d03d2f98fc","_source":{"type":"ImageAsset"}},{"_id":"79c6253b-92f9-4f31-9892-d61a4204585b","_source":{"type":"ImageAsset"}},{"_id":"356338b8-a58f-4f44-9a4b-01c4e35d7809","_source":{"type":"ImageAsset"}},{"_id":"29bdb0e4-9ec0-4a33-8ac3-034f522b1190","_source":{"type":"ImageAsset"}},{"_id":"0b5ee649-c24a-4559-a89a-493daa997ea7","_source":{"type":"ImageAsset"}},{"_id":"c505be6c-e98d-4adf-bab4-85e005e64279","_source":{"type":"ImageAsset"}},{"_id":"3dcfa89e-6924-4fe4-b581-6c2c0eef1bc6","_source":{"type":"ImageAsset"}},{"_id":"ff8d6998-ef81-4aa7-b501-a18cb041b9e0","_source":{"type":"ImageAsset"}},{"_id":"c07af570-5617-411c-8e75-b01f618157f2","_source":{"type":"ImageAsset"}},{"_id":"8e9889f7-86a5-4160-b4cf-ec4e0b19279a","_source":{"type":"ImageAsset"}},{"_id":"1d034c33-6121-453b-8f9c-194b39ada3aa","_source":{"type":"ImageAsset"}},{"_id":"fffcce23-3df3-49fb-b76f-4383ec0ebc6d","_source":{"type":"ImageAsset"}},{"_id":"a92cf2af-ceeb-40ac-8121-8fdaa0e70825","_source":{"type":"ImageAsset"}},{"_id":"246c17ee-0c32-45eb-8407-67333145a2f1","_source":{"type":"ImageAsset"}},{"_id":"a9220466-1d8a-48cb-b26f-22b35b0769ef","_source":{"type":"ImageAsset"}},{"_id":"f315a6e7-4bfb-467c-97bf-63054a14dfd5","_source":{"type":"ImageAsset"}},{"_id":"3323257f-6104-429e-8cbd-b044a8bcf90e","_source":{"type":"ImageAsset"}},{"_id":"bd8b981f-4681-4fda-a4d3-c6b840039ae4","_source":{"type":"ImageAsset"}},{"_id":"7b25161a-2824-40be-8ac3-7201881f1afe","_source":{"type":"ImageAsset"}},{"_id":"fb54fb44-0d22-4220-8d00-23443708edab","_source":{"type":"ImageAsset"}},{"_id":"b7b3bde9-6d75-4ae5-90e7-817887ac510b","_source":{"type":"ImageAsset"}},{"_id":"c6300eb5-b0df-4b7d-b0ba-954b7dbf75c2","_source":{"type":"ImageAsset"}},{"_id":"613c117b-f781-453a-a79a-7d846ccccfa2","_source":{"type":"ImageAsset"}},{"_id":"6ba4e055-04b1-467d-a994-1bb712aabb42","_source":{"type":"ImageAsset"}},{"_id":"f0d2146d-8eb9-4a03-910e-9f6dc18ab512","_source":{"type":"ImageAsset"}},{"_id":"b369f200-f158-4f82-bee0-f205441758e1","_source":{"type":"ImageAsset"}},{"_id":"cfe4b256-17f6-4c76-b926-e8fbbf3e164c","_source":{"type":"ImageAsset"}},{"_id":"c8e36496-6a25-42d5-8075-082d2d33400d","_source":{"type":"ImageAsset"}},{"_id":"b85ead4d-b44f-4537-9a18-8c7f580d3be4","_source":{"type":"ImageAsset"}},{"_id":"084a3c4d-faaf-4264-ac87-621ad3af5160","_source":{"type":"ImageAsset"}},{"_id":"05c50984-019b-4bbe-a173-f055533cc943","_source":{"type":"ImageAsset"}},{"_id":"f748b94d-6d27-4892-b154-2a36f018fc40","_source":{"type":"ImageAsset"}},{"_id":"bfc1c3f6-fa47-412d-b258-01a64a20cdc9","_source":{"type":"ImageAsset"}},{"_id":"c43ac98a-e14d-42c5-900d-78ca9a0f1572","_source":{"type":"ImageAsset"}},{"_id":"14d05ec4-fe3b-4c72-87f9-0cd64d24d587","_source":{"type":"ImageAsset"}},{"_id":"b7fe4647-881e-48eb-a128-d101e33b7213","_source":{"type":"ImageAsset"}},{"_id":"7f7ab5b7-5989-4f26-8e7e-75d35282d4b8","_source":{"type":"ImageAsset"}},{"_id":"c5070294-7ed8-4787-bcd5-d5794db853b0","_source":{"type":"ImageAsset"}}]},"suggest":{"autocorrect":[{"text":"nature","offset":0,"length":6,"options":[]}],"did_you_mean":[{"text":"Nature","offset":0,"length":6,"options":[]}]},"status":200},{"hits":{"hits":[{"_id":"e2f50f7e-7c09-4c6d-9333-0f19541cf877","_source":{"type":"VideoAsset"}},{"_id":"7d8b3010-610a-4684-ae2f-58a482c24267","_source":{"type":"VideoAsset"}}]},"status":200},{"status":200}]}
web-service_1         | [2020-05-08 23:05:47 +0000] [265] [web.model_search] [DEBUG] results: {'responses': [{'status': 200, 'suggest': {'did_you_mean': [{'length': 6, 'offset': 0, 'options': [], 'text': 'Nature'}], 'autocorrect': [{'length': 6, 'offset': 0, 'options': [], 'text': 'nature'}]}, 'hits': {'hits': [{'_id': '72c208df-4fad-49f6-bf28-a1ae7c4682db', '_source': {'type': 'VideoAsset'}}, {'_id': 'b2fa31bf-1b8e-41e4-b7e2-dda646171c08', '_source': {'type': 'VideoAsset'}}, {'_id': '1a49d595-46b5-42cf-94ca-c21523c9afaa', '_source': {'type': 'VideoAsset'}}, {'_id': '723084f5-0d54-4f55-8098-9b40eabc7c2e', '_source': {'type': 'VideoAsset'}}, {'_id': 'bd9f9de4-1b9e-4840-8c25-2a7acb300497', '_source': {'type': 'VideoAsset'}}, {'_id': '13f53d83-4a4d-41c1-a9a1-175bf10c3821', '_source': {'type': 'VideoAsset'}}, {'_id': '8956ec13-f0ad-47a3-a36f-cfae0b1be9d2', '_source': {'type': 'VideoAsset'}}, {'_id': '4451c02a-11ec-457e-a78d-4f6bae0d7113', '_source': {'type': 'VideoAsset'}}, {'_id': '07b100e3-9e1a-4ce3-bb20-09da7aec5e3c', '_source': {'type': 'VideoAsset'}}, {'_id': '8a6f424c-dffb-4a52-897d-f385ac2334fe', '_source': {'type': 'VideoAsset'}}, {'_id': 'f10fcda5-3532-49d6-8690-50ec108ee05e', '_source': {'type': 'VideoAsset'}}, {'_id': '0b6e7df0-95aa-4145-b50f-cc76a7098354', '_source': {'type': 'VideoAsset'}}, {'_id': 'b2c09d7d-d8cd-4a11-907a-b0561bf6a34e', '_source': {'type': 'VideoAsset'}}, {'_id': 'e02c4379-0f7f-41a0-92dc-210f1022f3c4', '_source': {'type': 'VideoAsset'}}, {'_id': 'aabe81d9-7882-4d91-9012-191e4a526edc', '_source': {'type': 'VideoAsset'}}, {'_id': '5610e39f-479d-4a39-b67d-c05de86bd8d3', '_source': {'type': 'VideoAsset'}}, {'_id': '9b8d66c4-7197-4a04-a645-5e4e7da7b311', '_source': {'type': 'VideoAsset'}}, {'_id': '205ee663-4a5c-45ae-94c9-fe26e23aff62', '_source': {'type': 'VideoAsset'}}, {'_id': 'd80fdf6e-0531-46c1-b5e4-1a515c9a1fe1', '_source': {'type': 'VideoAsset'}}, {'_id': 'cd091a7f-a244-411a-8b03-ff771e631fa5', '_source': {'type': 'VideoAsset'}}, {'_id': 'e58e458b-d144-44c3-b851-fd28df60b6f7', '_source': {'type': 'VideoAsset'}}, {'_id': 'b4488ab0-c818-49ff-9325-cf3e1a0a7800', '_source': {'type': 'VideoAsset'}}, {'_id': 'e907e8fc-f929-4450-aa37-9dadd4062d5f', '_source': {'type': 'VideoAsset'}}, {'_id': '8fbcbfbd-8748-4459-b11d-e63f6cce4b99', '_source': {'type': 'VideoAsset'}}, {'_id': '837323ea-d664-49a0-aa16-b954184405c9', '_source': {'type': 'VideoAsset'}}, {'_id': '65bd495e-f207-4c73-800e-92c600c870e9', '_source': {'type': 'VideoAsset'}}, {'_id': '22acb077-b854-448e-a775-9704e66879fa', '_source': {'type': 'VideoAsset'}}, {'_id': '745b1022-583b-4b47-b28f-64eeb3eba573', '_source': {'type': 'ImageAsset'}}, {'_id': '35909c80-26e7-46cf-b030-73ac437bd0bf', '_source': {'type': 'ImageAsset'}}, {'_id': '0074129d-708d-430b-85f9-fdfca96aab33', '_source': {'type': 'ImageAsset'}}, {'_id': '9cc0fdee-cdbe-458c-8436-ebc1d25d15d1', '_source': {'type': 'ImageAsset'}}, {'_id': 'bd1d0e2e-178b-4a0d-b5d8-36992b4bb5a0', '_source': {'type': 'ImageAsset'}}, {'_id': 'b81d9ad3-c679-4b60-a349-b438ed63b710', '_source': {'type': 'ImageAsset'}}, {'_id': '5b12e32b-e12a-4d75-9128-3701a91fde9a', '_source': {'type': 'ImageAsset'}}, {'_id': '7305c340-d9c3-4e52-be27-87d50b85164c', '_source': {'type': 'ImageAsset'}}, {'_id': 'd7cb3ecf-b26c-4359-953e-3bc8b57588c5', '_source': {'type': 'ImageAsset'}}, {'_id': '7574823d-c2cf-43e4-b035-cac1f3408fad', '_source': {'type': 'ImageAsset'}}, {'_id': '09906a35-0668-4f70-a57c-6e5215716393', '_source': {'type': 'ImageAsset'}}, {'_id': '6dcb1afb-8984-48eb-b489-39fb6bac9f83', '_source': {'type': 'ImageAsset'}}, {'_id': '21ba7594-7a16-4009-86bc-c406131ccb32', '_source': {'type': 'ImageAsset'}}, {'_id': 'c22c16ef-6692-4396-93de-34a2e7b8f951', '_source': {'type': 'ImageAsset'}}, {'_id': 'db6f78e3-3772-49f5-b12f-cc3df99c9e53', '_source': {'type': 'ImageAsset'}}, {'_id': '7ef41d9f-1a95-434f-a395-60a6e1df168c', '_source': {'type': 'ImageAsset'}}, {'_id': '07afc347-5cec-4aa3-81a5-671ef2359b32', '_source': {'type': 'ImageAsset'}}, {'_id': '4d6fd831-edde-4895-80a6-5780b64829ec', '_source': {'type': 'ImageAsset'}}, {'_id': 'fb4375c6-cd63-4a4e-befd-b171f1d7b95e', '_source': {'type': 'ImageAsset'}}, {'_id': '734ceadf-4e7f-4c9a-83a2-da51d81212eb', '_source': {'type': 'ImageAsset'}}, {'_id': 'b0c9f884-6b0d-4a8b-b2f5-25ebc28dfe32', '_source': {'type': 'ImageAsset'}}, {'_id': 'b27bbec1-f8b8-4fbf-89da-f1ebdf96524b', '_source': {'type': 'ImageAsset'}}, {'_id': 'ae009c0a-3090-4b29-beaf-535fac7e0446', '_source': {'type': 'ImageAsset'}}, {'_id': '5f0db89a-7fca-45d6-9703-a6cded757f0b', '_source': {'type': 'ImageAsset'}}, {'_id': '1a2c060a-f1a2-41f4-a245-76d50752b98f', '_source': {'type': 'ImageAsset'}}, {'_id': 'f4833b8d-0f09-442f-a88e-e5b657c0d6c2', '_source': {'type': 'ImageAsset'}}, {'_id': '9a9943c0-a65e-4f59-959c-e9013eba57fd', '_source': {'type': 'ImageAsset'}}, {'_id': '3e530120-c6f8-471b-abd8-1cd817beb5e9', '_source': {'type': 'ImageAsset'}}, {'_id': 'e3ee386d-49e0-4dae-8497-9958a210d4bf', '_source': {'type': 'ImageAsset'}}, {'_id': '931fea3e-1dba-41f4-802e-67731eaf066e', '_source': {'type': 'ImageAsset'}}, {'_id': 'dec8db7c-ecff-41a0-8a2b-534d808ce331', '_source': {'type': 'ImageAsset'}}, {'_id': '527f8b52-92f9-4888-9c11-87ea8e71c5e3', '_source': {'type': 'ImageAsset'}}, {'_id': 'ce2cb77d-cec9-4e0a-9c89-b4fa12899fbd', '_source': {'type': 'ImageAsset'}}, {'_id': '1aaa4fb6-811e-472b-a019-96984744390c', '_source': {'type': 'ImageAsset'}}, {'_id': '87a146b2-8a8d-4d68-9636-f18299e0c8fe', '_source': {'type': 'ImageAsset'}}, {'_id': '1a63688c-daf7-4cc7-bcbf-2dd51d6f98e9', '_source': {'type': 'ImageAsset'}}, {'_id': '99e7026b-4435-4ab1-963b-206229930214', '_source': {'type': 'ImageAsset'}}, {'_id': 'c502c598-8610-418a-9d10-e0575d3e31b3', '_source': {'type': 'ImageAsset'}}, {'_id': 'c2e9b4ef-0418-489c-8ffe-921f403b81db', '_source': {'type': 'ImageAsset'}}, {'_id': '214aecfc-d5aa-41c4-9f87-d0c857062b4a', '_source': {'type': 'ImageAsset'}}, {'_id': '64773c74-4096-4d96-9b36-984e5dcbf432', '_source': {'type': 'ImageAsset'}}, {'_id': '20b2ae93-c2a1-4657-a5d9-c56fba1c8392', '_source': {'type': 'ImageAsset'}}, {'_id': '645b97f1-3755-4702-b44b-7647b47bb65b', '_source': {'type': 'ImageAsset'}}, {'_id': '531d331e-28cc-40ba-bdc5-22f694f4a77c', '_source': {'type': 'ImageAsset'}}, {'_id': 'c2d64bcf-c5c5-4b23-bf21-040252f9f605', '_source': {'type': 'ImageAsset'}}, {'_id': 'c35e45c1-0a10-4309-9111-0f8059c1d491', '_source': {'type': 'ImageAsset'}}, {'_id': '0c9bff7f-9524-4d9e-b6a7-b1491ad8bf1f', '_source': {'type': 'ImageAsset'}}, {'_id': '4a302de2-2c6e-43ff-ad5a-b9b7ab45032e', '_source': {'type': 'ImageAsset'}}, {'_id': '98e0c3e0-cea2-4174-99e1-d2cbf10f7b00', '_source': {'type': 'ImageAsset'}}, {'_id': 'c1e8eefd-5e3a-4f8f-8a95-1fdcc24fc473', '_source': {'type': 'ImageAsset'}}, {'_id': '10b2a298-69e0-422c-bbc8-acca14e9a14e', '_source': {'type': 'ImageAsset'}}, {'_id': '23f6f3cb-fca9-4b11-9181-9224da1514bb', '_source': {'type': 'ImageAsset'}}, {'_id': '2f338a4e-3cc5-4f9a-b9d4-d2c6d9299c63', '_source': {'type': 'ImageAsset'}}, {'_id': '5e577863-ea30-46a7-b92b-ceeea6253bd4', '_source': {'type': 'ImageAsset'}}, {'_id': '329a4fbb-4189-45b7-974e-edfbd4804625', '_source': {'type': 'ImageAsset'}}, {'_id': '708433cf-223f-4251-a624-e8ddf5df35ac', '_source': {'type': 'ImageAsset'}}, {'_id': 'c6b7f38b-8319-4acc-b24c-782b880a2d1c', '_source': {'type': 'ImageAsset'}}, {'_id': '9a9f7c0b-b5ca-49ec-8a75-cea0e40ab30f', '_source': {'type': 'ImageAsset'}}, {'_id': 'c10fd639-a543-483e-9454-88ff8306800b', '_source': {'type': 'ImageAsset'}}, {'_id': '94d16b64-b724-4a85-bf4c-c44fe3cddfaf', '_source': {'type': 'ImageAsset'}}, {'_id': '625c2c04-6c14-400b-a1e1-c6cacb2d315f', '_source': {'type': 'ImageAsset'}}, {'_id': '5f16bcdd-4a76-4078-82bd-20f000fd257e', '_source': {'type': 'ImageAsset'}}, {'_id': 'b5c3f4b2-cb01-4c02-869b-1048ebcab322', '_source': {'type': 'ImageAsset'}}, {'_id': '14fd36a0-4613-468b-9bd0-ff0dc1772d1d', '_source': {'type': 'ImageAsset'}}, {'_id': 'f59ba4bc-8bf5-4385-9b9d-6861b5d5909a', '_source': {'type': 'ImageAsset'}}, {'_id': '7b8ffff5-739e-4a2a-ae61-30d03d2f98fc', '_source': {'type': 'ImageAsset'}}, {'_id': '79c6253b-92f9-4f31-9892-d61a4204585b', '_source': {'type': 'ImageAsset'}}, {'_id': '356338b8-a58f-4f44-9a4b-01c4e35d7809', '_source': {'type': 'ImageAsset'}}, {'_id': '29bdb0e4-9ec0-4a33-8ac3-034f522b1190', '_source': {'type': 'ImageAsset'}}, {'_id': '0b5ee649-c24a-4559-a89a-493daa997ea7', '_source': {'type': 'ImageAsset'}}, {'_id': 'c505be6c-e98d-4adf-bab4-85e005e64279', '_source': {'type': 'ImageAsset'}}, {'_id': '3dcfa89e-6924-4fe4-b581-6c2c0eef1bc6', '_source': {'type': 'ImageAsset'}}, {'_id': 'ff8d6998-ef81-4aa7-b501-a18cb041b9e0', '_source': {'type': 'ImageAsset'}}, {'_id': 'c07af570-5617-411c-8e75-b01f618157f2', '_source': {'type': 'ImageAsset'}}, {'_id': '8e9889f7-86a5-4160-b4cf-ec4e0b19279a', '_source': {'type': 'ImageAsset'}}, {'_id': '1d034c33-6121-453b-8f9c-194b39ada3aa', '_source': {'type': 'ImageAsset'}}, {'_id': 'fffcce23-3df3-49fb-b76f-4383ec0ebc6d', '_source': {'type': 'ImageAsset'}}, {'_id': 'a92cf2af-ceeb-40ac-8121-8fdaa0e70825', '_source': {'type': 'ImageAsset'}}, {'_id': '246c17ee-0c32-45eb-8407-67333145a2f1', '_source': {'type': 'ImageAsset'}}, {'_id': 'a9220466-1d8a-48cb-b26f-22b35b0769ef', '_source': {'type': 'ImageAsset'}}, {'_id': 'f315a6e7-4bfb-467c-97bf-63054a14dfd5', '_source': {'type': 'ImageAsset'}}, {'_id': '3323257f-6104-429e-8cbd-b044a8bcf90e', '_source': {'type': 'ImageAsset'}}, {'_id': 'bd8b981f-4681-4fda-a4d3-c6b840039ae4', '_source': {'type': 'ImageAsset'}}, {'_id': '7b25161a-2824-40be-8ac3-7201881f1afe', '_source': {'type': 'ImageAsset'}}, {'_id': 'fb54fb44-0d22-4220-8d00-23443708edab', '_source': {'type': 'ImageAsset'}}, {'_id': 'b7b3bde9-6d75-4ae5-90e7-817887ac510b', '_source': {'type': 'ImageAsset'}}, {'_id': 'c6300eb5-b0df-4b7d-b0ba-954b7dbf75c2', '_source': {'type': 'ImageAsset'}}, {'_id': '613c117b-f781-453a-a79a-7d846ccccfa2', '_source': {'type': 'ImageAsset'}}, {'_id': '6ba4e055-04b1-467d-a994-1bb712aabb42', '_source': {'type': 'ImageAsset'}}, {'_id': 'f0d2146d-8eb9-4a03-910e-9f6dc18ab512', '_source': {'type': 'ImageAsset'}}, {'_id': 'b369f200-f158-4f82-bee0-f205441758e1', '_source': {'type': 'ImageAsset'}}, {'_id': 'cfe4b256-17f6-4c76-b926-e8fbbf3e164c', '_source': {'type': 'ImageAsset'}}, {'_id': 'c8e36496-6a25-42d5-8075-082d2d33400d', '_source': {'type': 'ImageAsset'}}, {'_id': 'b85ead4d-b44f-4537-9a18-8c7f580d3be4', '_source': {'type': 'ImageAsset'}}, {'_id': '084a3c4d-faaf-4264-ac87-621ad3af5160', '_source': {'type': 'ImageAsset'}}, {'_id': '05c50984-019b-4bbe-a173-f055533cc943', '_source': {'type': 'ImageAsset'}}, {'_id': 'f748b94d-6d27-4892-b154-2a36f018fc40', '_source': {'type': 'ImageAsset'}}, {'_id': 'bfc1c3f6-fa47-412d-b258-01a64a20cdc9', '_source': {'type': 'ImageAsset'}}, {'_id': 'c43ac98a-e14d-42c5-900d-78ca9a0f1572', '_source': {'type': 'ImageAsset'}}, {'_id': '14d05ec4-fe3b-4c72-87f9-0cd64d24d587', '_source': {'type': 'ImageAsset'}}, {'_id': 'b7fe4647-881e-48eb-a128-d101e33b7213', '_source': {'type': 'ImageAsset'}}, {'_id': '7f7ab5b7-5989-4f26-8e7e-75d35282d4b8', '_source': {'type': 'ImageAsset'}}, {'_id': 'c5070294-7ed8-4787-bcd5-d5794db853b0', '_source': {'type': 'ImageAsset'}}]}}, {'status': 200, 'hits': {'hits': [{'_id': 'e2f50f7e-7c09-4c6d-9333-0f19541cf877', '_source': {'type': 'VideoAsset'}}, {'_id': '7d8b3010-610a-4684-ae2f-58a482c24267', '_source': {'type': 'VideoAsset'}}]}}, {'status': 200}]}
pgbouncer-service_1   | 2020-05-08 23:05:47.167 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40938 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:47.179 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40944 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:47 +0000] [265] [incoming_requests] [DEBUG] {"get": {}, "post": {}, "time": "2020-05-08T23:05:47.181957+00:00", "path": "/api/clicklogsquery/"}
web-service_1         | {"severity": "INFO", "textPayload": {"user": 1, "time": "2020-05-08T23:05:47.189071Z", "video_id": 45, "log_name": "media_search_v2", "action": "Q", "query": "Nature", "processed_query": "Nature", "corrected_query": "Nature", "page": 1, "results": [{"type": "video", "uuid": "72c208df-4fad-49f6-bf28-a1ae7c4682db"}, {"type": "video", "uuid": "b2fa31bf-1b8e-41e4-b7e2-dda646171c08"}, {"type": "video", "uuid": "1a49d595-46b5-42cf-94ca-c21523c9afaa"}, {"type": "video", "uuid": "723084f5-0d54-4f55-8098-9b40eabc7c2e"}, {"type": "video", "uuid": "bd9f9de4-1b9e-4840-8c25-2a7acb300497"}, {"type": "video", "uuid": "13f53d83-4a4d-41c1-a9a1-175bf10c3821"}, {"type": "video", "uuid": "8956ec13-f0ad-47a3-a36f-cfae0b1be9d2"}, {"type": "video", "uuid": "4451c02a-11ec-457e-a78d-4f6bae0d7113"}, {"type": "video", "uuid": "07b100e3-9e1a-4ce3-bb20-09da7aec5e3c"}, {"type": "video", "uuid": "8a6f424c-dffb-4a52-897d-f385ac2334fe"}, {"type": "video", "uuid": "f10fcda5-3532-49d6-8690-50ec108ee05e"}, {"type": "video", "uuid": "0b6e7df0-95aa-4145-b50f-cc76a7098354"}], "results_shape": [-1, 2], "language": "en", "filter": {"marketplace_enabled": true}}, "name": "click_logs"}
pgbouncer-service_1   | 2020-05-08 23:05:47.194 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40944 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:47.255 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40950 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:47 +0000] [264] [incoming_requests] [DEBUG] {"get": {"filter": "videos,photos,editorial", "source": "recommended", "q": "Nature", "autocorrect": "true", "video_duration": "7", "boost_terms": "[]", "page": "2", "sort": "", "did_you_mean": "true"}, "post": {}, "time": "2020-05-08T23:05:47.257414+00:00", "path": "/api/background-assets/"}
base_worker_1         | [2020-05-08 23:05:47 +0000] [7] [amqp] [DEBUG] heartbeat_tick : for connection 4b38861564db4d128568a3020245a256
base_worker_1         | [2020-05-08 23:05:47 +0000] [7] [amqp] [DEBUG] heartbeat_tick : Prev sent/recv: 32/120, now - 32/150, monotonic - 109619.015970334, last_heartbeat_sent - 109559.011306948, heartbeat int. - 60 for connection 4b38861564db4d128568a3020245a256
base_worker_1         | [2020-05-08 23:05:47 +0000] [7] [amqp] [DEBUG] heartbeat_tick: sending heartbeat for connection 4b38861564db4d128568a3020245a256
web-service_1         | 
web-service_1         | [2020-05-08 23:05:51 +0000] [264] [elasticsearch] [INFO] POST http://elasticsearch-v3:9200/media_43tc/_msearch?filter_path=responses.status%2Cresponses.hits.hits._id%2Cresponses.hits.hits._source.type%2Cresponses.hits.hits.matched_queries%2Cresponses.hits.hits.fields%2Cresponses.suggest%2Cresponses.hits.hits._source.query [status:200 request:0.109s]
web-service_1         | [2020-05-08 23:05:51 +0000] [264] [elasticsearch] [DEBUG] > {"index": "media_43tc"}
web-service_1         | {"from": 0, "query": {"bool": {"filter": [], "must_not": [{"term": {"src": 0}}, {"term": {"src": 1}}, {"term": {"src": 2}}, {"term": {"src": 3}}, {"term": {"src": 26}}, {"term": {"license": "user_private"}}, {"bool": {"must": [{"term": {"src": 16}}, {"bool": {"must_not": {"terms": {"getty_collection_code": ["NEW", "SPO", "ENT", "ARP", "AFP", "AFE", "GIEF", "WIV", "GIS", "SKP", "CRV", "ISF", "VTV"]}}}}]}}, {"term": {"src": 23}}, {"term": {"src": 24}}, {"term": {"src": 16}}, {"term": {"src": 25}}, {"term": {"src": 26}}, {"term": {"editorial": true}}, {"term": {"src": 16}}, {"term": {"src": 25}}, {"term": {"src": 26}}], "should": [{"term": {"type": {"value": "VideoAsset", "boost": 2}}}], "must": [{"query_string": {"default_field": "jam", "query": "Nature", "minimum_should_match": "50%"}}]}}, "size": 1000}
web-service_1         | {"index": "media_43tc"}
web-service_1         | {"from": 2, "query": {"bool": {"filter": [], "must_not": [{"term": {"src": 0}}, {"term": {"src": 1}}, {"term": {"src": 2}}, {"term": {"src": 3}}, {"term": {"src": 26}}, {"term": {"license": "user_private"}}, {"bool": {"must": [{"term": {"src": 16}}, {"bool": {"must_not": {"terms": {"getty_collection_code": ["NEW", "SPO", "ENT", "ARP", "AFP", "AFE", "GIEF", "WIV", "GIS", "SKP", "CRV", "ISF", "VTV"]}}}}]}}, {"term": {"src": 0}}, {"term": {"src": 1}}, {"term": {"src": 2}}, {"term": {"src": 3}}, {"term": {"src": 4}}, {"term": {"src": 5}}, {"term": {"src": 6}}, {"term": {"src": 7}}, {"term": {"src": 8}}, {"term": {"src": 9}}, {"term": {"src": 10}}, {"term": {"src": 11}}, {"term": {"src": 12}}, {"term": {"src": 13}}, {"term": {"src": 14}}, {"term": {"src": 15}}, {"term": {"src": 17}}, {"term": {"src": 18}}, {"term": {"src": 19}}, {"term": {"src": 20}}, {"term": {"src": 21}}, {"term": {"src": 22}}, {"term": {"editorial": true}}], "should": [{"term": {"type": {"value": "VideoAsset", "boost": 2}}}], "must": [{"query_string": {"default_field": "jam", "query": "Nature", "minimum_should_match": "50%"}}]}}, "size": 2}
web-service_1         | 
web-service_1         | [2020-05-08 23:05:51 +0000] [264] [elasticsearch] [DEBUG] < {"responses":[{"hits":{"hits":[{"_id":"72c208df-4fad-49f6-bf28-a1ae7c4682db","_source":{"type":"VideoAsset"}},{"_id":"b2fa31bf-1b8e-41e4-b7e2-dda646171c08","_source":{"type":"VideoAsset"}},{"_id":"1a49d595-46b5-42cf-94ca-c21523c9afaa","_source":{"type":"VideoAsset"}},{"_id":"723084f5-0d54-4f55-8098-9b40eabc7c2e","_source":{"type":"VideoAsset"}},{"_id":"bd9f9de4-1b9e-4840-8c25-2a7acb300497","_source":{"type":"VideoAsset"}},{"_id":"13f53d83-4a4d-41c1-a9a1-175bf10c3821","_source":{"type":"VideoAsset"}},{"_id":"8956ec13-f0ad-47a3-a36f-cfae0b1be9d2","_source":{"type":"VideoAsset"}},{"_id":"4451c02a-11ec-457e-a78d-4f6bae0d7113","_source":{"type":"VideoAsset"}},{"_id":"07b100e3-9e1a-4ce3-bb20-09da7aec5e3c","_source":{"type":"VideoAsset"}},{"_id":"8a6f424c-dffb-4a52-897d-f385ac2334fe","_source":{"type":"VideoAsset"}},{"_id":"f10fcda5-3532-49d6-8690-50ec108ee05e","_source":{"type":"VideoAsset"}},{"_id":"0b6e7df0-95aa-4145-b50f-cc76a7098354","_source":{"type":"VideoAsset"}},{"_id":"b2c09d7d-d8cd-4a11-907a-b0561bf6a34e","_source":{"type":"VideoAsset"}},{"_id":"e02c4379-0f7f-41a0-92dc-210f1022f3c4","_source":{"type":"VideoAsset"}},{"_id":"aabe81d9-7882-4d91-9012-191e4a526edc","_source":{"type":"VideoAsset"}},{"_id":"5610e39f-479d-4a39-b67d-c05de86bd8d3","_source":{"type":"VideoAsset"}},{"_id":"9b8d66c4-7197-4a04-a645-5e4e7da7b311","_source":{"type":"VideoAsset"}},{"_id":"205ee663-4a5c-45ae-94c9-fe26e23aff62","_source":{"type":"VideoAsset"}},{"_id":"d80fdf6e-0531-46c1-b5e4-1a515c9a1fe1","_source":{"type":"VideoAsset"}},{"_id":"cd091a7f-a244-411a-8b03-ff771e631fa5","_source":{"type":"VideoAsset"}},{"_id":"e58e458b-d144-44c3-b851-fd28df60b6f7","_source":{"type":"VideoAsset"}},{"_id":"b4488ab0-c818-49ff-9325-cf3e1a0a7800","_source":{"type":"VideoAsset"}},{"_id":"e907e8fc-f929-4450-aa37-9dadd4062d5f","_source":{"type":"VideoAsset"}},{"_id":"8fbcbfbd-8748-4459-b11d-e63f6cce4b99","_source":{"type":"VideoAsset"}},{"_id":"837323ea-d664-49a0-aa16-b954184405c9","_source":{"type":"VideoAsset"}},{"_id":"65bd495e-f207-4c73-800e-92c600c870e9","_source":{"type":"VideoAsset"}},{"_id":"22acb077-b854-448e-a775-9704e66879fa","_source":{"type":"VideoAsset"}},{"_id":"745b1022-583b-4b47-b28f-64eeb3eba573","_source":{"type":"ImageAsset"}},{"_id":"35909c80-26e7-46cf-b030-73ac437bd0bf","_source":{"type":"ImageAsset"}},{"_id":"0074129d-708d-430b-85f9-fdfca96aab33","_source":{"type":"ImageAsset"}},{"_id":"9cc0fdee-cdbe-458c-8436-ebc1d25d15d1","_source":{"type":"ImageAsset"}},{"_id":"bd1d0e2e-178b-4a0d-b5d8-36992b4bb5a0","_source":{"type":"ImageAsset"}},{"_id":"b81d9ad3-c679-4b60-a349-b438ed63b710","_source":{"type":"ImageAsset"}},{"_id":"5b12e32b-e12a-4d75-9128-3701a91fde9a","_source":{"type":"ImageAsset"}},{"_id":"7305c340-d9c3-4e52-be27-87d50b85164c","_source":{"type":"ImageAsset"}},{"_id":"d7cb3ecf-b26c-4359-953e-3bc8b57588c5","_source":{"type":"ImageAsset"}},{"_id":"7574823d-c2cf-43e4-b035-cac1f3408fad","_source":{"type":"ImageAsset"}},{"_id":"09906a35-0668-4f70-a57c-6e5215716393","_source":{"type":"ImageAsset"}},{"_id":"6dcb1afb-8984-48eb-b489-39fb6bac9f83","_source":{"type":"ImageAsset"}},{"_id":"21ba7594-7a16-4009-86bc-c406131ccb32","_source":{"type":"ImageAsset"}},{"_id":"c22c16ef-6692-4396-93de-34a2e7b8f951","_source":{"type":"ImageAsset"}},{"_id":"db6f78e3-3772-49f5-b12f-cc3df99c9e53","_source":{"type":"ImageAsset"}},{"_id":"7ef41d9f-1a95-434f-a395-60a6e1df168c","_source":{"type":"ImageAsset"}},{"_id":"07afc347-5cec-4aa3-81a5-671ef2359b32","_source":{"type":"ImageAsset"}},{"_id":"4d6fd831-edde-4895-80a6-5780b64829ec","_source":{"type":"ImageAsset"}},{"_id":"fb4375c6-cd63-4a4e-befd-b171f1d7b95e","_source":{"type":"ImageAsset"}},{"_id":"734ceadf-4e7f-4c9a-83a2-da51d81212eb","_source":{"type":"ImageAsset"}},{"_id":"b0c9f884-6b0d-4a8b-b2f5-25ebc28dfe32","_source":{"type":"ImageAsset"}},{"_id":"b27bbec1-f8b8-4fbf-89da-f1ebdf96524b","_source":{"type":"ImageAsset"}},{"_id":"ae009c0a-3090-4b29-beaf-535fac7e0446","_source":{"type":"ImageAsset"}},{"_id":"5f0db89a-7fca-45d6-9703-a6cded757f0b","_source":{"type":"ImageAsset"}},{"_id":"1a2c060a-f1a2-41f4-a245-76d50752b98f","_source":{"type":"ImageAsset"}},{"_id":"f4833b8d-0f09-442f-a88e-e5b657c0d6c2","_source":{"type":"ImageAsset"}},{"_id":"9a9943c0-a65e-4f59-959c-e9013eba57fd","_source":{"type":"ImageAsset"}},{"_id":"3e530120-c6f8-471b-abd8-1cd817beb5e9","_source":{"type":"ImageAsset"}},{"_id":"e3ee386d-49e0-4dae-8497-9958a210d4bf","_source":{"type":"ImageAsset"}},{"_id":"931fea3e-1dba-41f4-802e-67731eaf066e","_source":{"type":"ImageAsset"}},{"_id":"dec8db7c-ecff-41a0-8a2b-534d808ce331","_source":{"type":"ImageAsset"}},{"_id":"527f8b52-92f9-4888-9c11-87ea8e71c5e3","_source":{"type":"ImageAsset"}},{"_id":"ce2cb77d-cec9-4e0a-9c89-b4fa12899fbd","_source":{"type":"ImageAsset"}},{"_id":"1aaa4fb6-811e-472b-a019-96984744390c","_source":{"type":"ImageAsset"}},{"_id":"87a146b2-8a8d-4d68-9636-f18299e0c8fe","_source":{"type":"ImageAsset"}},{"_id":"1a63688c-daf7-4cc7-bcbf-2dd51d6f98e9","_source":{"type":"ImageAsset"}},{"_id":"99e7026b-4435-4ab1-963b-206229930214","_source":{"type":"ImageAsset"}},{"_id":"c502c598-8610-418a-9d10-e0575d3e31b3","_source":{"type":"ImageAsset"}},{"_id":"c2e9b4ef-0418-489c-8ffe-921f403b81db","_source":{"type":"ImageAsset"}},{"_id":"214aecfc-d5aa-41c4-9f87-d0c857062b4a","_source":{"type":"ImageAsset"}},{"_id":"64773c74-4096-4d96-9b36-984e5dcbf432","_source":{"type":"ImageAsset"}},{"_id":"20b2ae93-c2a1-4657-a5d9-c56fba1c8392","_source":{"type":"ImageAsset"}},{"_id":"645b97f1-3755-4702-b44b-7647b47bb65b","_source":{"type":"ImageAsset"}},{"_id":"531d331e-28cc-40ba-bdc5-22f694f4a77c","_source":{"type":"ImageAsset"}},{"_id":"c2d64bcf-c5c5-4b23-bf21-040252f9f605","_source":{"type":"ImageAsset"}},{"_id":"c35e45c1-0a10-4309-9111-0f8059c1d491","_source":{"type":"ImageAsset"}},{"_id":"0c9bff7f-9524-4d9e-b6a7-b1491ad8bf1f","_source":{"type":"ImageAsset"}},{"_id":"4a302de2-2c6e-43ff-ad5a-b9b7ab45032e","_source":{"type":"ImageAsset"}},{"_id":"98e0c3e0-cea2-4174-99e1-d2cbf10f7b00","_source":{"type":"ImageAsset"}},{"_id":"c1e8eefd-5e3a-4f8f-8a95-1fdcc24fc473","_source":{"type":"ImageAsset"}},{"_id":"10b2a298-69e0-422c-bbc8-acca14e9a14e","_source":{"type":"ImageAsset"}},{"_id":"23f6f3cb-fca9-4b11-9181-9224da1514bb","_source":{"type":"ImageAsset"}},{"_id":"2f338a4e-3cc5-4f9a-b9d4-d2c6d9299c63","_source":{"type":"ImageAsset"}},{"_id":"5e577863-ea30-46a7-b92b-ceeea6253bd4","_source":{"type":"ImageAsset"}},{"_id":"329a4fbb-4189-45b7-974e-edfbd4804625","_source":{"type":"ImageAsset"}},{"_id":"708433cf-223f-4251-a624-e8ddf5df35ac","_source":{"type":"ImageAsset"}},{"_id":"c6b7f38b-8319-4acc-b24c-782b880a2d1c","_source":{"type":"ImageAsset"}},{"_id":"9a9f7c0b-b5ca-49ec-8a75-cea0e40ab30f","_source":{"type":"ImageAsset"}},{"_id":"c10fd639-a543-483e-9454-88ff8306800b","_source":{"type":"ImageAsset"}},{"_id":"94d16b64-b724-4a85-bf4c-c44fe3cddfaf","_source":{"type":"ImageAsset"}},{"_id":"625c2c04-6c14-400b-a1e1-c6cacb2d315f","_source":{"type":"ImageAsset"}},{"_id":"5f16bcdd-4a76-4078-82bd-20f000fd257e","_source":{"type":"ImageAsset"}},{"_id":"b5c3f4b2-cb01-4c02-869b-1048ebcab322","_source":{"type":"ImageAsset"}},{"_id":"14fd36a0-4613-468b-9bd0-ff0dc1772d1d","_source":{"type":"ImageAsset"}},{"_id":"f59ba4bc-8bf5-4385-9b9d-6861b5d5909a","_source":{"type":"ImageAsset"}},{"_id":"7b8ffff5-739e-4a2a-ae61-30d03d2f98fc","_source":{"type":"ImageAsset"}},{"_id":"79c6253b-92f9-4f31-9892-d61a4204585b","_source":{"type":"ImageAsset"}},{"_id":"356338b8-a58f-4f44-9a4b-01c4e35d7809","_source":{"type":"ImageAsset"}},{"_id":"29bdb0e4-9ec0-4a33-8ac3-034f522b1190","_source":{"type":"ImageAsset"}},{"_id":"0b5ee649-c24a-4559-a89a-493daa997ea7","_source":{"type":"ImageAsset"}},{"_id":"c505be6c-e98d-4adf-bab4-85e005e64279","_source":{"type":"ImageAsset"}},{"_id":"3dcfa89e-6924-4fe4-b581-6c2c0eef1bc6","_source":{"type":"ImageAsset"}},{"_id":"ff8d6998-ef81-4aa7-b501-a18cb041b9e0","_source":{"type":"ImageAsset"}},{"_id":"c07af570-5617-411c-8e75-b01f618157f2","_source":{"type":"ImageAsset"}},{"_id":"8e9889f7-86a5-4160-b4cf-ec4e0b19279a","_source":{"type":"ImageAsset"}},{"_id":"1d034c33-6121-453b-8f9c-194b39ada3aa","_source":{"type":"ImageAsset"}},{"_id":"fffcce23-3df3-49fb-b76f-4383ec0ebc6d","_source":{"type":"ImageAsset"}},{"_id":"a92cf2af-ceeb-40ac-8121-8fdaa0e70825","_source":{"type":"ImageAsset"}},{"_id":"246c17ee-0c32-45eb-8407-67333145a2f1","_source":{"type":"ImageAsset"}},{"_id":"a9220466-1d8a-48cb-b26f-22b35b0769ef","_source":{"type":"ImageAsset"}},{"_id":"f315a6e7-4bfb-467c-97bf-63054a14dfd5","_source":{"type":"ImageAsset"}},{"_id":"3323257f-6104-429e-8cbd-b044a8bcf90e","_source":{"type":"ImageAsset"}},{"_id":"bd8b981f-4681-4fda-a4d3-c6b840039ae4","_source":{"type":"ImageAsset"}},{"_id":"7b25161a-2824-40be-8ac3-7201881f1afe","_source":{"type":"ImageAsset"}},{"_id":"fb54fb44-0d22-4220-8d00-23443708edab","_source":{"type":"ImageAsset"}},{"_id":"b7b3bde9-6d75-4ae5-90e7-817887ac510b","_source":{"type":"ImageAsset"}},{"_id":"c6300eb5-b0df-4b7d-b0ba-954b7dbf75c2","_source":{"type":"ImageAsset"}},{"_id":"613c117b-f781-453a-a79a-7d846ccccfa2","_source":{"type":"ImageAsset"}},{"_id":"6ba4e055-04b1-467d-a994-1bb712aabb42","_source":{"type":"ImageAsset"}},{"_id":"f0d2146d-8eb9-4a03-910e-9f6dc18ab512","_source":{"type":"ImageAsset"}},{"_id":"b369f200-f158-4f82-bee0-f205441758e1","_source":{"type":"ImageAsset"}},{"_id":"cfe4b256-17f6-4c76-b926-e8fbbf3e164c","_source":{"type":"ImageAsset"}},{"_id":"c8e36496-6a25-42d5-8075-082d2d33400d","_source":{"type":"ImageAsset"}},{"_id":"b85ead4d-b44f-4537-9a18-8c7f580d3be4","_source":{"type":"ImageAsset"}},{"_id":"084a3c4d-faaf-4264-ac87-621ad3af5160","_source":{"type":"ImageAsset"}},{"_id":"05c50984-019b-4bbe-a173-f055533cc943","_source":{"type":"ImageAsset"}},{"_id":"f748b94d-6d27-4892-b154-2a36f018fc40","_source":{"type":"ImageAsset"}},{"_id":"bfc1c3f6-fa47-412d-b258-01a64a20cdc9","_source":{"type":"ImageAsset"}},{"_id":"c43ac98a-e14d-42c5-900d-78ca9a0f1572","_source":{"type":"ImageAsset"}},{"_id":"14d05ec4-fe3b-4c72-87f9-0cd64d24d587","_source":{"type":"ImageAsset"}},{"_id":"b7fe4647-881e-48eb-a128-d101e33b7213","_source":{"type":"ImageAsset"}},{"_id":"7f7ab5b7-5989-4f26-8e7e-75d35282d4b8","_source":{"type":"ImageAsset"}},{"_id":"c5070294-7ed8-4787-bcd5-d5794db853b0","_source":{"type":"ImageAsset"}}]},"status":200},{"hits":{"hits":[{"_id":"b828b6d2-01a2-427c-ad15-db249ba09ac1","_source":{"type":"VideoAsset"}},{"_id":"2d403e6c-f5a8-444a-b981-89d7d2155a79","_source":{"type":"VideoAsset"}}]},"status":200}]}
web-service_1         | [2020-05-08 23:05:51 +0000] [264] [web.model_search] [DEBUG] results: {'responses': [{'status': 200, 'hits': {'hits': [{'_id': '72c208df-4fad-49f6-bf28-a1ae7c4682db', '_source': {'type': 'VideoAsset'}}, {'_id': 'b2fa31bf-1b8e-41e4-b7e2-dda646171c08', '_source': {'type': 'VideoAsset'}}, {'_id': '1a49d595-46b5-42cf-94ca-c21523c9afaa', '_source': {'type': 'VideoAsset'}}, {'_id': '723084f5-0d54-4f55-8098-9b40eabc7c2e', '_source': {'type': 'VideoAsset'}}, {'_id': 'bd9f9de4-1b9e-4840-8c25-2a7acb300497', '_source': {'type': 'VideoAsset'}}, {'_id': '13f53d83-4a4d-41c1-a9a1-175bf10c3821', '_source': {'type': 'VideoAsset'}}, {'_id': '8956ec13-f0ad-47a3-a36f-cfae0b1be9d2', '_source': {'type': 'VideoAsset'}}, {'_id': '4451c02a-11ec-457e-a78d-4f6bae0d7113', '_source': {'type': 'VideoAsset'}}, {'_id': '07b100e3-9e1a-4ce3-bb20-09da7aec5e3c', '_source': {'type': 'VideoAsset'}}, {'_id': '8a6f424c-dffb-4a52-897d-f385ac2334fe', '_source': {'type': 'VideoAsset'}}, {'_id': 'f10fcda5-3532-49d6-8690-50ec108ee05e', '_source': {'type': 'VideoAsset'}}, {'_id': '0b6e7df0-95aa-4145-b50f-cc76a7098354', '_source': {'type': 'VideoAsset'}}, {'_id': 'b2c09d7d-d8cd-4a11-907a-b0561bf6a34e', '_source': {'type': 'VideoAsset'}}, {'_id': 'e02c4379-0f7f-41a0-92dc-210f1022f3c4', '_source': {'type': 'VideoAsset'}}, {'_id': 'aabe81d9-7882-4d91-9012-191e4a526edc', '_source': {'type': 'VideoAsset'}}, {'_id': '5610e39f-479d-4a39-b67d-c05de86bd8d3', '_source': {'type': 'VideoAsset'}}, {'_id': '9b8d66c4-7197-4a04-a645-5e4e7da7b311', '_source': {'type': 'VideoAsset'}}, {'_id': '205ee663-4a5c-45ae-94c9-fe26e23aff62', '_source': {'type': 'VideoAsset'}}, {'_id': 'd80fdf6e-0531-46c1-b5e4-1a515c9a1fe1', '_source': {'type': 'VideoAsset'}}, {'_id': 'cd091a7f-a244-411a-8b03-ff771e631fa5', '_source': {'type': 'VideoAsset'}}, {'_id': 'e58e458b-d144-44c3-b851-fd28df60b6f7', '_source': {'type': 'VideoAsset'}}, {'_id': 'b4488ab0-c818-49ff-9325-cf3e1a0a7800', '_source': {'type': 'VideoAsset'}}, {'_id': 'e907e8fc-f929-4450-aa37-9dadd4062d5f', '_source': {'type': 'VideoAsset'}}, {'_id': '8fbcbfbd-8748-4459-b11d-e63f6cce4b99', '_source': {'type': 'VideoAsset'}}, {'_id': '837323ea-d664-49a0-aa16-b954184405c9', '_source': {'type': 'VideoAsset'}}, {'_id': '65bd495e-f207-4c73-800e-92c600c870e9', '_source': {'type': 'VideoAsset'}}, {'_id': '22acb077-b854-448e-a775-9704e66879fa', '_source': {'type': 'VideoAsset'}}, {'_id': '745b1022-583b-4b47-b28f-64eeb3eba573', '_source': {'type': 'ImageAsset'}}, {'_id': '35909c80-26e7-46cf-b030-73ac437bd0bf', '_source': {'type': 'ImageAsset'}}, {'_id': '0074129d-708d-430b-85f9-fdfca96aab33', '_source': {'type': 'ImageAsset'}}, {'_id': '9cc0fdee-cdbe-458c-8436-ebc1d25d15d1', '_source': {'type': 'ImageAsset'}}, {'_id': 'bd1d0e2e-178b-4a0d-b5d8-36992b4bb5a0', '_source': {'type': 'ImageAsset'}}, {'_id': 'b81d9ad3-c679-4b60-a349-b438ed63b710', '_source': {'type': 'ImageAsset'}}, {'_id': '5b12e32b-e12a-4d75-9128-3701a91fde9a', '_source': {'type': 'ImageAsset'}}, {'_id': '7305c340-d9c3-4e52-be27-87d50b85164c', '_source': {'type': 'ImageAsset'}}, {'_id': 'd7cb3ecf-b26c-4359-953e-3bc8b57588c5', '_source': {'type': 'ImageAsset'}}, {'_id': '7574823d-c2cf-43e4-b035-cac1f3408fad', '_source': {'type': 'ImageAsset'}}, {'_id': '09906a35-0668-4f70-a57c-6e5215716393', '_source': {'type': 'ImageAsset'}}, {'_id': '6dcb1afb-8984-48eb-b489-39fb6bac9f83', '_source': {'type': 'ImageAsset'}}, {'_id': '21ba7594-7a16-4009-86bc-c406131ccb32', '_source': {'type': 'ImageAsset'}}, {'_id': 'c22c16ef-6692-4396-93de-34a2e7b8f951', '_source': {'type': 'ImageAsset'}}, {'_id': 'db6f78e3-3772-49f5-b12f-cc3df99c9e53', '_source': {'type': 'ImageAsset'}}, {'_id': '7ef41d9f-1a95-434f-a395-60a6e1df168c', '_source': {'type': 'ImageAsset'}}, {'_id': '07afc347-5cec-4aa3-81a5-671ef2359b32', '_source': {'type': 'ImageAsset'}}, {'_id': '4d6fd831-edde-4895-80a6-5780b64829ec', '_source': {'type': 'ImageAsset'}}, {'_id': 'fb4375c6-cd63-4a4e-befd-b171f1d7b95e', '_source': {'type': 'ImageAsset'}}, {'_id': '734ceadf-4e7f-4c9a-83a2-da51d81212eb', '_source': {'type': 'ImageAsset'}}, {'_id': 'b0c9f884-6b0d-4a8b-b2f5-25ebc28dfe32', '_source': {'type': 'ImageAsset'}}, {'_id': 'b27bbec1-f8b8-4fbf-89da-f1ebdf96524b', '_source': {'type': 'ImageAsset'}}, {'_id': 'ae009c0a-3090-4b29-beaf-535fac7e0446', '_source': {'type': 'ImageAsset'}}, {'_id': '5f0db89a-7fca-45d6-9703-a6cded757f0b', '_source': {'type': 'ImageAsset'}}, {'_id': '1a2c060a-f1a2-41f4-a245-76d50752b98f', '_source': {'type': 'ImageAsset'}}, {'_id': 'f4833b8d-0f09-442f-a88e-e5b657c0d6c2', '_source': {'type': 'ImageAsset'}}, {'_id': '9a9943c0-a65e-4f59-959c-e9013eba57fd', '_source': {'type': 'ImageAsset'}}, {'_id': '3e530120-c6f8-471b-abd8-1cd817beb5e9', '_source': {'type': 'ImageAsset'}}, {'_id': 'e3ee386d-49e0-4dae-8497-9958a210d4bf', '_source': {'type': 'ImageAsset'}}, {'_id': '931fea3e-1dba-41f4-802e-67731eaf066e', '_source': {'type': 'ImageAsset'}}, {'_id': 'dec8db7c-ecff-41a0-8a2b-534d808ce331', '_source': {'type': 'ImageAsset'}}, {'_id': '527f8b52-92f9-4888-9c11-87ea8e71c5e3', '_source': {'type': 'ImageAsset'}}, {'_id': 'ce2cb77d-cec9-4e0a-9c89-b4fa12899fbd', '_source': {'type': 'ImageAsset'}}, {'_id': '1aaa4fb6-811e-472b-a019-96984744390c', '_source': {'type': 'ImageAsset'}}, {'_id': '87a146b2-8a8d-4d68-9636-f18299e0c8fe', '_source': {'type': 'ImageAsset'}}, {'_id': '1a63688c-daf7-4cc7-bcbf-2dd51d6f98e9', '_source': {'type': 'ImageAsset'}}, {'_id': '99e7026b-4435-4ab1-963b-206229930214', '_source': {'type': 'ImageAsset'}}, {'_id': 'c502c598-8610-418a-9d10-e0575d3e31b3', '_source': {'type': 'ImageAsset'}}, {'_id': 'c2e9b4ef-0418-489c-8ffe-921f403b81db', '_source': {'type': 'ImageAsset'}}, {'_id': '214aecfc-d5aa-41c4-9f87-d0c857062b4a', '_source': {'type': 'ImageAsset'}}, {'_id': '64773c74-4096-4d96-9b36-984e5dcbf432', '_source': {'type': 'ImageAsset'}}, {'_id': '20b2ae93-c2a1-4657-a5d9-c56fba1c8392', '_source': {'type': 'ImageAsset'}}, {'_id': '645b97f1-3755-4702-b44b-7647b47bb65b', '_source': {'type': 'ImageAsset'}}, {'_id': '531d331e-28cc-40ba-bdc5-22f694f4a77c', '_source': {'type': 'ImageAsset'}}, {'_id': 'c2d64bcf-c5c5-4b23-bf21-040252f9f605', '_source': {'type': 'ImageAsset'}}, {'_id': 'c35e45c1-0a10-4309-9111-0f8059c1d491', '_source': {'type': 'ImageAsset'}}, {'_id': '0c9bff7f-9524-4d9e-b6a7-b1491ad8bf1f', '_source': {'type': 'ImageAsset'}}, {'_id': '4a302de2-2c6e-43ff-ad5a-b9b7ab45032e', '_source': {'type': 'ImageAsset'}}, {'_id': '98e0c3e0-cea2-4174-99e1-d2cbf10f7b00', '_source': {'type': 'ImageAsset'}}, {'_id': 'c1e8eefd-5e3a-4f8f-8a95-1fdcc24fc473', '_source': {'type': 'ImageAsset'}}, {'_id': '10b2a298-69e0-422c-bbc8-acca14e9a14e', '_source': {'type': 'ImageAsset'}}, {'_id': '23f6f3cb-fca9-4b11-9181-9224da1514bb', '_source': {'type': 'ImageAsset'}}, {'_id': '2f338a4e-3cc5-4f9a-b9d4-d2c6d9299c63', '_source': {'type': 'ImageAsset'}}, {'_id': '5e577863-ea30-46a7-b92b-ceeea6253bd4', '_source': {'type': 'ImageAsset'}}, {'_id': '329a4fbb-4189-45b7-974e-edfbd4804625', '_source': {'type': 'ImageAsset'}}, {'_id': '708433cf-223f-4251-a624-e8ddf5df35ac', '_source': {'type': 'ImageAsset'}}, {'_id': 'c6b7f38b-8319-4acc-b24c-782b880a2d1c', '_source': {'type': 'ImageAsset'}}, {'_id': '9a9f7c0b-b5ca-49ec-8a75-cea0e40ab30f', '_source': {'type': 'ImageAsset'}}, {'_id': 'c10fd639-a543-483e-9454-88ff8306800b', '_source': {'type': 'ImageAsset'}}, {'_id': '94d16b64-b724-4a85-bf4c-c44fe3cddfaf', '_source': {'type': 'ImageAsset'}}, {'_id': '625c2c04-6c14-400b-a1e1-c6cacb2d315f', '_source': {'type': 'ImageAsset'}}, {'_id': '5f16bcdd-4a76-4078-82bd-20f000fd257e', '_source': {'type': 'ImageAsset'}}, {'_id': 'b5c3f4b2-cb01-4c02-869b-1048ebcab322', '_source': {'type': 'ImageAsset'}}, {'_id': '14fd36a0-4613-468b-9bd0-ff0dc1772d1d', '_source': {'type': 'ImageAsset'}}, {'_id': 'f59ba4bc-8bf5-4385-9b9d-6861b5d5909a', '_source': {'type': 'ImageAsset'}}, {'_id': '7b8ffff5-739e-4a2a-ae61-30d03d2f98fc', '_source': {'type': 'ImageAsset'}}, {'_id': '79c6253b-92f9-4f31-9892-d61a4204585b', '_source': {'type': 'ImageAsset'}}, {'_id': '356338b8-a58f-4f44-9a4b-01c4e35d7809', '_source': {'type': 'ImageAsset'}}, {'_id': '29bdb0e4-9ec0-4a33-8ac3-034f522b1190', '_source': {'type': 'ImageAsset'}}, {'_id': '0b5ee649-c24a-4559-a89a-493daa997ea7', '_source': {'type': 'ImageAsset'}}, {'_id': 'c505be6c-e98d-4adf-bab4-85e005e64279', '_source': {'type': 'ImageAsset'}}, {'_id': '3dcfa89e-6924-4fe4-b581-6c2c0eef1bc6', '_source': {'type': 'ImageAsset'}}, {'_id': 'ff8d6998-ef81-4aa7-b501-a18cb041b9e0', '_source': {'type': 'ImageAsset'}}, {'_id': 'c07af570-5617-411c-8e75-b01f618157f2', '_source': {'type': 'ImageAsset'}}, {'_id': '8e9889f7-86a5-4160-b4cf-ec4e0b19279a', '_source': {'type': 'ImageAsset'}}, {'_id': '1d034c33-6121-453b-8f9c-194b39ada3aa', '_source': {'type': 'ImageAsset'}}, {'_id': 'fffcce23-3df3-49fb-b76f-4383ec0ebc6d', '_source': {'type': 'ImageAsset'}}, {'_id': 'a92cf2af-ceeb-40ac-8121-8fdaa0e70825', '_source': {'type': 'ImageAsset'}}, {'_id': '246c17ee-0c32-45eb-8407-67333145a2f1', '_source': {'type': 'ImageAsset'}}, {'_id': 'a9220466-1d8a-48cb-b26f-22b35b0769ef', '_source': {'type': 'ImageAsset'}}, {'_id': 'f315a6e7-4bfb-467c-97bf-63054a14dfd5', '_source': {'type': 'ImageAsset'}}, {'_id': '3323257f-6104-429e-8cbd-b044a8bcf90e', '_source': {'type': 'ImageAsset'}}, {'_id': 'bd8b981f-4681-4fda-a4d3-c6b840039ae4', '_source': {'type': 'ImageAsset'}}, {'_id': '7b25161a-2824-40be-8ac3-7201881f1afe', '_source': {'type': 'ImageAsset'}}, {'_id': 'fb54fb44-0d22-4220-8d00-23443708edab', '_source': {'type': 'ImageAsset'}}, {'_id': 'b7b3bde9-6d75-4ae5-90e7-817887ac510b', '_source': {'type': 'ImageAsset'}}, {'_id': 'c6300eb5-b0df-4b7d-b0ba-954b7dbf75c2', '_source': {'type': 'ImageAsset'}}, {'_id': '613c117b-f781-453a-a79a-7d846ccccfa2', '_source': {'type': 'ImageAsset'}}, {'_id': '6ba4e055-04b1-467d-a994-1bb712aabb42', '_source': {'type': 'ImageAsset'}}, {'_id': 'f0d2146d-8eb9-4a03-910e-9f6dc18ab512', '_source': {'type': 'ImageAsset'}}, {'_id': 'b369f200-f158-4f82-bee0-f205441758e1', '_source': {'type': 'ImageAsset'}}, {'_id': 'cfe4b256-17f6-4c76-b926-e8fbbf3e164c', '_source': {'type': 'ImageAsset'}}, {'_id': 'c8e36496-6a25-42d5-8075-082d2d33400d', '_source': {'type': 'ImageAsset'}}, {'_id': 'b85ead4d-b44f-4537-9a18-8c7f580d3be4', '_source': {'type': 'ImageAsset'}}, {'_id': '084a3c4d-faaf-4264-ac87-621ad3af5160', '_source': {'type': 'ImageAsset'}}, {'_id': '05c50984-019b-4bbe-a173-f055533cc943', '_source': {'type': 'ImageAsset'}}, {'_id': 'f748b94d-6d27-4892-b154-2a36f018fc40', '_source': {'type': 'ImageAsset'}}, {'_id': 'bfc1c3f6-fa47-412d-b258-01a64a20cdc9', '_source': {'type': 'ImageAsset'}}, {'_id': 'c43ac98a-e14d-42c5-900d-78ca9a0f1572', '_source': {'type': 'ImageAsset'}}, {'_id': '14d05ec4-fe3b-4c72-87f9-0cd64d24d587', '_source': {'type': 'ImageAsset'}}, {'_id': 'b7fe4647-881e-48eb-a128-d101e33b7213', '_source': {'type': 'ImageAsset'}}, {'_id': '7f7ab5b7-5989-4f26-8e7e-75d35282d4b8', '_source': {'type': 'ImageAsset'}}, {'_id': 'c5070294-7ed8-4787-bcd5-d5794db853b0', '_source': {'type': 'ImageAsset'}}]}}, {'status': 200, 'hits': {'hits': [{'_id': 'b828b6d2-01a2-427c-ad15-db249ba09ac1', '_source': {'type': 'VideoAsset'}}, {'_id': '2d403e6c-f5a8-444a-b981-89d7d2155a79', '_source': {'type': 'VideoAsset'}}]}}]}
pgbouncer-service_1   | 2020-05-08 23:05:51.827 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40950 closing because: client close request (age=4)
pgbouncer-service_1   | 2020-05-08 23:05:51.845 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40958 login attempt: db=lumen5 user=lumen5 tls=no
web-service_1         | [2020-05-08 23:05:51 +0000] [265] [incoming_requests] [DEBUG] {"get": {}, "post": {}, "time": "2020-05-08T23:05:51.851638+00:00", "path": "/api/clicklogsquery/"}
web-service_1         | {"severity": "INFO", "textPayload": {"user": 1, "time": "2020-05-08T23:05:51.875488Z", "video_id": 45, "log_name": "media_search_v2", "action": "Q", "query": "Nature", "processed_query": "Nature", "corrected_query": "Nature", "page": 2, "results": [], "results_shape": [-1, 2], "language": "en", "filter": {"marketplace_enabled": true}}, "name": "click_logs"}
pgbouncer-service_1   | 2020-05-08 23:05:51.882 1 LOG C-0x556cc5259cf0: lumen5/lumen5@172.18.0.11:40958 closing because: client close request (age=0)
pgbouncer-service_1   | 2020-05-08 23:05:56.859 1 LOG stats: 3 xacts/s, 3 queries/s, in 4662 B/s, out 6590 B/s, xact 1149 us, query 1118 us, wait time 0 us
base_worker_1         | [2020-05-08 23:06:07 +0000] [7] [amqp] [DEBUG] heartbeat_tick : for connection 4b38861564db4d128568a3020245a256
base_worker_1         | [2020-05-08 23:06:07 +0000] [7] [amqp] [DEBUG] heartbeat_tick : Prev sent/recv: 32/150, now - 33/180, monotonic - 109639.021922854, last_heartbeat_sent - 109639.021921378, heartbeat int. - 60 for connection 4b38861564db4d128568a3020245a256
```