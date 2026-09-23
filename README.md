# Astro Starter Kit: Minimal

```sh
npm create astro@latest -- --template minimal
```

> 🧑‍🚀 **Seasoned astronaut?** Delete this file. Have fun!

## 🚀 Project Structure

Inside of your Astro project, you'll see the following folders and files:

```text
/
├── public/
├── src/
│   └── pages/
│       └── index.astro
└── package.json
```

Astro looks for `.astro` or `.md` files in the `src/pages/` directory. Each page is exposed as a route based on its file name.

There's nothing special about `src/components/`, but that's where we like to put any Astro/React/Vue/Svelte/Preact components.

Any static assets, like images, can be placed in the `public/` directory.

## 🧞 Commands

All commands are run from the root of the project, from a terminal:

| Command                   | Action                                           |
| :------------------------ | :----------------------------------------------- |
| `npm install`             | Installs dependencies                            |
| `npm run dev`             | Starts local dev server at `localhost:4321`      |
| `npm run build`           | Build your production site to `./dist/`          |
| `npm run preview`         | Preview your build locally, before deploying     |
| `npm run astro ...`       | Run CLI commands like `astro add`, `astro check` |
| `npm run astro -- --help` | Get help using the Astro CLI                     |

## 👀 Want to learn more?

Feel free to check [our documentation](https://docs.astro.build) or jump into our [Discord server](https://astro.build/chat).

## 🚢 Deployment Procedure

This project is currently deployed to the remote EliteDesk server (`192.168.10.168`) by being bundled directly inside the `BackendAPI`'s `public` folder. 

To deploy changes to the live portal:

1. **Build the Astro project locally**:
   ```bash
   npm run build
   ```
2. **Copy the build output (`dist/`) to the BackendAPI public directory**:
   ```bash
   rsync -av dist/ /home/robcasagrande/Projects/SmartCheckInSuite/BackendAPI/public/
   ```
3. **Execute the EliteDesk backend deployment script**:
   ```bash
   cd /home/robcasagrande/Projects/SmartCheckInSuite/BackendAPI
   ./deploy_elitedesk_backend.sh
   ```

*Note: This script synchronizes the BackendAPI folder via SSH to `100.98.28.34` (the Tailscale IP for the EliteDesk server), then builds and restarts the `smart-checkin-api` docker container which serves these static files.*

## 🗺️ URL Mappings (Caddy Reverse Proxy)

The central portal uses clean URLs that are reverse-proxied by a Caddy container running on the EliteDesk server. The configuration for these routes is located in `BackendAPI/Caddyfile.elitedesk`. 

**Current Active Mappings (URL → Destination):**
- `/kaliclock/*` → Proxies to host port `5050` (where KaliClock natively runs).
- `/voltage/*` → Rewrites to `/VoltageLogger` and serves statically from `BackendAPI/public/VoltageLogger`.
- `/ups/*` → Rewrites to `/UPS-Dashboard` and serves statically from `BackendAPI/public/UPS-Dashboard`.
- `/omada-backups/*` → Rewrites to `/omada-backups` and serves statically from `BackendAPI/public/omada-backups`.
- `/wifi-portal/*` → Proxies to host port `8000`.
- `/video-safebox/*` → Rewrites to `/Video_Safebox` and serves statically from `BackendAPI/public/Video_Safebox`.

*Important: If you modify the `Caddyfile.elitedesk` routes, running the deployment script (`deploy_elitedesk_backend.sh`) will copy the file to the server, but you **must** manually restart the `caddy-proxy` container on the remote server (`docker restart caddy-proxy`) for the new proxy rules to take effect!*
