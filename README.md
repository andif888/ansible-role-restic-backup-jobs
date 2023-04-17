# ansible-role-restic-backup-jobs

Role to create Restic backup jobs and scripts in cron scheduler. Restic must be on PATH.

## Table of content

- [Default Variables](#default-variables)
  - [restic_backup_jobs](#restic_backup_jobs)
  - [restic_backup_jobs_enable](#restic_backup_jobs_enable)
  - [restic_backup_jobs_install_path](#restic_backup_jobs_install_path)
  - [restic_backup_jobs_s3_bucket_name](#restic_backup_jobs_s3_bucket_name)
  - [restic_backup_jobs_s3_endpoint](#restic_backup_jobs_s3_endpoint)
  - [restic_backup_jobs_s3_repo](#restic_backup_jobs_s3_repo)
  - [restic_backup_jobs_s3_repo_access_key](#restic_backup_jobs_s3_repo_access_key)
  - [restic_backup_jobs_s3_repo_password](#restic_backup_jobs_s3_repo_password)
  - [restic_backup_jobs_s3_repo_secret_key](#restic_backup_jobs_s3_repo_secret_key)
  - [restic_backup_jobs_username](#restic_backup_jobs_username)
- [Discovered Tags](#discovered-tags)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Default Variables

### restic_backup_jobs

Job definition

#### Default value

```YAML
restic_backup_jobs: []
```

#### Example usage

```YAML
restic_backup_jobs:
  - name: "dfs"
    dirs:
      - "/srv/samba"
    excludes:
      - _tmp*
      - '*.bak'
    month: "*"
    weekday: "*"
    day: "*"
    hour: "22"
    minute: "13"
    user: "{{ restic_backup_jobs_username }}"
    state: present
    disabled: true
    retention:
      keep_last: 1
      # keep_hourly: 1
      keep_daily: 7
      keep_weekly: 4
      # keep_monthly: 6
      # keep_yearly
```

### restic_backup_jobs_enable

Enable restic backup for samba shares.

#### Default value

```YAML
restic_backup_jobs_enable: false
```

### restic_backup_jobs_install_path

Path to store scripts

#### Default value

```YAML
restic_backup_jobs_install_path: /root
```

### restic_backup_jobs_s3_bucket_name

Minio S3 bucket name for restic backup storage.

#### Default value

```YAML
restic_backup_jobs_s3_bucket_name: restic-{{ inventory_hostname }}
```

### restic_backup_jobs_s3_endpoint

Minio S3 endpoint for restic backup storage.

Example:

```yaml

backup__base__restic_s3_endpoint: "https://minio.{{ dns_domain }}"

restic_backup_jobs_s3_endpoint: "{{ backup__base__restic_s3_endpoint }}"

```

#### Default value

```YAML
restic_backup_jobs_s3_endpoint: '{{ backup__base__restic_s3_endpoint }}'
```

### restic_backup_jobs_s3_repo

Minio S3 repo URL for restic backup storage.

#### Default value

```YAML
restic_backup_jobs_s3_repo: s3:{{ restic_backup_jobs_s3_endpoint }}/{{ restic_backup_jobs_s3_bucket_name
  }}
```

### restic_backup_jobs_s3_repo_access_key

Minio S3 repo access key for restic backup storage.

#### Default value

```YAML
restic_backup_jobs_s3_repo_access_key: '{{ backup__base__restic_s3_repo_access_key
  }}'
```

### restic_backup_jobs_s3_repo_password

Minio S3 repo password for restic backup storage.

#### Default value

```YAML
restic_backup_jobs_s3_repo_password: '{{ backup__base__restic_s3_repo_password }}'
```

### restic_backup_jobs_s3_repo_secret_key

Minio S3 repo secret key for restic backup storage.

#### Default value

```YAML
restic_backup_jobs_s3_repo_secret_key: '{{ backup__base__restic_s3_repo_secret_key
  }}'
```

### restic_backup_jobs_username

username

#### Default value

```YAML
restic_backup_jobs_username: root
```

## Discovered Tags

**_backup-init-restic_**\
&emsp;Init backup if restic is enabled.

**_backup-list-restic_**\
&emsp;List backups if restic is enabled.

**_backup-restic_**\
&emsp;Run backup if restic is enabled.

**_never_**

**_restore-restic_**\
&emsp;Run restore if restic is enabled.

**_restore-restic-single_**\
&emsp;Run single item restore if restic is enabled.


## Dependencies

None.

## License

license (GPL-2.0-or-later, MIT, etc)

## Author

andif888
