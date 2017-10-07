---
title: "aaaConnectors w hello interfejsu użytkownika programu Azure AD Synchronization Service Manager | Dokumentacja firmy Microsoft"
description: "Zrozumienie hello kartę łączników w hello Menedżera usługi synchronizacji programu Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a>Za pomocą łączników o hello Azure AD Connect synchronizacji programu Service Manager

![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

Karta łączniki Hello jest używany toomanage, wszystkie aparatu synchronizacji hello systemów jest połączona z.

## <a name="connector-actions"></a>Akcje łącznika
| Akcja | Komentarz |
| --- | --- |
| Przycisk Utwórz |Nie używaj. Połączenie tooadditional AD lasów, należy użyć Kreatora instalacji hello. |
| Właściwości |Używany do domeny i jednostki Organizacyjnej filtrowania. |
| [Usuwanie](#delete) |Używane tooeither usunąć dane hello hello łącznika miejsca lub toodelete połączenia tooa lasu. |
| [Konfigurowanie profilów uruchamiania](#configure-run-profiles) |Z wyjątkiem domeny filtrowania nic tooconfigure tutaj. Akcję tę można stosować profilów uruchamiania toosee już skonfigurowane. |
| Uruchom polecenie |Używane toostart jednorazowy Uruchom profilu. |
| Stop |Zatrzymuje łącznika aktualnie uruchomione profilu. |
| Łącznik eksportu |Nie używaj. |
| Importuj łącznika |Nie używaj. |
| Łącznik aktualizacji |Nie używaj. |
| Odśwież schemat |Odświeża hello pamięci podręcznej schematu. Jest toouse preferowanych opcji powitania w Kreatorze instalacji hello zamiast tego należy również od który aktualizacje synchronizacji reguły. |
| [Obszar łączników wyszukiwania](#search-connector-space) |Obiekty toofind używane i zbyt[wykonaj obiekt i jego danych za pośrednictwem systemu hello](#follow-an-object-and-its-data-through-the-system). |

### <a name="delete"></a>Usuwanie
Akcja usuwania Hello jest używany dla dwóch różnych rzeczy.  
![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

Witaj opcja **usunąć tylko przestrzeni łącznika** powoduje usunięcie wszystkich danych, ale zachować hello konfiguracja.

Witaj opcja **usunąć Connector i łącznika miejsca** usuwa hello danych i konfiguracji hello. Ta opcja jest używana, gdy tooconnect tooa lasu nie mają już.

Obie te opcje synchronizować wszystkie obiekty i zaktualizować hello metaverse obiektów. Ta akcja jest operacją wymagającą dużo czasu.

### <a name="configure-run-profiles"></a>Konfigurowanie profilów uruchamiania
Ta opcja umożliwia hello toosee skonfigurowane dla łącznika profilów uruchamiania.

![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a>Obszar łączników wyszukiwania
Akcja przestrzeni łącznika wyszukiwania Hello jest przydatne toofind obiektów i rozwiązywania problemów danych.

![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

Najpierw wybrać **zakres**. Można wyszukiwać na podstawie danych (RDN, nazwa Wyróżniająca, zakotwiczenia, poddrzewa), lub stanu obiektu hello (wszystkie inne opcje).  
![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)  
Jeśli na przykład wykonać wyszukiwanie poddrzewa, możesz uzyskać wszystkie obiekty w jednej jednostce Organizacyjnej.  
![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)  
W tym miejscu. Wybierz obiekt, wybierz **właściwości**, i [po nim](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) z hello źródła łącznika, za pośrednictwem hello metaverse i toohello docelowych łącznika miejsca.

### <a name="changing-hello-ad-ds-account-password"></a>Zmiana hasła konta hello AD DS
Jeśli zmienisz hasło konta hello hello usługi synchronizacji nie będą już mogli tooimport/export zmiany tooon lokalnych AD.   Może pojawić się następujące hello:

- krok importu/eksportu Hello na powitania łącznika AD zakończy się niepowodzeniem z powodu błędu "nie-start — poświadczenia".
- W Podglądzie zdarzeń systemu Windows w dzienniku zdarzeń aplikacji hello zawiera błąd 6000 identyfikator zdarzenia i komunikat "hello zarządzania toorun agenta"contoso.com"nie powiodło się, ponieważ poświadczenia hello była nieprawidłowa."

tooresolve hello wystawiania, konto użytkownika hello usług AD DS aktualizacji przy użyciu następujących hello:


1. Uruchom hello Synchronization Service Manager (START → usługa synchronizacji).
</br>![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)
2. Przejdź toohello **łączniki** kartę.
3. Wybierz hello łączniku usługi AD, który jest skonfigurowany toouse hello konta usług AD DS.
4. W obszarze akcje, wybierz **właściwości**.
5. W wyskakującym oknie dialogowym hello wybierz opcję Połącz tooActive katalogu lasu:
6. Nazwa lasu Hello wskazuje hello odpowiedniej lokalnej usługi AD.
7. Nazwa użytkownika Hello wskazuje hello AD DS konto używane do synchronizacji.
8. Wprowadź nowe hasło hello hello AD DS konta w pole tekstowe hasła hello ![Azure AD Connect synchronizacji szyfrowania klucz narzędzia](media/active-directory-aadconnectsync-encryption-key/key6.png)
9. Kliknij przycisk OK toosave hello nowe hasło, a następnie ponownie uruchom hello usługi synchronizacji tooremove hello stare hasło z pamięci podręcznej.



## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.

Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
