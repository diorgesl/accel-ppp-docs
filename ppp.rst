[ppp]
======

The Point-to-Point Protocol (PPP) provides a standard method for transporting multi-protocol datagrams over point-to-point links.  PPP also defines an extensible Link Control Protocol.
Section ``[ppp]`` consist common ppp prams for PPPoE/PPtP/L2TP/SSTP.

**verbose=0|1**
  Default value is ``verbose=0``

  Writes more detailed logs.

**min-mtu=n**
  Default value is ``min-mtu=100``
  
  Minimum acceptable MTU.
  If client will try to negotiate less then specified MTU then it will be NAKed or disconnected if rejects greater MTU.

**mtu=n**
  By default is not defined.
  
  MTU which will be negotiated if client's MRU will be not acceptable.
  
**mru=n**
  By default is not defined.

  Prefered MRU.

**accomp=allow|deny**
  By default is: ``accomp=deny``

  Address/Control compression negotiation.
  
  * ``allow`` - prefere in send and don't deny in receive directions.
  
  * ``deny`` - disable in both directions.

**pcomp=allow|deny|n**
  By default is: ``pcomp=deny``

  Protocol field compression negotiation. 

  * allow - prefere in send and don't deny in receive directions.

  * deny - disable in both directions.

**ccp=n**
  By default is enabled: ``ccp=1``

  For disable CCP(*Compression Control Protocol*) negotiation set ``ccp=0``

**ccp-max-configure=n**
  By default is: ``ccp-max-configure=3``
  
  **TODO**
  
**sid-case=upper|lower**
  By default is: ``sid-case=lower``

  Specifies in which case generate session identifier.
  
**check-ip=0|1**
  By default is: ``check-ip=0``

  Specifies whether accel-ppp should check if IP already assigned to other ppp interface.
  
**single-session=replace|deny**
  By default is not defined.

  Specifies whether accel-ppp should control sessions count. If this option is absent session count control is turned off. If this option is ``replace`` then accel-ppp will terminate first session when second is authorized. If this option is ``deny`` then accel-ppp will deny second session authorization.

**mppe=require|prefer|deny**
  Default behavior - don't ask client for mppe, but allow it if client wants.
  
  Specifies mppe negotioation preference.
  
  ``require`` - ask client for mppe, if it rejects drop connection.
  
  ``prefer`` - ask client for mppe, if it rejects don't fail.
  
  ``deny`` - deny mppe.
 
 .. admonition:: Note:
    
    RADIUS may override this option by MS-MPPE-Encryption-Policy attribute.
  
**ipv4=deny|allow|prefer|require**
  By default is ``ipv4=allow``
  
  Specifies IPv4 (IPCP) negotioation algorithm: 

  ``deny`` - don't negotiate IPv4.
  
  ``allow`` - negotiate IPv4 only if client requests.
  
  ``prefer`` - ask client for IPv4 negotiation, don't fail if he rejects.
  
  ``require`` - require IPv4 negotiation.

**ipv6=deny|allow|prefer|require**
  By default is ``ipv6=deny``
  
  Specify IPv6 (IPCP) negotioation algorithm: 
  
  ``deny`` - don't negotiate IPv6.
  
  ``allow`` - negotiate IPv6 only if client requests.
  
  ``prefer`` - ask client for IPv6 negotiation, don't fail if he rejects.
  
  ``require`` - require IPv6 negotiation.
  
**ipv6-intf-id=x:x:x:x|random**
  By default is **fix**

  Specify fixed or random interface identifier for IPv6.
  
   ``random`` -
   
   Fixed ``x:x:x:x`` - 

**ipv6-peer-intf-id=x:x:x:x|random|ipv4|calling-sid**
  By default is **fix**
  
  Specifies peer interface identifier for IPv6. 
  
  ``random`` - **fix**
  
  ``ipv4`` - calculate interface identifier from IPv4 address, for example 192:168:0:1. 
  
  ``calling-sid`` - calculate interface identifier from Calling-Station-Id.

**ipv6-accept-peer-intf-id=0|1**
  By default is not defined.
  
  Specify whether to accept peer's interface identifier.

**lcp-echo-interval=n**
  By default is ``lcp-echo-interval=10`` **check**

  If this option is given and greater then 0 then lcp module will send echo-request every n seconds.

**lcp-echo-failure=n**
  By default is disabled ``lcp-echo-failure=0``

  Specifies maximum number of echo-requests may be sent without valid echo-reply, if exceeds connection will be terminated.

**lcp-echo-timeout=sec**
  By default is ``lcp-echo-timeout=60`` **check**

  Specifies timeout in seconds to wait for any peer activity. If this option specified it turns on adaptive *lcp echo functionality* and ``lcp-echo-failure`` is not used.

**unit-cache=n**
  By default is disabled: ``unit-cache=0``

  Specifies number of interfaces to keep in cache. It means that don't destory interface after corresponding session is destoyed, instead place it to cache and use it later for new sessions repeatedly. This should reduce kernel-level interface creation/deletion rate lack.

**unit-preallocate=0|1**
  By default is ``unit-preallocate=0``, ppp unit (interface) will allocate after authorization.

  Specified will accel-ppp allocate ppp unit (interface) before authorization, so Nas-Port and Nas-Port-Id would be defined in Access-Request phase.
