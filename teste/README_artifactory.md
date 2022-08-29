

# artifactory_proxy
Configuration to be applied to artifactory proxies.

Committing to master launches [https://ecm.jenkins.int.godaddy.com/job/ECM/job/artifactory_proxy] to apply iptables rules to production artifactory proxies


Go to the repository ECM/artifactory_proxy

Create a new branch and name it with jira ticket #. e.g. ASAA-3032.

### Edit iptables

Use any text editor to update the iptables file.
Add the specific entries using the format below:
```
 -A INPUT -s 54.183.54.138/32 -p tcp -m multiport --dports 80,443,10000:10100 -m comment --comment "WSS-tools SATT" -j ACCEPT
```
Save the iptables file.

commit it and push to origin.

Open the PR - Pull Request, merging it to branch __Master__.

Wait for the approval.


Merge it. __Click Merge pull request__ .

And confirm the merge clicking at __Confirm merge__ .

Delete the branch used to handle the ticket, to do it click __Delte branch__ .

Click __Delete branch__ and confirm.



