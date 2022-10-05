# Price-Engine :
~~~~~~~~~~~~~~~~
                Automated the purchas and checkout process of a bookshop
List of class  :
~~~~~~~~~~~~~~~~
/price-engine/src/main/java/com/ecom/bookShop/BookShopApplication.java :
                Is the entry point of the application
/price-engine/src/main/java/com/ecom/bookShop/controller/BookShopController.java:
                Endpoint explore class.It convert the response to JSON. 
                It ensure the data return by each method directly to JSON.
		/getPrice = It get the proces based on book title
		/checkout = Checkout the selected product added to cart and returns the bill amount
/price-engine/src/main/java/com/ecom/bookShop/dto/BookInfo.java:
                Is the Java Bean with below fields
	                title as string   
                        price as decimal
                        publishedOn as a integer
/price-engine/src/main/java/com/ecom/bookShop/dto/Checkout.java
                Class that will produce the final amount to be paid when given a list of books.
                        BookInfo as a List
                        totalDiscount as double
                        totalPrice  as double
                        totalPriceAfterDisc  as double
/price-engine/src/main/resources/rule/products.json 
                Added all books details. title,publishedYear & price are the fields 
/price-engine/src/main/resources/rule/rule.json
                Following busniess logic added 
                   I) All books published after 2000 have 10% discount.
                        -----------------------------------------
                        "name" : "Published after 2000 Year",
                        "discount" : 10,
                        "type" : "direct_discount_published_year"

                   II)Buy books worth more than £30 in total, get a 5% discount on the total.
                        -----------------------------------------
                        "name" : "Total greater than >30",
                        "discount" : 5,
                        "type" : "direct_discount_greater_30"
                
/price-engine/src/main/java/com/ecom/bookShop/service/BookShopService.java 
                It has two methods
                getPrice and checkOut
/price-engine/src/main/java/com/ecom/bookShop/service/BookShopServiceImpl.java
                getPrice method :-
                         a) Get the product details from products.json
                         b) Based on book Title get the price 
                         c) If given book not found throws exception as "Book not available, try another !!";
                         d) If system unable to read products.json file throws exception
                checkOut method :-
                         a) Get the product details from products.json
                         b) Calculates the total price with a 10% discount only for books published after 2000 
                         c) Calculates the total price with a 5% discount only for Buy books worth more than £30 in total
	

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


/price-engine/src/test/java/com/ecom/bookShop/controller/BookShopControllerTest.java

[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running TestSuite
[INFO] Tests run: 16, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.879 s - in TestSuite
[INFO] 
[INFO] Results:
[INFO] 
[INFO] Tests run: 16, Failures: 0, Errors: 0, Skipped: 0



~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
/price-engine/src/test/java/com/ecom/bookShop/service/BookShopServiceImplTest.java
Passed 8
Failed 0


~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~POSTMAN 
 
Import --> BookShop.postman_collection.json
select " Collections " --> getPrice 
                       GET: URL :http://localhost:2022/getPrice?title=Moby Dick
					   Select "Send"
					   Body : £15.20
					   ---> checkout
					   POST : URL :http://localhost:2022/checkout
					    Select "Send"
						Body:
					    "totalDiscount": 3.0,
						"totalPrice": 38.0,
						"totalPriceAfterDisc": 35.0
					   


Important Note :
~~~~~~~~~~~~~~~~
1) Common utilities like Exception handling,Logger and Common methods
3) Rules engine { rule.json and products.json } is easily extendable to include other discounts.
