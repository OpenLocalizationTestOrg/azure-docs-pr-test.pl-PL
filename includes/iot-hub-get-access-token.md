## <a name="obtain-an-azure-resource-manager-token"></a><span data-ttu-id="bcc3d-101">Uzyskaj token usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bcc3d-101">Obtain an Azure Resource Manager token</span></span>
<span data-ttu-id="bcc3d-102">Usługa Azure Active Directory musi uwierzytelniać wszystkie zadania, które należy wykonać na zasobów przy użyciu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bcc3d-102">Azure Active Directory must authenticate all the tasks that you perform on resources using the Azure Resource Manager.</span></span> <span data-ttu-id="bcc3d-103">Tu przykładzie jest używane uwierzytelnianie hasła, aby inne podejścia, zobacz [żądań uwierzytelniania usługi Azure Resource Manager][lnk-authenticate-arm].</span><span class="sxs-lookup"><span data-stu-id="bcc3d-103">The example shown here uses password authentication, for other approaches see [Authenticating Azure Resource Manager requests][lnk-authenticate-arm].</span></span>

1. <span data-ttu-id="bcc3d-104">Dodaj następujący kod do **Main** metody w pliku Program.cs do pobrania tokenu z usługi Azure AD przy użyciu identyfikatora aplikacji i hasła.</span><span class="sxs-lookup"><span data-stu-id="bcc3d-104">Add the following code to the **Main** method in Program.cs to retrieve a token from Azure AD using the application id and password.</span></span>
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed to obtain the token");
      return;
    }
    ```
2. <span data-ttu-id="bcc3d-105">Utwórz **element ResourceManagementClient** obiekt, który używa tokenu, dodając następujący kod na końcu **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="bcc3d-105">Create a **ResourceManagementClient** object that uses the token by adding the following code to the end of the **Main** method:</span></span>
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. <span data-ttu-id="bcc3d-106">Utwórz lub uzyskać odwołania do grupy zasobów, którego używasz:</span><span class="sxs-lookup"><span data-stu-id="bcc3d-106">Create, or obtain a reference to, the resource group you are using:</span></span>
   
    ```
    var rgResponse = client.ResourceGroups.CreateOrUpdate(rgName,
        new ResourceGroup("East US"));
    if (rgResponse.Properties.ProvisioningState != "Succeeded")
    {
      Console.WriteLine("Problem creating resource group");
      return;
    }
    ```

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx