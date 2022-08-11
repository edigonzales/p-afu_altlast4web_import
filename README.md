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
java -jar /Users/stefan/apps/ili2pg-4.7.0/ili2pg-4.7.0.jar --dbhost localhost --dbport 54322 --dbdatabase pub --dbusr ddluser --dbpwd ddluser --modeldir "https://models.geo.admin.ch;." --models SO_AfU_KbS_Publikation_20220623 --dbschema afu_altlasten_pub_v1 --baskets ch.so.afu.altlast4web.public --export public.xtf
```



---------------------------------------------------

```
java -jar /Users/stefan/apps/ili2pg-4.8.1-SNAPSHOT/ili2pg-4.8.1-SNAPSHOT.jar --dbhost localhost --dbport 54322 --dbdatabase pub --dbusr ddluser --dbpwd ddluser --nameByTopic --defaultSrsCode 2056 --createMetaInfo --strokeArcs --createBasketCol --modeldir "https://models.geo.admin.ch;." --models SO_AfU_KbS_Publikation_restricted_20220811 --dbschema afu_altlasten_pub_v1 --schemaimport
```
---------------------------------------------------


```
java -jar /Users/stefan/apps/ili2pg-4.8.1-SNAPSHOT/ili2pg-4.8.1-SNAPSHOT.jar --dbhost localhost --dbport 54322 --dbdatabase pub --dbusr ddluser --dbpwd ddluser --nameByTopic --defaultSrsCode 2056 --createMetaInfo --strokeArcs --modeldir "https://models.geo.admin.ch;." --models "SO_AfU_KbS_Publikation_20220811;SO_AfU_KbS_entlassene_Standorte_Publikation_20220811" --dbschema afu_altlasten_pub_v1 --schemaimport
```

export:
```
java -jar /Users/stefan/apps/ili2pg-4.8.1-SNAPSHOT/ili2pg-4.8.1-SNAPSHOT.jar --dbhost localhost --dbport 54322 --dbdatabase pub --dbusr ddluser --dbpwd ddluser --nameByTopic --defaultSrsCode 2056 --createMetaInfo --strokeArcs --modeldir "https://models.geo.admin.ch;." --models "SO_AfU_KbS_Publikation_20220811" --dbschema afu_altlasten_pub_v1 --export public.xtf

java -jar /Users/stefan/apps/ili2pg-4.8.1-SNAPSHOT/ili2pg-4.8.1-SNAPSHOT.jar --dbhost localhost --dbport 54322 --dbdatabase pub --dbusr ddluser --dbpwd ddluser --nameByTopic --defaultSrsCode 2056 --createMetaInfo --strokeArcs --modeldir "https://models.geo.admin.ch;." --models "SO_AfU_KbS_entlassene_Standorte_Publikation_20220811" --dbschema afu_altlasten_pub_v1 --export restricted.xtf

java -jar /Users/stefan/apps/ili2pg-4.8.1-SNAPSHOT/ili2pg-4.8.1-SNAPSHOT.jar --dbhost localhost --dbport 54322 --dbdatabase pub --dbusr ddluser --dbpwd ddluser --nameByTopic --defaultSrsCode 2056 --createMetaInfo --strokeArcs --modeldir "https://models.geo.admin.ch;." --models "SO_AfU_KbS_Publikation_20220811;SO_AfU_KbS_entlassene_Standorte_Publikation_20220811" --dbschema afu_altlasten_pub_v1 --export public_and_restricted.xtf
```

gpkg:
```
java -jar /Users/stefan/apps/ili2gpkg-4.8.0/ili2gpkg-4.8.0.jar --dbfile ch.so.afu.kbs_restricted.gpkg --nameByTopic --defaultSrsCode 2056 --createMetaInfo --strokeArcs --modeldir "https://models.geo.admin.ch;." --models "SO_AfU_KbS_Publikation_20220811;SO_AfU_KbS_entlassene_Standorte_Publikation_20220811" --doSchemaImport --import public_and_restricted.xt

```


