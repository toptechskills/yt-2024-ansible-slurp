# Code for Ansible YouTube video: How to read remote files into variables

[Video on YouTube](https://youtu.be/fXmPZNacitE). In the video I show how you can read remote files (i.e. files on target hosts) into variables using the `slurp`, `command` and `shell` module.

Spin up the Vagrant VMs (ARM VMs in this video, check out free dev env lesson of [Productive with Ansible course](https://learn.toptechskills.com/courses/productive-with-ansible) to see non-ARM setup):

```
vagrant up
```

Put demo `json` and `yaml` files in place on the VMs:

```
ssh 10.0.0.2

vi slurp.json
# {"key0": "...", "key1": "..."}

vi slurp.yaml
# key0: ...
# key1: ...
```

Run the playbooks:

```
ansible-playbook playbook.yml
ansible-playbook playbook_json.yml
ansible-playbook playbook_yaml.yml
ansible-playbook playbook_command.yml
ansible-playbook playbook_shell.yml
```
