# Rely - Community Help Platform

A full-stack web application that connects people within communities to help each other, with a reward points system to encourage participation.

## Features

- **User Authentication**: Secure signup and login with Supabase Auth
- **Communities**: Create or join communities using join codes
- **Help Requests**: Post requests for help with photos and location
- **Request Management**: Accept and complete requests to earn points
- **Points System**: Earn reward points by helping others
- **Real-time Feed**: View all help requests from your communities

## Tech Stack

### Frontend
- **React 18** with TypeScript
- **Vite** for fast development and building
- **Tailwind CSS** for styling
- **React Router** for navigation
- **Lucide React** for icons

### Backend
- **Supabase** for database and authentication
- **Supabase Edge Functions** for API endpoints
- **PostgreSQL** with Row Level Security (RLS)

## Getting Started

### Prerequisites

- Node.js 18 or higher
- npm or yarn
- A Supabase account

### Environment Setup

1. Create a `.env` file in the project root:

```env
VITE_SUPABASE_URL=your_supabase_project_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
```

2. Get your Supabase credentials:
   - Go to your Supabase project dashboard
   - Navigate to Settings > API
   - Copy the Project URL and anon/public key

### Installation

```bash
# Install dependencies
npm install

# Run development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

## Database Schema

The application uses the following tables:

- **profiles**: User profile information (linked to auth.users)
- **communities**: Community groups
- **community_members**: Junction table for user-community membership
- **requests**: Help requests with status tracking
- **transactions**: Point transaction history

All tables have Row Level Security enabled to ensure users can only access data from their communities.

## API Endpoints

### Requests API (`/functions/v1/requests`)
- `GET /requests?communityId=<id>` - Fetch requests (optionally filtered by community)
- `POST /requests` - Create a new request
- `POST /requests/:id/accept` - Accept a request
- `POST /requests/:id/complete` - Mark request as complete and award points

### Communities API (`/functions/v1/communities`)
- `GET /communities/mine` - Fetch user's communities
- `POST /communities` - Create a new community
- `POST /communities/join` - Join a community with a join code

## User Flow

1. **Sign Up / Login**: Create an account or sign in
2. **Join/Create Community**: Join an existing community with a code or create a new one
3. **Browse Feed**: View help requests from your communities
4. **Create Request**: Post a new help request with details, photo, and location
5. **Accept Request**: Help others by accepting their requests
6. **Complete Request**: Request creator marks the request as complete
7. **Earn Points**: Helper receives points as a reward

## Development

### Project Structure

```
src/
├── components/
│   ├── Navbar.tsx          # Navigation bar with user info
│   └── RequestCard.tsx     # Request display card component
├── pages/
│   ├── Login.tsx           # Login page
│   ├── Signup.tsx          # Signup page
│   ├── Home.tsx            # Landing page
│   ├── CreateRequest.tsx   # Request creation form
│   ├── Communities.tsx     # Community management
│   └── Feed.tsx            # Help requests feed
├── services/
│   ├── supabase.ts         # Supabase client setup
│   └── api.ts              # API service layer
├── types/
│   └── index.ts            # TypeScript type definitions
├── App.tsx                 # Main app with routing
└── main.tsx                # App entry point
```

### Edge Functions

The backend uses Supabase Edge Functions deployed at:
- `requests` - Handles all request-related operations
- `communities` - Manages community creation and joining

## Security

- All API routes require authentication
- Row Level Security (RLS) policies ensure users can only access data from their communities
- Request creators are the only ones who can mark requests as complete
- Points are awarded automatically when requests are completed

## License

MIT License
