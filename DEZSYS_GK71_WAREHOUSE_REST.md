# DEZSYS_GK71_WAREHOUSE_REST

Github Link: [GitHub - ThomasMicheler/DEZSYS_GK771_WAREHOUSE_REST](https://github.com/ThomasMicheler/DEZSYS_GK771_WAREHOUSE_REST.git)

## Einfuehrung

Der Lagerstandort Linz der grossen Handelskette KONSUM lagert alle Lebensmittel, Haushaltswaren und Hygieneartikel fuer die Filialen in Wien, Niederoesterreich und Burgenland. Das Lagerprogramm vor Ort soll um eine Schnittstelle erweitert werden, damit die Konzernzentrale alle Lagerdaten tagesaktuell abrufen kann. Um die Moeglichkeiten der Anbindung moeglichsts flexibel zu gestalten, sollen die Datenformate JSON und XML unterstuetzt werden.

## Daten des Lagerstandorts Lager Wien Nord

Hinzufügen Test Daten

```java

WharehauseData.java

// Erstelle ein Array von 30 Product-Objekten mit zufälligen Testdaten
this.warehouseProducts = new Product[30];

this.warehouseProducts[0] = new Product("P101", "Laptop", "Elektronik", 20, "Karton", 15, "Stück");

```

Aufbau des Produkt Objekts

```java
private String productID;
private String productName;
private String productCategory;
private int productQuantity;
private String productPackaging;
private int productSize;
private String productUnit;
public Product(String productID, String productName, String productCategory, int productQuantity, String productPackaging, int productSize, String productUnit){
    this.productID=productID;
    this.productName=productName;
    this.productCategory=productCategory;
    this.productQuantity=productQuantity;
    this.productPackaging=productPackaging;
    this.productSize=productSize;
    this.productUnit=productUnit;
}
```

Funktionsweise von **Rest**



```java
package tradearea.warehouse;

import org.springframework.web.bind.annotation.RestController;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.http.MediaType;

import tradearea.model.WarehouseData;

@RestController
public class WarehouseController {

    @Autowired
    private WarehouseService service;
	
    @RequestMapping("/")
    public String warehouseMain() {
    	String mainPage = "This is the warehouse application! (DEZSYS_WAREHOUSE_REST) <br/><br/>" +
                          "<a href='http://localhost:8080/warehouse/001/json'>Link to warehouse/001/json</a><br/>" +
                          "<a href='http://localhost:8080/warehouse/001/xml'>Link to warehouse/001/xml</a><br/>" +
                          "<a href='http://localhost:8080/warehouse/001/transfer'>Link to warehouse/001/transfer</a><br/>";
        return mainPage;
    }

    @RequestMapping(value="/warehouse/{inID}/json", produces = MediaType.APPLICATION_JSON_VALUE)
    public WarehouseData warehouseData( @PathVariable String inID ) {
        return service.getWarehouseData( inID );
    }

    @RequestMapping(value="/warehouse/{inID}/xml", produces = MediaType.APPLICATION_XML_VALUE)
    public WarehouseData warehouseDataXML( @PathVariable String inID ) {
        return service.getWarehouseData( inID );
    }

    @RequestMapping("/warehouse/{inID}/transfer")
    public String warehouseTransfer( @PathVariable String inID ) {
        return service.getGreetings("Warehouse.Transfer!");
    }

}
```

## Dokumente und Links

- XML Daten - [Warehouse](https://elearning.tgm.ac.at/mod/resource/view.php?id=79890 "warehouse") [[warehouse](https://elearning.tgm.ac.at/mod/resource/view.php?id=79890 "warehouse").xml]

- Spring Boot https://spring.io/projects/spring-boot

- Building an Application with Spring Boot https://spring.io/guides/gs/spring-boot/

- Spring Initializr [https://start.spring.io/](https://start.spring.io/)

- Building a RESTful Web Service https://spring.io/guides/gs/rest-service/

- Consuming a RESTful Web Service https://spring.io/guides/gs/consuming-rest/

- Consuming a RESTful Web Service with jQuery https://spring.io/guides/gs/consuming-rest-jquery/
