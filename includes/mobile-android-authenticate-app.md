
1. <span data-ttu-id="61f38-101">Witaj Otwórz projekt w programie Android Studio.</span><span class="sxs-lookup"><span data-stu-id="61f38-101">Open hello project in Android Studio.</span></span>

2. <span data-ttu-id="61f38-102">W **Eksplorator projektów** w programie Android Studio Otwórz plik ToDoActivity.java hello i dodaj następujące instrukcje importu hello:</span><span class="sxs-lookup"><span data-stu-id="61f38-102">In **Project Explorer** in Android Studio, open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. <span data-ttu-id="61f38-103">Dodaj następujące metody toohello hello **ToDoActivity** klasy:</span><span class="sxs-lookup"><span data-stu-id="61f38-103">Add hello following method toohello **ToDoActivity** class:</span></span>

        // You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using hello Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check hello request code matches hello one we send in hello login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check hello error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    <span data-ttu-id="61f38-104">Ten kod tworzy metody toohandle hello proces uwierzytelniania Google.</span><span class="sxs-lookup"><span data-stu-id="61f38-104">This code creates a method toohandle hello Google authentication process.</span></span> <span data-ttu-id="61f38-105">Okno dialogowe wyświetla identyfikator hello hello uwierzytelnianego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="61f38-105">A dialog displays hello ID of hello authenticated user.</span></span> <span data-ttu-id="61f38-106">Można kontynuować tylko na pomyślne uwierzytelnienie.</span><span class="sxs-lookup"><span data-stu-id="61f38-106">You can only proceed on a successful authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="61f38-107">Jeśli używasz dostawcy tożsamości innych niż Google, zmień wartość hello przekazany toohello **logowania** tooone metody z hello następujące wartości: _MicrosoftAccount_, _Facebook_, _Twitter_, lub _windowsazureactivedirectory_.</span><span class="sxs-lookup"><span data-stu-id="61f38-107">If you are using an identity provider other than Google, change hello value passed toohello **login** method tooone of hello following values: _MicrosoftAccount_, _Facebook_, _Twitter_, or _windowsazureactivedirectory_.</span></span>

4. <span data-ttu-id="61f38-108">W hello **onCreate** metody, Dodaj powitania po wierszu kodu po kodzie hello, tworzącym hello `MobileServiceClient` obiektu.</span><span class="sxs-lookup"><span data-stu-id="61f38-108">In hello **onCreate** method, add hello following line of code after hello code that instantiates hello `MobileServiceClient` object.</span></span>

        authenticate();

    <span data-ttu-id="61f38-109">To wywołanie uruchamia proces uwierzytelniania hello.</span><span class="sxs-lookup"><span data-stu-id="61f38-109">This call starts hello authentication process.</span></span>

5. <span data-ttu-id="61f38-110">Przenieś hello pozostałych kod po `authenticate();` w hello **onCreate** nowe tooa — metoda **createTable** metody:</span><span class="sxs-lookup"><span data-stu-id="61f38-110">Move hello remaining code after `authenticate();` in hello **onCreate** method tooa new **createTable** method:</span></span>

        private void createTable() {

            // Get hello table instance toouse.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter toobind hello items with hello view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load hello items from Azure.
            refreshItemsFromTable();
        }

6. <span data-ttu-id="61f38-111">tooensure przekierowania działa zgodnie z oczekiwaniami, Dodaj powitania po fragment _RedirectUrlActivity_ too_AndroidManifest.xml_:</span><span class="sxs-lookup"><span data-stu-id="61f38-111">tooensure redirection works as expected, add hello following snippet of _RedirectUrlActivity_ too_AndroidManifest.xml_:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. <span data-ttu-id="61f38-112">Dodaj too_build.gradle_ redirectUriScheme aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="61f38-112">Add redirectUriScheme too_build.gradle_ of your Android application.</span></span>

        android {
            buildTypes {
                release {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
                debug {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
            }
        }

8. <span data-ttu-id="61f38-113">Dodaj zależności toohello com.android.support:customtabs:23.0.1 Twojego build.gradle:</span><span class="sxs-lookup"><span data-stu-id="61f38-113">Add com.android.support:customtabs:23.0.1 toohello dependencies in your build.gradle:</span></span>

      <span data-ttu-id="61f38-114">zależności {/ /... "com.android.support:customtabs:23.0.1" Kompiluj}</span><span class="sxs-lookup"><span data-stu-id="61f38-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span></span>

9. <span data-ttu-id="61f38-115">Z hello **Uruchom** menu, kliknij przycisk **uruchamianie aplikacji** toostart hello aplikacji i zaloguj się przy użyciu dostawcy tożsamości wybrany.</span><span class="sxs-lookup"><span data-stu-id="61f38-115">From hello **Run** menu, click **Run app** toostart hello app and sign in with your chosen identity provider.</span></span>

> [!WARNING]
> <span data-ttu-id="61f38-116">Schemat adresów URL wymienionych Hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="61f38-116">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="61f38-117">Upewnij się, że wszystkie wystąpienia `{url_scheme_of_you_app}` Użyj hello sam case.</span><span class="sxs-lookup"><span data-stu-id="61f38-117">Ensure that all occurrences of `{url_scheme_of_you_app}` use hello same case.</span></span>

<span data-ttu-id="61f38-118">Jeśli pomyślnie zalogowano aplikacji hello powinny być uruchamiane bez błędów, a powinny być możliwe tooquery hello zaplecza usługi i wprowadzić toodata aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="61f38-118">When you are successfully signed in, hello app should run without errors, and you should be able tooquery hello back-end service and make updates toodata.</span></span>
