sa-munin
========

[![Build Status](https://travis-ci.org/softasap/sa-munin.svg?branch=master)](https://travis-ci.org/softasap/sa-munin)


Simple usage for node:

```
roles:
     - {
         role: "sa-munin"
       }

```

Simple usage for master:

```
roles:
     - {
         role: "sa-munin",
         munin_mode: master
       }

```



Exposing munin via nginx:

```
location /munin/static/ {
        alias /etc/munin/static/;
        expires modified +1w;
}

location /munin/ {
        auth_basic            "Restricted";
        # Create the htpasswd file with the htpasswd tool.
        auth_basic_user_file  /etc/nginx/htpasswd;

        alias /var/cache/munin/www/;
        expires modified +310s;
}
```
