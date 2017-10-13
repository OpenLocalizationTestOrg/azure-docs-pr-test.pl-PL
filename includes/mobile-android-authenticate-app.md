
1. Otwórz projekt w programie Android Studio.

2. W **Eksplorator projektów** w programie Android Studio Otwórz plik ToDoActivity.java i dodaj następujące instrukcje importu:

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. Dodaj następującą metodę do **ToDoActivity** klasy:

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

    Ten kod tworzy metodę, aby obsługiwać ten proces uwierzytelniania Google. Okno dialogowe wyświetla identyfikator uwierzytelnionego użytkownika. Można kontynuować tylko na pomyślne uwierzytelnienie.

    > [!NOTE]
    > Jeśli używasz dostawcy tożsamości innych niż Google, zmień wartość przekazana do **logowania** metodę na jedną z następujących wartości: _MicrosoftAccount_, _Facebook_, _Twitter_, lub _windowsazureactivedirectory_.

4. W **onCreate** metody, Dodaj następujący wiersz kodu po kodzie tworzącym `MobileServiceClient` obiektu.

        authenticate();

    Tego wywołania spowoduje uruchomienie procesu uwierzytelniania.

5. Przenieś pozostałych kod po `authenticate();` w **onCreate** nową metodę **createTable** metody:

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

6. Aby zapewnić przekierowania działa zgodnie z oczekiwaniami, Dodaj poniższy fragment _RedirectUrlActivity_ do _AndroidManifest.xml_:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. Dodaj redirectUriScheme do _build.gradle_ aplikacji systemu Android.

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

8. Dodaj com.android.support:customtabs:23.0.1 do zależności w Twojej build.gradle:

      zależności {/ /... "com.android.support:customtabs:23.0.1" Kompiluj}

9. Z **Uruchom** menu, kliknij przycisk **uruchamianie aplikacji** do Uruchom aplikację i zaloguj się przy użyciu dostawcy tożsamości wybrany.

> [!WARNING]
> Schemat adresu URL wymieniony jest rozróżniana wielkość liter.  Upewnij się, że wszystkie wystąpienia `{url_scheme_of_you_app}` wielkością liter.

Jeśli pomyślnie zalogowano aplikacji powinny być uruchamiane bez błędów, a można wysłać zapytania do usługi zaplecza i aktualizowanie danych.
