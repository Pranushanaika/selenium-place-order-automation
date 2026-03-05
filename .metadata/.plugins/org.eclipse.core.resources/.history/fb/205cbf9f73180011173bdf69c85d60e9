package Automation;

import java.time.Duration;
import java.util.List;

import org.junit.Test;
import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.Assert;
public class Firstproject {

	@Test
	public void verifyProduct() {
	{
		WebDriver driver = new ChromeDriver();
		
		driver.manage().window().maximize();
		driver.manage().deleteAllCookies();
		
		WebDriverWait Wait = new WebDriverWait(driver, Duration.ofSeconds(10));
		
		driver.get("https://practice.automationtesting.in/");
		JavascriptExecutor js = (JavascriptExecutor) driver;
		js.executeScript("window.scrollBy(0,750);");
		
		// Get Product Title from Listing Page
		String productName = driver.findElement(By.cssSelector("h3")).getText();
		System.out.println("Listing Product Name: " + productName);

		// Get Product Price from Listing Page
		String productPrice = driver.findElement(By.cssSelector(".price .woocommerce-Price-amount")).getText();
		System.out.println("Listing Product Price: " + productPrice);
		double listingPriceValue = Double.parseDouble(
		        productPrice.replaceAll("[^0-9.]", "")
		);

		System.out.println("Listing Price Numeric: " + listingPriceValue);
	
		//     Add the product to cart
		
		WebElement addToCart = Wait.until(
			    ExpectedConditions.presenceOfElementLocated(By.cssSelector(".add_to_cart_button"))
			);
		
		addToCart.click();
		
	
		//Select multiple products to cart
		
//		for (int i = 0; i < 2; i++) {
//		    List<WebElement> buttons = driver.findElements(By.cssSelector(".add_to_cart_button"));
//		    
//		    WebElement btn = buttons.get(i);
//
//		    ((JavascriptExecutor) driver).executeScript("arguments[0].click();", btn);
//		    Thread.sleep(1000);
//		   
//		}
//		
//		List<WebElement> products = driver.findElements(By.cssSelector("a.woocommerce-LoopProduct-link"));
//				
//
//		String secondProductName = products.get(1).getText(); // index 1 = second product
//		
//		System.out.println("Second Product Name: " + secondProductName);
		
		
		//  view the basket 
		
		WebElement viewBasket = Wait.until(
		    ExpectedConditions.elementToBeClickable(By.cssSelector("a.added_to_cart"))
		);

		((JavascriptExecutor) driver).executeScript("arguments[0].scrollIntoView(true);", viewBasket);
		((JavascriptExecutor) driver).executeScript("arguments[0].click();", viewBasket);
		
		// Get Product Name from Basket
		String basketProductName = Wait.until(
		        ExpectedConditions.visibilityOfElementLocated(
		                By.cssSelector(".product-name a"))).getText();

		System.out.println("Basket Product Name: " + basketProductName);

		// Get Product Price from Basket
		String basketProductPrice = driver.findElement(
		        By.cssSelector(".product-price .woocommerce-Price-amount")).getText();

		System.out.println("Basket Product Price: " + basketProductPrice);
		// Assertions to verify product details
		Assert.assertEquals(basketProductName.trim(), productName.trim(),
		        "❌ Product name mismatch between listing page and basket");

		Assert.assertEquals(basketProductPrice.trim(), productPrice.trim(),
		        "❌ Product price mismatch between listing page and basket");

		System.out.println("✅ Product name and price verified successfully.");
		
				WebElement qty = Wait.until(ExpectedConditions.visibilityOfElementLocated(
				        By.cssSelector("input.qty")
				));
				
				qty.clear();

				int userQuantity = 4;
				qty.sendKeys(String.valueOf(userQuantity));
				
				//  WAIT for basket total to refresh
				driver.findElement(By.name("update_cart")).click();

				// Wait until loader disappears (REAL FIX)
				Wait.until(ExpectedConditions.invisibilityOfElementLocated(
				        By.cssSelector(".blockUI.blockOverlay")
				));

				//  DEBUG 
				String qtyValue = driver.findElement(By.cssSelector("input.qty")).getAttribute("value");
				System.out.println("Quantity: " + qtyValue);

				List<WebElement> basketRows = driver.findElements(By.cssSelector(".cart_totals tr"));
				for (WebElement row : basketRows) {
				    System.out.println(row.getText());
				}

				// Get Basket Total
				
				String basketTotal = driver.findElement(By.cssSelector(".cart_totals .order-total .amount")).getText();
				double basketTotalValue = Double.parseDouble(
				        basketTotal.replaceAll("[^0-9.]", "")
				);

				System.out.println("Basket Total Numeric: " + basketTotalValue);
				double expectedTotal = listingPriceValue * userQuantity;

				System.out.println("Expected Total (Price × Quantity): " + expectedTotal);
				Assert.assertEquals(basketTotalValue, expectedTotal,
				        "❌ Basket total is not equal to Listing Price × Quantity");

				System.out.println("✅ Basket total matches Listing Price × Quantity");
		       

		        //  Proceed to checkout
		        WebElement checkoutBtn = Wait.until(
		                ExpectedConditions.presenceOfElementLocated(By.cssSelector(".checkout-button")));
		        js.executeScript("arguments[0].click();", checkoutBtn);
                 // WAIT for checkout table
		        Wait.until(ExpectedConditions.visibilityOfElementLocated(By.cssSelector(".shop_table")));

		        // DEBUG breakdown
		        List<WebElement> checkoutRows = driver.findElements(By.cssSelector(".shop_table tr"));
		        for (WebElement row : checkoutRows) {
		            System.out.println(row.getText());
		        }

		        // Get Checkout Total
		        WebElement checkoutTotalElement = Wait.until(
		                ExpectedConditions.visibilityOfElementLocated(By.cssSelector(".order-total .amount")));
		        String checkoutTotal = checkoutTotalElement.getText();
		        System.out.println("Checkout Total: " + checkoutTotal);

		        //  Assertion: Basket total matches Checkout total
		        Assert.assertEquals(checkoutTotal, basketTotal,
		                "❌ Total mismatch! Basket: " + basketTotal + ", Checkout: " + checkoutTotal);

		        System.out.println("✅ Total matches between Basket and Checkout.");
		      
		        //Billing details
		       Wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("billing_first_name"))).sendKeys("Pranusha");
		       driver.findElement(By.id("billing_last_name")).sendKeys("Naika");
		       driver.findElement(By.id("billing_company")).sendKeys("Techatcore");
		       driver.findElement(By.id("billing_email")).sendKeys("Pranushanaika@gmail.com");
		       driver.findElement(By.id("billing_phone")).sendKeys("8688795513");
		       driver.findElement(By.id("billing_address_1")).sendKeys("Kotagally");
			   driver.findElement(By.id("billing_city")).sendKeys("nzb");

			   WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(20));

			// Click country dropdown
			   
			   WebElement countryDropdown = wait.until(
					    ExpectedConditions.presenceOfElementLocated(By.id("s2id_billing_country"))
					);

					// Scroll properly to avoid header overlap
					((JavascriptExecutor) driver).executeScript(
					    "arguments[0].scrollIntoView({block: 'center'});", countryDropdown
					);

					// Wait until clickable
					wait.until(ExpectedConditions.elementToBeClickable(countryDropdown));

					// Try normal click
					try {
					    countryDropdown.click();
					} catch (Exception e) {
					    // Fallback to JS click if intercepted
					    ((JavascriptExecutor) driver).executeScript(
					        "arguments[0].click();", countryDropdown
					    );
					}

			// Wait for input box (Select2 creates dynamic input)
			WebElement countryInput = wait.until(
			        ExpectedConditions.visibilityOfElementLocated(
			                By.xpath("//div[@id='select2-drop']//input"))
			);
			countryInput.sendKeys("India");

			// Wait and click EXACT match (not first suggestion)
			WebElement indiaOption = wait.until(
			        ExpectedConditions.elementToBeClickable(
			        		By.xpath("(//div[@class='select2-result-label' and normalize-space()='India'])[last()]")));
			indiaOption.click();
	
			// We can user thread.sleep() method or Webdriverwait() for small wait 
			
//			Thread.sleep(2000); 
			WebDriverWait wait1 = new WebDriverWait(driver , Duration.ofSeconds(10));

			// Code for Click state dropdown
			
			WebElement stateDropdown = wait.until(
			        ExpectedConditions.elementToBeClickable(By.id("s2id_billing_state")));
			stateDropdown.click();

			// Wait for state input
			WebElement stateInput = wait.until(
			        ExpectedConditions.visibilityOfElementLocated(
			                By.xpath("//div[@id='select2-drop']//input"))
			);

			// Enter state
			stateInput.sendKeys("Telangana");
			stateInput.sendKeys(Keys.ENTER);

			WebElement postcode = wait.until(
			        ExpectedConditions.elementToBeClickable(By.id("billing_postcode"))
			);
			postcode.clear();
			postcode.sendKeys("503001");
			driver.findElement(By.id("payment_method_cod")).click();
			WebElement placeOrder = wait.until(
				    ExpectedConditions.presenceOfElementLocated(By.id("place_order"))
				);

				// scroll to button
				((JavascriptExecutor) driver).executeScript(
				    "arguments[0].scrollIntoView({block:'center'});", placeOrder);

				//  wait to avoid overlay issues
//				Thread.sleep(1000);

				// JS click (bypasses overlay issue)
				((JavascriptExecutor) driver).executeScript(
				    "arguments[0].click();", placeOrder);
				WebElement successMessage = Wait.until(
				        ExpectedConditions.visibilityOfElementLocated(
				                By.cssSelector(".woocommerce-thankyou-order-received")));

				String message = successMessage.getText();

				System.out.println("Order Message: " + message);

				Assert.assertTrue(message.contains("Thank you"),
				        "❌ Order confirmation message not displayed");

				System.out.println("✅ Order placed successfully.");
				driver.quit();
				   	          
	}
	}
}


