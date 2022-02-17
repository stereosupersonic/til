# Organize playbooks with tasks

```
tasks:
  - import_tasks: tasks/imported-tasks.yml
```
Just like with variable include files, tasks are formatted in a flat list in the included file. As an example, the

tasks/imported-tasks.yml could look like this:
```
---
- name: Add profile info for user.
  copy:
    src: example_profile
    dest: "/home/{{ username }}/.profile"
    owner: "{{ username }}"
    group: "{{ username }}"
    mode: 0744
- name: Add private keys for user.
  copy:
    src: "{{ item.src }}"
    dest: "/home/{{ username }}/.ssh/{{ item.dest }}"
    owner: "{{ username }}"
    group: "{{ username }}"
    mode: 0600
  with_items: "{{ ssh_private_keys }}"
- name: Restart example service.
  service:
    name: example
    state: restarted
```
