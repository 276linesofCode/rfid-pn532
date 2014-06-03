#RFID
Driver for the rfid-pn532 Tessel RFID module ([PN532](http://www.adafruit.com/datasheets/pn532longds.pdf)).

##Installation
```sh
npm install rfid-pn532
```
##Example
```js
/*********************************************
This basic RFID example listens for an RFID
device to come within range of the module,
then logs its UID to the console.
*********************************************/

var tessel = require('tessel');

var rfid = require('../').use(tessel.port['A']); // Replace '../' with 'rfid-pn532' in your own code

rfid.on('ready', function (version) {
  console.log('Ready to read RFID card');

  rfid.on('data', function(uid) {
    console.log('UID:', uid);
  });
});
```

##Methods

##### * `rfid.setPollPeriod(pollPeriod, callback(err))` Set the time in milliseconds between each check for an RFID device.

##### * `rfid.mifareClassicAuthenticateBlock(cardUID, blockNumber, authType, authKey, callback(err))` Authenticate a block of memory to read or write on a MIFARE classic card. `cardUID` is the UID of the card to authenticate. `blockNumber` is the block address to authenticate. `authType` can be `0` for authorization type A or `1` for type B. `authKey` is an array containing the authorization key for the memory block, most commonly `[0xFF, 0xFF, 0xFF, 0xFF, 0xFF, 0xFF]`.

##### * `rfid.mifareClassicReadBlock(blockNumber, callback(err, data))` Read a block of memory on a MIFARE classic card. `blockNumber` is the address of the block to read.

##### * `rfid.mifareClassicWriteBlock(blockNumber, data, callback(err))` Write a block of memory on a MIFARE classic card. `blockNumber` is the address of the block to write. `data` is an array containing the 16 bytes of data to write to the block.

##Events

##### * `rfid.on('data', callback(data))` Emitted when data is available.

##### * `rfid.on('error', callback(err))` Emitted upon error.

##### * `rfid.on('ready', callback())` Emitted upon first successful communication between the Tessel and the module.

##TODO
Implement commands for additional NFC card types

## License
MIT
APACHE
