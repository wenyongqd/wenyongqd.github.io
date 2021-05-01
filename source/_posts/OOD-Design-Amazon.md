---
title: OOD-Design Amazon
subtitle: "\"Anyone can be cool, but awesome take practice.\""
date: 2020-07-02 14:03:18
header-img: "banner-902587_1280.jpg"
tags:
    - OOD
---
![image](chalk-1839568__480.jpg)
> "成功好像一门孤独的行为艺术。对于成功者而言，只有两天是开心的，一个是做决定的那天，一个是收获的那天，剩下的时间，都是无止境的煎熬和绚烂后的平静"

> "我们最大的敌人，就是自我怀疑"
## Requirements and Goals of the System   
****
##### We will designing a system with the following requirements: 
1. Users should be able to add new items to sell.   
2. Users should be able to search for products by their name or category.
3. Users can search and view all the products, but they have to become a registered member to buy a product.
4. Users should be able to add/modify/remove product items in their shopping cart.
5. Users can checkout and buy items in their shopping cart.
6. Users can rate and add a review for a product.
7. The User should be able to specify a shipping address where their order will be delivered.
8. Users can cancel an order if it has not shipped.
9. Users should get notifications whenever there is a change in the order or shipping status.
10. Users should be able to pay through credit cards or electronic bank transfer.
11. Users should be able to track their shipment to see the current state of their order.

## Use case Diagram
##### We have four main Actors in our system:     
- **Admin**: Mainly responsible for account management and adding or modifying new product categories.
- **Guest**: All guests can search the catalog, add/remove items to the shopping cart, as well as become registered members.
- **Member**: Members can perform all the activities that guests can, in addition to which, they can place orders and add new products to sell.
- **System**: Mainly responsible for sending notifications for orders and shipping updates.

Here are the top use cases of the Online Shopping System:

1. Add/update products; whenever a product is added or modified, we will update the catalog.
2. Search for products by their name or category.
3. Add/remove product items in the shopping cart.
4. Check-out to buy product items in the shopping cart.
5. Make a payment to place an order.
6. Add a new product category.
7. Send notifications to members with shipment updates.