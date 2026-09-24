# Role: apt_thirdparty

## Example playbook

```yaml
---
- hosts: all
  become: true
  roles:
    - ansible-suite.apt_thirdparty
```

### Multiple packages installation example
```yml
---
- hosts: all
  become: true
  tasks:
    - name: Installation of multiple third-party packages
      ansible.builtin.include_role:
        name: ansible-role-apt_thirdparty
      vars:
        apt_thirdparty_pkg: "{{ item.name }}"
        apt_thirdparty_pkg_install_mode: url
        apt_thirdparty_pkg_url: "{{ item.url }}"
      loop:
        - name: package1
          url: https://example.com/package1.deb
        - name: package2
          url: https://example.com/package2.deb
```

## Role Variables

A description of the available variables (`defaults/main.yml`) is provided below:

| Variable | Default | Description |
| --- | --- | --- |
| `apt_thirdparty_state` | `present` | General state of the role resources (`present` or `absent`). |
| `apt_thirdparty_repo_format` | `deb822` | Format of the repository configuration (`deb822` or `line`). |
| `apt_thirdparty_repo_line_remove` | `{{ apt_thirdparty_repo_format != 'line' }}` | Automatically clean up legacy line-based repo files if deb822 is active. |
| `apt_thirdparty_repo_suite` | `{{ ansible_distribution_release }}` | Distribution release codename (e.g., `bookworm`, `jammy`). |
| `apt_thirdparty_repo_components` | `[main]` | List of repository components. |
| `apt_thirdparty_unattended_upgrades_filename` | `"90unattended-upgrades-{{ apt_thirdparty_repo_name }}"` | Filename for unattended-upgrades configuration. |
| `apt_thirdparty_unattended_upgrades_origins_patterns` | Dynamic based on allowed origins | Patterns defining allowed origins for automatic upgrades. |
| `apt_thirdparty_unattended_upgrades_allowed_origins` | `[]` | List of allowed origins for unattended upgrades. |
