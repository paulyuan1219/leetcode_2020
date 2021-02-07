```
(base) MacBook-Pro:docker weiyuan$ ./run_dev.sh 
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
44ed2f2768c2
e38a0add9928
b09f4dd60f27
6edcd52e73b2
8671cb72359d
acf9fea14e2c
1aeaa4fb8b00
446bc6ab8fd2
2c977500aa67
36d70b9cc40f
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
Creating docker_stripe-cli_1         ... done
Creating docker_video-data-service_1 ... done
Creating docker_media-proxy_1        ... done
Creating docker_rabbitmq-ha_1        ... done
Creating docker_elasticsearch-v3_1   ... done
Creating docker_frontend_1           ... done
Creating docker_db_1                 ... done
Creating docker_pgbouncer-service_1  ... done
Creating docker_web-service_1        ... done
Creating docker_base_worker_1        ... done
Attaching to docker_stripe-cli_1, docker_db_1, docker_media-proxy_1, docker_rabbitmq-ha_1, docker_elasticsearch-v3_1, docker_video-data-service_1, docker_frontend_1, docker_pgbouncer-service_1, docker_base_worker_1, docker_web-service_1
db_1                  | 
db_1                  | PostgreSQL Database directory appears to contain a database; Skipping initialization
db_1                  | 
db_1                  | LOG:  database system was interrupted; last known up at 2020-06-11 23:21:36 UTC
elasticsearch-v3_1    | File '/opt/plugins/ltr-1.1.0-es6.3.1.zip' already there; not retrieving.
elasticsearch-v3_1    | 
media-proxy_1         | Operations to perform:
media-proxy_1         |   Apply all migrations: admin, auth, contenttypes, sessions
media-proxy_1         | Running migrations:
pgbouncer-service_1   | grep: /etc/pgbouncer/userlist.txt: No such file or directory
db_1                  | LOG:  database system was not properly shut down; automatic recovery in progress
db_1                  | LOG:  invalid record length at 0/1F76A08: wanted 24, got 0
db_1                  | LOG:  redo is not required
pgbouncer-service_1   | Wrote authentication credentials to /etc/pgbouncer/userlist.txt
pgbouncer-service_1   | Create pgbouncer config in /etc/pgbouncer
db_1                  | LOG:  MultiXact member wraparound protections are now enabled
stripe-cli_1          | Checking for new versions...
db_1                  | LOG:  autovacuum launcher started
db_1                  | LOG:  database system is ready to accept connections
stripe-cli_1          | Getting ready...
media-proxy_1         |   Applying contenttypes.0001_initial... OK
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
media-proxy_1         |   Applying auth.0001_initial... OK
pgbouncer-service_1   | Starting /usr/bin/pgbouncer /etc/pgbouncer/pgbouncer.ini...
stripe-cli_1          | 
stripe-cli_1          | Ready! Your webhook signing secret is whsec_vpNp3D1KO49WOVYhNTKOhoeWaQDub8NK (^C to quit)
media-proxy_1         |   Applying admin.0001_initial... OK
pgbouncer-service_1   | 2020-06-11 23:32:07.730 1 LOG file descriptor limit: 1048576 (H:1048576), max_client_conn: 500, max fds possible: 510
media-proxy_1         |   Applying admin.0002_logentry_remove_auto_add... OK
pgbouncer-service_1   | 2020-06-11 23:32:07.731 1 LOG listening on 0.0.0.0:5432
pgbouncer-service_1   | 2020-06-11 23:32:07.731 1 LOG process up: pgbouncer 1.9.0, libevent 2.1.8-stable (epoll), adns: udns 0.4, tls: LibreSSL 2.6.5
media-proxy_1         |   Applying admin.0003_logentry_add_action_flag_choices... OK
media-proxy_1         |   Applying contenttypes.0002_remove_content_type_name... OK
media-proxy_1         |   Applying auth.0002_alter_permission_name_max_length... OK
media-proxy_1         |   Applying auth.0003_alter_user_email_max_length... OK
media-proxy_1         |   Applying auth.0004_alter_user_username_opts... OK
media-proxy_1         |   Applying auth.0005_alter_user_last_login_null... OK
media-proxy_1         |   Applying auth.0006_require_contenttypes_0002... OK
media-proxy_1         |   Applying auth.0007_alter_validators_add_error_messages... OK
media-proxy_1         |   Applying auth.0008_alter_user_username_max_length... OK
media-proxy_1         |   Applying auth.0009_alter_user_last_name_max_length... OK
media-proxy_1         |   Applying sessions.0001_initial... OK
media-proxy_1         | [2020-06-11 23:32:08 +0000] [9] [INFO] Starting gunicorn 19.9.0
media-proxy_1         | [2020-06-11 23:32:08 +0000] [9] [INFO] Listening at: http://0.0.0.0:7999 (9)
media-proxy_1         | [2020-06-11 23:32:08 +0000] [9] [INFO] Using worker: sync
media-proxy_1         | /usr/local/lib/python3.8/os.py:1023: RuntimeWarning: line buffering (buffering=1) isn't supported in binary mode, the default buffer size will be used
media-proxy_1         |   return io.open(fd, *args, **kwargs)
media-proxy_1         | [2020-06-11 23:32:08 +0000] [11] [INFO] Booting worker with pid: 11
elasticsearch-v3_1    | -> Downloading file:///opt/plugins/ltr-1.1.0-es6.3.1.zip
[=================================================] 100%?? 
rabbitmq-ha_1         | Waiting for pid file '/var/lib/rabbitmq/mnesia/rabbit@queue.pid' to appear
rabbitmq-ha_1         | pid is 10
rabbitmq-ha_1         | Waiting for erlang distribution on node 'rabbit@queue' while OS process '10' is running
web-service_1         | 2020-06-11 23:32:11,045 - [bugsnag] WARNING - No API key configured, couldn't notify
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "manage.py", line 9, in <module>
web-service_1         |     execute_from_command_line(sys.argv)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/core/management/__init__.py", line 381, in execute_from_command_line
web-service_1         |     utility.execute()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/core/management/__init__.py", line 325, in execute
web-service_1         |     settings.INSTALLED_APPS
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 79, in __getattr__
web-service_1         |     self._setup(name)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 66, in _setup
web-service_1         |     self._wrapped = Settings(settings_module)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 157, in __init__
web-service_1         |     mod = importlib.import_module(self.SETTINGS_MODULE)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/importlib/__init__.py", line 126, in import_module
web-service_1         |     return _bootstrap._gcd_import(name[level:], package, level)
web-service_1         |   File "<frozen importlib._bootstrap>", line 986, in _gcd_import
web-service_1         |   File "<frozen importlib._bootstrap>", line 969, in _find_and_load
web-service_1         |   File "<frozen importlib._bootstrap>", line 958, in _find_and_load_unlocked
web-service_1         |   File "<frozen importlib._bootstrap>", line 673, in _load_unlocked
web-service_1         |   File "<frozen importlib._bootstrap_external>", line 673, in exec_module
web-service_1         |   File "<frozen importlib._bootstrap>", line 222, in _call_with_frames_removed
web-service_1         |   File "/opt/app/videobysniply/settings.py", line 501, in <module>
web-service_1         |     if settings.DEBUG:
web-service_1         | NameError: name 'settings' is not defined
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
web-service_1         | 2020-06-11 23:32:12,298 - [bugsnag] WARNING - No API key configured, couldn't notify
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "manage.py", line 9, in <module>
web-service_1         |     execute_from_command_line(sys.argv)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/core/management/__init__.py", line 381, in execute_from_command_line
web-service_1         |     utility.execute()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/core/management/__init__.py", line 325, in execute
web-service_1         |     settings.INSTALLED_APPS
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 79, in __getattr__
web-service_1         |     self._setup(name)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 66, in _setup
web-service_1         |     self._wrapped = Settings(settings_module)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 157, in __init__
web-service_1         |     mod = importlib.import_module(self.SETTINGS_MODULE)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/importlib/__init__.py", line 126, in import_module
web-service_1         |     return _bootstrap._gcd_import(name[level:], package, level)
web-service_1         |   File "<frozen importlib._bootstrap>", line 986, in _gcd_import
web-service_1         |   File "<frozen importlib._bootstrap>", line 969, in _find_and_load
web-service_1         |   File "<frozen importlib._bootstrap>", line 958, in _find_and_load_unlocked
web-service_1         |   File "<frozen importlib._bootstrap>", line 673, in _load_unlocked
web-service_1         |   File "<frozen importlib._bootstrap_external>", line 673, in exec_module
web-service_1         |   File "<frozen importlib._bootstrap>", line 222, in _call_with_frames_removed
web-service_1         |   File "/opt/app/videobysniply/settings.py", line 501, in <module>
web-service_1         |     if settings.DEBUG:
web-service_1         | NameError: name 'settings' is not defined
web-service_1         | 2020-06-11 23:32:13,827 - [bugsnag] WARNING - No API key configured, couldn't notify
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "manage.py", line 9, in <module>
web-service_1         |     execute_from_command_line(sys.argv)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/core/management/__init__.py", line 381, in execute_from_command_line
web-service_1         |     utility.execute()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/core/management/__init__.py", line 325, in execute
web-service_1         |     settings.INSTALLED_APPS
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 79, in __getattr__
web-service_1         |     self._setup(name)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 66, in _setup
web-service_1         |     self._wrapped = Settings(settings_module)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 157, in __init__
web-service_1         |     mod = importlib.import_module(self.SETTINGS_MODULE)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/importlib/__init__.py", line 126, in import_module
web-service_1         |     return _bootstrap._gcd_import(name[level:], package, level)
web-service_1         |   File "<frozen importlib._bootstrap>", line 986, in _gcd_import
web-service_1         |   File "<frozen importlib._bootstrap>", line 969, in _find_and_load
web-service_1         |   File "<frozen importlib._bootstrap>", line 958, in _find_and_load_unlocked
web-service_1         |   File "<frozen importlib._bootstrap>", line 673, in _load_unlocked
web-service_1         |   File "<frozen importlib._bootstrap_external>", line 673, in exec_module
web-service_1         |   File "<frozen importlib._bootstrap>", line 222, in _call_with_frames_removed
web-service_1         |   File "/opt/app/videobysniply/settings.py", line 501, in <module>
web-service_1         |     if settings.DEBUG:
web-service_1         | NameError: name 'settings' is not defined
elasticsearch-v3_1    | [2020-06-11T23:32:14,106][INFO ][o.e.n.Node               ] [es-node-0] initializing ...
elasticsearch-v3_1    | [2020-06-11T23:32:14,183][INFO ][o.e.e.NodeEnvironment    ] [es-node-0] using [1] data paths, mounts [[/usr/share/elasticsearch/data (/dev/sda1)]], net usable_space [77.2gb], net total_space [100.3gb], types [ext4]
elasticsearch-v3_1    | [2020-06-11T23:32:14,183][INFO ][o.e.e.NodeEnvironment    ] [es-node-0] heap size [494.9mb], compressed ordinary object pointers [true]
elasticsearch-v3_1    | [2020-06-11T23:32:14,221][INFO ][o.e.n.Node               ] [es-node-0] node name [es-node-0], node ID [aYb7htMrSguOa_exsTLuRw]
elasticsearch-v3_1    | [2020-06-11T23:32:14,222][INFO ][o.e.n.Node               ] [es-node-0] version[6.3.1], pid[83], build[default/tar/eb782d0/2018-06-29T21:59:26.107521Z], OS[Linux/4.19.76-linuxkit/amd64], JVM[Oracle Corporation/OpenJDK 64-Bit Server VM/10.0.1/10.0.1+10]
elasticsearch-v3_1    | [2020-06-11T23:32:14,223][INFO ][o.e.n.Node               ] [es-node-0] JVM arguments [-Xms1g, -Xmx1g, -XX:+UseConcMarkSweepGC, -XX:CMSInitiatingOccupancyFraction=75, -XX:+UseCMSInitiatingOccupancyOnly, -XX:+AlwaysPreTouch, -Xss1m, -Djava.awt.headless=true, -Dfile.encoding=UTF-8, -Djna.nosys=true, -XX:-OmitStackTraceInFastThrow, -Dio.netty.noUnsafe=true, -Dio.netty.noKeySetOptimization=true, -Dio.netty.recycler.maxCapacityPerThread=0, -Dlog4j.shutdownHookEnabled=false, -Dlog4j2.disable.jmx=true, -Djava.io.tmpdir=/tmp/elasticsearch.m9f7hfza, -XX:+HeapDumpOnOutOfMemoryError, -XX:HeapDumpPath=data, -XX:ErrorFile=logs/hs_err_pid%p.log, -Xlog:gc*,gc+age=trace,safepoint:file=logs/gc.log:utctime,pid,tags:filecount=32,filesize=64m, -Djava.locale.providers=COMPAT, -Des.cgroups.hierarchy.override=/, -Xms512m, -Xmx512m, -Des.path.home=/usr/share/elasticsearch, -Des.path.conf=/usr/share/elasticsearch/config, -Des.distribution.flavor=default, -Des.distribution.type=tar]
web-service_1         | 2020-06-11 23:32:15,253 [31] [gunicorn.error] [INFO] Starting gunicorn 20.0.4
web-service_1         | 2020-06-11 23:32:15,254 [31] [gunicorn.error] [INFO] Listening at: http://0.0.0.0:8000 (31)
web-service_1         | 2020-06-11 23:32:15,254 [31] [gunicorn.error] [INFO] Using worker: sync
web-service_1         | 2020-06-11 23:32:15,261 [40] [gunicorn.error] [INFO] Booting worker with pid: 40
web-service_1         | 2020-06-11 23:32:15,299 [41] [gunicorn.error] [INFO] Booting worker with pid: 41
web-service_1         | 2020-06-11 23:32:16,024 [40] [gunicorn.error] [ERROR] Exception in worker process
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/arbiter.py", line 583, in spawn_worker
web-service_1         |     worker.init_process()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/workers/base.py", line 119, in init_process
web-service_1         |     self.load_wsgi()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/workers/base.py", line 144, in load_wsgi
web-service_1         |     self.wsgi = self.app.wsgi()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/app/base.py", line 67, in wsgi
web-service_1         |     self.callable = self.load()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/app/wsgiapp.py", line 49, in load
web-service_1         |     return self.load_wsgiapp()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/app/wsgiapp.py", line 39, in load_wsgiapp
web-service_1         |     return util.import_app(self.app_uri)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/util.py", line 358, in import_app
web-service_1         |     mod = importlib.import_module(module)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/importlib/__init__.py", line 126, in import_module
web-service_1         |     return _bootstrap._gcd_import(name[level:], package, level)
web-service_1         |   File "<frozen importlib._bootstrap>", line 986, in _gcd_import
web-service_1         |   File "<frozen importlib._bootstrap>", line 969, in _find_and_load
web-service_1         |   File "<frozen importlib._bootstrap>", line 958, in _find_and_load_unlocked
web-service_1         |   File "<frozen importlib._bootstrap>", line 673, in _load_unlocked
web-service_1         |   File "<frozen importlib._bootstrap_external>", line 673, in exec_module
web-service_1         |   File "<frozen importlib._bootstrap>", line 222, in _call_with_frames_removed
web-service_1         |   File "/opt/app/videobysniply/wsgi.py", line 15, in <module>
web-service_1         |     application = get_wsgi_application()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/core/wsgi.py", line 12, in get_wsgi_application
web-service_1         |     django.setup(set_prefix=False)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/__init__.py", line 19, in setup
web-service_1         |     configure_logging(settings.LOGGING_CONFIG, settings.LOGGING)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 79, in __getattr__
web-service_1         |     self._setup(name)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 66, in _setup
web-service_1         |     self._wrapped = Settings(settings_module)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 157, in __init__
web-service_1         |     mod = importlib.import_module(self.SETTINGS_MODULE)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/importlib/__init__.py", line 126, in import_module
web-service_1         |     return _bootstrap._gcd_import(name[level:], package, level)
web-service_1         |   File "<frozen importlib._bootstrap>", line 986, in _gcd_import
web-service_1         |   File "<frozen importlib._bootstrap>", line 969, in _find_and_load
web-service_1         |   File "<frozen importlib._bootstrap>", line 958, in _find_and_load_unlocked
web-service_1         |   File "<frozen importlib._bootstrap>", line 673, in _load_unlocked
web-service_1         |   File "<frozen importlib._bootstrap_external>", line 673, in exec_module
web-service_1         |   File "<frozen importlib._bootstrap>", line 222, in _call_with_frames_removed
web-service_1         |   File "/opt/app/videobysniply/settings.py", line 501, in <module>
web-service_1         |     if settings.DEBUG:
web-service_1         | NameError: name 'settings' is not defined
web-service_1         | 2020-06-11 23:32:16,036 [40] [gunicorn.error] [INFO] Worker exiting (pid: 40)
web-service_1         | 2020-06-11 23:32:16,044 [41] [gunicorn.error] [ERROR] Exception in worker process
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/arbiter.py", line 583, in spawn_worker
web-service_1         |     worker.init_process()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/workers/base.py", line 119, in init_process
web-service_1         |     self.load_wsgi()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/workers/base.py", line 144, in load_wsgi
web-service_1         |     self.wsgi = self.app.wsgi()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/app/base.py", line 67, in wsgi
web-service_1         |     self.callable = self.load()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/app/wsgiapp.py", line 49, in load
web-service_1         |     return self.load_wsgiapp()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/app/wsgiapp.py", line 39, in load_wsgiapp
web-service_1         |     return util.import_app(self.app_uri)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/util.py", line 358, in import_app
web-service_1         |     mod = importlib.import_module(module)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/importlib/__init__.py", line 126, in import_module
web-service_1         |     return _bootstrap._gcd_import(name[level:], package, level)
web-service_1         |   File "<frozen importlib._bootstrap>", line 986, in _gcd_import
web-service_1         |   File "<frozen importlib._bootstrap>", line 969, in _find_and_load
web-service_1         |   File "<frozen importlib._bootstrap>", line 958, in _find_and_load_unlocked
web-service_1         |   File "<frozen importlib._bootstrap>", line 673, in _load_unlocked
web-service_1         |   File "<frozen importlib._bootstrap_external>", line 673, in exec_module
web-service_1         |   File "<frozen importlib._bootstrap>", line 222, in _call_with_frames_removed
web-service_1         |   File "/opt/app/videobysniply/wsgi.py", line 15, in <module>
web-service_1         |     application = get_wsgi_application()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/core/wsgi.py", line 12, in get_wsgi_application
web-service_1         |     django.setup(set_prefix=False)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/__init__.py", line 19, in setup
web-service_1         |     configure_logging(settings.LOGGING_CONFIG, settings.LOGGING)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 79, in __getattr__
web-service_1         |     self._setup(name)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 66, in _setup
web-service_1         |     self._wrapped = Settings(settings_module)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 157, in __init__
web-service_1         |     mod = importlib.import_module(self.SETTINGS_MODULE)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/importlib/__init__.py", line 126, in import_module
web-service_1         |     return _bootstrap._gcd_import(name[level:], package, level)
web-service_1         |   File "<frozen importlib._bootstrap>", line 986, in _gcd_import
web-service_1         |   File "<frozen importlib._bootstrap>", line 969, in _find_and_load
web-service_1         |   File "<frozen importlib._bootstrap>", line 958, in _find_and_load_unlocked
web-service_1         |   File "<frozen importlib._bootstrap>", line 673, in _load_unlocked
web-service_1         |   File "<frozen importlib._bootstrap_external>", line 673, in exec_module
web-service_1         |   File "<frozen importlib._bootstrap>", line 222, in _call_with_frames_removed
web-service_1         |   File "/opt/app/videobysniply/settings.py", line 501, in <module>
web-service_1         |     if settings.DEBUG:
web-service_1         | NameError: name 'settings' is not defined
web-service_1         | 2020-06-11 23:32:16,062 [41] [gunicorn.error] [INFO] Worker exiting (pid: 41)
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/arbiter.py", line 209, in run
web-service_1         |     self.sleep()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/arbiter.py", line 357, in sleep
web-service_1         |     ready = select.select([self.PIPE[0]], [], [], 1.0)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/arbiter.py", line 242, in handle_chld
web-service_1         |     self.reap_workers()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/arbiter.py", line 525, in reap_workers
web-service_1         |     raise HaltServer(reason, self.WORKER_BOOT_ERROR)
web-service_1         | gunicorn.errors.HaltServer: <HaltServer 'Worker failed to boot.' 3>
web-service_1         | 
web-service_1         | During handling of the above exception, another exception occurred:
web-service_1         | 
web-service_1         | Traceback (most recent call last):
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/bin/gunicorn", line 8, in <module>
web-service_1         |     sys.exit(run())
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/app/wsgiapp.py", line 58, in run
web-service_1         |     WSGIApplication("%(prog)s [OPTIONS] [APP_MODULE]").run()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/app/base.py", line 228, in run
web-service_1         |     super().run()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/app/base.py", line 72, in run
web-service_1         |     Arbiter(self).run()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/arbiter.py", line 229, in run
web-service_1         |     self.halt(reason=inst.reason, exit_status=inst.exit_status)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/arbiter.py", line 342, in halt
web-service_1         |     self.stop()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/arbiter.py", line 393, in stop
web-service_1         |     time.sleep(0.1)
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/arbiter.py", line 242, in handle_chld
web-service_1         |     self.reap_workers()
web-service_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/gunicorn/arbiter.py", line 525, in reap_workers
web-service_1         |     raise HaltServer(reason, self.WORKER_BOOT_ERROR)
web-service_1         | gunicorn.errors.HaltServer: <HaltServer 'Worker failed to boot.' 3>
docker_web-service_1 exited with code 1
elasticsearch-v3_1    | [2020-06-11T23:32:17,121][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [aggs-matrix-stats]
elasticsearch-v3_1    | [2020-06-11T23:32:17,122][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [analysis-common]
elasticsearch-v3_1    | [2020-06-11T23:32:17,122][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [ingest-common]
elasticsearch-v3_1    | [2020-06-11T23:32:17,122][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [lang-expression]
elasticsearch-v3_1    | [2020-06-11T23:32:17,122][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [lang-mustache]
elasticsearch-v3_1    | [2020-06-11T23:32:17,122][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [lang-painless]
elasticsearch-v3_1    | [2020-06-11T23:32:17,122][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [mapper-extras]
elasticsearch-v3_1    | [2020-06-11T23:32:17,122][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [parent-join]
elasticsearch-v3_1    | [2020-06-11T23:32:17,123][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [percolator]
elasticsearch-v3_1    | [2020-06-11T23:32:17,123][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [rank-eval]
elasticsearch-v3_1    | [2020-06-11T23:32:17,123][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [reindex]
elasticsearch-v3_1    | [2020-06-11T23:32:17,123][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [repository-url]
elasticsearch-v3_1    | [2020-06-11T23:32:17,123][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [transport-netty4]
elasticsearch-v3_1    | [2020-06-11T23:32:17,123][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [tribe]
elasticsearch-v3_1    | [2020-06-11T23:32:17,124][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-core]
elasticsearch-v3_1    | [2020-06-11T23:32:17,124][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-deprecation]
elasticsearch-v3_1    | [2020-06-11T23:32:17,124][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-graph]
elasticsearch-v3_1    | [2020-06-11T23:32:17,124][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-logstash]
elasticsearch-v3_1    | [2020-06-11T23:32:17,124][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-ml]
elasticsearch-v3_1    | [2020-06-11T23:32:17,125][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-monitoring]
elasticsearch-v3_1    | [2020-06-11T23:32:17,125][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-rollup]
elasticsearch-v3_1    | [2020-06-11T23:32:17,125][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-security]
elasticsearch-v3_1    | [2020-06-11T23:32:17,125][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-sql]
elasticsearch-v3_1    | [2020-06-11T23:32:17,125][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-upgrade]
elasticsearch-v3_1    | [2020-06-11T23:32:17,125][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded module [x-pack-watcher]
elasticsearch-v3_1    | [2020-06-11T23:32:17,126][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded plugin [ingest-geoip]
elasticsearch-v3_1    | [2020-06-11T23:32:17,126][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded plugin [ingest-user-agent]
elasticsearch-v3_1    | [2020-06-11T23:32:17,126][INFO ][o.e.p.PluginsService     ] [es-node-0] loaded plugin [ltr]
rabbitmq-ha_1         | 2020-06-11 23:32:18.943 [info] <0.9.0> Feature flags: list of feature flags found:
rabbitmq-ha_1         | 2020-06-11 23:32:18.943 [info] <0.9.0> Feature flags: feature flag states written to disk: yes
rabbitmq-ha_1         | 2020-06-11 23:32:19.092 [info] <0.349.0> 
rabbitmq-ha_1         |  Starting RabbitMQ 3.7.26 on Erlang 22.3.4.1
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
rabbitmq-ha_1         | 2020-06-11 23:32:19.093 [info] <0.349.0> 
rabbitmq-ha_1         |  node           : rabbit@queue
rabbitmq-ha_1         |  home dir       : /var/lib/rabbitmq
rabbitmq-ha_1         |  config file(s) : (none)
rabbitmq-ha_1         |  cookie hash    : RXpdghmKylNDH3wj+3JhPA==
rabbitmq-ha_1         |  log(s)         : <stdout>
rabbitmq-ha_1         |  database dir   : /var/lib/rabbitmq/mnesia/rabbit@queue
rabbitmq-ha_1         | 2020-06-11 23:32:19.112 [info] <0.349.0> Running boot step pre_boot defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.112 [info] <0.349.0> Running boot step rabbit_core_metrics defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.112 [info] <0.349.0> Running boot step rabbit_alarm defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.135 [info] <0.376.0> Memory high watermark set to 3185 MiB (3340320768 bytes) of 7963 MiB (8350801920 bytes) total
elasticsearch-v3_1    | [2020-06-11T23:32:19,144][WARN ][o.e.d.c.s.Settings       ] [http.enabled] setting was deprecated in Elasticsearch and will be removed in a future release! See the breaking changes documentation for the next major version.
rabbitmq-ha_1         | 2020-06-11 23:32:19.148 [info] <0.392.0> Enabling free disk space monitoring
rabbitmq-ha_1         | 2020-06-11 23:32:19.148 [info] <0.392.0> Disk free limit set to 50MB
rabbitmq-ha_1         | 2020-06-11 23:32:19.167 [info] <0.349.0> Running boot step code_server_cache defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.167 [info] <0.349.0> Running boot step file_handle_cache defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.167 [info] <0.397.0> FHC read buffering:  OFF
rabbitmq-ha_1         | 2020-06-11 23:32:19.167 [info] <0.397.0> FHC write buffering: ON
rabbitmq-ha_1         | 2020-06-11 23:32:19.167 [info] <0.396.0> Limiting to approx 1048476 file handles (943626 sockets)
rabbitmq-ha_1         | 2020-06-11 23:32:19.168 [info] <0.349.0> Running boot step worker_pool defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.168 [info] <0.352.0> Will use 6 processes for default worker pool
rabbitmq-ha_1         | 2020-06-11 23:32:19.168 [info] <0.352.0> Starting worker pool 'worker_pool' with 6 processes in it
rabbitmq-ha_1         | 2020-06-11 23:32:19.169 [info] <0.349.0> Running boot step database defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.172 [info] <0.349.0> Waiting for Mnesia tables for 30000 ms, 9 retries left
rabbitmq-ha_1         | 2020-06-11 23:32:19.217 [info] <0.349.0> Waiting for Mnesia tables for 30000 ms, 9 retries left
rabbitmq-ha_1         | 2020-06-11 23:32:19.217 [info] <0.349.0> Peer discovery backend rabbit_peer_discovery_classic_config does not support registration, skipping registration.
rabbitmq-ha_1         | 2020-06-11 23:32:19.217 [info] <0.349.0> Running boot step database_sync defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.217 [info] <0.349.0> Running boot step feature_flags defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.218 [info] <0.349.0> Running boot step codec_correctness_check defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.218 [info] <0.349.0> Running boot step external_infrastructure defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.218 [info] <0.349.0> Running boot step rabbit_registry defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.218 [info] <0.349.0> Running boot step rabbit_auth_mechanism_cr_demo defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.219 [info] <0.349.0> Running boot step rabbit_queue_location_random defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.219 [info] <0.349.0> Running boot step rabbit_event defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.219 [info] <0.349.0> Running boot step rabbit_auth_mechanism_amqplain defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.220 [info] <0.349.0> Running boot step rabbit_auth_mechanism_plain defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.220 [info] <0.349.0> Running boot step rabbit_exchange_type_direct defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.220 [info] <0.349.0> Running boot step rabbit_exchange_type_fanout defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.220 [info] <0.349.0> Running boot step rabbit_exchange_type_headers defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.221 [info] <0.349.0> Running boot step rabbit_exchange_type_topic defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.221 [info] <0.349.0> Running boot step rabbit_mirror_queue_mode_all defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.221 [info] <0.349.0> Running boot step rabbit_mirror_queue_mode_exactly defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.221 [info] <0.349.0> Running boot step rabbit_mirror_queue_mode_nodes defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.221 [info] <0.349.0> Running boot step rabbit_priority_queue defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.221 [info] <0.349.0> Priority queues enabled, real BQ is rabbit_variable_queue
rabbitmq-ha_1         | 2020-06-11 23:32:19.222 [info] <0.349.0> Running boot step rabbit_queue_location_client_local defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.222 [info] <0.349.0> Running boot step rabbit_queue_location_min_masters defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.222 [info] <0.349.0> Running boot step kernel_ready defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.222 [info] <0.349.0> Running boot step rabbit_sysmon_minder defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.222 [info] <0.349.0> Running boot step rabbit_epmd_monitor defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.235 [info] <0.421.0> epmd monitor knows us, inter-node communication (distribution) port: 25672
rabbitmq-ha_1         | 2020-06-11 23:32:19.235 [info] <0.349.0> Running boot step guid_generator defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.238 [info] <0.349.0> Running boot step rabbit_node_monitor defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.239 [info] <0.427.0> Starting rabbit_node_monitor
rabbitmq-ha_1         | 2020-06-11 23:32:19.239 [info] <0.349.0> Running boot step delegate_sup defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.239 [info] <0.349.0> Running boot step rabbit_memory_monitor defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.239 [info] <0.349.0> Running boot step core_initialized defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.239 [info] <0.349.0> Running boot step upgrade_queues defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.270 [info] <0.349.0> Running boot step rabbit_connection_tracking defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.271 [info] <0.349.0> Running boot step rabbit_connection_tracking_handler defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.271 [info] <0.349.0> Running boot step rabbit_exchange_parameters defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.271 [info] <0.349.0> Running boot step rabbit_mirror_queue_misc defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.271 [info] <0.349.0> Running boot step rabbit_policies defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.272 [info] <0.349.0> Running boot step rabbit_policy defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.272 [info] <0.349.0> Running boot step rabbit_queue_location_validator defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.273 [info] <0.349.0> Running boot step rabbit_vhost_limit defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.273 [info] <0.349.0> Running boot step rabbit_mgmt_reset_handler defined by app rabbitmq_management
rabbitmq-ha_1         | 2020-06-11 23:32:19.273 [info] <0.349.0> Running boot step rabbit_mgmt_db_handler defined by app rabbitmq_management_agent
rabbitmq-ha_1         | 2020-06-11 23:32:19.273 [info] <0.349.0> Management plugin: using rates mode 'basic'
rabbitmq-ha_1         | 2020-06-11 23:32:19.274 [info] <0.349.0> Running boot step recovery defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.276 [info] <0.464.0> Making sure data directory '/var/lib/rabbitmq/mnesia/rabbit@queue/msg_stores/vhosts/628WB79CIFDYO9LJI6DKMI09L' for vhost '/' exists
rabbitmq-ha_1         | 2020-06-11 23:32:19.289 [info] <0.464.0> Starting message stores for vhost '/'
rabbitmq-ha_1         | 2020-06-11 23:32:19.289 [info] <0.468.0> Message store "628WB79CIFDYO9LJI6DKMI09L/msg_store_transient": using rabbit_msg_store_ets_index to provide index
rabbitmq-ha_1         | 2020-06-11 23:32:19.306 [info] <0.464.0> Started message store of type transient for vhost '/'
rabbitmq-ha_1         | 2020-06-11 23:32:19.307 [info] <0.472.0> Message store "628WB79CIFDYO9LJI6DKMI09L/msg_store_persistent": using rabbit_msg_store_ets_index to provide index
rabbitmq-ha_1         | 2020-06-11 23:32:19.308 [warning] <0.472.0> Message store "628WB79CIFDYO9LJI6DKMI09L/msg_store_persistent": rebuilding indices from scratch
rabbitmq-ha_1         | 2020-06-11 23:32:19.314 [info] <0.464.0> Started message store of type persistent for vhost '/'
rabbitmq-ha_1         | 2020-06-11 23:32:19.343 [info] <0.349.0> Running boot step load_definitions defined by app rabbitmq_management
rabbitmq-ha_1         | 2020-06-11 23:32:19.343 [info] <0.349.0> Running boot step empty_db_check defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.343 [info] <0.349.0> Running boot step rabbit_looking_glass defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.343 [info] <0.349.0> Running boot step rabbit_core_metrics_gc defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.343 [info] <0.349.0> Running boot step background_gc defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.344 [info] <0.349.0> Running boot step connection_tracking defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.344 [info] <0.349.0> Setting up a table for connection tracking on this node: tracked_connection_on_node_rabbit@queue
rabbitmq-ha_1         | 2020-06-11 23:32:19.345 [info] <0.349.0> Setting up a table for per-vhost connection counting on this node: tracked_connection_per_vhost_on_node_rabbit@queue
rabbitmq-ha_1         | 2020-06-11 23:32:19.345 [info] <0.349.0> Running boot step routing_ready defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.345 [info] <0.349.0> Running boot step pre_flight defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.345 [info] <0.349.0> Running boot step notify_cluster defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.345 [info] <0.349.0> Running boot step networking defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.349 [info] <0.526.0> started TCP listener on [::]:5672
rabbitmq-ha_1         | 2020-06-11 23:32:19.363 [info] <0.349.0> Running boot step cluster_name defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.363 [info] <0.349.0> Running boot step direct_client defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.363 [info] <0.349.0> Running boot step os_signal_handler defined by app rabbit
rabbitmq-ha_1         | 2020-06-11 23:32:19.375 [info] <0.528.0> Swapping OS signal event handler (erl_signal_server) for our own
rabbitmq-ha_1         | 2020-06-11 23:32:19.423 [info] <0.578.0> Management plugin: HTTP (non-TLS) listener started on port 15672
rabbitmq-ha_1         | 2020-06-11 23:32:19.423 [info] <0.685.0> Statistics database started.
rabbitmq-ha_1         | 2020-06-11 23:32:19.423 [info] <0.684.0> Starting worker pool 'management_worker_pool' with 3 processes in it
rabbitmq-ha_1         | 2020-06-11 23:32:19.686 [info] <0.9.0> Server startup complete; 3 plugins started.
rabbitmq-ha_1         |  * rabbitmq_management
rabbitmq-ha_1         |  * rabbitmq_web_dispatch
rabbitmq-ha_1         |  * rabbitmq_management_agent
rabbitmq-ha_1         |  completed with 3 plugins.
rabbitmq-ha_1         | Applications 'rabbit_and_plugins' are running on node 'rabbit@queue'
elasticsearch-v3_1    | [2020-06-11T23:32:20,407][INFO ][o.e.d.DiscoveryModule    ] [es-node-0] using discovery type [single-node]
rabbitmq-ha_1         | Adding user "l5user" ...
rabbitmq-ha_1         | 2020-06-11 23:32:20.929 [info] <0.702.0> Creating user 'l5user'
rabbitmq-ha_1         | Error:
rabbitmq-ha_1         | User "l5user" already exists
elasticsearch-v3_1    | [2020-06-11T23:32:21,099][INFO ][o.e.n.Node               ] [es-node-0] initialized
elasticsearch-v3_1    | [2020-06-11T23:32:21,100][INFO ][o.e.n.Node               ] [es-node-0] starting ...
elasticsearch-v3_1    | [2020-06-11T23:32:21,377][INFO ][o.e.t.TransportService   ] [es-node-0] publish_address {172.18.0.7:9300}, bound_addresses {0.0.0.0:9300}
elasticsearch-v3_1    | [2020-06-11T23:32:21,471][INFO ][o.e.h.n.Netty4HttpServerTransport] [es-node-0] publish_address {172.18.0.7:9200}, bound_addresses {0.0.0.0:9200}
elasticsearch-v3_1    | [2020-06-11T23:32:21,472][INFO ][o.e.n.Node               ] [es-node-0] started
rabbitmq-ha_1         | Setting permissions for user "l5user" in vhost "/" ...
rabbitmq-ha_1         | 2020-06-11 23:32:22.152 [info] <0.709.0> Setting permissions for 'l5user' in '/' to '.*', '.*', '.*'
elasticsearch-v3_1    | [2020-06-11T23:32:22,243][INFO ][o.e.l.LicenseService     ] [es-node-0] license [4e93e032-8f16-44d7-98c2-f731da6e970e] mode [basic] - valid
elasticsearch-v3_1    | [2020-06-11T23:32:22,246][INFO ][o.e.g.GatewayService     ] [es-node-0] recovered [12] indices into cluster_state
elasticsearch-v3_1    | [2020-06-11T23:32:23,160][INFO ][o.e.c.r.a.AllocationService] [es-node-0] Cluster health status changed from [RED] to [YELLOW] (reason: [shards started [[audio_31a7][0]] ...]).
rabbitmq-ha_1         | 2020-06-11 23:32:23.505 [info] <0.716.0> Creating user 'celery_user'
rabbitmq-ha_1         | Adding user "celery_user" ...
rabbitmq-ha_1         | Error:
rabbitmq-ha_1         | User "celery_user" already exists
rabbitmq-ha_1         | Setting permissions for user "celery_user" in vhost "/" ...
rabbitmq-ha_1         | 2020-06-11 23:32:24.370 [info] <0.723.0> Setting permissions for 'celery_user' in '/' to '.*', '.*', '.*'
rabbitmq-ha_1         | Adding user "http_user" ...
rabbitmq-ha_1         | 2020-06-11 23:32:25.265 [info] <0.730.0> Creating user 'http_user'
rabbitmq-ha_1         | Error:
rabbitmq-ha_1         | User "http_user" already exists
rabbitmq-ha_1         | Setting permissions for user "http_user" in vhost "/" ...
rabbitmq-ha_1         | 2020-06-11 23:32:26.085 [info] <0.737.0> Setting permissions for 'http_user' in '/' to '', '', '.*'
rabbitmq-ha_1         | Setting tags for user "http_user" to [management] ...
rabbitmq-ha_1         | 2020-06-11 23:32:26.863 [info] <0.744.0> Setting user tags for user 'http_user' to [management]
rabbitmq-ha_1         | *** RabbitMQ user accounts ('l5user', 'celery_user' and 'http_user') setup. ***
frontend_1            | npm WARN react-dom@16.13.1 requires a peer of react@^16.13.1 but none is installed. You must install peer dependencies yourself.
frontend_1            | npm WARN acorn-jsx@5.0.1 requires a peer of acorn@^6.0.0 but none is installed. You must install peer dependencies yourself.
frontend_1            | npm WARN babel-eslint@11.0.0-beta.2 requires a peer of eslint@>= 6.0.0 but none is installed. You must install peer dependencies yourself.
frontend_1            | npm WARN chai-immutable@1.6.0 requires a peer of chai@>= 2.0.0 < 4 but none is installed. You must install peer dependencies yourself.
frontend_1            | npm WARN karma-requirejs@1.1.0 requires a peer of requirejs@^2.1.0 but none is installed. You must install peer dependencies yourself.
frontend_1            | npm WARN The package identity-obj-proxy is included as both a dev and production dependency.
frontend_1            | 
frontend_1            | audited 3553 packages in 20.624s
base_worker_1         | 2020-06-11 23:32:30,381 - [bugsnag] WARNING - No API key configured, couldn't notify
base_worker_1         | Traceback (most recent call last):
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/celery/app/utils.py", line 352, in find_app
base_worker_1         |     sym = symbol_by_name(app, imp=imp)
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/celery/bin/base.py", line 500, in symbol_by_name
base_worker_1         |     return imports.symbol_by_name(name, imp=imp)
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/kombu/utils/imports.py", line 62, in symbol_by_name
base_worker_1         |     return getattr(module, cls_name) if cls_name else module
base_worker_1         | AttributeError: module 'web' has no attribute 'tasks'
base_worker_1         | 
base_worker_1         | During handling of the above exception, another exception occurred:
base_worker_1         | 
base_worker_1         | Traceback (most recent call last):
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/bin/celery", line 8, in <module>
base_worker_1         |     sys.exit(main())
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/celery/__main__.py", line 16, in main
base_worker_1         |     _main()
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/celery/bin/celery.py", line 322, in main
base_worker_1         |     cmd.execute_from_commandline(argv)
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/celery/bin/celery.py", line 484, in execute_from_commandline
base_worker_1         |     super(CeleryCommand, self).execute_from_commandline(argv)))
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/celery/bin/base.py", line 273, in execute_from_commandline
base_worker_1         |     argv = self.setup_app_from_commandline(argv)
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/celery/bin/base.py", line 475, in setup_app_from_commandline
base_worker_1         |     self.app = self.find_app(app)
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/celery/bin/base.py", line 497, in find_app
base_worker_1         |     return find_app(app, symbol_by_name=self.symbol_by_name)
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/celery/app/utils.py", line 355, in find_app
base_worker_1         |     sym = imp(app)
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/celery/utils/imports.py", line 104, in import_from_cwd
base_worker_1         |     return imp(module, package=package)
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/importlib/__init__.py", line 126, in import_module
base_worker_1         |     return _bootstrap._gcd_import(name[level:], package, level)
base_worker_1         |   File "<frozen importlib._bootstrap>", line 986, in _gcd_import
base_worker_1         |   File "<frozen importlib._bootstrap>", line 969, in _find_and_load
base_worker_1         |   File "<frozen importlib._bootstrap>", line 958, in _find_and_load_unlocked
base_worker_1         |   File "<frozen importlib._bootstrap>", line 673, in _load_unlocked
base_worker_1         |   File "<frozen importlib._bootstrap_external>", line 673, in exec_module
base_worker_1         |   File "<frozen importlib._bootstrap>", line 222, in _call_with_frames_removed
base_worker_1         |   File "/opt/app/web/tasks/__init__.py", line 27, in <module>
base_worker_1         |     tasks_app = Celery('web', broker=settings.CELERY_BROKER_URL)
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 79, in __getattr__
base_worker_1         |     self._setup(name)
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 66, in _setup
base_worker_1         |     self._wrapped = Settings(settings_module)
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/site-packages/django/conf/__init__.py", line 157, in __init__
base_worker_1         |     mod = importlib.import_module(self.SETTINGS_MODULE)
base_worker_1         |   File "/home/l5user/.local/share/virtualenvs/app-ueEJiAOq/lib/python3.5/importlib/__init__.py", line 126, in import_module
base_worker_1         |     return _bootstrap._gcd_import(name[level:], package, level)
base_worker_1         |   File "<frozen importlib._bootstrap>", line 986, in _gcd_import
base_worker_1         |   File "<frozen importlib._bootstrap>", line 969, in _find_and_load
base_worker_1         |   File "<frozen importlib._bootstrap>", line 958, in _find_and_load_unlocked
base_worker_1         |   File "<frozen importlib._bootstrap>", line 673, in _load_unlocked
base_worker_1         |   File "<frozen importlib._bootstrap_external>", line 673, in exec_module
base_worker_1         |   File "<frozen importlib._bootstrap>", line 222, in _call_with_frames_removed
base_worker_1         |   File "/opt/app/videobysniply/settings.py", line 501, in <module>
base_worker_1         |     if settings.DEBUG:
base_worker_1         | NameError: name 'settings' is not defined
docker_base_worker_1 exited with code 1
frontend_1            | 
frontend_1            | 59 packages are looking for funding
frontend_1            |   run `npm fund` for details
frontend_1            | 
frontend_1            | found 3425 vulnerabilities (3422 low, 1 moderate, 2 high)
frontend_1            |   run `npm audit fix` to fix them, or `npm audit` for details
frontend_1            | 
frontend_1            | > rendering@ server /opt/app
frontend_1            | > webpack-dev-server --config webpack.config.dev.js
frontend_1            | 
frontend_1            | ℹ ｢wds｣: Project is running at http://0.0.0.0:3000/
frontend_1            | ℹ ｢wds｣: webpack output is served from http://localhost:3000/frontend/bundles/
frontend_1            | ℹ ｢wds｣: Content not from webpack is served from /opt/app
frontend_1            | ℹ ｢wds｣: 404s will fallback to /index.html


```