# Shibboleth MFA Duo Preauth

This provides a replacement to the Duo failmode=safe functionality that
was found in Duo's own Shibboleth module for IdP version 3.2 and
earlier. This code will work with the Shibboleth MFA Duo module in IdP
3.3 and above. 

The script is written mostly in javascript and tested on a system using 
the Nashorn/Java8 javascript library. 

## Installation

Replace the default conf/authn/mfa-authn-config.xml with the copy 
found in this archive. Customize your copy:

* Change the first authn flow if needed. It is "authn/Password" in this copy. 
  Make sure to edit the entry key on the second flow to match.
* Find the maxRetry and timeOut variables and change them as needed.
* Find the duoScope variable and change it to match your environment. In
  our system, the MFA function gets the bare username and we add
  "@ncsu.edu" to make the username used in Duo. You may need to adjust
  the code to suit your environment.

In addition, make sure you already have the conf/authn/duo.properties
values set for your environment. This script will use those values for
your API host and keys.

It may help to increase the "idp.loglevel.idp" to "DEBUG" in
conf/logback.xml while doing initial testing.

## References

* [DuoAuthnConfiguration](https://wiki.shibboleth.net/confluence/display/IDP30/DuoAuthnConfiguration)
* [MultiFactorAuthnConfiguration](https://wiki.shibboleth.net/confluence/display/IDP30/MultiFactorAuthnConfiguration)
* [duo_shibboleth for IdP 3.2 and earlier](https://github.com/duosecurity/duo_shibboleth)
* [Duo Auth API doc](https://duo.com/docs/authapi)
* [nashorn javascript http client](https://gist.github.com/billybong/a462152889b6616deb02)
* [jsSHA javascript SHA implementations](https://github.com/Caligatio/jsSHA)


