hasło szczegółowych tooenable zresetować w swojej aplikacji, konieczne będzie toocreate zasady resetowania hasła. Uwaga określono opcję resetowania hasła na poziomie dzierżawy tego hello [tutaj](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md). Ta zasada opisuje hello procesów, które konsumentów hello będzie przejście przez podczas resetowania hasła i zawartość hello tokeny hello aplikacji zostanie wyświetlony po pomyślnym ukończeniu.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

W sekcji Ustawienia zasad hello, zaznacz **zasady resetowania hasła** i kliknij przycisk **+ Dodaj**.

![Wybierz zasady rejestracji i logowania i kliknij przycisk Dodaj hello](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

Wprowadź zasady **nazwa** dla tooreference Twojej aplikacji. Na przykład wprowadź wartość `SSPR`.

Wybierz pozycję **Dostawcy tożsamości** i zaznacz pozycję **Resetuj hasło przy użyciu adresu e-mail**. Kliknij przycisk **OK**.

![Wybierz resetowania hasła przy użyciu adresu e-mail jako dostawca tożsamości, a następnie kliknij przycisk OK hello](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

Wybierz pozycję **Oświadczenia aplikacji**. Wybrać oświadczenia, które mają być zwracane w tokenach autoryzacji hello wysyłane aplikacji tooyour wstecz po funkcji resetowania hasła powiodło się. Na przykład wybierz pozycję **Identyfikator obiektu użytkownika**.

![Wybierz część oświadczeń aplikacji i kliknij przycisk OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

Kliknij przycisk **Utwórz** tooadd hello zasad. zasada Hello jest wyświetlana jako **B2C_1_SSPR**. Witaj **B2C_1_** prefiks jest dołączany toohello nazwy.

Otwórz hello zasady, wybierając **B2C_1_SSPR**. Sprawdź ustawienia hello określony w tabeli hello, a następnie kliknij przycisk **Uruchom teraz**.

![Wybierz zasady, a następnie uruchom je](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| Ustawienie      | Wartość  |
| ------------ | ------ |
| **Aplikacje** | Aplikacja Contoso B2C |
| **Wybierz adres URL odpowiedzi** | `https://localhost:44316/` |

Otwiera nową kartę przeglądarki i możesz sprawdzić, czy resetowania hasła hello korzystanie w aplikacji.

> [!NOTE]
> Zajmuje minutę tooa do tworzenia zasad on i aktualizuje tootake efekt.
>
