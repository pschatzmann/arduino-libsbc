# arduino-libsbc

SBC, or low-complexity subband codec, is an audio subband codec specified by the Bluetooth Special Interest Group (SIG) for the Advanced Audio Distribution Profile (A2DP). SBC is a digital audio encoder and decoder used to transfer data to Bluetooth audio output devices like headphones or loudspeakers. It can also be used on the Internet. It was designed with Bluetooth bandwidth limitations and processing power in mind to obtain a reasonably good audio quality at medium bit rates with low computational complexity. As of A2DP version 1.3, the Low Complexity Subband Coding remains the default codec and its implementation is mandatory for devices supporting that profile, but vendors are free to add their own codecs to match their needs.

The current implementation can be found as part of other projects. Unfortunately I did not find any stand alone library with only the decoder, so I decided to create this project and make it Arduino complient.




