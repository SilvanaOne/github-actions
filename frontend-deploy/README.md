# Frontend Deploy

This action sets up Node.js, installs dependencies from `package.json`, build a package and deploy it via SSH to the remote server.


## Example

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout GitHub Actions
      uses: actions/checkout@v3
      with:
        repository: Staketab/github-actions
        path: .github/actions
        token: ${{ secrets.GH_TOKEN }}

    - name: Deploy React.js
      uses: ./.github/actions/frontend-deploy
      with:
        webroot: /var/www
        ssh_hostname: ${{ secrets.IP_ADDRESS }}
        ssh_username: ${{ secrets.SERVER_USERNAME }}
        ssh_password: ${{ secrets.SSH_KEY }}
        lib_latest: true
        keep_source_maps: true
        nodejs_version: 14.x
        github_token: ${{ secrets.GH_TOKEN }}
```


## Inputs

| Name               | Requirement | Default | Description                                   |
| ------------------ | ----------- | ------- | --------------------------------------------- |
| `domain`           | *required*  |         | Domain name                                   |
| `ssh_hostname`     | *required*  |         | SSH hostname                                  |
| `ssh_username`     | *required*  |         | SSH username                                  |
| `ssh_password`     | *required*  |         | SSH password                                  |
| `lib_latest`       | *optional*  | `false` | Install the latest version of `@staketab/lib` |
| `keep_source_maps` | *optional*  | `true`  | Keep JavaScript Source Maps                   |
| `nodejs_version`   | *optional*  | `14.x`  | Node.js version                               |
| `github_token`     | *required*  |         | GitHub Personal Access Token (PAT)            |