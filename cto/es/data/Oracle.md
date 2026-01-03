# Oracle

String Operations

## Instalation

```bash
docker run -d --name oracle19c \
  -p 1521:1521 -p 5500:5500 \
  -e ORACLE_PASSWORD=$PASS \
  gvenzl/oracle-xe
```

url : `jdbc:oracle:thin:@//localhost:1521/XE`

user: system
pass: $PASS

Oracle

- Case Sensitive: Sensitive
- String Quotes: Single Only

Check support for internalization.

Support for colation.

Read the chapter of a databse book.

DBMS Random https://stackoverflow.com/questions/1568630/generating-random-number-in-each-row-in-oracle-query

## QA

- What is an schema in oracle

## References

- https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/Format-Models.html#GUID-DFB23985-2943-4C6A-96DF-DF0F664CED96
- https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/NLS_TIMESTAMP_FORMAT.html#GUID-1070C91E-6C9D-4FAF-BD58-7880DBED9899
- https://www.techonthenet.com/oracle/functions/to_date.php
- Oracle functions to_char, extract, to_date, to_timestamp, …
- https://www.oracletutorial.com/oracle-date-functions/oracle-to_date/
- https://github.com/wnameless/docker-oracle-xe-11g
- https://stackoverflow.com/questions/67805311/oracle-database-installation-on-ubuntu-18-04