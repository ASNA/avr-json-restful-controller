Json RESTful controller for AVR

The ASNA.JsonRestRouting library provides the classes needed to provide a Json RESTful API for ASNA Visual RPG for .NET. The ASNA.JsonRestRouting library was written in ASNA Visual RPG. It's intent is to make it easy to work with Json in your AVR apps. 

The library includes three classes: 

* Controller - The base controller from which you'll derive your own custom controllers.
* RouteAction - A class, derived from `System.Web.Routing.iRouteHandler` that instances an returns a given controller. You won't use this class directly. 
* Router - A class that routes RESTful routes you provide. It uses ASP.NET's built-in `System.Web.Routing` routing engine. You won't use this class directly. 

The library isn't documented yet, but you can learn a lot about it from these examples: 

* [A very basic example that can also be used a project template ](https://github.com/ASNA/avr-restful-api-template)

* [A more advanced example that shows how to populate a client-side grid with this library](https://github.com/ASNA/avr-restful-api-with-tabulator)

Here is a quick example of a RESTful controller. The AVR Json RESTful library automatically converts any return value to Json. 

    Using System
    Using System.Collections.Generic
    
    // An example controller.
    BegClass CustomerController Access(*Public) Extends(ASNA.JsonRestRouting.Controller)

        // Example ShowAction method. 
        BegFunc ShowAction Access(*Public) Type(CustomerEntity) 
            DclSrParm Id Type(*Integer4) 
    
            // This method hardcodes a customer lookup. In production, you'd use the given Id value 
            // to look up the exact customer number. 
    
            DclFld Entity Type(CustomerEntity) New()
            Entity.CMCustNo = Convert.ToInt32(Id)
            Entity.CMName = 'Neil Young'
            Entity.CMAddr1 = 'Broken Arrow'
            Entity.CMCity = 'Santa Cruz'
            Entity.CMState = 'CA'
            Entity.CMCntry = 'US'
            Entity.CMPostCode = '95603'
            Entity.CMPhone = '(831) 205-3345'
            Entity.CMFax  = 8312053346
            Entity.CMActive = '1'
    
            // The ASNA.JsonRestRouting router implicitly maps the return type to Json. 
            LeaveSr Entity 
        EndFunc        
    
    EndClass
    
    // Example entity class. 
    BegClass CustomerEntity Access(*Public)
        DclProp CMCustNo    Type(*Integer4) Access(*Public)
        DclProp CMName      Type(*String) Access(*Public)
        DclProp CMAddr1     Type(*String) Access(*Public)
        DclProp CMCity      Type(*String) Access(*Public)
        DclProp CMState     Type(*String) Access(*Public)
        DclProp CMCntry     Type(*String) Access(*Public)
        DclProp CMPostCode  Type(*String) Access(*Public)
        DclProp CMActive    Type(*String) Access(*Public)
        DclProp CMFax       Type(*Packed) Len(9,0) Access(*Public)
        DclProp CMPhone     Type(*String) Access(*Public)
    EndClass
        
