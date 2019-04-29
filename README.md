# nau7802

NAU7802 A/D converter library for Node.js

It supports I2C.1 and I2C.2 of Raspberry Pi.

## Installation

```
npm install nau7802
```

## Enable I2C

If it's the first time to use the I2C functionalities of your Raspberry Pi, some steps are needed to enable them.

Run

```
sudo raspi-config
```

on the terminal. It will open the software and hardware config tool. Select **"5 Interfacing Options"** > **"P5 I2C"**, then select *"YES"* to the question "Would you like the ARM I2C interface to be enabled?". After closing the tool by < Finish > button, you are ready to use I2C!

## Example

```
const NAU7802 = require('nau7802');

const adc = new NAU7802(1); // NAU7802 is connected to I2C.1 bus
adc.start();
adc.selectChannel1(); // Selec channel
adc.setRate80SPS(); // Sampling rate
adc.startCycle();

setInterval(()=>{
  console.log("ADC value=%d", adc.readADCValue());
  }, 1000);

```

## API

### constructor (i2cBusNumber)
* i2cBusNumber : Number of I2C bus (1 or 2). If not specified, I2C.1 will be selected.

### start ()
Open I2C, reset all registers and start analog to digital conversion.
### resetResisters ()
Reset all registers of NAU7802.
### calibrate ()
Start calibration and wait until it finishes.
### setRate10SPS ()
Select conversion rate.
### setRate20SPS ()
Select conversion rate.
### setRate40SPS ()
Select conversion rate.
### setRate80SPS ()
Select conversion rate.
### setRate320SPS ()
Select conversion rate. 320SPS is the default value.
### selectChannel1 ()
Select Channel 1 and calibrate.
### selectChannel2 ()
Select Channel 1 and calibrate.
### startCycle ()
Start conversion cycle manually.
### readADCValue ()
Read 24-bit value of A/D conversion result. It returns signed value.
### getRevision ()
Read the revision code.

### setRegValue (regAddress, value)
Set a register's value.
* regAddress : Register address
* value : Byte to write

### readRegValue (regAddress)
Read a register's current value.
* regAddress : Register address

### setRegisterBit (regAddress, bitIndex)
Set a register's single bit to 1.
* regAddress : Register address
* index : Bit index

### setRegisterBit (regAddress, bitIndex)
Clear a register's single bit to 0.
* regAddress : Register address
* index : Bit index

### waitForBitValue (regAddress, bitIndex, bitValue, timeoutMsec)
Wait until the specified bit value become true or false.
* regAddress : Register address
* bitIndex : Bit bit index
* bitValue : Desired value (0 or 1)
* timeoutMsec : Timeout (msec)
