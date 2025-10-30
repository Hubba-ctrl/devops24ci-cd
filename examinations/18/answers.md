# QUESTION A
#!/usr/bin/env python3
from ansible.module_utils.basic import AnsibleModule

def reverse(text: str) -> str:
    return text[::-1]

def main() -> None:
    mod = AnsibleModule(
        argument_spec=dict(
            message=dict(type="str", required=False, default="This is a really fun default"),
        ),
        supports_check_mode=True,
    )

    orig_msg = mod.params["message"]
    rev_msg = reverse(orig_msg)

    if orig_msg == "fail me":
        mod.fail_json(
            msg="You requested this to fail",
            changed=True,
            original_message=orig_msg,
            reversed_message=rev_msg
        )
    elif orig_msg == rev_msg:
        mod.exit_json(
            changed=False,
            original_message=orig_msg,
            reversed_message=rev_msg
        )
    else:
        mod.exit_json(
            changed=True,
            original_message=orig_msg,
            reversed_message=rev_msg
        )

if __name__ == "__main__":
    main()


# QUESTION B
mkdir -p  ~/.ansible/plugins/modules

# QUESTION C 
---
- name: Use my own anagrammer module
  hosts: all
  gather_facts: false

  tasks:
    - name: Test anagrammer default
      anagrammer:
        message: "{{ message | default(omit) }}"
      register: result

    - name: Show result
      ansible.builtin.debug:
        var: result

    - name: test anagrammer
      anagrammer:
        message: "{{ item }}"
      loop:
        ["testar", "sirap i paris", "fail me"]



# BONUS QUESTION

In Python, values like 0, "", [], and None are false, while everything else is true.
Ansible works kind of the same, but it also counts strings like "yes", "true", or "on" as true, and "no", "false", or "off" as false.
To make sure Ansible reads it right, I’d just use filters like | bool or | type_debug so I know what’s actually being checked.