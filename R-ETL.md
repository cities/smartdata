Use R for ETL (Extract-Transform-Load)

## csv
```
df.A <- read.csv('/path/to/tableA.csv', header=T)
write.table(df.A, row.names=F, header=T, sep=",")
```

## tab
```
df.A <- read.table('/path/to/tableA.tab', header=T, sep="\t")
write.table(df.A, row.names=F, header=T, sep="\t")
```

## Excel
```
install.packages("gdata")
require(gdata)
df.A <- read.xls("tableA.xls")
```

## dbf 
```
require('foreign')
df.A <- read.dbf('tableA.dbf')
write.dbf(df.A, 'tableB.dbf')
```

## sqlite
```
require(RSQLite)
# connect to the sqlite file
conn = dbConnect(drv="SQLite", dbname="/path/to/tableA.sqlite")
dbListTables(con)
df.A <- dbReadTable(conn, 'tableA', row.names=NULL)
#or get a data.frame from a query
df.A = dbGetQuery( conn, 'select * from tableA' )
table_name <- 'tableB'
if (dbExistsTable(conn, table_name))  dbRemoveTable(conn, table_name)
dbWriteTable(conn, table_name, df.A, row.names = F)
```

## mysql
```
require(RMySQL)
conn <- dbConnect(MySQL(), group='trondheim', dbname='database_name')
dbListTables(conn)
df.A <- dbReadTable(conn, 'tableA', row.names=NULL)
table_name <- 'tableB'
if (dbExistsTable(conn, table_name))  dbRemoveTable(conn, table_name)
dbWriteTable(conn, table_name, df.A, row.names = F)
```

## postgresql
```
require(foreign)
require(RPostgreSQL)
conn <- dbConnect(PostgreSQL(), user= "username", password="***", dbname="database_name")
dbListTables(conn)
df.A <- dbReadTable(conn, 'tableA')

#read table from a schema other than public
df.A2 <- dbReadTable(conn, c('schema', 'tableA'))

table_name <- "tableB"
if (dbExistsTable(conn, table_name))  dbRemoveTable(conn, table_name)
dbWriteTable(conn, table_name, data, row.names = F)
```

## SAS
```
install.packages("sas7bdat")
require(sas7bdat)
df.A <- read.sas7bdat('/path/to/tableA.sas7bdat')
require(foreign)
df.A <- read.xport('/path/to/tableA.xpt')

```

## SPSS
```
require(foreign)
df.A <- read.spss('/path/to/tableA.spss')
```

## Stata
```
require(foreign)
df.A <- read.dta('/path/to/tableA.dta')
write.dta(df.A, '/path/to/tableB.dta')

```

## References
1. http://www.ats.ucla.edu/STAT/r/faq/inputdata_R.htm
