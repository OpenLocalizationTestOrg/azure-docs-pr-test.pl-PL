## <a name="test-your-code"></a>Testowanie kodu

Aby uruchomić projekt, w programie Visual Studio, wybierz **F5**. Aplikacja **właściwości MainWindow** jest wyświetlana, jak pokazano poniżej:

![Testowanie aplikacji](./media/active-directory-develop-guidedsetup-windesktop-test/samplescreenshot.png)

Uruchamianie aplikacji po raz pierwszy i wybierz **wywołać Microsoft interfejsu API programu Graph** przycisku, zostanie wyświetlony monit do logowania. Użyj konta usługi Azure Active Directory (konta firmowego lub szkolnego) lub konta Microsoft (live.com, outlook.com), aby przetestować go.

![Zaloguj się do aplikacji](./media/active-directory-develop-guidedsetup-windesktop-test/signinscreenshot.png)

### <a name="provide-consent-for-application-access"></a>Podaj zgody na dostęp do aplikacji
Podczas pierwszego logowania się do aplikacji, zostanie również wyświetlony monit zapewnienie wyrażenia zgody na umożliwić aplikacji dostęp do Twojego profilu i logowanie się w, jak pokazano poniżej: 

![Wyrażenie zgody na dostęp do aplikacji](./media/active-directory-develop-guidedsetup-windesktop-test/consentscreen.png)

### <a name="view-application-results"></a>Wyświetl wyniki aplikacji
Po zalogowaniu, powinny być widoczne informacje o profilu użytkownika, które jest zwracany przez wywołanie interfejsu API programu Microsoft Graph. Wyniki są wyświetlane w **wyniki wywołania interfejsu API** pole. Podstawowe informacje o token, który został uzyskany za pośrednictwem wywołania `AcquireTokenAsync` lub `AcquireTokenSilentAsync` powinny być widoczne w **informacji o tokenie** pole. Wyniki obejmują następujące właściwości:

|Właściwość  |Format  |Opis |
|---------|---------|---------|
|**Nazwa** |Imię i nazwisko użytkownika |Imię i nazwisko użytkownika.|
|**Nazwa użytkownika** |<span>user@domain.com</span> |Nazwa użytkownika, która jest używana do identyfikacji użytkownika.|
|**Wygaśnięcia tokenu** |Data/godzina |Czas, w którym token jest ważny. MSAL rozszerza datę wygaśnięcia, odnowienie tokenu w razie potrzeby.|
|**Token dostępu** |Ciąg |Tokenu ciąg, który jest wysyłany do HTTP żądań, które wymagają *nagłówek autoryzacji*.|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Więcej informacji o zakresach i uprawnień delegowanych

Wymaga interfejsu API programu Microsoft Graph *user.read* zakresu odczytać profilu użytkownika. Ten zakres jest automatycznie dodawany domyślnie w każdej aplikacji, która jest zarejestrowana w portalu rejestracji aplikacji. Inne interfejsy API dla programu Microsoft Graph, a także niestandardowych interfejsów API dla serwera zaplecza może wymagać dodatkowych zakresów. Wymaga interfejsu API programu Microsoft Graph *Calendars.Read* zakres, aby wyświetlić listę kalendarzy użytkownika.

Aby uzyskać dostęp do kalendarzy użytkownika w kontekście aplikacji, należy dodać *Calendars.Read* delegowane uprawnienia do informacji o rejestracji aplikacji. Następnie należy dodać *Calendars.Read* zakres do `acquireTokenSilent` wywołania. 

>[!NOTE]
>Użytkownik może zostać wyświetlony monit dla dodatkowych zgody, jak zwiększyć liczbę zakresów.

<!--end-collapse-->

[!INCLUDE  [Help and support](./active-directory-develop-help-support-include.md)]
