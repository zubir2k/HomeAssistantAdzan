![Home Assistant Adzan](https://user-images.githubusercontent.com/1905339/170957516-6173d318-2600-4372-bc19-b13e224272de.png)\
[![Repo](https://img.shields.io/badge/zubir2k-repository-brightgreen?logo=github)](https://zubirco.de/) 
[![Donate](https://img.shields.io/badge/donate-Coffee-yellow.svg)](https://zubirco.de/buymecoffee)

Automation for Malaysia Adzan (Muslim call to prayer) based on the following sources:
- JAKIM Official (eSolat) - [Website](https://www.e-solat.gov.my).
- AzanPro - [Website](https://api.azanpro.com).
- Home Assistant Official Islamic Prayer Time - [Website](https://www.home-assistant.io/integrations/islamic_prayer_times).

**Whats New in v4**
- Fully revamped eSolat sensors.
- Easy install with minimal configuration.
- Prayer time sensor will show in timestamp format. 12/24hours format are now in attributes.
- Automation are now created by default automatically. However, you may choose to create your own.
- Dynamic Media Player selector.
- Added support the official Home Assistant Islamic Prayer Time
- Volume Slider Control based on the selected speaker/media_players
- Version checker & updater (NOTE: The updater will only update essential files only).

**The Default Automation will perform the following:**
- Play TTS (for Google) or Play audio TTS (for Alexa)
- Play Azan
- Send Persistent Notification (Azan & 15min Reminder)
- Send default Notification (notify.notify)

## Screenshot
![image](https://user-images.githubusercontent.com/1905339/154905774-b63319d5-4b4b-46e5-9fab-8efdeeb10400.png)

![image](https://github.com/zubir2k/HomeAssistantAdzan/assets/1905339/edf6e02f-d883-4bcd-860b-1a0adcf85213)

![image](https://github.com/zubir2k/HomeAssistantAdzan/assets/1905339/83adcf9b-b3be-486e-872f-13c3a8136acd)

![lovelace-dashboard](https://user-images.githubusercontent.com/1905339/196147059-341c5e1d-17af-4d88-b9de-a0932759dc85.png)

![image](https://github.com/zubir2k/HomeAssistantAdzan/assets/1905339/f8a19c2a-dedf-45a1-905a-af0d4110d043)

## Video Tutorial

[![Youtube](https://user-images.githubusercontent.com/1905339/197347154-463881c9-dfdb-4dbb-ae03-5764022a0a84.png)](https://youtu.be/SVzybCpjWGQ)

- Automation Adzan using Home Assistant: https://youtu.be/SVzybCpjWGQ
- Beginners Guide to Home Assistant: https://youtu.be/-jyegp-mL20 

## Installation
### 1. Copy all files
- Browse into your Home Assistant directory and paste all files into `\config` and `\media`.

### 2. Add eSolat into [configuration.yaml](configuration.yaml)
- Add the following line into the config file

```yaml
homeassistant:
  packages: !include_dir_named HAMY/
```

- Restart Home Assistant to take effect.

### 3. Dashboard [lovelace-ui.yaml](lovelace-ui.yaml)
- Add new card, scroll at the bottom and choose Manual. 
- Copy & paste the YAML respectively.

![image](https://user-images.githubusercontent.com/1905339/196153827-56e67de2-1591-46aa-9b10-090d5dfb9633.png)

## Configure eSolat
### 1. Source
- Select source (Jakim/AzanPro/Local/Islamic Prayer Time)
- Enter state code (not applicable for Islamic Prayer Time) -- Refer state code [here](https://www.e-solat.gov.my/index.php?siteId=24&pageId=50). 
- For Islamic Prayer Time, please ensure to complete the configuration in the Home Assistant Integration menu

### 2. Azan Audio & Automation
- Select your preferred media player 
- Choose your automation (Google or Alexa). Select Custom if you wish to use your own automation.
- **For Google**, please enter `azan.mp3` and `azansubuh.mp3` as your audio files. You may use your own mp3 stored in your `\media` folder.
- **For Alexa**, please enter your `home_url`. **IMPORTANT**: Please ensure [Alexa_Media_Player](https://github.com/custom-components/alexa_media_player) addon has been configured.

### 3. Refresh
- Click here 
[![Open your Home Assistant instance and show your automations.](https://my.home-assistant.io/badges/automations.svg)](https://my.home-assistant.io/redirect/automations/) to open your automation panel.
- Run `Azan Yearly Update`

> ![image](https://user-images.githubusercontent.com/1905339/211257538-94f8e7fb-60dc-4fa9-a355-5e5ea887ece6.png)

- Press both Online and Local sensors to take effect. 

## Automation Ideas
There are many ways that you can benefit from the prayer time sensors.

### 1. Execute action upon x minute **before** prayer time.
Example: 15min before Maghrib, play random surah. `15*60` where 15 is in minutes.

```yaml
{{ state_attr('sensor.solat_maghrib', '24hours') == (now().strftime('%s') | int + 15*60) | timestamp_custom("%H:%M", false) }}
```

### 2. Random play audio
Example: Random play Surah before/after azan.

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

### 3. Others
Send notification to any Android TVs and perhaps then shutting off the TV. \
Example: Alert family to get ready for Maghrib. Then turn off the TV 😁

## Special Thanks
- [@farxpeace](https://github.com/farxpeace) - for the original integration code for AzanPro
- [HomeAssistantMalaysia](https://www.facebook.com/groups/homeassistantmalaysia)

*You may also try [GPS Based](https://github.com/zubir2k/HomeAssistantEsolatGPS) Solat sensor using Appdaemon. (API provided by MPT)*

## ⚠ Disclaimer
THIS IS NOT AN INTEGRATION ADD-ON ([issue#3](https://github.com/zubir2k/HomeAssistantAdzan/issues/3)). THIS IS A TEMPLATE THAT CREATES SENSORS AND AUTOMATION FOR ADZAN PRAYER.
