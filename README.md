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
          repoUrl: git@gist.github.com:f6281d95065d3b942f13a8436768669f.git
          # token: ${{ secrets.GH_PAT }}
          # path: .tmpsecrets
          envFile: .tmpsecrets/.develop.ci-cd
          ageSecretKey: ${{ secrets.AGE_SECRET_KEY }}
      # ....
      - name: Test
        run: |
          set -e

          echo "PUBLIC_ENV: ${PUBLIC_ENV}"
          echo "RANDOM_ENV: ${RANDOM_ENV}"
          echo "MYSQL_ENV: ${MYSQL_ENV}"
          echo "KEY_ENV: ${KEY_ENV}"
          echo "TOKEN_ENV: ${TOKEN_ENV}"
          echo "PASSWORD_ENV: ${PASSWORD_ENV}"
          echo "SECRET_ENV: ${SECRET_ENV}"
```

# Options

Field | Required | Example
------------ | ------------  | -------------
**repoUrl** | YES | Ex: `git@gist.github.com:f6281d95065d3b942f13a8436768669f.git`
**path** | NO | Ex: `.tmpsecrets` (default) | 
**ageSecretKey** | YES | Ex: `AGE-SECRET-KEY123------------------------------------------------------456`
**envFile** | YES | Ex: `.tmpsecrets/.env1|.tmpsecrets/.env2`
**excludeEnv** | NO | Ex: `EXCLUDE_ENV|RANDOM_ENV_TEST`
**maskEnv** | NO | Ex: `SOME_ENV_NEED|OTHER_ENV|.*RANDOM_ENV|PREFIX_.*`, [default](https://github.com/datphan/export-env-action?tab=readme-ov-file#-mask-default-mysqlkeytokenpasswordsecretsididentityawsgcpcryptoencryptionadddressipdatabasecert)