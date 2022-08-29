
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

To add certificate pem files, please see this jenkins job - https://ecm.jenkins.int.godaddy.com/job/apiproxy_cert_install


## Steps-by-Step to perform Apiproxy.

- Clone apiproxy repository. "Check if you already have this repository local before clone."
- Edit <environment>/haproxy.yaml. Where <environment> could be [dev|test|prod].
    Add client: cn: and client name at backend entry.
- Run ./haproxy-configuration-builder/haproxy_configuration_builder/builder.py --conf [dev|test|prod]
- Commit it:
    - git add .
    - git commit -m "message."
    - git push 
- Create a PR in GitHub, repository ECM/apiproxy. Wait for approval.

4 - Install certificates at using the Jenkins job at: Jenkins Apiproxy-cert-install
- Confirm installation at slack channel <- check where to check it.>
- Go to GitHub:
    - ECM/apiproxy-cert-dev.  https://github.secureserver.net/ECM/apiproxy-certs-dev
    - ECM/apiproxy-cert-test. https://github.secureserver.net/ECM/apiproxy-certs-test
    - ECM/apiproxy-cert-prod. https://github.secureserver.net/ECM/apiproxy-certs-prod
<br/>
- Approve the PR and merge it. To do it you have to click at **Pull requests**, inside it select the specific **Pull Requests** related to the environment you are working with. First approve the Pull Request and after goes at botton of the page and click in **Merge pull request** and after **Confirm merge**.
- Run Apiproxy Jenkins job (Build Now) at: link...
- 
- 
- https://ecm.jenkins.int.godaddy.com/job/apiproxy_cert_install/

## Editing field

## Monitoring


## Knowledge Base





