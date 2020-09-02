# Why do we need https?

### Link to articles: https://howhttps.works/why-do-we-need-https/

### DotNet Security Cheat Sheet

##### .Net Framework: Microsoft's principal platform for enterprise development.
##### It's kept up-to-date by Microsoft with the Windows Update service.
##### Individual frameworks can be kept up to date using NuGet. 
##### ASP.NET Web Forms is the original browser-based application development API for the .NET framework, and is still the most common enterprise platform for web application development.

##### Example:
protected override OnInit(EventArgs e) {
    base.OnInit(e);
    ViewStateUserKey = Session.SessionID;
}

##### Further example:
rivate const string AntiXsrfTokenKey = "__AntiXsrfToken";
private const string AntiXsrfUserNameKey = "__AntiXsrfUserName";
private string _antiXsrfTokenValue;
protected void Page_Init(object sender, EventArgs e)
{
    // The code below helps to protect against XSRF attacks
    var requestCookie = Request.Cookies[AntiXsrfTokenKey];
    Guid requestCookieGuidValue;
    if (requestCookie != null && Guid.TryParse(requestCookie.Value, out requestCookieGuidValue))
    {
       // Use the Anti-XSRF token from the cookie
       _antiXsrfTokenValue = requestCookie.Value;
       Page.ViewStateUserKey = _antiXsrfTokenValue;
    }
    else
    {
       // Generate a new Anti-XSRF token and save to the cookie
       _antiXsrfTokenValue = Guid.NewGuid().ToString("N");
       Page.ViewStateUserKey = _antiXsrfTokenValue;
       var responseCookie = new HttpCookie(AntiXsrfTokenKey)
       {
          HttpOnly = true,
          Value = _antiXsrfTokenValue
       };
       if (FormsAuthentication.RequireSSL && Request.IsSecureConnection)
       {
          responseCookie.Secure = true;
       }
       Response.Cookies.Set(responseCookie);
    }
    Page.PreLoad += master_Page_PreLoad;
}
protected void master_Page_PreLoad(object sender, EventArgs e)
{
    if (!IsPostBack)
    {
       // Set Anti-XSRF token
       ViewState[AntiXsrfTokenKey] = Page.ViewStateUserKey;
       ViewState[AntiXsrfUserNameKey] = Context.User.Identity.Name ?? String.Empty;
    }
    else
    {
       // Validate the Anti-XSRF token

if ((string)ViewState[AntiXsrfTokenKey] != _antiXsrfTokenValue ||
          (string)ViewState[AntiXsrfUserNameKey] != (Context.User.Identity.Name ?? String.Empty))
       {
          throw new InvalidOperationException("Validation of Anti-XSRF token failed.");
       }
    }
}

### OWASP Top 10 for ASP.net Core – Broken Authentication and Session Management

##### All passwords stored in a database should be hashed and have an individual salt 

##### Out of the box you are going to have secure password hashes and an individual salt used.

##### Salting is the act of adding a random string of text to your password before hashing it.

##### Link for more info: https://dotnetcoretutorials.com/2017/10/16/owasp-top-10-asp-net-core-broken-authentication-session-management/

### Link to Safeguard individual privacy with cloud services from Microsoft: https://www.microsoft.com/en-us/trust-center/privacy/gdpr-overview?&OCID=AID641639_SEM_CBaJdkAr&msclkid=69e6e33dba521b93d7d9b9c7e8f92223
