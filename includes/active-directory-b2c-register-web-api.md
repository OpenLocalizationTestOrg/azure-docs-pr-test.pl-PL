[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister interfejsu API, sieci web za pomocą ustawień hello określony w tabeli hello.

![Przykład ustawień rejestracji dla nowego internetowego interfejsu API](./media/active-directory-b2c-register-web-api/b2c-new-web-api-settings.png)

| Ustawienie      | Wartość przykładowa  | Opis                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Nazwa** | Interfejs API Contoso B2C | Wprowadź **nazwa** dla aplikacji hello, która opisuje tooconsumers Twojego interfejsu API. | 
| **Uwzględnij aplikację internetową/internetowy interfejs API** | Tak | Wybierz pozycję **Tak** dla internetowego interfejsu API. |
| **Zezwalaj na niejawny przepływ** | Tak | Wybierz pozycję **Tak**, jeśli Twoja aplikacja używa [logowania za pomocą uwierzytelniania OpenID Connect](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md) |
| **Adres URL odpowiedzi** | `https://localhost:44316/` | Adresy URL odpowiedzi to punkty końcowe, w których usługa Azure AD B2C będzie zwracać wszystkie tokeny żądane przez Twoją aplikację. Wprowadź [odpowiedni](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url) **adres URL odpowiedzi**. W tym przykładzie Twój internetowy interfejs API jest lokalny i nasłuchuje na porcie 44316. |
| **Identyfikator URI identyfikatora aplikacji** | api | Identyfikator URI aplikacji Hello jest identyfikatorem hello używany dla interfejsu API sieci web. Witaj pełny identyfikator, który zostanie wygenerowany identyfikator URI, łącznie z domeną hello. |

Kliknij przycisk **Utwórz** tooregister aplikacji.

Nowo zarejestrowanych aplikacji jest wyświetlane na liście aplikacji hello dla dzierżawy B2C hello. Wybierz interfejs API sieci web z listy hello. wyświetlane jest okienko właściwości Hello interfejsu API.

![Właściwości internetowego interfejsu API](./media/active-directory-b2c-register-web-api/b2c-web-api-properties.png)

Zwróć uwagę na powitania unikatowych **identyfikator klienta aplikacji**. Użycie Identyfikatora hello w kodzie aplikacji.
