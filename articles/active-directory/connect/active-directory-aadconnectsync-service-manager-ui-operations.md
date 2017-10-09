---
title: "Operacje Menedżera usługi synchronizacji programu Azure AD Connect | Dokumentacja firmy Microsoft"
description: "Zrozumienie karcie operacje hello hello Menedżera usługi synchronizacji programu Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: decbc53613d456a71cd116c40c5e1fd761efd4af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-sync-service-manager-operations-tab"></a>Przy użyciu hello kartę działania Menedżera usługi synchronizacji

![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

Hello operacji karcie są wyświetlane wyniki hello hello ostatniej operacji. Na tej karcie jest toounderstand klucza i rozwiązywania problemów.

## <a name="understand-hello-information-visible-in-hello-operations-tab"></a>Zrozumienie hello informacji widocznych na karcie operacje hello
Witaj górnej połowie zawiera wszystkie elementy w kolejności chronologicznej. Domyślnie dziennik operacji hello przechowuje informacje o hello ostatnich siedmiu dni, ale ustawienie to można zmienić z hello [harmonogramu](active-directory-aadconnectsync-feature-scheduler.md). Ma toolook dla dowolnego przebiegu pokazywać stanu Powodzenie. Można zmienić sortowania, klikając nagłówki hello hello.

Witaj **stan** kolumny jest hello najważniejsze informacje i pokazuje hello najbardziej poważny problem dla przebiegu. Oto krótkie podsumowanie stanów najczęściej hello w kolejności priorytetu tooinvestigate (gdzie * wskazać ciągi możliwy błąd kilka).

| Stan | Komentarz |
| --- | --- |
| Zatrzymano-* |Nie można ukończyć powitalnych Uruchom. Na przykład jeśli hello systemu zdalnego nie działa i nie można skontaktować się z. |
| Zatrzymano-— limit błędów |Wystąpiły błędy więcej niż 5000. Witaj, Uruchom automatycznie zostało zatrzymane powodu toohello dużej liczby błędów. |
| Ukończono -\*— błędy |Zakończono uruchomienie Hello, ale wystąpiły błędy (mniej niż 5000), które należy zbadać. |
| Ukończono -\*— ostrzeżenia |Uruchom Hello ukończone, ale niektóre dane nie jest w stanie hello oczekiwano. Jeśli masz błędy, następnie ten komunikat jest zwykle tylko objawem. Dopóki usunąć błędy, nie powinien być sprawdzony ostrzeżenia. |
| powodzenie |Brak problemów. |

Po zaznaczeniu wiersza dolnej hello aktualizuje tooshow szczegóły hello uruchomienia. Maks z dołu hello toohello, może mieć listy informacją o tym **krok nr**. Ta lista jest wyświetlana tylko, jeśli masz wiele domen w lesie gdzie każdej domeny jest reprezentowany przez krok. Nazwa domeny Hello można znaleźć pozycji hello **partycji**. W obszarze **statystyki synchronizacji**, można znaleźć więcej informacji na temat hello liczbę zmian, które zostały przetworzone. Możesz kliknąć hello łącza tooget listę obiektów hello zmienione. Jeśli masz obiektów z błędami, te błędy są wyświetlane w oknie **błędy synchronizacji**.

Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z obiektu, który nie jest synchronizowanie](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.

Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
