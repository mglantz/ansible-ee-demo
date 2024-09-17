# ansible-ee-demo

A demonstration of how to build execution environments

# Prerequisites
* A system to build on
* ansible-builder
* Podman or docker (podman preferred)
* Access to a container base image to start from

You can, for example, install ansible-builder and podman as such:
```
pip3 install ansible-builder podman
```

# Simple version
If you only need to add a specific collection to an existing execution environment, you only have to create the two files shown in the ```simple``` directory. Try to build the defined execution enviroment as such:

* Clone this repository:
```
git clone https://github.com/mglantz/ansible-ee-demo
```

* Login to registry.redhat.io using the podman command.
```
podman login registry.redhat.io
```

* Inspect the files stored in the simple directory.
```
cd simple
# Main configuration file
cat execution-environment.yml

# File which contains the Ansible requirements
cat requirements.yml
```

* Run the ansible-builder command to create your new execution environment
```
# from the simple directory
ansible-builder build -v3 -t simple-custom-ee --build-arg EE_BASE_IMAGE=registry.redhat.io/ansible-automation-platform-21/ee-minimal-rhel8:latest
```

# Advanced version
If you need to add things such as Python and RPM requirements and further modifications, we will need to use some additional features of ansible-builder.

To build an more advanced example of a custom execution enviroment, follow these steps:

* Clone this repository:
```
git clone https://github.com/mglantz/ansible-ee-demo
```

* Login to registry.redhat.io using the podman command.
```
podman login registry.redhat.io
```

* Inspect the files stored in the advanced directory.
```
cd advanced

# Main configuration file
cat execution-environment.yml

# File which contains the Ansible dependencies
cat requirements.yml

# File which contains Python dependencies
cat requirements.txt

# File which contains RPM dependencies
cat bindep.txt
```

* Build the more advanced customer execution-environment as such:
```
ansible-builder build -v3 -t advanced-custom-ee --build-arg EE_BASE_IMAGE=registry.redhat.io/ansible-automation-platform-21/ee-minimal-rhel8:latest
```
