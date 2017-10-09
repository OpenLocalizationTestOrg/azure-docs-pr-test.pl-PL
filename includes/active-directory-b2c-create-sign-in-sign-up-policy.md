Logowanie tooenable dla aplikacji, konieczne będzie zasad toocreate logowania. Ta zasada opis hello procesów, które konsumentów będzie przejście przez podczas logowania i zawartość hello tokeny hello aplikacji zostanie wyświetlony na pomyślne logowania.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

W sekcji Ustawienia zasad hello, zaznacz **zasad rejestracji i logowania** i kliknij przycisk **+ Dodaj**.

![Wybierz zasady rejestracji lub logowania i kliknij przycisk Dodaj](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

Wprowadź zasady **nazwa** dla tooreference Twojej aplikacji. Na przykład wprowadź wartość `SiUpIn`.

Wybierz pozycję **Dostawcy tożsamości** i zaznacz pozycję **Tworzenie konta za pomocą adresu e-mail**. Opcjonalnie możesz również wybrać dostawców tożsamości społecznościowych, jeśli są już skonfigurowani. Kliknij przycisk **OK**.

![Wybierz zapisywania wiadomości E-mail jako dostawca tożsamości i kliknij przycisk OK hello](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

Wybierz pozycję **Atrybuty tworzenia konta**. Wybierz atrybuty ma toocollect od konsumenta hello podczas tworzenia konta. Na przykład zaznacz pozycje **Kraj/Region**, **Nazwa wyświetlana** i **Kod pocztowy**. Kliknij przycisk **OK**.

![Wybierz niektóre atrybuty i kliknij przycisk OK hello](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

Wybierz pozycję **Oświadczenia aplikacji**. Wybrać oświadczenia, które mają być zwracane w tokenach autoryzacji hello wysłanych wstecz tooyour aplikacji po pomyślnej rejestracji lub logowania systemu. Na przykład wybierz pozycje **Nazwa wyświetlana**, **Dostawca tożsamości**, **Kod pocztowy**, **Użytkownik jest nowy** i **Identyfikator obiektu użytkownika**.

![Wybierz część oświadczeń aplikacji i kliknij przycisk OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

Kliknij przycisk **Utwórz** tooadd hello zasad. zasada Hello jest wyświetlana jako **B2C_1_SiUpIn**. Witaj **B2C_1_** prefiks jest dołączany toohello nazwy.

Otwórz hello zasady, wybierając **B2C_1_SiUpIn**. Sprawdź ustawienia hello określony w tabeli hello, a następnie kliknij przycisk **Uruchom teraz**.

![Wybierz zasady, a następnie uruchom je](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| Ustawienie      | Wartość  |
| ------------ | ------ |
| **Aplikacje** | Aplikacja Contoso B2C |
| **Wybierz adres URL odpowiedzi** | `https://localhost:44316/` |

Można sprawdzić hello środowisko rejestracji i logowania użytkownika, zgodnie z konfiguracją i otwiera nową kartę przeglądarki.

> [!NOTE]
> Zajmuje minutę tooa do tworzenia zasad on i aktualizuje tootake efekt.
>