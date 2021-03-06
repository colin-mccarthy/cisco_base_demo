# cisco_base_demo

Using DHCP option 67 you can push a script to the device to be executed using the Cisco ZTP process. This script will need to set up SSH connectivity between the device and Ansible Tower. Then with a provisioning callback URL and a host config key a host can contact Tower and request a configuration update using a job template. The request from the host must be a POST. Here is an example using curl:

```curl --data "host_config_key=5a8ec154832b780b9bdef1061764ae5a" https://10.42.0.42:443/api/v2/job_templates/22/callback/```


![callback][1]

Note the requesting host must be defined in the inventory associated with the job template. If Tower fails to locate the host, the request will be denied. That is why DHCP must be configured to assign the correct IP and that IP must be added into inventory before hand.

Successful requests create an entry on the Jobs page, where results and history can be viewed.


by default the host headers are  `REMOTE_HOST_HEADERS = ['REMOTE_ADDR', 'REMOTE_HOST']`
If you’re behind a load balancer you'll need to allow `HTTP_X_FORWARDED_FOR`


Usefull Links:

https://github.com/ansible/awx/blob/devel/awx/api/templates/api/job_template_callback.md




[1]: readme_pics/callback.jpg
