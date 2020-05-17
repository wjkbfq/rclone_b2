# Rclone Github Action for backblaze B2
[wei/rclone: Wraps the rclone CLI to be used in Github Actions](wei/rclone)

This Action wraps [rclone](https://rclone.org) to enable syncing files and directories to and from different cloud storage providers.


## Features
 * "rsync for cloud storage"
 * sync to and from different cloud storage providers
 * backup files or deploy artifacts to remote storage


## Usage

### Github Actions
```
on: push
jobs:
  rclone:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: rclone
      uses: wei/rclone@v1
      env:
        RCLONE_CONF: ${{ secrets.RCLONE_CONF }}
      with:
        args: copy <source>:<source_path> <dest>:<dest_path>
```
`RCLONE_CONF` can be omitted if [CLI arguments](https://rclone.org/flags/#backend-flags) or [environment variables](https://rclone.org/docs/#environment-variables) are supplied. `RCLONE_CONF` can also be encrypted if [`RCLONE_CONFIG_PASS`](https://rclone.org/docs/#configuration-encryption) secret is supplied.

### Docker
```
docker run --rm -e "RCLONE_CONF=$(cat ~/.config/rclone/rclone.conf)" $(docker build -q .) \
  copy <source>:<source_path> <dest>:<dest_path>
```

## Author
[Wei He](https://github.com/wei) _github@weispot.com_


## License
[MIT](https://wei.mit-license.org)
