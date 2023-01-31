# FAQ Troubleshooting

## Why can't I see my posts? All I see is Sorry, no posts match your criteria? {#why-cant-i-see-my-posts-all-i-see-is-sorry-no-posts-match-your-criteria}

Clearing your browser cache and cookies may resolve this problem. Also, check your `search.php` and `index.php` template files for errors.

See also:

* [I Make Changes and Nothing Happens](https://codex.wordpress.org/I%20Make%20Changes%20and%20Nothing%20Happens)

## How do I find more help? {#how-do-i-find-more-help}

There are various resources that will help you find more help with WordPress, in addition to these [FAQ](https://codex.wordpress.org/FAQ).

* [Troubleshooting](https://codex.wordpress.org/Troubleshooting)
* [Finding WordPress Help](https://codex.wordpress.org/Finding%20WordPress%20Help)
* [Using the Support Forums](https://codex.wordpress.org/Using%20the%20Support%20Forums)
* [Resources and Technical Articles about WordPress](https://codex.wordpress.org/Technical%20Articles)
* [Installation Problems](https://codex.wordpress.org/Troubleshooting#Installation_Problems)

## Where can I find help with the CSS problems I'm having? {#where-can-i-find-help-with-the-css-problems-im-having}

The following are articles that will help you troubleshoot and solve many of your [CSS](https://codex.wordpress.org/CSS) problems:

* [Blog Design and Layout](https://codex.wordpress.org/Blog%20Design%20and%20Layout)
* [Finding Your CSS Styles](https://codex.wordpress.org/Finding%20Your%20CSS%20Styles)
* [CSS Fixing Browser Bugs](https://codex.wordpress.org/CSS%20Fixing%20Browser%20Bugs)
* [CSS Troubleshooting](https://codex.wordpress.org/CSS%20Troubleshooting)
* [WordPress CSS Information and Resources](https://codex.wordpress.org/CSS)

## Why do I get an error message about Sending Referrers? {#why-do-i-get-an-error-message-about-sending-referrers}

If you got this message when trying to save a post, consider checking [Administration](https://codex.wordpress.org/Administration_Screens) > [Settings](https://codex.wordpress.org/Administration_Screens#General) > [General](https://codex.wordpress.org/Settings_General_Screen) and make sure both your **WordPress address (URI)** and the **Blog address (URI)** do not use 'www'. For example, instead of **http://www.sample.com** use **http://sample.com** in those fields. This information originally reported via [https://wordpress.org/support/topic/72235](https://wordpress.org/support/topic/72235)

See also:

* [Enable Sending Referrers](https://codex.wordpress.org/Enable%20Sending%20Referrers)

## How do I empty a database table? {#how-do-i-empty-a-database-table}

See also:

* [Emptying a Database Table](https://codex.wordpress.org/Emptying%20a%20Database%20Table)

## How do I fix the following error SQL/DB Error errcode 13 Can't create/write to file? {#how-do-i-fix-the-following-error-sql-db-error-errcode-13-cant-create-write-to-file}

**Problem:** The MySQL variable `tmpdir` is set to a directory that cannot be written to when using PHP to access MySQL.

To verify this, enter MySQL at the command line and type `show variables`;

You'll get a long list and one of them will read: **tmpdir = /somedir/** (whatever your setting is.)

**Solution:** Alter the **tmpdir** variable to point to a writable directory.

**Steps:**

1. Find the **my.cnf** file. On *nix systems this is usually in **/etc/**. On Windows system, Find the **my.ini**.
2. Once found, open this in a simple text editor and find the **[mysqld]** section.
3. Under this section, find the **tmpdir** line. If this line is commented (has a **#** at the start), delete the **#** and edit the line so that it reads: **tmpdir = /writable/dir** where **/writable/dir** is a directory to which you can write. Some use **/tmp**, or you might also try **/var/tmp** or **/usr/tmp**. On Windows, use **C:/Windows/tmp**.
4. Save the file.
5. Shutdown MySQL by typing `mysqlshutdown -u -p shutdown`.
6. Start MySQL by going to the MySQL directory and typing `./bin/safe_mysqld &`. Usually the MySQL directory is in **/usr/local** or sometimes in **/usr/** on Linux systems.

If none of this make sense and you have someone to administrate your system for you, show the above to them and they should be able to figure it out.

**Description:** You get a warning message on your browser that says:

Warning: Cannot modify header information – headers already sent by (output started at

**Reason and Solution:**

It is usually because there are spaces, new lines, or other stuff before an opening `<!--?php &lt;/code&gt;&lt;/strong&gt; tag or after a closing &lt;strong&gt;&lt;code&gt;?-->` tag, typically in **wp-config.php**. This could be true about some other file too, so please check the error message, as it will list the specific file name where the error occurred (see "Interpreting the Error Message" below). Replacing the faulty file with one from your most recent backup or one from a fresh WordPress download is your best bet, but if neither of those are an option, please follow the steps below.

Just because you cannot see anything does not mean that PHP sees the same.

1. Download the file mentioned in the error message via [FTP](https://codex.wordpress.org/FTP%20Clients) or the file manager provided in your host's control panel.
2. Open that file in a [plain text editor](https://codex.wordpress.org/Glossary#Text%20editor) (**NOT** MS Word or similar. Notepad or BBEdit are fine).
3. Check that the _very_ first characters are with no blank lines or spaces after it.
4. Before saving, or use the Save as dialog, ensure the file encoding is not **`UTF-8 BOM`** but plain **`UTF-8`** or any without the **`BOM`** suffix.

To be sure about the end of the file, do this:

1. Place the cursor between the ? and >
2. Now press the DELETE key on your computer **Note to MAC users**: The "DELETE" key on a PC deletes characters to the _right_ of the cursor. That is the key noted here.
3. Keep that key pressed
4. For at least 15 seconds
5. Now type > and
6. **save** without pressing any other key at all.
7. If you press another key, you will bring the problem back.
8. DO **NOT** PUT CODE IN UNNECESSARY CODE BLOCKS, PUT THEM IN A SINGLE PHP BLOCK.

Wrong:

```
<?php
some code;
?>

<?php
some other codes;
?>
```

Correct:

```
<?php
code;

some other code;
?>
```

Upload the file back to your server after editing and saving the file.

**Note**: Also check the encoding of the file. If the file is encoded as UTF-8 with BOM, the BOM is seen as a character which starts the output.

**Interpreting the Error Message:**

If the error message states: `Warning: Cannot modify header information - headers already sent by (output started at /path/blog/wp-config.php:34) in /path/blog/wp-login.php on line 42`, then the problem is at line #34 of `wp-config.php`, not line #42 of `wp-login.php`. In this scenario, line #42 of `wp-login.php` is the victim. It is being affected by the excess whitespace at line #34 of `wp-config.php`.

If the error message states: `Warning: Cannot modify header information - headers already sent by (output started at /path/wp-admin/admin-header.php:8) in /path/wp-admin/post.php on line 569`, then the problem is at line #8 of `admin-header.php`, not line #569 of `post.php`. In this scenario, line #569 of `post.php` is the victim. It is being affected by the excess whitespace at line #8 of `admin-header.php`.

**Other issues that might cause that error:**

In case you've used the function: wp_redirect() or tried to use a header redirect after the header (or any content at all was sent) that error message will pop. Instead use javascript redirection if needed.

## Why doesn't my "Publish" or "Save Draft" button work? {#why-doesnt-my-publish-or-save-draft-button-work}

To resolve this and similar issues, disable your plugins one at a time until you find the source of the issue. Generally, this will be due to two or more plugins trying to use the same resources (for example, JQuery or other Java-based tools).

In addition, it could be that there is a problem with your browser. A common resolution is to empty the browser's cache. Please consult the documentation for your preferred browser to learn how to do this.

## Why can't I see the visual rich editor or Quicktag buttons when using Apple's Safari browser? {#why-cant-i-see-the-visual-rich-editor-or-quicktag-buttons-when-using-apples-safari-browser}

Update your Safari browser. Early versions of Safari are not supported.

## E-mailed passwords are not being received {#e-mailed-passwords-are-not-being-received}

**Description:** When users try to register with your blog or change their passwords by entering their username and/or email, WordPress indicates that their password has been emailed to them, but it is never received.

**Reason and Solutions:** WordPress uses the standard PHP mail() function, which uses sendmail. No account information is needed. This is not generally a problem if you are using a hosting service, but if you are using your own box and do not have an SMTP server, the mail will never send. If you are using a *NIX box, you should have either postfix or sendmail on your machine; you will just need to set them up (search the Internet for how-to's). If you do not want to go through setting up a complete mail server on your *NIX box you may find [ssmtp](https://packages.debian.org/stable/mail/ssmtp) useful — it provides _"A secure, effective and simple way of getting mail off a system to your mail hub"_. On a Windows machine, try a sendmail emulator like [Glob SendMail](http://glob.com.au/sendmail/).

More help can be found on this thread of the WordPress Support Forums: https://wordpress.org/support/topic.php?id=24981 For a plugin based alternative, you could try [Configure SMTP](http://coffee2code.com/wp-plugins/configure-smtp/): _"Configure SMTP mailing in WordPress, including support for sending e-mail via SSL/TLS (such as GMail)."_

**Windows Host Server Specific:** Check your "Relay" settings on the SMTP Virtual Server. Grant access to `127.0.0.1` . Then in your _php.ini_ file, set the `SMTP` setting to the same IP address. Also set `smtp_port` to `25`.

**Ensure Proper Return Address is Used:** By default, the WordPress mailer fills in the From: field with _wordpress@example.com_ and the From: name as _WordPress_.

This is fine if this is a valid e-mail address. For example, if your real e-mail is _wordpress@example.com_, your host should pass the email on for delivery. It will probably send your mail as long as _example.com_ is setup to send and receive mail, even if _wordpress_ is not a valid mail box. But if you set you real email as the From: address and it's something like _wordpress@example.com_, the mail may not send because _gmail.com_ is not a domain handled by the mail server.

**Treated as Spam:** Your email message may have been routed to a spam folder or even worse, simply discarded as malicious. There are a couple measures you can use to convince recipient's mail servers that your message is legitimate and should be delivered as addressed.

**SPF:** (Sender Policy Framework) This is the most common anti-spam measure used. If you are on a hosted system, there is a good chance your host has set this up for the mail server you are using. Have WordPress email you and check the message headers for evidence that the message passed the SPF check. You can get a message sent by following the Forgot Password link on the login page. To keep your old password, do not follow the link in the message.  
If your system email failed the SPF check, you can set up the credentials if you have access to your DNS records and your mail server's domain belongs to you. Check the return path of the email your system sent. If the mail server listed there has your domain name, you can set up SPF credentials. There are several how-tos on the Internet.

**DKIM:** (Domain Key Identified Mail) This system is also used. You can use both SPF and DKIM in the same message. Again, just as with SPF, you can check if your receiving mailserver verified your host's domain key by examining the mail header. There is a fair chance no signature key was provided, indicating your host chose to not use this protocol. Also as with SPF, if you can edit your DNS records and the mail server belongs to your domain, you can set up DKIM credentials yourself. Some how-tos exist if you search the Internet.

To get WordPress to send the proper DKIM keys, hook the `'phpmailer_init'` action. You are passed the `$phpmailer` object. Set the necessary properties and return the object. See the class source code for more information. It's on _wp-includes/class-phpmailer.php_ .

## I used the Quicktag <!–nextpage–> in a post so why doesn't it work? {#i-used-the-quicktag-nextpage-in-a-post-so-why-doesnt-it-work}

In some [Themes](https://codex.wordpress.org/Using%20Themes), such as the WordPress Classic Theme, you may see the <!–nextpage–> work properly on your main page, but other [Themes](https://codex.wordpress.org/Using%20Themes), such as the WordPress default Theme, may only show the _page break_ when viewing the posts individually. It may be necessary to change your Theme's [template](https://codex.wordpress.org/Templates) _page.php_ or _index.php_ file to make this feature work according to your wishes. You'll need to add the following:

```
<?php wp_link_pages(); ?>
```

## MySQL Error 28 {#mysql-error-28}

It could be because:

* you are out of space on /tmp (wherever tmpdir is), or,
* you have too many files in /tmp (even if there is lots of free space)

This is a MySQL error and has nothing to do with WordPress directly; you should contact your host about it. Some users have reported that running a "repair table" command in [phpMyAdmin](https://codex.wordpress.org/phpMyAdmin) fixed the problem.

## Why are the Quote Marks escaped or not escaped? {#why-are-the-quote-marks-escaped-or-not-escaped}

If you write plugins or make advanced custom templates, you may eventually find yourself dealing with data in the database. WordPress _usually_ manages this data for you in such a way that it is immediately usable. There are circumstances though (especially if you are dealing directly with the database without using WordPress) where you will experience weirdness.

For example, quote marks cannot be stored directly in the MySQL database. MySQL uses quote marks in its SQL language. When a quote mark is used, for example, in a post, when the post is saved to the database, every quote mark gets escaped. That means a backslash character is prepended, which signifies that the next character should be taken as part of the input, and not as part of the SQL command.

For example, if you are adding the following in your post:

```
...an article about "Happiness" is at
<a href="http://example.com/happy" title="Happiness">Happiness</a>
if you would like to read it...
```

Is actually imported into the database looking like this:

```
...an article about \"Happiness\" is at
<a href=\"http://example.com/happy\" title=\"Happiness\">Happiness</a>
if you would like to read it...
```

When pulling data out of the database, the backslashes may not always be automatically removed. If this becomes an issue, you can use the [stripslashes()](https://php.net/stripslashes) PHP function on the text.

**Description:** When anyone tries to comment on a post, the window goes blank and the comment doesn't appear to have been recognised by WordPress.

**Reason and Solution:**  
The Theme that you are using is missing a critical part of the comment form so WordPress doesn't know which post the comment refers to. You need to check the comment.php in your Theme and ensure that the following code appears within the form.

```
<input type="hidden" name="comment_post_ID" value="<?php echo $id; ?>" />
```

Relevant discussion threads:

* [https://wordpress.org/support/topic/38683](https://wordpress.org/support/topic/38683)

Sometimes it may be necessary to deactivate all plugins, but you can't access the administrative menus to do so. One of two methods are available to deactivate all plugins.

Use [phpMyAdmin](https://codex.wordpress.org/phpMyAdmin) to deactivate all plugins.

1. In the table wp_options, under the _option_name_ column (field) find the _active_plugins_ row
2. Change the _option_value_ field to: **a:0:{}**

Or reset your plugins folder via [FTP](https://codex.wordpress.org/FTP%20Clients) or the file manager provided in your host's control panel. This method preserves plugin options but requires plugins be manually reactivated.

1. Via FTP or your host's file manager, navigate to the wp-contents folder (directory)
2. Via FTP or your host's file manager, rename the folder "plugins" to "plugins.hold"
3. Login to your WordPress administration plugins page (/wp-admin/plugins.php) – this will disable any plugin that is "missing".
4. Via FTP or your host's file manager, rename "plugins.hold" back to "plugins"

## How to clear the "Briefly unavailable for scheduled maintenance" message after doing automatic upgrade? {#how-to-clear-the-briefly-unavailable-for-scheduled-maintenance-message-after-doing-automatic-upgrade)}

As part of the automatic upgrade WordPress places a file named `.maintenance` in the blog **base** folder (folder that contains the wp-admin folder). If that file exists, then vistors will see the message **Briefly unavailable for scheduled maintenance. Check back in a minute.**

To stop that message from being displayed to vistors, just delete the `.maintenance` file. The automatic upgrade should be executed again, just in case it failed.

Note the core automatic upgrade feature was added with [Version 2.7](https://codex.wordpress.org/Version%202.7).

## How to fix 404 error when using Pretty Permalinks? {#how-to-fix-404-error-when-using-pretty-permalinks}

If an error 404 occurs when using the [Pretty Permalink](https://codex.wordpress.org/Introduction_to_Blogging#Pretty_Permalinks) choices such as **Day and Name** in [Administration](https://codex.wordpress.org/Administration_Screens) > [Settings](https://codex.wordpress.org/Administration_Screens#Permalinks) > [Settings_Permalinks_Screen](https://codex.wordpress.org/Settings_Permalinks_Screen) it could be a result of the **mod_rewrite** module not being activated/installed. The solution is to activate **mod_rewrite** for the Apache web-server. Check the apache/conf/httpd.conf file for the line _# LoadModule rewrite_module modules/mod_rewrite.so_  
and delete the # in front of the line. Then stop Apache and start it again. **Note:** you may have to ask your host to activate mod_rewrite.

See also:

* [Using Permalinks](https://codex.wordpress.org/Using%20Permalinks)

Relevant discussion thread:

* [https://wordpress.org/support/topic/234726](https://wordpress.org/support/topic/234726)

Not sure why this problem happens, but here's a couple of things to try one of these two solutions.

This usually fixes the problem:

1. Create new admin user (e.g. newadmin) with Administrator Role
2. Login as 'newadmin'
3. Degrade the old 'admin' user to Role of Subscriber and Save
4. Promote the old 'admin' back to Administrator Role and Save
5. Login as the old 'admin'

If that doesn't work, try:

1. Create a new admin user (e.g. newadmin) with Administrator Role
2. Login as 'newadmin'
3. Delete the old 'admin' user and assign any posts to 'newadmin'
4. Create 'admin' user with Administrator Role
5. Login as 'admin'
6. Delete 'newadmin' user and assign posts to 'admin'

## Why is the wrong author name displayed for a post on a blog? {#why-is-the-wrong-author-name-displayed-for-a-post-on-a-blog}

This problem is usually solved by the same solution as is presented in the question right before this one:  
[Why isn't the admin user listed as an author when editing posts?](https://codex.wordpress.org/FAQ_Troubleshooting#Why_isn.27t_the_admin_user_listed_as_an_author_when_editing_posts.3F)

## An update was just released, so why does my blog not recognize the update is available? {#an-update-was-just-released-so-why-does-my-blog-not-recognize-the-update-is-available}

When an update is released, notification of that release is displayed at the top administration screens saying **WordPress x.x.x is available! Please update now.** Not every blog will see that message at the same time. Your blog is programmed to check for updates every 12 hours, but the timing of that check is purely random. So if your blog just checked for updates minutes before an update was released, you won't see the update message until your blog checks for updates 12 hours later.

If you want your blog to check right now for updates, you can delete the **update_core** option name record in your _wp_options_ table. Note that plugins and themes each have their own check and update cycle, controlled by the records **update_plugins** and **update_themes**, in _wp_options_.

Relevant discussion thread:

* [https://wordpress.org/support/topic/242485](https://wordpress.org/support/topic/242485)

## Why did I lose custom changes to the WordPress Default Theme during the last automatic upgrade? {#why-did-i-lose-custom-changes-to-the-wordpress-default-theme-during-the-last-automatic-upgrade}

A core upgrade copies all the new files from the distribution over the old ones, so if you changed existing files in the WordPress default theme (e.g. _wp-content/themes/twentysixteen/style.css_), those changes got overwritten with the new version of that file.

Please note, a core upgrade goes through a list of "old files", as defined in _wp-admin/includes/update-core.php_, and deletes those files. Any files not on the list, and not in the distribution, are preserved.

**Remember, that before upgrades, whether automatic or manual, both the WordPress Files and database should be backed-up as explained in [WordPress Backups](https://codex.wordpress.org/WordPress%20Backups).**

A better way to modify the default theme is by using a [child theme](https://codex.wordpress.org/Child%20Themes). It's a little more work to set up, but worth the effort because your customizations will be safe when the main theme is updated.

See also:

* [WordPress Backups](https://codex.wordpress.org/WordPress%20Backups)
* [Child Themes](https://codex.wordpress.org/Child%20Themes)

## How do you repair a MySQL database table? {#how-do-you-repair-a-mysql-database-table}

Every once in a while, it may be necessary to repair one or more MySQL database tables. According to the [How to Repair MyISAM Tables at dev.mysql.com](https://dev.mysql.com/doc/refman/5.7/en/myisam-repair.html) there are a number of reasons to repair a table including errors such as "tbl_name.frm is locked against change", "Can't find file tbl_name.MYI (Errcode: nnn)", "Unexpected end of file", "Record file is crashed", or "Got error nnn from table handler".

Here are the steps to repair a table in a MySQL database using [phpMyAdmin](https://codex.wordpress.org/phpMyAdmin):

1. Login to hosting account.
2. Login to [phpMyAdmin](https://codex.wordpress.org/phpMyAdmin).
3. Choose the affected database. If you only have one database, it should choose it by default so you don't need to do anything.
4. In the main panel, you should see a list of your database tables. Check the boxes by the tables that need repair.
5. At the bottom of the window just below the list of tables, there is a drop down menu. Choose "Repair Table"

Remember, that it is advisable to have a current backup of your database at all times.

See also:

* [WordPress Backups](https://codex.wordpress.org/WordPress%20Backups)

## Changelog

- 2023-01-31: Original content from [FAQ Troubleshooting](https://wordpress.org/documentation/article/faq-troubleshooting-2/).