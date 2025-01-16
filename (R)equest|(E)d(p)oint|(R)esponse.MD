# REPR - (R)equest|(E)d(p)oint|(R)esponse Pattern

* <a href="https://medium.com/codenx/repr-pattern-endpoints-in-net-8-013fff3e8cfa">Medium Blog</a>


* The REPR design pattern is an approach that helps developers enhance code maintainability, reusability, and extensibility by isolating concerns.
* Developers may create well-structured and easily expandable APIs by concentrating on the request, endpoint, and response.

* The REPR design pattern promotes modularization and guarantees a distinct separation between the input request, the logic at the endpoint, and the output response.
* The REPR design pattern simplifies API development by organizing your APIs around endpoints instead of controllers.
* Remember that the REPR design pattern is neither REST-based nor resource-based.
* Instead, it is a pattern used for defining your API endpoints.


* The REPR pattern solves the problem of controller by eliminating the need to have multiple action methods in one controller.
* Instead, the REPR pattern adheres to the single responsibility principle, allowing you to have one controller per action supported in a typical use case.
* * Other key benefits include the separation of concerns, improved code reusability, improved readability and maintainability, better testability and simpler debugging, and improved security and scalability.

* However, the REPR pattern also has certain downsides. These include increased complexity and duplication of code.

* CreateCustomerController.cs
```
using Microsoft.AspNetCore.Mvc;
using Swashbuckle.AspNetCore.Annotations;
using System.Net.Mime;

namespace Endpoints.Customer.CreateCustomer
{
    [Produces(MediaTypeNames.Application.Json)]
    [Consumes(MediaTypeNames.Application.Json)]
    [Route("api/[controller]")]
    [ApiController]
    public class CreateCustomerController : ControllerBase
    {
        [HttpPost(Name = "CreateCustomer")]
        [ProducesResponseType(StatusCodes.Status204NoContent)]
        [SwaggerOperation(Tags = new[] { "Customer" })]
        public ActionResult CreateCustomerAsync(CreateCustomerRequest request)
        {
            //TODO: Implement logic like validation, mapping etc.
            return NoContent();
        }
    }
}
```

* CreateCustomerRequest.cs
```
using Endpoints.Customer.CreateCustomer;

namespace Endpoints.Customer.UpdateCustomer
{
    public class UpdateCustomerRequest : CreateCustomerRequest
    {
        public int Id { get; set; }
    }
}
```

* GetCustomerByIdController.cs
```
using Microsoft.AspNetCore.Mvc;
using Swashbuckle.AspNetCore.Annotations;
using System.Net.Mime;

namespace Endpoints.Customer.GetCustomerById
{
    [Produces(MediaTypeNames.Application.Json)]
    [Consumes(MediaTypeNames.Application.Json)]
    [Route("api/[controller]")]
    [ApiController]
    public class GetCustomerByIdController : ControllerBase
    {
        [HttpGet("{id}", Name = "GetCustomerById")]
        [ProducesResponseType(StatusCodes.Status200OK)]
        [SwaggerOperation(Tags = new[] { "Customer" })]
        public ActionResult GetCustomerByIdAsync(int id)
        {
            return Ok(new GetCustomerByIdResponse { CustomerId = id });
        }
    }
}
```

* GetCustomerByIdResponse.cs
```
namespace Endpoints.Customer.GetCustomerById
{
    public class GetCustomerByIdResponse
    {
        public int CustomerId { get; set; }

        public string FirstName { get; set; }

        public string LastName { get; set; }

        public int Age { get; set; }

        public string Email { get; set; }
    }
}

```

* UpdateCustomerController.cs
```
using Microsoft.AspNetCore.Mvc;
using Swashbuckle.AspNetCore.Annotations;
using System.Net.Mime;

namespace Endpoints.Customer.UpdateCustomer
{
    [Produces(MediaTypeNames.Application.Json)]
    [Consumes(MediaTypeNames.Application.Json)]
    [Route("api/[controller]")]
    [ApiController]
    public class UpdateCustomerController : ControllerBase
    {
        [HttpPost(Name = "UpdateCustomer1")]
        [ProducesResponseType(StatusCodes.Status204NoContent)]
        [SwaggerOperation(Tags = new[] { "Customer" })]
        public ActionResult UpdateCustomer1Async(UpdateCustomerRequest request)
        {
            //TODO: Implement logic like validation, mapping etc.
            return NoContent();
        }
    }
}
```

* UpdateCustomerRequest.cs
```
using Endpoints.Customer.CreateCustomer;

namespace Endpoints.Customer.UpdateCustomer
{
    public class UpdateCustomerRequest : CreateCustomerRequest
    {
        public int Id { get; set; }
    }
}
```
