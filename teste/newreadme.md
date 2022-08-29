# Apiproxy
Apiproxy configurations

Updating the envionment specific haproxy.cfg file and checking into master on this repo will trigger
https://ecm.jenkins.int.godaddy.com/job/ECM/job/apiproxy/job/master
which lays down the file in the appropriate apiproxy environment and reloads the config.

The haproxy.cfg files in this repo should no longer be edited directly.   They are built from the
yaml config file in environments/[dev|test|prod]/haproxy.yaml .   Update this file, then
to rebuild config...
```
./haproxy-configuration-builder/haproxy_configuration_builder/builder.py --conf [dev|test|prod]
```
Note: you will also need ruby installed

To add certificate pem files, please run this jenkins job - [apiproxy_cert_install](https://ecm.jenkins.int.godaddy.com/job/apiproxy_cert_install)

### Steps-by-Step to perform Apiproxy.

Clone apiproxy repository. "Check if you already have this repository local before clone."
Edit <environment>/haproxy.yaml. Where <environment> could be [dev|test|prod]. Add client: cn: and client name at backend entry.

Run ./haproxy-configuration-builder/haproxy_configuration_builder/builder.py --conf [dev|test|prod]
    
Commit it and push to origin:
    - git add .
    - git commit -m "message."
    - git push 
Create a PR in GitHub, repository ECM/apiproxy. Wait for approval.

Install certificates at using the Jenkins job at: Jenkins [apiproxy_cert_install](https://ecm.jenkins.int.godaddy.com/job/apiproxy_cert_install).
Confirm installation at [ecm_monitors](https://godaddy.slack.com/archives/C04S9FGV4) slack channel.
<br/>
- Go to the spedific GitHub repository:
    - [ECM/apiproxy-cert-dev](https://github.secureserver.net/ECM/apiproxy-certs-dev)
    - [ECM/apiproxy-cert-test](https://github.secureserver.net/ECM/apiproxy-certs-test)
    - [ECM/apiproxy-cert-prod](https://github.secureserver.net/ECM/apiproxy-certs-prod)
<br/>
Approve the PR and merge it.
<br/>
To do it you have to click at **Pull requests**, inside it select the specific **Pull Requests** related to the environment you are working with. First approve the Pull Request and after goes at botton of the page and click in **Merge pull request** and after **Confirm merge**.
Run Apiproxy Jenkins job (Build Now) at [apiproxy](https://ecm.jenkins.int.godaddy.com/job/ECM/job/apiproxy/job/master/).
<br/>

[apiproxy_cert_install](https://ecm.jenkins.int.godaddy.com/job/apiproxy_cert_install/) job.
<br/>

### haproxy.yaml editing fields
<br/>
At haproxy.yaml file you will edit to add the client name, cn and client name under the backend, below you have a sample of it.
<br/>
<br/>
e.g.
<br/>
Adding access for WS Integration Provisioning API on APIProxy.
<br/>
<br/>
Request:
<br/>
What is the backend API or APIProxy endpoint? - messaging.apiproxy.test.ext.godaddy.com
<br/>
Is this a new backend for APIProxy? - No
<br/>
What is the common name (CN) of the client cert you will use? - provisioning.api.client.test -sucuri.net
<br/>
Is this a new client to APIProxy? - Yes
<br/>
Is this a new CN→Backend mapping? - Yes
<br/>
Renewing an existing cert? - No
<br/>
<br/>
ECM/apiproxy/environments/test/haproxy.yaml
<br/>
```
./haproxy-configuration-builder/haproxy_configuration_builder/builder.py --conf [dev|test|prod]
```
```
---
client: provisioning
cn: provisioning.api.client.test-sucuri.net
---
```
and
```
<br/>
Messaging does not accept new entries.
<br/>
```
<br/>
### Monitoring

Monitoring is displayed at "ecm_monitors Slack channel". It will display a message with # job you runned at the jenkins job with a GREEN mark for success or RED mark for failure.

[ecm_monitors](https://godaddy.slack.com/archives/C04S9FGV4) - Slack channel.

### Knowledge Base

If you have a RED error message at ecm_monitor check if you ran the jenkins job.
