[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister aplikacji sieci web, użyj ustawień hello określony w tabeli hello.

![Przykład ustawień rejestracji dla nowej aplikacji internetowej](./media/active-directory-b2c-register-web-app/b2c-new-app-settings.png)

| Ustawienie      | Wartość przykładowa  | Opis                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Nazwa** | Aplikacja Contoso B2C | Wprowadź **nazwa** dla aplikacji hello, która opisuje tooconsumers Twojej aplikacji. | 
| **Uwzględnij aplikację internetową/internetowy interfejs API** | Tak | Wybierz pozycję **Tak** dla aplikacji internetowej. |
| **Zezwalaj na niejawny przepływ** | Tak | Wybierz pozycję **Tak**, jeśli Twoja aplikacja używa [logowania za pomocą uwierzytelniania OpenID Connect](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md) |
| **Adres URL odpowiedzi** | `https://localhost:44316` | Adresy URL odpowiedzi to punkty końcowe, w których usługa Azure AD B2C będzie zwracać wszystkie tokeny żądane przez Twoją aplikację. Wprowadź [odpowiedni](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url) **adres URL odpowiedzi**. W tym przykładzie Twoja aplikacja jest lokalna i nasłuchuje na porcie 44316. |

Kliknij przycisk **Utwórz** tooregister aplikacji.

Nowo zarejestrowanych aplikacji jest wyświetlane na liście aplikacji hello dla dzierżawy B2C hello. Wybierz aplikację sieci web z listy hello. w okienku właściwości aplikacji sieci web Hello jest wyświetlany.

![Właściwości aplikacji internetowej](./media/active-directory-b2c-register-web-app/b2c-web-app-properties.png)

Zwróć uwagę na powitania unikatowych **identyfikator klienta aplikacji**. Użycie Identyfikatora hello w kodzie aplikacji.
