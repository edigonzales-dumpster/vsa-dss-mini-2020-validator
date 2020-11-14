# vsa-dss-mini-2020-validator

## todo
- 'bessere' (besser unterscheidbare) OID
- Gradle Build o.ä. für Automatisation der Tests
  * Anzahl Errors etc. muss überprüft werden.
- ...

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

## Daten in Datenbank importieren
```
java -jar /Users/stefan/apps/ili2pg-4.4.2/ili2pg-4.4.2.jar \
--dbhost localhost --dbport 54321 --dbdatabase edit --dbusr admin --dbpwd admin \
--disableValidation \
--dbschema vsadssmini_fk --models VSADSSMINI_2020_LV95 --modeldir "models/;http://models.geo.admin.ch" \
--import fubar.xtf
```


## Daten exportieren
```
java -jar /Users/stefan/apps/ili2pg-4.4.2/ili2pg-4.4.2.jar \
--dbhost localhost --dbport 54321 --dbdatabase edit --dbusr admin --dbpwd admin \
--dbschema vsadssmini_fk --models VSADSSMINI_2020_LV95 --modeldir "models/;http://models.geo.admin.ch" \
--disableValidation \
--export fubar2.xtf &&
xmllint --format fubar2.xtf -o fubar2.xtf
```

Achtung: 
- https://github.com/claeis/ilivalidator/issues/276 
- Testdatensätze sollen nur das nötigste beinhalten, d.h. EXTERNAL-Zeugs kann/soll entfernt werden.

## Daten prüfen

```
java -jar /Users/stefan/apps/ilivalidator-1.11.8/ilivalidator-1.11.8.jar --modeldir "models/;http://models.geo.admin.ch" fubar.xtf
```

```
java -jar /Users/stefan/apps/ilivalidator-1.11.8/ilivalidator-1.11.8.jar --modeldir "models/;http://models.geo.admin.ch" --config config.toml fubar.xtf
```

## Modell prüfen
```
java -jar /Users/stefan/apps/ili2c-5.1.2/ili2c.jar --modeldir "models/;http://models.geo.admin.ch" models/VSADSSMINI_2020_LV95_Validierung_A.ili
```