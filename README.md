# CS411 Final Project

## Disclaimer!
- This guide was created using a **Linux OS** machine!
- When running `python app.py` (the Flask server), expect an error stating

<hr>

## Assignments
The following assignments are located in the following directories:

1. CS411 Project Assignment 1: [Pitches](https://github.com/dlhi/CS411-Project/blob/master/docs/01%20Project%20Proposals/project_proposals.md)
2. CS411 Project Assignment 2: [User Stories](https://github.com/dlhi/CS411-Project/blob/master/docs/02%20User%20Stories/UserStories.pdf)
3. CS411 Project Assignment 3: [Prototype Demo #1 (API)](https://github.com/dlhi/CS411-Project/blob/master/prototype/03%20api_demo/app.py)
4. CS411 Project Assignment 4: [Analysis / Platform Decision](https://github.com/dlhi/CS411-Project/blob/master/docs/04%20Decisions/CAS411%20Team%20Assignment%203.pdf)
5. CS411 Project Assignment 5: [Prototype Demo #2 (OAuth)](https://github.com/dlhi/CS411-Project/blob/master/prototype/05%20oauth_demo/app.py)

## Setup

1. Clone the repository from Github.
2. Current Base Flask code is hosted on branch **flask_base**. Switch to this branch and create new branches if needed.
3. Create a virtual environment and begin downloading the required libraries.
    * To begin, install virtual environment. Make sure to install using **pip3**.
        `pip3 install virtualenv`
    * Create a virtual environment. There are several ways to do this, but this is the terminal command I used: <br />
            `virtualenv -p /usr/bin/python3 venv` <br />
        You can also use: <br />
            `virtualenv -p python3 venv`
4. Enter the virtual environment with the following command:
    *   `source venv/bin/activate`
5. Install the required dependencies to run Flask with the following command:
    *   `pip3 install -r requirements.txt`
    * At the time of writing this guide, you should check if the required dependencies have been installed correctly by running the following in the terminal line:
        `pip3 freeze`
    
        cachetools==3.1.1
        certifi==2019.9.11
        chardet==3.0.4
        Click==7.0
        Django==2.2.6
        Flask==1.1.1
        google-api-python-client==1.7.11
        google-auth==1.7.2
        google-auth-httplib2==0.0.3
        google-auth-oauthlib==0.4.1
        httplib2==0.14.0
        idna==2.8
        itsdangerous==1.1.0
        Jinja2==2.10.3
        MarkupSafe==1.1.1
        oauthlib==3.1.0
        pkg-resources==0.0.0
        pyasn1==0.4.8
        pyasn1-modules==0.2.7
        pymongo==3.9.0
        pytz==2019.3
        requests==2.22.0
        requests-oauthlib==1.3.0
        rsa==4.0
        six==1.13.0
        sqlparse==0.3.0
        uritemplate==3.0.0
        urllib3==1.25.6
        Werkzeug==0.16.0

    * Your `pip3 freeze` command should match the above.

6. To use the Spotify API, you must have a Client ID and Secret. However, you do not want to release these identifiers to the public.
    * Create a file named **config.cfg** in the same directory as **app.py, requirements.txt, LICENSE, ...**
    * Go to [Spotify Developer](https://developer.spotify.com/dashboard/applications)
    * Create your own application and look for the Client ID and Secret. You will need both of these to use the API.
    * You also need to set your own session secret to use Flask Sessions.
    * Your **config.cfg** should resemble the following:

        [DEFAULT]

        client_id = your_id_here <br />
        client_secret = your_secret_here <br />

7. You are now ready to run the Flask application. To run the application, execute the following command in the terminal line:
    *   `python3 app.py`

## Notes
* Spotify does not allow *POST* requests. Instead, use *PUT* to communicate with the server. 
    - Supporting documentation: [Link](https://stackoverflow.com/questions/46119001/swift-spotify-api-error-code-405-add-to-library)
* However, Python Flask HTTP requests do NOT support *PUT* requests.
    - You can get around this limitation by adding the redirected URL to Spotify's whitelist of supported websites on the Spotify Web API Application dashboard.
    - Once your URL is whitelisted, you can proceed to use *POST* requests!
* Cannot use POST or GET requests in link callback due to authorization expectations for a specific request from the Spotify server.
* Cannot use Flask session variables as they are too small to store the required user data.
* You cannot store JSON information with single quotes. They **must** be double quotes.
* In Django, do not put in {{}} into other {{}}
    - Supporting Documentation: [Link](https://stackoverflow.com/questions/27704913/templatesyntaxerror-expected-token-got/47025013)
* In order to create playlists using the Youtube API, you **MUST** be logging into our application with an account that possesses a Youtube Channel. You will not be able to create playlists if you are not logged in with a channel.
* In my Linux VM (running Ubuntu 16.04 OS), I could not run the Flask application on Firefox. Switch to Chrome if you are experiencing this issue.
    - Firefox's display stated a tab crashed repeatedly.
* You may run into the following errors: 
    * KeyError: 'access_token'
        - `access_token = response_data["access_token"]`
        - Solution: Try accessing the same URL again, should refresh. E.g. go to localhost:portnumber again.
    
