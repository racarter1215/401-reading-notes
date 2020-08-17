# How to Send Email Using SendGrid with Azure

### SendGrid: cloud-based email service that provides reliable transactional email delivery, scalability, and real-time analytics along with flexible APIs

##### Additional SendGrid info: https://sendgrid.com/

##### How to sign up:
##### Sign in to the Azure portal.

##### In the Azure portal menu or the home page, select Create a resource.

##### Search for and select SendGrid.

##### Complete the signup form and select Create.

##### Enter a Name to identify your SendGrid service in your Azure settings. Names must be between 1 and 100 characters in length and contain only alphanumeric characters, dashes, dots, and underscores. The name must be unique in your list of subscribed Azure Store Items.

##### Enter and confirm your Password.

##### Choose your Subscription.

##### Create a new Resource group or use an existing one.

##### In the Pricing tier section select the SendGrid plan you want to sign up for.

##### Enter a Promotion Code if you have one.

##### Enter your Contact Information.

##### Review and accept the Legal terms.

##### After confirming your purchase you will see a Deployment Succeeded pop-up and you will see your account listed.

##### After you have completed your purchase and clicked the Manage button to initiate the email verification process, you will receive an email from SendGrid asking you to verify your account. If you do not receive this email, or have problems verifying your account, please see our FAQ.

##### You can only send up to 100 emails/day until you have verified your account.

##### To modify your subscription plan or see the SendGrid contact settings, click the name of your SendGrid service to open the SendGrid Marketplace dashboard.

##### To send an email using SendGrid, you must supply your API Key.

#####  SendGrid NuGet package is the easiest way to get the SendGrid API and to configure your application with all dependencies. 

##### Example of how to create email:
var msg = new SendGridMessage();

msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

var recipients = new List<EmailAddress>
{
    new EmailAddress("jeff@example.com", "Jeff Smith"),
    new EmailAddress("anna@example.com", "Anna Lidman"),
    new EmailAddress("peter@example.com", "Peter Saddow")
};
msg.AddTos(recipients);

msg.SetSubject("Testing the SendGrid C# Library");

msg.AddContent(MimeType.Text, "Hello World plain text!");
msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

##### Sending email via API example:
using System;
using System.Threading.Tasks;
using SendGrid;
using SendGrid.Helpers.Mail;

namespace Example
{
    internal class Example
    {
        private static void Main()
        {
            Execute().Wait();
        }

        static async Task Execute()
        {
            var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
            var client = new SendGridClient(apiKey);
            var msg = new SendGridMessage()
            {
                From = new EmailAddress("test@example.com", "DX Team"),
                Subject = "Hello World from the SendGrid CSharp SDK!",
                PlainTextContent = "Hello, Email!",
                HtmlContent = "<strong>Hello, Email!</strong>"
            };
            msg.AddTo(new EmailAddress("test@example.com", "Test User"));
            var response = await client.SendEmailAsync(msg);
        }
    }
}

##### Send email using MailHelper example:
{
   "Logging": {
   "IncludeScopes": false,
   "LogLevel": {
   "Default": "Debug",
   "System": "Information",
   "Microsoft": "Information"
     }
   },
 "SENDGRID_API_KEY": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
}

