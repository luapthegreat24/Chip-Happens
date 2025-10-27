# 🍪 Cookie Haven - Mobile Stripe Setup Guide

## ✅ What I've Set Up For You

1. **Environment Configuration**

   - `.env` - Local development configuration
   - `.env.production` - Production/mobile configuration

2. **Stripe Server**

   - `server/index.js` - Production-ready Stripe server
   - `server/package.json` - Server dependencies
   - `server/vercel.json` - Vercel deployment config
   - `server/.env` - Server environment variables

3. **App Updates**

   - Updated `Checkout.tsx` to use environment variables
   - Server URL is now dynamic (works for both local and deployed)

4. **Deployment Scripts**
   - `deploy-stripe.bat` - Automated deployment script (Windows)
   - `server/README.md` - Detailed deployment instructions

---

## 🚀 Quick Start - Deploy Your Stripe Server

### Option 1: Automated (Easy) ⭐

1. **Double-click** `deploy-stripe.bat` in your project folder
2. Follow the Vercel prompts
3. Copy the deployed URL
4. Update `.env.production` with your URL
5. Rebuild your app

### Option 2: Manual Deployment

#### Step 1: Install Vercel CLI

```powershell
npm install -g vercel
```

#### Step 2: Deploy Server

```powershell
cd server
npm install
vercel
```

#### Step 3: Add Stripe Secret Key

```powershell
vercel env add STRIPE_SECRET_KEY
```

Paste: `sk_test_51SDRD2KLsgahIll1V81w8mkMxJxuE2ar0GWiSqtbmpBvSHjJvKbWzS2InQV1qiiPwpZ7BH0WAfdS6LbsW8RQ7B5w00L3kJQOSe`

#### Step 4: Production Deploy

```powershell
vercel --prod
```

#### Step 5: Update App Configuration

Open `.env.production` and update:

```
VITE_STRIPE_SERVER_URL=https://your-vercel-url.vercel.app
```

#### Step 6: Rebuild App

```powershell
cd ..
npm run build
npx cap sync android
```

#### Step 7: Build APK in Android Studio

- Open Android Studio
- Build → Generate Signed Bundle / APK

---

## 🧪 Testing Your Setup

### Test Deployed Server

Open your Vercel URL in a browser:

```
https://your-server-url.vercel.app/
```

You should see:

```json
{
  "status": "ok",
  "message": "Cookie Haven Stripe Server is running!",
  "timestamp": "2025-10-27T..."
}
```

### Test in Mobile App

1. Build and install APK on your phone
2. Add items to cart
3. Go to checkout
4. Select "Credit/Debit Card" payment
5. Click "Place Order"
6. You should be redirected to Stripe checkout

---

## 🔧 Troubleshooting

### Issue: "Payment Error: Failed to fetch"

- ✅ Make sure server is deployed
- ✅ Check `.env.production` has correct URL
- ✅ Rebuild app after updating environment variables

### Issue: "Stripe server is running on port 4242"

- This means the app is trying to connect to localhost
- ✅ Update `.env.production` with your Vercel URL
- ✅ Rebuild: `npm run build && npx cap sync android`

### Issue: Vercel deployment fails

- ✅ Make sure you're in the `server` folder
- ✅ Run `npm install` first
- ✅ Check you're logged into Vercel: `vercel login`

---

## 💳 Stripe Test Cards

Use these cards to test payments:

| Card Number         | Result                  |
| ------------------- | ----------------------- |
| 4242 4242 4242 4242 | Success                 |
| 4000 0000 0000 9995 | Declined                |
| 4000 0027 6000 3184 | Requires authentication |

- Use any future expiry date (e.g., 12/34)
- Use any 3-digit CVC (e.g., 123)
- Use any billing ZIP code

---

## 📱 For Production (Real Payments)

1. Go to https://dashboard.stripe.com/apikeys
2. Switch from "Test mode" to "Live mode"
3. Copy your **Live Secret Key** (starts with `sk_live_`)
4. Update environment variable in Vercel:
   ```bash
   vercel env add STRIPE_SECRET_KEY production
   ```
   Paste your live key
5. Redeploy: `vercel --prod`

---

## 🎯 Current Status

✅ Local web app - Stripe works (localhost:4242)
✅ Environment variables configured
✅ Server code ready for deployment
⏳ **YOU NEED TO**: Deploy server to Vercel
⏳ **YOU NEED TO**: Update .env.production with deployed URL
⏳ **YOU NEED TO**: Rebuild app for mobile

---

## 🆘 Need Help?

Check the detailed guide in `server/README.md`
