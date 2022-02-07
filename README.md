# RESTAssured_API_Testing
## Tast Discription.
Document a test plan and testing checklist for a REST API of your choice (ex: Google Maps API, Skyscanner, Yahoo Finance, etc) 2. Implement 3 simple tests in the programming language and framework of your choice. The tests might include HTTP method testing, API error handling, or content validation, but ultimately it is up to you to choose which test to demonstrate.

### POM.xml
It contains all the TEST DEPENDENCIES
1. Rest Assured
2. TestNG
3. Json-simple
4. apache poi
5. Gson
### GET Class contain
1.Google Map API Status Code and Status line validation
2.Google Map- Header Validation
3.Google Map-Printing All Header
import org.testng.Assert;
import org.testng.annotations.Test;

import io.restassured.RestAssured;
import io.restassured.response.Response;
import io.restassured.specification.RequestSpecification;

public class Test_Get_request {
	@Test
	void Google_Map_Get_req()
	{				
		Response response= RestAssured.get("https://maps.googleapis.com");
		System.out.println(response.asString());
		System.out.println(response.getBody().asString());
		System.out.println(response.statusCode());
		System.out.println(response.statusLine());
		System.out.println(response.getHeader("Content_Type"));
		System.out.println(response.getContentType());
		System.out.println(response.getTime()); 
		
		
		int statusCode= response.getStatusCode();
		Assert.assertEquals(statusCode, 200);
		System.out.println("status code is  " +statusCode);
		String statusLine= response.getStatusLine();
   	System.out.println("status Line is  " +statusLine); 			
	}
	
	void Google_Map_Nearest_Resuarent()
	{
				/*--String responseBody= response.getBody().asString();
		System.out.println("Response Body is  " +responseBody);***/
		Response response= RestAssured.get("https://maps.googleapis.com");
		System.out.println(response.getContentType());
		
		String contentType= response.header("Content_type");
		System.out.println("status Line is  " +contentType); 
		Assert.assertEquals(contentType, "text/html; charset=UTF-8");		
	}	

}
## Post,PUT,Delete Class contain
1. Insert a person details, update an delete.

### Post
import java.util.HashMap;
import java.util.Map;
import org.json.simple.JSONObject;
import org.testng.annotations.Test;
import static io.restassured.RestAssured.* ;
import io.restassured.RestAssured;
import io.restassured.response.Response;

public class Test_post_request {
	@Test
	 void test_01_post() {
		Map<String, Object> map= new HashMap<String, Object>();		
		Response response= RestAssured.get("https://reqres.in/api/users");
		map.put("First Name:", "Tahia");
		map.put("Last Name", "Mahee");
		map.put("UserName", "Tahia");
		map.put("Pass:", "Tahia123");
		map.put("Email: ", "tahiamahee@gmail.com");		
		
		/*String responseBody= response.getBody().asString();
		System.out.println("Response Body is  " +responseBody);*/
		System.out.println(map);
		JSONObject request = new JSONObject(map);
		System.out.println(request);
		
		given().header("Contant_Type","application/json").body(request.toJSONString()).
		when().post("https://reqres.in/api/users").
		then().statusCode(201);
		
		System.out.println(response.asString());
		System.out.println(response.getBody().asString());
		System.out.println(response.statusCode());
		System.out.println(response.statusLine());
		System.out.println(response.getHeader("Content_Type"));
		System.out.println(response.getContentType());
		System.out.println(response.getTime()); 

		try{

			when().
		post("https://reqres.in/api/users").
		then().statusCode(204).
		log().all();
		}
		catch(AssertionError ae){
           
			System.out.println("Invalied error code");}}}

### Put
import static io.restassured.RestAssured.given;
import static io.restassured.RestAssured.when;

import java.util.HashMap;
import java.util.Map;

import org.json.simple.JSONObject;
import org.testng.annotations.Test;

import io.restassured.RestAssured;
import io.restassured.response.Response;

public class Test_put {


@Test
void test_01_put() {
	Map<String, Object> map= new HashMap<String, Object>();
	
	/***Response response= RestAssured.get("http://restapi.demoqa.com/customer");***/
	map.put("First Name:", "Tahia");
	map.put("Last Name", "Mahee");
	map.put("UserName", "Tahia");
	map.put("Pass:", "Tahia123");
	map.put("Email: ", "tahiamahee@gmail.com");
	/*String responseBody= response.getBody().asString();
	System.out.println("Response Body is  " +responseBody);*/
	System.out.println(map);
	JSONObject request = new JSONObject(map);
	System.out.println(request);
	
	Response response= RestAssured.get("https://reqres.in/api/users/2");
	given().header("Contant_Type","application/json").body(request.toJSONString()).
	when().put("https://reqres.in/api/users/2").
	then().statusCode(200);

	System.out.println(response.asString());
	System.out.println(response.getBody().asString());
	System.out.println(response.statusCode());
	System.out.println(response.statusLine());
	System.out.println(response.getHeader("Content_Type"));
	System.out.println(response.getContentType());
	System.out.println(response.getTime()); 

	try{

		when().
	put("https://reqres.in/api/users/2").
	then().statusCode(204).
	log().all();
	}
	catch(AssertionError ae){
       
		System.out.println("Invalied error code will be 200");}
}
	
}


  
 ### Delete
import static io.restassured.RestAssured.*;
import java.util.HashMap;
import java.util.Map;
import org.json.simple.JSONObject;
import org.testng.annotations.Test;
import io.restassured.RestAssured;
import io.restassured.response.Response;
public class Test_Delete {
	
	@Test
	 void test_01_Delete() {
		
		Response response= RestAssured.get("https://reqres.in/api/users/2");
	
		when().
		delete("https://reqres.in/api/users/2").
		then().statusCode(204).
		log().all();
			
		System.out.println(response.asString());
		System.out.println(response.getBody().asString());
		System.out.println(response.statusCode());
		System.out.println(response.statusLine());
		System.out.println(response.getHeader("Content_Type"));
		System.out.println(response.getContentType());
		System.out.println(response.getTime()); 

		try{

			when().
		delete("https://reqres.in/api/users/2").
		then().statusCode(204).
		log().all();
		}
		catch(AssertionError ae){
           
			System.out.println("Invalied error code");}}}
      
### Error_Handeling

import static io.restassured.RestAssured.when;

import org.testng.annotations.Test;

import io.restassured.RestAssured;
import io.restassured.response.Response;

public class Error_handeling {

	@Test
	 void test_error_handel() {	
		
		try{

			Response response= RestAssured.get("https://reqres.in/api/users/2");
		when().
		delete("https://reqres.in/api/users/2").
		then().statusCode(204).
		log().all();
		}
		catch(AssertionError ae){
           
			System.out.println("Invalied error code");}}




  
  
  




