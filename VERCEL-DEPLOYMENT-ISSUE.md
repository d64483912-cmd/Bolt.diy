# ⚠️ Vercel Deployment Limitation

## Issue Summary

Bolt.diy is built using **Remix with Cloudflare Workers runtime**, which is **not directly compatible** with Vercel's serverless functions (which use Node.js/Edge runtime).

### Error Encountered
```
500: INTERNAL_SERVER_ERROR  
Code: FUNCTION_INVOCATION_FAILED
```

### Root Cause

1. **Cloudflare-Specific Dependencies**: The app uses `@remix-run/cloudflare` and `@remix-run/cloudflare-pages`
2. **Runtime Incompatibility**: Cloudflare Workers APIs are different from Node.js/Vercel Edge runtime
3. **Build Configuration**: The entire app is configured for Cloudflare Pages deployment pipeline

---

## ✅ Recommended Solution: Deploy to Cloudflare Pages (FREE)

Bolt.diy is **optimized** for Cloudflare Pages deployment. Cloudflare offers:
- **Free tier** with generous limits
- **Global CDN** with excellent performance
- **Native Remix support** with zero configuration
- **Built-in environment variables** management

### Quick Deployment to Cloudflare Pages

#### Option 1: Using Wrangler CLI (Fastest)

```bash
# 1. Install Wrangler
npm install -g wrangler

# 2. Login to Cloudflare
wrangler login

# 3. Build the project
pnpm run build

# 4. Deploy
pnpm run deploy
```

#### Option 2: Using Cloudflare Dashboard (No CLI)

1. **Go to** [Cloudflare Pages](https://pages.cloudflare.com/)
2. **Click** "Create a project"
3. **Connect** your GitHub repository: `https://github.com/d64483912-cmd/Bolt.diy.git`
4. **Configure build settings**:
   - Build command: `pnpm run build`
   - Build output directory: `build/client`
   - Root directory: `/`
   - Framework preset: `Remix`

5. **Add environment variables** in Cloudflare dashboard:
   ```
   OPEN_ROUTER_API_KEY=your_key_here
   ANTHROPIC_API_KEY=your_key_here
   OPENAI_API_KEY=your_key_here
   # ... add other API keys as needed
   ```

6. **Click** "Save and Deploy"

Your app will be live at: `https://your-project-name.pages.dev`

---

## 🔧 Alternative: Convert to Vercel (Advanced)

If you **must** deploy to Vercel, here are the required changes:

### Major Modifications Needed

1. **Replace Cloudflare adapters** with Node.js adapters:
   ```bash
   # Remove Cloudflare packages
   pnpm remove @remix-run/cloudflare @remix-run/cloudflare-pages
   
   # Add Node.js packages  
   pnpm add @remix-run/node @remix-run/vercel
   ```

2. **Update all route files** (~30+ files) to use `@remix-run/node` instead of `@remix-run/cloudflare`

3. **Replace Cloudflare-specific APIs**:
   - Context: `AppLoadContext` (Cloudflare) → Node.js request/response
   - Environment variables: `context.cloudflare.env` → `process.env`
   - KV storage: Need to migrate to alternative (Redis, PostgreSQL, etc.)

4. **Update vite.config.ts**:
   - Remove `remixCloudflareDevProxy`
   - Configure for Node.js target

5. **Create Vercel serverless function entry**:
   ```javascript
   // api/index.js
   import { createRequestHandler } from '@remix-run/vercel';
   import * as build from '../build/server/index.js';
   
   export default createRequestHandler({ build });
   ```

6. **Update vercel.json**:
   ```json
   {
     "rewrites": [{ "source": "/(.*)", "destination": "/api/index" }]
   }
   ```

### Estimated Effort
- **Time**: 4-8 hours of development
- **Risk**: High (breaking changes across the entire codebase)
- **Testing**: Extensive testing required for all features

---

## 📊 Platform Comparison

| Feature | Cloudflare Pages | Vercel |
|---------|------------------|--------|
| **Free Tier** | ✅ 500 builds/month | ✅ 100 GB bandwidth |
| **Remix Support** | ✅ Native | ⚠️ Requires adapter |
| **Global CDN** | ✅ 300+ locations | ✅ Edge Network |
| **Build Time** | ~2-3 min | ~2-3 min |
| **Cold Start** | < 50ms | < 100ms |
| **Setup Complexity** | ✅ Zero config | ⚠️ Requires migration |
| **This Project** | ✅ **Ready to deploy** | ❌ Needs major refactor |

---

## 🎯 Recommendation

**Deploy to Cloudflare Pages** - it's the path of least resistance and provides excellent performance. The platform is specifically designed for this type of application.

**Deployment time**: ~5 minutes  
**Code changes required**: None

---

## 📚 Additional Resources

- [Cloudflare Pages Documentation](https://developers.cloudflare.com/pages/)
- [Remix on Cloudflare Pages](https://remix.run/docs/en/main/guides/deployment#cloudflare-pages)
- [Wrangler CLI Documentation](https://developers.cloudflare.com/workers/wrangler/)
- [Environment Variables on Cloudflare](https://developers.cloudflare.com/pages/configuration/build-configuration/)

---

## ✨ Quick Start (Cloudflare Pages)

```bash
# Clone the repository (if not already done)
git clone https://github.com/d64483912-cmd/Bolt.diy.git
cd Bolt.diy

# Install dependencies
pnpm install

# Build the project
pnpm run build

# Deploy to Cloudflare Pages
wrangler login
pnpm run deploy
```

**That's it!** Your Bolt.diy instance is now live. 🚀

---

*Last updated: Based on deployment attempt to Vercel on [current date]*
