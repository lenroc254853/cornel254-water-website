# MajiReport - Setup Guide

## Overview
MajiReport is a production-ready water issue reporting system for Kenya that connects citizens with water experts who coordinate with utility companies for faster resolution.

## Features
- Mobile-first responsive design
- Multi-step issue reporting with photos
- Location-based tracking (County → Subcounty → Ward + Landmarks)
- Anonymous reporting option
- Real-time issue tracking
- Admin dashboard with filtering and analytics
- Secure authentication
- Media upload with compression
- GitHub-based location data (easily updatable)

## Tech Stack
- Frontend: React + TypeScript + Vite + Tailwind CSS
- Backend: Supabase (Database + Storage + Auth)
- Icons: Lucide React
- Location Data: GitHub JSON repository

## Prerequisites
1. Node.js 18+ and npm
2. Supabase account and project

## Setup Instructions

### 1. Supabase Configuration

The database schema has already been created with the following tables:
- `profiles` - User profiles with role-based access
- `location_cache` - Cached location data (Counties, Subcounties, Wards)
- `issues` - Water issue reports
- `issue_media` - Photos/videos attached to issues
- `issue_updates` - Timeline of issue status changes
- `issue_feedback` - User feedback after resolution

### 2. Storage Bucket Setup

You need to create a storage bucket for media uploads:

1. Go to Supabase Dashboard → Storage
2. Create a new bucket named `issue-media`
3. Set it as **Public** (so URLs are accessible)
4. Configure the bucket policies:
   - Allow public INSERT for authenticated and anonymous users
   - Allow public SELECT for everyone

### 3. Create Admin User

Create an admin user through Supabase:

1. Go to Authentication → Users
2. Add a new user with email and password
3. After creation, go to SQL Editor and run:
   ```sql
   INSERT INTO profiles (id, email, full_name, role)
   VALUES (
     'USER_ID_FROM_AUTH',
     'admin@example.com',
     'Admin Name',
     'admin'
   );
   ```

### 4. Environment Variables

The Supabase environment variables are automatically available:
- `VITE_SUPABASE_URL`
- `VITE_SUPABASE_ANON_KEY`

### 5. Location Data

The app automatically fetches Kenya location data from:
```
https://raw.githubusercontent.com/CodeForAfrica/kenya-geo-data/main/data/kenya_counties_subcounties_wards.json
```

The data is:
- Cached locally in browser localStorage
- Refreshed every 7 days automatically
- Falls back to cached data if GitHub is unavailable

To update location data:
1. Update the JSON file in the GitHub repository
2. Users will automatically receive updates within 7 days
3. Or clear localStorage to force immediate refresh

### 6. Install Dependencies

```bash
npm install
```

### 7. Run Development Server

```bash
npm run dev
```

The app will be available at `http://localhost:5173`

### 8. Build for Production

```bash
npm run build
```

## User Roles

### Public User (Reporter)
- Submit water issues with photos
- Track issue status using issue number
- Provide feedback after resolution
- Report anonymously (optional)

### Administrator (Water Expert)
- Access admin dashboard
- Review and validate submitted issues
- Update issue status and urgency
- Assign issues to utility companies
- Add internal notes
- View analytics and export data

## Key Features

### Issue Reporting
1. Multi-step form (4 steps)
2. Issue type selection (10+ types)
3. Detailed description
4. Location selection (County → Subcounty → Ward)
5. Landmark-based location description
6. GPS coordinates (auto-detected if available)
7. Photo upload (required, auto-compressed)
8. Video upload (optional)
9. Contact details (optional for non-anonymous)
10. Auto-generated unique issue number (WTR-YYYY-####)

### Issue Tracking
- Public tracking by issue number
- Status timeline with updates
- View attached media
- Provide feedback when resolved

### Admin Dashboard
- Filter by status, urgency, type, location
- Search by issue number or description
- Export to CSV
- View detailed issue information
- Update status and urgency
- Assign to utility companies
- Add notes and updates

### Analytics
- Total issues, resolved count, resolution time
- Issues by status, urgency, type
- Top counties by issue count
- 30-day trend analysis

## Issue Workflow

1. **Submitted** - New issue reported
2. **Under Review** - Admin reviewing the issue
3. **Verified** - Issue validated by admin
4. **Escalated** - Forwarded to utility company
5. **In Progress** - Being resolved
6. **Resolved** - Issue fixed
7. **Reopened** - Issue reported again

## Security Features

- Row Level Security (RLS) on all tables
- Authenticated admin access only for dashboard
- Public can report and track issues
- Anonymous reporting supported
- Media file validation and compression
- Secure storage with public URLs

## Mobile Optimization

- Mobile-first responsive design
- Touch-friendly UI
- Optimized images
- Fast loading on slow connections
- Offline draft saving (localStorage)
- PWA-ready

## Support

For issues or questions, contact the development team.

## License

Copyright 2024. All rights reserved.
