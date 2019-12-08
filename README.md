# TOC-chatbot

A chatbot based on LINE using a finite-state-machine.

![fsm](./img/show-fsm.png)

## States
The initial state is set to `user`.

Every time `user` state is triggered to `advance` to another state, it will `go_back` immediately to `user` state after the bot replies corresponding message.

* user
	* Input: "go to state1"
		* Reply: "I'm entering state1"

	* Input: "go to state2"
		* Reply: "I'm entering state2"


## Setup
### Prerequisite
* Python 3.6
* Line App and Developers
* HTTPS Server
* pygraphviz/graphviz(For visualizing FSM)


#### Install Dependency
```sh
pip3 install -r requirements.txt
```


#### Secret Data
A `.env` file is needed to store `LINE_CHANNEL_SECRET` and `LINE_CHANNEL_ACCESS_TOKEN`.

You should issue these on LINE Developers, and **MUST** copy and paste them to `.env` correctly.


# 
## Deploy to HEROKU
Connect to Heroku in order to deploy.

### Heroku CLI installation

* [macOS, Windows](https://devcenter.heroku.com/articles/heroku-cli)


### Upload project to Heroku

1. Add local project to Heroku project

	```
	heroku git:remote -a {HEROKU_APP_NAME}
	```

2. Upload project

	```
	git add .
	git commit -m "Add code"
	git push -f heroku master
	```

3. Set Environment - Line Messaging API Secret Keys

	```
	heroku config:set LINE_CHANNEL_SECRET=your_line_channel_secret
	heroku config:set LINE_CHANNEL_ACCESS_TOKEN=your_line_channel_access_token
	```
	
	Or you can go to setting to set Config Vars on HEROKU.

4. Your Project is now running on Heroku!

	```
	url: `{HEROKU_APP_NAME}.herokuapp.com/callback`
	debug command: `heroku logs --tail --app {HEROKU_APP_NAME}`
	```

5. Dealing with `pygraphviz` install errors

	run commands below
	```
	heroku buildpacks:set heroku/python
	
	heroku buildpacks:add --index 1 heroku-community/apt
	```

# 
#### Run Locally
You can either setup https server or using `ngrok` as a proxy.


#### Ngrok
* [ macOS, Windows, Linux](https://ngrok.com/download)

**`ngrok` would be used in the following instruction**

```sh
ngrok http 8000
```

After that, `ngrok` would generate a https URL.	(*eg. https://464ac8bf.ngrok.io*)

Paste the https URL to the webhook URL on LINE Developers.


Next, add one of these in the end to check the functions.

> /callback	-> Echo every text messages you send
> /webhook	-> Check the functionality of states
> /show-fsm	-> Download the diagram of FSM or send the image on LINE


#### Run the server

```sh
python3 app.py
```

Now the app is running on localhost, we can check the webhook events.

By using ngrok, we can debug and check the status easily and conveniently.
