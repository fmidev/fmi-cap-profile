![FMI logo](resources/fmi-logo.png)

---

# FMI CAP Profile Version 1.1.0-draft

This version:

* <https://alerts.fmi.fi/cap/profile/v1.1.0/fmi-cap-profile-v1.1.0.html>
* <https://alerts.fmi.fi/cap/profile/v1.1.0/fmi-cap-profile-v1.1.0.md> (Authoritative)

Current operative version:
* <https://alerts.fmi.fi/cap/profile/current>


## Overview

This document defines a CAP profile for warnings issued by the [Finnish Meteorological Institute](https://www.ilmatieteenlaitos.fi/). The profile extends [MetCoOp CAP profile v1.0](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md) by placing further restrictions while being 100% compatible.


## Profile versioning

This profile is versioned using semantic versioning. Changes in patch and minor versions are backwards compatible when the client implementation conforms to the compatibility rules.


## General compatibility rules

* No expectations shall be made on element order, unless explicitly specified otherwise.
* No expectations shall be made on time zone. The zone offset must always be read from the [date-time element](#date-time-elements).
* A previously unknown element value must be ignored gracefully.
* No expectations shall be made on existence of a certain element value.
* No expectations shall be made on element content intended for human audience.
* Client should be able to handle any value defined by CAP standard even when this profile defines it unused.


## Date-time elements

Date-time elements shall be presented in local time zone **Europe/Helsinki**. That is `+02:00` (EET) or `+03:00` (EEST).


## alert

**Use:** mandatory  
**MetCoOp profile:** [alert](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#alert)

The `<alert>` element is the root element of the CAP document. The `<alert>` describes a single FMI warning in all three languages (Finnish, Swedish, English) targeted at a single or multiple areas.


### identifier

**Use:** mandatory  
**MetCoOp profile:** [identifier](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#identifier)

The `<identifier>` element specifies a unique string to identify the document. The identifier is a [URN (Uniform Resource Name)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) kind of [URI (Uniform Resource Identifier)](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier), referencing to an [OID (Object identifier)](https://en.wikipedia.org/wiki/Object_identifier). The base of the OID is a WMO alerting country-msg [2.49.0.1](http://www.oid-info.com/get/2.49.0.1).

CAP alert identifier format of an FMI warning:

```
urn:oid:2.49.0.1.<country>.<authority>.<authority-specific-oid-tree>
```

| Field           | Description |
| --------------- | ----------- |
| country         | [ISO 3166-1 numeric](https://en.wikipedia.org/wiki/ISO_3166-1_numeric) country code. That is `246` for Finland. |
| authority       | National [alerting authority number](https://alertingauthority.wmo.int/) registered by WMO. That is `0` for FMI. |
| authority-specific-oid-tree | An OID tree (integers separated by period) identifying the CAP message. May contain arbitrarily long non-negative integers. |

**Compatibility rule:** Do not parse the identifier at all. It _should_ be used only as a unique string per [sender](#sender) identifying the message. The format of the identifier is subject to change in major versions, and the authority-specific-oid-tree part format is subject to change in patch versions.


### sender

**Use:** mandatory  
**MetCoOp profile:** [sender](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#sender)

The `<sender>` element content is the [WMO alerting authority](https://alertingauthority.wmo.int/) OID ([2.49.0.0](http://www.oid-info.com/get/2.49.0.0)) formatted as a URN. For FMI it is:

```
urn:oid:2.49.0.0.246.0
```


### sent

**Use:** mandatory  
**MetCoOp profile:** [sent](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#sent)

The `<sent>` element contains the publication time of the warning.


### status

**Use:** mandatory  
**MetCoOp profile:** [status](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#status)

The `<status>` element is as specified by MetCoOp profile specification.


### msgType

**Use:** mandatory  
**MetCoOp profile:** [msgType](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#msgtype)

The `<msgType>` element is as specified by MetCoOp profile specification.


### source

**Use:** omitted  
**MetCoOp profile:** [source](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#source)

The `<source>` element is omitted, as specified by the MetCoOp profile.


### scope

**Use:** mandatory  
**MetCoOp profile:** [scope](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#scope)

The `<scope>` element is as specified by MetCoOp profile specification.


### restriction

**Use:** omitted  
**MetCoOp profile:** [restriction](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#restriction)

The `<restriction>` element is omitted, as specified by the MetCoOp profile.


### code

**Use:** mandatory  
**MetCoOp profile:** [code](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#code)

The `<code>` element has multiple instances. The following codes are always included:

1. The CAP document conforms to FMI CAP profile version 1.1.0.
```
profile:cap:https://alerts.fmi.fi/cap/profile/v1.1.0
```

2. The CAP document conforms to MetCoOp CAP profile version 1.0.
```
profile:cap:https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md
```

**Compatibility rule:** Within minor versions of the FMI profile the format of the URL shall remain the same. Only the version number is subject to change reflecting the current profile version number.


### note

**Use:** omitted  
**MetCoOp profile:** [note](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#note)

The `<note>` element is omitted, as specified by the MetCoOp profile.


### references

**Use:** conditional  
**MetCoOp profile:** [references](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#references)

The `<references>` element is as specified by MetCoOp profile specification. It is _omitted_ with msgType `Alert`. With msgType `Update` or `Cancel` this element is _mandatory_ and contains references to all previously issued non-expired alerts it supersedes. References are given in the CAP standard format:

```
<sender>,<identifier>,<sent>
```


### incidents

**Use:** omitted  
**MetCoOp profile:** [incidents](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#incidents)

The `<incidents>` element is currently omitted.


## info

**Use:** mandatory  
**MetCoOp profile:** [info](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#info)

The `<info>` element has multiple instances, one localized element for each provided language in undefined order.

* Finnish
* Swedish
* English


### language

**Use:** mandatory  
**MetCoOp profile:** [language](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#language)

The `<language>` element has one of the following values:

| Language name | `<language>` |
| ------------- | ------------ |
| Finnish       | fi-FI        |
| Swedish       | sv-FI        |
| English       | en-GB        |


### category

**Use:** mandatory  
**MetCoOp profile:** [category](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#category)

The `<category>` element value is always:

```
Met
```


### event

**Use:** mandatory  
**MetCoOp profile:** [event](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#event)

The `<event>` element value is a fixed localized string determined by [FMI event code](#eventcode). Possible values are listed in following table.

| Event code        | `<event>` Finnish          | `<event>` Swedish               | `<event>` English           |
| :---------------- | :------------------------- | :------------------------------ | :-------------------------- |
| coldWeather       | Pakkasvaroitus             | Varning för köld                | Cold warning                |
| forestFireWeather | Maastopalovaroitus         | Varning för terrängbrand        | Wildfire warning            |
| hotWeather        | Hellevaroitus              | Varning för värmebölja          | Heat wave warning           |
| pedestrianSafety  | Jalankulkusää              | Fotgängarvädret                 | Pedestrian weather warning  |
| rain              | Sadevaroitus               | Nederbördsvarning               | Heavy rain warning          |
| seaIcing          | Jäätämisvaroitus           | Varning för nedisning av fartyg | Ice accreation warning      |
| seaThunderstorm   | Raju ukonilma              | Varning för våldsamt åskväder   | Severe thunderstorm warning |
| seaWaterHeight    | Merivedenkorkeusvaroitus   | Varning för vattenstånd         | Sea level warning           |
| seaWaveHeight     | Aallokkovaroitus           | Varning för hård sjögång        | Wave height warning         |
| seaWind           | Tuulivaroitus merelle      | Vind varning för sjöområden     | Wind warning for sea area   |
| thunderstorm      | Raju ukonilma              | Varning för våldsamt åskväder   | Severe thunderstorm warning |
| trafficWeather    | Liikennesää                | Trafikvädret                    | Traffic weather warning     |
| uvNote            | UV-tiedote                 | UV-meddelande                   | UV advisory                 |
| wind              | Tuulivaroitus maa-alueille | Vindvarning för landområden     | Wind warning for land areas |

**Compatibility rule:** Do not determine the event from the contents of the `<event>` element. Instead, use [`<eventCode>`](#eventcode) with `<valueName>` referring to this profile. Use contents of this element to display the event to the end user. The `<event>` content is subject to change in patch versions.


### responseType

**Use:** omitted  
**MetCoOp profile:** [responseType](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#responsetype)

The `<responseType>` element is currently omitted.


### urgency

**Use:** mandatory  
**MetCoOp profile:** [urgency](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#urgency)

The `<urgency>` element value is determined from the duration between [\<sent>](#sent) and [\<onset>](#onset). The following table describes the threshold for each urgency value.

| Distance (h) | `<urgency>` |
| :----------: | :---------- |
| _x_ < 1      | Immediate   |
| 1 ≤ _x_ < 6  | Expected    |
| 6 ≤ _x_      | Future      |

**Compatibility rule:** The distance threshold values may change in minor versions.

### severity

**Use:** mandatory  
**MetCoOp profile:** [severity](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#severity)

The `<severity>` element content is mapped 1:1 with the [colour code system](https://en.ilmatieteenlaitos.fi/information-on-warnings) used by FMI. The mapping is presented in the following table.

| Colour | `<severity>` |
| :----- | :----------- |
| Green  | Minor        |
| Yellow | Moderate     |
| Orange | Severe       |
| Red    | Extreme      |


### certainty

**Use:** mandatory  
**MetCoOp profile:** [certainty](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#certainty)

The `<certainty>` element content is mapped from FMI warning probability (see [Numeric parameters](#numeric-parameters)) by the CAP specification.

| Probability | `<certainty>` |
| ----------: | :-------------|
| >50%        | Likely        |
| ≤50%        | Possible      |

Following `<certainty>` values are never used:

* Observed
* Unlikely
* Unknown (as mandated by MetCoOp profile)

**Compatibility rule:** The probability threshold values may change in minor versions.


### audience

**Use:** omitted  
**MetCoOp profile:** [audience](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#audience)

The `<audience>` element is omitted, as specified by the MetCoOp profile.


### eventCode

**Use:** mandatory  
**MetCoOp profile:** [eventCode](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#eventcode)

The `<eventCode>` element has a single instance. Its `<valueName>` is always:

```
profile:cap:https://alerts.fmi.fi/cap/profile/v1.1.0
```

The `<value>` is one of the values in the table below. See [event](#event) for code descriptions.

| `<value>`         |
| :---------------- |
| coldWeather       |
| forestFireWeather |
| hotWeather        |
| pedestrianSafety  |
| rain              |
| seaIcing          |
| seaThunderstorm   |
| seaWaterHeight    |
| seaWaveHeight     |
| seaWind           |
| thunderstorm      |
| trafficWeather    |
| uvNote            |
| wind              |

**Compatibility rule:** Use `<eventCode>` with `<valueName>` referring to this profile to determine the event type instead of [`<event>`](#event). Codes may be removed (not used anymore) in minor versions. New event codes may be added in major versions.


### effective

**Use:** omitted  
**MetCoOp profile:** [effective](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#effective)

The `<effective>` element is omitted, as specified by the MetCoOp profile.


### onset

**Use:** mandatory  
**MetCoOp profile:** [onset](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#onset)

The `<onset>` element is as specified by MetCoOp profile specification.


### expires

**Use:** mandatory  
**MetCoOp profile:** [expires](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#expires)

The `<expires>` element is as specified by MetCoOp profile specification.


### senderName

**Use:** mandatory  
**MetCoOp profile:** [senderName](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#sendername)

The `<senderName>` element content is the official localized name of FMI.


### headline

**Use:** mandatory  
**MetCoOp profile:** [headline](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#headline)

The `<headline>` element is as specified by MetCoOp profile specification. The content is localized.


### description

**Use:** mandatory  
**MetCoOp profile:** [description](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#description)

The `<description>` element is as specified by MetCoOp profile specification. The content is localized.


### instruction

**Use:** omitted  
**MetCoOp profile:** [instruction](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#instruction)

The `<instruction>` element is currently omitted.


### web

**Use:** mandatory  
**MetCoOp profile:** [web](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#web)

The `<web>` element content is a URL linking to the localized warnings front page on the FMI website.


### contact

**Use:** mandatory  
**MetCoOp profile:** [contact](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#contact)

The `<contact>` element content is a URL linking to the contact information page on the FMI website.


### parameter

**Use:** mandatory  
**MetCoOp profile:** [parameter](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#parameter)

The `<parameter>` element has multiple instances.

#### Colour parameter

**Use:** mandatory  
**`<valueName>`** color (_note the spelling_)

Colour code indicating the severity of the awareness level. Possible values are listed in the table below.

| `<value>` | Description                 |
| :-------- | :-------------------------- |
| green     | no major danger (not used)  |
| yellow    | dangerous weather may occur |
| orange    | dangerous weather           |
| red       | very dangerous weather      |


#### Numeric parameters

**Use:** conditional  
**`<valueName>`** _see table below_

The existence of numeric parameters depends on the warning being issued. The table below lists possible parameters, the parameter value format, accompanying unit of measure parameter and [event codes](#eventcode) the parameter is applicable with.

The numeric parameter value is either an integer or a decimal number. In the table below the number of decimals is presented in parentheses in the _`<value>` format_ column. The value is always formatted in `en_US` locale regardless of the info locale to ensure compatibility with automated systems.

Most numeric parameters are accompanied by a parameter denoting a unit of measure (uom). Possible unit values for each parameter are listed in the _UOM `<value>`_ column of the table below.

| Parameter      | `<valueName>` | `<value>` format | UOM `<valueName>` | UOM `<value>`  | Applicable events  |
| :------------- | :-------------| :--------------- | :---------------- | :------------- | :----------------- |
| Precipitation  | precipitation | integer          | precipitationUom  | mm/h <br> mm/d | rain               |
| Probability    | probability   | integer          | probabilityUom    | %              | _(optionally any)_ |
| Temperature    | temperature   | integer          | temperatureUom    | °C             | hotWeather         |
| UV index       | uvIndex       | integer          | _n/a_             | _n/a_          | uvNote             |
| Wave height    | waveHeight    | decimal (1)      | waveHeightUom     | m              | seaWaveHeight      |
| Wind direction | windDirection | integer          | windDirectionUom  | °              | seaThunderstorm <br> seaWind <br> thunderstorm <br> wind |
| Wind intensity | windIntensity | integer          | windIntensityUom  | m/s            | seaThunderstorm <br> seaWind <br> thunderstorm <br> wind |


#### Warning cause parameter

**Use:** conditional  
**`<valueName>`** eventCause

Warnings may contain zero or more associated causes. Possible values are listed in the table below with [event codes](#eventcode) the value is  applicable with. If a warning has multiple causes, all existing values are listed in unspecified order in the `<value>` element separated by a whitespace. On zero causes the parameter is omitted.

| `<value>`              | Applicable events                    |
| :--------------------- | :----------------------------------- |
| bitingFrost            | coldWeather                          |
| blowingSnow            | trafficWeather                       |
| driftingSnow           | trafficWeather                       |
| fallingTemperature     | trafficWeather                       |
| fog                    | trafficWeather                       |
| freezingRain           | trafficWeather                       |
| freezingDrizzle        | trafficWeather                       |
| highWater              | seaWaterHeight                       |
| hoarfrostAffectedRoads | trafficWeather                       |
| iceCoveredRoads        | trafficWeather                       |
| rain                   | pedestrianSafety                     |
| risingTemperature      | trafficWeather                       |
| shallowWater           | seaWaterHeight                       |
| sleet                  | trafficWeather                       |
| slushCoveredRoads      | trafficWeather                       |
| snow                   | pedestrianSafety <br> trafficWeather |
| snowCoveredRoads       | trafficWeather                       |
| snowOnIce              | pedestrianSafety                     |
| snowOrSleet            | trafficWeather                       |
| snowRuttedRoads        | trafficWeather                       |
| snowstorm              | trafficWeather                       |
| strongWind             | trafficWeather                       |
| tamping                | pedestrianSafety                     |
| tightFrost             | coldWeather                          |
| waterOnIce             | pedestrianSafety                     |


#### Typical impacts parameter

**Use:** conditional  
**`<valueName>`** typicalImpacts

The `<value>` content is a localized description of the typical impacts of the event. This parameter is included whenever such description exists, otherwise omitted.


#### Other parameters

The `eventEndingTime` parameter suggested by MetCoOp CAP profile is currently omitted.


### resource

**Use:** omitted  
**MetCoOp profile:** [resource](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#resource)

The `<resource>` element is currently omitted.


## area

**Use:** mandatory  
**MetCoOp profile:** [area](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#area)

The `<area>` element is as specified by MetCoOp profile specification. See description of child elements in this profile for further details.


### areaDesc

**Use:** mandatory  
**MetCoOp profile:** [areaDesc](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#areadesc)

The `<areaDesc>` element contains the official localized name of the area in the language of the surrounding `<info>` element. If no localized name exists, official name in sender language shall be used. If area has no official name (e.g. arbitrary free-hand polygons), this element contains a comma+space (`', '`) separated list of named areas that overlap the polygon with at least 20% coverage.


### polygon

**Use:** mandatory  
**MetCoOp profile:** [polygon](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#polygon)

The `<polygon>` element is as specified by MetCoOp profile specification.


### circle

**Use:** omitted  
**MetCoOp profile:** [circle](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#circle)

The `<circle>` element is currently omitted.


### geocode

**Use:** conditional  
**MetCoOp profile:** [geocode](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#geocode)

The `<geocode>` element is used when a proper value exists in the code sets listed in the table below. If a value exists in multiple code sets, an element is created for each code set. When no code exists, the geocode element is omitted.

| `<valueName>`  | `<value>` description |
| :------------- | :-------------------- |
| ISO 3166-2     | [ISO 3166-2:FI](https://fi.wikipedia.org/wiki/ISO_3166-2:FI) county code. |
| FI-kuntanumero | Finnish municipality number ([kuntanumero](https://fi.wikipedia.org/wiki/Kuntanumero)), declared in [kuntaluettelo](https://dvv.fi/haku/-/q/kuntaluettelo) (municipality directory) published by [Digi- ja väestötietovirasto](https://dvv.fi). |
| METAREA        | Baltic sub-areas declared in [WMO No. 9 Volume D Information for Shipping](https://community.wmo.int/activity-areas/operational-information-service/volume-d-information-shipping). |


### altitude

**Use:** omitted  
**MetCoOp profile:** [altitude](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#altitude)

The `<altitude>` element is currently omitted.


### ceiling

**Use:** omitted  
**MetCoOp profile:** [ceiling](https://git.smhi.se/metcoop/metcoop-cap-profile/blob/version-1.0/metcoop-cap-profile.md#ceiling)

The `<ceiling>` element is currently omitted.
