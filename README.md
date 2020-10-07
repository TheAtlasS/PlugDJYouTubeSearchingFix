# PlugDJ YouTube Searching Fix

This will guide you through how to setup this script to run which fixes the YouTube searching function on plug.dj.

1. You'll need to add the extension TamperMonkey (or another userscript manager) you can get it on [Chrome](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=en) or [Firefox](https://addons.mozilla.org/en-US/firefox/addon/tampermonkey/)
2. Open TamperMonkey by clicking on the extension in the top right and clicking on Create a new script ![image1](https://github.com/TheAtlasS/PlugDJYoutubeSearchingFix/blob/main/PlugDJ1.jpg) 
3. You should end up here ![image2](https://github.com/TheAtlasS/PlugDJYoutubeSearchingFix/blob/main/PlugDJ2.jpg) 
4. Copy the code portion and paste it into the console. You can get the code for it [here](#code). When you're finished it should look like this ![image3](https://github.com/TheAtlasS/PlugDJYoutubeSearchingFix/blob/main/PlugDJ3.jpg) 
5. Save the script by clicking file in the top left and then save
6. After saving it should take you to a screen like this just make sure the script is enabled ![image4](https://github.com/TheAtlasS/PlugDJYoutubeSearchingFix/blob/main/PlugDJ4.jpg) 
7. Test that the script is working on your favorite plug.dj channel (plug.dj/itzmasayoshi) 

# Troubleshooting
1. If you are on chrome, make sure that TamperMonkey has access on all sites by right clicking the extension icon then clicking "This can read and and change site data" then "on all sites"
2. Make sure that the script is enabled in TamperMonkey by going to the page shown in step 6 and verifying the enabled option is on

# Code

    // ==UserScript==
    // @name         Plug dj script
    // @namespace    http://tampermonkey.net/
    // @version      0.1
    // @description  update the api key to the one that is stored in localstorage every time the page loads
    // @author       You
    // @include      *plug.dj*
    // @grant        none
    // ==/UserScript==

    /* global $, gapi, API, _, require */
    (function() {
        'use strict';

        function plugReady() {
            return typeof API !== 'undefined' && API.enabled && typeof jQuery !== 'undefined' && typeof require !== 'undefined';
        }

        function init() {
            let apiKey = window.localStorage.getItem('apiKey');
            apiKey = apiKey ? apiKey : 'AIzaSyBcxa-UmtTV-N4KEwKS-rkksA9dNuL4UZE';
            window.gapi.client.setApiKey(apiKey);
        }

        (function autoReload() {
            if (!plugReady()) {
                setTimeout(autoReload, 200);
            } else {
                init();
            }
        })();
    })();
