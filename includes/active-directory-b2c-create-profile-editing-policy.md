Profil tooenable edycji w swojej aplikacji, konieczne będzie toocreate profilu edytowanie zasad. Ta zasada opisuje hello procesów, które konsumentów będzie przejście przez podczas edycji i hello zawartość profilu tokenów otrzymujących aplikacji hello na pomyślne zakończenie.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

W sekcji Ustawienia zasad hello, zaznacz **profilu edytowanie zasad** i kliknij przycisk **+ Dodaj**.

![Wybierz profil edytowanie zasad, a następnie kliknij przycisk Dodaj hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

Wprowadź zasady **nazwa** dla tooreference Twojej aplikacji. Na przykład wprowadź wartość `SiPe`.

Wybierz pozycję **Dostawcy tożsamości** i zaznacz pozycję **Logowanie za pomocą konta lokalnego**. Opcjonalnie możesz również wybrać dostawców tożsamości społecznościowych, jeśli są już skonfigurowani. Kliknij przycisk **OK**.

![Wybierz lokalnego konta Logowanie jako dostawca tożsamości, a następnie kliknij przycisk OK hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

Wybierz pozycję **Atrybuty profilu**. Wybierz atrybuty powitania klienta można wyświetlać i edytować swój profil. Na przykład zaznacz pozycje **Kraj/Region**, **Nazwa wyświetlana** i **Kod pocztowy**. Kliknij przycisk **OK**.

![Wybierz niektóre atrybuty i kliknij przycisk OK hello](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

Wybierz pozycję **Oświadczenia aplikacji**. Wybrać oświadczenia, które mają być zwracane w tokenach autoryzacji hello wysłanych wstecz tooyour aplikacji po pomyślnej sposób edytowania profilów. Na przykład wybierz pozycje **Nazwa wyświetlana**, **Kod pocztowy**.

![Wybierz część oświadczeń aplikacji i kliknij przycisk OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

Kliknij przycisk **Utwórz** tooadd hello zasad. zasada Hello jest wyświetlana jako **B2C_1_SiPe**. Witaj **B2C_1_** prefiks jest dołączany toohello nazwy.

Otwórz hello zasady, wybierając **B2C_1_SiPe**. Sprawdź ustawienia hello określony w tabeli hello, a następnie kliknij przycisk **Uruchom teraz**.

![Wybierz zasady, a następnie uruchom je](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| Ustawienie      | Wartość  |
| ------------ | ------ |
| **Aplikacje** | Aplikacja Contoso B2C |
| **Wybierz adres URL odpowiedzi** | `https://localhost:44316/` |

Można sprawdzić profilu hello edytowania zgodnie z konfiguracją konsumenta i otwiera nową kartę przeglądarki.

> [!NOTE]
> Zajmuje minutę tooa do tworzenia zasad on i aktualizuje tootake efekt.
>