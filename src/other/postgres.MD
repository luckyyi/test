# dump & restore
- dump
```
pg_dump -Fc --no-acl --no-owner --table=media_exported -h localhost -p 5432 -U postgres storefront > storefront_media_for_qa_201707101715.dump
```

- restore
```
pg_restore --verbose --clean --no-acl --no-owner -h storefronts-pg-qa.cfjnafc8bsrz.us-east-1.rds.amazonaws.com -U localservices -p 5432 -d storefront storefront_media_for_qa_201707101715.dump
```
