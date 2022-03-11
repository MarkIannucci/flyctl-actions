# GitHub Actions for flyctl

This action wraps the flyctl CLI tool to allow deploying and managing fly apps.

## Usage

### Deploy

```yaml
name: Deploy to Fly
on: [push]
jobs:
  deploy:
    name: Deploy proxy
    runs-on: ubuntu-latest
    steps:
      # This step checks out a copy of your repository.
      - uses: actions/checkout@v2
      - uses: superfly/flyctl-actions@master
        env:
          FLY_API_TOKEN: ${{ secrets.FLY_API_TOKEN }}
        with:
          args: "deploy"
```


### Run one off scripts

```yaml
name: Run on Fly
on: [push]
jobs:
  deploy:
    name: Run script
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: superfly/flyctl-actions@master
        env:
          FLY_API_TOKEN: ${{ secrets.FLY_API_TOKEN }}
        with:
          args: "ssh console --command 'sh ./myscript.sh'"
```

See the [flyctl](https://github.com/superfly/flyctl) GitHub project for more information on using `flyctl`.

## Secrets

`FLY_API_TOKEN` - **Required**. The token to use for authentication. You can find a token by running `flyctl auth token` or going to your [user settings on fly.io](https://fly.io/user/personal_access_tokens).

