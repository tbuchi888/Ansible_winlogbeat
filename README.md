# Ansible_winlogbeat
This is playbook to install winlogbeat on Windows server 2012.
I made this playbook in reference to the contents of the following official sites.
https://www.elastic.co/guide/en/beats/winlogbeat/current/winlogbeat-getting-started.html

## Preparing for Step
### Please download the following as a precondition beforehand.

- files/winlogbeat-1.2.3-windows.zip
  - [winlogbeat-1.2.3-windows.zip](https://download.elastic.co/beats/winlogbeat/winlogbeat-1.2.3-windows.zip)
  - [sha1](https://download.elastic.co/beats/winlogbeat/winlogbeat-1.2.3-windows.zip.sha1.txt)
- files/pscx.msi
  - [pscx.msi](http://download-codeplex.sec.s-msft.com/Download/Release?ProjectName=pscx&DownloadId=923562&FileTime=130585918034470000&Build=20959)

### And make a file templates/winlogbeat.yml.j2

Please make "winlogbeat.yml.j2" which changed `winlogbeat.yml` to as follows.

```
#diff winlogbeat.yml winlogbeat.yml.j2
42c42
<     hosts: ["localhost:9200"]
---
>     hosts: ["{{ elas_hosts }}:{{ elas_hosts_port }}"]
```

### Set variables for your Elasticsearch
Please change variables of IPaddress or hostname and port for your Elasticsearch hosts on install_winlogbeat.yml.

```
  vars:
# Elasticsearch hosts
    elas_hosts: 172.23.252.19
    elas_hosts_port: 9200
# reinstall winlogbeat
    reinstall: true
```
