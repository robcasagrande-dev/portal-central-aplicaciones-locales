## Development

When starting the dev server, use background mode:

```
astro dev --background
```

Manage the background server with `astro dev stop`, `astro dev status`, and `astro dev logs`.

## Documentation

Full documentation: https://docs.astro.build

Consult these guides before working on related tasks:

- [Adding pages, dynamic routes, or middleware](https://docs.astro.build/en/guides/routing/)
- [Working with Astro components](https://docs.astro.build/en/basics/astro-components/)
- [Using React, Vue, Svelte, or other framework components](https://docs.astro.build/en/guides/framework-components/)
- [Adding or managing content](https://docs.astro.build/en/guides/content-collections/)
- [Adding styles or using Tailwind](https://docs.astro.build/en/guides/styling/)
- [Supporting multiple languages](https://docs.astro.build/en/guides/internationalization/)

## 🚢 Deployment Procedure

This project (the Astro portal) is served by the `BackendAPI` Docker container running on the remote EliteDesk server (`100.98.28.34` / `192.168.10.168`). To deploy changes:

1. Build the Astro project locally:
   ```bash
   npm run build
   ```
2. Copy the static build output (`dist/`) into the `BackendAPI`'s `public/` folder, which is where the backend serves static files from:
   ```bash
   rsync -av dist/ /home/robcasagrande/Projects/SmartCheckInSuite/BackendAPI/public/
   ```
3. Run the deployment script from the `BackendAPI` directory to sync and rebuild the Docker containers on the remote server:
   ```bash
   cd /home/robcasagrande/Projects/SmartCheckInSuite/BackendAPI && ./deploy_elitedesk_backend.sh
   ```
This will push the new files via SSH, rebuild the `backend-api` container, and restart it so the changes take effect immediately on `http://192.168.10.168/`.
