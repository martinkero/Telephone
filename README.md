Telephone is a VoIP program which allows you to make phone calls over
the internet. It can be used to call regular phones via any
appropriate SIP provider. If your office or home phone works via SIP,
you can use that phone number on your Mac anywhere you have decent
internet connection.

Building
--------

Telephone's SIP user agent is based on [pjsip][]. You need to build it
before building Telephone. Name the directory _pjproject_ and place it
near Telephone, in the same parent directory.

  [pjsip]: http://www.pjsip.org/

    $ svn checkout http://svn.pjsip.org/repos/pjproject/tags/1.12 pjproject
    $ cd pjproject

Create the file `pjlib/include/pj/config_site.h` with the following
contents.

    #define PJSIP_DONT_SWITCH_TO_TCP 1
    #define PJSUA_MAX_ACC 32
    #define PJMEDIA_RTP_PT_TELEPHONE_EVENTS 101
    #define PJMEDIA_RTP_PT_TELEPHONE_EVENTS_STR "101"
    #define PJ_DNS_MAX_IP_IN_A_REC 32
    #define PJ_DNS_SRV_MAX_ADDR 32
    #define PJSIP_MAX_RESOLVED_ADDRESSES 32

Configure and build Telephone

    $ CFLAGS="-O2 -arch i386 -arch x86_64" ./configure --disable-ssl
    $ make

Coding Style
------------

Telephone source code follows [Google Objective-C Style Guide][coding_style].

  [coding_style]: http://google-styleguide.googlecode.com/svn/trunk/objcguide.xml


Martins notes 1.0.4:
--------------------

* The old svn portaudio is no longer avaiable, use this portaudio:

         $ cd third_party/portaudio/
         $ git clone https://git.assembla.com/portaudio.git
         $ git checkout 00502b

* Change linker flags to your version: pjproject/pjlib/bin/pjlib-test-i386-apple-darwin15.5.0
* Build with 10.9 SDK with 10.11 as target (el capitan)
