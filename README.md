nethorologist
=============

A program to divine the current time zone, using whatever methods are
available. There are multiple means, listed in order of preference:

- Time zone information directly from an attached, live GPS
- Querying network time zone services using geolocation information from an
   attached, live GPS
- Querying network geolocation services using discovered wireless networks
   from an attached, live radio, then using this information to query network
   time zone services
- Querying network time zone services using network information based on our
   point of network ingress (last outgoing NAT)
- Asking the user


use
===

Run nethorologist --tz to get time zone output.
Run nethorologist --cc to get country code output.

components
==========

"getegress" -- determine our egress address using:
	* whatismyip.com
	* ipconfig.me
	output: a list of ip addresses. each represents some service's concept
		of our globally routable source address.


"worldweatheronline" -- determine timezone based off ip address using
	* worldweatheronline.com
	output: XML
		<?xml version="1.0" encoding="UTF-8"?>
		<data>
			<request>
				<type>IP</type>
				<query>65.182.57.205</query>
			</request>
			<time_zone>
				<localtime>2012-09-08 03:38</localtime>
				<utcOffset>-4.0</utcOffset>
			</time_zone>
		</data>
	requires: egress IP

"ipinfodb" -- determine timezone based off ip address using
	* ipinfodb (http://www.ipinfodb.com/ip_location_api.php)
	output: XML
		<?xml version="1.0" encoding="UTF-8"?>
		<Response>
			<statusCode>OK</statusCode>
			<statusMessage></statusMessage>
			<ipAddress>65.182.57.205</ipAddress>
			<countryCode>US</countryCode>
			<countryName>UNITED STATES</countryName>
			<regionName>GEORGIA</regionName>
			<cityName>ATLANTA</cityName>
			<zipCode>30308</zipCode>
			<latitude>33.749</latitude>
			<longitude>-84.388</longitude>
			<timeZone>-04:00</timeZone>
		</Response>
	requires: nothing
	http://api.ipinfodb.com/v3/ip-city/?key=<your_api_key>&ip=74.125.45.100
