# Kentik Netbox Integration

Kentik and Netbox have announced the beginning of  a series of integrations between products. This initial integration takes advantage of both the flexibility of the Kentik UI and the ability of Netbox to allow the customer to create custom links for objects within its database.

For example, while in Netbox looking at a network device, the customer can have a custom Kentik “button” that will allow the customer to launch that device into a few different views within the Kentik UI.

When a view is selected, the current device will be launched into an existing authenticated Kentik browser window into a specific dashboard or device view.

This custom button/link capability will work for any data type that overlaps both Kentik and Netbox data structures. This will include Devices, Sites and ASNs to start.

## Example Netbox Configuration
  
In our example configuration we’ll show you how to configure a custom link that will “launch” a selected device from the Netbox device page into a IP Netflow overview page for the device in Kentik.

To configure Netbox, navigate to Customization then to Custom Links. Note: with older Netbox versions this may be in Other then Custom Links. Next, click the “+” to add a custom link. When selected, you will be presented with a page that gives you all the options to fill out:


**Name:** This will be the name of the link object you are creating

**Content Types:** This is the specific Netbox data type that you will apply this custom link to. In our case, we want the button to appear on the Netbox “devices” page, so we are going to choose DCIM > Device.

  

**Weight:** (from the Netbox documentation) *“A numeric weight used to override alphabetic ordering of links by name. Custom fields with a lower weight will be listed before those with a higher weight. (Note that weight applies within the context of a custom link group, if defined.)”*

**Group Name:** If you have multiple links that will apply to an object type (devices in our case) we can create a group wich will present a single button that, when selected, will display a dropdown of all the available custom links. This name will appear on the Button.

**Button Class:** The color of the button

**Enabled:** Is this custom link enabled for use?

**New Window:** When selected this will launch the custom link into a new browser window/tab

**Link Text:**  This will be the text displayed on the link

**Link URL:**  The Kentik UI URL to open when selecting the custom link. NOTE: You will notice that Netbox is making use of Jinja templating here to extract the Netbox object name and insert it into the URL. There are differences in the formatting between before and after v3.5 of Netbox noted below.

Here is a text version of the link in the image above:
```
https://portal.kentik.com/v4/core/quick-views/devices/{{ object }}/traffic
```

### v3.5 Netbox API Changes

In Netbox version **3.2.0** the `{{ object }}` nomenclature was added and the '{{ obj.name }}' was kept for backwards compatibility, however, in Netbox version **3.5.0** Netbox dropped the use of `{{ obj.name }}`.

### Kentik UI URLs

#### Devices

Network explorer overview (Netflow)
```
https://portal.kentik.com/v4/core/quick-views/devices/{{ object }}/traffic
```

NMS Device Dashboard (NMS/Metrics)
```
https://portal.kentik.com/v4/library/dashboards/24315/guided?device={{ object }}
```

#### Sites

Network Explorer Sites Overview (Netflow)
```
https://portal.kentik.com/v4/core/quick-views/sites/{{ object }}/traffic
```

#### ASN
ASN Network Explorer Overview (Netflow)
```
https://portal.kentik.com/v4/core/quick-views/asn/{{ object }}/traffic
```

#### IP Prefix
IP Prefix Network Explorer Overview (Netflow)
```
https://portal.kentik.com/v4/core/quick-views/route-prefix/{{ object }}%20(%20-%20)
```

#### IP Address
IP Address Network Explorer Overview (Netflow)
```
https://portal.kentik.com/v4/core/quick-views/ip/{{ object }}/traffic
```





