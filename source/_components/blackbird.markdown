---
layout: page
title: "Blackbird 8x8 HDMI Matrix Switch"
description: "Instructions on how to integrate Monoprice Blackbird 4k 8x8 HDBaseT Matrix Switch into Home Assistant."
date: 2018-03-29 16:35
sidebar: true
comments: false
sharing: true
footer: true
logo: monoprice.svg
ha_category: Media Player
ha_release: 0.68
ha_iot_class: Local Polling
redirect_from:
 - /components/media_player.blackbird/
---

The `blackbird` platform allows you to control [Monoprice Blackbird Matrix Switch](https://www.monoprice.com/product?p_id=21819) using a serial connection.

To add a Blackbird device to your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
media_player:
  - platform: blackbird
    port: /dev/ttyUSB0
    zones:
      1:
        name: Living Room
    sources:
      3:
        name: BluRay
```

{% configuration %}
port:
  description: The serial port to which Blackbird matrix switch is connected. [`port`](#port) and [`host`](#host) cannot be specified concurrently.
  required: exclusive
  type: string
host:
  description: The IP address of the Blackbird matrix switch. [`port`](#port) and [`host`](#host) cannot be specified concurrently.
  required: exclusive
  type: string
zones:
  description: This is the list of zones available. Valid zones are 1, 2, 3, 4, 5, 6, 7, 8. Each zone must have a name assigned to it.
  required: true
  type: integer
  keys:
    name:
      description: The name of the zone.
sources:
  description: The list of sources available. Valid source numbers are 1, 2, 3, 4, 5, 6, 7, 8. Each source number corresponds to the input number on the Blackbird matrix switch. Similar to zones, each source must have a name assigned to it.
  required: true
  type: integer
  keys:
    name:
      description: The name of the source.
{% endconfiguration %}

### {% linkable_title Service `media_player.blackbird_set_all_zones` %}

Set all zones to the same input source. This service allows you to immediately synchronize all the TVs in your home. Regardless of `entity_id` provided, all zones will be updated.

| Service data attribute | Optional | Description |
| ---------------------- | -------- | ----------- |
| `entity_id` | yes | String that points at an `entity_id` of a zone.
| `source` | no | String of source name to activate.
