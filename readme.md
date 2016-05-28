#Spring boot
Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run"

##Requirment
1. Build with maven.
2. Install with http://start.spring.io/ and JPA Configuration. - download
3. Extract and import maven project with IDE Eclipse.
4. Add Depedency Mysql Connector with MYSQL.
5. Add configuration application.properties.
6. Create java bean entity with Annotation (Hibernate), - Clean & Build.

##Code
	4. Add Depedency Mysql Connector with MYSQL.
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<version>5.1.35</version>
		</dependency>
	
	5. Add configuration application.properties.
		spring.datasource.url=jdbc:mysql://localhost/arrizaqu
		spring.datasource.username=root
		spring.datasource.password=
		spring.datasource.driver-class-name=com.mysql.jdbc.Driver
		spring.jpa.generate-ddl=true
	
	6. Create java bean entity with Annotation (Hibernate), - Clean & Build.
		@Entity
		public class Customer {
			@Id
			private String id;
			@Column(name="name")
			private String name;
			@Column(name="email", nullable=false, unique=true)
			private String email;
	
##Reference
1. http://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/

