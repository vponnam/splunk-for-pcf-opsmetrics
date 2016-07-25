## Splunk Add-on for PCF Ops Metrics

The Splunk Add-on for [PCF Ops Metrics](https://network.pivotal.io/products/ops-metrics) uses the *Splunk Add-on for Java Management Extensions (JMX)* to provide additional monitoring and alerting of PCF. You must [download](https://splunkbase.splunk.com/app/2647/) and [configure](http://docs.splunk.com/Documentation/AddOns/released/JMX/Configureinput) that add-on first. Then, you can copy and paste the contents of this repository into `$SPLUNK_HOME/etc/apps/Splunk_TA_jmx` and restart Splunk.

__NB__ The *Splunk Add-on for JMX* is intended to replace the add-on components of *Monitoring of Java Virtual Machines with JMX*. See migration guide [here](http://docs.splunk.com/Documentation/AddOns/latest/JMX/Releasehistory) for details.

Many of the dashboards in this add-on were taken from Mark Seidenstricker's [splunk-pcf-monitor](https://github.com/mjseid/splunk-pcf-monitor) and updated to support the latest 1.6 version of PCF Ops Metrics.

Documentation for the Splunk JMX add-on is located [here](http://docs.splunk.com/Documentation/AddOns/latest/JMX/About).

For installation and set-up instructions, refer to the Installation and Configuration [section](http://docs.splunk.com/Documentation/AddOns/latest/JMX/Hardwareandsoftwarerequirements).

For release notes, refer to the Release notes [section](http://docs.splunk.com/Documentation/AddOns/latest/JMX/Releasenotes).

For PCF platform logging, visit [splunk-for-pcf-logging](https://github.com/pivotalservices/splunk-for-pcf-logging).

## Install
After you have installed and configured the Splunk JMX Add-On (see above) you can follow these instructions to install the custom dashboards into the Add-On

* Login to your Splunk instance, for example:
```
    ssh -i "splunk.pem" ec2-user@ec2-53-44-87-326.compute-1.amazonaws.com
```

* Add new dashboards to the Add-On
```
    $ cd /opt/splunk/etc/apps
    $ mkdir opsmetrics
    $ wget -qO- "https://github.com/pivotalservices/splunk-for-pcf-opsmetrics/archive/1.0.0.tar.gz" \
      | tar -xzC opsmetrics --strip-components 1
    $ cd /opt/splunk/etc/apps/Splunk_TA_jmx
    $ cp /opt/splunk/etc/apps/opsmetrics/default/data/ui/nav/default.xml default/data/ui/nav/default.xml
    $ cd /opt/splunk/etc/apps/Splunk_TA_jmx/local
    $ cp -R /opt/splunk/etc/apps/opsmetrics/local/data/ data/
```

* Restart Splunk
```
    $ /opt/splunk/bin/splunk restart
```
