
1. Witaj Otwórz projekt w programie Android Studio.

2. W **Eksplorator projektów** w programie Android Studio Otwórz plik ToDoActivity.java hello i dodaj następujące instrukcje importu hello:

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. Dodaj następujące metody toohello hello **ToDoActivity** klasy:

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

    Ten kod tworzy metody toohandle hello proces uwierzytelniania Google. Okno dialogowe wyświetla identyfikator hello hello uwierzytelnianego użytkownika. Można kontynuować tylko na pomyślne uwierzytelnienie.

    > [!NOTE]
    > Jeśli używasz dostawcy tożsamości innych niż Google, zmień wartość hello przekazany toohello **logowania** tooone metody z hello następujące wartości: _MicrosoftAccount_, _Facebook_, _Twitter_, lub _windowsazureactivedirectory_.

4. W hello **onCreate** metody, Dodaj powitania po wierszu kodu po kodzie hello, tworzącym hello `MobileServiceClient` obiektu.

        authenticate();

    To wywołanie uruchamia proces uwierzytelniania hello.

5. Przenieś hello pozostałych kod po `authenticate();` w hello **onCreate** nowe tooa — metoda **createTable** metody:

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

6. tooensure przekierowania działa zgodnie z oczekiwaniami, Dodaj powitania po fragment _RedirectUrlActivity_ too_AndroidManifest.xml_:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. Dodaj too_build.gradle_ redirectUriScheme aplikacji systemu Android.

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

8. Dodaj zależności toohello com.android.support:customtabs:23.0.1 Twojego build.gradle:

      zależności {/ /... "com.android.support:customtabs:23.0.1" Kompiluj}

9. Z hello **Uruchom** menu, kliknij przycisk **uruchamianie aplikacji** toostart hello aplikacji i zaloguj się przy użyciu dostawcy tożsamości wybrany.

> [!WARNING]
> Schemat adresów URL wymienionych Hello jest rozróżniana wielkość liter.  Upewnij się, że wszystkie wystąpienia `{url_scheme_of_you_app}` Użyj hello sam case.

Jeśli pomyślnie zalogowano aplikacji hello powinny być uruchamiane bez błędów, a powinny być możliwe tooquery hello zaplecza usługi i wprowadzić toodata aktualizacji.
