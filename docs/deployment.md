# Deployment

## Canonical public URL

https://wakouzan-kichijoji.com/hinan-navi/

## Hosting

Production web deployment is hosted on Hostinger.

GitHub is not the production hosting source of truth for the deployed application.

## Release method

The historical-disaster release was deployed as a controlled delta:

- 2 modified files
- 17 added files
- 0 removed files

Total delta: **19 files**

The final remote smoke test fetched all 19 files from production and compared SHA-256 values against the approved local release.

Result:

`19 / 19 MATCH`

## Separation of concerns

- GitHub → public project documentation and technical history
- Hostinger → production web application
- archival storage → large release artifacts, generated datasets, audit evidence, rollback packages

## Rollback

Production promotion created a rollback package before modifying canonical production.

Rollback artifacts are maintained outside this public repository.
