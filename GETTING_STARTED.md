# Getting Started

## Setup Postgres
This repo ships with a `Dockerfile` for a postgres image you can use in
`postgres-docker/Dockerfile`.

Build the docker image
```sh
docker build -t postgresql postgres-docker/
```

Run the docker image
```sh
docker run --rm -P --name database postgresql
```

Find out the port the postgres instance is running on
```sh
docker ps
```
## Setup Discord
In order to test the bot, you need to have a dedicated testing server.

1) [Click Here](https://discord.new/vkaVjTnf4aDc) to use our template. This is a server template functionality provided by Discord.
2) Create a bot account ([guide](https://discordpy.readthedocs.io/en/latest/discord.html#creating-a-bot-account)).
3) Get your bot's Client ID, replace `{ID}` with it, and then go to the URL in order to add the bot to your testing server.

```
https://discordapp.com/api/oauth2/authorize?client_id={ID}&permissions=8&scope=bot
```
## Get the bot running

Build the docker image for the bot
```sh
docker build -t discordbot .
```
A number of environment variables are required to run the bot.  Many of these
environment variables come from discord.  

+ `MOD_ID` is the id of the mod role
+ `TALK_ID` is the id of the talk role
+ `WG_AND_TEAMS_ID` is the id of the working groups and teams role
+ `DISCORD_TOKEN` is the token used to connect to discord
+ `DATABASE_URL` is the url where the database is running, you will need to
  update the port to the port your instance of postgres is running on

Once you have your guild setup, you can run the bot
```sh
docker run -e "MOD_ID=" -e "TALK_ID=" -e "DISCORD_TOKEN=" -e "DATABASE_URL=postgres://docker:docker@172.17.0.1:32768" --add-host=database:172.17.0.2 --rm -it discordbot
```
