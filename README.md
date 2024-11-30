# Usage

First, you need a gist or repo to store your encrypted env

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
          repoUrl: https://gist.github.com/f6281d95065d3b942f13a8436768669f.git
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
          echo "SID_ENV: ${SID_ENV}"
          echo "SECRET_ENV: ${SECRET_ENV}"
          echo "IDENTITY_ENV: ${IDENTITY_ENV}"
          echo "AWS_ENV: ${AWS_ENV}"
          echo "GCP_ENV: ${GCP_ENV}"
          echo "CRYPTO_ENV: ${CRYPTO_ENV}"
          echo "ENCRYPTION_ENV: ${ENCRYPTION_ENV}"
          echo "IP_ENV: ${IP_ENV}"
          echo "DATABASE_ENV: ${DATABASE_ENV}"
          echo "CERT_ENV: ${CERT_ENV}"
```

The result will be:

```bash
PUBLIC_ENV: PUBLIC_ENV-display-on-deploy
RANDOM_ENV: RANDOM_ENV-display-on-deploy
MYSQL_ENV: ***
KEY_ENV: ***
TOKEN_ENV: ***
PASSWORD_ENV: ***
SID_ENV: ***
SECRET_ENV: ***
IDENTITY_ENV: ***
AWS_ENV: ***
GCP_ENV: ***
CRYPTO_ENV: ***
ENCRYPTION_ENV: ***
IP_ENV: ***
DATABASE_ENV: ***
CERT_ENV: ***
```

# Options

| Field         | Required        | Example |
| :------------ |:---------------:| :-------|
| **repoUrl** | YES | `https://gist.github.com/f6281d95065d3b942f13a8436768669f.git` |
| **path** | NO | `.tmpsecrets` (default)
| **ageSecretKey** | YES | `AGE-SECRET-KEY123------------------------------------------------------456` |
| **envFile** | YES | `.tmpsecrets/.env1\|.tmpsecrets/.env2` |
| **excludeEnv** | NO | `EXCLUDE_ENV\|RANDOM_ENV_TEST` |
| **maskEnv** | NO | `SOME_ENV_NEED\|OTHER_ENV\|.*RANDOM_ENV\|PREFIX_.*`, [see default](https://github.com/datphan/export-env-action?tab=readme-ov-file#-mask-default-mysqlkeytokenpasswordsecretsididentityawsgcpcryptoencryptionadddressipdatabasecert) |
