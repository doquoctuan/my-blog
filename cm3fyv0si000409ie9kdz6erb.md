---
title: "Folder Structures in .NET Projects: A Comprehensive Guide"
datePublished: Wed Nov 13 2024 14:18:24 GMT+0000 (Coordinated Universal Time)
cuid: cm3fyv0si000409ie9kdz6erb
slug: folder-structures-in-net-projects-a-comprehensive-guide
tags: net

---

1. #### **Basic** [**ASP.NET**](http://ASP.NET) **MVC Project**
    

```plaintext
/Controllers/
    HomeController.cs
/Models/
    Product.cs
    Order.cs
/Views/
    /Home/
        Index.cshtml
    /Shared/
        _Layout.cshtml
/Services/
    OrderService.cs
/DataAccess/
    ProductRepository.cs
```

2. #### **Feature-Based Project**
    

```plaintext
/Features/
    /Products/
        Models/
            Product.cs
        Controllers/
            ProductController.cs
        Views/
            ProductView.cshtml
        Services/
            ProductService.cs
    /Orders/
        Models/
            Order.cs
        Controllers/
            OrderController.cs
        Views/
            OrderView.cshtml
        Services/
            OrderService.cs
```

3. #### **DDD Project Structure**
    

```plaintext
/Domain/
    /Products/
        Product.cs
        ProductService.cs
        ProductRepository.cs
    /Orders/
        Order.cs
        OrderService.cs
        OrderRepository.cs
/Infrastructure/
    /Persistence/
        DatabaseContext.cs
    /Repositories/
        ProductRepository.cs
/Application/
    /Commands/
        CreateProductCommand.cs
    /Queries/
        GetProductByIdQuery.cs
```