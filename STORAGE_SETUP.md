# Storage Bucket Setup Guide

## Create Storage Bucket

You need to create a storage bucket in Supabase for media uploads (photos and videos).

### Method 1: Using Supabase Dashboard (Recommended)

1. Go to your Supabase project dashboard
2. Navigate to **Storage** in the left sidebar
3. Click **New Bucket**
4. Configure the bucket:
   - **Name**: `issue-media`
   - **Public bucket**: ✅ Check this box
   - Click **Create bucket**

### Method 2: Using SQL

Run this SQL in your Supabase SQL Editor:

```sql
-- Create the storage bucket
INSERT INTO storage.buckets (id, name, public)
VALUES ('issue-media', 'issue-media', true)
ON CONFLICT (id) DO NOTHING;
```

## Configure Storage Policies

After creating the bucket, you need to set up policies to allow public access for uploads and viewing.

### Using SQL (Run in SQL Editor):

```sql
-- Allow anyone to upload files (INSERT)
CREATE POLICY "Allow public uploads"
ON storage.objects
FOR INSERT
TO public
WITH CHECK (bucket_id = 'issue-media');

-- Allow anyone to view/download files (SELECT)
CREATE POLICY "Allow public access to files"
ON storage.objects
FOR SELECT
TO public
USING (bucket_id = 'issue-media');

-- Allow authenticated users to upload
CREATE POLICY "Allow authenticated uploads"
ON storage.objects
FOR INSERT
TO authenticated
WITH CHECK (bucket_id = 'issue-media');

-- Allow authenticated users to view
CREATE POLICY "Allow authenticated access"
ON storage.objects
FOR SELECT
TO authenticated
USING (bucket_id = 'issue-media');
```

### Using Dashboard (Alternative):

1. Go to **Storage** → Click on `issue-media` bucket
2. Click **Policies** tab
3. Create the following policies:

**Policy 1: Public Upload**
- Operation: INSERT
- Target roles: public
- Policy definition: `bucket_id = 'issue-media'`

**Policy 2: Public Read**
- Operation: SELECT
- Target roles: public
- Policy definition: `bucket_id = 'issue-media'`

**Policy 3: Authenticated Upload**
- Operation: INSERT
- Target roles: authenticated
- Policy definition: `bucket_id = 'issue-media'`

**Policy 4: Authenticated Read**
- Operation: SELECT
- Target roles: authenticated
- Policy definition: `bucket_id = 'issue-media'`

## Verify Setup

To verify the bucket is set up correctly:

1. Go to **Storage** → `issue-media` bucket
2. Try uploading a test file
3. Check that the file is accessible via its public URL
4. The URL format should be:
   ```
   https://[YOUR_PROJECT_REF].supabase.co/storage/v1/object/public/issue-media/[FILE_PATH]
   ```

## File Upload Limits

Configure file upload limits in your Supabase dashboard:

1. Go to **Storage** → `issue-media` → **Configuration**
2. Recommended settings:
   - **Max file size**: 50 MB (for videos)
   - **Allowed MIME types**:
     - `image/jpeg`
     - `image/jpg`
     - `image/png`
     - `image/webp`
     - `video/mp4`
     - `video/quicktime`

## Security Notes

- The bucket is public to allow anonymous reporting
- Files are validated on the client-side before upload
- Images are automatically compressed before upload
- All uploads are logged in the `issue_media` table
- File paths include issue IDs for organization

## Troubleshooting

### Error: "Bucket not found"
- Make sure the bucket name is exactly `issue-media`
- Check that the bucket exists in the Storage section

### Error: "Permission denied"
- Verify storage policies are created correctly
- Check that the bucket is set as public
- Ensure RLS policies allow the operation

### Error: "File too large"
- Check max file size settings
- Images should be under 10MB (auto-compressed)
- Videos should be under 50MB

## Maintenance

- Monitor storage usage in Supabase dashboard
- Set up automatic cleanup for old files if needed
- Consider implementing file retention policies
- Review and optimize storage costs regularly
