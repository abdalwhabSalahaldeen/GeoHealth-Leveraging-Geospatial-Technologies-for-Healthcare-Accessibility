# GeoHealth-Leveraging-Geospatial-Technologies-for-Healthcare-Accessibility
GeoHealth: Using Geoserver, Leaflet, PostgreSQL, jQuery, and more to find the nearest hospital for users. Revolutionizing healthcare accessibility with precise geospatial data and efficient routing. #GIS #Healthcare


# using geoserver,leaflet,leaflet routeing machaine , postgreSQL, geoserver, jquery, to find nersest hosptial for user location 
# and find short path from user location to nearest hospital.

# Requirements as used in this project:

     PostgreSQL - 14
     Postgis - 3.2.3
     Geoserver - 2.21.1
     Leaflet JS - 1.9.2
    
    
# Step 1: Create database with the required extensions
 using pgadmin4 interface in windows 10 create database


![pgadmin4 create database](https://user-images.githubusercontent.com/43234860/207780234-24f2571a-5a06-40be-b7b8-f08b81f6f131.PNG)

add postgis exintion.

![postgis extntion](https://user-images.githubusercontent.com/43234860/207780384-8ad4e44a-15f5-47c1-910c-08b7fa34f4bf.PNG)

# step 2: connect qgis with postgresql and import shapefile to postgresql by qgis.
![image](https://user-images.githubusercontent.com/43234860/207780551-153b4bbb-aced-43f7-9898-04ff5b236dee.png)

![qgis](https://user-images.githubusercontent.com/43234860/207780794-90d72e87-ace7-4aea-8c06-49e1b7e28d1c.PNG)

![image](https://user-images.githubusercontent.com/43234860/207780910-2989677d-5a66-480e-8584-5e0d43d599b1.png)

import shapefile to database:
![image](https://user-images.githubusercontent.com/43234860/207781024-7131368d-309c-43f4-8a10-db1dd1ac53bc.png)


# step 3: test SQL statement in pgadmin4 in our data(hospital data):
 SQL:
 
      SELECT name,id,geom,
      geom <-> 'SRID=4326;POINT(40 10)'::geometry AS dist
      from hospitals ORDER BY dist LIMIT 3;

![admin4 sql](https://user-images.githubusercontent.com/43234860/207781520-26cc93ba-9c16-4b70-901f-de04a7537d5a.PNG)

# step 4: connect geoserver with database:
go to : http://localhost:8080/geoserver/web/?0
login with defult login information 
    username : admin
    password : geoserver
# create Workspaces.

![geoserver](https://user-images.githubusercontent.com/43234860/207781865-edeb5eed-6bdf-4954-ae6d-b06e7fc1ec09.PNG)

# create Store.
    in this step connect postgreSQL to geoserver using locahost, port , username , password , and database name.
![image](https://user-images.githubusercontent.com/43234860/207782124-ddd2bb63-cfaf-44ca-953d-e7ab07dfb047.png)

#add layer and add SQL statement:
![image](https://user-images.githubusercontent.com/43234860/207782223-1570391e-a8b3-4e9b-b09e-a23da7858626.png)

![image](https://user-images.githubusercontent.com/43234860/207782248-041d6c1d-923c-4f14-9f36-fa09eb03ad68.png)

![image](https://user-images.githubusercontent.com/43234860/207782266-99104534-7f2b-429f-811d-6825bed65118.png)

#create 4 parameter:

Validation regular expression:
using this : 

    ^[\d]+$

in geoserver SQL viewer add this code:

    SELECT name,id,geom,
    geom <-> 'SRID=4326;POINT(%x%.%x2% %y%.%y2%)'::geometry AS dist
    from hospitals2 ORDER BY dist LIMIT 1

![image](https://user-images.githubusercontent.com/43234860/207783416-4c95020f-9d52-4598-a3bd-8037d6ea4fdc.png)

# now go to layer preview:

    show or data as geojson we get url like this:
http://localhost:8080/geoserver/karary/ows?service=WFS&version=1.0.0&request=GetFeature&typeName=karary%3Alastone&maxFeatures=50&outputFormat=application%2Fjson&viewparams=x:40;x2:2000,y:10;y2:235500

# you most change x,x2,y,y2 from user location 

    x : it's Math.trunc(position.coords.longitude)
    x2 :  the decimal part from a x
    y : it's Math.trunc(position.coords.latitude)
    xy :  the decimal part from a y
![image](https://user-images.githubusercontent.com/43234860/207783814-9e7f95e5-205b-41b7-9053-bb9935caec01.png)

# step 4: create web page using html css js.
using html css js , leaflet, leaflet routing machine , jquery to create map.html page.

# to run map.html without erorr:
    Type windows+R or open "Run"

    Execute the following command:

     chrome.exe --user-data-dir="C://Chrome dev session" --disable-web-security
 
    open map.html in this brower window that open from last code.

final result :
![image](https://user-images.githubusercontent.com/43234860/207784068-1cffc582-dfd5-48b0-a141-715aa7463047.png)
