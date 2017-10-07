---
title: aaaAzure AD Android wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak toobuild aplikacji systemu Android, która integruje się z usługą Azure AD, logowania i wywołania usługi Azure AD chronione interfejsów API przy użyciu uwierzytelniania OAuth."
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a>Integrowanie usługi Azure AD do aplikacji systemu Android
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Spróbuj hello Podgląd nowe [portalu dla deweloperów](https://identity.microsoft.com/Docs/Android), który pomoże Ci rozpocząć pracę z usługą Azure AD w ciągu kilku minut. portalu dla deweloperów Hello przeprowadzi Cię przez proces hello rejestrowanie aplikacji i Integrowanie usługi Azure AD w kodzie. Po zakończeniu będziesz mieć prostą aplikację, która może uwierzytelniać użytkowników w dzierżawie oraz zaplecze, które mogą zaakceptować tokeny i sprawdzania poprawności.
>
>

Jeśli projektujesz aplikacja usługi Azure Active Directory (Azure AD) umożliwia proste i bezpośrednie dla tooauthenticate można użytkowników przy użyciu ich lokalnych kont usługi Active Directory. Umożliwia również toosecurely Twojej aplikacji korzystać z dowolnej sieci web interfejsu API chronione przez usługę Azure AD, takich jak hello interfejsami API usługi Office 365 lub hello interfejsu API Azure.

W przypadku systemu Android klientów, którzy potrzebują tooaccess chronionych zasobów usługi Azure AD zapewnia hello Active Directory Authentication Library (ADAL). jedynym celem ADAL Hello jest toomake go łatwo tooget tokenów dostępu do aplikacji. jak łatwo jest, firma Microsoft będzie tworzenie aplikacji systemu Android listy zadań do wykonania który toodemonstrate:

* Pobiera dostępu tokeny na potrzeby wywoływania API listy zadań do wykonania przy użyciu hello [protokół uwierzytelniania OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Pobiera listę zadań do wykonania przez użytkownika.
* Wylogowuje użytkowników.

tooget uruchomiona, należy dzierżawa usługi Azure AD można tworzyć użytkowników i zarejestrowanie aplikacji. Jeśli nie masz już dzierżawę, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a>Krok 1: Pobierz i uruchom hello TODO interfejsu API REST Node.js przykładowym serwerem
Przykładowe TODO interfejsu API REST Node.js Hello są zapisywane w szczególności toowork względem naszego istniejący przykład tworzenia pojedynczej dzierżawy interfejsu API REST zadań do wykonania dla usługi Azure AD. Jest to wymagane w przypadku hello Szybki Start.

Aby uzyskać informacje dotyczące tooset to, zobacz temat nasze przykłady istniejących w [Microsoft usługi Azure Active Directory próbki REST API for Node.js](active-directory-devquickstarts-webapi-nodejs.md).


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a>Krok 2: Zarejestruj interfejsu API sieci web z dzierżawy usługi Azure AD
Usługa Active Directory obsługuje dodawanie dwa typy aplikacji:

- Interfejsy API, które oferują toousers usług sieci Web
- Aplikacji (z systemem w sieci web hello lub na urządzeniu), które uzyskują dostęp do tych interfejsów API sieci web

W tym kroku jest zarejestrowanie hello interfejsu API sieci web, której używasz lokalnie do testowania w tym przykładzie. Zazwyczaj interfejs API sieci web to usługa REST, która jest funkcja oferty, które mają tooaccess aplikacji. Usługi Azure AD może pomóc chronić dowolnego punktu końcowego.

Zakłada się, że w przypadku rejestrowania hello interfejsu API REST TODO odwołuje się do wcześniej. Ale działa to w przypadku dowolnego interfejsu API sieci web interesujące toohelp ochrony usługi Azure Active Directory.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Na górnym pasku powitania kliknij swoje konto. W hello **katalogu** wybierz dzierżawy usługi Azure AD hello miejscu tooregister aplikacji.
3. Kliknij przycisk **więcej usług** w lewym okienku hello, a następnie wybierz **usługi Azure Active Directory**.
4. Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.
5. Wprowadź przyjazną nazwę dla aplikacji hello (na przykład **TodoListService**), wybierz pozycję **aplikacji sieci Web i/lub interfejs API sieci Web**i kliknij przycisk **dalej**.
6. Dla przykładu hello hello logowania jednokrotnego adresu URL, wprowadź hello podstawowego adresu URL. Domyślnie jest to `https://localhost:8080`.
7. Kliknij przycisk **OK** toocomplete hello rejestracji.
8. Nadal w hello portalu Azure, przejdź do strony aplikacji tooyour, Znajdź wartość Identyfikatora aplikacji hello i skopiuj go. Należy to później podczas konfigurowania aplikacji.
9. Z hello **ustawienia** -> **właściwości** strony, aktualizacja aplikacji hello identyfikator URI — wprowadź `https://<your_tenant_name>/TodoListService`. Zastąp `<your_tenant_name>` o nazwie hello dzierżawy usługi Azure AD.

## <a name="step-3-register-hello-sample-android-native-client-application"></a>Krok 3: Zarejestruj hello przykładowej aplikacji systemu Android Native Client
W tym przykładzie należy zarejestrować aplikacji sieci web. Dzięki temu toocommunicate Twojej aplikacji z hello zarejestrowana tylko interfejs API sieci web. Usługi Azure AD będą odrzucać tooeven Zezwalaj tooask Twojej aplikacji do logowania, o ile jest on zarejestrowany. Który jest częścią zabezpieczeń hello hello modelu.

Zakłada się, że w przypadku rejestrowania hello Przykładowa aplikacja odwołuje się do wcześniej. Jednak ta procedura działa w przypadku dowolnej aplikacji, która projektujesz.

> [!NOTE]
> Może zastanawiasz się, dlaczego chcesz umieścić zarówno aplikacji, jak i interfejs API sieci web w jednej dzierżawy. Ponieważ użytkownik może mieć odgadnąć, można utworzyć aplikację, która uzyskuje dostęp do zewnętrznego interfejsu API, który jest zarejestrowany w usłudze Azure AD z innego dzierżawcę. Jeśli możesz to zrobić, klienci będą tooconsent toohello stosowania hello interfejsu API w aplikacji hello monit. Biblioteki uwierzytelniania usługi Active Directory dla systemu iOS zapewnia obsługę tej zgody. Jak możemy zapoznać się z bardziej zaawansowane funkcje, zobaczysz, że jest ważnym elementem hello pracy wymagane tooaccess hello zestawu Microsoft APIs z platformy Azure i pakietu Office, a także innych dostawcy usług. Teraz, ponieważ w zarejestrowany zarówno interfejs API sieci web i aplikacji w obszarze hello sam dzierżawy, nie będą widzieć żadnych monitów o zgodę. Dotyczy to zazwyczaj hello specjalnie dla własnego toouse firmy w przypadku tworzenia aplikacji.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Na górnym pasku powitania kliknij swoje konto. W hello **katalogu** wybierz dzierżawy usługi Azure AD hello miejscu tooregister aplikacji.
3. Kliknij przycisk **więcej usług** w lewym okienku hello, a następnie wybierz **usługi Azure Active Directory**.
4. Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.
5. Wprowadź przyjazną nazwę dla aplikacji hello (na przykład **TodoListClient Android**), wybierz pozycję **natywną aplikację kliencką**i kliknij przycisk **dalej**.
6. Identyfikator URI przekierowania dla hello, wprowadź `http://TodoListClient`. Kliknij przycisk **Zakończ**.
7. Ze strony aplikacji hello Znajdź wartość Identyfikatora aplikacji hello i skopiuj go. Należy to później podczas konfigurowania aplikacji.
8. Z hello **ustawienia** wybierz pozycję **wymagane uprawnienia** i wybierz **Dodaj**.  Zlokalizuj i wybierz TodoListService, dodać hello **TodoListService dostępu** uprawnienie w obszarze **delegowane uprawnienia**i kliknij przycisk **gotowe**.

toobuild z Maven, można użyć pom.xml na najwyższym poziomie hello:

1. Klonuj to repozytorium w wybranym katalogu:

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. Wykonaj kroki hello hello [wymagania wstępne tooset Twojego środowiska Maven dla systemu Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).
3. Konfigurowanie emulatora hello z 19 zestawu SDK.
4. Przejdź toohello folderu głównego, gdzie sklonować repozytorium hello.
5. Uruchom następujące polecenie:`mvn clean install`
6. Zmień hello katalogu toohello Szybki Start próbki:`cd samples\hello`
7. Uruchom następujące polecenie:`mvn android:deploy android:run`

   Powinny pojawić się uruchamianie aplikacji hello.
8. Wprowadź tootry poświadczenia użytkownika testowego.

Pakiety JAR zostaną przesłane obok hello AAR pakietu.

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a>Krok 4: Pobierz hello ADAL dla systemu Android i dodać go tooyour Eclipse roboczym
Wprowadziliśmy go łatwo możesz toohave wiele opcji toouse ADAL w projekcie systemu Android:

* Tooimport kod źródłowy hello można użyć tej biblioteki do aplikacji tooyour Eclipse i łącza.
* Jeśli używasz programu Android Studio, używając hello AAR pakietu format i odwołanie hello plików binarnych.

### <a name="option-1-source-zip"></a>Opcja 1: Źródło Zip
toodownload kopię hello źródła kodu, kliknij przycisk **Pobierz ZIP** po prawej stronie powitania hello strony. Można także [pobrać z witryny GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).

### <a name="option-2-source-via-git"></a>Opcja 2: Źródło za pomocą narzędzia Git
Kod źródłowy hello tooget hello zestawu SDK przez Git, wpisz:

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a>Opcja 3: Pliki binarne, za pomocą narzędzia Gradle
Pliki binarne hello możesz pobrać ze strony hello Maven centralnym repozytorium. Pakiet AAR Hello mogą zostać włączone w następujący sposób w projekcie w programie Android Studio:

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a>Opcja 4: AAR za pomocą narzędzia Maven
Jeśli używasz hello M2Eclipse wtyczki, można określić zależności hello w pliku pom.xml:

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a>Opcja 5: JAR pakietu znajduje się w folderze libs hello
Możesz pobrać plik JAR hello z repozytorium Maven hello i upuść ją na powitania **biblioteki** folder w projekcie. Toocopy hello wymaganych zasobów tooyour projektu również jest potrzebna, ponieważ pakiety JAR hello nie zawierają je.

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a>Krok 5: Dodawanie odwołań tooAndroid ADAL tooyour projektu
1. Dodaj odwołanie do projektu tooyour i określ go jako biblioteka systemu Android. Jeśli nie jesteś pewien sposób toodo, można uzyskać więcej informacji na temat hello [lokacji Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).
2. Dodaj hello zależności projektu do debugowania do ustawień projektu.
3. Aktualizacja tooinclude pliku AndroidManifest.xml projektu:

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. Utwórz wystąpienie kontekst AuthenticationContext na Twoje działania głównego. Hello szczegóły tego wywołania wykraczają poza zakres tego tematu hello, ale można uzyskać dobry początek, analizując hello [próbki Android Native Client](https://github.com/AzureADSamples/NativeClient-Android). Poniższy przykład hello, SharedPreferences jest hello domyślne w pamięci podręcznej i urząd jest w formie hello `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. Skopiuj ten kod bloku toohandle hello koniec AuthenticationActivity po hello użytkownik wprowadza poświadczenia i odbiera kod autoryzacji:

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. tooask dla tokenu, zdefiniuj wywołanie zwrotne:

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. Na koniec uzyskać tokenu przy użyciu wywołanie zwrotne:

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

Oto objaśnienie parametrów hello:

* *zasób* jest wymagany i jest zasobem hello próbujesz tooaccess.
* *ClientID* jest wymagany i pochodzi z usługi Azure AD.
* *RedirectUri* nie jest wymagane toobe podany dla wywołania acquireToken hello. Można skonfigurować go jako nazwę pakietu.
* *PromptBehavior* pomaga tooask poświadczenia tooskip hello w pamięci podręcznej i plików cookie.
* *Wywołanie zwrotne* jest wywoływana po kod autoryzacji hello są wymieniane dla tokenu. Ma ona obiektu AuthenticationResult, który ma token dostępu, Data wygasła i identyfikator informacji o tokenie.
* *acquireTokenSilent* jest opcjonalna. Można go wywołać toohandle buforowanie i odświeżanie tokenu. Umożliwia także hello wersję usługi synchronizacji. Akceptuje *userId* jako parametr.

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

Przy użyciu tego przewodnika, powinien mieć, jakie muszą toosuccessfully integracji z usługą Azure Active Directory. Więcej przykładów dotyczących tej pracy, odwiedź stronę hello AzureADSamples / repozytorium w witrynie GitHub.

## <a name="important-information"></a>Ważne informacje
### <a name="customization"></a>Dostosowywanie
Zasoby aplikacji można zastąpić zasoby biblioteki projektu. Dzieje się tak, gdy aplikacja została skompilowana. Z tego powodu można dostosować uwierzytelniania działania układu hello sposób. Należy się, że identyfikator kontrolki hello hello tookeep tej biblioteki ADAL używa (WebView).

### <a name="broker"></a>Broker
aplikacji Portal firmy usługi Intune Microsoft Hello zawiera składnik brokera hello. Witaj, konto jest tworzone w elementu AccountManager. Typ konta Hello jest "com.microsoft.workaccount." Elementu AccountManager umożliwia tylko jedno konto logowania jednokrotnego. Tworzy plik cookie logowania jednokrotnego dla użytkownika powitania po zakończeniu hello urządzenia wyzwanie dla jednej z aplikacji hello.

ADAL używa konta brokera hello, jeśli jedno konto użytkownika jest tworzona w tym uwierzytelniania i użytkownik wybierze nie tooskip go. Można pominąć hello brokera użytkownikowi:

   `AuthenticationSettings.Instance.setSkipBroker(true);`

Należy tooregister specjalne RedirectUri użycia brokera. RedirectUri jest w formacie hello `msauth://packagename/Base64UrlencodedSignature`. Twoje RedirectUri dla aplikacji można uzyskać za pomocą brokerRedirectPrint.ps1 skryptu hello lub mContext.getBrokerRedirectUri wywołania interfejsu API hello. Podpis Hello jest powiązane tooyour certyfikaty podpisywania.

bieżący model brokera Hello jest jeden użytkownik. Element AuthenticationContext zawiera hello interfejsu API metody tooget hello brokera użytkownika.

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

Manifest aplikacji powinien mieć następujące uprawnienia toouse elementu AccountManager kont hello. Aby uzyskać więcej informacji, zobacz hello [elementu AccountManager informacji na temat witryny systemu Android hello](http://developer.android.com/reference/android/accounts/AccountManager.html).

* GET_ACCOUNTS
* USE_CREDENTIALS
* MANAGE_ACCOUNTS

### <a name="authority-url-and-ad-fs"></a>Adres URL urzędu i usługami AD FS
Active Directory Federation Services (AD FS) nie został rozpoznany jako produkcji STS, więc należy tooturn odnajdywania instancji i przekazać wartość false w hello kontekst AuthenticationContext konstruktora.

adres URL urzędu Hello wymaga wystąpienia usługi STS i [nazwa dzierżawcy](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).

### <a name="querying-cache-items"></a>Wykonywanie zapytania o elementy pamięci podręcznej
Biblioteka ADAL udostępnia pamięć podręczną domyślne w SharedPreferences z niektórych prostych pamięci podręcznej funkcje zapytań. Możesz uzyskać hello bieżącej pamięci podręcznej z kontekst AuthenticationContext przy użyciu:

    ITokenCacheStore cache = mContext.getCache();

Można też podać implementacji pamięci podręcznej, jeśli chcesz, aby toocustomize go.

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a>Zachowanie monitu
Biblioteka ADAL zapewnia zachowanie monitu toospecify opcji. PromptBehavior.Auto wyświetli hello interfejsu użytkownika, jeśli token odświeżania hello jest nieprawidłowy i wymagane są poświadczenia użytkownika. PromptBehavior.Always pominie hello użycia pamięci podręcznej i zawsze pokazuj hello interfejsu użytkownika.

### <a name="silent-token-request-from-cache-and-refresh"></a>Dyskretnej żądania tokenu z pamięci podręcznej i Odśwież
Dyskretnej żądania tokenu nie używa hello podręcznym interfejsu użytkownika i nie wymaga działania. Zwraca token z hello pamięci podręcznej, jeśli jest dostępna. Jeśli hello token wygasł, ta metoda próbuje toorefresh go. Jeśli token odświeżania hello wygasł lub nie powiodło się, zwraca authenticationexception —.

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

Można również przeprowadzać synchronizacji wywołać za pomocą tej metody. Można ustawić wartości null toocallback lub użyć acquireTokenSilentSync.

### <a name="diagnostics"></a>Diagnostyka
Są to hello podstawowego źródła informacji do diagnozowania problemów:

* Wyjątki
* Dzienniki
* Śledzenie sieci

Należy zauważyć, że identyfikatorów korelacji centralnej toohello diagnostyki w bibliotece hello. Jeśli chcesz, aby toocorrelate ADAL żądania z innymi operacjami w kodzie można ustawić z identyfikatorów korelacji na podstawie danego żądania. Jeśli identyfikator korelacji nie jest ustawiona, biblioteka ADAL wygeneruje losowy. Wszystkie komunikaty dziennika i wywołania sieci zostanie następnie opatrzone identyfikatora hello korelacji. Witaj automatycznie wygenerowany zmiany Identyfikatora dla każdego żądania.

#### <a name="exceptions"></a>Wyjątki
Wyjątki są najpierw hello diagnostycznych. Spróbujemy tooprovide przydatne komunikaty. Jeśli znajdziesz taki, który nie jest pomocna, zgłoś problem i Daj nam znać. Zawierają informacje urządzenia, takie jak modelu oraz liczbę zestawu SDK.

#### <a name="logs"></a>Dzienniki
Można skonfigurować hello biblioteki toogenerate komunikatów dziennika, których można używać toohelp diagnozowanie problemów. Możesz skonfigurować rejestrowanie wprowadzając następujące hello wywołać tooconfigure ADAL użyje toohand poza wszystkich komunikatach dziennika, ponieważ jest ona generowana wywołanie zwrotne.

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

Komunikaty mogą być zapisywane tooa niestandardowego pliku dziennika, jak pokazano w hello następującego kodu. Niestety nie istnieje standardowy sposób pobierania dzienniki z urządzenia. Brak niektórych usług, które mogą pomóc Ci z tym. Można również zapasów własnych, takie jak wysyłanie hello tooa serwera plików.

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

Są to hello poziomów rejestrowania:
* Błąd (wyjątków)
* Warn (ostrzeżenie)
* Informacje o (celów informacyjnych)
* Pełne (więcej szczegółów)

Ustaw poziom dziennika hello następująco:

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 Wszystkie komunikaty dziennika są wysyłane toologcat, w wywołania zwrotne — Dodawanie tooany dziennik niestandardowy.
Plik dziennika tooa można uzyskać z logcat w następujący sposób:

    adb logcat > "C:\logmsg\logfile.txt"

 Aby uzyskać więcej informacji o poleceniach adb, zobacz hello [logcat informacji na temat witryny systemu Android hello](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).

#### <a name="network-traces"></a>Śledzenie sieci
Można użyć różnych narzędzi toocapture hello ruch HTTP generuje biblioteki ADAL.  Jest to najbardziej przydatne, jeśli znasz hello protokołu OAuth lub jeśli potrzebujesz tooMicrosoft informacje diagnostyczne tooprovide lub inne kanały pomocy technicznej.

Fiddler jest hello najprostszym narzędzie śledzenia HTTP. Użyj następujących hello łączy tooset go rekordu toocorrectly ADAL ruchu sieciowego. Dla narzędzia śledzenia, takiego jak toobe Fiddler lub Charlesa przydatne należy go skonfigurować toorecord bez szyfrowania ruchu protokołu SSL.  

> [!NOTE]
> Ślady generowane w ten sposób mogą zawierać wysoko uprzywilejowane informacje, takie jak tokenów dostępu, nazwy użytkowników i hasła. Jeśli używasz konta produkcji, nie są udostępniane te operacje śledzenia stron trzecich. Toosupply toosomeone śledzenia, w kolejności tooget obsługi, należy odtworzyć problem hello przy użyciu tymczasowego konta o nazwach użytkowników i hasła, czy nie stanowi udostępniania.

* Z witryny sieci Web hello strony firmy Telerik: [ustawienia zapasowej Fiddler dla systemu Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)
* Z witryny GitHub: [skonfigurować reguły Fiddler dotyczące biblioteki ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)

### <a name="dialog-mode"></a>Tryb okna dialogowego
Metoda acquireToken Hello bez działania obsługuje wiersza okna dialogowego.

### <a name="encryption"></a>Szyfrowanie
Biblioteka ADAL szyfruje hello tokeny i magazynu w SharedPreferences domyślnie. Można przyjrzeć się hello StorageHelper klasy toosee hello szczegóły. Android wprowadzonej Android Keystore 4.3 (interfejs API 18) bezpieczny magazyn kluczy prywatnych. Biblioteka ADAL użyty dla interfejsu API 18 lub nowszym. Jeśli chcesz toouse biblioteki ADAL dla niższych wersjach zestawu SDK, należy tooprovide klucza tajnego w AuthenticationSettings.INSTANCE.setSecretKey.

### <a name="oauth2-bearer-challenge"></a>Żądania elementu nośnego OAuth2
Hello klasy AuthenticationParameters udostępnia funkcje tooget authorization_uri z hello żądania elementu nośnego OAuth2.

### <a name="session-cookies-in-webview"></a>Pliki cookie z sesji w widoku sieci Web
Po zamknięciu aplikacji hello android WebView nie czyści plików cookie sesji. Który można obsługiwać przy użyciu ten przykładowy kod:

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

Aby uzyskać więcej informacji o plikach cookie, zobacz hello [CookieSyncManager informacji na temat witryny systemu Android hello](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).

### <a name="resource-overrides"></a>Zastąpienia zasobów
Biblioteka ADAL Hello zawiera ciągi angielskiej wersji językowej ProgressDialog wiadomości. Aplikacji należy je zastąpić, jeśli chcesz zlokalizowanych ciągów.

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a>Okno dialogowe NTLM
ADAL w wersji 1.1.0 obsługuje okno dialogowe NTLM, jest przetwarzany przez zdarzenie onReceivedHttpAuthRequest hello z WebViewClient. Możesz dostosować hello układ i ciągi dla hello — okno dialogowe.

### <a name="cross-app-sso"></a>Usługa rejestracji Jednokrotnej w wielu aplikacji
Dowiedz się [jak tooenable logowania jednokrotnego wielu aplikacji w systemie Android przy użyciu biblioteki ADAL](active-directory-sso-android.md).  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
