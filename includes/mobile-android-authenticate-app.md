
1. <span data-ttu-id="40815-101">Otwórz projekt w programie Android Studio.</span><span class="sxs-lookup"><span data-stu-id="40815-101">Open the project in Android Studio.</span></span>

2. <span data-ttu-id="40815-102">W **Eksplorator projektów** w programie Android Studio Otwórz plik ToDoActivity.java i dodaj następujące instrukcje importu:</span><span class="sxs-lookup"><span data-stu-id="40815-102">In **Project Explorer** in Android Studio, open the ToDoActivity.java file and add the following import statements:</span></span>

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. <span data-ttu-id="40815-103">Dodaj następującą metodę do **ToDoActivity** klasy:</span><span class="sxs-lookup"><span data-stu-id="40815-103">Add the following method to the **ToDoActivity** class:</span></span>

        // You can choose any unique number here to differentiate auth providers from each other. Note this is the same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using the Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check the request code matches the one we send in the login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check the error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    <span data-ttu-id="40815-104">Ten kod tworzy metodę, aby obsługiwać ten proces uwierzytelniania Google.</span><span class="sxs-lookup"><span data-stu-id="40815-104">This code creates a method to handle the Google authentication process.</span></span> <span data-ttu-id="40815-105">Okno dialogowe wyświetla identyfikator uwierzytelnionego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="40815-105">A dialog displays the ID of the authenticated user.</span></span> <span data-ttu-id="40815-106">Można kontynuować tylko na pomyślne uwierzytelnienie.</span><span class="sxs-lookup"><span data-stu-id="40815-106">You can only proceed on a successful authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="40815-107">Jeśli używasz dostawcy tożsamości innych niż Google, zmień wartość przekazana do **logowania** metodę na jedną z następujących wartości: _MicrosoftAccount_, _Facebook_, _Twitter_, lub _windowsazureactivedirectory_.</span><span class="sxs-lookup"><span data-stu-id="40815-107">If you are using an identity provider other than Google, change the value passed to the **login** method to one of the following values: _MicrosoftAccount_, _Facebook_, _Twitter_, or _windowsazureactivedirectory_.</span></span>

4. <span data-ttu-id="40815-108">W **onCreate** metody, Dodaj następujący wiersz kodu po kodzie tworzącym `MobileServiceClient` obiektu.</span><span class="sxs-lookup"><span data-stu-id="40815-108">In the **onCreate** method, add the following line of code after the code that instantiates the `MobileServiceClient` object.</span></span>

        authenticate();

    <span data-ttu-id="40815-109">Tego wywołania spowoduje uruchomienie procesu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="40815-109">This call starts the authentication process.</span></span>

5. <span data-ttu-id="40815-110">Przenieś pozostałych kod po `authenticate();` w **onCreate** nową metodę **createTable** metody:</span><span class="sxs-lookup"><span data-stu-id="40815-110">Move the remaining code after `authenticate();` in the **onCreate** method to a new **createTable** method:</span></span>

        private void createTable() {

            // Get the table instance to use.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter to bind the items with the view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load the items from Azure.
            refreshItemsFromTable();
        }

6. <span data-ttu-id="40815-111">Aby zapewnić przekierowania działa zgodnie z oczekiwaniami, Dodaj poniższy fragment _RedirectUrlActivity_ do _AndroidManifest.xml_:</span><span class="sxs-lookup"><span data-stu-id="40815-111">To ensure redirection works as expected, add the following snippet of _RedirectUrlActivity_ to _AndroidManifest.xml_:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. <span data-ttu-id="40815-112">Dodaj redirectUriScheme do _build.gradle_ aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="40815-112">Add redirectUriScheme to _build.gradle_ of your Android application.</span></span>

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

8. <span data-ttu-id="40815-113">Dodaj com.android.support:customtabs:23.0.1 do zależności w Twojej build.gradle:</span><span class="sxs-lookup"><span data-stu-id="40815-113">Add com.android.support:customtabs:23.0.1 to the dependencies in your build.gradle:</span></span>

      <span data-ttu-id="40815-114">zależności {/ /... "com.android.support:customtabs:23.0.1" Kompiluj}</span><span class="sxs-lookup"><span data-stu-id="40815-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span></span>

9. <span data-ttu-id="40815-115">Z **Uruchom** menu, kliknij przycisk **uruchamianie aplikacji** do Uruchom aplikację i zaloguj się przy użyciu dostawcy tożsamości wybrany.</span><span class="sxs-lookup"><span data-stu-id="40815-115">From the **Run** menu, click **Run app** to start the app and sign in with your chosen identity provider.</span></span>

> [!WARNING]
> <span data-ttu-id="40815-116">Schemat adresu URL wymieniony jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="40815-116">The URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="40815-117">Upewnij się, że wszystkie wystąpienia `{url_scheme_of_you_app}` wielkością liter.</span><span class="sxs-lookup"><span data-stu-id="40815-117">Ensure that all occurrences of `{url_scheme_of_you_app}` use the same case.</span></span>

<span data-ttu-id="40815-118">Jeśli pomyślnie zalogowano aplikacji powinny być uruchamiane bez błędów, a można wysłać zapytania do usługi zaplecza i aktualizowanie danych.</span><span class="sxs-lookup"><span data-stu-id="40815-118">When you are successfully signed in, the app should run without errors, and you should be able to query the back-end service and make updates to data.</span></span>
