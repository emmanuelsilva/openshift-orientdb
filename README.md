# Openshift OrientDB Cartridge

**WARNING** : The cartridge havent been tested yet


This cartridge provides [OrientDB](http://www.orientechnologies.com/orientdb/) on the Openshift Platform.

**OrientDB** is an open source NoSQL database management system written in Java. It has features of both Document and Graph management, as it’s document-based database, but the relationships are managed as in graph databases with direct connections between records. 

OrientDB is incredibly fast: it can store up to 150,000 records per second on common hardware. In addition, this database supports schema-less, schema-full and schema-mixed modes. It also has a strong security profiling system based on users and roles and supports SQL as a query language. 

**OpenShift’s cartridge model** to make it easier for independent software vendors (ISVs) offering core services in multiple platforms and for a wider array of cloud ecosystems and marketplaces. This open standard for technology packaging and deployment enables ISVs and end-users to integrate their own middleware, databases, and services into the platform and make them available to PaaS developers building applications.

# Tutorial 
_This was taken from [here](https://www.mail-archive.com/orient-database@googlegroups.com/msg07051.html)._

You first have to have a cartridge that exposes the web_app and then you 
add this as a database, same way as you would mysql.  This behavior can be 
changed in the yml config if you want to expose orientdb directly to the 
web.  Ie so that you can use orientdb's as a public rest server.

Here are the steps to create via openshift's web interface

1. In your applications tab choose create new application
2. In type of application scroll to bottom and choose Do-it-youself 0.1 or 
Php or any cartridge that exposes a web_app external port
3.  If you choose diy, then on the next page fill in public url to whatever 
you want and click create application
4. It will ask you if you will be changing the code of application, choose 
no not now
5. Once your app is setup from the bottom of the screen click see a list of 
cartridges you can add 
6. Scroll to the very bottom left side where it says Install your own 
cartridge and paste in the RAW link to the yml file
  To get the raw yml link do this: In a new browser tab navigate to the 
github repository here <https://github.com/jjfraz11/openshift-orientdb> then 
click on the metadata folder, then click the manifest.yml file, then click 
on the raw button located in the upper right corner of the editor window, a 
new window will open, copy the url.
7. Go back to the openshift tab, to the Install your own cartridge and 
paste the yml link
8. Click next then click add cartridge
9. After install it will give you a page with the username and password plus 
the internal port to connect to orientdb, this is what you would use to 
connect from a Php application, ie if you choose Php as your 
web_application gear instead of DIY

That should be it, to verify assuming you installed the opshift rhc client 
tools on your pc you can do a port forward from you client machine and 
access orient db either via console or web interface.  Note:  I could not 
connect to orientdb using the console via ssh, openshift will not let you 
run shell scripts.  But testing remotely from client pc using port-forward 
worked fine.

To test open a cmd line and type rhc port-forward -a yourappname
It will show you a list of Local ports mapped to open-shift internal ports
you should see a listing for orientdb and orientdb_web, open a web browser 
and connect to the local oreintdb_web or connect via console

Also note when I connected to the orientdb_web interface the default 
password was still admin, even though it was set to be auto-generated by 
the cartridges installer script.
