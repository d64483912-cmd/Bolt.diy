# 🚀 Cloudflare Pages Deployment - Quick Start

## Why Cloudflare Pages?

Bolt.diy is built with **Remix + Cloudflare Workers**, making Cloudflare Pages the native deployment platform.

**Benefits:**
- ✅ **Zero configuration** - works out of the box
- ✅ **Free tier** with generous limits
- ✅ **Global CDN** (300+ locations)
- ✅ **Fast cold starts** (< 50ms)
- ✅ **No code changes needed**

---

## 🎯 Deployment Methods

### Method 1: Wrangler CLI (Recommended - 5 minutes)

```bash
# 1. Install Wrangler globally
npm install -g wrangler

# 2. Login to Cloudflare
wrangler login

# 3. Build your project
pnpm run build

# 4. Deploy
pnpm run deploy
```

**That's it!** Your app is now live. 🎉

---

### Method 2: GitHub Integration (Automatic Deployments)

1. **Go to Cloudflare Pages**  
   Visit: https://pages.cloudflare.com/

2. **Create a project**  
   Click "Create a project" → "Connect to Git"

3. **Select your repository**  
   Choose: `d64483912-cmd/Bolt.diy`

4. **Configure build settings**:
   - **Framework preset**: Remix
   - **Build command**: `pnpm run build`
   - **Build output directory**: `build/client`
   - **Root directory**: `/`

5. **Add environment variables**:
   Click "Environment variables" and add:
   ```
   OPEN_ROUTER_API_KEY=your_openrouter_api_key
   ANTHROPIC_API_KEY=your_anthropic_api_key
   OPENAI_API_KEY=your_openai_api_key
   GOOGLE_GENERATIVE_AI_API_KEY=your_google_api_key
   GROQ_API_KEY=your_groq_api_key
   ```

6. **Save and Deploy**  
   Click "Save and Deploy"

**Your app will be live at**: `https://your-project.pages.dev`

---

### Method 3: Wrangler with Configuration (Advanced)

If you want custom settings, create or update `wrangler.toml`:

```toml
name = "bolt-diy"
compatibility_date = "2024-01-01"
pages_build_output_dir = "build/client"

[env.production]
# Add environment variables here
```

Then deploy:
```bash
wrangler pages deploy build/client --project-name=bolt-diy
```

---

## 🔧 Post-Deployment Configuration

### Adding Environment Variables

**Via Wrangler CLI:**
```bash
wrangler pages secret put OPEN_ROUTER_API_KEY
# Enter your API key when prompted
```

**Via Dashboard:**
1. Go to your project on Cloudflare Pages
2. Click "Settings" → "Environment Variables"
3. Add your variables
4. Redeploy for changes to take effect

---

### Custom Domain

1. Go to your project on Cloudflare Pages
2. Click "Custom domains"
3. Click "Set up a custom domain"
4. Follow the DNS configuration instructions

---

## 📊 What Happens During Deployment?

```
1. Dependencies Installation
   └─ pnpm install (1609 packages)

2. Build Process
   └─ remix vite:build
   └─ Generates build/client/ and build/server/

3. Deploy to Edge
   └─ Uploads to Cloudflare's global network
   └─ Available in 300+ locations worldwide

4. Live! 🚀
   └─ Your app is accessible at your-project.pages.dev
```

---

## 🛠️ Troubleshooting

### Build fails with "command not found"

**Solution**: Ensure pnpm is available:
```bash
npm install -g pnpm
```

### Environment variables not working

**Solution**: 
1. Check variable names (case-sensitive)
2. Redeploy after adding variables
3. Verify in Cloudflare dashboard under Settings → Environment Variables

### Deployment succeeds but app shows errors

**Solution**:
1. Check Cloudflare Pages logs
2. Verify all required environment variables are set
3. Ensure API keys are valid
4. Check Functions logs for runtime errors

---

## 📈 Monitoring Your Deployment

### View Logs

**Cloudflare Dashboard:**
1. Go to your project
2. Click on a deployment
3. View "Build logs" and "Functions logs"

**Via Wrangler:**
```bash
wrangler pages deployment tail
```

### Analytics

Cloudflare Pages provides:
- Requests per second
- Bandwidth usage
- Error rates
- Geographic distribution

Access via: Project → Analytics

---

## 🔄 Continuous Deployment

Once connected to GitHub:
- **Every push** to main branch triggers automatic deployment
- **Pull requests** get preview deployments
- **Rollback** to any previous deployment instantly

---

## 💰 Pricing

**Free Tier Includes:**
- 500 builds/month
- Unlimited requests
- Unlimited bandwidth
- Unlimited sites

**No credit card required!**

---

## ✨ Next Steps

After deployment:

1. **Configure your API keys**  
   Add environment variables in Cloudflare dashboard

2. **Test the application**  
   Visit your deployment URL and verify functionality

3. **Select OpenRouter models**  
   - Click Settings ⚙️
   - Enable OpenRouter provider
   - Toggle "Free models only"
   - Start chatting!

4. **Set up custom domain** (optional)  
   Follow the custom domain guide above

---

## 📚 Additional Resources

- [Cloudflare Pages Docs](https://developers.cloudflare.com/pages/)
- [Remix on Cloudflare](https://remix.run/docs/en/main/guides/deployment#cloudflare-pages)
- [Wrangler CLI Docs](https://developers.cloudflare.com/workers/wrangler/)
- [Environment Variables Guide](https://developers.cloudflare.com/pages/configuration/build-configuration/)

---

## 🆘 Need Help?

- **Cloudflare Discord**: https://discord.gg/cloudflaredev
- **Bolt.diy Issues**: https://github.com/d64483912-cmd/Bolt.diy/issues
- **Documentation**: https://stackblitz-labs.github.io/bolt.diy/

---

**Happy deploying! 🎉**
