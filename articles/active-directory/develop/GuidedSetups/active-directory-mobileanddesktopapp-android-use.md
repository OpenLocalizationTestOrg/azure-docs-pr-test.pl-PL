---
title: "aaaAzure AD w wersji 2 dla systemu Android wprowadzenie - Użyj | Dokumentacja firmy Microsoft"
description: "Jak uzyskać token dostępu i wywołania interfejsu API programu Microsoft Graph lub interfejsów API, które wymagają tokenów dostępu z punktu końcowego w wersji 2 usługi Azure Active Directory aplikacji systemu Android"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 4480d89eb7638fe7d588c8cebd2b1e3c9d4c6e3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Użyj hello biblioteki uwierzytelniania firmy Microsoft (MSAL) tooget token dla hello interfejsu API programu Microsoft Graph

1.  Otwórz: `MainActivity` (w obszarze `app`  >  `java`  >  `{domain}.{appname}`)
2.  Dodaj hello importuje następujące:

```java
import android.app.Activity;
import android.content.Intent;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;
import com.android.volley.*;
import com.android.volley.toolbox.JsonObjectRequest;
import com.android.volley.toolbox.Volley;
import org.json.JSONObject;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import com.microsoft.identity.client.*;
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
Zastąp hello `MainActivity` klasy z poniżej:
</li>
</ol>

```java
public class MainActivity extends AppCompatActivity {

    final static String CLIENT_ID = "[Enter hello application Id here]";
    final static String SCOPES [] = {"https://graph.microsoft.com/User.Read"};
    final static String MSGRAPH_URL = "https://graph.microsoft.com/v1.0/me";

    /* UI & Debugging Variables */
    private static final String TAG = MainActivity.class.getSimpleName();
    Button callGraphButton;
    Button signOutButton;

    /* Azure AD Variables */
    private PublicClientApplication sampleApp;
    private AuthenticationResult authResult;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        callGraphButton = (Button) findViewById(R.id.callGraph);
        signOutButton = (Button) findViewById(R.id.clearCache);

        callGraphButton.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                onCallGraphClicked();
            }
        });

        signOutButton.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                onSignOutClicked();
            }
        });

  /* Configure your sample app and save state for this activity */
        sampleApp = null;
        if (sampleApp == null) {
            sampleApp = new PublicClientApplication(
                    this.getApplicationContext(),
                    CLIENT_ID);
        }

  /* Attempt tooget a user and acquireTokenSilent
   * If this fails we do an interactive request
   */
        List<User> users = null;

        try {
            users = sampleApp.getUsers();

            if (users != null && users.size() == 1) {
          /* We have 1 user */

                sampleApp.acquireTokenSilentAsync(SCOPES, users.get(0), getAuthSilentCallback());
            } else {
          /* We have no user */

          /* Let's do an interactive request */
                sampleApp.acquireToken(this, SCOPES, getAuthInteractiveCallback());
            }
        } catch (MsalClientException e) {
            Log.d(TAG, "MSAL Exception Generated while getting users: " + e.toString());

        } catch (IndexOutOfBoundsException e) {
            Log.d(TAG, "User at this position does not exist: " + e.toString());
        }

    }

//
// App callbacks for MSAL
// ======================
// getActivity() - returns activity so we can acquireToken within a callback
// getAuthSilentCallback() - callback defined toohandle acquireTokenSilent() case
// getAuthInteractiveCallback() - callback defined toohandle acquireToken() case
//

    public Activity getActivity() {
        return this;
    }

    /* Callback method for acquireTokenSilent calls 
     * Looks if tokens are in hello cache (refreshes if necessary and if we don't forceRefresh)
     * else errors that we need toodo an interactive request.
     */
    private AuthenticationCallback getAuthSilentCallback() {
        return new AuthenticationCallback() {
            @Override
            public void onSuccess(AuthenticationResult authenticationResult) {
            /* Successfully got a token, call Graph now */
                Log.d(TAG, "Successfully authenticated");

            /* Store hello authResult */
                authResult = authenticationResult;

            /* call graph */
                callGraphAPI();

            /* update hello UI toopost call Graph state */
                updateSuccessUI();
            }

            @Override
            public void onError(MsalException exception) {
            /* Failed tooacquireToken */
                Log.d(TAG, "Authentication failed: " + exception.toString());

                if (exception instanceof MsalClientException) {
                /* Exception inside MSAL, more info inside MsalError.java */
                } else if (exception instanceof MsalServiceException) {
                /* Exception when communicating with hello STS, likely config issue */
                } else if (exception instanceof MsalUiRequiredException) {
                /* Tokens expired or no session, retry with interactive */
                }
            }

            @Override
            public void onCancel() {
            /* User canceled hello authentication */
                Log.d(TAG, "User cancelled login.");
            }
        };
    }


    /* Callback used for interactive request.  If succeeds we use hello access
         * token toocall hello Microsoft Graph. Does not check cache
         */
    private AuthenticationCallback getAuthInteractiveCallback() {
        return new AuthenticationCallback() {
            @Override
            public void onSuccess(AuthenticationResult authenticationResult) {
            /* Successfully got a token, call graph now */
                Log.d(TAG, "Successfully authenticated");
                Log.d(TAG, "ID Token: " + authenticationResult.getIdToken());

            /* Store hello auth result */
                authResult = authenticationResult;

            /* call Graph */
                callGraphAPI();

            /* update hello UI toopost call Graph state */
                updateSuccessUI();
            }

            @Override
            public void onError(MsalException exception) {
            /* Failed tooacquireToken */
                Log.d(TAG, "Authentication failed: " + exception.toString());

                if (exception instanceof MsalClientException) {
                /* Exception inside MSAL, more info inside MsalError.java */
                } else if (exception instanceof MsalServiceException) {
                /* Exception when communicating with hello STS, likely config issue */
                }
            }

            @Override
            public void onCancel() {
            /* User canceled hello authentication */
                Log.d(TAG, "User cancelled login.");
            }
        };
    }

    /* Set hello UI for successful token acquisition data */
    private void updateSuccessUI() {
        callGraphButton.setVisibility(View.INVISIBLE);
        signOutButton.setVisibility(View.VISIBLE);
        findViewById(R.id.welcome).setVisibility(View.VISIBLE);
        ((TextView) findViewById(R.id.welcome)).setText("Welcome, " +
                authResult.getUser().getName());
        findViewById(R.id.graphData).setVisibility(View.VISIBLE);
    }

    /* Use MSAL tooacquireToken for hello end-user
     * Callback will call Graph api w/ access token & update UI
     */
    private void onCallGraphClicked() {
        sampleApp.acquireToken(getActivity(), SCOPES, getAuthInteractiveCallback());
    }

    /* Handles hello redirect from hello System Browser */
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        sampleApp.handleInteractiveRequestRedirect(requestCode, resultCode, data);
    }

}
```
<!--start-collapse-->
### <a name="more-information"></a>Więcej informacji
#### <a name="getting-a-user-token-interactive"></a>Pobieranie tokenu użytkownika interakcyjnego
Wywoływanie hello `AcquireTokenAsync` — metoda powoduje monitowanie okna hello toosign użytkownika w. Aplikacje zwykle wymagają toosign użytkownika, w interaktywnie hello muszą tooaccess po raz pierwszy chronionego zasobu lub tooacquire dyskretnej operacji tokenu nie powiedzie się, (np. hasło użytkownika hello ważność).

#### <a name="getting-a-user-token-silently"></a>Pobieranie tokenu użytkownika dyskretnej
`AcquireTokenSilentAsync`obsługuje przejęć tokenu i wznowienie bez interakcji użytkownika. Po `AcquireTokenAsync` jest wykonywana na powitania po raz pierwszy, `AcquireTokenSilentAsync` hello metody najczęściej używanych tooobtain tokenów tooaccess chronionych zasobów w kolejnych wywołaniach — jako toorequest wywołania lub odnowić tokeny są wprowadzane w trybie dyskretnym.
Po pewnym czasie `AcquireTokenSilentAsync` zakończy się niepowodzeniem — np. użytkownika hello zalogował lub została zmieniona hasła na innym urządzeniu. Gdy MSAL wykryje, że hello problem można rozwiązać, gdyż akcję interaktywne, jego generowane `MsalUiRequiredException`. Aplikacja może obsłużyć tego wyjątku na dwa sposoby:

1.  Nawiązywanie połączeń z `AcquireTokenAsync` natychmiast, która powoduje monitowanie użytkownika hello toosign w. Ten wzorzec jest zazwyczaj używany w aplikacji online w przypadku, gdy nie żadnej zawartości w trybie offline w aplikacji hello dostępnej dla użytkownika hello. Hello próbki wygenerowane za pomocą tego Instalatora z przewodnikiem używa tego wzorca: Zobacz go w akcji powitania po raz pierwszy wykonać próbki hello: ponieważ żaden użytkownik nigdy używana aplikacja hello `PublicClientApp.Users.FirstOrDefault` będzie zawierać wartości null i `MsalUiRequiredException` zostanie wygenerowany wyjątek. Witaj kodu w przykładowym hello, a następnie uchwytów hello wyjątku przez wywołanie metody `AcquireTokenAsync` powodujące monitowania użytkownika hello toosign w.
2.  Aplikacje można również ustawić oznaczenia wizualne użytkownik toohello interakcyjne logowanie jest wymagany, dlatego hello użytkownik może wybrać toosign odpowiednich momentach hello w lub ponowić aplikacji hello `AcquireTokenSilentAsync` w późniejszym czasie. Jest ona powszechnie stosowana, gdy użytkownik hello jest stanie tooaccess funkcjonalność aplikacji hello bez są zakłócone — na przykład Brak dostępnej zawartości w trybie offline w aplikacji hello. W takim przypadku hello użytkownika można określić, gdy mają toosign w tooaccess hello chroniony zasób, lub toorefresh hello przestarzałe informacje lub aplikacji można określić tooretry `AcquireTokenSilentAsync` przywrócenie sieci po są tymczasowo niedostępne.
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Wywołanie interfejsu API programu Microsoft Graph hello przy użyciu tokenu hello, który został uzyskany
1.  Dodaj następujące metody do hello hello `MainActivity` klasy:

```java
/* Use Volley toomake an HTTP request toohello /me endpoint from MS Graph using an access token */
private void callGraphAPI() {
    Log.d(TAG, "Starting volley request toograph");

    /* Make sure we have a token toosend toograph */
    if (authResult.getAccessToken() == null) {return;}

    RequestQueue queue = Volley.newRequestQueue(this);
    JSONObject parameters = new JSONObject();

    try {
        parameters.put("key", "value");
    } catch (Exception e) {
        Log.d(TAG, "Failed tooput parameters: " + e.toString());
    }
    JsonObjectRequest request = new JsonObjectRequest(Request.Method.GET, MSGRAPH_URL,
            parameters,new Response.Listener<JSONObject>() {
        @Override
        public void onResponse(JSONObject response) {
            /* Successfully called graph, process data and send tooUI */
            Log.d(TAG, "Response: " + response.toString());

            updateGraphUI(response);
        }
    }, new Response.ErrorListener() {
        @Override
        public void onErrorResponse(VolleyError error) {
            Log.d(TAG, "Error: " + error.toString());
        }
    }) {
        @Override
        public Map<String, String> getHeaders() throws AuthFailureError {
            Map<String, String> headers = new HashMap<>();
            headers.put("Authorization", "Bearer " + authResult.getAccessToken());
            return headers;
        }
    };

    Log.d(TAG, "Adding HTTP GET tooQueue, Request: " + request.toString());

    request.setRetryPolicy(new DefaultRetryPolicy(
            3000,
            DefaultRetryPolicy.DEFAULT_MAX_RETRIES,
            DefaultRetryPolicy.DEFAULT_BACKOFF_MULT));
    queue.add(request);
}

/* Sets hello Graph response */
private void updateGraphUI(JSONObject graphResponse) {
    TextView graphText = (TextView) findViewById(R.id.graphData);
    graphText.setText(graphResponse.toString());
}
```
<!--start-collapse-->
### <a name="more-information-about-making-a-rest-call-against-a-protected-api"></a>Więcej informacji na temat nawiązywania połączenia przed chronionego interfejsu API REST

W tej przykładowej aplikacji `callGraphAPI` wywołania `getAccessToken` , a następnie tworzy HTTP `GET` żądania dotyczącego zasobu, który wymaga tokenu i zwraca hello zawartości. Ta metoda dodaje token hello nabyte w hello *nagłówek autoryzacji HTTP*. Dla tego przykładu zasób hello jest hello interfejsu API programu Microsoft Graph *mnie* punktu końcowego — Wyświetla informacje o profilu użytkownika hello.
<!--end-collapse-->

## <a name="setup-sign-out"></a>Instalator wylogowania

1.  Dodaj następujące metody do hello hello `MainActivity` klasy:

```java
/* Clears a user's tokens from hello cache.
 * Logically similar too"sign out" but only signs out of this app.
 */
private void onSignOutClicked() {

    /* Attempt tooget a user and remove their cookies from cache */
    List<User> users = null;

    try {
        users = sampleApp.getUsers();

        if (users == null) {
            /* We have no users */

        } else if (users.size() == 1) {
            /* We have 1 user */
            /* Remove from token cache */
            sampleApp.remove(users.get(0));
            updateSignedOutUI();

        }
        else {
            /* We have multiple users */
            for (int i = 0; i < users.size(); i++) {
                sampleApp.remove(users.get(i));
            }
        }

        Toast.makeText(getBaseContext(), "Signed Out!", Toast.LENGTH_SHORT)
                .show();

    } catch (MsalClientException e) {
        Log.d(TAG, "MSAL Exception Generated while getting users: " + e.toString());

    } catch (IndexOutOfBoundsException e) {
        Log.d(TAG, "User at this position does not exist: " + e.toString());
    }
}

/* Set hello UI for signed-out user */
private void updateSignedOutUI() {
    callGraphButton.setVisibility(View.VISIBLE);
    signOutButton.setVisibility(View.INVISIBLE);
    findViewById(R.id.welcome).setVisibility(View.INVISIBLE);
    findViewById(R.id.graphData).setVisibility(View.INVISIBLE);
    ((TextView) findViewById(R.id.graphData)).setText("No Data");
}
```
<!--start-collapse-->
### <a name="more-information"></a>Więcej informacji

`onSignOutClicked`powyżej usuwa hello użytkownika z pamięci podręcznej użytkownika MSAL — to skutecznie informuje o MSAL tooforget hello bieżącego użytkownika, tooacquire przyszłych żądania tokenu tylko powiedzie się, jeśli zawiera ona toobe interaktywnego.
Mimo że aplikacji hello w tym przykładzie obsługuje pojedynczego użytkownika, MSAL obsługuje scenariusze, gdzie wiele kont może być zalogowany na powitania jednocześnie — przykładem jest aplikacja poczty e-mail których użytkownik ma wiele kont.
<!--end-collapse-->
