"# h2-database-manager" 

Steps to introduce database change control into project
1. Add needed repositores : for change control -> org.liquibase:liquibase-core:3.3.0, database Driver -> com.h2database:h2:1.3.170 
2. configure maven to run the process as build , by adding properties to a liquibase.properties file or adding those properties directly to maven 
		a) 
			<plugin>
				<groupId>org.liquibase</groupId>
				<artifactId>liquibase-maven-plugin</artifactId>
				<version>3.0.5</version>
				<configuration>
					<propertyFile>src/main/resources/liquibase/liquibase.properties</propertyFile>
				</configuration>
				<executions>
					<execution>
						<goals>
							<goal>update</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
			
			url=jdbc:h2:~/test
			username=sa
			password=sa
			driver=org.h2.Driver
			changeLogFile=src/main/resources/liquibase-ChangeLog.xml
				
		b) <plugin>
				<groupId>org.liquibase</groupId>
				<artifactId>liquibase-maven-plugin</artifactId>
				<version>3.0.5</version>
				<configuration>
					<changeLogFile>src/main/resources/org/liquibase/business_table.xml</changeLogFile>
					<driver>oracle.jdbc.driver.OracleDriver</driver>
					<url>jdbc:oracle:thin:@tf-appserv-linux:1521:xe</url>
					<username>liquibaseTest</username>
					<password>pass</password>
				</configuration>
				<executions>
					<execution>
						<phase>process-resources</phase>
						<goals>
							<goal>update</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
			
			
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<databaseChangeLog  xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
		xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.0.xsd">

	<include file="src/main/resources/liquibase/create_tables.sql"/>
	<changeSet author="John (generated)" id="1439225004329-1">
		<createTable tableName="APP_USER">
			<column autoIncrement="true" name="id" type="BIGINT">
				<constraints primaryKey="true"/>
			</column>
			<column name="accessToken" type="VARCHAR(255)"/>
			<column name="needCaptcha" type="BIT(1)">
				<constraints nullable="false"/>
			</column>
			<column name="password" type="VARCHAR(255)"/>
			<column name="refreshToken" type="VARCHAR(255)"/>
			<column name="tokenExpiration" type="datetime"/>
			<column name="username" type="VARCHAR(255)">
				<constraints nullable="false"/>
			</column>
			<column name="preference_id" type="BIGINT"/>
			<column name="address" type="VARCHAR(255)"/>
		</createTable>
	</changeSet>

</databaseChangeLog>

CREATE TABLE PRODUCT (
  PROD_ID VARCHAR(20),
  PROD_NAME VARCHAR(30)
);