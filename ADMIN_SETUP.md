# Admin User Setup Guide

## Creating Your First Admin User

To access the admin dashboard, you need to create an admin user account. Follow these steps:

### Step 1: Create User in Supabase Authentication

1. Go to your Supabase Dashboard
2. Navigate to **Authentication** → **Users**
3. Click **Add User** (or **Invite**)
4. Enter user details:
   - **Email**: admin@yourdomain.com (use your actual email)
   - **Password**: Create a strong password
   - **Auto Confirm User**: ✅ Check this (skip email confirmation)
5. Click **Create User**
6. **Important**: Copy the User ID (UUID) - you'll need it in the next step

### Step 2: Add Admin Role to Profile

After creating the user, you need to add them to the `profiles` table with admin role:

#### Using SQL Editor:

1. Go to **SQL Editor**
2. Create a new query
3. Paste and run this SQL (replace the placeholders):

```sql
-- Replace 'YOUR_USER_ID' with the actual UUID from Step 1
-- Replace the email with your admin email
INSERT INTO profiles (id, email, full_name, role)
VALUES (
  'YOUR_USER_ID_HERE',
  'admin@yourdomain.com',
  'Admin Name',
  'admin'
);
```

**Example:**
```sql
INSERT INTO profiles (id, email, full_name, role)
VALUES (
  'a1b2c3d4-e5f6-7890-abcd-ef1234567890',
  'john.doe@example.com',
  'John Doe',
  'admin'
);
```

#### Using Table Editor (Alternative):

1. Go to **Table Editor**
2. Select the `profiles` table
3. Click **Insert row**
4. Fill in the fields:
   - **id**: Paste the User ID from Step 1
   - **email**: Same email as authentication user
   - **full_name**: Admin's full name
   - **role**: Select `admin` from dropdown
5. Click **Save**

### Step 3: Verify Admin Access

1. Open your MajiReport application
2. Click **Admin Login** in the header
3. Sign in with the credentials you created
4. You should be redirected to the Admin Dashboard
5. Verify you can see:
   - Dashboard with statistics
   - Issue list
   - Analytics menu option

## Creating Additional Admin Users

To create more admin users, repeat the process:

1. Create user in Authentication
2. Add profile entry with `role = 'admin'`

## Removing Admin Access

To revoke admin access from a user:

```sql
UPDATE profiles
SET role = 'reporter'
WHERE email = 'user@example.com';
```

## Troubleshooting

### "Invalid email or password" error
- Double-check the email and password
- Ensure the user was created in Supabase Authentication
- Check if "Auto Confirm User" was enabled

### Can't access admin dashboard after login
- Verify the user has a profile entry in the `profiles` table
- Check that the `role` field is set to `'admin'`
- Run this query to verify:
  ```sql
  SELECT * FROM profiles WHERE email = 'your-email@example.com';
  ```

### "User not found" in profiles table
- Make sure the `id` in profiles matches the User ID in Authentication
- The IDs must match exactly (they are UUIDs)

### Logged in but redirected to login page
- Clear browser cache and cookies
- Check browser console for errors
- Verify Supabase environment variables are set correctly

## Security Best Practices

1. **Use Strong Passwords**
   - Minimum 12 characters
   - Mix of uppercase, lowercase, numbers, symbols
   - Avoid common words or patterns

2. **Limit Admin Access**
   - Only create admin accounts for trusted personnel
   - Review admin list regularly
   - Remove admin access when no longer needed

3. **Monitor Admin Activity**
   - Check the `issue_updates` table to see admin actions
   - All status changes are logged with admin user ID

4. **Regular Password Updates**
   - Encourage admins to change passwords periodically
   - Use Supabase's password reset functionality

## Admin Capabilities

Once logged in as admin, you can:

✅ View all submitted issues
✅ Filter and search issues
✅ Update issue status and urgency
✅ Assign issues to utility companies
✅ Add internal admin notes
✅ Add public update messages
✅ View issue timeline and history
✅ Export data to CSV
✅ View analytics and reports
✅ Access all uploaded media

## Need Help?

If you encounter issues during setup:
1. Check the Supabase logs for error messages
2. Verify RLS policies are correctly set up
3. Ensure the database schema is complete
4. Review the SETUP.md file for general setup instructions
