# RhodeCode VCS Server

This image is the same as ckulka/rhodecode-rccontrol, with the exception that a
VCS Server is installed and ready-to-use.

```bash
docker run -it -p 9900:9900 ckulka/rhodecode-vcsserver
```

The following `docker-compose.yaml` file spins up a complete RhodeCode stack

```yaml
version: "3"

services:
  vcsserver:
    image: ckulka/rhodecode-vcsserver

  db:
    image: postgres:alpine
    environment:
      POSTGRES_PASSWORD: cookiemonster

  rhodecode:
    image: ckulka/rhodecode-ce
    environment:
      RC_USER: admin
      RC_PASSWORD: ilovecookies
      RC_EMAIL: adalovelace@example.com
      RC_DB: postgresql://postgres:cookiemonster@db
      RC_CONFIG: |
        [app:main]
        vcs.server = vcsserver:9900
    ports:
      - "5000:5000"
    links:
      - db
      - vcsserver
```

For more details, see `ckulka/rhodecode-rccontrol`.