# Deployment Guide

## Vercel Deployment

This repository is configured to deploy on Vercel with flexible project root settings.

### Configuration Options

You can deploy this application with Vercel using either configuration:

#### Option 1: Root-level Deployment (Recommended)
- **Project Root**: Leave empty or set to `/` (repository root)
- **Build Command**: `npm run vercel-build` (or leave default)
- **Output Directory**: `frontend/dist`
- **Install Command**: `npm install` (or leave default)

The root-level `vercel.json` will be used, which builds from `frontend/package.json`.

#### Option 2: Frontend-only Deployment
- **Project Root**: `frontend`
- **Build Command**: `npm run build`
- **Output Directory**: `dist`
- **Install Command**: `npm install` (or leave default)

The `frontend/vercel.json` will be used, which is specifically configured for this setup.

### Configuration Files

- **Root `/vercel.json`**: Used when Project Root is set to repository root
- **Frontend `/frontend/vercel.json`**: Used when Project Root is set to `frontend`

Both configurations:
- Use the `@vercel/static-build` builder
- Output to the `dist` directory (Vite's default)
- Configure routes for Single Page Application (SPA) behavior
- Redirect all routes to `index.html` for client-side routing

### Framework Detection

Vercel should automatically detect:
- **Framework**: Vite
- **Node Version**: Automatically detected from package.json or uses latest LTS

### Troubleshooting

**404 Errors**: If you encounter 404 errors after deployment:
1. Verify the Project Root setting matches one of the options above
2. Check that the Output Directory is correctly set (`dist` or `frontend/dist`)
3. Ensure the build completes successfully in the deployment logs
4. Verify that `frontend/dist/index.html` exists after build

**Build Failures**: 
1. Check the deployment logs in Vercel dashboard
2. Ensure all dependencies in `frontend/package.json` are correctly specified
3. Verify Node version compatibility

### Local Testing

To test the build locally before deploying:

```bash
cd frontend
npm install
npm run build
npm run preview
```

This will build the app and serve it locally on port 4173 for testing.
