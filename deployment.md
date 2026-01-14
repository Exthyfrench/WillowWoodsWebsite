# WordPress on GoDaddy - Backup & Deployment Guide

## Prerequisites
- GoDaddy account access
- FTP client (FileZilla recommended - free)
- Database management tool (phpMyAdmin via GoDaddy, or MySQL Workbench)
- Text editor (VS Code works fine)

---

## Part 1: Complete Site Backup via cPanel

### Step 1: Access cPanel on GoDaddy
1. Log in to your GoDaddy account
2. Go to **Hosting** → Find your hosting plan
3. Click **Manage** on your hosting account
4. Look for **cPanel** button or link (usually near the top)
5. Click to access cPanel

### Step 2: Backup Your Database Using phpMyAdmin
1. In cPanel, scroll down to the **Databases** section
2. Click **phpMyAdmin**
3. On the left side, click your WordPress database name (usually `wp_[yourname]` or `wordpress`)
4. Click the **Export** tab at the top
5. Make sure **SQL** is selected under "Export Method"
6. Click **Go** button
7. A `.sql` file will download to your computer - **save this somewhere safe**

### Step 3: Backup Your WordPress Files Using File Manager
1. Back in cPanel, find **File Manager** in the Files section
2. Click **File Manager**
3. Make sure **public_html** is selected on the left (this is where your WordPress site lives)
4. You'll see your WordPress folders: `wp-admin`, `wp-content`, `wp-includes`, etc.
5. Select all files by pressing **Ctrl+A**
6. Right-click → **Compress** → Choose **gzip** or **zip** format
7. A compressed file will be created (like `public_html.tar.gz` or `public_html.zip`)
8. Right-click the compressed file → **Download**
9. Save to your computer - **this is your complete backup**

**Alternative Step 3 - If Compression Fails:**
1. In File Manager, select just the **wp-content** folder (most important)
2. Right-click → **Compress** → **gzip** or **zip**
3. Download this compressed folder
4. Repeat for `wp-admin` and root level files if needed

### Step 4: Create a Backup Summary
Create a text file on your computer with this info:
```
BACKUP DATE: [TODAY'S DATE]

DATABASE BACKUP:
- File: [database-name].sql
- Location: [your computer folder path]

FILES BACKUP:
- File: public_html.tar.gz (or .zip)
- Location: [your computer folder path]

CPANEL LOGIN:
- cPanel URL: [your GoDaddy-provided cPanel address]
- Username: [your cPanel username]

WORDPRESS LOGIN:
- Admin URL: yoursite.com/wp-admin
- Admin Username: [your WordPress admin username]
```

---

## Part 2: Making Changes to Your WordPress Site

### Option A: Using WordPress Admin Dashboard (Easiest)
1. Go to `yoursite.com/wp-admin`
2. Log in with your WordPress credentials
3. Make changes via:
   - **Pages** - edit existing pages
   - **Posts** - add/edit blog posts
   - **Appearance** → **Customize** - change theme/design
   - **Plugins** - add functionality

### Option B: Editing Theme Files via FTP (Advanced)
1. Connect via FileZilla (see Part 1, Step 2)
2. Navigate to `public_html/wp-content/themes/[your-theme-name]`
3. Download the files you want to edit
4. Edit locally in VS Code
5. Upload modified files back to the same location

### Option C: Uploading a Custom Plugin
1. Create/download your plugin folder
2. Connect via FileZilla
3. Navigate to `public_html/wp-content/plugins`
4. Upload your plugin folder
5. In WordPress Admin: **Plugins** → **Activate** your plugin

---

## Part 3: Deploying Changes

### After Making Changes in WordPress Admin:
- Changes are **automatically saved** to the database
- **No deployment needed** - changes go live immediately
- Visit your site to verify

### After Editing Files via FTP:
1. Make changes locally in VS Code
2. Save the file
3. In FileZilla, upload the file to the same location it came from
4. **Clear your browser cache** (Ctrl+Shift+Delete)
5. Visit your site to verify changes appear

### Best Practice Workflow:
```
1. Make local backup (Part 1)
2. Make ONE small change
3. Deploy/Upload
4. Test on live site
5. If good → continue with next change
6. If broken → restore from backup
```

---

## Part 4: If Something Goes Wrong - Restore from Backup

### Restore Database:
1. Go to cPanel → **phpMyAdmin**
2. Click your database name
3. Click **Import** at the top
4. Select your `.sql` backup file
5. Click **Go**
6. Wait for completion message

### Restore Files:
1. Connect via FileZilla
2. Delete the broken files in `public_html`
3. Upload the backup files back
4. Clear browser cache and test

---

## Part 5: Important Folders to Know

| Folder | Purpose |
|--------|---------|
| `wp-content/themes` | Theme files |
| `wp-content/plugins` | Plugin files |
| `wp-content/uploads` | Images & media |
| `wp-admin` | WordPress administration (don't edit) |
| `wp-includes` | Core WordPress files (don't edit) |
| `wp-config.php` | Database configuration (don't edit) |

---

## Part 6: Quick Reference

### GoDaddy Support
- GoDaddy Help: support.godaddy.com
- Open a support ticket if you get stuck

### WordPress Support
- wordpress.org/support for plugin/theme issues
- Your theme/plugin's support forums

### Regular Maintenance
- **Weekly**: Check site for errors
- **Monthly**: Backup entire site (Part 1)
- **Before any change**: Create backup
