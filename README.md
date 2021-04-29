# Astronomical Private Blockchain Application


### Purpose and API Workflow

1. It will create a Genesis Block when we run the application.
2. The user will request the application to send a message to be signed using a Wallet and in this way verify the ownership over the wallet address. The message format will be: `<WALLET_ADRESS>:${new Date().getTime().toString().slice(0,-3)}:starRegistry`;
3. Once the user have the message the user can use a Wallet to sign the message.
4. The user will try to submit the Star object for that it will submit: `wallet address`, `message`, `signature` and the `star` object with the star information.
5. The application will verify if the time elapsed from the request ownership (the time is contained in the message) and the time when you submit the star is less than 5 minutes.
6. If everything is okay the star information will be stored in the block and added to the `chain`
7. The application will allow us to retrieve the Star objects belong to an owner (wallet address). 


## Dependencies

- This application was created using Node.js. The architecture uses ES6 classes. To run the project you will require Node.js and npm.
- Core libraries and npm modules:
    - "bitcoinjs-lib": "^4.0.3",
    - "bitcoinjs-message": "^2.0.0",
    - "body-parser": "^1.18.3",
    - "crypto-js": "^3.1.9-1",
    - "express": "^4.16.4",
    - "hex2ascii": "0.0.3",
    - "morgan": "^1.9.1"
    Remember if you need install any other library you will use `npm install <npm_module_name>`

Libraries purpose:

1. `bitcoinjs-lib` and `bitcoinjs-message`. Helps us verify the wallet address ownership and signature verification.
2. `express` The REST API for the project created using Express.js framework.
3. `body-parser` this library will be used as middleware module for Express and will help us to read the json data submitted in a POST request.
4. `crypto-js` Used to create the block hash.
5. `hex2ascii` Used to **decode** the data saved in the body of a Block.

## Code Overview

The Boilerplate code is a simple architecture for a Blockchain application, it includes a REST APIs application to expose the your Blockchain application methods to your client applications or users.

1. `app.js` file. It contains the configuration and initialization of the REST API.
2. `BlockchainController.js` file. It contains the routes of the REST Api. Those are the methods that expose the urls you will need to call when make a request to the application.
3. `src` folder. Contains the `Block` and `BlockChain` classes.

### Running Locally

1. Download or clone our boilerplate code.
2. Then we need to install all the libraries and module dependencies, to do that: open a terminal and run the command `npm install`
3. Use the command: `node app.js`
4. You can check in your terminal the the Express application is listening in the PORT 8000
5. Using [Postman](https://www.postman.com/) you can GET http://localhost:8000/block/height/0 which will create/request the Genesis Block
![alt text](https://github.com/WolfeTyler/astronomical-private-blockchain/screenshots/PostmanGenesisBlock.png "Postman Genesis Block")
6. Next in Postman POST http://localhost:8000/requestValidation to request ownership which will respond with a message
8. Sign the message using a Bitcoin wallet such as [Electrum](https://electrum.org/#home) (with Legacy seeding)
9. You can then submit a new star to the blockchain
10. Finally, all stars can be retrieved by owner based on their Bitcoin wallet id
