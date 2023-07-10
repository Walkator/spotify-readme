<div align="center">
  <img src="assets/spotify.svg" width="100" align="center">
  <h1>Spotify Readme</h1>
</div>

<p align="center">
  A dynamic, simple and real-time Spotify Play Now widget for your README files that syncs with the currently playing song. If you're not currently playing a song, one of your recent songs will be displayed! Feel free to ask for help or ask any PR/problem/suggestion 😄
</p>

## Previews

#### Default
```
/api
```
![setup-screenshot](assets/preview.png)


## Setup/Deployment

#### 1. Spotify's API

* Head over to the <a href="https://developer.spotify.com/dashboard/">Spotify developer portal</a>.
  * Create a Spotify application.
    * In the **App name** & **App description** fields, you may put whatever you want.
    * Agree with Spotify's TOS and click **Create**.
  * Take note of the **Client ID** & **Client Secret**.
  * Click **Edit Settings**.
    * Add `http://localhost/callback/` to **Redirect URIs**.

#### 2. Intermediary Steps

```
https://accounts.spotify.com/authorize?client_id={CLIENT_ID}&response_type=code&scope=user-read-currently-playing,user-read-recently-played&redirect_uri=http://localhost/callback/
```

* Copy and paste the above link into your browser.
  * Replace `{CLIENT_ID}` with the **Client ID** you got from your Spotify application.
  * Vist the URL.
    * Log in if you're not already signed in.
    * Click **Agree**.
* After you get redirected to a blank page, retrieve the URL from your browser's URL bar. It should be in the following format: `http://localhost/callback/?code={CODE}`.
  * Take note of the `{CODE}` portion of the URL.
* Head over to <a href="https://base64.io">base64.io</a>.
  * Create a string in the form of `{CLIENT_ID}:{CLIENT_SECRET}` and encode it to base 64.
  * Take note of the encoded base 64 string.
* If you're on Windows or don't have the `curl` command, head over to <a href="https://httpie.io/cli/run">httpie.io/cli/run</a>.
  * Press enter.
  * Clear the pre-filled command.
* If you're on Linux or Mac with the `curl` command, open up your preferred terminal.
* Run the following command (replace `{BASE_64}` and `{CODE}` with their respective values):

  ```
  curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Authorization: Basic {BASE_64}" -d "grant_type=authorization_code&redirect_uri=http://localhost/callback/&code={CODE}" https://accounts.spotify.com/api/token
  ```

* If you did everything correctly, you should get a response in the form of a JSON object.
  * Take note of the `refresh_token`'s value.

#### 3. Host on Vercel

* Fork this repository.
* Head over to <a href="https://vercel.com">Vercel</a> and create an account if you don't already have one.
  * Add a new project on Vercel.
    * Link your GitHub account if you haven't done so already.
    * Make sure Vercel has access to the forked respository.
    * Import the forked respository into your project.
      * Give it a meaningful project name.
      * Keep the default options for the other settings.
      * Add the following environment variables along with their appropriate values:
        * `CLIENT_ID`
        * `CLIENT_SECRET`
        * `REFRESH_TOKEN`
      * Click **Deploy**.
      * Click **Continue to Dashboard**.
        * Find the **Domains** field and take note of the URL.
          * Example: `{PROJECT_NAME}.vercel.app`.

#### 4. Add to your GitHub

* In any markdown file, add the following (replace `{PROJECT_NAME}` with the name you gave your Vercel project):

```html
<img src="https://{PROJECT_NAME}.vercel.app/api" alt="Current Spotify Song">
```

## Note

This wasn't a completely original idea. This was inspired by <a href="https://github.com/novatorem/novatorem">novatorem's project</a> that was supposed to be for me only. Since others have asked for the source code, I decided to make this a public repo. I also incorporated the latest two PR's from the orignal project into this one and made it easy to customize!

<sub>**This feature is a fork of [tthn0](https://github.com/tthn0)**</sub>
