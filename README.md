# issuer

<p align="center">
  <img style="float: right;" src=".github/hello.png" alt="hello gopher"/>
</p>

In trying to [make a TODO system around my GitHub repos](https://shindakun.dev/posts/working-on-a-new-flow/) I wanted each new ticket to bubble up into a master repo and kanban board. `issuer` is the result of that. It is designed to be hosted on Google Cloud functions.

Simply add the triggering URL to your source repositories and make sure that it is set to send new issues.

Because I like to live life on the edge we're supplying all configuration options as environment variables.

- SECRET - The secret entered in webhook settings, used to verify the request is from GitHub
- GITHUBTOKEN - A GitHub [personal access token](https://github.com/settings/tokens)
- REPOOWNER - The name of the owner of the repo (your GitHub username)
- ISSUEREPO - The name of the repo you want to bubble issues up to
- PROJECTCOLUMN - The ID of the TODO column in your repos project

issuer was created as a learning project.

## Deploying

Deploying is simply a matter of running `gcloud` and filling in the correct options.

```bash
gcloud functions deploy issuer \
  --source https://github.com/shindakun/issuer \
  --entry-point HandleWebhook \
  --runtime go111 \
  --trigger-http \
  --memory=128MB \
  --set-env-vars SECRET=secret,GITHUBTOKEN=personalaccesstoken,REPOOWNER=yourname,ISSUEREPO=to,PROJECTCOLUMN=1234
```