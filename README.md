# Usage

Fist you need a gist or repo to store your env secrets

- Make a fork of this [gist](https://gist.github.com/datphan/f6281d95065d3b942f13a8436768669f) and store it as `SECRET_GIST_URL`

- Follow the gist [README.md](https://gist.github.com/datphan/f6281d95065d3b942f13a8436768669f#file-readme-md)

Then modify your github actions workflows:

```yaml
jobs:
  job-name:
    # ....
    steps:
      # ....
      - name: Prepare secrets and environments
        uses: singulcode/decrypt-export-env-action@master
        with:
          gistUrl: ${{ env.SECRET_GIST_URL }}
          path: .tmpsecrets
          envFile: .tmpsecrets/.env1|.tmpsecrets/.env2
          ageSecretKey: ${{ secrets.AGE_SECRET_KEY }}
      # ....
      - name: Test
        run: |
          echo $PUBLIC_ENV
          echo $RANDOM_ENV
          echo $MASKED_ACCESS_KEY
          echo $MASKED_SOME_SECRET
          echo $SOME_EMAIL_ALSO_MAKSED
```

# Options

Field | Required | Example
------------ | ------------  | -------------
**gistUrl** | YES | Ex: `git@gist.github.com:f6281d95065d3b942f13a8436768669f.git`
**path** | NO | Ex: `.tmpsecrets` (default) | 
**ageSecretKey** | YES | Ex: `AGE-SECRET-KEY123------------------------------------------------------456`
**envFile** | YES | Ex: `.tmpsecrets/.env1|.tmpsecrets/.env2`
**excludeEnv** | NO | Ex: `EXCLUDE_ENV|RANDOM_ENV_TEST`
**maskEnv** | NO | Ex: `SOME_ENV_NEED|OTHER_ENV|.*RANDOM_ENV|PREFIX_.*`