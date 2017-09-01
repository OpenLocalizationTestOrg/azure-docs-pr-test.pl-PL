[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

Aby zarejestrować swoją mobilną lub natywną aplikację, użyj ustawień określonych w tabeli.

![Przykład ustawień rejestracji dla nowej aplikacji mobilnej lub natywnej](./media/active-directory-b2c-register-mobile-native-app/b2c-new-mobile-native-app-settings.png)

| Ustawienie      | Wartość przykładowa  | Opis                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Nazwa** | Aplikacja Contoso B2C | Wprowadź **Nazwę**, która będzie opisywać aplikację użytkownikom. |
| **Natywny klient** | Tak | Wybierz pozycję **Tak** dla aplikacji mobilnej lub natywnej. |
| **Niestandardowy identyfikator URI przekierowania** | `com.onmicrosoft.contoso.appname://redirect/path` | Wprowadź identyfikator URI przekierowania ze schematem niestandardowym. Pamiętaj, aby wybrać [właściwy identyfikator URI przekierowywania](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-native-application-redirect-uri). Nie powinien on zawierać znaków specjalnych, takich jak podkreślenia. |

Kliknij pozycję **Utwórz**, aby zarejestrować aplikację.

Nowo zarejestrowana aplikacja jest wyświetlana na liście aplikacji dla dzierżawy usługi B2C. Wybierz aplikację mobilną lub natywną z listy. Zostanie wyświetlone okienko właściwości aplikacji.

![Właściwości aplikacji](./media/active-directory-b2c-register-mobile-native-app/b2c-mobile-native-app-properties.png)

Zanotuj globalnie unikatowy **Identyfikator klienta aplikacji**. Użyjesz tego identyfikatora w kodzie Twojej aplikacji.

Jeśli Twoja natywna aplikacja wywołuje internetowy interfejs API zabezpieczony przez usługę Azure AD B2C, wykonaj następujące kroki:
   1. Utwórz wpis tajny aplikacji, przechodząc do bloku **Klucze** i klikając przycisk **Wygeneruj klucz**. Zanotuj wartość pola **Klucz aplikacji**. Użyj tej wartości jako wpisu tajnego aplikacji w kodzie Twojej aplikacji.
   2. Kliknij pozycję **Dostęp do interfejsu API**, kliknij pozycję **Dodaj** i wybierz swój internetowy interfejs API oraz zakresy (uprawnienia).

> [!NOTE]
> **Klucz tajny aplikacji** jest ważnym poświadczeniem zabezpieczeń i powinien być odpowiednio zabezpieczony.
> 
