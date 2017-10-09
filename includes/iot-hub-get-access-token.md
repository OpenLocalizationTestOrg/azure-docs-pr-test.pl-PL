## <a name="obtain-an-azure-resource-manager-token"></a>Uzyskaj token usługi Azure Resource Manager
Usługa Azure Active Directory musi uwierzytelniać wszystkie zadania hello, które należy wykonać na zasobów przy użyciu hello Azure Resource Manager. Witaj przykładzie używa uwierzytelniania hasła można znaleźć inne podejścia [żądań uwierzytelniania usługi Azure Resource Manager][lnk-authenticate-arm].

1. Dodaj hello następującego kodu toohello **Main** metody w pliku Program.cs tooretrieve token z usługi Azure AD przy użyciu identyfikatora aplikacji hello i hasła.
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed tooobtain hello token");
      return;
    }
    ```
2. Utworzyć **element ResourceManagementClient** obiektów, że używa hello token przez dodanie hello kod zakończenia toohello hello **Main** metody:
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. Utwórz lub uzyskać odwołania do hello grupy zasobów, którego używasz:
   
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