# Deployment Guide for Bolt.diy

## ⚠️ Important: Deployment Platform Notice

**Bolt.diy is optimized for Cloudflare Pages deployment.** While this guide mentions Vercel, the application is built with Remix + Cloudflare Workers runtime, which requires significant modifications to run on Vercel.

### Recommended Deployment: Cloudflare Pages (FREE)

✅ **For the easiest deployment experience, see:**
- **[VERCEL-DEPLOYMENT-ISSUE.md](./VERCEL-DEPLOYMENT-ISSUE.md)** - Detailed explanation and Cloudflare Pages deployment guide
- **Quick Start**: `pnpm run build && wrangler login && pnpm run deploy`

---

## Vercel Deployment (Requires Code Modifications)

This guide covers deploying Bolt.diy to Vercel, but **note that this requires converting the app from Cloudflare Workers to Node.js runtime**.

> **Alternative**: For zero-config deployment, use Cloudflare Pages instead (see above).

## Prerequisites

1. A Vercel account (sign up at https://vercel.com)
2. An OpenRouter API key (get it from https://openrouter.ai/keys)
3. Git repository with your Bolt.diy code

## Quick Deploy to Vercel

### Option 1: Deploy via Vercel CLI

1. **Install Vercel CLI:**
   ```bash
   npm install -g vercel
   ```

2. **Login to Vercel:**
   ```bash
   vercel login
   ```

3. **Deploy the project:**
   ```bash
   vercel
   ```

4. **Set environment variables:**
   ```bash
   # Set your OpenRouter API key (required)
   vercel env add OPEN_ROUTER_API_KEY
   
   # Optional: Add other provider API keys
   vercel env add ANTHROPIC_API_KEY
   vercel env add OPENAI_API_KEY
   vercel env add GOOGLE_GENERATIVE_AI_API_KEY
   vercel env add GROQ_API_KEY
   vercel env add DEEPSEEK_API_KEY
   vercel env add MISTRAL_API_KEY
   ```

5. **Deploy to production:**
   ```bash
   vercel --prod
   ```

### Option 2: Deploy via Vercel Dashboard

1. **Import your Git repository:**
   - Go to https://vercel.com/new
   - Import your Git repository (GitHub, GitLab, or Bitbucket)
   - Select the repository containing Bolt.diy

2. **Configure build settings:**
   - Framework Preset: **Remix**
   - Build Command: `pnpm run build`
   - Output Directory: `build/client`
   - Install Command: `pnpm install`

3. **Add environment variables:**
   Go to your project settings → Environment Variables and add:

   **Required:**
   - `OPEN_ROUTER_API_KEY`: Your OpenRouter API key

   **Optional (for additional providers):**
   - `ANTHROPIC_API_KEY`: For Claude models
   - `OPENAI_API_KEY`: For GPT models
   - `GOOGLE_GENERATIVE_AI_API_KEY`: For Gemini models
   - `GROQ_API_KEY`: For Groq models
   - `DEEPSEEK_API_KEY`: For DeepSeek models
   - `MISTRAL_API_KEY`: For Mistral models
   - `XAI_API_KEY`: For X.AI models
   - `COHERE_API_KEY`: For Cohere models
   - `TOGETHER_API_KEY`: For Together AI models
   - `PERPLEXITY_API_KEY`: For Perplexity models
   - `MOONSHOT_API_KEY`: For Moonshot models
   - `HuggingFace_API_KEY`: For HuggingFace models
   - `HYPERBOLIC_API_KEY`: For Hyperbolic models
   - `GITHUB_API_KEY`: For GitHub Models

4. **Deploy:**
   - Click "Deploy"
   - Wait for the build to complete
   - Your app will be available at `https://your-project.vercel.app`

### Option 3: Deploy via Git Integration

1. **Push to Git:**
   ```bash
   git add .
   git commit -m "Deploy Bolt.diy"
   git push origin main
   ```

2. **Automatic deployment:**
   - If you've connected your Git repository to Vercel, it will automatically deploy on push

## Using OpenRouter Free Models

Once deployed, you can use OpenRouter's free models:

1. Go to Settings (⚙️) → Providers
2. Enable **OpenRouter**
3. Your API key will be automatically used from environment variables
4. In the model selector, click **"Free models only"** toggle to filter free models
5. Select a free model like:
   - Meta Llama models
   - Google Gemini Flash
   - And many more!

## Configuring Model Selection

The application allows you to:
- Select different AI providers from the dashboard
- Switch between models in real-time
- Filter OpenRouter models to show only free options
- Enter custom API keys per provider in the settings UI

## Post-Deployment Configuration

### Adding/Updating Environment Variables

**Via CLI:**
```bash
vercel env add VARIABLE_NAME
vercel env pull  # Download all env vars to .env.local
```

**Via Dashboard:**
1. Go to your project on Vercel
2. Settings → Environment Variables
3. Add or edit variables
4. Redeploy for changes to take effect

### Domain Configuration

1. Go to your project settings on Vercel
2. Navigate to Domains
3. Add your custom domain
4. Follow the DNS configuration instructions

## Troubleshooting

### Build Failures

**Issue:** Build fails with dependency errors
**Solution:**
```bash
# Clear cache and redeploy
vercel --force
```

**Issue:** Missing environment variables
**Solution:**
- Verify all required environment variables are set
- Check that variable names match exactly (case-sensitive)

### Runtime Errors

**Issue:** API key not working
**Solution:**
- Verify your OpenRouter API key is valid
- Check that it's correctly set in Vercel environment variables
- Ensure the variable name is exactly `OPEN_ROUTER_API_KEY`

**Issue:** Models not loading
**Solution:**
- Check browser console for errors
- Verify network requests to OpenRouter API are successful
- Ensure CORS settings are properly configured

## Production Best Practices

1. **Security:**
   - Never commit API keys to Git
   - Use environment variables for all secrets
   - Enable Vercel's security headers (already configured in vercel.json)

2. **Performance:**
   - Monitor your Vercel analytics
   - Use OpenRouter's free models for cost optimization
   - Enable caching where appropriate

3. **Monitoring:**
   - Check Vercel logs for errors
   - Monitor API usage in OpenRouter dashboard
   - Set up alerts for deployment failures

## Additional Resources

- [Vercel Documentation](https://vercel.com/docs)
- [OpenRouter Documentation](https://openrouter.ai/docs)
- [Remix Deployment Guide](https://remix.run/docs/en/main/guides/deployment)
- [Bolt.diy Documentation](https://stackblitz-labs.github.io/bolt.diy/)

## Support

For issues:
- Vercel: https://vercel.com/support
- OpenRouter: https://openrouter.ai/docs
- Bolt.diy: https://thinktank.ottomator.ai
