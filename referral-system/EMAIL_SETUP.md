# Free Email Automation with Firebase

## Recommended: Firebase Extension + Resend (Free Tier)

### Why This Stack?
- **Firebase Trigger Mail Extension**: Automatically sends emails when documents are added to Firestore
- **Resend**: 3,000 free emails/month, modern API, great deliverability
- **Total cost**: $0 (within free tiers)

---

## Setup Instructions

### Step 1: Create Resend Account

1. Go to [resend.com](https://resend.com) and sign up (free)
2. Verify your domain OR use their test domain for development
3. Go to **API Keys** → Create an API key
4. Save the API key (starts with `re_`)

### Step 2: Install Firebase Extension

1. Go to [Firebase Console](https://console.firebase.google.com) → Your project
2. Click **Extensions** in the left sidebar
3. Search for **"Trigger Email"** (by Firebase)
4. Click **Install**
5. Configure:
   - **SMTP connection URI**: Use Resend's SMTP:
     ```
     smtps://resend:YOUR_API_KEY@smtp.resend.com:465
     ```
   - **Email documents collection**: `mail`
   - **Default FROM address**: `Satio <hello@satio.app>` (must be verified domain)

### Step 3: Update Your Waitlist Code

Add this function to send the welcome email when someone signs up:

```javascript
// Add this after successfully creating the waitlist entry
async function sendWelcomeEmail(email, referralCode, referralLink) {
    const mailDoc = {
        to: email,
        message: {
            subject: "You're on the Satio waitlist! 🌻",
            html: generateWelcomeEmailHTML(referralLink)
        }
    };

    // Add to 'mail' collection - Firebase Extension picks it up automatically
    await db.collection('mail').add(mailDoc);
}

function generateWelcomeEmailHTML(referralLink) {
    return `
<!DOCTYPE html>
<html>
<head>
    <style>
        body { font-family: 'Inter', -apple-system, sans-serif; background: #FAFAF8; margin: 0; padding: 40px 20px; }
        .card { max-width: 520px; margin: 0 auto; background: white; border-radius: 16px; overflow: hidden; }
        .header { background: #E8836B; padding: 32px; text-align: center; color: white; }
        .header h1 { margin: 0; font-size: 24px; }
        .body { padding: 40px; }
        .body p { color: #2D2D2D; font-size: 16px; line-height: 1.6; margin: 0 0 24px; }
        .referral-box { background: #F5F5F3; border-radius: 12px; padding: 24px; margin-bottom: 24px; }
        .referral-label { color: #5B5FC7; font-size: 14px; font-weight: 600; text-transform: uppercase; margin: 0 0 12px; }
        .referral-link { background: white; border: 1px solid #E8E8E6; border-radius: 8px; padding: 12px 16px; word-break: break-all; margin-bottom: 16px; }
        .referral-link a { color: #2D2D2D; text-decoration: none; }
        .btn { display: inline-block; background: #5B5FC7; color: white; padding: 12px 24px; border-radius: 8px; text-decoration: none; font-weight: 600; }
        .tiers { margin-bottom: 24px; }
        .tier { display: flex; align-items: flex-start; padding: 12px 0; border-bottom: 1px solid #E8E8E6; }
        .tier:last-child { border-bottom: none; }
        .tier-icon { width: 32px; height: 32px; background: #F5F5F3; border-radius: 50%; text-align: center; line-height: 32px; margin-right: 12px; }
        .tier-name { font-weight: 600; color: #2D2D2D; font-size: 14px; }
        .tier-req { color: #E8836B; font-size: 14px; }
        .tier-reward { color: #6B6B6B; font-size: 13px; }
        .footer { background: #F5F5F3; padding: 24px; text-align: center; }
        .footer p { color: #9B9B9B; font-size: 12px; margin: 0; }
        .footer a { color: #9B9B9B; }
    </style>
</head>
<body>
    <div class="card">
        <div class="header">
            <h1>You're on the list!</h1>
        </div>
        <div class="body">
            <p>Hey there,</p>
            <p>Welcome to the Satio founding members waitlist. We're building an AI nutrition coach that actually understands <em>why</em> you eat the way you do.</p>
            <p>You'll be among the first to try it when we launch.</p>

            <div class="referral-box">
                <p class="referral-label">Your Referral Link</p>
                <p style="color: #6B6B6B; font-size: 14px; margin: 0 0 16px;">Share to move up the waitlist and unlock rewards:</p>
                <div class="referral-link">
                    <a href="${referralLink}">${referralLink}</a>
                </div>
                <a href="${referralLink}" class="btn">Share Your Link</a>
            </div>

            <p style="font-weight: 600; margin-bottom: 16px;">Unlock rewards with referrals:</p>
            <div class="tiers">
                <div class="tier">
                    <div class="tier-icon">🌱</div>
                    <div>
                        <span class="tier-name">Seedling</span> <span style="color: #9B9B9B;">(You are here)</span><br>
                        <span class="tier-reward">Founding member status</span>
                    </div>
                </div>
                <div class="tier">
                    <div class="tier-icon">🌿</div>
                    <div>
                        <span class="tier-name">Grower</span> <span class="tier-req">(3 referrals)</span><br>
                        <span class="tier-reward">Priority access + 2 months free Pro</span>
                    </div>
                </div>
                <div class="tier">
                    <div class="tier-icon">🌳</div>
                    <div>
                        <span class="tier-name">Cultivator</span> <span class="tier-req">(10 referrals)</span><br>
                        <span class="tier-reward">Lifetime Pro + name in app credits</span>
                    </div>
                </div>
            </div>

            <p style="color: #6B6B6B; font-size: 14px;">We'll email you when it's your turn. Follow us on <a href="https://twitter.com/satioapp" style="color: #5B5FC7;">Twitter</a> for updates.</p>
        </div>
        <div class="footer">
            <p>Satio — AI nutrition coaching that understands you</p>
            <p style="margin-top: 8px;"><a href="https://satio.app/privacy.html">Privacy</a></p>
        </div>
    </div>
</body>
</html>
    `;
}
```

### Step 4: Update handleWaitlistSubmit

In your `index-v2 copy.html`, modify the submit handler to send the email:

```javascript
// After this line in handleWaitlistSubmit:
// await setDoc(doc(db, 'waitlist', hashedEmail), userData);

// Add:
await sendWelcomeEmail(email, referralCode, referralLink);
```

---

## Alternative: Resend Direct API (No Extension)

If you prefer not to use the Firebase Extension, you can call Resend's API directly via a Firebase Cloud Function:

### 1. Create Cloud Function

```javascript
// functions/index.js
const functions = require('firebase-functions');
const { Resend } = require('resend');

const resend = new Resend(process.env.RESEND_API_KEY);

exports.sendWelcomeEmail = functions.firestore
    .document('waitlist/{docId}')
    .onCreate(async (snap, context) => {
        const data = snap.data();

        await resend.emails.send({
            from: 'Satio <hello@satio.app>',
            to: data.email,
            subject: "You're on the Satio waitlist! 🌻",
            html: generateEmailHTML(data.referralCode)
        });
    });
```

### 2. Deploy
```bash
cd functions
npm install resend
firebase functions:config:set resend.api_key="re_YOUR_API_KEY"
firebase deploy --only functions
```

---

## Free Tier Limits

| Service | Free Tier |
|---------|-----------|
| **Resend** | 3,000 emails/month |
| **Firebase Firestore** | 50K reads, 20K writes/day |
| **Firebase Functions** | 2M invocations/month |

For a waitlist, this is more than enough!

---

## Quick Start Checklist

- [ ] Create Resend account at resend.com
- [ ] Get API key from Resend dashboard
- [ ] Install "Trigger Email" extension in Firebase
- [ ] Configure SMTP with Resend credentials
- [ ] Add email sending code to your waitlist
- [ ] Test with your own email
- [ ] Verify domain in Resend for production

---

## Domain Verification (For Production)

To send from `hello@satio.app` instead of Resend's test domain:

1. In Resend dashboard → **Domains** → **Add Domain**
2. Enter `satio.app`
3. Add the DNS records Resend provides to your domain registrar
4. Wait for verification (usually 5-15 minutes)

Without domain verification, emails will come from a Resend test address.
