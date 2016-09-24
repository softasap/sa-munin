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


After install you can get suggestions, what other plugins you can use on your host:

```

/etc/munin$ sudo munin-node-configure --suggest
Plugin                     | Used | Suggestions                            
------                     | ---- | -----------                            
acpi                       | no   | no [cannot read /proc/acpi/thermal_zone/*/temperature]
amavis                     | no   | no                                     
apache_accesses            | no   | no [LWP::UserAgent not found]          
apache_processes           | no   | no [LWP::UserAgent not found]          
apache_volume              | no   | no [LWP::UserAgent not found]          
apc_envunit_               | no   | no [no units to monitor]               
bonding_err_               | no   | no [No /proc/net/bonding]              
courier_mta_mailqueue      | no   | no [spooldir not found]                
courier_mta_mailstats      | no   | no [could not find executable]         
courier_mta_mailvolume     | no   | no [could not find executable]         
cps_                       | no   | no                                     
cpu                        | yes  | yes                                    

```

# combining with other roles

I recommend adding conf.d dir both, for master and node configs.
This will allow to template with ansible independent parts of configuration in the separate files,
and don't be scared, that fuzzy regexp's will ruin master config file.

```
includedir /etc/munin/munin-conf.d
```

If you need to do it in the middle of the roles play, you can use include role.
See example of such role here:  https://github.com/softasap/sa-include
