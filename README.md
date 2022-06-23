# p-afu_altlast4web_import

In gretljobs:
```
docker-compose down
docker volume prune
docker-compose up --build
```


```
java -jar /Users/stefan/apps/ili2pg-4.7.0/ili2pg-4.7.0.jar --dbhost localhost --dbport 54322 --dbdatabase pub --dbusr ddluser --dbpwd ddluser --nameByTopic --defaultSrsCode 2056 --createMetaInfo --strokeArcs --createBasketCol --modeldir "https://models.geo.admin.ch;." --models SO_AfU_KbS_Publikation_restricted_20220623 --dbschema afu_altlasten_pub_v1 --schemaimport
```

```
WITH topics AS
(
    SELECT DISTINCT
        split_part(iliname, '.', 1) || '.' || split_part(iliname, '.', 2) AS topicname
    FROM
        afu_altlasten_pub_v1.t_ili2db_classname
    WHERE
        iliname ILIKE '%restricted%'
)
INSERT INTO
    afu_altlasten_pub_v1.t_ili2db_basket
    (
        t_id,
        topic,
        attachmentkey
    )
SELECT
    nextval('afu_altlasten_pub_v1.t_ili2db_seq'),
    topics.topicname,
    'foo'
FROM
    topics
;
```


```
java -jar /Users/stefan/apps/ili2pg-4.7.0/ili2pg-4.7.0.jar --dbhost localhost --dbport 54322 --dbdatabase pub --dbusr ddluser --dbpwd ddluser --modeldir "https://models.geo.admin.ch;." --models SO_AfU_KbS_Publikation_restricted_20220623 --dbschema afu_altlasten_pub_v1 --export restricted.xtf
```

```
java -jar /Users/stefan/apps/ili2pg-4.7.0/ili2pg-4.7.0.jar --dbhost localhost --dbport 54322 --dbdatabase pub --dbusr ddluser --dbpwd ddluser --modeldir "https://models.geo.admin.ch;." --models SO_AfU_KbS_Publikation_restricted_20220623 --exportModels SO_AfU_KbS_Publikation_20220623 --dbschema afu_altlasten_pub_v1 --export public.xtf
```

