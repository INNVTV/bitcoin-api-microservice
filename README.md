# Bitcoin API/Microservice
API endpoint that generates new Bitcoin addresses on server, passes public key back to requester and stores the associated private key to a MongoDB database.

# Use Cases
* Cloud Services
* IoT Edge Devices
* Background Processes

# Technologies used:
* .Net Core
* Nbitcoin
* C#
* MongoDB
* Docker

# Building project
Run the docker compose file:

     docker-compose build
     docker-compose up

If you are developing outside of docker you may need to run:

    dotnet restore

...before running

    dotnet build

...to ensure all packages are available. You should also note that your ports may be different than the Compose focused instructions provided below.

# Running the demo
Once you have your project running you can access the API endpoint using a GET request in your browser:
**localhost:8000/api/generate/publickeys/{int:count}**

Here is an example resulting in a single public key being generated:

    http://localhost:8000/api/generate/publickeys/1

And this will result in 5:

    http://localhost:8000/api/generate/publickeys/5

# Private key storage
To test that private keys are being stored use a MongoDB client such as Compass, Robo 3T or Navicat and navigate to:

     mongodb://mongodb:27017

As long as you don't shut down your docker instances after generating a few keys you should see the public keys with their associated private keys stored as records in the "keys" collection under the "bitcoin" database.

# Security
In a production environment you should encrypt the private key(s) prior to database storage. The application itself should only have a key for encryption. The decryption key should be held in a secure location accessible only to a secondary microservice that is used for signing transactions.
