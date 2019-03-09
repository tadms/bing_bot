# bing_bot

Overview
--------
Perform a random number of Bing searches, with random search terms, waiting a random
number of seconds between each search.  

Requirements
------------
#### Raspberry Pi
* **Raspbian OS**
  * Browser: Chromium
  * Packages: `jq, curl`  


Setup
-----
#### Raspberry Pi

In a terminal, run the following command in your desired directory:

`curl -sSL https://raw.githubusercontent.com/tadms/bing_bot/master/bin/setup | bash`


#### Credentials / Cookie Setup

The **bing_bot** relies on your Chromium generated cookies to authenticate with Bing.  The value of your Bing cookie request header gets passed to each cURL request.  This value is not stored in clear text on the system.  As a result, some manual steps are required.
1. On your Raspberry Pi, launch the GUI.  

2. Launch the Chromium browser, and manually sign into https://www.bing.com.

3. Once you are successfully signed in, perform a bing search.

4. Ensure that reward points are added to your account successfully.

5. In Chromium, open the Developer Tools (F12) and select the ***Network*** tab.

6. Under the ***Network*** tab, select the ***Headers*** tab.

6. Refresh the page in Chromium.

7. This will create a long list of requests.  Scroll to the top to find the first request, starting with `search?=`.

8. Click on this request to display the HTTP headers.  

9. Under ***Request Headers***, copy the value for `cookie:`.

10. Paste this value into `bing_bot/conf/cookie.txt`. <br>
`vim bing_bot/conf/cookie.txt`


Cron/Schedule Setup
-------------------
(Optional) Set up a cron job to run the **bing_bot** on a daily schedule. <br>
`crontab -e` <br>
`0 2 * * * sleep $(shuf -i 1-3600 -n 1) && /home/pi/bing_bot/bin/bing_bot` <br>
  * *Note:  The `sleep` command is used to randomize the start time.*


Configuration
-------------
The default configuration can be found in `conf/default_conf.json`.

    {
    	"min_seconds_between_searches": "15",
    	"max_seconds_between_searches": "60",
    	"min_amount_of_searches_to_run": "45",
    	"max_amount_of_searches_to_run": "60",
    	"log_file_path": "/var/log/bing_bot/bing_bot.log",
    	"random_words_repo": "https://raw.githubusercontent.com/tadms/random/master/words.json"
    }


Usage
-----
    ./bing_bot                      Start up the bing_bot with defaults
    ./bing_bot -c [config.json]     Start up the bing_bot with a custom config
    ./bing_bot -h                   Display this screen
