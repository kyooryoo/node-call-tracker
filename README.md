# Calling Tracking Demo with Node
We can use unique identifiers to measure the impact of past decisions and fine-tune future ones. You can track the phone numbers that are used for campaigns on television, radio, magazine, print or online advertising, find the most popular ones for improving future campaigns.

## Use case
* Use different numbers for different campaigns (TV, Radio, Print, Online, etc.)
* Forward the call to these numbers to the same call center numbers
* Track the number of calls through different campaign associated numbers
* Use the collected data to improve business decision making for future campaigns

## Prerequisites
* Prepare some Nexmo Virtual Number
* Have [Nexmo CLI](https://github.com/Nexmo/nexmo-cli/) installed
* Use Heroku to publish local web server

## Step by Step Guide
1. Reuse the code
```sh
git clone https://github.com/nexmo/node-call-tracking.git
cd node-call-tracking
mv example.env .env
npm install
```
2. Publish local port and note down returned link [ngrok_url]
```sh
./ngrok http 5000
```
3. Create the nexmo application and note down returned app ID [nexmo_app]

```sh
nexmo app:create "call-track" [ngrok_url]/answer [ngrok_url]/event --keyfile private.key
```
4. Buy numbers that will be tracked and note down returned number [nexmo_num]
```sh
nexmo number:buy --country_code US
```
5. Link the number to the app
```sh
nexmo link:app [nexmo_num] [nexmo_app]
```
6. Fill the .env file with proper variable values
```sh
PROXY_TO_NUMBER=[your_real_call_center_number]
```
7. Run the App and
```sh
npm start
```

The application should be available on <http://localhost:5000>.

### Using the App

Call one of the virtual numbers that you rented. The call will be tracked and forwarded to the desired destination number.

You can see a list of tracked calls by accessing <http://localhost:5000/tracked-calls>.
