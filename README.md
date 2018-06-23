# Iframe state card for [Home Assistant](https://home-assistant.io)

<img src="https://i.imgur.com/rwFiDcq.gif" height="500">

KNOWN PROBLEMS: CSS and code could be better arranged, scalling on page zoom/resize could be better.

## Installation
* Download `/www/custom_ui/state-card-iframe.html` to `<your-hass-configuration-dir>/www/custom_ui/` (create the folder structure if you don't have it - mind the permissions)
* Add it to your `configuration.yaml`:
```yaml
frontend:
  extra_html_url:
    - /local/custom_ui/state-card-iframe.html
```
* Create one or more template sensors, binary_sensor(s), input_text(s) etc. in your `configuration.yaml`. E.g.:
```yaml
sensor:
  - platform: template
    sensors:
      iframe:
        value_template: iframe
      iframe2:
        value_template: iframe
```
* Add your sensor to a group.. E.g.:
```yaml
group:
  group_iframe:
    name: ' '   > in this format the iframe will not have a name above
    entities:
      - sensor.iframe
  group_iframe2:
    name: 'Name'   > with a name
    entities:
      - sensor.iframe2
```
* Customize your newly created sensor in the `customize` section or your `customize.yaml` file:

The scale, height and scale _should_ create the right size for the iframes. Iframes are a bit finicky to work with and sometimes the content they show don't scale properly.
```diff
- All options are mandatory!
```

```yaml
  customize:
    sensor.iframe:
      custom_ui_state_card: state-card-iframe
      config:
        height: 490    > in pixels, height of the iframe (more work needed)
        width: 108     > in %, width of the iframe (more work needed)
        scale: 1       > scales up or down the content of the iframe (it affects both the height and the width)
        url: https://www.youtube.com/embed/tgbNymZ7vqY    > url of the resource (**please note that some websites won't allow iframe embeding**)
    sensor.iframe2:
      custom_ui_state_card: state-card-iframe
      config:
        height: 350
        width: 108
        scale: 1
        url: https://embed.windy.com/embed2.html
 ```
## For [Lovelace](https://gist.github.com/ciotlosm/9508388876edf92c4c1f3579e740fbd5)
Download `/www/custom_ui/lovelace-iframe.html` to `<your-hass-configuration-dir>/www/custom_ui/` and add the following in your configuration.

```
frontend:
  extra_html_url:
  - /local/lovelace-iframe.html
```

```
# Example ui-lovelace.yaml. Create this file as <config>/ui-lovelace.yaml. Title is optional, height is recommended.
views:
- name: Iframe
  cards:
  - type: "custom:lovelace-iframe"
    height: 550
    title: Weather
    url: https://embed.windy.com/embed2.html?lat=48.234&lon=8.598&zoom=5&level=surface&overlay=radar&menu=&message=&marker=&calendar=&pressure=&type=map&location=coordinates&detail=&detailLat=48.234&detailLon=8.598&metricWind=default&metricTemp=default&radarRange=-1
```

## Changelog
```
Version 20180623:
Added lovelace custom card
Version 20180206:
Disabled more info card
Version 20180129:
Added functionality to prevent scrolling in the iframe (e.g. for embedded maps). To enable scrolling, click once.
```
