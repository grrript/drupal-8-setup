# How to set up Drupal 8 on a local environment using Drupal Console  (for Mac OS X).

Requirements: Drupal Console Launcher and Composer

## Step 1  - Install Drupal Console Launcher globally
Run these commands on the terminal:

<pre><code>curl https://drupalconsole.com/installer -L -o drupal.phar
mv drupal.phar /usr/local/bin/drupal
chmod +x /usr/local/bin/drupal</code></pre>

When finished, run this command on any directory:

<pre><code>drupal</code></pre>

This will list the available commands.


## Step 2 - Initialize configuration for Drupal Console

<pre><code>drupal init --override</code></pre>

Follow the prompts.


## Step 3 - Go to your projects directory

On the terminal, go to the root directory where you create your sites in your local environment. This root directory could be named <code>'sites'</code> for example. So run this command: 

<pre><code>cd ~/sites</code></pre>


## Step 4  - Install drupal console on the Drupal site.

Drupal console must be installed for EVERY Drupal site.

Run this command on the terminal:

<pre><code>composer create-project drupal-composer/drupal-project:8.x-dev my_site --prefer-dist --no-progress --no-interaction</code></pre>

where <code>my_site</code> is the root folder of the Drupal 8 project you are about to create. You decide what the  project folder name is. This step will set up the project composer config files and a folder called <code>'web'</code> where the drupal 8 codebase will be saved.

Then run this command: 

<pre><code> cd ~/sites/my_site </code></pre>

where <code>my_site</code> is the project folder name.


## Step 5 - Install the new Drupal site

Under the folder <code>~/sites/my_site</code>, run this command on the terminal:

<pre><code>drupal site:install</code></pre>

Follow the instructions on the screen. You will be asked for database user and password. This is the user name and password for the MYSQL databases (not the credentials for the Drupal site).

This will create a Drupal 8 database on your local MAMP using the db name and user/password you provided when you were prompted these info in the terminal.

This step also creates the database connection info in the <code>sites/default/settings.php</code> file.


## Step 6 - Create a settings.local.php file (optional)

Under the <code>sites/default</code> folder, create the <code>settings.local.php</code> file:

<pre><code>touch settings.local.php</code></pre>

Copy from <code>settings.php</code>   the folowing (using the database connection info created in the previous step):

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

then paste them into <code>settings.local.php</code>.

Note: Port number is <code>8889</code> if you are using MAMP. Also, note database name, username, and password are unique to this Drupal project.


## Step 7 - Then uncomment these lines in the settings.php file:

<pre><code># if (file_exists($app_root . '/' . $site_path . '/settings.local.php')) {
#   include $app_root . '/' . $site_path . '/settings.local.php';
# }</code></pre>


