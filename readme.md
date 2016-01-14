## How to build a weathermap using the OpenAPI

**These files can be used to create a .war file which can be hosted on the data aggregator.** 
**The index.html can reference internal or external web sites and links.**

1. Clone the weathermap repository to your local system.
2. You must update the index.html file to point at your Data Aggregator
   * This app is set up to leverge the **geo-spacial attributes for devices**. Each device must have geo-spacial attributes associated with it. You can find out more about how to use the RestFUL API to update these attributes here: http://<insert DA Host>:8581/rest/devices/documentation
   * See the following options: Device.Elevation, Device.Latitude, Device.Longitude
   * The default locations used for this sample app are AZ, NY, MI, FL and the DA
   * The routers are all a member of a group called TIXCHANGE and the name of all the devices end with SITE or WAN
   * Each interface on the routers have had the decription updated with "Link to" so for example:
     * router AZ-SITE has interfaces Gi1 with description "Link to NY-WAN" 
     * router FL-SITE has interfaces Gi1 with description "Link to NY-WAN"
     * router MI-SITE has interfaces Gi1 with description "Link to NY-WAN"
     * router NY-WAN has interfaces Gi1 with description "Origin: NY Destination: DataCeter", Gi2's description "Origin:NY Destination:FL", Gi3's description "Origin: NY Destination: AZ" and Gi4's description is "Origin: NY Destination:MI"
     * This is a template so feel free to tie it into your own inventory database and have fun with it.
![Image of CAPM Weathermap](https://github.com/CA-PM/weathermap/images/weathermap.png) 
3. Create the WAR file: (you can also do this on your DA if you have java installed /usr/bin/jar)
   * C:\Program Files\Java\jdk1.7.0_45\bin\jar -cfm ..\weathermap-bundle-2.6.0.war META-INF\MANIFEST.MF *
4. Move to DA Deploy directory:
   * C:\bin\pscp.exe ..\weathermap-bundle-2.6.0.war root@<da host>:/opt/IMDataAggregator/apache-karaf-2.3.0/deploy/
5. Test and profit by going to http://<da host>:8581/apps/weathermap/index.html
   * Once you tested it just include it in a web view in your performance center and you’re good to go

**NOTE:** the MANIFEST.MF file contains all the info about version etc. so you have to keep all that in order when you create the war file. I you make changes to the files you have to update the version. 
