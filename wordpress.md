# WordPress

This section will provide a brief overview of common WP CLI functions. For complete documentation, please review the [Official Documentation](https://developer.wordpress.org/cli/commands/). 

---------------
<br><br>



## WP Export
Export all posts
```cmd
wp export --dir=/tmp/ --post_type=post
```
<br> 

Export all Posts by a Given User between Two Dates
```cmd
wp export --dir=/tmp/ --user=admin --post_type=post --start_date=2011-01-01 --end_date=2011-12-31
```
<br> 

Export all Posts by ID
```cmd
wp export --dir=/tmp/ --post__in=123,124,125
```
<br> 


## WP Import
Import Posts/Pages from a given export file.
```cmd
wp import example.wordpress.2016-06-21.xml --authors=create
```
<br> 


## WP Media
Regenerate thumbnails, without confirmation
```cmd
wp media regenerate --yes
```
<br> 

List all registered image sizes
```cmd
wp media image-size
```
<br> 

Import File
```cmd
wp media import ~/Downloads/image.png --title="A downloaded picture"
```
<br> 

Import File and set it to be a featured image for a post
```cmd
wp media import ~/Downloads/image.png --post_id=123 --title="A downloaded picture" --featured_image
```
<br> 



## WP Option
Get the site URL
```cmd
wp option get siteurl
```
<br> 

Add Option
```cmd
wp option add my_option foobar
```
<br> 

Update Option
```cmd
wp option update my_option '{"foo": "bar"}' --format=json
```
<br> 

Delete Option
```cmd
wp option delete my_option
```
<br> 

## WP Plugin
Activate a plugin
```cmd
wp plugin activate hello
```
<br> 

Deactivate a plugin
```cmd
wp plugin deactivate hello
```
<br> 

Delete a plugin
```cmd
wp plugin delete hello
```
<br> 

Install & Activate
```cmd
wp plugin install bbpress --activate
```
<br> 

Check if Plugin is Installed
```cmd
wp plugin is-installed hello
```
<br> 

Check if Plugin is Active
```cmd
wp plugin is-active hello
```
<br> 

Get Plugin Details
```cmd
wp plugin get bbpress --format=json
```
<br> 

List All Plugins
```cmd
wp plugin list --format=json
```
<br> 

List All Active Plugins
```cmd
wp plugin list --status=active --format=json
```
<br> 

Update Single Plugins
```cmd
wp plugin update bbpress --version=dev
```
<br> 

Update All Plugins
```cmd
wp plugin update --all --exclude=akismet
```
<br> 

## WP Post
Create A Post
```cmd
wp post create --post_type=post --post_title='A sample post'
```
<br> 

Update Post
```cmd
wp post update 123 --post_status=draft
```
<br> 

Delete Post
```cmd
wp post delete 123
```
<br> 

Get List of Posts
```cmd
wp post list
```
<br> 

Get Details for a Single Post
```cmd
wp post get 123
```
<br> 


## WP Post-Type
List all of the post types
```cmd
wp post-type list
```
<br> 

Get Post Type Details
```cmd
wp post-type get page --fields=name,label,hierarchical --format=json
```
<br> 



## WP Rewrite
Flush Rewrite Rules
```cmd
wp rewrite flush
```
<br> 

Update Permalink Structure
```cmd
wp rewrite structure '/%year%/%monthnum%/%postname%'
```
<br> 

List Rewrite Rules
```cmd
wp rewrite list --format=json
```
<br> 


## WP Scaffold
Generate a new plugin with unit tests
```cmd
wp scaffold plugin sample-plugin
```
<br> 

Create new theme (based on _S)
```cmd 
wp scaffold _s sample-theme --theme_name="Sample Theme" --author="John Doe"
```
<br> 

Create a child theme
```cmd
wp scaffold child-theme
```
<br> 

Generate Code For Post Type Registration
```cmd
wp scaffold post-type movie --label=Movie --theme=simple-life
```
<br> 

## WP Search-Replace
Search and replace but skip one column
```cmd
wp search-replace 'http://example.test' 'http://example.com' --skip-columns=guid
```
<br> 

Dry Run Search & Replace
```cmd
wp search-replace 'foo' 'bar' wp_posts wp_postmeta wp_terms --dry-run
```
<br> 


## WP Transient
Delete All Expired Transients
```cmd
wp transient delete --expired
```
<br> 

Delete all Transients
```cmd
wp transient delete --all
```
<br> 


## WP User
List User ID's
```cmd
wp user list --field=ID
```
<br> 

Create a new user
```cmd
wp user create bob bob@example.com --role=author
```
<br> 

Update existing user
```cmd
wp user update 123 --display_name=Mary --user_pass=marypass
```
<br> 

Delete User and Reassing Posts
```cmd
wp user delete 123 --reassign=567
```
