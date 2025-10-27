# Second Brain - AI-Powered Personal Memory and Learning Hub

An intelligent note-taking application that uses AI to help you capture, organize, and learn from your personal knowledge.

## Features

### Core Features
- **Real-time Note Management**: Create, edit, and delete notes with instant sync across devices
- **Firebase Authentication**: Secure anonymous authentication
- **Responsive Design**: Works on desktop and mobile browsers

### AI-Powered Features
- **Image to Note**: Upload images and automatically extract text and create structured notes
- **Smart Search**: Ask questions in natural language and get AI-powered answers from your notes
- **Related Notes**: Discover connections between your notes using AI
- **Quiz Generation**: Generate interactive quizzes from your notes for active learning

## Tech Stack

- **Frontend**: React 18 + TypeScript + Vite + Tailwind CSS
- **Backend**: Node.js + Express + TypeScript
- **Database**: Firebase Firestore
- **Authentication**: Firebase Auth
- **AI**: Google Gemini API
- **File Upload**: Multer

## Setup Instructions

### Prerequisites
- Node.js (LTS version)
- Firebase project
- Google Gemini API key

### 1. Clone and Install Dependencies

```bash
cd second-brain
npm run install:all
```

### 2. Firebase Setup

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Create a new project
3. Enable Authentication (Anonymous sign-in)
4. Create a Firestore database
5. Get your Firebase configuration

### 3. Environment Configuration

1. Copy `env.example` to `.env` in the root directory
2. Copy `env.example` to `client/.env.local`
3. Fill in your Firebase configuration and Gemini API key:

```env
# Firebase Configuration
VITE_FIREBASE_API_KEY=your_firebase_api_key
VITE_FIREBASE_AUTH_DOMAIN=your_project_id.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_project_id.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your_messaging_sender_id
VITE_FIREBASE_APP_ID=your_app_id

# Gemini AI API Key
GEMINI_API_KEY=your_gemini_api_key
```

### 4. Get Gemini API Key

1. Go to [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Create a new API key
3. Add it to your `.env` file

### 5. Run the Application

```bash
# Start both client and server
npm run dev

# Or start them separately
npm run dev:client  # Runs on http://localhost:3000
npm run dev:server  # Runs on http://localhost:4000
```

## Usage

1. **Sign In**: The app uses anonymous authentication - just click "Get Started"
2. **Create Notes**: Click "New Note" to create a text note
3. **AI Features**: Click "AI Features" to:
   - Upload images to create notes automatically
   - Search your notes with natural language
   - Find related notes
   - Generate quizzes

## Project Structure

```
second-brain/
├── client/                 # React frontend
│   ├── src/
│   │   ├── components/     # React components
│   │   ├── contexts/       # React contexts
│   │   ├── lib/           # Firebase configuration
│   │   └── types/         # TypeScript types
│   └── package.json
├── server/                 # Express backend
│   ├── src/
│   │   └── index.ts       # Server with AI endpoints
│   └── package.json
└── package.json           # Root package.json
```

## API Endpoints

- `POST /api/notes/image` - Create note from image
- `POST /api/search` - Smart search
- `POST /api/notes/related` - Find related notes
- `POST /api/notes/quiz` - Generate quiz

## Development

### Building for Production

```bash
npm run build
```

### Linting

```bash
cd client && npm run lint
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

MIT License - see LICENSE file for details
