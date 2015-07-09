# HomeKit for Bluetooth (BLE)

Apple's HomeKit protocol supports both IP and BLE devices. While there appear to be a few open source implementations
of IP stacks around (notably https://github.com/KhaosT/HAP-NodeJS), I couldn't find any BLE stacks. So, here's one for
you to play with.

This stack runs on the Nordic BLE nRF51 series of chips. The projects compiles using the "standard" Eclipse/GCC toolchain
setup.

# Code

The code provides all the services required to pair iOS with a BLE device and to operate that device once paired. It
runs on the Nordic nRF51 PCA10028 development board.

## Timings

Here are some perliminary timings. Note that all crypto code is in C and assembly level tweaking should improve things greatly. Also note that these times do not include the time to send and receive the payloads. But, anyway, numbers:

### Pairing

Pairing is dominated by the SRP algorithm which is very slow and expensive. Fortunately this only happens once when the iOS device is being associated with the HomeKit device. 

Time: 42 seconds

### Verify

Verify happens everytime an iOS device reconnected to the HomeKit device. Ideally this should be as fast as possible.

Time: 4 seconds

# Thanks

I want to thank a number of projects which made this possible:

1. https://github.com/KhaosT/HAP-NodeJS - which documents the HomeKit protocols for IP and allowed me to guess how they
were implemented over Bluetooth.

2. http://tweetnacl.cr.yp.to - which provides the compact eliptical curve implementations, as well as the sha512 hash.

3. https://tls.mbed.org - which provides the core multi-precission math routines used in the SRP implementation.

# Notes

Please note that this software was produced without any reference to any propriatery documentation or information. I
am not a MFi licensee, nor do I have access to any related information.
