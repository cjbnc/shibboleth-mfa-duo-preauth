# Shibboleth MFA Duo Preauth

This provides a replacement to the Duo failmode=safe functionality that
was found in Duo's own Shibboleth module for IdP version 3.2 and
earlier. This code is written to work with the Shibboleth MFA Duo module
in IdP 3.3 and above.

The code is written in javascript with calls to java classes. It has
been tested on a system using the Nashorn/Java8 javascript library.

## Dependencies

The code depends on Duo's [duo_client_java] library and requires 
its dependencies as well. Those are currently:

* duo-client-0.2.1 
* org.json-chargebee-1.0 
* okhttp-2.3.0 

One way to get those is to manually download them from maven
repositories when building the IdP. For example:

    # after running the IdP install.sh
    cd /opt/shibboleth-idp/webapp/WEB-INF/lib/
    wget https://dl.bintray.com/uniconiam/maven/com/duosecurity/duo-client/0.2.1/duo-client-0.2.1.jar
    wget http://repo1.maven.org/maven2/org/json/org.json/chargebee-1.0/org.json-chargebee-1.0.jar
    wget http://repo1.maven.org/maven2/com/squareup/okhttp/okhttp/2.3.0/okhttp-2.3.0.jar

[duo_client_java]: https://github.com/duosecurity/duo_client_java

## Installation

Configure your IdP to work with the built-in Duo/MFA architecture. 
Refer to the documentation linked in the references below for help.

Once that works, copy/merge this conf/authn/mfa-authn-config.xml
with your version. Customize your copy:

* Change the first authn flow if needed. It is "authn/Password" in this
  copy. Make sure to edit the entry key on the second flow to match.
* Find the maxRetry and timeOut variables and change them as needed.
* Find the duoScope variable and change it to match your environment. In
  our system, the MFA function gets the bare username and we add
  "@ncsu.edu" to make the username used in Duo. You may need to adjust
  the code to suit your environment.

In addition, make sure you already have the conf/authn/duo.properties
values set for your environment. This code will use those values for
your API host and keys.

It may help to increase the "idp.loglevel.idp" to "DEBUG" in
conf/logback.xml while doing initial testing.

## References

* [DuoAuthnConfiguration](https://wiki.shibboleth.net/confluence/display/IDP30/DuoAuthnConfiguration)
* [MultiFactorAuthnConfiguration](https://wiki.shibboleth.net/confluence/display/IDP30/MultiFactorAuthnConfiguration)
* [duo_shibboleth for IdP 3.2 and earlier](https://github.com/duosecurity/duo_shibboleth)
* [Duo Auth API doc](https://duo.com/docs/authapi)


