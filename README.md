# p-afu_altlast4web_import

In gretljobs:
```
docker-compose down
docker volume prune
docker-compose up --build
```


```
java -jar /Users/stefan/apps/ili2pg-4.7.0/ili2pg-4.7.0.jar --dbhost localhost --dbport 54322 --dbdatabase pub --dbusr ddluser --dbpwd ddluser --importBid --nameByTopic --defaultSrsCode 2056 --createMetaInfo --strokeArcs --createBasketCol --modeldir "https://models.geo.admin.ch;." --models SO_AfU_KbS_Publikation_20220623 --dbschema geops_altlast4web --schemaimport
```

```
INSERT INTO
    afu_altlasten_pub_v1.t_ili2db_basket
    (
        t_id,
        topic,
        t_ili_tid,
        attachmentkey
    )
SELECT
    nextval('afu_altlasten_pub_v1.t_ili2db_seq'),
    'SO_AfU_KbS_Publikation_20220623.KbS',
    'ch.so.afu.altlast4web.public',
    'foo'
;

INSERT INTO
    afu_altlasten_pub_v1.t_ili2db_basket
    (
        t_id,
        topic,
        t_ili_tid,
        attachmentkey
    )
SELECT
    nextval('afu_altlasten_pub_v1.t_ili2db_seq'),
    'SO_AfU_KbS_Publikation_20220623.KbS',
    'ch.so.afu.altlast4web.restricted',
    'bar'
;
```


Export-Befehl aus altlast4web:
```
java -jar /Users/stefan/apps/ili2pg-4.7.0/ili2pg-4.7.0.jar --dbhost localhost --dbport 54322 --dbdatabase pub --dbusr ddluser --dbpwd ddluser --modeldir "https://models.geo.admin.ch;." --models SO_AfU_KbS_Publikation_20220623 --dbschema geops_altlast4web --export alles.xtf
```

Import in Pub-DB:
```
java -jar /Users/stefan/apps/ili2pg-4.7.0/ili2pg-4.7.0.jar --dbhost localhost --dbport 54322 --dbdatabase pub --dbusr ddluser --dbpwd ddluser --importBid --nameByTopic --defaultSrsCode 2056 --createMetaInfo --strokeArcs --createBasketCol --modeldir "https://models.geo.admin.ch;." --models SO_AfU_KbS_Publikation_20220623 --dbschema afu_altlasten_pub_v1 --schemaimport

java -jar /Users/stefan/apps/ili2pg-4.7.0/ili2pg-4.7.0.jar --dbhost localhost --dbport 54322 --dbdatabase pub --dbusr ddluser --dbpwd ddluser --importBid --modeldir "https://models.geo.admin.ch;." --models SO_AfU_KbS_Publikation_20220623 --dbschema afu_altlasten_pub_v1 --import alles.xtf
```
-> Alle Daten in einer Tabelle. Darstellung im Web GIS Client wie bei den anderen geschützten Layern. Getrennter Export (falls nicht bereits durch altlast4web) für Datenbezug:

```
java -jar /Users/stefan/apps/ili2pg-4.7.0/ili2pg-4.7.0.jar --dbhost localhost --dbport 54322 --dbdatabase pub --dbusr ddluser --dbpwd ddluser --modeldir "https://models.geo.admin.ch;." --models SO_AfU_KbS_Publikation_20220623 --dbschema afu_altlasten_pub_v1 --export public.xtf
```

