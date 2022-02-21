# Home Assistant Adzan 3.0 ![visitors](https://visitor-badge.glitch.me/badge?page_id=zubir2k.homeassistantadzan.visitor-badge)
Automation for Malaysia Adzan (Muslim call to prayer) based on the following sources:
- JAKIM Official (eSolat) - [Website](https://www.e-solat.gov.my).
- AzanPro - [Website](https://api.azanpro.com).
- Aladhan (for Hijri Dates) - [Website](https://aladhan.com/islamic-calendar-api)

**Whats New in 3.0**
- Source and location can be entered using input text and input select.
- Easily change sources if one failed (i.e. Timeout)
- Solat data can be stored locally and use as source. 
- Added Persistent Notification as default notification.

![image](https://user-images.githubusercontent.com/1905339/154905774-b63319d5-4b4b-46e5-9fab-8efdeeb10400.png)

![image](https://user-images.githubusercontent.com/1905339/141753194-579d9190-969f-4029-bf6c-92d7fdd65ab2.png)

## Installation
### 1. [configuration.yaml](configuration.yaml)
- Copy the lines into your configuration.yaml.
- It will enable/create the following:
  1. Downloader
  2. Input Select (for source selection)
  3. Input Text (for state/location code
  4. Load solat sensors
- Copy [esolat.yaml](esolat.yaml) into `/config`. **DO NOT ALTER THIS FILE**
- Reboot your Home Assistant to take effect.
- Once rebooted, perform the following:
  1. Enter your location code `input_text.solat` based on location/zone list
  2. Enter your Home Assistant URL in `input_text.homeurl`
  3. Select source (eSolat/AzanPro/Local)

**eSolat**\
https://www.e-solat.gov.my/index.php?siteId=24&pageId=50

**AzanPro**\
https://api.azanpro.com/zones

### 2. [automation.yaml](automation.yaml)
Copy the automations into your current automations.yaml
- Azan 3.0
- Azan 3.0 Yearly Update \
  (you need to run it once for the initial setup. It will save a esolat.json file into your ``/www/`` path)

![image](https://user-images.githubusercontent.com/1905339/141753839-1d9b3570-331e-4e3c-a487-572adc47e7cc.png)

**Adzan:**\
It is highly recommended to use speaker group (via Home Assistant) or from your Alexa or Google Home App.\
Example use in this automation is *all_devices* `media_player.all_devices` 

**Random verse:**\
You may add/remove audio files depending on your preferences.\
You can also use URL by changing the `media-source://media_source/local/audio/xxx.mp3`
```yaml
  - service: media_player.play_media
    data:
      media_content_type: audio/mp3
      media_content_id: |
        {{ ["media-source://media_source/local/audio/surah1.mp3",
            "media-source://media_source/local/audio/surah2.mp3",
            "media-source://media_source/local/audio/surah3.mp3",
            "media-source://media_source/local/audio/surah4.mp3",
            ] | random }}
```

### 2(a). [automation_alexa.yaml](automation_alexa.yaml) -- For Alexa Devices
- **IMPORTANT**: Please ensure [Alexa_Media_Player](https://github.com/custom-components/alexa_media_player) addon has been configured.
- Audio files must be placed at ``/config/www/audio``
- Due to Alexa restriction, it will only work on Home Assistant with SSL (HTTPS) -- tested to work on Cloudflare SSL
- [Alexa Documentation](https://developer.amazon.com/en-US/docs/alexa/custom-skills/speech-synthesis-markup-language-ssml-reference.html#audio)

**Audio requirements:**
- Bit rate: 48kbps
- Sample rate: 22050Hz, 24000Hz, or 16000Hz
- Duration: Cannot exceed 4min (240sec)

### 2(b). Raspberry Pi Audio
- Ensure VLC is installed. For HA hosted in a RaspberryPi, you may use [Local-VLC](https://github.com/rodripf/hassio-local-vlc) addon.
- Ensure official [VLC Media Player](https://www.home-assistant.io/integrations/vlc_telnet) integration is configured.
- **IMPORTANT**: All audio files must be stored in ``/share/audio``

### 3. [lovelace.yaml](lovelace.yaml)
Add new entities card on your dashboard and paste the YAML codes.

![image](https://user-images.githubusercontent.com/1905339/141753688-0944797d-cd20-430e-97a7-104ebc010a4f.png)

## MP3 Audio Files
Copy 2 audio files into your `/media/audio/` OR `/config/www/audio` OR `/share/audio`
- azan.mp3
- azansubuh.mp3
- azan_alexa.mp3
- azansubuh_alexa.mp3

## In-depth Video Tutorial
- Automation Adzan using Home Assistant: https://youtu.be/DZGJwaeQuGA
- Beginners Guide to Home Assistant: https://youtu.be/-jyegp-mL20 

## Special Thanks
- [@farxpeace](https://github.com/farxpeace) - for the original code
- [HomeAssistantMalaysia](https://www.facebook.com/groups/homeassistantmalaysia)
