# ansible-role-update_sync_haproxy_certs_config

Configures HAProxy certificate sync from S3. Intended for ASP use. Requires `ansible-role-sync_haproxy_certs` to have been baked into the AMI.

## Variables

Configured via the `_acme` dict (set by caller from `ACME` vars):

| Key | Default | Description |
|-----|---------|-------------|
| `s3_bucket` | `""` | S3 bucket to sync certs from (required) |
| `ssl_path` | `/etc/haproxy/ssl` | Local target directory |
| `instance_name` | `haproxy` | systemd service name to reload on cert change |

## Usage

```yaml
# vars/acme.yml
ACME:
  s3_bucket: "my-acme-bucket"

# site.yml
- ansible.builtin.set_fact:
    _acme: "{{ ACME }}"

- role: update_sync_haproxy_certs_config
  tags: [sync_haproxy_certs]
```
