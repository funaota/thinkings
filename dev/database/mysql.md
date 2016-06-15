# DB

## index

1. backup & restore
1. delete data

---------------

### backup & restore

#### backup

`mysqldump --single-transaction -u USER_NAME -p DB_NAME > dump_file`

#### restore

`mysql -u USER_NAME -p DB_NAME < dump_file`

---------------

### delete data

delete DB_NAME.TABLE_NAME where hoge=hoge

----------------