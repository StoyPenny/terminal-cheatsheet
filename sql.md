# MySQL
A collection of useful MySQL terminal commands. 

---------------


### Access MySQL
Login to a MySQL session. 
```cmd
mysql -u [username] -p;  // will prompt for password
```
<br>

### Show All Databases
Show all of the available databases.
```cmd
show databases;
```
<br>

### Create A Database
Select a database.
```cmd
create database [database];
```
<br>

### Select A Database
Select a database.
```cmd
use [database];
```
<br>

### Show All Tables
Show all of the tables in the active database.
```cmd
show tables;
```
<br>

### Show Table Structure
Show the table structure for a specific table.
```cmd
describe [table];
```
<br>

### Select Data From Table
Select data from the active database.
```cmd
SELECT * FROM [table];
```
<br>

### Update Data In A Table
Update a row in the database based on conditions.
```cmd
UPDATE [table] SET [column] = '[updated-value]' WHERE [column] = [value];
```
<br>

### Clone A Database
Copy a database to another database on the same server.
```cmd
mysqldump -u <user name> --password=<pwd> <original db> | mysql -u <user name> -p <new db>
```
<br>

### Backup Database
Create a backup of a single database. You must specify the database name as well as the folder where the database will be saved to. 
```
mysqldump -u USER -p products > /mnt/backups/products.sql
```
<br>

### Backup All Databases
Backup all databases in one command, just specifiy a location to store the backup. 
```
mysqldump -u USER -p --all-databases > /mnt/backups/all_databases.sql
```
<br>

### Backup and Compress Databases
Make a backup of the database and also compress the database to save space on the server. You will need to specify the database that you would like to backup as well as where you would like to store it. 
```
mysqldump -u USER -p -C products > /mnt/backups/products.sql.tgz
```
<br>

### Get Size of All Tables in Database (KB)
Get the KB size of all the tables in a database.
```sql
SELECT
  TABLE_NAME AS `Table`,
  ROUND((DATA_LENGTH + INDEX_LENGTH) / 1024) AS `Size (KB)`
FROM
  information_schema.TABLES
WHERE
  TABLE_SCHEMA = "{{database_name}}"
ORDER BY
  (DATA_LENGTH + INDEX_LENGTH)
DESC;
```
<br>

### Get Size of All Tables in Database (MB)
Get the MB size of all the tables in a database.
```sql
SELECT
  TABLE_NAME AS `Table`,
  ROUND((DATA_LENGTH + INDEX_LENGTH) / 1024 / 1024) AS `Size (MB)`
FROM
  information_schema.TABLES
WHERE
  TABLE_SCHEMA = "{{database_name}}"
ORDER BY
  (DATA_LENGTH + INDEX_LENGTH)
DESC;
```
<br>

### Get Size of One Table in a Database (KB)
Get the KB size of all the tables in a database.
```sql
SELECT
  TABLE_NAME AS `Table`,
  ROUND((DATA_LENGTH + INDEX_LENGTH) / 1024) AS `Size (KB)`
FROM
  information_schema.TABLES
WHERE
  	TABLE_SCHEMA = "{{database_name}}"
  AND
    TABLE_NAME = "{{table_name}}"
ORDER BY
  (DATA_LENGTH + INDEX_LENGTH)
DESC;
```


---------------


## WordPress MySQL Queries
This file is a collection of useful WordPress database queries. These queries range from clean up and maintenance to enhancements and recovery. Commands are listed in no particular order...

**TOC**
- [Update The Site URL in the Database](#update-the-site-url-in-the-database)
- [Get User ID by Email](#get-user-id-by-email)
- [Update User Password](#update-user-password)
- [Update The Site URL in the Database](#update-the-site-url-in-the-database)
- [Update User Password](#update-user-password)
- [Delete Post Revisions](#delete-post-revisions)
- [Find & Remove Orphaned Post Meta](#find-and-remove-orphaned-post-meta)
- [Find & Remove Orphaned Comment Meta](#find-and-remove-orphaned-comment-meta)
- [Find and Remove WP Session Data](#find-and-remove-wp-session-data)
- [Delete WP Transients](#delete-wp-transients)
- [Remove Unused Tags](#remove-unused-tags)
- [Disable Pingbacks and Trackbacks](#disable-pingbacks-and-trackbacks)
- [Delete Pingbacks and Trackbacks from the database](#delete-pingbacks-and-trackbacks-from-the-database)
- [Find WP Version In Database](#find-wp-version-in-database)
- [Delete All Spam Comments](#delete-all-spam-comments)
- [Update GUID](#update-guid)
- [Update URLs in Content](#update-urls-in-content)
- [Find Posts With The Most Spam](#find-posts-with-the-most-spam)
- [Find Where Spam Comes From](#find-where-spam-comes-from)
- [Find All Posts With A Field](#find-all-posts-with-a-field)
- [Find All Posts Where Field Is Missing](#find-all-posts-where-field-is-missing)
- [Disable All Plugins](#disable-all-plugins)
- [Remove Encoded Characters](#remove-encoded-characters)
- [Delete the Feed Cache](#delete-the-feed-cache)
- [Switch Themes](#switch-themes)
<br><br>

### Update The Site URL in the Database
<pre>UPDATE wp_options SET option_value = '<b>http://yourwebsite.com</b>' WHERE option_name = 'siteurl';</pre>
<pre>UPDATE wp_options SET option_value = '<b>http://yourwebsite.com</b>' WHERE option_name = 'home';</pre>
<br>


### Get User ID by Email
<pre>SELECT ID FROM wp_users WHERE user_email='<b>someone@somewhere.com</b>';</pre>
<br>

### Update User Password
<pre>UPDATE wp_users SET user_pass = MD5( '<b>new_password</b>' ) WHERE ID = <b>user_id</b>;</pre>
<br>


### Delete Post Revisions
Delete all post revisions:
<pre>DELETE FROM wp_posts WHERE post_type = "revision";</pre>
<br>


### Find & Remove Orphaned Post Meta
Find any orphaned Post Meta:
<pre>SELECT COUNT(pm.meta_id) as row_count FROM wp_postmeta pm LEFT JOIN wp_posts wp ON wp.ID = pm.post_id WHERE wp.ID IS NULL;</pre>
Delete orphaned Post Meta:
<pre>DELETE pm FROM wp_postmeta pm LEFT JOIN wp_posts wp ON wp.ID = pm.post_id WHERE wp.ID IS NULL;</pre>
<br>


### Find & Remove Orphaned Comment Meta
Find any orphaned Comment Meta:
<pre>SELECT COUNT(*) as row_count FROM wp_commentmeta WHERE comment_id NOT IN (SELECT comment_id FROM wp_comments);</pre>
Delete orphaned Comment Meta:
<pre>DELETE FROM wp_commentmeta WHERE comment_id NOT IN (SELECT comment_id FROM wp_comments);</pre>
<br>


### Find and Remove WP Session Data
Find any session data:
<pre>SELECT * FROM `wp_options` WHERE `option_name` LIKE '_wp_session_%';</pre>
<pre>DELETE FROM `wp_options` WHERE `option_name` LIKE '_wp_session_%';</pre>
<br>


### Delete WP Transients
<pre>DELETE FROM `wp_options` WHERE `option_name` LIKE ('%_transient_%');</pre>
<br>


### Remove Unused Tags
<pre>DELETE FROM wp_terms WHERE term_id IN (SELECT term_id FROM wp_term_taxonomy WHERE count = 0 );</pre>
<pre>DELETE FROM wp_term_taxonomy WHERE term_id not IN (SELECT term_id FROM wp_terms);</pre>
<pre>DELETE FROM wp_term_relationships WHERE term_taxonomy_id not IN (SELECT term_taxonomy_id FROM wp_term_taxonomy);</pre>
<br>


### Disable Pingbacks and Trackbacks
Disable Pingbacks on your website.
<pre>UPDATE wp_posts SET ping_status = 'closed';</pre>
<br>


### Delete Pingbacks and Trackbacks from the database
<pre>DELETE FROM wp_comments WHERE comment_type = 'pingback';</pre>
<pre>DELETE FROM wp_comments WHERE comment_type = 'trackback';</pre>
<br>


### Find WP Version In Database
Use the following command to give you the database version number:
<pre>SELECT * FROM `wp_options` where option_name = 'db_version';</pre>
Once you have the number that it gives back to you, you can cross reference that with the table on [this page of the Codex](https://codex.wordpress.org/WordPress_Versions) to find what version of WordPress you are running.
<br>
<br>


### Delete All Spam Comments
<pre>DELETE FROM wp_comments WHERE comment_approved = 'spam';</pre>
<br>


### Update GUID
<pre>UPDATE wp_posts SET guid = REPLACE (guid, '<b>http://www.oldsiteurl.com</b>', '<b>http://www.newsiteurl.com</b>');
</pre>
<br>


### Update URLs in Content
<pre>UPDATE wp_posts SET post_content = REPLACE (post_content, '<b>http://www.oldsiteurl.com</b>', '<b>http://www.newsiteurl.com</b>');</pre>
<br>



### Find Posts With The Most Spam
This query is useful for finding which of your posts attract the most spam
<pre>
SELECT `comment_post_ID`, COUNT(*) as amount
FROM `wp_comments`
WHERE `comment_approved` = 'spam'
GROUP BY `comment_post_ID`
ORDER BY amount DESC
LIMIT 0, 20
</pre>
<br>


### Find Where Spam Comes From
Use this query to find where your spam is coming from. This will show you the top 30 IPs that are spamming your site:
<pre>
SELECT   `comment_author_IP`, COUNT(*) AS amount
FROM     `wp_comments`
WHERE    `comment_approved` = 'spam'
GROUP BY `comment_author_IP`
HAVING    amount &gt; 10
ORDER BY  amount DESC
LIMIT     0, 30
</pre>

If there are some big offenders here, you can safely block them in your `.htaccess` file.
<pre>
# IP block list
order allow,deny
deny from 173.242.120.58
allow from all
</pre>
<br>


### Find All Posts With A Field
Find all posts (or pages) that have a specific field attached to them.
<pre>
SELECT wp_posts.ID, wp_postmeta.meta_key
 FROM wp_posts
 JOIN wp_postmeta ON wp_posts.ID = wp_postmeta.post_id
 AND wp_postmeta.meta_key = 'FIELD_NAME'
 WHERE wp_posts.post_type = 'post'
 order by wp_posts.ID asc
</pre>
<br>


### Find All Posts Where Field Is Missing
Use the following command if you are looking for a group of posts that are missing a specific field.
<pre>
SELECT wp_posts.ID, wp_postmeta.meta_key
 FROM wp_posts
 LEFT JOIN wp_postmeta ON wp_posts.ID = wp_postmeta.post_id
 AND wp_postmeta.meta_key = 'CUSTOM_FIELD_NAME'
 WHERE wp_postmeta.meta_key is null and wp_posts.post_type = 'post'
 order by wp_posts.ID asc 
</pre>
<br>


### Disable All Plugins
The following command will disable all plugins on your website. Very useful when testing websites or when encountering an error on your website.
<pre>UPDATE wp_options SET option_value = 'a:0:{}' WHERE option_name = 'active_plugins';</pre>
<br>



### Remove Encoded Characters
Use the following SQL commands to remove weird characters from your website.
<pre>
UPDATE wp_posts SET post_content = REPLACE(post_content, 'â€œ', '“');
UPDATE wp_posts SET post_content = REPLACE(post_content, 'â€', '”');
UPDATE wp_posts SET post_content = REPLACE(post_content, 'â€™', '’');
UPDATE wp_posts SET post_content = REPLACE(post_content, 'â€˜', '‘');
UPDATE wp_posts SET post_content = REPLACE(post_content, 'â€”', '–');
UPDATE wp_posts SET post_content = REPLACE(post_content, 'â€“', '—');
UPDATE wp_posts SET post_content = REPLACE(post_content, 'â€¢', '-');
UPDATE wp_posts SET post_content = REPLACE(post_content, 'â€¦', '…');

UPDATE wp_comments SET comment_content = REPLACE(comment_content, 'â€œ', '“');
UPDATE wp_comments SET comment_content = REPLACE(comment_content, 'â€', '”');
UPDATE wp_comments SET comment_content = REPLACE(comment_content, 'â€™', '’');
UPDATE wp_comments SET comment_content = REPLACE(comment_content, 'â€˜', '‘');
UPDATE wp_comments SET comment_content = REPLACE(comment_content, 'â€”', '–');
UPDATE wp_comments SET comment_content = REPLACE(comment_content, 'â€“', '—');
UPDATE wp_comments SET comment_content = REPLACE(comment_content, 'â€¢', '-');
UPDATE wp_comments SET comment_content = REPLACE(comment_content, 'â€¦', '…');
</pre>
<br>



### Delete the Feed Cache
<pre>DELETE FROM `wp_options` WHERE `option_name` LIKE ('_transient%_feed_%');</pre>
<br>


### Switch Themes
Use the following command to easily switch themes without accessing the WP Admin.
<pre>UPDATE wp_options SET option_value = '<b>twentynineteen</b>' WHERE option_name = 'template' or option_name = 'stylesheet';</pre>


### Find Posts with Content
Find posts/pages with specific content. 
`SELECT * FROM wp_postmeta WHERE meta_value LIKE '%bontera%'`
`SELECT * FROM wp_posts WHERE post_content LIKE '%bontera%'`


### Get Page Title by ID
`SELECT post_title FROM wp_posts WHERE id = 12860`
