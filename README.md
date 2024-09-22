# Ansible Role: Nomad TLS Certificate Generation

This Ansible role generates TLS certificates for [HashiCorp Nomad](https://www.nomadproject.io/) using the built-in `nomad tls` commands. It creates a self-signed certificate authority (CA), a server certificate, a client certificate, and a CLI certificate. The certificates are stored in the specified directory.

## Features

- **Automated TLS Certificate Creation**: Automatically generates Nomad TLS certificates (CA, server, client, and CLI certificates) using the `nomad tls` commands.
- **Customizable Directory**: Certificates can be stored in a directory of your choice by overriding the `nomad_tls_certificates_directory` variable.
- **Idempotent Execution**: Each certificate creation task checks if the certificate already exists and skips the task if the certificate is already present, ensuring that the role can be run multiple times without overwriting existing files

## Requirements

- The `nomad` CLI must be installed on the target machine where this role is being executed.

## Role Variables

Here are the role variables and their default values. You will need to override them in your playbook or inventory to suit your environment:

| Variable | Description | Default |
| - | - | - |
| nomad_tls_certificates_directory | Path to the directory where certificates will be stored. Defaults to the playbook's directory. | "{{ playbook_dir }}" |

## Example Playbook

```yaml
- hosts: servers
  become: true
  roles:
    - role: dsegurag.nomad_tls_certificates
      vars:
        nomad_tls_certificates_directory: "/etc/nomad/tls"
```

## Dependencies

- **Nomad CLI**: The `nomad` CLI is required to create the TLS certificates. If Nomad is not installed on your target machine, you can use [this Ansible role](https://github.com/dsegurag/ansible-role-nomad-installation) to install Nomad easily.

## License

MIT License

## Author Information

This role was created by Daniel Segura.
