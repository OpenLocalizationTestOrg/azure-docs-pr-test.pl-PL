---
title: "AAA \"nie ma dostępu do tego błędu aplikacji firmowych podczas korzystania z aplikacji serwera Proxy aplikacji | Dokumentacja firmy Microsoft\""
description: "Jak tooresolve dostępu typowe problemy związane z aplikacji serwera Proxy aplikacji usługi Azure AD."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 490b106b7d774ee43fc076cc5d082997a1df85e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cant-access-this-corporate-application-error-when-using-an-application-proxy-application"></a>Błąd "Nie można uzyskać dostępu do tej aplikacji firmowych" podczas korzystania z aplikacji serwera Proxy aplikacji

W tym artykule pomocy tootroubleshoot typowych problemów, które muszą ponieść kiedy zostanie wyświetlony komunikat o błędzie "nie ma dostępu tej aplikacji firmowych" aplikacji serwera Proxy aplikacji usługi Azure AD.

## <a name="overview"></a>Omówienie
Gdy zostanie wyświetlony ten błąd strony hello również udostępniać kod stanu. Ten kod jest prawdopodobnie jednym z następujących hello:

-   **Limit czasu bramy**: powitania serwera Proxy aplikacji usługi jest tooreach hello łącznika. Zwykle oznacza to problem z hello przypisania łącznika, łącznik sam lub hello sieci reguły wokół hello łącznika.

-   **Zła brama**: hello łącznika jest tooreach hello wewnętrznej bazy danych aplikacji. Może to oznaczać błąd konfiguracji aplikacji hello.

-   **Dostęp zabroniony**: hello użytkownik nie jest upoważniony tooaccess aplikacji hello. Może się to zdarzyć, gdy hello użytkownika nie jest przypisany toohello aplikacji w usłudze Azure Active Directory lub jeśli hello wewnętrznej bazy danych hello użytkownika nie ma aplikacji hello tooaccess uprawnienia.

toofind hello kod wyglądu tekstu hello w lewym dolnym hello hello komunikat o błędzie dla pola "Kodu stanu" hello. Wyszukaj także wszelkie uwagi na powitania dołu strony hello z dodatkowych porad.

   ![Błąd limitu czasu bramy](./media/application-proxy/connection-problem.png)

Szczegółowe informacje dotyczące sposobu tootroubleshoot hello przyczynę tych błędów oraz dodatkowe szczegóły dotyczące sugerowanej poprawki Zobacz hello odpowiedniej sekcji poniżej.

## <a name="gateway-timeout-errors"></a>Błędy przekroczenia limitu czasu bramy

Przekroczenie limitu czasu bramy występuje, gdy usługa hello próbuje łącznika hello tooreach i toowithin hello limicie. Zwykle jest to spowodowane aplikacji przypisany tooa grupy łącznika z nie łączników pracy lub niektóre porty wymagane przez hello łącznika nie są otwarte.


## <a name="bad-gateway-errors"></a>Zły błędy bramy

Błąd bramy zły wskazuje, że ten łącznik hello jest tooreach hello wewnętrznej bazy danych aplikacji. Upewnij się, opublikowano hello właściwej aplikacji. Typowych błędów, które są przyczyną tego błędu:

-   Literówka lub błędy w hello wewnętrznego adresu URL

-   Nie publikowania hello katalog główny aplikacji hello. Na przykład publikowania <http://expenses/reimbursement> , ale w trakcie tooaccess <http://expenses>

-   Problemy związane z konfiguracją delegowanie ograniczone protokołu Kerberos (KCD) hello

-   Problemy z hello wewnętrznej bazy danych aplikacji

## <a name="forbidden-errors"></a>Błędy niedozwolonych

Jeśli zostanie wyświetlony błąd zabronione, hello użytkownikowi nie przypisano toohello aplikacji. Może to być w usłudze Azure Active Directory lub na powitania wewnętrznej bazy danych aplikacji.

toolearn tooassign użytkowników toohello aplikacji na platformie Azure, zobacz temat hello [dokumentacji konfiguracji](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal#add-a-test-user).

Jeśli potwierdzisz, że użytkownik hello jest przypisany toohello aplikacji na platformie Azure, sprawdź konfigurację użytkownika hello w hello wewnętrznej bazy danych aplikacji. Jeśli używasz uwierzytelniania systemu Windows zintegrowany/delegowania ograniczonego protokołu Kerberos, widać stronę dotyczącą rozwiązywania KCD dla wskazówki.

## <a name="check-hello-applications-internal-url"></a>Wewnętrzny adres URL aplikacji hello wyboru

Pierwszym krokiem szybki, sprawdź ponownie sprawdź i napraw hello wewnętrznego adresu URL przez otwarcie aplikacji hello za pomocą **aplikacje dla przedsiębiorstw**, a następnie wybierając hello **serwera Proxy aplikacji** menu. Sprawdź, czy jest to hello poprawny wewnętrzny adres URL, hello korzysta z aplikacji hello tooaccess sieci lokalnej.

## <a name="check-hello-application-is-assigned-tooa-working-connector-group"></a>Sprawdź, czy aplikacja hello jest przypisany tooa Praca grupy łącznika

Aplikacja hello tooverify przypisano tooa łącznika grupę roboczą:

1.  Otwórz aplikację hello w portalu hello przechodząc zbyt**usługi Azure Active Directory**, klikając pozycję na **aplikacje dla przedsiębiorstw**, następnie **wszystkie aplikacje.** Otwórz aplikację hello, a następnie wybierz **serwera Proxy aplikacji** z menu po lewej stronie powitania.

2.  Spójrz na powitania pole grupy łącznika. Jeśli w grupie hello nie żadne łączniki active, zostanie wyświetlone ostrzeżenie. Jeśli nie widzisz wszelkie ostrzeżenia, przesuń zbyt "Sprawdź, czy wszystkie wymagane porty na białej".

3.  Jeśli to hello niewłaściwej grupy łącznika, użyj hello listy rozwijanej tooselect hello prawidłowej grupy, a następnie upewnij się, że nie są już wyświetlane ostrzeżenia. Jeśli jest to hello przeznaczone grupy łącznik, kliknij przycisk hello komunikat tooopen hello strona z ostrzeżeniem o zarządzania łącznika.

4.  W tym miejscu są kilka sposobów toodrill w dalszych:

  * Przenieś łącznika usługi active do grupy hello: Jeśli masz łącznika usługi active muszą należeć do grupy toothis i ma wiersza z procesów toohello docelowej zaplecza aplikacji hello łącznika można przenieść do grupy hello przypisane. toodo tak, kliknij przycisk hello łącznika. W polu "Łącznik grupy" hello Użyj hello tooselect listy rozwijanej hello prawidłowej grupy, a następnie kliknij przycisk Zapisz.

  * Pobierz nowy łącznik, dla tej grupy: na tej stronie można uzyskać łącze hello zbyt[Pobierz nowy łącznik](https://download.msappproxy.net/Subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/Connector/Download). Hello łącznika potrzeb toobe zainstalowany na komputerze z aplikacją zaplecza toohello bezpośredniego procesów z wiersza i zwykle znajduje się na hello tym samym serwerze co aplikacja hello. Użyj hello Pobierz łącznik łącze toodownload łącznika na komputerze docelowym hello. Następnie kliknij hello łącznika, a następnie użyj toomake listy rozwijanej "Łącznik grupy" hello się, że należy toohello prawo grupy.

  * Zbadaj łącznik nieaktywne: Jeśli łącznik pokazuje jako nieaktywny, tooreach hello usługa ta jest. Jest to zazwyczaj powodu toosome wymagane porty blokowane. toosolve ten problem, Przenieś na zbyt "Sprawdź wszystkie wymagane porty są białej".

Po zakończeniu korzystania z tych kroków aplikacja hello tooensure jest grupy przypisanej tooa z łączników, ponownie aplikacji hello testowej pracy. Jeśli nadal nie działa ono, nadal toohello następnej sekcji.

## <a name="check-all-required-ports-are-whitelisted"></a>Sprawdź, czy wszystkie wymagane porty na białej

tooverify, czy wszystkie wymagane porty są otwarte, zobacz dokumentację dotyczącą na otwieranie portów. Jeśli wszystkie hello wymagane porty są otwarte, należy przenieść toohello następnej sekcji.

## <a name="check-for-other-connector-errors"></a>Sprawdź, czy inne błędy łącznika

Jeśli żaden z powyższych hello rozwiązać problem hello, następnym krokiem hello jest toolook problemy lub komunikaty o błędach z hello łącznik sam. Można wyświetlić niektórych typowych błędów w hello [Rozwiązywanie problemów dotyczących dokumentu](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors). 

Można również sprawdzić bezpośrednio na powitania łącznika dzienniki tooidentify wszelkie błędy. Wiele nasze komunikaty o błędach, być może tooshare bardziej szczegółowe zalecenia dotyczące poprawki. toolearn tooview hello dzienników, zobacz temat [naszej dokumentacji łączniki](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).

## <a name="additional-resolutions"></a>Dodatkowe rozwiązania

Jeśli hello powyżej nie rozwiąże problemu hello, istnieje kilka różnych przyczyn. problem hello tooidentify:

Jeśli aplikacja jest skonfigurowana toouse zintegrowane uwierzytelnianie systemu (IWA), bez logowania jednokrotnego dla aplikacji hello testowej. Jeśli nie, Przenieś toohello następnego akapitu. Aplikacja hello toocheck bez rejestracji jednokrotnej, Otwórz aplikację za pomocą **aplikacje dla przedsiębiorstw,** i przejdź toohello **rejestracji jednokrotnej** menu. Witaj zmiany listy rozwijanej "Zintegrowane uwierzytelnianie systemu Windows" za "Azure AD rejestracji jednokrotnej wyłączone". 

Teraz Otwórz przeglądarkę i spróbuj ponownie aplikacji hello tooaccess. Powinien zostać wyświetlony monit o uwierzytelnienie oraz uzyskiwanie do aplikacji hello. Jeśli wynik działania, hello problem dotyczy hello konfigurację delegowanie ograniczone protokołu Kerberos (KCD), która umożliwia hello rejestracji jednokrotnej. Zobacz hello KCD Rozwiązywanie problemów z strony.

W przypadku kontynuowania toosee hello błąd Przejdź toohello maszyny, gdzie powitalne łącznik jest zainstalowany, otwórz przeglądarki, a następnie spróbuj tooreach hello wewnętrzny adres URL użyty dla aplikacji hello. Witaj łącznik działa jak innego klienta z hello tym samym komputerze. Jeśli nie dotrzeć aplikacji hello, zbadać, dlaczego komputer ten jest aplikacji hello tooreach lub użyć łącznika na serwerze, który jest w stanie tooaccess hello aplikacji.

Jeśli aplikacja hello z tego komputera, toolook problemy lub komunikaty o błędach z hello łącznik sam może nawiązać połączenie. Można wyświetlić niektórych typowych błędów w hello [Rozwiązywanie problemów dotyczących dokumentu](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors). Można również sprawdzić bezpośrednio na powitania łącznika dzienniki tooidentify wszelkie błędy. Wiele nasze komunikaty o błędach, być może tooshare bardziej szczegółowe zalecenia dotyczące poprawki. toolearn tooview hello dzienników, zobacz temat [naszej dokumentacji łączniki](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).

## <a name="next-steps"></a>Następne kroki
[Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD](application-proxy-understand-connectors.md)
