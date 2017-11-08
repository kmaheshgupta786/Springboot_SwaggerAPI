Spring Boot + Swagger API Integration


Simple code link:

https://dzone.com/articles/spring-boot-restful-api-documentation-with-swagger


Dependencies:
-------------

<dependency>
	<groupId>io.springfox</groupId>
	<artifactId>springfox-swagger2</artifactId>
	<version>2.7.0</version>
	<scope>compile</scope>
</dependency>
<dependency>
	<groupId>io.springfox</groupId>
	<artifactId>springfox-swagger-ui</artifactId>
	<version>2.7.0</version>
	<scope>compile</scope>
</dependency>

in Main Class:
---------------

Annotations:

@Configuration
@EnableSwagger2

Method inside class:

@Bean
public Docket newsApi() {
	return new Docket(DocumentationType.SWAGGER_2)
			.select()
			.apis(RequestHandlerSelectors.basePackage("com.cisco.sso.nba.synup"))
			.paths(regex("/dsyncup/.*"))
			.build();
}



=================================================

sample code snippet :


@Configuration
@EnableSwagger2
....
public class NbaSyncUpBootApplication {
	
	public static void main(String[] args) {
	
		printMemoryBefore();
		SpringApplication.run(NbaSyncUpBootApplication.class, args);
		printMemoryAfter();
	}
	
		
	@Bean
    public Docket newsApi() {
        return new Docket(DocumentationType.SWAGGER_2)
                .select()
                .apis(RequestHandlerSelectors.basePackage("com.cisco.sso.nba.synup"))   
                .paths(regex("/dsyncup/.*"))
                .build();
    }
}

=================================================

problem : Got Runtime Exception
	java.lang.NoSuchMethodError: com.google.common.collect.Multimaps.asMap(Lcom/google/common/collect/ListMultimap;)Ljava/util/Map;
	
solution :
	Issue with guava.jar file.
	
	Details:
	1. My project was running on guava 14.0 version.
	2. After adding dependencies its compiled correctly but failed at run time. Given the exception as "java.lang.NoSuchMethodError: com.google.common.collect.Multimaps.asMap(Lcom/google/common/collect/ListMultimap;)Ljava/util/Map;"
	3. To solve this - updated guava 14.0 version with 17.0 version
	4. Ran on browser:
		http://localhost:9999/NbaSynUpService/swagger-ui.html#/
		
		It listed out all apis.

