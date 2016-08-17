# Ansible_winlogbeat
This is playbook to install winlogbeat on Windows server 2012.
I made this playbook in reference to the contents of the following official sites.
https://www.elastic.co/guide/en/beats/winlogbeat/current/winlogbeat-getting-started.html

## Preparing for Step
### Elastisearch and Kibana
You must prepare for the environment of Elastisearch and Kibana.
For example, 
You can build environment in the following on Docker 
if you are the environment where you use docker-compose.

```
git clone https://github.com/tbuchi888/elasticsearch-kibana-docker-compose.git
cd elasticsearch-kibana-docker-compose
docker-comporse up -d
```

### Please download the following as a precondition beforehand.
- files/winlogbeat-1.2.3-windows.zip
  - [winlogbeat-1.2.3-windows.zip](https://download.elastic.co/beats/winlogbeat/winlogbeat-1.2.3-windows.zip)
  - [sha1](https://download.elastic.co/beats/winlogbeat/winlogbeat-1.2.3-windows.zip.sha1.txt)
- files/pscx.msi
  - [pscx.msi](http://download-codeplex.sec.s-msft.com/Download/Release?ProjectName=pscx&DownloadId=923562&FileTime=130585918034470000&Build=20959)

### And make a file templates/winlogbeat.yml.j2
Please make "winlogbeat.yml.j2" which changed `winlogbeat.yml` to as follows.
As follows in the case of winlogbeat-1.2.3.

```
#diff winlogbeat.yml winlogbeat.yml.j2
42c42
<     hosts: ["localhost:9200"]
---
>     hosts: ["{{ elas_hosts }}:{{ elas_hosts_port }}"]
```

### Set variables for your Elasticsearch
Please change variables of IPaddress or hostname and port for 
your Elasticsearch hosts on 'install_winlogbeat.yml'.

```
  vars:
# Elasticsearch hosts
    elas_hosts: 192.168.33.100
    elas_hosts_port: 9200
# reinstall winlogbeat
    reinstall: true
```

### Change hosts for your environment of Windows servers
You must change inventory hosts file of Ansible for your environment of Windows servers.

## Run Playbook

```
ansible-playbook -i hosts install_winlogbeat.yml -v
```

## Caution
This program is free software; you can redistribute it and/or modify it under
the terms of the GNU General Public License as published by the Free Software
Foundation; either version 2 of the License, or (at your option) any later
version.

This program is distributed in the hope that it will be useful, but WITHOUT
ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS
FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with
this program. If not, see http://www.gnu.org/licenses/.
