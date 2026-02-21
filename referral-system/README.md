# Satio Referral System

A custom referral system for the Satio waitlist using Firebase.

## Setup Instructions

### 1. Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Create a project" → Name it "satio-waitlist"
3. Disable Google Analytics (not needed)
4. Click "Create project"

### 2. Set Up Firestore Database

1. In Firebase Console, go to **Build** → **Firestore Database**
2. Click "Create database"
3. Choose "Start in test mode" (we'll add security rules later)
4. Select your region (e.g., `us-central1`)

### 3. Get Firebase Config

1. Go to **Project Settings** (gear icon)
2. Scroll to "Your apps" → Click web icon (`</>`)
3. Register app name: "satio-waitlist-web"
4. Copy the `firebaseConfig` object
5. Paste it in `index-v2 copy.html` where indicated

### 4. Security Rules (Important!)

In Firestore → Rules, replace with:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow anyone to create a new waitlist entry
    match /waitlist/{email} {
      allow create: if request.resource.data.keys().hasAll(['email', 'referralCode', 'joinedAt'])
                    && request.resource.data.email is string
                    && request.resource.data.referralCode is string;
      // Allow reading own entry by referral code lookup
      allow read: if true;
      // Only allow updating referral count (not other fields)
      allow update: if request.resource.data.diff(resource.data).affectedKeys().hasOnly(['referralCount']);
    }

    // Allow lookup by referral code
    match /referralCodes/{code} {
      allow read: if true;
      allow create: if true;
    }
  }
}
```

### 5. Deploy

Just host the HTML file anywhere (GitHub Pages, Netlify, Vercel, etc.)

## How It Works

1. User visits `satio.app` or `satio.app?ref=ABC123`
2. If `?ref=` exists, we store it in localStorage
3. User enters email and joins waitlist
4. System generates unique referral code for new user
5. If referred, increment referrer's count
6. User sees their referral link and current tier

## Data Structure

```
/waitlist/{email_hash}
  - email: "user@example.com"
  - referralCode: "SAT-X7K9M2"
  - referredBy: "SAT-ABC123" (optional)
  - referralCount: 0
  - tier: "seedling"
  - joinedAt: timestamp

/referralCodes/{code}
  - email: "user@example.com"
```

## Tiers

- **Seedling** (0 referrals): Basic founding member
- **Grower** (3+ referrals): Priority access + 2 months free Pro
- **Cultivator** (10+ referrals): Lifetime Pro + name in credits
