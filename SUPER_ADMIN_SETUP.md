# Super Admin Setup Guide

## Quick Setup Instructions

Your MajiVoice platform now has an easy super admin setup process. Follow these steps:

### Step 1: Access the Setup Page

Once your app is running, navigate to:

```
http://localhost:5173/#setup-admin
```

Or manually navigate by typing `setup-admin` in the URL hash (you can modify the app to show this page directly).

### Step 2: Create Your Super Admin Account

On the setup page, you'll see a form where you can create your first super admin account:

1. **Email**: Enter your admin email (default: `admin@majivoice.ke`)
2. **Password**: Create a strong password (minimum 8 characters)
3. **Full Name**: Enter your full name (default: `Super Administrator`)
4. Click **Create Super Admin**

### Step 3: Login to Admin Dashboard

After successful creation:

1. You'll see a success message with your login credentials
2. Click **Go to Login** or navigate to the home page
3. Click **Admin Login** in the header
4. Enter your email and password
5. You'll be redirected to the Admin Dashboard

## What You Can Do as Admin

Once logged in, you have access to:

- **Dashboard**: View all submitted water issues
- **Filter & Search**: Find issues by status, urgency, type, county, subcounty, or ward
- **Update Issues**: Change status, urgency, assign to utility companies
- **Add Notes**: Internal admin notes and public update messages
- **View Media**: Access all photos and videos attached to issues
- **Analytics**: View comprehensive statistics and trends
- **Export Data**: Download issue data as CSV

## Location Data

The system now uses the following counties and subcounties:

### Kisumu County
- Kisumu East (6 wards)
- Kisumu West (5 wards)
- Kisumu Central (5 wards)
- Seme (4 wards)
- Nyando (5 wards)
- Muhoroni (5 wards)
- Nyakach (5 wards)

### Homa Bay County
- Homa Bay Town (4 wards)
- Ndhiwa (6 wards)
- Rangwe (3 wards)
- Suba North (4 wards)
- Suba South (4 wards)
- Mbita (4 wards)
- Karachuonyo (6 wards)
- Kasipul (4 wards)

All location data is now hardcoded in the application for faster performance and offline support.

## Alternative Setup Method

If the setup page doesn't work, you can create an admin user manually:

### Using Edge Function Directly

```bash
curl -X POST https://YOUR_PROJECT_REF.supabase.co/functions/v1/create-admin \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_ANON_KEY" \
  -d '{
    "email": "admin@majivoice.ke",
    "password": "YourStrongPassword123!",
    "full_name": "Super Administrator"
  }'
```

### Using Supabase Dashboard

1. Go to Supabase Dashboard > Authentication > Users
2. Click **Add User**
3. Enter email and password
4. Check **Auto Confirm User**
5. Copy the User ID
6. Go to SQL Editor and run:

```sql
INSERT INTO profiles (id, email, full_name, role)
VALUES (
  'PASTE_USER_ID_HERE',
  'admin@majivoice.ke',
  'Super Administrator',
  'admin'
);
```

## Security Notes

- Use a strong password with at least 12 characters
- Change the default email address
- After creating your admin account, you may want to remove or protect the setup page
- All admin actions are logged in the `issue_updates` table
- Only create admin accounts for trusted personnel

## Troubleshooting

### "Failed to create admin user"
- Check that your Supabase environment variables are set correctly
- Verify the Edge Function is deployed
- Check browser console for detailed error messages

### "Email already exists"
- The email is already registered
- Use a different email or login with existing credentials

### Can't access setup page
- Make sure the app is running: `npm run dev`
- Try accessing directly via URL hash: `/#setup-admin`
- Check browser console for routing errors

## Production Deployment

For production, you should:

1. Create your super admin account first
2. Remove or protect the setup page route
3. Use environment-specific admin emails
4. Enable email verification for additional security

## Need Help?

If you encounter any issues:
1. Check the browser console for errors
2. Verify Supabase connection in Network tab
3. Check Edge Function logs in Supabase Dashboard
4. Review the ADMIN_SETUP.md for manual setup instructions

---

**Your Super Admin Credentials:**
- Default Email: `admin@majivoice.ke`
- Password: (set during setup)

**Setup Page URL:**
- Development: `http://localhost:5173/#setup-admin`
- Production: `https://yourdomain.com/#setup-admin`
