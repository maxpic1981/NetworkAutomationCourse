# **Week 3: Data model**

## **Overview**

The ansible playbooks in this directory is to generate the data model and the configurations files for each node. It use a simple leaf and spine topology. 

![Data model diagram](https://github.com/maxpic1981/NetworkAutomationCourse/blob/master/Week-3/Leaf%20and%20Spine%20-%20GNS3.png "GNS3 Leaf and Spine diagram")


## **Data model**

Infrastructure data model is in the file *fabric.yml* and contains the following field:

* **Links:** Details about the links between the node. (*left, right, as, ipv4 address, ports*)
* **Nodes:** Details about the node. (*name, router-id, management ip, management interface, bgp asn*)

There is no service playbook because the information related to the service are include in the fabric.yml file (bgp as). 


## Playbooks:

The following playbooks is use to generate the data model and the nodes configurations:

* **create-data-model.yml:** generathe the file **nodes.yml* that contain the data model representation for each nodes.

*nodes.yml example:*
```yaml
---

nodes:
 S1:
   rid: 1.1.1.1
   as: 65001 
   
   interfaces:
     FastEthernet0/1:   { ipv4: 10.0.12.1  }
     FastEthernet0/0:   { ipv4: 10.0.11.1 }
     FastEthernet1/0:   { ipv4: 10.0.10.11 }

   ebgp:
     LE2:   { ipv4: 10.0.12.2, neighbor_as: 65102  }
     LE1:   { ipv4: 10.0.11.2, neighbor_as: 65101  }
```

* **gen_base_config.yml:** Generate the base configuration and the interface configuration based from the *nodes.yml* file.

* **gen_bgp_config.yml:** Service playbook that generate the bgp configuration for each nodes based from the *nodes.yml* file.



