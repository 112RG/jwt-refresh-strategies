# JWT refresh stratergies using fastify
Some simple ways to using JWT tokens and refresh tokens on non SPA apps. Keep in mind it is much easier when using something like Vue or Angular to have refresh tokens. But why do they get to have all the fun of refresh tokens? Explained in this repo are two ways you can use refresh tokens. I use this in app using PUG as a templating engine and served by fastify. 

Why didn't I just use sessions? Not sure really I guess I didn't want to. I guess I like that I can trust JWT's sent by the client and use it for add roles etc. Plus they are super quick and it allows me to not care about state server side.

## Refreshing the inline

This is when you refresh the token on a get request to a protected resource. And then return the new tokens as a cookie on th reply

Example user requests /protected our function authenticate() checks if the auth token is expired if so it then tries to refresh it using the refresh token. If this completes successfully a .setCookie() is sent back to the client in the reply

---

## Redirect refresh

This is when you redirect the user to a /refresh endpoint on a get request to a protected resource 

A example of this is as such. A user with an expired auth token, requests /protected it fails since there token is expired. They are redirect to /refresh and if a valid refresh token is given new tokens are issued. They are then redirected back to there orginal request in this case /protected and this time it succedes. 