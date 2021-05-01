---
title: Spring MVC
subtitle: "\" \"— Jean Sibelius"
date: 2020-03-19 17:06:29
tags: 
    - Spring MVC
---
> An investment in knowledge pays the best interest.

![learning](https://miro.medium.com/max/1300/1*HVk_I6uY39blUq-W6sEELA.png)
<small class="img-hint">“The mind, once stretched by a new idea, never returns to its original dimensions.” — Ralph Waldo Emerson</small>

## Following The Life of a Request
![Spring-MVC](Spring.png)
<small class="img-hint">request couriers information to several stops on its way to producing the desired results.</small>

When the request leaves the browser ❶, it carries information about what the user is asking for. At the least, the request will be carrying the requested URL. But it may also carry additional data, such as the information submitted in a form by the user.

The first stop in the request's travel is at Spring's **DispatcherServlet**. Like most Java-based web frameworks, Spring MVC funnels requests through a single front controller servlet. A **front controller** is a common web application pattern where a single servlet delegates responsibility for a request to other components of an application to perform actual processing. In the case of Spring MVC, **DispatcherServlet** is the front controller.

The **DispatcherServlet**'s job is to send the request to a Spring MVC controller. A **controller** is a Spring component that process the request. But a typical application may have several controllers, and **DispatcherServlet** needs some help deciding which controller to send the request to. So the **DispatcherServlet** consults one or more **handler mappings** ❷ to figure out where the request's next stop will be. The handler mapping pays particular attention to the URL carried by the request when making its decision.

Once an appropriate controller has been chosen, DispatcherServlet sends the request on its merry way to the chosen controller ❸. At the controller, the request drops off its payload (the information submitted by the user) and patiently waits while the controller processes that information. (Actually, a well-designed controller performs little or no processing itself and instead delegates responsibility for the business logic to one or more service objects.)

The logic performed by a controller often results in some information that needs to be carried back to the user and displayed in the browser. This information that needs to be carried back to the user and displayed in the browser. This information is referred to as the **model**. But sending raw information back to the user isn't sufficient--it needs to be formatted in a user-friendly format, typically HTML. For that, the information needs to be given to a view, typically a JavaServer Page (**JSP**).

One of the last things a controller does is package up the package up the model data and identify the name of a view that should render the output. It then sends the request, along with the model and view name, back to the **DispatcherServlet** ❹.

So that the controller doesn’t get coupled to a particular view, the view name passed back to **DispatcherServlet** doesn’t directly identify a specific JSP. It doesn’t even necessarily suggest that the view is a JSP. Instead, it only carries a logical name that will be used to look up the actual view that will produce the result. The **DispatcherServlet** consults a view resolver ❺ to map the logical view name to a spe- cific view implementation, which may or may not be a JSP.

Now that **DispatcherServlet** knows which view will render the result, the request’s job is almost over. Its final stop is at the view implementation ❻, typically a JSP, where it delivers the model data. The request’s job is finally done. The view will use the model data to render output that will be carried back to the client by the (not- so-hardworking) response object ❼.

 

