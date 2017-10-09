
1. W pliku projektu hello MainPage.xaml.cs Dodaj hello **przy użyciu** instrukcji:
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. Zastąp hello **metody AuthenticateAsync** metody z hello następującego kodu:
   
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
   
    W tej wersji programu **metody AuthenticateAsync**, aplikacja hello próbuje toouse poświadczeń przechowywanych w hello **PasswordVault** tooaccess hello usługi. Regularne logowanie również jest wykonywane, gdy nie istnieje żadne przechowywanych poświadczeń.
   
   > [!NOTE]
   > Buforowany token wygasł, a po uwierzytelnieniu wygaśnięcia tokenu może również wystąpić, gdy aplikacja hello jest używany. toolearn toodetermine Jeśli token jest ważność, zobacz temat [Sprawdź, czy tokeny uwierzytelniania wygasła](http://aka.ms/jww5vp). Błędy autoryzacji toohandling rozwiązania pokrewne tooexpiring tokenów, zobacz hello post [buforowania i obsługa wygaśnięcia tokenów w usłudze Azure Mobile Services zarządzane SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx). 
   > 
   > 
3. Ponowne uruchomienie aplikacji hello dwa razy.
   
    Należy zauważyć, że na powitania pierwszego rozruchu, zarejestruj się przy użyciu dostawcy hello ponownie jest wymagana. Jednak po ponownym uruchomieniu drugiego hello hello buforowane poświadczenia są używane i logowania jest pomijane. 

