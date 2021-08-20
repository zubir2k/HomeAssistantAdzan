# Home Assistant Adzan ![visitors](https://visitor-badge.glitch.me/badge?page_id=zubir2k.homeassistantadzan.visitor-badge)
Automation for Malaysia Adzan (Muslim call to prayer) based on the following sources:
- JAKIM Official (eSolat) - [Website](https://www.e-solat.gov.my).
- AzanPro (in separate [folder](https://github.com/zubir2k/HomeAssistantAdzan/tree/main/azanpro)) - [Website](https://api.azanpro.com).

## Installation
### 1. [configuration.yaml](configuration.yaml)
- Copy the sensors to your current configuration.yaml.
- Change the location code `<location code>` based on location/zone list

**eSolat**\
https://www.e-solat.gov.my/index.php?siteId=24&pageId=50
```yaml
  - platform: rest
    resource: https://www.e-solat.gov.my/index.php?r=esolatApi/takwimsolat&period=today&zone=<location code>
    name: Jakim Official
```

**AzanPro**\
https://api.azanpro.com/zones
```yaml
  - platform: rest
    resource: https://api.azanpro.com/times/today.json?zone=<location code>&format=24-hour
    name: AzanPro API
```

### 2. [automation.yaml](automations.yaml)
Copy 3 automations into your current automations.yaml
- Adzan
- Adzan Subuh
- Random verse of Al Quran audio playback (*x*) minute before Maghrib

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

### 3. [lovelace.yaml](lovelace.yaml)
Add new entities card on your dashboard and paste the YAML codes.

![image](https://raw.githubusercontent.com/zubir2k/HomeAssistantAdzan/main/lovelace-card.png)

## MP3 Audio Files
Copy 2 audio files into your `/media/audio/` OR `/config/www/audio`
- azan.mp3
- azansubuh.mp3

## In-depth Video Tutorial
- https://youtu.be/DZGJwaeQuGA

## Special Thanks
- [@farxpeace](https://github.com/farxpeace) - for the original code
- [HomeAssistantMalaysia](https://www.facebook.com/groups/homeassistantmalaysia)
