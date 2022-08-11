## Fichier /etc/gitlab/gitlab.rb

```
letsencrypt['auto_renew'] = true
letsencrypt['auto_renew_hour'] = "12"
letsencrypt['auto_renew_minute'] = "30" # Should be a number or cron expression, if specified.
letsencrypt['auto_renew_day_of_month'] = "*/7"
```


## Fichier runner-data/config.toml 

```
concurrent = 4
check_interval = 0

[session_server]
  session_timeout = 1500

[[runners]]
  name = "runner2"
  url = "https://${DOMAIN_GITLAB}/"
  token = "${TOKEN}"
  executor = "docker"
  [runners.docker]
    tls_verify = false
    image = "docker:dind"
    pull_policy = "if-not-present"
    privileged = true
    disable_entrypoint_overwrite = false
    oom_kill_disable = false
    disable_cache = false
    volumes = ["/var/run/docker.sock:/var/run/docker.sock"]
    shm_size = 0 
```
