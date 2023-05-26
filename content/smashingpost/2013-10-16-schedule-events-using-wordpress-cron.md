---
title: Schedule Events Using WordPress Cron
slug: schedule-events-using-wordpress-cron
image: >-
  https://www.smashingmagazine.com/general/2014/04/09/184620-revision-30/attachment/clock-tower_mini-opt/
date: 2013-10-16T08:45:13.000Z
author: jonathan-goldford
description: >-
  I don’t know about you, but I wake up every morning with at least 10 emails
  that I didn’t have when I went to sleep. While most people probably know that
  these emails aren’t being sent manually by some sleep-deprived, coffee-fuelled
  intern, many people don’t understand **the ins and outs of the systems that
  automate tasks** such as sending email.
categories:
  - WordPress
  - Tools
  - Workflow
  - Techniques (WP)
---
I don’t know about you, but I wake up every morning with at least 10 emails that I didn’t have when I went to sleep. While most people probably know that these emails aren’t being sent manually by some sleep-deprived, coffee-fuelled intern, many people don’t understand the <strong>ins and outs of the systems that automate tasks</strong> such as sending email.

<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff2759f2-bc17-4386-a3bd-3335cae18db1/clock-tower-mini-opt.jpg"><img loading="lazy" decoding="async" loading="lazy" decoding="async" class="109420" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ff2759f2-bc17-4386-a3bd-3335cae18db1/clock-tower-mini-opt.jpg" alt="WordPress Cron" title="Schedule Events Using WordPress Cron" width="500" height="248" /></a><br>
<em>(Image: <a href="https://www.flickr.com/photos/waferboard/7568549198/">Don Schuetze</a>)</em>

That’s where cron and WordPress Cron come into play. But they can be used for far more than filling inboxes to the brim. Before we dive into the specifics of both, here is a quick breakdown of the <strong>topics we’ll cover</strong> below:

*   What is cron and how does WordPress fit into it?
*   Introducing WordPress Cron
*   Limitations of WordPress Cron (and solutions to fix ’em)
*   What tasks is WordPress Cron used for?
*   How does WordPress execute scheduled tasks?
*   How to schedule tasks through WordPress Cron
*   Tips for developing with WordPress Cron
*   Popular plugins that use WordPress Cron

Still interested? Let’s get to it.

{{% feature-panel %}}

## What Is Cron And How Does WordPress Fit Into It?

Cron is a system originally built for UNIX that enables users to execute commands, programs and other actions at specified times. As Wikipedia so eloquently puts it, “<strong>Cron is a time-based job scheduler</strong>.”

## <span class="rh">Further Reading</span> on SmashingMag:

*   [How To Harness The Machines: Being Productive With Task Runners](https://www.smashingmagazine.com/2016/06/harness-machines-productive-task-runners/)
*   [<span class="headline">How To Fix The Web: Obscure Back-End Techniques And Terminal Secrets</span>](https://www.smashingmagazine.com/2013/07/how-to-fix-the-web-obscure-back-end-techniques-and-terminal-secrets/)
*   [10 Useful WordPress Hook Hacks](https://www.smashingmagazine.com/2009/08/10-useful-wordpress-hook-hacks/)
*   [A Simple Workflow From Development To Deployment](https://www.smashingmagazine.com/2015/07/development-to-deployment-workflow/)

Basically, what that means is you can schedule an action to take place at a specific time, without having to manually execute code at that time. But how does this relate to your website — particularly, your WordPress website? Setting up your WordPress website to use the UNIX cron system built into your server’s operating system is possible; however, it can be difficult for two main reasons:

1.  Your host might not permit you to set up cron for security reasons.
2.  Different servers might require cron to be set up in different ways, which would require familiarity with a wide variety of systems.

If the WordPress team couldn’t rely on using each server’s cron, then how did they schedule tasks to be performed? They built WordPress Cron.</p>

## Introducing WordPress Cron

WordPress Cron is what many people refer to as a “pseudo-cron system.” The difference is in how UNIX cron and WordPress Cron take action. A typical UNIX cron system runs in this order:

1.  A time tied to an action occurs.
2.  Cron runs the action tied to that time.

With WordPress Cron, it works a little differently:

1.  A visitor comes to any page on your WordPress website.
2.  WordPress Cron checks each cron event to see whether the scheduled time has passed.
3.  If the scheduled time for that event has passed, then WordPress Cron executes any actions tied to that event.</p>

## Limitations Of WordPress Cron (And Solutions To Fix ’Em)

You may be wondering, “What happens if no one visits my website at all? Does WordPress Cron not run?” The biggest limitation of WordPress Cron stems from its inability to run without visitors. This leads to a few potential issues.</p>

### WordPress Cron Is Imprecise (Zero Visits = Zero Cron Runs)

If you’ve scheduled an email to be sent at 2:00 pm on Monday, then the email likely wouldn’t be sent precisely at that time, unless your website received a visit at exactly 2:00 pm. Instead, the email would be sent at the time of the first visit after 2:00 pm.

In most cases, this has little impact. But what if the email was a reminder for an event the next day, Tuesday? If the next visitor came on Tuesday night, then the email would likely serve no benefit, and could possibly confuse visitors.

So, consider the impact of no visits. If a website gets no traffic at all, then WordPress Cron will never run.

The solution is to <strong>create a more precise cron system</strong>.

If your website requires the timing to be exact, you could follow one of two methods. You could set up your server’s cron to hit <code>wp-cron.php</code> at a regular interval by following the instructions outlined in <a href="https://wp.tutsplus.com/articles/insights-into-wp-cron-an-introduction-to-scheduling-tasks-in-wordpress/">Harish Chouhan’s article on Wptuts+</a>. If this seems overly complicated, you could use a tool such as <a href="https://www.pingdom.com/">Pingdom</a> to trigger an HTTP request directly to <code>wp-cron.php</code>.</p>

### Running Heavy Processes Could Slow Down Your Website

Similar to running any heavy process on page load, WordPress Cron could slow down your website significantly for the visitor who triggers a heavy process tied to a scheduled event.

The solution is to <strong>keep WordPress Cron actions simple</strong>.

Especially if you run actions frequently, keep the actions tied to scheduled cron events as simple as possible. Every extra ounce of complexity will hinder the performance for your end users.</p>

## What Tasks Is WordPress Cron Used For?

We’ve covered what WordPress Cron is and what its limitations are. Now it’s time to discuss what it’s actually used for. WordPress Cron can be employed to schedule two types of hooks:

*   those to execute at a regular, repeating interval;
*   those to execute only once at a fixed time.</p>

### Examples of Tasks Scheduled at a Regular, Repeating Interval

WordPress’ core and a number of plugins use WordPress Cron to execute the following tasks at regular, repeating intervals:

*   backing up the website,
*   checking the WordPress version to ensure it’s up to date,
*   checking for updates to plugins and themes,
*   optimizing the database to improve performance.</p>

### Examples of Tasks Scheduled to Run Only Once at a Fixed Time

Single events that occur only once are used for actions such as:

*   publishing a blog post at a specific time,
*   sending an email at a specific time.</p>

## How Does WordPress Execute Scheduled Tasks?

Before jumping into how to schedule your own events, it might be helpful to understand how WordPress Cron operates. WordPress Cron runs using two files:

*   `/wp-includes/cron.php` This file contains the entire WordPress Cron API and the functions you’ll need to schedule events.
*   `/wp-cron.php` This file actually executes WordPress Cron and calls the hooks attached to the scheduled events. This file is loaded through the [spawn_cron()](https://codex.wordpress.org/Function_Reference/spawn_cron) function in `cron.php`.

We’ve got the files now, but what happens when a WordPress page loads? We’ll walk through the process here together (but it’s worth having a solid understanding of <a href="https://www.smashingmagazine.com/2012/02/16/inside-wordpress-actions-filters/">hooks and filters</a> before going through it):

1.  A visitor requests a page on your website.
2.  In `/wp-includes/default-filters.php`, WordPress hooks the `wp_cron()` function to the `init` action.
3.  When the `init` action occurs in `/wp-settings.php`, `wp_cron()` runs.
4.  The `wp_cron()` function ensures that WordPress Cron is not disabled and that the earliest scheduled cron event has passed its execution time.
5.  If it has passed its execution time, then `spawn_cron()` runs and first checks whether we’re already carrying out cron and, if so, doesn’t run it again.

        if ( defined('DOING_CRON') || isset($_GET['doing_wp_cron']) )
          return;

6.  Starting on line 247 of `cron.php`, `spawn_cron()` loads `wp-cron.php` through the HTTP request. (Using `wp_remote_post()` to load `wp-cron.php` doesn’t prevent the remainder of the page from loading for the visitor.)

        $cron_request = apply_filters( 'cron_request', array(
          'url' => site_url( 'wp-cron.php?doing_wp_cron=' . $doing_wp_cron ),
          'key' => $doing_wp_cron,
          'args' => array( 'timeout' => 0.01, 'blocking' => false, 'sslverify' => apply_filters( 'https_local_ssl_verify', true ) )
        ) );

        wp_remote_post( $cron_request['url'], $cron_request['args'] );

7.  The `wp-cron.php` file loads and loops through all of the scheduled cron events, doing the following:
    *   **Line 85**.  If the event is on a recurring schedule, then WordPress runs [wp_reschedule_event()](https://codex.wordpress.org/Function_Reference/wp_reschedule_event) to schedule the next occurrence of this event.
    *   **Line 90**.  WordPress unschedules the current event, using [wp_unschedule_event()](https://codex.wordpress.org/Function_Reference/wp_unschedule_event), so that it doesn’t run again in the future.
    *   **Line 92**.  WordPress runs all of the functions tied to the hook provided in the cron event, including all of the actions that were scheduled to run at this second or prior to this second, using [do_action_ref_array()](https://codex.wordpress.org/Function_Reference/do_action_ref_array).

        foreach ( $crons as $timestamp => $cronhooks ) {
          if ( $timestamp > $gmt_time )
            break;

          foreach ( $cronhooks as $hook => $keys ) {

            foreach ( $keys as $k => $v ) {

              $schedule = $v['schedule'];

              if ( $schedule != false ) {
                $new_args = array($timestamp, $schedule, $hook, $v['args']);
                call_user_func_array('wp_reschedule_event', $new_args);
              }

              wp_unschedule_event( $timestamp, $hook, $v['args'] );

              do_action_ref_array( $hook, $v['args'] );

              // If the hook ran too long and another cron process stole the lock, quit.
              if ( _get_cron_lock() != $doing_wp_cron )
                return;
            }
          }
        }

As is the case with a lot of the WordPress source code, the process is organized in a way that makes it fairly easy to follow. I encourage you to look at the code yourself in both <code>cron.php</code> and <code>wp-cron.php</code> to learn more.</p>

## How To Schedule Tasks Through WordPress Cron?

If you’ve made it this far, then we can finally turn our attention to how to use WordPress Cron in our own plugins.</p>

### Create Recurring Events in WordPress Cron

Creating an event that repeats on a fixed schedule is done using <a href="https://codex.wordpress.org/Function_Reference/wp_schedule_event">wp_schedule_event( $timestamp, $recurrence, $hook, $args )</a>, in which the following four parameters are used:

*   `$timestamp` (required: integer) This is the time when you want the event to occur. This must be in a UNIX timestamp and must be in GMT. If you’re using local time, then convert it to GMT first or else the event won’t fire at the correct time.
*   `$recurrence` (required: string) This is how often the event should occur. The default options are `hourly`, `twicedaily` or `daily`. You can also add your own options, which we’ll touch on shortly.
*   `$hook` (required: string) This is the name of the action hook you’d like to execute. The advantage of calling an action hook instead of a function directly is that you can tie multiple functions to one hook using [add_action()](https://codex.wordpress.org/Function_Reference/add_action).
*   `$args` (optional: array) These are any arguments you want to pass to the hooked function or functions. This could be a post ID, a backup schedule ID, a user ID or any other information you’ll use in your functions.

Let’s say we built a plugin that backs up the WordPress database once a day. Here’s what the code would look like if we were to schedule the backup with WordPress Cron:

<pre><code class="language-php">
//On plugin activation schedule our daily database backup
register_activation_hook( __FILE__, 'wi_create_daily_backup_schedule' );
function wi_create_daily_backup_schedule(){
  //Use wp_next_scheduled to check if the event is already scheduled
  $timestamp = wp_next_scheduled( 'wi_create_daily_backup' );

  //If $timestamp == false schedule daily backups since it hasn't been done previously
  if( $timestamp == false ){
    //Schedule the event for right now, then to repeat daily using the hook 'wi_create_daily_backup'
    wp_schedule_event( time(), 'daily', 'wi_create_daily_backup' );
  }
}

//Hook our function , wi_create_backup(), into the action wi_create_daily_backup
add_action( 'wi_create_daily_backup', 'wi_create_backup' );
function wi_create_backup(){
  //Run code to create backup.
}
</code></pre>

To start, we hook <code>wi_create_daily_backup_schedule()</code> to <code>register_activation_hook()</code> so that our cron backup event will be added immediately when the plugin is activated. In <code>wi_create_daily_backup_schedule()</code>, we do two things:

1.  We use [wp_next_scheduled()](https://codex.wordpress.org/Function_Reference/wp_next_scheduled) to check whether our cron event has already been created. And `wp_next_scheduled()` will either return a timestamp of the next scheduled event for a hook (`wi_create_daily_backup`) or return `false`, telling us that our cron event is not scheduled.
2.  If `$timestamp == false`, then we schedule our cron event for daily backups. We schedule the first backup to happen immediately by using the PHP function `time()`, and then we pass the `daily` recurrence schedule and our `wi_create_daily_backup` hook.

After creating the scheduled event, all that’s left to do is tie our backup function to the <code>wi_create_backup</code> action. We use <code>add_action( 'wi_create_daily_backup', 'wi_create_backup' )</code> to hook our function. Then, we write our <code>wi_create_backup()</code> function to generate a backup of the website.</p>

### Adding a New WordPress Cron Schedule

As I mentioned when discussing recurring events, the default options for recurring schedules are <code>hourly</code>, <code>twicedaily</code> and <code>daily</code>. But <strong>what if, instead of running our backup daily, we wanted to run it weekly?</strong> WordPress makes a weekly schedule easy with the <code>cron_schedules</code> filter. To make the schedule weekly, you’d write the following code in your plugin:

<pre><code class="language-php">
add_filter( 'cron_schedules', 'wi_add_weekly_schedule' );
function wi_add_weekly_schedule( $schedules ) {
  $schedules['weekly'] = array(
    'interval' =&gt; 7 * 24 * 60 * 60, //7 days * 24 hours * 60 minutes * 60 seconds
    'display' =&gt; __( 'Once Weekly', 'my-plugin-domain' )
  );
  /*
  You could add another schedule by creating an additional array element
  $schedules['biweekly'] = array(
    'interval' =&gt; 7 * 24 * 60 * 60 * 2
    'display' =&gt; __( 'Every Other Week', 'my-plugin-domain' )
  );
  */

  return $schedules;
}
</code></pre>

The <code>$schedules</code> array is passed into our function and enables us to add the <code>weekly</code> key with the desired schedule. For the <code>interval</code> key, we must include the number of seconds we’d like between the times this cron event runs. To run once weekly, we calculate 7 days × 24 hours × 60 minutes × 60 seconds to give us the total number of seconds in a week. Then, we create the display name, “Once Weekly,” in case others need to read a description of our schedule.

Don’t forget to <strong>localize your description</strong> using <a href="https://codex.wordpress.org/Function_Reference/_2">__()</a>, so that it can be translated later. If you’re interested in adding more than one schedule, simply create a new array key within <code>$schedules</code>, such as <code>$schedules[‘biweekly’]</code>, and add the interval and description. To complete our function, we return the <code>$schedules</code> array, including our new schedule.

Looking at the previous example of our backup schedule, if we wanted it to run weekly, we’d simply take this:

<pre><code class="language-php">
wp_schedule_event( time(), <strong>'daily'</strong>, 'wi_create_daily_backup' );
</code></pre>

And we’d change it to this, using the new <code>weekly</code> schedule we created:

<pre><code class="language-php">
wp_schedule_event( time(), <strong>'weekly'</strong>, 'wi_create_daily_backup' );
</code></pre>

Now, our backup will run once a week.</p>

### Removing Scheduled Cron Events

Returning to our backup plugin example, what we’ve done so far does have one problem. We haven’t removed our scheduled backup event upon deactivation of the plugin. This won’t actually cause an error when the event executes daily, but it will force cron to run, possibly slowing down the website ever so slightly. Removing our scheduled event is easy.

<pre><code class="language-php">
register_deactivation_hook( __FILE__, 'wi_remove_daily_backup_schedule' );
function wi_remove_daily_backup_schedule(){
  wp_clear_scheduled_hook( 'wi_create_daily_backup' );
}
</code></pre>

Very much like we did on activation, we hook a function, <code>wi_remove_daily_backup_schedule()</code>, to the deactivation of our plugin. We pass the event hook <code>wi_create_daily_backup</code> to <a href="https://codex.wordpress.org/Function_Reference/wp_clear_scheduled_hook">wp_clear_scheduled_hook()</a>, and then the schedule will be removed from WordPress Cron.

It’s worth noting that <code>wp_clear_scheduled_hook()</code> will remove all events associated with that hook. If you want to remove only one event, then use <a href="https://codex.wordpress.org/Function_Reference/wp_unschedule_event">wp_unschedule_event()</a> instead; this function requires that you pass in the timestamp of the event you wish to remove.</p>

### Create a Single Event in WordPress Cron

Creating a single event to occur at a specified time is sometimes required. To create a single event in WordPress Cron, we must use <a href="https://codex.wordpress.org/Function_Reference/wp_schedule_single_event">wp_schedule_single_event( $timestamp, $hook, $args )</a>. The parameters here are exactly the same as <code>wp_schedule_event()</code>, except that they don’t include the <code>$recurrence</code> parameter, thus allowing the event to occur only once.

Let’s say we want to send a reminder email for a volunteer activity that will happen in the future. You can use this code directly inside a function run when the post about the volunteer activity is saved in WordPress’ admin section.

<pre><code class="language-php">
//Convert start time from local time to GMT since WP Cron sends based on GMT
$start_time_gmt = strtotime( get_gmt_from_date( date( 'Y-m-d H:i:s', $start_time ) ) . ' GMT' );

//Set reminder time for three days before event start time
$time_prior_event = 3 * 24 * 60 * 60; //3 days * 24 hours * 60 minutes * 60 seconds
$reminder_time = $start_time_gmt - $time_prior_event;

//Remove existing cron event for this post if one exists
//We pass $post_id because cron event arguments are required to remove the scheduled event
wp_clear_scheduled_hook( 'wi_send_reminder_email', array( $post_id ) );

//Schedule the reminder
wp_schedule_single_event( $reminder_time, 'wi_send_reminder_email', array( $post_id ) );
//...
</code></pre>

<strong>In this code, a number of important steps are happening.</strong> First, if the time of the volunteer activity is stored in a variable in local time, then we have to convert it to GMT, because WordPress Cron is not run using local time. Once converted to the variable <code>$start_time_gmt</code>, we set <code>$reminder_time</code> to the volunteer activity’s start time minus the number of seconds prior to the event that we wish to send the email.

We then remove any scheduled events for this hook and post to avoid scheduling our event multiple times when the post is saved. Remember that you must pass an array, including the same arguments that you used to create the scheduled event, in order to remove it. In this case, we’re passing the post’s ID. This makes sense, after all. You want to remove the scheduled email reminder not for every volunteer activity, only for the one that the user is saving.

Once we’ve created the reminder time and cleared any previously scheduled events, we create the new event using <code>wp_schedule_single_event()</code>, with the timestamp <code>$reminder_time</code>. We also pass in the <code>$post_id</code> for this particular post so that we can include custom information in our email, such as the post’s title, the time of the activity, the description of the activity and any other information.

To actually send the email when the cron event occurs, we hook the function that we want to execute when the event fires to <code>wi_send_reminder_email</code>.

<pre><code class="language-php">
//Hook our function, wi_send_event_reminder_email(), into the action wi_send_reminder_email
add_action( 'wi_send_reminder_email', 'wi_send_event_reminder_email' );
function wi_send_event_reminder_email( $post_id ){
  //Run code to send reminder email, customizing based on the post id
}
</code></pre>

## Tips For Developing With WordPress Cron

When you code with WordPress Cron, a couple of tools in particular could really help your development process.</p>

### WP Crontrol

<a href="https://wordpress.org/plugins/wp-crontrol/">WP Crontrol</a> is a WordPress plugin that helps you develop using the WordPress Cron API. It displays all scheduled cron events, enables you to edit, run or delete cron events using a GUI and also enables you to see all available cron schedules.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="109413" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75b7c0f8-f790-4939-91ad-5592eb3fa093/wp-crontrol-mini.jpg" alt="WP-Crontrol" width="500" height="197" /><br>
<em>The admin interface of WP Crontrol.</em>

I highly recommend WP Crontrol if you plan to use the WordPress Cron API in a plugin.</p>

### IDE Debugger

If you develop plugins using an integrated development environment (IDE) instead of a basic text editor, then a debugger can be a hugely helpful resource for reviewing the array of cron events and creating new events. If you’re not already using an IDE, two of the most popular are <a href="https://projects.eclipse.org/projects/tools.pdt">Eclipse</a> and <a href="https://netbeans.org/">NetBeans</a>, but plenty more are out there to choose from.</p>

## Examples Of WordPress Cron Used In Popular Plugins

The WordPress Cron API is used often in popular plugins across the WordPress platform. To give you a feel for its use, I’ll cover how two rather popular plugins employ the API.</p>

### Akismet

<a href="https://wordpress.org/plugins/akismet/">Akismet</a> is the leading spam-prevention tool for WordPress. At the time of writing, it’s been downloaded over 14 million times.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="109412" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f239164f-1efa-45ca-af5c-84ff7e7aa54c/akismet-mini.jpg" alt="Akismet" width="500" height="162" />

Akismet uses the WordPress Cron API for a number of purposes, including:

*   Rechecking in the future whether a comment is spam in the event that Akismet’s servers are unreachable during a check;
*   Rechecking an Akismet API key if the plugin is unable to verify at that moment due to an unreachable server;
*   Deleting old spam comments on a regular basis;

To delete old spam comments, Akismet creates a daily event and deletes comments over a certain age every day.

<pre><code class="language-php">
if ( function_exists('wp_next_scheduled') &amp;&amp; function_exists('wp_schedule_event') ) {
  // WP 2.1+: delete old comments daily
  if ( !wp_next_scheduled('akismet_scheduled_delete') )
    wp_schedule_event(time(), 'daily', 'akismet_scheduled_delete');
}
</code></pre>

### Broken Link Checker

  return $schedules;
}
</code></pre>

The <code>$schedules</code> array is passed into our function and enables us to add the <code>weekly</code> key with the desired schedule. For the <code>interval</code> key, we must include the number of seconds we’d like between the times this cron event runs. To run once weekly, we calculate 7 days × 24 hours × 60 minutes × 60 seconds to give us the total number of seconds in a week. Then, we create the display name, “Once Weekly,” in case others need to read a description of our schedule.

Don’t forget to <strong>localize your description</strong> using <a href="https://codex.wordpress.org/Function_Reference/_2">__()</a>, so that it can be translated later. If you’re interested in adding more than one schedule, simply create a new array key within <code>$schedules</code>, such as <code>$schedules[‘biweekly’]</code>, and add the interval and description. To complete our function, we return the <code>$schedules</code> array, including our new schedule.

Looking at the previous example of our backup schedule, if we wanted it to run weekly, we’d simply take this:

<pre><code class="language-php">
wp_schedule_event( time(), <strong>'daily'</strong>, 'wi_create_daily_backup' );
</code></pre>

And we’d change it to this, using the new <code>weekly</code> schedule we created:

<pre><code class="language-php">
wp_schedule_event( time(), <strong>'weekly'</strong>, 'wi_create_daily_backup' );
</code></pre>

Now, our backup will run once a week.</p>

### Removing Scheduled Cron Events

Returning to our backup plugin example, what we’ve done so far does have one problem. We haven’t removed our scheduled backup event upon deactivation of the plugin. This won’t actually cause an error when the event executes daily, but it will force cron to run, possibly slowing down the website ever so slightly. Removing our scheduled event is easy.

<pre><code class="language-php">
register_deactivation_hook( __FILE__, 'wi_remove_daily_backup_schedule' );
function wi_remove_daily_backup_schedule(){
  wp_clear_scheduled_hook( 'wi_create_daily_backup' );
}
</code></pre>

Very much like we did on activation, we hook a function, <code>wi_remove_daily_backup_schedule()</code>, to the deactivation of our plugin. We pass the event hook <code>wi_create_daily_backup</code> to <a href="https://codex.wordpress.org/Function_Reference/wp_clear_scheduled_hook">wp_clear_scheduled_hook()</a>, and then the schedule will be removed from WordPress Cron.

It’s worth noting that <code>wp_clear_scheduled_hook()</code> will remove all events associated with that hook. If you want to remove only one event, then use <a href="https://codex.wordpress.org/Function_Reference/wp_unschedule_event">wp_unschedule_event()</a> instead; this function requires that you pass in the timestamp of the event you wish to remove.</p>

### Create a Single Event in WordPress Cron

Creating a single event to occur at a specified time is sometimes required. To create a single event in WordPress Cron, we must use <a href="https://codex.wordpress.org/Function_Reference/wp_schedule_single_event">wp_schedule_single_event( $timestamp, $hook, $args )</a>. The parameters here are exactly the same as <code>wp_schedule_event()</code>, except that they don’t include the <code>$recurrence</code> parameter, thus allowing the event to occur only once.

Let’s say we want to send a reminder email for a volunteer activity that will happen in the future. You can use this code directly inside a function run when the post about the volunteer activity is saved in WordPress’ admin section.

<pre><code class="language-php">
//Convert start time from local time to GMT since WP Cron sends based on GMT
$start_time_gmt = strtotime( get_gmt_from_date( date( 'Y-m-d H:i:s', $start_time ) ) . ' GMT' );

//Set reminder time for three days before event start time
$time_prior_event = 3 * 24 * 60 * 60; //3 days * 24 hours * 60 minutes * 60 seconds
$reminder_time = $start_time_gmt - $time_prior_event;

//Remove existing cron event for this post if one exists
//We pass $post_id because cron event arguments are required to remove the scheduled event
wp_clear_scheduled_hook( 'wi_send_reminder_email', array( $post_id ) );

//Schedule the reminder
wp_schedule_single_event( $reminder_time, 'wi_send_reminder_email', array( $post_id ) );
//...
</code></pre>

<strong>In this code, a number of important steps are happening.</strong> First, if the time of the volunteer activity is stored in a variable in local time, then we have to convert it to GMT, because WordPress Cron is not run using local time. Once converted to the variable <code>$start_time_gmt</code>, we set <code>$reminder_time</code> to the volunteer activity’s start time minus the number of seconds prior to the event that we wish to send the email.

We then remove any scheduled events for this hook and post to avoid scheduling our event multiple times when the post is saved. Remember that you must pass an array, including the same arguments that you used to create the scheduled event, in order to remove it. In this case, we’re passing the post’s ID. This makes sense, after all. You want to remove the scheduled email reminder not for every volunteer activity, only for the one that the user is saving.

Once we’ve created the reminder time and cleared any previously scheduled events, we create the new event using <code>wp_schedule_single_event()</code>, with the timestamp <code>$reminder_time</code>. We also pass in the <code>$post_id</code> for this particular post so that we can include custom information in our email, such as the post’s title, the time of the activity, the description of the activity and any other information.

To actually send the email when the cron event occurs, we hook the function that we want to execute when the event fires to <code>wi_send_reminder_email</code>.

<pre><code class="language-php">
//Hook our function, wi_send_event_reminder_email(), into the action wi_send_reminder_email
add_action( 'wi_send_reminder_email', 'wi_send_event_reminder_email' );
function wi_send_event_reminder_email( $post_id ){
  //Run code to send reminder email, customizing based on the post id
}
</code></pre>

## Tips For Developing With WordPress Cron

When you code with WordPress Cron, a couple of tools in particular could really help your development process.</p>

### WP Crontrol

<a href="https://wordpress.org/plugins/wp-crontrol/">WP Crontrol</a> is a WordPress plugin that helps you develop using the WordPress Cron API. It displays all scheduled cron events, enables you to edit, run or delete cron events using a GUI and also enables you to see all available cron schedules.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="109413" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/75b7c0f8-f790-4939-91ad-5592eb3fa093/wp-crontrol-mini.jpg" alt="WP-Crontrol" width="500" height="197" /><br>
<em>The admin interface of WP Crontrol.</em>

I highly recommend WP Crontrol if you plan to use the WordPress Cron API in a plugin.</p>

### IDE Debugger

If you develop plugins using an integrated development environment (IDE) instead of a basic text editor, then a debugger can be a hugely helpful resource for reviewing the array of cron events and creating new events. If you’re not already using an IDE, two of the most popular are <a href="https://projects.eclipse.org/projects/tools.pdt">Eclipse</a> and <a href="https://netbeans.org/">NetBeans</a>, but plenty more are out there to choose from.</p>

## Examples Of WordPress Cron Used In Popular Plugins

The WordPress Cron API is used often in popular plugins across the WordPress platform. To give you a feel for its use, I’ll cover how two rather popular plugins employ the API.</p>

### Akismet

<a href="https://wordpress.org/plugins/akismet/">Akismet</a> is the leading spam-prevention tool for WordPress. At the time of writing, it’s been downloaded over 14 million times.

<img loading="lazy" decoding="async" loading="lazy" decoding="async" class="109412" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f239164f-1efa-45ca-af5c-84ff7e7aa54c/akismet-mini.jpg" alt="Akismet" width="500" height="162" />

Akismet uses the WordPress Cron API for a number of purposes, including:

*   Rechecking in the future whether a comment is spam in the event that Akismet’s servers are unreachable during a check;
*   Rechecking an Akismet API key if the plugin is unable to verify at that moment due to an unreachable server;
*   Deleting old spam comments on a regular basis;

To delete old spam comments, Akismet creates a daily event and deletes comments over a certain age every day.

<pre><code class="language-php">
if ( function_exists('wp_next_scheduled') &amp;&amp; function_exists('wp_schedule_event') ) {
  // WP 2.1+: delete old comments daily
  if ( !wp_next_scheduled('akismet_scheduled_delete') )
    wp_schedule_event(time(), 'daily', 'akismet_scheduled_delete');
}
</code></pre>

### Broken Link Checker

<a href="https://wordpress.org/plugins/broken-link-checker/">Broken Link Checker</a> is a WordPress plugin that checks your entire website for broken links. It uses WordPress Cron for a number of regular activities, including:

*   Checking new links hourly to ensure they’re not broken,
*   Emailing notifications about broken links on the website,
*   Completing database maintenance every two months,
*   Updating news about the plugin every day,

Broken Link Checker creates each of these schedules through one function, <code>setup_cron_events()</code>.

<pre><code class="language-php">
/**
* Install or uninstall the plugin's Cron events based on current settings.
*
* @uses wsBrokenLinkChecker::$conf Uses $conf-&gt;options to determine if events need to be (un)installed.
*
* @return void
*/
function setup_cron_events(){
  //Link monitor
  if ( $this-&gt;conf-&gt;options['run_via_cron'] ){
    if (!wp_next_scheduled('blc_cron_check_links')) {
      wp_schedule_event( time(), 'hourly', 'blc_cron_check_links' );
    }
  } else {
    wp_clear_scheduled_hook('blc_cron_check_links');
  }

  //Email notifications about broken links
  if ( $this-&gt;conf-&gt;options['send_email_notifications'] || $this-&gt;conf-&gt;options['send_authors_email_notifications'] ){
    if ( !wp_next_scheduled('blc_cron_email_notifications') ){
      wp_schedule_event(time(), $this-&gt;conf-&gt;options['notification_schedule'], 'blc_cron_email_notifications');
    }
  } else {
    wp_clear_scheduled_hook('blc_cron_email_notifications');
  }

  //Run database maintenance every two weeks or so
  if ( !wp_next_scheduled('blc_cron_database_maintenance') ){
    wp_schedule_event(time(), 'bimonthly', 'blc_cron_database_maintenance');
  }

  //Check for news notices related to this plugin
  if ( !wp_next_scheduled('blc_cron_check_news') ){
    wp_schedule_event(time(), 'daily', 'blc_cron_check_news');
  }
}
</code></pre>

## Conclusion

By now, you’re probably croned out, but I’m glad you stuck with me. You should now have a solid understanding of what WordPress Cron is, how it works and how you can use it to automate different features and functionality in your plugin.

If you have experience with WordPress Cron or have just started playing around, I’d love to hear from you in the comments. What issues have you run into? What are you using it for? Any tips for speeding up development? Do you know of any plugins that use the WordPress Cron API in an innovative way?

<em>(al ea)</em>

