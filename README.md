# Mattermost/OpsGenie Integration

* [Feature summary](#feature-summary)
* [Set up](#set-up)
    * [Installation HTTP](#installation-http)
    * [Installation Mattermost Cloud](#installation-mattermost-cloud)
    * [Configuration](#configuration)
* [Admin guide](#admin-guide)
    * [Slash commands](#slash-commands)
* [End user guide](#end-user-guide)
    * [Get started](#get-started)
    * [Use /opsgenie commands](#use-genie-commands)
* [Development environment](#development-environment)
    * [Manual installation](#manual-installation)
    * [Install dependencies](#install-dependencies)
    * [Run the local development environment](#run-the-local-development-environment)
  * [Run the local development environment with Docker](#run-the-local-development-environment-with-docker)

This application allows you to integrate OpsGenie to your Mattermost instance, letting you know when a new alert is created, as well as getting notified about alert updates. Also, allows the user to create new alerts, add notes to alerts, close alerts, assign alerts, etc. without moving from the Mattermost window.

# Feature summary

**OpsGenie to Mattermost notifications:** Link your Mattermost channels with the OpsGenie Teams you want to see, so you and your team can get notifications about the creation and updates of each alert.

# Set up

## Installation HTTP

To install, as a Mattermost system admin user, run the command ``/apps install http OPSGENIE_API`` in any channel. The ``/genie`` command should be available after the configuration has been successfully installed.

The ``OPSGENIE_API`` should be replaced with the URL where the OpsGenie API instance is running. Example: ``/apps install http https://myapp.com/manifest.json``

## Installation Mattermost Cloud

To install, as a Mattermost system admin user, run the command ``/apps install listed genie`` in any channel. The ``/genie`` command should be available after the configuration has been successfully installed.


## Configuration

After [installing](#installation)) the app:
1. Open your OpsGenie profile to get your credentials and link to your Mattermost instance.
2. Select the **Integrations** tab in the **Settings** menu. Then, click on the **Add Integration** button.
3. Inside the **Add Integration** menu, select the **API** option.
4. Update the integration name and access. Finish the **API** integration set up clicking the **Save Integration** button.
5. Copy the given API Key.
6. Return to Mattermost. 
7. As a Mattermost system admin user, run the ``/genie configure`` command.
8. In the configuration modal, enter your API Key.

# Admin guide

## Slash commands

- ``/genie configure``: This command will enable all the other commands; it asks the administrator for an API key (which will be used to execute calls to OpsGenie’s API).

# End user guide

## Get started

## Use ``/genie`` commands

- ``/genie help``: This command will show all current commands available for this application.
- ``/genie alert create``: Allow any user to create a new alert.
- ``/genie alert note``: Adds a note to an existing alert.
- ``/genie alert close``: Closes an existing alert.
- ``/genie alert ack``: Acknowledge an existing alert.
- ``/genie alert unack``: UnAcknowledge an existing alert.
- ``/genie alert snooze``: Snooze an existing alert for a period of time.
- ``/genie alert assign``: Assign an existing to a mattermost team member.
- ``/genie alert own``: Take ownership of an existing alert (assign alert to yourself).
- ``/genie alert priority``: Set the priority of an existing alert.
- ``/genie alert list``: Get a list of the existing alerts.
- ``/genie team list``: Get a list of the existing teams.
- ``/genie subscription add``: Creates a new subscription for notifications: choose a team and a channel and get notified of the updates in that team. You can subscribe more than one team per channel.
- ``/genie subscription list``: Show the list of all subscriptions made in all of your channels.
- ``/genie subscription remove``: Will allow you to remove a subscription. No more notifications from that team will be received.

# Development environment

## Manual installation

*  Download the latest repository release.

### Run the local development environment

* You need to have installed at least node version 15 and maximum version 18. You can download the latest lts version of node for the required operating system here https://nodejs.org/es/download/

### Install dependencies
* Move to the project directory or execute ``cd`` command to the project directory and execute ``npm install`` with a terminal to download all dependency libraries.

```
$ npm install
```

*  Update the environment configuration file. The ``.env`` file must be modified or added to set the environment variables, it must be in the root of the repository.

```
file: .env

PROJECT=mattermost-opsgenie-app
PORT=4002
HOST=http://localhost:4002
```

Variable definition

- PROJECT: In case of executing the project with Docker using the ``.build.sh`` file, this variable will be used for the name of the container
- PORT: Port number on which the OpsGenie integration is listening
- HOST: OpsGenie API usage URL

* Finally, the project must be executed.

```
$ npm run dev
```

Or, if you would like to use the Makefile command:

```
$ make watch
```

### Run the local development environment with Docker

* You need to have Docker installed. You can find the necessary steps to install Docker for the following operating systems:

[Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
[Mac](https://docs.docker.com/desktop/mac/install/)
[Windows](https://docs.docker.com/desktop/windows/install/)

* Once you have Docker installed, the next step would be to run the ``make run-server`` command to create the API container and expose it locally or on the server, depending on the case required.

```
$ make run-server
```

When the container is created correctly, the API will be running at the url http://127.0.0.1:4002. If Mattermost is running on the same machine, run this slash command in Mattermost to install the app:

```
/apps install http http://127.0.0.1:4002
```

To stop the container, execute:

```
$ make stop-server
```
