# Odoo Production Environment Template
## Using Odoo + Postgresql + Nginx with Docker-compose

## Odoo conf

<code>[options]
; Modules Config
addons_path = /mnt/extra-addons
; Security Config
admin_passwd = your_master_passwd
csv_internal_sep = ,
data_dir = /var/lib/odoo
; Database config
db_host = db ;Docker reference to postgre database
db_maxconn = 9
db_name = your_database
db_filter = your_database
db_password = your_db_password
db_port = 5432
db_template = template1
db_user = your_db_user
; Server Config
demo = {}
email_from = False
geoip_database = /usr/share/GeoIP/GeoLite2-City.mmdb
limit_memory_hard = 6000000000
limit_memory_soft = 6000000000
limit_request = 8192
limit_time_cpu = 43200
limit_time_real = 86400
limit_time_real_cron = -1
list_db = True
log_db = False
log_db_level = warning
log_handler = :INFO
log_level = info
logfile = None
logrotate = False
longpolling_port = 8072
max_cron_threads = 2
osv_memory_age_limit = 1.0
osv_memory_count_limit = False
pg_path = None
pidfile = None
proxy_mode = True
reportgz = False
server_wide_modules = web
smtp_password = False
smtp_port = 25
smtp_server = localhost
smtp_ssl = False
smtp_user = False
syslog = False
test_commit = False
test_enable = False
test_file = False
test_report_directory = False
translate_modules = ['all']
unaccent = False
without_demo = True
;workers = 5
xmlrpc = True
xmlrpc_port = 8069
xmlrpc_interface = 0.0.0.0</code>



## Nginx Default Config
server {
    listen [::]:80;
    listen 80;

    location ~ /.well-known/acme-challenge {
        allow all;
        root /var/www/html;
    }

    location / {
        proxy_set_header X-Real-IP  $remote_addr;
        proxy_set_header X-Forwarded-For $remote_addr;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header Host $host;
        proxy_pass http://odoo:8069;
    }

    location ~* /web/static/ {
        proxy_set_header X-Real-IP  $remote_addr;
        proxy_set_header X-Forwarded-For $remote_addr;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header Host $host;
        proxy_pass http://odoo:8069;
    }
}

