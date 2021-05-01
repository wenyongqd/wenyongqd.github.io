---
title: Refactoring in Action
subtitle: "\"Anyone can be cool, but awesome take practice.\""
author:     "Wenyong"
header-img: "post-bg-js-version.jpg"
date: 2020-03-14 17:39:51
tags:
    - Refactor
    - Java
---


### Rafactoring, a First Example
The sample program is very simple. It is a program to calculate and print a statement of a customer's charges at a video store.

![uml](uml.png)
<small class="img-hint">Class diagram of the starting-point classes. Only the most important features are shown.</small>

##### Movie
```java
public class Movie {
    public static final int CHILDRENS = 2;
    public static final int REGULAR = 0;
    public static final int NEW_RELEASE = 1;

    private String title;
    private int priceCode;

    public Movie(String title, int priceCode) {
	this.title = title;
	this.priceCode = priceCode;
    }
    public int getPriceCode() {
	return priceCode;
    }
    public void setPriceCode(int arg) {
	priceCode = arg;
    }
    public String getTitle() {
	return title;
    }
}
```

##### Rental
```java
public class Rental {

    private Movie movie;
    private int daysRented;

    public Rental(Movie movie, int daysRented) {
	this.movie = movie;
	this.daysRented = daysRented;
    }

    public int getDaysRented() {
	return daysRented;
    }

    public Movie getMovie() {
	return movie;
    }
}
```

##### Customer
```java
public class Customer {
    private String name;
    private List rentals = new ArrayList();

    public Customer(String name) {
	this.name = name;
    }
    public String getName() {
	return name;
    }
    public void addRental(Rental arg) {
	rentals.add(arg);
    }
    public String statement() {
	double totalAmount = 0;
	int frequentRenterPoints = 0;
	Iterator rentalIterator = rentals.iterator();
	String result = "Rentals: " + getName() + "\n";
	while (rentalIterator.hasNext()) {
	    double thisAmount = 0;
	    Rental each = (Rental) rentalIterator.next();

	    //determine amounts for each line
		switch (each.getMovie().getPriceCode()) {
			case Movie.REGULAR:
				thisAmount += 2;
				if (each.getDaysRented() > 2)
					thisAmount += (each.getDaysRented() - 2) * 1.5;
				break;
			case Movie.NEW_RELEASE:
				thisAmount += each.getDaysRented() * 3;
				break;
			case Movie.CHILDRENS:
				thisAmount += 1.5;
				if (each.getDaysRented() > 3)
					thisAmount += (each.getDaysRented() - 3) * 1.5;
				break;
		}

	    // add frequent renter points
	    frequentRenterPoints ++;
	    // add bonus for a two day new release rental
	    if ((each.getMovie().getPriceCode() == Movie.NEW_RELEASE) &&
		each.getDaysRented() > 1) frequentRenterPoints ++;

	    //show figures for this rental
	    result += each.getDaysRented() +
		" days of '" + each.getMovie().getTitle() +
		"' $" + String.valueOf(thisAmount) + "\n";
	    totalAmount += thisAmount;
	}
	//add footer lines
	result += "Total = $" + totalAmount + "\n";
	result += "Frequent renter points = " + frequentRenterPoints + "\n";
	return result + "---\n";
    }
}
```
### The First Step in Refactoring

Whenever I do refactoring, the first step is always the same. I need to build a solid set of tests for that section of code. The tests are essential because even though I follow refactorings structured to avoid most of the opportunities for introducing bugs, I'm still human and still make mistakes. 

##### TestMovieRental
```java
import junit.framework.TestCase;

public class TestMovieRental extends TestCase {
    private Rental rentMatrix, rentMatrix2;
    private Customer customer;

    public void setUp() {
	rentMatrix = new Rental(new Movie("Matrix",Movie.REGULAR),4);
	rentMatrix2 = new Rental(new Movie("Matrix2",Movie.NEW_RELEASE),5);
	customer = new Customer("John Hood");
    }
    public void testInitialCustomer() {
	assertEquals("Rentals: John Hood\n"+
		     "Total = $0.0\n"+
		     "Frequent renter points = 0\n"+
		     "---\n",
		     customer.statement());
    }
    public void testRentingCustomer() {
	customer.addRental(rentMatrix);
	customer.addRental(rentMatrix2);
	assertEquals("Rentals: John Hood\n"+
		     "4 days of 'Matrix' $5.0\n"+
		     "5 days of 'Matrix2' $15.0\n"+
		     "Total = $20.0\n"+
		     "Frequent renter points = 3\n"+
		     "---\n",
		     customer.statement());
    }
/*---- public void testHtmlCustomer() {
	customer.addRental(rentMatrix);
	customer.addRental(rentMatrix2);
	assertEquals("<html><head><title>Rentals: John Hood</title></head><body>\n"+
		     "<h1>Rentals: John Hood</h1>\n"+
		     "<table border=1><tr><th>Days</th><th>Title</th><th>Charge</th></tr>\n"+
		     "<tr><td align=right>4</td><td>Matrix<td align=right>$5.0</td></tr>\n"+
		     "<tr><td align=right>5</td><td>Matrix2<td align=right>$15.0</td></tr>\n"+
		     "<tr><td></td><td><i>total</i><td align=right>$20.0</td></tr>\n"+
		     "</table><p>Frequent renter points = 3</p>\n"+
		     "</body></html>\n",
		     customer.htmlStatement());
    }
--- */
}
```
---
### Decomposing and Redistributing the Statement Method

The obvious first target of my attention is the overly long statement method. When I look at a long method like that, I am looking to decompose the method into smaller pieces. Smaller pieces of code tend to make things more manageable.

My first step is to find a logical clump of code and use Extract Method. An obvious piece here is the switch statement. This looks like it would make a good chunk to extract into its own method.

```java
public class Customer {
    private String name;
    private List rentals = new ArrayList();

    public Customer(String name) {
	this.name = name;
    }
    public String getName() {
	return name;
    }
    public void addRental(Rental arg) {
	rentals.add(arg);
    }
    public String statement() {
	double totalAmount = 0;
	int frequentRenterPoints = 0;
	Iterator rentalIterator = rentals.iterator();
	String result = "Rentals: " + getName() + "\n";
	while (rentalIterator.hasNext()) {
	    double thisAmount = 0;
	    Rental each = (Rental) rentalIterator.next();

	    //determine amounts for each line
	    thisAmount = chargeForRental(thisAmount, each);

	    // add frequent renter points
	    frequentRenterPoints ++;
	    // add bonus for a two day new release rental
	    if ((each.getMovie().getPriceCode() == Movie.NEW_RELEASE) &&
		each.getDaysRented() > 1) frequentRenterPoints ++;

	    //show figures for this rental
	    result += each.getDaysRented() +
		" days of '" + each.getMovie().getTitle() +
		"' $" + String.valueOf(thisAmount) + "\n";
	    totalAmount += thisAmount;
	}
	//add footer lines
	result += "Total = $" + totalAmount + "\n";
	result += "Frequent renter points = " + frequentRenterPoints + "\n";
	return result + "---\n";
    }
    
	private double chargeForRental(double thisAmount, Rental each) {
		switch (each.getMovie().getPriceCode()) {
	    case Movie.REGULAR:
		thisAmount += 2;
		if (each.getDaysRented() > 2)
		    thisAmount += (each.getDaysRented() - 2) * 1.5;
		break;
	    case Movie.NEW_RELEASE:
		thisAmount += each.getDaysRented() * 3;
		break;
	    case Movie.CHILDRENS:
		thisAmount += 1.5;
		if (each.getDaysRented() > 3)
		    thisAmount += (each.getDaysRented() - 3) * 1.5;
		break;
	    }
		return thisAmount;
	}
}
```
<img class="shadow" width="320" src="https://i.pinimg.com/originals/3f/7b/b2/3f7bb2b20904c961f25fa065a9c7d102.jpg" />