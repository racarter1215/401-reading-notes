# Policies

### Example of policy:
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);

    services.AddAuthorization(options =>
    {
        options.AddPolicy("AtLeast21", policy =>
            policy.Requirements.Add(new MinimumAgeRequirement(21)));
    });
}

##### The above has a single requirement (over 21)

##### Example of IAuthorizationService:
/// <summary>
/// Checks policy based permissions for a user
/// </summary>
public interface IAuthorizationService
{
    /// <summary>
    /// Checks if a user meets a specific set of requirements for the specified resource
    /// </summary>
    /// <param name="user">The user to evaluate the requirements against.</param>
    /// <param name="resource">
    /// An optional resource the policy should be checked with.
    /// If a resource is not required for policy evaluation you may pass null as the value
    /// </param>
    /// <param name="requirements">The requirements to evaluate.</param>
    /// <returns>
    /// A flag indicating whether authorization has succeeded.
    /// This value is <value>true</value> when the user fulfills the policy; 
    /// otherwise <value>false</value>.
    /// </returns>
    /// <remarks>
    /// Resource is an optional parameter and may be null. Please ensure that you check 
    /// it is not null before acting upon it.
    /// </remarks>
    Task<AuthorizationResult> AuthorizeAsync(ClaimsPrincipal user, object resource, 
                                     IEnumerable<IAuthorizationRequirement> requirements);

    /// <summary>
    /// Checks if a user meets a specific authorization policy
    /// </summary>
    /// <param name="user">The user to check the policy against.</param>
    /// <param name="resource">
    /// An optional resource the policy should be checked with.
    /// If a resource is not required for policy evaluation you may pass null as the value
    /// </param>
    /// <param name="policyName">The name of the policy to check against a specific 
    /// context.</param>
    /// <returns>
    /// A flag indicating whether authorization has succeeded.
    /// Returns a flag indicating whether the user, and optional resource has fulfilled 
    /// the policy.    
    /// <value>true</value> when the policy has been fulfilled; 
    /// otherwise <value>false</value>.
    /// </returns>
    /// <remarks>
    /// Resource is an optional parameter and may be null. Please ensure that you check
    /// it is not null before acting upon it.
    /// </remarks>
    Task<AuthorizationResult> AuthorizeAsync(
                                ClaimsPrincipal user, object resource, string policyName);
}
##### IAuthorizationHandlers check if requirements are met:
/// <summary>
/// Classes implementing this interface are able to make a decision if authorization
/// is allowed.
/// </summary>
public interface IAuthorizationHandler
{
    /// <summary>
    /// Makes a decision if authorization is allowed.
    /// </summary>
    /// <param name="context">The authorization information.</param>
    Task HandleAsync(AuthorizationHandlerContext context);
}
##### Simplified default implementation of authorization service:
public async Task<AuthorizationResult> AuthorizeAsync(ClaimsPrincipal user, 
             object resource, IEnumerable<IAuthorizationRequirement> requirements)
{
    // Create a tracking context from the authorization inputs.
    var authContext = _contextFactory.CreateContext(requirements, user, resource);

    // By default this returns an IEnumerable<IAuthorizationHandlers> from DI.
    var handlers = await _handlers.GetHandlersAsync(authContext);

    // Invoke all handlers.
    foreach (var handler in handlers)
    {
        await handler.HandleAsync(authContext);
    }

    // Check the context, by default success is when all requirements have been met.
    return _evaluator.Evaluate(authContext);
}

### Apply policies to MVC controllers

##### Use [Authorize] with policy names:
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc;

[Authorize(Policy = "AtLeast21")]
public class AlcoholPurchaseController : Controller
{
    public IActionResult Index() => View();
}

##### How to do it with Razor Pages:
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc.RazorPages;

[Authorize(Policy = "AtLeast21")]
public class AlcoholPurchaseModel : PageModel
{
}


### Custom Authorization Policy Providers using IAuthorizationPolicyProvider in ASP.NET Core

##### Examples of scenarios where a custom IAuthorizationPolicyProvider may be useful include:
###### Using an external service to provide policy evaluation.
###### Using a large range of policies (for different room numbers or ages, for example), so it doesn't make sense to add each individual authorization policy with an AuthorizationOptions.AddPolicy call.
###### Creating policies at runtime based on information in an external data source (like a database) or determining authorization requirements dynamically through another mechanism.

##### The IAuthorizationPolicyProvider interface contains three APIs:
###### GetPolicyAsync returns an authorization policy for a given name.
###### GetDefaultPolicyAsync returns the default authorization policy (the policy used for [Authorize] attributes without a policy specified).
###### GetFallbackPolicyAsync returns the fallback authorization policy (the policy used by the Authorization Middleware when no policy is specified).

##### Custom Authorization Attributes example:
internal class MinimumAgeAuthorizeAttribute : AuthorizeAttribute
{
    const string POLICY_PREFIX = "MinimumAge";

    public MinimumAgeAuthorizeAttribute(int age) => Age = age;

    // Get or set the Age property by manipulating the underlying Policy property
    public int Age
    {
        get
        {
            if (int.TryParse(Policy.Substring(POLICY_PREFIX.Length), out var age))
            {
                return age;
            }
            return default(int);
        }
        set
        {
            Policy = $"{POLICY_PREFIX}{value.ToString()}";
        }
    }
}
