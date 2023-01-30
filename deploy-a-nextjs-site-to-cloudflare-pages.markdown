# Deploy a next.js site to Cloudflare pages

This guide will walk you through deploying a Next.js site to Cloudflare Pages.

1. Setup a Github repo, and add the next.js landing site. Cloudflare will pull changes from this repo and build the site.
2. Go to Cloudflare dashboard, and choose Pages. Click Create a project and select **Connect to Git**
3. Click **Connect Github**
4. Follow the prompts to connect to the repository from step 1.
5. Back in the Cloudflare Pages UI click to select the chosen repo, then **Begin setup**
6. Configure the Pages site:
  * Framework preset: `next.js (Static HTML export)`
  * Build command: `next build && next export`
  * Build output directory: `out`

  Using `next export` builds static HTML files and won't start the nodejs server.

7. Configure the environment variables
  * `NODE_VERSION` = `17.9.1`

  Pages won't build on nodejs that is too old or too new.

7. Hit **Save and deploy**