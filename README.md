# vsa-dss-mini-2020-validator

## Datenbank für Erfassung von Testdaten
```
docker-compose up
```

## Modell in Datenbank importieren
```
java -jar /Users/stefan/apps/ili2pg-4.4.2/ili2pg-4.4.2.jar \
--dbschema vsadssmini_fk --models VSADSSMINI_2020_LV95 --modeldir "models/;http://models.geo.admin.ch" \
--defaultSrsCode 2056 --createGeomIdx --createFk --createFkIdx --createUnique --createEnumTabs --beautifyEnumDispName --createNumChecks --nameByTopic --strokeArcs --smart2Inheritance \
--createscript vsadssmini_fk.sql
```

## Daten exportieren
```
java -jar /Users/stefan/apps/ili2pg-4.4.2/ili2pg-4.4.2.jar \
--dbhost localhost --dbport 54321 --dbdatabase edit --dbusr admin --dbpwd admin \
--dbschema vsadssmini_fk --models VSADSSMINI_2020_LV95 --modeldir "models/;http://models.geo.admin.ch" \
--disableValidation \
--export fubar.xtf
```

Achtung: 
- https://github.com/claeis/ilivalidator/issues/276 
- Testdatensätze sollen nur das nötigste beinhalten, d.h. EXTERNAL-Zeugs kann/soll entfernt werden.