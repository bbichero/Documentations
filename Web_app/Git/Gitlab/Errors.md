**Errors**
------
[Official documentation maintenance](https://docs.gitlab.com/ce/administration/raketasks/maintenance.html)

Run a diagnostic check of all gitlab services:
```
sudo gitlab-rake gitlab:check
```
### Gitlab shell
---
Troubleshooting error for ssh git clone:
```
ssh -Tv git@${GITLAB_FQDN}
```

Rebuild `authorized_keys` file:
```
sudo gitlab-rake gitlab:shell:setup
```