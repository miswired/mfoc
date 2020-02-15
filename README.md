MFOC is an open source implementation of "offline nested" attack by Nethemba.

This program allow to recover authentication keys from MIFARE Classic card.

Please note MFOC is able to recover keys from target only if it have a known key: default one (hardcoded in MFOC) or custom one (user provided using command line).

# Build from source
Install Prerequisites, below instructions are for Ubuntu

```
sudo apt-get update  
sudo apt-get install git binutils make csh g++ sed gawk autoconf automake autotools-dev libglib2.0-dev libnfc-dev liblzma-dev libnfc-bin
```

```
git checkout hardnested
autoreconf -is
./configure
make && sudo make install
```

# Disable pn533_usb
Some readers require pn533_usb to be disabled. If you have trouble do this.

```
modprobe -r pn533_usb
```

Then add pn533_usb to blacklist
/etc/modprobe.d/blacklist-libnfc.conf


# Usage #
Put one MIFARE Classic tag that you want keys recovering;
Lauching mfoc, you will need to pass options, see
```
mfoc -h
```

Test for default keys and find all the others if it has them.
```
mfoc -O outputfile.dmp
```

Give it a key to use if you know one of the good keys.
```
mfoc -O outputfile.mfd -k AABBCCDDEEFF
```

Or find a key if none known by providing optimizatio parameters.
```
mfoc -C -R 0:A -s 250 -S 250 -v 5
```
