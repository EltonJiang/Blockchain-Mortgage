OBC Mortgage Demo
=================
Contact Andreas Kind @IBM, 2016

## Window 0: Start CA service
$ cd <WORKSPACE>/obc-dev-env
$ vagrant ssh
> cd $GOPATH/src/github.com/openblockchain/obc-peer/obc-ca
> go build -o obcca-server
> ./obcca-server

## Window 1: Start peer
$ cd <WORKSPACE>/obc-dev-env
$ vagrant ssh
> cd $GOPATH/src/github.com/openblockchain/obc-peer
> OPENCHAIN_SECURITY_ENABLED=true OPENCHAIN_SECURITY_PRIVACY=true ./obc-peer peer --peer-chaincodedev

## Window 2: Run compile, start and validate chanced
$ cd <WORKSPACE>/obc-dev-env
$ vagrant ssh
> cd $GOPATH/src/github.com/openblockchain/obc-peer/openchain/example/chaincode/chaincode_mortgage
> go build
> OPENCHAIN_CHAINCODE_ID_NAME=myMortgage OPENCHAIN_PEER_ADDRESS=0.0.0.0:30303 ./chaincode_mortgage

## Start local web server to provide ‘mortgage.html’ on http://localhost:8080
node server.js

With these lines in server.js:
var connect = require('connect');
var serveStatic = require('serve-static');
//connect().use(serveStatic(__dirname)).listen(8080);
connect().use(serveStatic(‘<YOUR_WWW_PATH>’)).listen(8080);

## Open web application
http://localhost:8080/mortgage_<VERSION>.html

Menu -> Deploy Contract (needed as first step)
Menu -> Console
Menu -> Process
...
