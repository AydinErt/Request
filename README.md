# Request


package master_branch.http_request.Day_05;

import io.restassured.http.ContentType;
import io.restassured.response.Response;
import org.junit.Before;
import org.junit.Test;

import static io.restassured.RestAssured.*;
import static org.junit.Assert.assertEquals;

public class GetRequest_11 {

    @Before
    public void setUp() {
        // RestAssured baseURI = ConfigurationReader.get("pet_store_url");
        //  String url ="https://petstore.swagger.io/v2/pet/findByStatus?status=sold";

    }

    @Test
    public void singleQueryParamTest() {




        String url ="https://reqres.in/api/users?page=2&per_page=3";
       /*  Response response = given().accept(ContentType.JSON).queryParam("page", "2").
                 queryParam("per_page", "3").
                 get(""); */
        Response response = given().get(url);
        response.prettyPrint();


        response.then().assertThat()
                .statusCode(200)
                .contentType("application/json")
                .statusLine("HTTP/1.1 200 OK");


        int firstDataId=response.path("data[0].id");
        int firstDataId2=response.path("data.id[0]");
        System.out.println("firstDataId = " + firstDataId2);


        String firstDataEmail = response.path("data[0].email");
        String firstDataFirst_name= response.path("data[0].first_name");
        String firstDataLast_name = response.path("data.last_name[0]");
        String firstDataAvatar= response.path("data[0].avatar");

        assertEquals(4, firstDataId);
        assertEquals("eve.holt@reqres.in", firstDataEmail);
        assertEquals("Eve", firstDataFirst_name);
        assertEquals("Holt", firstDataLast_name);
        assertEquals("https://reqres.in/img/faces/4-image.jpg", firstDataAvatar);



        String nameEve =response.path("data.find{it.id==4}.first_name");
        System.out.println("nameEve = " + nameEve);




}
}
