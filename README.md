# Google Maps to Waze

It's hard to argue that Google Maps is an essential tool for searching places. It's also true that Waze is an amazing navigation app for driving. Unfortunately, there is no straightforward way to open Google Maps links with Waze and manual searching is often tedious, tricky and doesn't provide you with correct results.

The Google Maps to Waze Telegram bot is designed to solve this exact problem.  
The bot is available at https://t.me/gmaps_2_waze_bot  
It's available for anyone and completely free, try it out!

## Usage

You can deploy your own bot if you like!  
There are two types of deployment - polling and webhook, check the details below.

#### Polling

The most quick and basic setup.

Create a Telegram bot, copy `.env.example` to `.env`, set `TELEGRAM_TOKEN`, comment out everything else in the `Webhook` section.  
Run `docker compose up -d`

That's it, the bot is ready to use!

As simple as it is, this type has one big drawback - the bot needs to constantly poll Telegram API for new messages to detect when something is sent. It means that around 99.99% of requests are wasted which is not a clean or efficient design.

#### Webhook

The most efficient but advanced setup.  
Requires a domain and open HTTP(S) ports to run the endpoint.

Create a Telegram bot, copy `.env.example` to `.env`, set all the environment variables accordingly.  
Run `docker compose -f docker-compose.https-endpoint.yml -f docker-compose.yml up -d`

The solution leverages [nginx-proxy](https://github.com/nginx-proxy/nginx-proxy) and [acme-companion](https://github.com/nginx-proxy/acme-companion) sidecars to automatically configure Nginx and issue/renew SSL certificates for your (sub)domain, no manual actions are needed!  
Then the bot will be publicly available at this secure endpoint and linked to the Telegram bot automatically.

This type is as efficient as possible as now Telegram sends all new messages to your endpoint and the bot does not need to constantly poll Telegram API to detect when something is sent. 

## Testing and development

If you want to test the Webhook deployment but don't have a domain or server, you can use free services like [Serveo](https://serveo.net/) or [Ngrok](https://ngrok.com/) to expose your local server to the internet.
