# drupal-8-setup  - for Mac

## Step 1  - Install Drupal Console Launcher
Run these commands on the terminal:

<div><code>curl https://drupalconsole.com/installer -L -o drupal.phar</code></div>
<div><code>mv drupal.phar /usr/local/bin/drupal</code></div>
<div><code>chmod +x /usr/local/bin/drupal</code></div>

When finished, run this command:

<code>drupal</code>

to check if the install worked.


## Step 2 - Go to your projects directory

On the terminal, go to the directory where you create your sites in your local environment. Say you create your sites under this directory structure: 

<code>cd ~/sites</code>

## Step 3  - install drupal console

Run this command on the terminal:

<code>composer create-project drupal-composer/drupal-project:8.x-dev my_site --prefer-dist --no-progress --no-interaction</code>

(where 'my_site' is the root folder of the Drupal 8 project you are about to create. You decide what the  project folder name is).


## Step 4 - Go to the root directory of the Drupal site you just created from step 3.

If you used the folder name 'my_site', then run this command on the terminal:

<code> cd ~/sites/my_site </code>


## Step 5 - Install the new Drupal site

Run this command on the terminal:

<code>drupal site:install</code>

Follow the instructions on the screen. You will be asked for database user and password. This is the user name and password for the MYSQL databases (not the credentials for the Drupal site).

This will create a Drupal 8 database on your local MAMP using the db name and user/password you provided when you were prompted these info in the terminal.

This step also creates the database connection info in the settings.php file.


## Step 6 - create a settings.local.php in sites/default folder with the database connection info created in the previous step. It would look like this:

<div><code>$config_directories['sync'] = '../config/sync'; </code></div>
<div><code>$databases['default']['default'] = array (</code></div>
<div><code> 'database' => 'enter_a_db_name',</code></div>
<div><code>  'username' => 'enter_a_username',</code></div>
<div><code>  'password' => 'enter_a_password',</code></div>
<div><code>  'prefix' => '',</code></div>
<div><code>  'host' => '127.0.0.1',</code></div>
<div><code>  'port' => '8889',</code></div>
<div><code>  'namespace' => 'Drupal\\Core\\Database\\Driver\\mysql', </code></div>
<div><code>  'driver' => 'mysql',</code></div>
);
<div><code>$settings['install_profile'] = 'standard';</code></div>

Note: Port number is 8889 if you are using MAMP.


## Step 7 - Then uncomment out this part in the settings.php file:

<div># if (file_exists($app_root . '/' . $site_path . '/settings.local.php')) {</div>
<div>#   include $app_root . '/' . $site_path . '/settings.local.php';</div>
<div># }</div>


