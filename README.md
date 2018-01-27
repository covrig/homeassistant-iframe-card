# Iframe state card for [Home Assistant](https://home-assistant.io)

<img src="https://i.imgur.com/rwFiDcq.gif" height="500">

KNOWN PROBLEMS: CSS is a mess, code is a mess, weird scaling due the the width being give in percents

## Installation
* Download `/www/custom_ui/state-card-iframe.html` to `<your-hass-configuration-dir>/www/custom_ui/` (create the folder structure if you don't have it - mind the permissions)
* Add it to your `configuration.yaml`:
```yaml
frontend:
  extra_html_url:
    - /local/custom_ui/state-card-iframe.html
```
* Create one or more sensors, binary_sensor(s), input_text(s) etc. in your `configuration.yaml`. E.g.:
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

## Changelog
Version 20180128:
```
- Start!
```
