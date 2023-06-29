# Scheduling
## Manual Scheduling
Scheduling means making usre pods are matched to nodes so that they can be run. They can handle pods from different namespaces. 

- We can specify the node in the initial YAML file:

![](images/2.3.png)

- We can also create a file to bind the pod to a node:

![](images/2.4.png)
Here we specify the node, and bind it to 