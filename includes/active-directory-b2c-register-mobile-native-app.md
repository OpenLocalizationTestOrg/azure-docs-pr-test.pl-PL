[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister aplikacji mobilnych lub macierzystego, użyj ustawień hello określony w tabeli hello.

![Przykład ustawień rejestracji dla nowej aplikacji mobilnej lub natywnej](./media/active-directory-b2c-register-mobile-native-app/b2c-new-mobile-native-app-settings.png)

| Ustawienie      | Wartość przykładowa  | Opis                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Nazwa** | Aplikacja Contoso B2C | Wprowadź **nazwa** dla aplikacji hello, która opisuje tooconsumers Twojej aplikacji. |
| **Natywny klient** | Tak | Wybierz pozycję **Tak** dla aplikacji mobilnej lub natywnej. |
| **Niestandardowy identyfikator URI przekierowania** | `com.onmicrosoft.contoso.appname://redirect/path` | Wprowadź identyfikator URI przekierowania ze schematem niestandardowym. Pamiętaj, aby wybrać [właściwy identyfikator URI przekierowywania](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-native-application-redirect-uri). Nie powinien on zawierać znaków specjalnych, takich jak podkreślenia. |

Kliknij przycisk **Utwórz** tooregister aplikacji.

Nowo zarejestrowanych aplikacji jest wyświetlane na liście aplikacji hello dla dzierżawy B2C hello. Wybierz aplikacji mobilnych lub macierzysty z listy hello. okienko właściwości aplikacji Hello jest wyświetlany.

![Właściwości aplikacji](./media/active-directory-b2c-register-mobile-native-app/b2c-mobile-native-app-properties.png)

Zwróć uwagę na powitania unikatowych **identyfikator klienta aplikacji**. Użycie Identyfikatora hello w kodzie aplikacji.

Jeśli Twoja natywna aplikacja wywołuje internetowy interfejs API zabezpieczony przez usługę Azure AD B2C, wykonaj następujące kroki:
   1. Utwórz klucz tajny aplikacji przez przejście toohello **klucze** bloku i klikając hello **Wygeneruj klucz** przycisku. Zwróć uwagę na powitania **klucz aplikacji** wartość. Wartość hello są używane jako klucz tajny aplikacji hello w kodzie aplikacji.
   2. Kliknij pozycję **Dostęp do interfejsu API**, kliknij pozycję **Dodaj** i wybierz swój internetowy interfejs API oraz zakresy (uprawnienia).

> [!NOTE]
> **Klucz tajny aplikacji** jest ważnym poświadczeniem zabezpieczeń i powinien być odpowiednio zabezpieczony.
> 
