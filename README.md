<snippet>
  <content>

## create-netscaler-vip

This project is for creating a VIP on a Citrix Netscaler ADC.
<br>The script add servers,services,lb vserver and cs vserver. It was created for HTTP/HTTPS vips (these lb vserver services are HTTP) but it can be easily adapted to any service.
<br>In the vars file (group_vars/localVPX/vars) you have to define your tla name and the ip of th vip, the service type of the vip and the port , the server ip's.
<br>It was written to create content-switched vips but all modules have tags , so you can run any of them if you want only to create a server, service , lb vserver.
<br>When you run it you also need to specify the state(present/absent) of each part of the vip. Using absent you can remove any part of thw vip. You can also remove the whole vip if you want.
<br>The process of creating a vip needs 2 steps. So you need the run the script twice. This is because in the first step using a jinja template a svg file is created  and used in the step2 for binding the services to the lb vserver. 
<br>So step1 creates everything , but it can not bind the services to the lb vserver. Step2 it binds the services to the lb vserver.
<br>You can also remove the vip. This is also a 2 step process as you need to remove the cs vserver first (step1) and then you can remove all the other parts.

## Installation

It is written in Ansible (ansible 2.7.1) The python version used is 2.7.12.
<br> Also you need the Nitro API python SDK.

## Usage

you create a  whole vip like this:
<br>Step1 : ansible-playbook -i inventory  create_cs.yml  -e "server_state=present service_state=present lb_state=present cs_state=present"  --skip-tags bindservices
<br>Step2 : ansible-playbook -i inventory  create_cs.yml  -e "server_state=present service_state=present lb_state=present cs_state=present"  --tags bindservices

you can also remove the vip like this:
<br>Step1 : ansible-playbook -i inventory  create_cs.yml  -e "server_state=present service_state=present lb_state=present cs_state=absent"  --skip-tags bindservices
<br>Step2 : ansible-playbook -i inventory  create_cs.yml  -e "server_state=absent service_state=absent lb_state=absent cs_state=absent"  --skip-tags bindservices
## Credits

This was written by Mihai Cziraki
</content>
</snippet>
