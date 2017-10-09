
Witaj poprzednim przykładzie pokazano standardowe logowania, która wymaga powitania klienta toocontact zarówno hello tożsamości dostawcy i hello Azure usługi zaplecza przy każdym uruchomieniu aplikacji hello. Ta metoda jest nieefektywne i może mieć problemy związane z użycia, jeśli wielu klientów toostart aplikacji jednocześnie. Lepszym rozwiązaniem jest token autoryzacji hello toocache zwrócony przez hello Azure usługi i spróbuj toouse to najpierw przed przy użyciu opartych na dostawcy logowania.

> [!NOTE]
> Może buforować hello token wystawiony przez hello usługi Azure, niezależnie od tego, czy używasz uwierzytelniania zarządzanych przez klienta lub zarządzane usługi zaplecza. W tym samouczku korzysta z zarządzanymi przez usługę uwierzytelniania.
>
>

1. Otwórz plik ToDoActivity.java hello i dodaj następujące instrukcje importu hello:

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. Dodaj następujące elementy członkowskie toohello hello `ToDoActivity` klasy.

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. W pliku ToDoActivity.java hello Dodaj powitania po definicji hello `cacheUserToken` metody.

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    Ta metoda hello identyfikator użytkownika i token są przechowywane w pliku preferencji, który jest oznaczony jako prywatny. Należy chronić dostępu toohello w pamięci podręcznej, dzięki czemu inne aplikacje na urządzeniu hello nie ma tokenu toohello dostępu. preferencji Hello jest w trybie piaskownicy dla aplikacji hello. Jednak jeśli ktoś uzyska dostęp do urządzenia toohello, istnieje możliwość, że może uzyskują dostęp toohello pamięci podręcznej tokenu w inny sposób.

   > [!NOTE]
   > Można dodatkowo zabezpieczyć hello token z szyfrowaniem, jeśli dane tooyour token dostępu jest uznawany za bardzo ważne, a ktoś może uzyskać dostępu do urządzenia toohello. Całkowicie bezpieczna wykracza poza zakres tego samouczka, hello jednak i zależy od wymagań dotyczących zabezpieczeń.
   >
   >
4. W pliku ToDoActivity.java hello Dodaj powitania po definicji hello `loadUserTokenCache` metody.

        private boolean loadUserTokenCache(MobileServiceClient client)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            String userId = prefs.getString(USERIDPREF, null);
            if (userId == null)
                return false;
            String token = prefs.getString(TOKENPREF, null);
            if (token == null)
                return false;

            MobileServiceUser user = new MobileServiceUser(userId);
            user.setAuthenticationToken(token);
            client.setCurrentUser(user);

            return true;
        }
5. W hello *ToDoActivity.java* pliku, Zastąp hello `authenticate` metody z hello następujące metody, która używa tokenu pamięć podręczną. Dostawca logowania hello w razie potrzeby zmienić toouse innego konta niż Google.

        private void authenticate() {
            // We first try tooload a token cache if one exists.
            if (loadUserTokenCache(mClient))
            {
                createTable();
            }
            // If we failed tooload a token cache, login and create a token cache
            else
            {
                // Login using hello Google provider.    
                ListenableFuture<MobileServiceUser> mLogin = mClient.login(MobileServiceAuthenticationProvider.Google);

                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        createAndShowDialog("You must log in. Login Required", "Error");
                    }           
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        createAndShowDialog(String.format(
                                "You are now logged in - %1$2s",
                                user.getUserId()), "Success");
                        cacheUserToken(mClient.getCurrentUser());
                        createTable();    
                    }
                });
            }
        }
6. Tworzenie hello aplikacji i test uwierzytelniania przy użyciu prawidłowego konta. Uruchom co najmniej dwa razy. Podczas pierwszego uruchomienia hello możesz odbierać prompt toosign w i utworzyć hello tokenu pamięć podręczną. Po każdym uruchomieniu prób tooload hello pamięci podręcznej tokenu uwierzytelniania. Nie może być wymagane toosign w.
