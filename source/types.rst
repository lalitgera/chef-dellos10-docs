##############################
Dell EMC Networking Chef types
##############################

The Dell EMC Networking Chef types facilitate device provisioning running Dell EMC Networking OS10 software. This information describes the Chef types and attributes available in Dell EMC Networking Chef module.

Type: os10_route
****************

The ``os10_route`` resource type is used to manage static routes in OS10 Enterprise Edition switches.

**Attributes**

==============      ================================================
Attribute           Description 
==============      ================================================
``route_ip``        Target IP address to which the route must be configured
                    This is the name property of os10_route resource
``next_hop``        List of the next-hop IP address for the route to be configured
==============      ================================================

Type: os10_snmp
***************

The ``os10_snmp`` resource type is to used to manage SNMP configuration in OS10 EE switches. 
The os10_snmp resource is not an ensurable type and hence does not have an ensure attribute.

**Attributes**

=====================           ================================================
Attribute                       Description
=====================           ================================================
``community``                   This property is a dictionary of community string with its access right; will be the only list of community string entries present in the SNMP configuration (for example, ``{'public'=>'ro', 'private'=>'rw'}``
``contact``                     Contact property of SNMP server; there can be only one entry for contact, and an empty string for contact will remove the contact entry from the SNMP configuration
``location``                    Location property of the SNMP server; there can be only one entry for location, and an empty string for location will remove the location entry
``traps``                       Dictionary of entries where the key is trap category and values are the list of subcategory
``host``                        Dictionary of entries where the key is list of ip, port, version and community string
=====================           ================================================


Type: os10_monitor
******************

The ``os10_monitor`` resource type is to used to manage port monitor (mirroring) session configuration in OS10 Enterprise Edition switches.

**Attributes**

====================           ================================================   
Attribute                      Description                                     
====================           ================================================
 ``port_id``                   Configures the monitor session ID in the switch (1 to 18); this is the name property of os10_monitor resource 
 ``source``                    Conifgures the source interfaces for this monitoring session (for example, ['ethernet 1/1/9', 'ethernet 1/1/10']) 
 ``destination``               Configures the destination interface to which traffic has to be mirrored (for example, 'ethernet 1/1/10') 
 ``flowbase``                  Enables or disable flow-based monitoring (true, false); this optional value defaults to false 
 ``shutdown``                  Enables or disables the monitoring session; if the shutdown is false, the session will be configured but in shutdown state; this operational value defaults to true 
====================           ================================================

Type: os10_interface
********************

The ``os10_interface`` resource type is used to manage interface configuration in OS10 Enterprise Edition switches.

**Attributes**

====================          ==================================================
Attribute                     Description
====================          ==================================================
``interface_name``            Configures the interface name; this is the name property for os10_interface resource 
``desc``                      Configures the description of the interface 
``mtu``                       Configures the maximum transmission unit (MTU) of the interface 
``switchport_mode``           Configures the switchport mode of the interface (either trunk or access in case of switchport; trunk, access, absent); can be false when not in L2 mode 
``admin``                     Configures the administrative state of the interface (up, down) 
``ip_address``                Configures the IPv4 address and mask of the interface in ip/prefixlen format 
``ipv6_address``              Configures the IPv6 address and mask of the interface in ip/prefixlen format 
``ipv6_autoconfig``           Enables or disables IPv6 autoconfig (true, false) 
``ip_helper``                 Specifies a string of IP addresses for the interface to which UDP broadcasts need to be forwarded to 
``portmode``                  Configures the port mode according to the device type 
``suppress_ra``               Configures IPv6 router advertisements if set to true (true, false) 
====================          ==================================================

Type: os10_image_upgrade
************************

The ``os10_image_upgrade`` resource type is used to upgrade / downgrade OS10EE images by providing the filename and location of the image.

**Attribute**

====================          ==================================================
Attribute                     Description                                      
====================          ==================================================
``url``                       Configures the location of the binary image in the remote server; image will be downloaded and installed in the standby partition of the switch
====================          ================================================== 

Type: os10_bgp
**************

The resource definition for os10_bgp that is used to configure base bgp configuration in OS10 Enterprise Edition switches.

**Attributes**

==================================               ==================================================
Attribute                                        Description                                   
==================================               ==================================================
``asn_num``                                      Configures the autonomous system (AS) number of the BGP configuration (1 to 4294967295 or 0.1 to 65535.65535)
``bestpath_as_path``                             Configures the bestpath selection to either ignore or include prefixes received from different AS paths during multipath calculation 
``bestpath_ignore_router_id``                    Configures bestpath computation to ignore router identifier 
``bestpath_med_confed``                          Configures bestpath to compare MED among confederation paths 
``bestpath_med_missing_as_worst``                Configures bestpath to treat missing MED as the least preferred one 
``fast_external_fallover``                       Configures reset session if a link to a directly connected external peer goes down 
``log_neighbor_changes``                         Configures logging of neighbors up/down 
``max_path_ebgp``                                Configures the maximum number of paths to forward packets through eBGP (1 to 128) 
``max_path_ibgp``                                Configures the maximum number of paths to forward packets through iBGP (1 to 128) 
``outbound_optimization``                        Enables outbound optimization for IBGP peer-group members 
``router_id``                                    Configures the IP address of the local BGP router instance 
==================================               ==================================================

Type: os10_bgp_af
*****************

**Attributes**

==============================                   ===============================
Attribute                                        Description                                             
==============================                   ===============================
``asn_num``                                      Configures the AS number of the BGP configuration (1 to 4294967295 or 0.1 to 65535.65535)
``address_family``                               Specifies the address family mode (ipv4, ipv6)
``default_metric``                               Sets the default metric of redistributed routes (1 to 4294967295)
``network_add_list``                             Specifies a list of IPs and masks along with optional route-map string
``redistribute_connected``                       Configures connected routes to be redistributed into BGP
``redistribute_ospf``                            Configures OSPF routes to be redistributed into BGP
``redistribute_static``                          Configures static routes to be redistributed into BGP
==============================                   ===============================

Type: os10_bgp_nbr
******************

**Attributes**

==============================                   ===============================
Attribute                                        Description    
==============================                   ===============================
``asn_num``                                      Configures the AS number of the BGP configuration (1 to 4294967295 or 0.1 to 65535.65535)
``associate_peer_group``                         Specifies the inherit configuration of a peer-group; peer-group property should be configured first before configuring this property
``advertisement_interval``                       Specifies the minimum interval between sending BGP routing updates; (1 to 600; default 30)
``advertisement_start``                          Sets the delay initiating OPEN message for the specified time
``connection_retry_timer``                       Sets the delay initiating OPEN message for the specified time (0 to 240)
``password``                                     Specifies the MD5 password for authentication (up to 128 characters)
``peer_config``                                  Specifies the neighbor router address
``remote_as``                                    Specifies the AS number of the BGP neighbor
``remove_private_as``                            Enables or disables configuration to remove private AS number from outbound updates
``send_community_ext``                           Enables or disables sending extended community attribute
``send_community_std``                           Enables or disables sending standard community attribute
``shutdown``                                     Sets the shutdown state of the neighbor
``timers``                                       Specifies the array of two timer values - keepalive interval and holdtime values; keepalive value should be between 1-65535 with default of 60; holdtimer value should be between 3-65535 with default of 180
``address_family``                               Specifies the address family mode (ipv4, ipv6 unicast)
``allowas_in``                                   Specifies to allow local AS number in as-path (1 to 10)``af_activate`` | Enables the address family for this neighbor
``af_activate``                                  Enables the address family for this neighbor
==============================                   ===============================

Type: os10_bgp_nbr_group
************************

**Attributes**

==================================               ===============================
Attribute                                        Description                                            
==================================               ===============================
``asn_num``                                      Specifies the AS number of the BGP configuration (1 to 4294967295 or 0.1 to 65535.65535 
``advertisement_interval``                       Specifies the minimum interval between sending BGP routing updates (1 to 600; default 30) 
``advertisement_start``                          Sets the delay initiating OPEN message for the specified time (0 to 240) 
``connection_retry_timer``                       Configures the peer connection retry timer (10 to 65535; default 60) 
``password``                                     Sets the MD5 password for authentication (up to 128 characters) 
``peer_group_config``                            Specifies the neighbor template name 
``remote_as``                                    Specifies the AS number of the BGP neighbor 
``remove_private_as``                            Enables or disables configuration to remove private AS number from outbound updates 
``send_community_ext``                           Enables or disables sending extended community attribute 
``send_community_std``                           Enables or disables sending standard community attribute 
``timers``                                       Specifies the keepalive interval and holdtime values; keepalive value should be between 1 to 65535 with default value of 60; hold timer should be between 3 to 65535 with default value of 180 
``address_family``                               Specifies the address family mode (ipv4 or ipv6 unicast) 
``af_activate``                                  Enables the address family for this neighbor 
==================================               ===============================

Type: os10_lldp
***************

The ``os10_lldp`` resource type is to used to manage global LLDP configuration in OS10 EE switches. The os10_lldp resource is not an ensurable type and hence does not have an ensure attribute.

**Attributes**

==================================               ===============================
Attribute                                        Description   
==================================               ===============================
``holdtime_multiplier``                          Configures the holdtime multiplier (2 to 10); an empty string will remove the holdtime multiplier value from the LLDP configuration 
``reinit``                                       Configures the reinit value (1 to 10); an empty string will remove the reinit value from the LLDP configuration 
``timer``                                        Configures the timer value (5 to 254); an empty string will remove the timer value from the LLDP configuration 
``med_fast_start_repeat_count``                  Configures the med fast start repeat count (1 to 10); an empty string will remove the med fast start repeat count value from the LLDP configuration 
``enable``                                       Enables or disables LLDP globally (true, false) 
``med_network_policy``                           Configures the med network policy with a set of hash keys id<1-32>, app, vlan_id<1-4093>, vlan_type<tag/untag>, priority<0-7>, dscp<0-63> 
==================================               ===============================

Type: os10_lldp_interface
*************************

The ``os10_lldp_interface`` resource type is to used to manage LLDP configuration per interface in OS10 EE switches. The os10_lldp resource is not an ensurable type and hence does not have an ensure attribute. The per interface name is given as arg for the resource.

**Attributes**

=======================================          ===============================
Attribute                                        Description
=======================================          =============================== 
``receive``                                      Enables or disables the reception of LLDP for that interface (true, false) 
``transmit``                                     Enables or disables the transmission of LLDP for that interface (true, false) 
``med``                                          Enables or disables the MED LLDP for that interface; LLDP MED can be enabled only when LLDP transmit and receive are enabled; LLDP receive/transmit can be disabled only when LLDP MED is disabled (true, false) 
``med_tlv_select_inventory``                     Enables or disables the MED TLV select inventory LLDP for that interface (true, false) 
``med_tlv_select_network_policy``                Enables or disables the MED TLV select network policy LLDP for that interface (true, false) 
``med_network_policy``                           Configures the med network policy (1 to 32) to add and remove the network policies 
``tlv_select``                                   Configures the tlv select option and suboption as array of values
=======================================          ===============================
