# Rclone Github Action for backblaze B2

> Fork from [wei/rclone: Wraps the rclone CLI to be used in Github Actions](wei/rclone)


## Features
- This Action wraps [rclone](https://rclone.org) to enable syncing files and directories from github repository to backblaze B2 cloud storage bucket.
- All files exclude "/{.git,.github}/".


## Usage

### workflow.yml Example

```sh
on: push
jobs:
  rclone:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: <workflow_name>
      uses: wjkbfq/rclone_b2@master
      env:
        RCLONE_CONF: ${{ secrets.RCLONE_CONF }}
      with:
        args: sync --exclude "/{.git,.github}/" ./ <storage_name>:<bucket_name>/
```

### Environment Variables
| Key             | Value                       | Type   | Required |
| --------------- | --------------------------- | ------ | -------- |
| <workflow_name> | Workflow name               | String | No       |
| <storage_name>  | Storage name in RCLONE_CONF | String | Yes      |
| <bucket_name>   | Storage bucket name         | String | Yes      |

### Secret Variables
| Key         | Value                            | Type    | Required |
| ----------- | -------------------------------- | ------- | -------- |
| RCLONE_CONF | Rclone configuration information | Secrets | Yes      |

### RCLONE_CONF Example
`RCLONE_CONF` can be omitted if [CLI arguments](https://rclone.org/flags/#backend-flags) or [environment variables](https://rclone.org/docs/#environment-variables) are supplied. `RCLONE_CONF` can also be encrypted if [`RCLONE_CONFIG_PASS`](https://rclone.org/docs/#configuration-encryption) secret is supplied.

```sh
[<storage_name>]
type = b2
account = <applicationKey_ID>
key = <applicationKey>
hard_delete = true
```

### Docker

```sh
docker run --rm -e "RCLONE_CONF=$(cat ~/.config/rclone/rclone.conf)" $(docker build -q .) \
  sync --exclude "/{.git,.github}/" ./ <storage_name>:<bucket_name>/
```

## Author
- [Wei He](https://github.com/wei) _github@weispot.com_
- [wjkbfq (wz)](https://github.com/wjkbfq) _k@kunn.cc_

## License
[MIT](https://wei.mit-license.org)

## end
