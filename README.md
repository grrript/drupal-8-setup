# How to set up Drupal 8 on a local environment using Drupal Console  (for Mac OS X).

Updated: 2017 Oct 19

Requirements: Drupal Console Launcher and Composer

## Step 1  - Install Drupal Console Launcher globally

Check if you may have already installed Drupal Console Launcher.

Run this command on the terminal:

<pre><code>drupal self-update</code></pre>

If the command is not recognized, then <code>Drupal Console Launcher</code> has not been installed. 

To intsall, run these commands on the terminal:

<pre><code>curl https://drupalconsole.com/installer -L -o drupal.phar
mv drupal.phar /usr/local/bin/drupal
chmod +x /usr/local/bin/drupal</code></pre>

When finished, run this command on any directory:

<pre><code>drupal</code></pre>

This will list the available commands if <code>Drupal Console Launcher</code> was installed successfully.


## Step 2 - Initialize configuration for Drupal Console

<pre><code>drupal init --override</code></pre>

Follow the prompts.


## Step 3 - Go to your site projects directory

On the terminal, go to the root directory where you create your sites in your local environment. You probably have named this root directory to be <code>'sites'</code> for example. Go to the <code>'sites'</code> directory: 

<pre><code>cd ~/sites</code></pre>


## Step 4  - Install Drupal Console on the Drupal site.

Drupal Console must be installed for EVERY Drupal site.

Run this command on the terminal:

<pre><code>composer create-project drupal-composer/drupal-project:8.x-dev my_site --prefer-dist --no-progress --no-interaction</code></pre>

where <code>my_site</code> is the root folder of the Drupal 8 project you are about to create. You decide what the  project folder name is. 

If you get an error message that composer is not a valid command, then you must install <code>Composer</code> first.

This step will do 2 things: set up the project composer config files (like the composer.json file) and a folder called <code>'web'</code> where the drupal 8 codebase will be saved.

Go the the Drupal project directory: 

<pre><code> cd ~/sites/my_site </code></pre>

where <code>my_site</code> is the project folder name.


## Step 5 - Install the new Drupal site

Under the folder <code>~/sites/my_site</code>, run this command on the terminal:

<pre><code>drupal site:install</code></pre>

Follow the instructions on the screen. You will be asked for database user and password. This is the user name and password for the MYSQL databases (not the credentials for the Drupal site).

This will create a Drupal 8 database on your local MAMP using the db name and user/password you provided when you were prompted these info in the terminal.

This step also creates the database connection info in the <code>sites/default/settings.php</code> file.


## Step 6 - Create a settings.local.php file (optional)

Under the <code>my_site/sites/default</code> folder, create the <code>settings.local.php</code> file:

<pre><code>touch settings.local.php</code></pre>

Remove from <code>settings.php</code>   the following code that starts with <code>$config_directories['sync']</code>:

<pre>
<code><</code><code>?</code><code>php</code>
<code>
$config_directories['sync'] = '../config/sync'; 

$databases['default']['default'] = array (
  'database' => 'enter_a_db_name',
  'username' => 'enter_a_username',
  'password' => 'enter_a_password',
  'prefix' => '',
  'host' => '127.0.0.1',
  'port' => '8889',
  'namespace' => 'Drupal\\Core\\Database\\Driver\\mysql',
  'driver' => 'mysql',
);
$settings['install_profile'] = 'standard';
</code>
</pre>

then paste them into <code>settings.local.php</code>. Note that the <code><?php</code> must appear at the very beginning of the <code>settings.local.php</code> file.

Note: Port number is <code>8889</code> if you are using MAMP. Also, note that database name, username, and password are unique to this Drupal project.


## Step 7 - Then uncomment these lines in the settings.php file:

If you did step 6, then you must uncomment a few lines in the <code>settings.php</code> file by removing <code>'#'</code>: 

<pre><code># if (file_exists($app_root . '/' . $site_path . '/settings.local.php')) {
#   include $app_root . '/' . $site_path . '/settings.local.php';
# }</code></pre>


