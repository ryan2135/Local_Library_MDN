# Updated 5.30.25

Original docs: https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started

It's been a couple of years since I've gone through this tutorial. I spun this up today doing the following:

1. Created a codespace off the repos
2. Changed into the directory express-locallibrary-tutorial
3. Started up server
<pre>DEBUG=express-locallibrary-tutorial:* npm start</pre>
4. Created book db 
<pre>node populatedb.js mongodb://127.0.0.1/local_library</pre>

I would like to reproduce this tutorial more professionally using React.

<hr style="border:2px solid gray">


# IMPORTANT:

## How to recreate this dev environment from scratch:
* Create a repository with just a README.md
* Open that repository in Codespaces
* At the command palette: 
  * ```Dev Containers: Add Dev Container Configuration Files...```
	* ```Create a new configuration```
	* ```mongo```
* Documentation
  * [Instructions](https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-an-existing-folder-in-a-container)
  * [More instructions](https://github.com/devcontainers/templates/issues/113#issuecomment-1406905679)
  * Further [documentation on devcontainer.json](https://containers.dev/supporting)
* At the command line, you can use ```mongosh```
* You can also use the [MongoDB for VSCode extension](https://marketplace.visualstudio.com/items?itemName=mongodb.mongodb-vscode) (pre-installed) to connect to Mongo.

### Notes
* The Mongo Database is available at ```mongodb://localhost:27017```
* You can [forward](https://docs.github.com/en/codespaces/developing-in-codespaces/forwarding-ports-in-your-codespace) the port locally (see also forwardPorts below)
* Data stored in Mongo is persisted when you shutdown the Codespace.
* Data stored in Mongo is *NOT persisted* if you delete the Codespace.

---

---

# Node.js & Mongo DB (javascript-node-mongo)

Develop applications in Node.js and Mongo DB. Includes Node.js, eslint, and yarn in a container linked to a Mongo DB.

## Options

| Options Id | Description | Type | Default Value |
|-----|-----|-----|-----|
| imageVariant | Node.js version (use -bullseye variants on local arm64/Apple Silicon): | string | 20 |

This template references an image that was [pre-built](https://containers.dev/implementors/reference/#prebuilding) to automatically include needed devcontainer.json metadata.

* **Image**: mcr.microsoft.com/devcontainers/javascript-node ([source](https://github.com/devcontainers/images/tree/main/src/javascript-node))
* **Applies devcontainer.json contents from image**: Yes ([source](https://github.com/devcontainers/images/blob/main/src/javascript-node/.devcontainer/devcontainer.json))

## Using this template

This template creates two containers, one for Node.js and one for MongoDB. You will be connected to the Node.js container, and from within that container the MongoDB container will be available on on **`localhost`** port 27017 The MongoDB instance can be managed in VS Code via the automatically installed MongoDB extension. Database options can be configured in `.devcontainer/docker-compose.yml` and data is persisted in a volume called `mongo-data`.

It uses the `mcr.microsoft.com/devcontainers/javascript-node` image which includes `git`, `eslint`, `zsh`, [Oh My Zsh!](https://ohmyz.sh/), a non-root `vscode` user with `sudo` access, and a set of common dependencies for development.

You also can connect to MongoDB from an external tool when connected to the Dev Contaner from a local tool by updating `.devcontainer/devcontainer.json` as follows:

```json
"forwardPorts": [ "27017" ]
```

### Adding another service

You can add other services to your `.devcontainer/docker-compose.yml` file [as described in Docker's documentaiton](https://docs.docker.com/compose/compose-file/#service-configuration-reference). However, if you want anything running in this service to be available in the container on localhost, or want to forward the service locally, be sure to add this line to the service config:

```yaml
# Runs the service on the same network as the database container, allows "forwardPorts" in devcontainer.json function.
network_mode: service:db
```

### Using the forwardPorts property

By default, web frameworks and tools often only listen to localhost inside the container. As a result, we recommend using the `forwardPorts` property to make these ports available locally.

```json
"forwardPorts": [9000]
```

The `ports` property in `docker-compose.yml` [publishes](https://docs.docker.com/config/containers/container-networking/#published-ports) rather than forwards the port. This will not work in a cloud environment like Codespaces and applications need to listen to `*` or `0.0.0.0` for the application to be accessible externally. Fortunately the `forwardPorts` property does not have this limitation.


---

_Note: This file was auto-generated from the [devcontainer-template.json](https://github.com/devcontainers/templates/blob/main/src/javascript-node-mongo/devcontainer-template.json).  Add additional notes to a `NOTES.md`._
