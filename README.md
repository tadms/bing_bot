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


Quick Setup
-----------
In a terminal, simply run the following command in your desired directory:

`curl -sSL https://raw.githubusercontent.com/tadms/bing_bot/master/bin/setup | bash`


Manual Setup
------------
#### Raspberry Pi

1. In a terminal, change to your desired directory to hold the project. <br>
`cd /home/pi`

2. Clone this repository. <br>
`git clone https://github.com/tadms/bing_bot`

3. Ensure that the files under the bin directory are executable. <br>
`chmod -R +x bing_bot/bin/`

4. (Optional) Modify config as desired. <br>
`vim bing_bot/conf/default_conf.json`

5. Change to the bin directory.  
`cd bing_bot/bin`

5. Start up the bing_bot: <br>
`./bing_bot`

6. (Optional) Set up a cron job to run the bing_bot on daily schedule. <br>
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
    	"browser_process_name": "chromium-browser",
    	"log_file_path": "../log/bing_bot.log",
    	"random_words_repo": "https://raw.githubusercontent.com/tadms/random/master/words.json"
    }


Usage
-----
    ./bing_bot                      Start up the bing_bot with defaults
    ./bing_bot -c [config.json]     Start up the bing_bot with a custom config
    ./bing_bot -h                   Display this screen
