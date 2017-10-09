
1. <span data-ttu-id="e4890-101">W pliku projektu hello MainPage.xaml.cs Dodaj hello **przy użyciu** instrukcji:</span><span class="sxs-lookup"><span data-stu-id="e4890-101">In hello MainPage.xaml.cs project file, add hello following **using** statements:</span></span>
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. <span data-ttu-id="e4890-102">Zastąp hello **metody AuthenticateAsync** metody z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="e4890-102">Replace hello **AuthenticateAsync** method with hello following code:</span></span>
   
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
   
            // This sample uses hello Facebook provider.
            var provider = MobileServiceAuthenticationProvider.Facebook;
   
            // Use hello PasswordVault toosecurely store and access credentials.
            PasswordVault vault = new PasswordVault();
            PasswordCredential credential = null;
   
            try
            {
                // Try tooget an existing credential from hello vault.
                credential = vault.FindAllByResource(provider.ToString()).FirstOrDefault();
            }
            catch (Exception)
            {
                // When there is no matching resource an error occurs, which we ignore.
            }
   
            if (credential != null)
            {
                // Create a user from hello stored credentials.
                user = new MobileServiceUser(credential.UserName);
                credential.RetrievePassword();
                user.MobileServiceAuthenticationToken = credential.Password;
   
                // Set hello user from hello stored credentials.
                App.MobileService.CurrentUser = user;
   
                // Consider adding a check toodetermine if hello token is 
                // expired, as shown in this post: http://aka.ms/jww5vp.
   
                success = true;
                message = string.Format("Cached credentials for user - {0}", user.UserId);
            }
            else
            {
                try
                {
                    // Login with hello identity provider.
                    user = await App.MobileService
                        .LoginAsync(provider);
   
                    // Create and store hello user credentials.
                    credential = new PasswordCredential(provider.ToString(),
                        user.UserId, user.MobileServiceAuthenticationToken);
                    vault.Add(credential);
   
                    success = true;
                    message = string.Format("You are now logged in - {0}", user.UserId);
                }
                catch (MobileServiceInvalidOperationException)
                {
                    message = "You must log in. Login Required";
                }
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
   
            return success;
        }
   
    <span data-ttu-id="e4890-103">W tej wersji programu **metody AuthenticateAsync**, aplikacja hello próbuje toouse poświadczeń przechowywanych w hello **PasswordVault** tooaccess hello usługi.</span><span class="sxs-lookup"><span data-stu-id="e4890-103">In this version of **AuthenticateAsync**, hello app tries toouse credentials stored in hello **PasswordVault** tooaccess hello service.</span></span> <span data-ttu-id="e4890-104">Regularne logowanie również jest wykonywane, gdy nie istnieje żadne przechowywanych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="e4890-104">A regular sign-in is also performed when there is no stored credential.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e4890-105">Buforowany token wygasł, a po uwierzytelnieniu wygaśnięcia tokenu może również wystąpić, gdy aplikacja hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="e4890-105">A cached token may be expired, and token expiration can also occur after authentication when hello app is in use.</span></span> <span data-ttu-id="e4890-106">toolearn toodetermine Jeśli token jest ważność, zobacz temat [Sprawdź, czy tokeny uwierzytelniania wygasła](http://aka.ms/jww5vp).</span><span class="sxs-lookup"><span data-stu-id="e4890-106">toolearn how toodetermine if a token is expired, see [Check for expired authentication tokens](http://aka.ms/jww5vp).</span></span> <span data-ttu-id="e4890-107">Błędy autoryzacji toohandling rozwiązania pokrewne tooexpiring tokenów, zobacz hello post [buforowania i obsługa wygaśnięcia tokenów w usłudze Azure Mobile Services zarządzane SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4890-107">For a solution toohandling authorization errors related tooexpiring tokens, see hello post [Caching and handling expired tokens in Azure Mobile Services managed SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span></span> 
   > 
   > 
3. <span data-ttu-id="e4890-108">Ponowne uruchomienie aplikacji hello dwa razy.</span><span class="sxs-lookup"><span data-stu-id="e4890-108">Restart hello app twice.</span></span>
   
    <span data-ttu-id="e4890-109">Należy zauważyć, że na powitania pierwszego rozruchu, zarejestruj się przy użyciu dostawcy hello ponownie jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="e4890-109">Notice that on hello first start-up, sign-in with hello provider is again required.</span></span> <span data-ttu-id="e4890-110">Jednak po ponownym uruchomieniu drugiego hello hello buforowane poświadczenia są używane i logowania jest pomijane.</span><span class="sxs-lookup"><span data-stu-id="e4890-110">However, on hello second restart hello cached credentials are used and sign-in is bypassed.</span></span> 

