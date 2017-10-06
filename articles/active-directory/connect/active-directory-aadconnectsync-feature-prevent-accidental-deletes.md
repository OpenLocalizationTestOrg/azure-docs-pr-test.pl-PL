---
title: 'Synchronizacja programu Azure AD Connect: Zapobieganie przypadkowemu usuwaniu | Dokumentacja firmy Microsoft'
description: "W tym temacie opisano hello Zapobieganie przypadkowemu usuwaniu (zapobieganie przypadkowym usunięciu) funkcji w programie Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b852cb4-2850-40a1-8280-8724081601f7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 159597f8354806fcaea1430e0ff84956338592a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-prevent-accidental-deletes"></a>Synchronizacja programu Azure AD Connect: zapobieganie przypadkowemu usuwaniu
W tym temacie opisano hello Zapobieganie przypadkowemu usuwaniu (zapobieganie przypadkowym usunięciu) funkcji w programie Azure AD Connect.

Po zainstalowaniu programu Azure AD Connect, zapobieganie przypadkowemu usuwa jest domyślnie włączona i skonfigurowana toonot — Zezwalaj na eksport z więcej niż 500 usuwa. Ta funkcja jest zaprojektowana tooprotect z konfiguracji przypadkowemu zmiany i zmienia tooyour lokalnego katalogu, które będą wpływać na liczbę użytkowników i innych obiektów.

## <a name="what-is-prevent-accidental-deletes"></a>Co to jest Zapobieganie przypadkowemu usuwaniu
Typowe scenariusze Zobacz wiele usuwa obejmują:

* Zmienia zbyt[filtrowania](active-directory-aadconnectsync-configure-filtering.md) w przypadku, gdy cały [OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) lub [domeny](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) nie jest zaznaczona.
* Wszystkie obiekty w jednostce Organizacyjnej zostaną usunięte.
* Jednostka Organizacyjna zostanie zmieniona, więc wszystkie obiekty w nim są traktowane jako toobe poza zakresem synchronizacji.

Wartość domyślna Hello 500 obiektów można zmienić przy użyciu programu PowerShell przy użyciu `Enable-ADSyncExportDeletionThreshold`. Należy skonfigurować ten rozmiar hello toofit wartość w Twojej organizacji. Ponieważ harmonogramu synchronizacji hello uruchamia co 30 minut, wartość hello jest liczba hello usuwa występuje w ciągu 30 minut.

Jeśli istnieje zbyt wiele toobe usunięcia umieszczone wyeksportowane tooAzure AD, hello eksportu zostanie zatrzymane i odbierać wiadomości e-mail, jak to:

![Zapobieganie przypadkowemu usuwaniu poczty e-mail](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/email.png)

> *Witaj (technicznych skontaktuj się z). Godzinie hello usługi synchronizacji tożsamości wykrył, że hello liczba operacji usunięcia przekracza próg usuwania skonfigurowanych hello (nazwa organizacji). Całkowita liczba (numer) obiektów zostały wysłane do usunięcia w tej synchronizacji tożsamości, uruchom. To osiągnięto lub przekroczono hello skonfigurowana wartość progowa usuwania obiektów (numer). Konieczne jest tooprovide potwierdzenie, że te usunięcie powinny być przetworzone przed firma Microsoft będzie kontynuowana. Zobacz hello uniemożliwia przypadkowym usunięciu, aby uzyskać więcej informacji o błędzie hello wymienione w tej wiadomości e-mail.*
>
> 

Można również wyświetlić stan hello `stopped-deletion-threshold-exceeded` podczas przeglądania w hello **Menedżera usługi synchronizacji** interfejsu użytkownika dla profilu eksportu hello.
![Zapobieganie przypadkowemu usuwaniu interfejsu użytkownika Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)

Jeśli to nieoczekiwany, badanie i podjąć działania naprawcze. toosee, które obiekty są o usunięciu toobe hello następujące:

1. Uruchom **usługi synchronizacji** z hello Start Menu.
2. Przejdź za**łączniki**.
3. Wybierz hello łącznika z typem **usługi Azure Active Directory**.
4. W obszarze **akcje** toohello prawej strony, wybierz opcję **przestrzeni łącznika wyszukiwania**.
5. W hello wyskakujących w obszarze **zakres**, wybierz pozycję **rozłączona, ponieważ** i wybierz czas w przeszłości hello. Kliknij przycisk **wyszukiwania**. Ta strona zawiera widok wszystkich obiektów o toobe usunięte. Klikając każdego elementu, można uzyskać dodatkowe informacje na temat hello obiektu. Możesz również kliknąć **ustawienie kolumny** tooadd dodatkowe atrybuty toobe widocznych w siatce hello.

![Obszar łączników wyszukiwania](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/searchcs.png)

W razie potrzeby wszystkie usuwa hello są następnie hello następujące:

1. tooretrieve hello bieżący próg usuwania, uruchom polecenie cmdlet programu PowerShell hello `Get-ADSyncExportDeletionThreshold`. Podaj nazwę i hasło konta administratora globalnego usługi Azure AD. Witaj, wartość domyślna to 500.
2. tootemporarily wyłączyć tę ochronę i pozwól tych usuwa przejść, uruchom polecenie cmdlet programu PowerShell hello: `Disable-ADSyncExportDeletionThreshold`. Podaj nazwę i hasło konta administratora globalnego usługi Azure AD.
   ![Poświadczenia](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)
3. Z hello Azure łącznika usługi Active Directory nadal wybrana, wybierz akcję hello **Uruchom** i wybierz **wyeksportować**.
4. Włącz toore hello ochrony, należy uruchomić polecenie cmdlet programu PowerShell hello: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`. Zastąp wartość hello zauważyć podczas pobierania hello bieżący próg usuwania 500. Podaj nazwę i hasło konta administratora globalnego usługi Azure AD.

## <a name="next-steps"></a>Następne kroki
**Tematy poglądowe**

* [Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji](active-directory-aadconnectsync-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
