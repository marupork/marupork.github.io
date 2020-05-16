# Oracle Installation with Liquibase Maven Plugin Setup

[<<](../)

## Table-of-Contents

- [Oracle Installation](#oracle-installation)
- [Liquibase Maven Plugin](#liquibase-mvn-plugin)

## oracle-installation

1. Install `Oracle Database 18c Express Edition` - [XE downloads](https://www.oracle.com/database/technologies/xe-downloads.html)
1. After installation, run `cmd as an admin`
1. Login

   ```console
    sqlplus / AS SYSDBA
    ALTER SESSION SET "_ORACLE_SCRIPT"=true;
   ```

1. Drop user

   ```console
    DROP USER schema_user CASCADE
    ;
   ```

1. Create user

   ```console
    CREATE user schema_user IDENTIFIED BY password;
   ```

1. Grant all access to user

   ```console
    GRANT CONNECT, RESOURCE, DBA TO schema_user;
    GRANT CREATE SESSION GRANT ANY PRIVILEGE TO schema_user;
    GRANT UNLIMITED TABLESPACE TO schema_user;
   ```

1. Connect using your user

   ```console
    CONNECT schema_user/password@localhost:1521/xe
   ```

1. Run sql script

   ```console
    @C:/create.sql;
   ```

1. Connection

   ```properties
    url: jdbc:oracle:thin:@localhost:1521:XE
    username: schema_user
    password: password
   ```

## liquibase-mvn-plugin

1. Add the following on pom.xml

    ```xml
    <build>
        <plugins>
            <plugin>
                <groupId>org.liquibase</groupId>
                <artifactId>liquibase-maven-plugin</artifactId>
                <version>${liquibase-version}</version>
                <configuration>
                    <driver>com.mysql.cj.jdbc.Driver</driver>
                    <url>jdbc:oracle:thin:@localhost:1521:XE</url>
                    <username>schema_user</username>
                    <password>password</password>
                    <!-- contains version changes used in liquibase:update-->
                    <changeLogFile>src/main/resources/db/update.xml</changeLogFile>
                </configuration>
            </plugin>
        </plugins>
    </build>
    ```

1. `/db/update.xml`

    ```xml
    <databaseChangeLog xmlns="http://www.liquibase.org/xml/ns/dbchangelog" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:ext="http://www.liquibase.org/xml/ns/dbchangelog-ext"
    xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog
    http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.0.xsd
    http://www.liquibase.org/xml/ns/dbchangelog-ext
    http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-ext.xsd">
        <include file="db/changelog/changelog-1.0.xml"/>
    </databaseChangeLog>
    ```

1. sample changeset: `/db/changelog/changelog-1.0.xml`

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <databaseChangeLog xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:ext="http://www.liquibase.org/xml/ns/dbchangelog-ext"
    xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog
    http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.0.xsd
    http://www.liquibase.org/xml/ns/dbchangelog-ext
    http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-ext.xsd">
    <changeSet id="01" author="maru.pork">
        <comment>Comment</comment>
        <sql></sql>
        <rollback></rollback>
    </changeSet>
    ```

1. Usage

    ```console
    mvn liquibase:dropAll
    mvn liquibase:update
    ```

[<<](../)
