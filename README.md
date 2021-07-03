# Home Assistant Adzan
Automation for Malaysia Adzan (Muslim call to prayer) based on JAKIM standards.
Prayer time data is pulled via API call from AzanPro (https://api.azanpro.com/).

## Installation
### 1. [configuration.yaml](configuration.yaml)
Copy the sensors to your current configuration.yaml
Change the location code based on this list https://api.azanpro.com/zones

### 2. [automation.yaml](automations.yaml)
Copy 3 automations into your current automations.yaml
- Adzan
- Adzan Subuh
- Daily refresh

### 3. [lovelace.yaml](lovelace.yaml)
Add new entities card on your dashboard and paste the YAML codes.

## MP3 Audio Files
Copy 2 audio files into your /media/audio/
- azan.mp3
- azansubuh.mp3

## Special Thanks
- [@farxpeace](https://github.com/farxpeace) - for the original code
- [HomeAssistantMalaysia](https://www.facebook.com/groups/homeassistantmalaysia)
