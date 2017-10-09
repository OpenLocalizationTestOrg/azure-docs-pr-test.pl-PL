---
title: "obiekt, który nie jest synchronizowanie tooAzure AD aaaTroubleshoot | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z powodu obiektu nie można zsynchronizować tooAzure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 81e0a0793a1d5ec76cfcaec6e974726d7854f58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-object-that-is-not-synchronizing-tooazure-ad"></a>Rozwiązywanie problemów z obiektu, który nie jest synchronizowanie tooAzure AD

Jeśli obiekt nie synchronizuje jako oczekiwanego tooAzure AD, a następnie można go z kilku przyczyn. Jeśli otrzymali wiadomości e-mail błędu z usługi Azure AD, zobacz błąd hello Azure AD Connect Health Odczytaj [Rozwiązywanie problemów z błędami eksportu](active-directory-aadconnect-troubleshoot-sync-errors.md) zamiast tego. Ale jeśli rozwiązywania problemu, w których hello obiektu nie jest w usłudze Azure AD, wówczas w tym temacie jest dla Ciebie. Opisuje sposób synchronizacji toofind błędy w składniku lokalne powitania Azure AD Connect.

błędy hello toofind, ma toolook w kilku różnych miejscach hello w następującej kolejności:

1. Witaj [dzienniki operacji](#operations) do znajdowania zidentyfikowane przez aparat synchronizacji hello podczas importowania i synchronizacji błędy.
2. Witaj [przestrzeni łącznika](#connector-space-object-properties) do znajdowania brakujących obiektów i błędy synchronizacji.
3. Witaj [metaverse](#metaverse-object-properties) do znajdowania problemów związanych z danymi.

Uruchom [Menedżera usługi synchronizacji](active-directory-aadconnectsync-service-manager-ui.md) przed rozpoczęciem tych kroków.

## <a name="operations"></a>Operacje
karcie operacje Hello hello Synchronization Service Manager jest gdzie należy zacząć Rozwiązywanie problemów. Hello operacji karcie są wyświetlane wyniki hello hello ostatniej operacji.  
![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/operations.png)  

Witaj górnej połowie zawiera wszystkie elementy stały. Domyślnie dziennik operacji hello przechowuje informacje o hello ostatnich siedmiu dni, ale ustawienie to można zmienić z hello [harmonogramu](active-directory-aadconnectsync-feature-scheduler.md). Ma toolook dla dowolnego przebiegu pokazywać stanu Powodzenie. Można zmienić sortowania, klikając nagłówki hello hello.

Witaj **stan** kolumny jest hello najważniejsze informacje i pokazuje hello najbardziej poważny problem dla przebiegu. Oto krótkie podsumowanie stanów najczęściej hello w kolejności priorytetu tooinvestigate (gdzie * wskazać ciągi możliwy błąd kilka).

| Stan | Komentarz |
| --- | --- |
| Zatrzymano-* |Nie można ukończyć powitalnych Uruchom. Na przykład jeśli hello systemu zdalnego nie działa i nie można skontaktować się z. |
| Zatrzymano-— limit błędów |Wystąpiły błędy więcej niż 5000. Witaj, Uruchom automatycznie zostało zatrzymane powodu toohello dużej liczby błędów. |
| Ukończono -\*— błędy |Zakończono uruchomienie Hello, ale wystąpiły błędy (mniej niż 5000), które należy zbadać. |
| Ukończono -\*— ostrzeżenia |Uruchom Hello ukończone, ale niektóre dane nie jest w stanie hello oczekiwano. Jeśli masz błędy, następnie ten komunikat jest zwykle tylko objawem. Dopóki usunąć błędy, nie powinien być sprawdzony ostrzeżenia. |
| powodzenie |Brak problemów. |

Po zaznaczeniu wiersza dolnej hello aktualizuje tooshow szczegóły hello uruchomienia. Maks z dołu hello toohello, może mieć listy informacją o tym **krok nr**. Ta lista jest wyświetlana tylko, jeśli masz wiele domen w lesie gdzie każdej domeny jest reprezentowany przez krok. Nazwa domeny Hello można znaleźć pozycji hello **partycji**. W obszarze **statystyki synchronizacji**, można znaleźć więcej informacji na temat hello liczbę zmian, które zostały przetworzone. Możesz kliknąć hello łącza tooget listę obiektów hello zmienione. Jeśli masz obiektów z błędami, te błędy są wyświetlane w oknie **błędy synchronizacji**.

### <a name="troubleshoot-errors-in-operations-tab"></a>Rozwiązywanie problemów na karcie operacje
![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorsync.png)  
W przypadku błędów zarówno obiekt hello błąd i błąd hello, sama są łącza, aby uzyskać więcej informacji.

Start, klikając ciąg błędu hello (**wyzwalane synchronizacji — zasada — błąd — funkcja** w obraz powitania). Najpierw przedstawiono przegląd hello obiektu. toosee hello błędu, kliknij przycisk hello **ślad stosu**. Ślad informacje debugowania poziomu hello błędu.

Kliknąć prawym przyciskiem myszy w hello **informacje stosu wywołań** wybierz **Zaznacz wszystko**, i **kopiowania**. Możesz skopiować hello stosu i przeglądać błąd hello Twojego ulubionego edytora, takiego jak Notatnik.

* Jeśli błąd hello jest z **SyncRulesEngine**, a następnie informacje stosu wywołań hello najpierw zawiera listę wszystkich atrybutów obiektu hello. Przewiń w dół do momentu wyświetlenia pozycji hello **InnerException = >**.  
  ![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorinnerexception.png)  
  wiersz powitania po pokazuje hello błędu. Hello ilustracji powyżej błąd hello jest utworzony niestandardowy Fabrikam reguły synchronizacji.

Jeśli błąd hello, sam nie zapewnia wystarczającą ilość informacji, to toolook czas na powitania samych danych. Można kliknąć łącze hello z identyfikatorem obiektu hello i kontynuować rozwiązywanie problemów z hello [łącznika miejsce obiekt importowany](#cs-import).

## <a name="connector-space-object-properties"></a>Właściwości obiektu obszaru łącznika
Jeśli nie masz żadnych błędy znalezione w hello [operacji](#operations) karcie, a następnie hello następnym krokiem jest obiekt miejsca toofollow hello łącznika usługi Active Directory, toohello metaverse i tooAzure AD. W tej ścieżce powinien znajdować się w przypadku hello problem.

### <a name="search-for-an-object-in-hello-cs"></a>Wyszukiwanie obiektu w hello CS

W **Menedżera usługi synchronizacji**, kliknij przycisk **łączniki**, wybierz hello łącznika usługi Active Directory, a **przestrzeni łącznika wyszukiwania**.

W **zakres**, wybierz pozycję **RDN** (gdy ma toosearch na powitania atrybutu CN) lub **nazwa Wyróżniająca lub zakotwiczenia** (jeśli ma toosearch na atrybut distinguishedName hello). Wprowadź wartość, a następnie kliknij przycisk **wyszukiwania**.  
![Wyszukiwanie w obszarze łączników](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearch.png)  

Jeśli nie znajdziesz obiektu hello szukasz, a następnie może spowodowały odfiltrowanie z [filtrowanie oparte na domenie](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) lub [filtrowanie na podstawie jednostki Organizacyjnej](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Witaj odczytu [skonfigurować filtrowanie](active-directory-aadconnectsync-configure-filtering.md) tooverify temat, który hello filtrowanie jest skonfigurowany zgodnie z oczekiwaniami.

Inne przydatne wyszukiwania jest hello tooselect łącznika usługi Azure AD, w **zakres** wybierz **oczekującego importowania**i wybierz hello **Dodaj** wyboru. To wyszukiwanie zapewnia wszystkie synchronizowane obiekty w usłudze Azure AD, która nie może być skojarzony z obiektem lokalnym.  
![Łącznik miejsce wyszukiwania oddzielony](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearchorphan.png)  
Te obiekty zostały utworzone przez inny aparat synchronizacji lub aparatem synchronizacji z innej konfiguracji filtrowania. Ten widok znajduje się lista **oddzielony** obiektów nie jest już zarządzany. Należy Przejrzyj tę listę i Rozważ usunięcie tych obiektów przy użyciu hello [programu Azure AD PowerShell](http://aka.ms/aadposh) polecenia cmdlet.

### <a name="cs-import"></a>Importuj CS
Po otwarciu obiektu cs istnieje kilka kart u góry hello. Witaj **zaimportować** karcie są wyświetlane dane hello, które są przygotowywane po zaimportowaniu.  
![Obiekt CS](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/csobject.png)    
Witaj **stara wartość** pokazuje, co to jest przechowywane w Connect i hello **nową wartość** co zostały odebrane z systemu źródłowego hello i nie została jeszcze zastosowana. Jeśli występuje błąd w obiekcie hello, zmiany nie są przetwarzane.

**Błąd**  
![Obiekt CS](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssyncerror.png)  
Witaj **błąd synchronizacji** karta jest widoczna, jeśli występuje problem z obiektem hello tylko. Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z błędami synchronizacji](#troubleshoot-errors-in-operations-tab).

### <a name="cs-lineage"></a>Elementy powiązane CS
Karta elementy powiązane Hello przedstawia, jak obiekt miejsca łącznika hello jest powiązane toohello obiektu metaverse. Możesz wyświetlać importowane hello łącznika Ostatnia zmiana hello system połączony i danych toopopulate zasady stosowane w hello metaverse.  
![Elementy powiązane CS](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineage.png)  
W hello **akcji** kolumny widoczny jest jeden **przychodzący** reguły synchronizacji z akcją hello **udostępniania**. Który wskazuje, że tak długo, jak długo ma ten obiekt przestrzeni łącznika, pozostanie hello obiektu metaverse. Jeśli lista hello reguł synchronizacji zamiast tego zawiera reguły synchronizacji w kierunku **wychodzące** i **udostępniania**, wskazuje, czy ten obiekt jest usunięty po usunięciu obiektu metaverse hello.  
![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineageout.png)  
Możesz również sprawdzić w hello **PasswordSync** kolumny, która hello przestrzeni łącznika przychodzących może przyczynić się zmiany toohello hasła, ponieważ jedna reguła synchronizacji ma wartość hello **True**. To hasło zostanie przesłany tooAzure AD za pomocą hello wychodzącą regułę.

Na karcie elementy powiązane hello, możesz uzyskać toohello metaverse klikając [właściwości obiektu Metaverse](#mv-attributes).

U dołu hello wszystkie karty są dwa przyciski: **Podgląd** i **dziennika**.

### <a name="preview"></a>Wersja zapoznawcza
Strona podglądu Hello jest używane toosynchronize jednego pojedynczego obiektu. Jest przydatne, jeśli są Rozwiązywanie problemów z niektórych reguł niestandardowych synchronizacji i chcesz toosee hello wpływ zmian na pojedynczy obiekt. Możesz wybrać między **pełnej synchronizacji** i **synchronizacja różnicowa**. Możesz też wybrać między **Generowanie podglądu**, który przechowuje tylko hello zmiany w pamięci, i **zatwierdzić Podgląd**, który zaktualizowany hello metaverse i etapy wszystkie zmiany tootarget — obszary łączników.  
![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/preview.png)  
Możesz sprawdzić obiekt hello i reguły, które zostały zastosowane do przepływu określonego atrybutu.  
![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/previewresult.png)

### <a name="log"></a>Log
Strona dziennika Hello jest używany toosee hello hasła synchronizacji status i Historia. Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z synchronizacją hasła](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).

## <a name="metaverse-object-properties"></a>Właściwości obiektu Metaverse
Jest zazwyczaj lepiej toostart wyszukiwanie od źródła hello usługi Active Directory [przestrzeni łącznika](#connector-space). Ale można również uruchomić wyszukiwanie od hello metaverse.

### <a name="search-for-an-object-in-hello-mv"></a>Wyszukiwanie obiektu w hello MV
W **Menedżera usługi synchronizacji**, kliknij przycisk **wyszukiwanie Metaverse**. Utwórz zapytanie, należy znać znajduje hello użytkownika. Atrybuty wspólne, takie jak nazwa konta (sAMAccountName) i userPrincipalName można wyszukiwać. Aby uzyskać więcej informacji, zobacz [wyszukiwanie Metaverse](active-directory-aadconnectsync-service-manager-ui-mvsearch.md).
![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvsearch.png)  

W hello **wyniki wyszukiwania** oknie kliknij obiekt hello.

Jeśli nie znalazła obiekt hello, następnie go nie osiągnęła jeszcze hello metaverse. Kontynuować toosearch dla obiekt hello w hello usługi Active Directory [przestrzeni łącznika](#connector-space-object-properties). Może to być błąd z synchronizacji, która blokuje hello obiektu metaverse toohello najbliższych lub może być stosowany filtr.

### <a name="mv-attributes"></a>Atrybuty MV
Na karcie Atrybuty hello można zobaczyć wartości hello i łącznika, które przyczyniły się go.  
![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvobject.png)  

Jeśli obiektu nie można zsynchronizować, przejrzyj następujące atrybuty w magazynie metaverse hello hello:
- Nie jest atrybutem hello **cloudFiltered** stanowią i ustawić także**true**? Jeśli jest, a następnie filtrowane, zgodnie z kroków toohello [na atrybutach filtrowania](active-directory-aadconnectsync-configure-filtering.md#attribute-based-filtering).
- Nie jest atrybutem hello **sourceAnchor** obecny? Jeśli nie masz topologią lasu zasobów konta? Jeśli obiekt jest rozpoznawany jako połączona Skrzynka pocztowa (atrybut hello **msExchRecipientTypeDetails** ma wartość hello 2), hello sourceAnchor jest przekazanych przez las hello z włączonym kontem usługi Active Directory, a następnie. Upewnij się, hello głównego konta został zaimportowany i poprawnie synchronizowane. Witaj głównego konta musi być wymienione w hello [łączniki](#mv-connectors) dla obiekt hello.

### <a name="mv-connectors"></a>Łączniki MV
Witaj łączniki karcie są wyświetlane wszystkie obszary łączników, które ma reprezentacji w postaci obiektu hello.  
![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvconnectors.png)  
Musisz mieć łącznika na:

- Każdy użytkownik hello lasu usługi Active Directory jest reprezentowana w. Taka reprezentacja mogą obejmować foreignSecurityPrincipals i skontaktuj się z pomocą obiektów.
- Łącznik usługi Azure AD.

Braku hello tooAzure łącznika AD należy odczytać [atrybuty MV](#MV-attributes) tooverify hello kryteria są udostępniane tooAzure AD.

Na tej karcie można też toonavigate toohello [obiekt miejsca łącznika](#connector-space-object-properties). Wybierz wiersz i kliknij przycisk **właściwości**.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.

Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
