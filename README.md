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
