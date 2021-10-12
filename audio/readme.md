## Audio Files
These are the azan audio files used for the automation.\
Copy them to your media folder. 

## For Alexa Devices
File with prefix \_alexa is audio file formatted for Alexa devices.
Please place the audio file to /config/www/audio path.

**Audio requirements:**
- Bit rate: 48kbps
- Sample rate: 22050Hz, 24000Hz, or 16000Hz
- Duration: Cannot exceed 4min (240sec)

**How to convert audio (with Audacity)**
1. Open the file to convert.
2. Set the Project Rate (Hz) in the lower-left corner to ``16000``.
3. Click File > Export Audio and change the Save as type to MP3 Files.
4. Click Options, set the Quality to ``48kbps`` and the Bit Rate Mode to ``Constant``.
