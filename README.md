# foreman_installer

Role to interact with foreman-installer

## Requirements

N/A

## Role Variables

```yaml
vars:
  foreman_installer:
    foreman_installer_pkg:          # foreman installer package. You probably want either "foreman-installer" or "foreman-installer-katello".
    foreman_installer_verbose:      # Run the installe with -v option
    foreman_installer_scenario:     # Scenario. Required
    installer_scenarios_answers:    # Dict of custom answers that for the installer. This is merged with your scenarios default answers in the {{ scenario }}-answers.yml file 
    foreman_installer_options: []   # Array of extra options to pass to whenever the installer is ran
    katello_ca:                     # String containing the custom CA cert. Katello Only.
    katello_cert:                   # String containing the custom cert. Katello Only.
    katello_key:                    # String containing the custom key. Katello Only.
    katello_csr:                    # String containing the custom csr. Katello Only.
    katello_certs_dir:              # Directory to store the certificates
    update_certs:                   # Set to True to force Certificate Update.
```

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

### Basic Foreman scenario

```yaml
    - hosts:
      - foreman.example.com
      roles:
        - role: foreman_installer
          foreman_installer_scenario: foreman
          installer_scenarios_answers:
            foreman:
              admin_password: changeme
```

### Katello scenario with custom certificates

```yaml
    - hosts:
      - foreman.example.com
    var_files:
      - group_vars/vault_certs.yml
    roles:
       - role: foreman_installer
         foreman_installer_pkg: foreman-installer-katello
         foreman_installer_scenario: katello
         installer_scenarios_answers:
           foreman:
             admin_password: changeme
         katello_ca: "{{ vault_katello_ca }}"
         katello_cert: "{{ vault_katello_cert }}"
         katello_key: "{{ vault_katello_key }}"
         katello_csr: "{{ vault_katello_csr }}"

```
