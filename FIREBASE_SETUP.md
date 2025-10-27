# Firebase Setup Guide for Second Brain

This guide will help you set up Firebase Authentication and Firestore for the Second Brain application.

## Step 1: Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Create a project" or "Add project"
3. Enter project name: `second-brain` (or your preferred name)
4. Enable Google Analytics (optional)
5. Click "Create project"

## Step 2: Enable Authentication

1. In your Firebase project, go to **Authentication** in the left sidebar
2. Click **Get started**
3. Go to the **Sign-in method** tab
4. Click on **Anonymous** in the providers list
5. Toggle **Enable** to ON
6. Click **Save**

## Step 3: Create Firestore Database

1. In your Firebase project, go to **Firestore Database** in the left sidebar
2. Click **Create database**
3. Choose **Start in test mode** (for development)
4. Select a location for your database (choose closest to your users)
5. Click **Done**

## Step 4: Get Firebase Configuration

1. In your Firebase project, go to **Project Settings** (gear icon)
2. Scroll down to **Your apps** section
3. Click **Web app** icon (`</>`)
4. Enter app nickname: `second-brain-web`
5. Click **Register app**
6. Copy the Firebase configuration object

## Step 5: Configure Environment Variables

1. Copy `env.example` to `.env` in the root directory
2. Copy `client/env.local.example` to `client/.env.local`
3. Fill in your Firebase configuration:

```env
# In .env (for server)
GEMINI_API_KEY=your_gemini_api_key_here

# In client/.env.local (for client)
VITE_FIREBASE_API_KEY=your_api_key_here
VITE_FIREBASE_AUTH_DOMAIN=your_project_id.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id_here
VITE_FIREBASE_STORAGE_BUCKET=your_project_id.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id_here
VITE_FIREBASE_APP_ID=your_app_id_here
```

## Step 6: Set Up Firestore Security Rules

1. Go to **Firestore Database** → **Rules** tab
2. Replace the default rules with:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Users can only access their own notes
    match /notes/{noteId} {
      allow read, write: if request.auth != null && resource.data.userId == request.auth.uid;
      allow create: if request.auth != null && request.resource.data.userId == request.auth.uid;
    }
  }
}
```

3. Click **Publish**

## Step 7: Test the Setup

1. Run the application:
   ```bash
   npm run dev
   ```

2. Open http://localhost:3000
3. Click "Get Started" to test anonymous authentication
4. Try creating a note to test Firestore integration

## Troubleshooting

### Common Issues:

1. **"Firebase: Error (auth/configuration-not-found)"**
   - Check that your environment variables are correctly set
   - Ensure the Firebase config object is complete

2. **"Permission denied" errors**
   - Verify Firestore security rules are set up correctly
   - Check that anonymous authentication is enabled

3. **"Missing or insufficient permissions"**
   - Ensure the user is authenticated before trying to access Firestore
   - Check that the `userId` field matches the authenticated user's UID

### Development vs Production:

- **Development**: Use test mode for Firestore (allows all reads/writes)
- **Production**: Use the security rules above and consider additional validation

## Next Steps

Once Firebase is configured:

1. Get a Gemini API key from [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Add it to your `.env` file
3. Start using the AI features!

## Security Notes

- Never commit your `.env` files to version control
- Use environment variables for all sensitive configuration
- Consider using Firebase App Check for additional security in production
- Regularly review and update your Firestore security rules
