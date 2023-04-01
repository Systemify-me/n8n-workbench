# n8n-workbench-syncer
This project helps to sync local n8n workflows with remote host.

### Installation - Local

1. Install node.js ( https://nodejs.org/en/download/ ), n8n ( `npm run n8n-install` ) and git
2. Clone or "Save as zip" this repo. The most important is ./workbench folder - you might want to rename it as well. You can safely remove all other files in the root folder
3. Create your private repo for the project, e.g. on bitbucket 
4. Create 2 access tokens at https://bitbucket.org/%username%/%reponame%/admin/access-tokens: with read rights (for remote pull) and with read+write rights (for local push) 
5. Run `npm i` - that will install all necessary modules
6. Add lines to the ./workbench/.env: 
```
REPO_PULL_URL="https://x-token-auth:xxx" - bitbucket url for pull
REPO_PUSH_URL="https://x-token-auth:xxx" - bitbucket url for push
REPO_PUSH_AUTHOR="xxx@bots.bitbucket.org"- bitbucket email for push
N8N_ENCRYPTION_KEY="n8n_long_secret_key" - encryption key
```
7. Optonally, you can add more settings to the .env in order to configure n8n instance:
```
N8N_TEMPLATES_ENABLED=false
N8N_USER_MANAGEMENT_DISABLED=true
N8N_METRICS=true
EXECUTIONS_DATA_PRUNE=true
EXECUTIONS_DATA_MAX_AGE=168
```

### Installation - Host
1. Install node.js ( https://nodejs.org/en/download/ ), n8n ( `npm run n8n-install` ) and git
2. Manually copy *./workbench* folder to the host (most important is to keep `.env` outside of repo)
3. Run `npm i` - that will install all necessary modules

### Workflow - Local
0. Ensure you're in *./workbench* folder (run `cd ./workbench`) 
1. Run `npm run ex` - that will **clean** folder *project*, export workflow and creds, clones your private repo, commit all changes and push them to the bitbucket

### Workflow - Host
1. Run `npm run imr` - that will **clean** folder *project*, pull your private repo, import downloaded workflows and creds to the n8n instance, and run n8n with envs variables
