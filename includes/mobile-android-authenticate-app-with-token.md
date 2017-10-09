
<span data-ttu-id="fb478-101">Witaj poprzednim przykładzie pokazano standardowe logowania, która wymaga powitania klienta toocontact zarówno hello tożsamości dostawcy i hello Azure usługi zaplecza przy każdym uruchomieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="fb478-101">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello back-end Azure service every time hello app starts.</span></span> <span data-ttu-id="fb478-102">Ta metoda jest nieefektywne i może mieć problemy związane z użycia, jeśli wielu klientów toostart aplikacji jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="fb478-102">This method is inefficient, and you can have usage-related issues if many customers try toostart your app simultaneously.</span></span> <span data-ttu-id="fb478-103">Lepszym rozwiązaniem jest token autoryzacji hello toocache zwrócony przez hello Azure usługi i spróbuj toouse to najpierw przed przy użyciu opartych na dostawcy logowania.</span><span class="sxs-lookup"><span data-stu-id="fb478-103">A better approach is toocache hello authorization token returned by hello Azure service, and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="fb478-104">Może buforować hello token wystawiony przez hello usługi Azure, niezależnie od tego, czy używasz uwierzytelniania zarządzanych przez klienta lub zarządzane usługi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="fb478-104">You can cache hello token issued by hello back-end Azure service regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="fb478-105">W tym samouczku korzysta z zarządzanymi przez usługę uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="fb478-105">This tutorial uses service-managed authentication.</span></span>
>
>

1. <span data-ttu-id="fb478-106">Otwórz plik ToDoActivity.java hello i dodaj następujące instrukcje importu hello:</span><span class="sxs-lookup"><span data-stu-id="fb478-106">Open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. <span data-ttu-id="fb478-107">Dodaj następujące elementy członkowskie toohello hello `ToDoActivity` klasy.</span><span class="sxs-lookup"><span data-stu-id="fb478-107">Add hello following members toohello `ToDoActivity` class.</span></span>

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. <span data-ttu-id="fb478-108">W pliku ToDoActivity.java hello Dodaj powitania po definicji hello `cacheUserToken` metody.</span><span class="sxs-lookup"><span data-stu-id="fb478-108">In hello ToDoActivity.java file, add hello following definition for hello `cacheUserToken` method.</span></span>

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    <span data-ttu-id="fb478-109">Ta metoda hello identyfikator użytkownika i token są przechowywane w pliku preferencji, który jest oznaczony jako prywatny.</span><span class="sxs-lookup"><span data-stu-id="fb478-109">This method stores hello user ID and token in a preference file that is marked private.</span></span> <span data-ttu-id="fb478-110">Należy chronić dostępu toohello w pamięci podręcznej, dzięki czemu inne aplikacje na urządzeniu hello nie ma tokenu toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="fb478-110">This should protect access toohello cache so that other apps on hello device do not have access toohello token.</span></span> <span data-ttu-id="fb478-111">preferencji Hello jest w trybie piaskownicy dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="fb478-111">hello preference is sandboxed for hello app.</span></span> <span data-ttu-id="fb478-112">Jednak jeśli ktoś uzyska dostęp do urządzenia toohello, istnieje możliwość, że może uzyskują dostęp toohello pamięci podręcznej tokenu w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="fb478-112">However, if someone gains access toohello device, it is possible that they may gain access toohello token cache through other means.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fb478-113">Można dodatkowo zabezpieczyć hello token z szyfrowaniem, jeśli dane tooyour token dostępu jest uznawany za bardzo ważne, a ktoś może uzyskać dostępu do urządzenia toohello.</span><span class="sxs-lookup"><span data-stu-id="fb478-113">You can further protect hello token with encryption, if token access tooyour data is considered highly sensitive and someone may gain access toohello device.</span></span> <span data-ttu-id="fb478-114">Całkowicie bezpieczna wykracza poza zakres tego samouczka, hello jednak i zależy od wymagań dotyczących zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="fb478-114">A completely secure solution is beyond hello scope of this tutorial, however, and depends on your security requirements.</span></span>
   >
   >
4. <span data-ttu-id="fb478-115">W pliku ToDoActivity.java hello Dodaj powitania po definicji hello `loadUserTokenCache` metody.</span><span class="sxs-lookup"><span data-stu-id="fb478-115">In hello ToDoActivity.java file, add hello following definition for hello `loadUserTokenCache` method.</span></span>

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
5. <span data-ttu-id="fb478-116">W hello *ToDoActivity.java* pliku, Zastąp hello `authenticate` metody z hello następujące metody, która używa tokenu pamięć podręczną.</span><span class="sxs-lookup"><span data-stu-id="fb478-116">In hello *ToDoActivity.java* file, replace hello `authenticate` method with hello following method, which uses a token cache.</span></span> <span data-ttu-id="fb478-117">Dostawca logowania hello w razie potrzeby zmienić toouse innego konta niż Google.</span><span class="sxs-lookup"><span data-stu-id="fb478-117">Change hello login provider if you want toouse an account other than Google.</span></span>

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
6. <span data-ttu-id="fb478-118">Tworzenie hello aplikacji i test uwierzytelniania przy użyciu prawidłowego konta.</span><span class="sxs-lookup"><span data-stu-id="fb478-118">Build hello app and test authentication using a valid account.</span></span> <span data-ttu-id="fb478-119">Uruchom co najmniej dwa razy.</span><span class="sxs-lookup"><span data-stu-id="fb478-119">Run it at least twice.</span></span> <span data-ttu-id="fb478-120">Podczas pierwszego uruchomienia hello możesz odbierać prompt toosign w i utworzyć hello tokenu pamięć podręczną.</span><span class="sxs-lookup"><span data-stu-id="fb478-120">During hello first run, you should receive a prompt toosign in and create hello token cache.</span></span> <span data-ttu-id="fb478-121">Po każdym uruchomieniu prób tooload hello pamięci podręcznej tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="fb478-121">After that, each run attempts tooload hello token cache for authentication.</span></span> <span data-ttu-id="fb478-122">Nie może być wymagane toosign w.</span><span class="sxs-lookup"><span data-stu-id="fb478-122">You should not be required toosign in.</span></span>
