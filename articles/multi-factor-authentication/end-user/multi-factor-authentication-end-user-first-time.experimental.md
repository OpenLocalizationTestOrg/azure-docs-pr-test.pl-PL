---
title: "aaaSet się weryfikację dwuetapową dla konta firmowego lub szkolnego | Dokumentacja firmy Microsoft"
description: "Gdy firma skonfiguruje Azure Multi-Factor Authentication, będzie toosign zostanie wyświetlony monit o utworzenie konta włączono weryfikację dwuetapową. Dowiedz się, jak tooset go. "
services: multi-factor-authentication
keywords: "jak toouse azure directory, usługi active directory w chmurze hello, samouczek usługi active directory"
documentationcenter: 
author: kgremban
manager: femila
editor: pblachar
ms.assetid: 46f83a6a-dbdd-4375-8dc4-e7ea77c16357
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2d0348081eefa42c23de2047044688879dcb5966
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-my-account-for-two-step-verification"></a>Skonfiguruj moje konto na potrzeby weryfikacji dwuetapowej
Weryfikacja dwuetapowa to dodatkowe zabezpieczenia krok, który pomaga chronić Twoje konto dokonując przeszkodę dla innych osób toobreak w. Jeśli czytasz ten artykuł, prawdopodobnie masz wiadomość e-mail od firmy lub szkoły administratorem temat uwierzytelniania wieloskładnikowego. Lub może być nastąpiła toosign w i otrzymano komunikat z pytaniem tooset się dodatkowej weryfikacji zabezpieczeń. Sytuacji hello **nie można zalogować przed ukończeniem procesu automatycznej rejestracji hello**.

Ten artykuł pomoże Ci skonfigurować Twoje **konto służbowe**. Jeśli chcesz tooenable weryfikacji dwuetapowej dla własnego, osobistego konta Microsoft, zobacz [o weryfikacji dwuetapowej](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).

## <a name="set-up-your-account"></a>Konfigurowanie konta

Gdy dział IT wymaga toostart przy użyciu weryfikacji dwuetapowej informacją o tym ekranu **administrator wymaga skonfigurowania tego konta na dodatkowej weryfikacji zabezpieczeń** pojawi się:

![Konfiguracja](./media/multi-factor-authentication-end-user-first-time/first.png)

Wybierz tooget pracę, **teraz skonfigurować.**

Jeśli nie pojawia się ekran podobny do tego po zalogowaniu, postępuj zgodnie ze wskazówkami hello [zarządzać ustawieniami na potrzeby weryfikacji dwuetapowej](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page) toofind hello ustawienia strony, której można zarządzać opcji weryfikacji. 

## <a name="decide-how-you-want-tooverify-your-sign-ins"></a>Określa sposób tooverify sesje logowania

pierwsze pytanie Hello w procesie rejestracji hello jest sposób nam toocontact użytkownik. Spójrz na powitania Opcje tabeli hello i użyj hello łącza toogo toohello ustawień czynności dla każdej metody.

| Metoda kontaktu | Opis |
| --- | --- |
| [Aplikacji mobilnej](#use-a-mobile-app-as-the-contact-method) |- **Odbieranie powiadomień o weryfikacji.** Ta opcja wypycha powiadomienie toohello wystawcy uwierzytelnienia aplikacji na smartfonie lub tablecie. Wyświetlanie hello powiadomień i, jeśli jest to uzasadnione, wybierz **Uwierzytelnij** w aplikacji hello. Konto służbowe może wymagać wprowadzenia kodu PIN przed uwierzytelniania.<br>- **Użyj kodu weryfikacyjnego.** W tym trybie hello aplikacja uwierzytelniania generuje kod weryfikacyjny, który aktualizuje co 30 sekund. Wprowadź kod weryfikacyjny z najbardziej aktualną hello w hello w interfejsie logowania.<br>Aplikacja Microsoft Authenticator Hello jest dostępna dla [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), i [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |
| [Telefonu komórkowego połączenia lub wiadomości SMS](#use-your-mobile-phone-as-the-contact-method) |- **Połączenie telefoniczne** miejsc wywołania automatycznych głosu toohello numer telefonu należy podać. Odpowiedzi na wywołanie hello, a następnie naciśnij klawisz # w tooauthenticate klawiaturze telefonu hello.<br>- **Wiadomość SMS** kończy się wiadomość tekstową zawierającą kod weryfikacyjny. Następujący wiersz hello w tekście hello Odpowiedz na wiadomość SMS toohello lub wprowadź kod weryfikacyjny hello dostarczone do hello w interfejsie logowania. |
| [Z telefonem biurowym](#use-your-office-phone-as-the-contact-method) |Umieszcza automatycznych głosu wywołania toohello numer telefonu, który podasz. Hello odpowiedzi wywołań i naciska klawisz # na powitania phone klawiatury tooauthenticate. |

## <a name="use-a-mobile-app-as-hello-contact-method"></a>Użyj aplikacji mobilnej jako metody kontaktu hello
Za pomocą tej metody wymaga zainstalowania aplikacji uwierzytelniania na swój telefon lub tablet. Witaj kroki opisane w tym artykule opierają się na aplikacji Microsoft Authenticator hello, która jest dostępna dla [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), i [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

1. Wybierz **aplikacji mobilnej** z listy rozwijanej hello.
2. Wybierz opcję **otrzymywać powiadomienia na potrzeby weryfikacji** lub **Użyj kodu weryfikacyjnego**, a następnie wybierz pozycję **Konfigurowanie**.

   ![Dodatkowe zabezpieczenia weryfikacji ekranu](./media/multi-factor-authentication-end-user-first-time/mobileapp.png)

3. Na swój telefon lub tablet, Otwórz aplikację hello i wybierz  **+**  tooadd konta. (Na urządzeniach z systemem Android, wybierz hello wielokropkiem, następnie **Dodaj konto**.)
4. Określ, czy tooadd konta firmowego lub szkolnego. Otwiera Hello skaner kodów QR w telefonie. Jeśli aparatu nie działa prawidłowo, można wybrać tooenter informacji o firmie ręcznie. Aby uzyskać więcej informacji, zobacz [ręcznie dodać konto](#add-an-account-manually).  
5. Skanuj obraz kodu QR hello pojawił się z ekranem hello konfigurowania hello aplikacji mobilnej.  Wybierz **gotowe** tooclose hello QR kodu ekranu.  

   ![Ekran kod QR](./media/multi-factor-authentication-end-user-first-time/scan2.png)

6. Po zakończeniu aktywacji w telefonie hello, wybierz **kontaktu mnie**.  Ten krok wysyła powiadomienie lub telefon tooyour kod weryfikacyjny. Wybierz **Sprawdź**.  
7. Jeśli zatwierdzanie weryfikacji logowania firmy wymaga numeru PIN, wprowadź go.

   ![Pole wprowadzania numeru PIN](./media/multi-factor-authentication-end-user-first-time/scan3.png)

8. Po zakończeniu wprowadzania numeru PIN, wybierz **Zamknij**. W tym momencie weryfikacja zostanie pomyślnie.
9. Firma Microsoft zaleca, możesz wprowadzić numer telefonu komórkowego na wypadek utraty aplikacji mobilnej tooyour dostępu. Określ w Twoim kraju z listy rozwijanej hello, a następnie wprowadź numer telefonu komórkowego w polu Nazwa kraju toohello dalej pole hello. Wybierz **dalej**.
10. Jesteś w tym momencie zostanie wyświetlony monit o tooset zapasowe haseł aplikacji dla aplikacji korzystających z przeglądarki, takich jak Outlook 2010 lub starszy lub hello natywna aplikacja poczty e-mail na urządzeniach Apple. Ta akcja jest, ponieważ niektóre aplikacje nie obsługują weryfikacji dwuetapowej. Nie należy używać tych aplikacji, kliknij przycisk **gotowe** i Pomiń pozostałe hello te kroki.
11. Jeśli używasz tych aplikacji Kopiuj hasło aplikacji hello podane i wklej go do aplikacji zamiast prawidłowe hasło. Witaj można użyć tego samego hasła aplikacji dla wielu aplikacji. Aby uzyskać więcej informacji [pomoc przy użyciu haseł aplikacji].
12. Kliknij przycisk **Gotowe**.

### <a name="add-an-account-manually"></a>Ręcznie dodaj konto
Tooadd konto aplikacji mobilnej toohello ręcznie, zamiast używać czytnika hello QR, wykonaj następujące kroki.

1. Wybierz hello **ręcznie wprowadź konto** przycisku.  
2. Wprowadź kod hello i hello adresu URL znajdujące się na powitania tej samej stronie, który pokazuje hello kod kreskowy. Te informacje o przechodzi w hello **kod** i **adres URL** pól na powitania aplikacji mobilnej.

    ![Konfiguracja](./media/multi-factor-authentication-end-user-first-time/barcode2.png)
3. Po zakończeniu aktywacji hello wybierz **kontaktu mnie**. Ten krok wysyła powiadomienie lub telefon tooyour kod weryfikacyjny. Wybierz **Sprawdź**.

## <a name="use-your-mobile-phone-as-hello-contact-method"></a>Użyć telefonu komórkowego jako metody kontaktu hello
1. Wybierz **numer telefonu uwierzytelniania** z listy rozwijanej hello.  

    ![Konfiguracja](./media/multi-factor-authentication-end-user-first-time/phone.png)  
2. Wybierz swój kraj z listy rozwijanej hello, a następnie wprowadź numer telefonu komórkowego.
3. Wybierz metodę hello toouse wolisz z telefonem komórkowym - SMS lub połączenie.
4. Wybierz **kontaktu mnie** tooverify Twojego numeru telefonu. W zależności od wybrany tryb hello możemy wysłać tekstu lub zadzwonić do Ciebie. Postępuj zgodnie z instrukcjami hello na ekranie powitania, a następnie wybierz **Sprawdź**.
5. Jesteś w tym momencie zostanie wyświetlony monit o tooset zapasowe haseł aplikacji dla aplikacji korzystających z przeglądarki, takich jak Outlook 2010 lub starszy lub hello natywna aplikacja poczty e-mail na urządzeniach Apple. Ta akcja jest, ponieważ niektóre aplikacje nie obsługują weryfikacji dwuetapowej. Nie należy używać tych aplikacji, kliknij przycisk **gotowe** i pominąć hello pozostałe kroki hello.
6. Jeśli używasz tych aplikacji Kopiuj hasło aplikacji hello podane i wklej go do aplikacji zamiast prawidłowe hasło. Witaj można użyć tego samego hasła aplikacji dla wielu aplikacji. Aby uzyskać więcej informacji [pomoc przy użyciu haseł aplikacji].
7. Kliknij przycisk **Gotowe**.

## <a name="use-your-office-phone-as-hello-contact-method"></a>Użyj jako metody kontaktu hello telefon biurowy
1. Wybierz **telefon biurowy** z listy rozwijanej hello  

    ![Konfiguracja](./media/multi-factor-authentication-end-user-first-time/office.png)  
2. pole numeru telefonu Hello jest automatycznie wypełniany swoje informacje kontaktowe firmy. Jeśli liczba hello jest nieprawidłowe lub brakujące, poproś administratora o jego toomake zmiany.
3. Wybierz **kontaktu mnie** tooverify Twojego numeru telefonu i firma Microsoft będzie wywoływać numer. Postępuj zgodnie z instrukcjami hello na ekranie powitania, a następnie wybierz **Sprawdź**.
4. Jesteś w tym momencie zostanie wyświetlony monit o tooset zapasowe haseł aplikacji dla aplikacji korzystających z przeglądarki, takich jak Outlook 2010 lub starszy lub hello natywna aplikacja poczty e-mail na urządzeniach Apple. Ta akcja jest, ponieważ niektóre aplikacje nie obsługują weryfikacji dwuetapowej. Nie należy używać tych aplikacji, kliknij przycisk **gotowe** i pominąć hello pozostałe kroki hello.
5. Jeśli używasz tych aplikacji Kopiuj hasło aplikacji hello podane i wklej go do aplikacji zamiast prawidłowe hasło. Witaj można użyć tego samego hasła aplikacji dla wielu aplikacji. Aby uzyskać więcej informacji, zobacz [co to są hasła aplikacji](multi-factor-authentication-end-user-app-passwords.md).
6. Kliknij przycisk **Gotowe**.

## <a name="next-steps"></a>Następne kroki
* Zmienianie opcji i [zarządzać ustawieniami na potrzeby weryfikacji dwuetapowej](multi-factor-authentication-end-user-manage-settings.md)
* Konfigurowanie [hasła aplikacji](multi-factor-authentication-end-user-app-passwords.md) dla aplikacji natywnych urządzenia, które nie obsługują weryfikacji dwuetapowej.
* Zapoznaj się z hello [aplikacji Microsoft Authenticator](microsoft-authenticator-app-how-to.md) Aby szybko i bezpiecznie uwierzytelniania nawet wtedy, gdy nie ma usługi komórki.

