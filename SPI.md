# Session Initiation Protocol

    A application that communicates voice through IP (VoIP or Voice-over-IP) will use this protocol. 
    This protocol solves many issues when stablishing a session between mobile devices and is quicker than H.323.

## How it works
* User A wants to contact user B
* A tries to find where is B
* A and B register requests on a server
* A invites B to a conversation - the invite goes through a server
* B accepts the invite
* A and B trade info about how they interpret (code) audio information
    * Linphone uses SIP

## Problems
* If the IP of the device is behind a private network, there will be difficulties
    * Sollution: ICE / STUN


## Invite Sample

``` 
INVITE sips:Bob@TMC.com SIP/2.0
Via: SIP/2.0/TLS client.ANC.com:5061;branch = z9hG4bK74bf9
Max-Forwards: 70
From: Alice<sips:Alice@TTP.com>;tag = 1234567
To: Bob<sips:Bob@TMC.com>
Call-ID: 12345601@192.168.2.1
CSeq: 1 INVITE
Contact: <sips:Alice@client.ANC.com>
Allow: INVITE, ACK, CANCEL, OPTIONS, BYE, REFER, NOTIFY
Supported: replaces
Content-Type: application/sdp
Content-Length: ...

v = 0
o = Alice 2890844526 2890844526 IN IP4 client.ANC.com
s = Session SDP
c = IN IP4 client.ANC.com
t = 3034423619 0
m = audio 49170 RTP/AVP 0
a = rtpmap:0 PCMU/8000

```

## Some things this session allows
* Ease of connection 