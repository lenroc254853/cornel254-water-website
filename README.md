# MajiReport - Water Issue Reporting System for Kenya

A production-ready mobile-first web application that connects citizens with water service experts to report, track, and resolve water-related issues across Kenya.

## Overview

MajiReport serves as a bridge between citizens and water utilities, ensuring accountability and structured follow-up for water service delivery. All reports are reviewed by a water expert coordinator who validates issues and escalates them to relevant water utility companies.

## Key Features

### For Public Users
- **Quick Reporting**: Submit water issues in under 2 minutes with a simple 4-step form
- **Photo Documentation**: Upload photos (required) and videos (optional) with automatic compression
- **Location-Based**: Select County → Subcounty → Ward + provide landmark descriptions
- **Anonymous Option**: Report issues anonymously if preferred
- **GPS Detection**: Automatic GPS coordinates if available
- **Issue Tracking**: Track progress using unique issue number (WTR-YYYY-####)
- **Real-time Updates**: View timeline of status changes and admin actions
- **Feedback System**: Rate and provide feedback after resolution

### For Administrators
- **Comprehensive Dashboard**: View all issues with advanced filtering
- **Status Management**: Update issue status through workflow (Submitted → Under Review → Verified → Escalated → In Progress → Resolved)
- **Urgency Control**: Set priority levels (Low, Medium, High, Critical)
- **Utility Assignment**: Assign issues to specific water utility companies
- **Internal Notes**: Add private admin notes for tracking
- **Public Updates**: Post update messages visible to reporters
- **Export Data**: Download issue data as CSV
- **Analytics**: View trends, statistics, and performance metrics

## Tech Stack

- **Frontend**: React 18 + TypeScript + Vite
- **Styling**: Tailwind CSS
- **Database**: Supabase (PostgreSQL)
- **Storage**: Supabase Storage (for media files)
- **Authentication**: Supabase Auth
- **Icons**: Lucide React
- **Location Data**: GitHub-hosted JSON (Kenya Counties/Subcounties/Wards)

## Project Structure

```
src/
├── components/          # Reusable UI components
│   ├── Header.tsx      # Navigation header
│   └── Footer.tsx      # Site footer
├── contexts/           # React contexts
│   └── AuthContext.tsx # Authentication state management
├── lib/                # Utilities and services
│   ├── supabase.ts    # Supabase client
│   ├── database.types.ts # TypeScript types for database
│   ├── constants.ts   # App constants (issue types, statuses)
│   ├── locationService.ts # Location data fetching and caching
│   └── mediaUtils.ts  # Image compression and validation
├── pages/             # Application pages
│   ├── HomePage.tsx   # Landing page
│   ├── ReportIssuePage.tsx # Issue reporting form
│   ├── TrackIssuePage.tsx # Public issue tracking
│   ├── AdminLoginPage.tsx # Admin authentication
│   ├── AdminDashboardPage.tsx # Admin issue list
│   ├── AdminIssueDetailPage.tsx # Admin issue management
│   └── AdminAnalyticsPage.tsx # Analytics and insights
├── App.tsx            # Main app component with routing
└── main.tsx           # App entry point
```

## Database Schema

### Tables
- **profiles**: User profiles with role-based access (admin/reporter)
- **location_cache**: Cached location data (Counties, Subcounties, Wards)
- **issues**: Water issue reports with full details
- **issue_media**: Photos and videos attached to issues
- **issue_updates**: Timeline of status changes and actions
- **issue_feedback**: User feedback after resolution

### Security
- Row Level Security (RLS) enabled on all tables
- Public can create and view issues
- Only admins can update issue status
- Anonymous reporting supported

## Setup Instructions

### Prerequisites
- Node.js 18+ and npm
- Supabase account and project

### 1. Install Dependencies
```bash
npm install
```

### 2. Configure Supabase

The database schema has been automatically created. You need to:

1. **Create Storage Bucket** (See STORAGE_SETUP.md)
   - Create bucket named `issue-media`
   - Set as public
   - Configure upload policies

2. **Create Admin User** (See ADMIN_SETUP.md)
   - Create user in Supabase Authentication
   - Add profile with admin role

### 3. Environment Variables

Supabase environment variables are automatically available:
- `VITE_SUPABASE_URL`
- `VITE_SUPABASE_ANON_KEY`

### 4. Run Development Server
```bash
npm run dev
```

### 5. Build for Production
```bash
npm run build
```

## Issue Types Supported

1. No water supply
2. Low pressure
3. Burst pipes
4. Leaks
5. Contaminated water
6. Sewer blockage/overflow
7. Illegal connections
8. Faulty meters
9. Borehole/well issues
10. Flooding related to infrastructure

## Issue Workflow States

1. **Submitted**: New issue reported by citizen
2. **Under Review**: Admin reviewing and validating
3. **Verified**: Issue confirmed and documented
4. **Escalated**: Forwarded to utility company
5. **In Progress**: Being actively resolved
6. **Resolved**: Issue fixed and closed
7. **Reopened**: Issue reported again

## Location Data

Location data is automatically fetched from GitHub and includes:
- All 47 Counties in Kenya
- Subcounties for each county
- Wards for each subcounty

**Features:**
- Cached locally for 7 days
- Automatic refresh
- Offline fallback
- Dependent dropdowns (County → Subcounty → Ward)
- Mandatory landmark description for precise location

## Media Upload

- **Images**: Required, auto-compressed to max 1920px
- **Videos**: Optional, max 50MB
- **Formats**: JPG, PNG, WebP, MP4, MOV
- **Storage**: Supabase Storage with public URLs
- **Validation**: Client-side file type and size checks

## Mobile Optimization

- Mobile-first responsive design
- Touch-friendly UI elements
- Optimized for slow connections
- Works on all screen sizes
- Progressive Web App ready

## Documentation

- **SETUP.md**: Complete setup guide
- **STORAGE_SETUP.md**: Storage bucket configuration
- **ADMIN_SETUP.md**: Admin user creation guide

## Scripts

```bash
npm run dev          # Start development server
npm run build        # Build for production
npm run preview      # Preview production build
npm run lint         # Run ESLint
npm run typecheck    # Run TypeScript type checking
```

## Security Features

- Row Level Security (RLS) on all database tables
- Authenticated admin access for dashboard
- Public reporting and tracking
- Anonymous reporting option
- Secure media storage
- Input validation and sanitization

## Browser Support

- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## Performance

- Fast initial load
- Optimized images
- Code splitting
- Lazy loading
- Efficient caching

## Future Enhancements

- SMS-based reporting
- Utility company login portals
- County-level dashboards
- Public transparency reports
- AI-based issue categorization
- Push notifications
- Offline-first capability
- Multi-language support

## Support

For technical support or questions:
- Check the documentation files
- Review Supabase logs for errors
- Verify database schema and RLS policies

## License

Copyright 2024. All rights reserved.

## Contributors

Built with care for better water service delivery in Kenya.
