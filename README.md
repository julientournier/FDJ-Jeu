Franchise Management Heroku Game
================================

HTML5 node.js mobile app game. Developed from [Cloudspokes Challenge](http://www.cloudspokes.com/challenges/1536).

Original demo: http://cheezburger.herokuapp.com


## How do I get this working for *my* DiscoDonuts org?

* Spin up a copy from the latest dot.
* Create a folder to hold this in.
* Pull down the code using `git clone https://github.com/cowie/FM-Heroku.git MyFolder`
* Go into the folder, adjust the file `/conf/config.json` with your login credentials. You'll get the first three items from `Setup->Develop->Remote Access->Cheezburger` 
        Client ID = Consumer Key
        Client Secret = Consumer Secret
        Callback = Callback URL
You'll get the next two from your username/password. To reset/get your security token (NEEDED), you'll need to go to `Setup->My Personal Information->Reset my Security Token' Put your pasword and token in together, like this: `SecretPassword123SUPERCRAZYTOKEN320432423423432`

* Back in your terminal, run the following

    `heroku create`
    `git add .`
    `git commit -m "This is awesome"`
    `git push heroku master`
    
## That's cool, but I'm not serving cheezburgers to cats, what do I do?

* Do what I said above, through the step where you adjusted login credentials.
* Change the following elements as needed
* Images
    *Falling Burger: `/web/img/burger.png (DONT RENAME)`
    
    *Catching Cat: `/web/img/cat.png (SRS, DONT RENAME)`
    
    *Background: `/web/img/red-bg.jpg (Totally rename. JUST KIDDING DONT RENAME)`
    
* Titles/etc: Index.html, you'll probably want sse help here.

    Line 8: Title of app/page
    
    Line 19: Actual header on page
    
    Line 34: Instructions line
    

Cheezburger
==========

HTML5 mobile web app game powered by Heroku and Salesforce

This is an entry for [a CloudSpokes challenge](http://www.cloudspokes.com/challenges/1536).

Live presentation: http://cheezburger.herokuapp.com

## Features

* Our favorite cheezburger cat meme is finally arrived as a mobile game!
* Game can be opened right from mobile browser (iPhone users should add it to their home screen for maximum experience, and
there are in-game instructions for this)
* Using Geolocation API for locating the nearest franchise location from salesforce records, score is submitted specifically to that store
* Using W3C motion API for controlling the game (tilting the phone)
* All kind of crazy CSS transforms
* Using cache manifest for fast loading
* Leaderboard/High Score based on specific store location
* Tested on iPhone 4S, and Samsung Galaxy S2

## Configuration

* `conf/config.json` contains all salesforce related OAuth2 credentials you need for basic setup
(You need to generate OAuth credentials in database.com, under the menu Develop -> Remote Access, and copy the client ID,
secret and callback fields to the config. For username use your username, for passwordAndToken use your password +
a token generated by My Personal Information -> Reset My Security Token)
* If you need to modify backend logic (for example you need a bit different database.com fields, etc.), it's very straightforward in
the `/lib/salesforce-connector.js` file (it is using the `node-salesforce` library to connect to Salesforce)
* If you want to customize the UI, you will find the css/images in the `/web` directory

## Run locally

* Install necessary node.js libraries with `npm install`
* Launch the web server with `node ./server.js`

## Deployment on Heroku

* Issue `heroku create [app-name] --stack cedar` in a terminal, then clone the prompted git URL
* Copy content of this repository to the empty heroku repo
* `git commit -a` and `git push origin master` to push&deploy the repository on heroku
* `heroku open` will open your brand new application in a browser

## Database.com relations

The sample setup is the following (according to the challenge requirements):

* `Account__c` object with `lat__c` and `long__c` fields, which are Number(3, 6) data types. This is a list
of franchise locations.
* Patron name is stored in `patron__c` object with field `Name`. Basically they are the users of our game.
* Each score submission is stored in `score__c` object with field `points__c`, with lookup relationship to account and patron.

When a user submits a score, a new score record is always created. A new patron record is also created, if the patron's name did
not exist before.

## License

MIT license
