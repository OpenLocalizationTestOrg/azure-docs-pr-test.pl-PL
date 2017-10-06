---
title: "Synchronizacja programu Azure AD Connect: LargeObject obsługi błędów spowodowanych przez atrybut certyfikatu użytkownika | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera kroki korygujące hello LargeObject błędy spowodowane przez atrybut certyfikatu użytkownika."
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 146ad5b3-74d9-4a83-b9e8-0973a19828d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e547fb5f601b92f6f5154de9997651b1f28c51b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-handling-largeobject-errors-caused-by-usercertificate-attribute"></a>Synchronizacja programu Azure AD Connect: LargeObject obsługi błędów spowodowanych przez atrybut certyfikatu użytkownika

Usługi Azure AD wymusza maksymalny limit **15** certyfikatu wartości na powitania **userCertificate** atrybutu. Jeśli usługa Azure AD Connect eksportuje obiektu z więcej niż 15 tooAzure wartości AD, Azure AD zwraca **LargeObject** błędu z komunikatem:

>*"obiekt elastycznie hello jest zbyt duży. Przytnij hello liczbę wartości atrybutów dla tego obiektu. Witaj operacja zostanie ponowiona w hello następnego cyklu synchronizacji..."*

Witaj LargeObject błąd może być spowodowane przez inne atrybuty AD. w rzeczywistości jest spowodowany przez atrybut certyfikatu użytkownika hello tooconfirm, należy tooverify względem obiektu hello w lokalnej usłudze AD lub w hello [wyszukiwanie Metaverse Menedżera usługi synchronizacji](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-mvsearch).

tooobtain hello listę obiektów w dzierżawie LargeObject błędów, użyj jednej z hello następujące metody:

 * Po włączeniu dzierżawy dla usługi Azure AD Connect Health dla synchronizacji mogą odwoływać się toohello [raport o błędzie synchronizacji](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health-sync#object-level-synchronization-error-report-preview) podane.
 
 * Hello powiadomienia e-mail dla błędów synchronizacji katalogu wysyłany na końcu hello cyklu synchronizacji ma hello listy obiektów z błędami LargeObject. 
 * Witaj [kartę operacje Menedżera usługi synchronizacji](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-operations) Wyświetla hello listy obiektów z błędami LargeObject kliknięcie hello najnowsze operacji tooAzure AD eksportowania.
 
## <a name="mitigation-options"></a>Środki zaradcze opcje
Do momentu rozwiązania hello LargeObject błąd toohello zmiany atrybutu, inne tego samego obiektu nie może być eksportowane tooAzure AD. Błąd hello tooresolve, można rozważyć hello następujące opcje:

 * Uaktualnij Azure AD Connect toobuild 1.1.524.0 lub po. W programie Azure AD Connect kompilacji 1.1.524.0, reguły synchronizacji out-of-box hello zostały zaktualizowane toonot eksportu atrybutów userCertificate i userSMIMECertificate Jeśli hello atrybutów ma więcej niż 15 wartości. Aby uzyskać więcej informacji na temat tooupgrade Azure AD Connect, zobacz tooarticle [Azure AD Connect: uaktualnianie z poprzedniej wersji toohello najnowszych](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version).

 * Implementowanie **reguła synchronizacji ruchu wychodzącego** w programie Azure AD Connect, które eksportuje **wartość zamiast hello rzeczywiste wartości dla obiektów z więcej niż 15 certyfikatu wartości null**. Ta opcja jest odpowiednia, jeśli nie wymagają żadnego hello certyfikatu wartości toobe wyeksportowane tooAzure AD dla obiektów z wartościami więcej niż 15. Aby uzyskać więcej informacji na temat tooimplement reguły tej synchronizacji, można znaleźć w sekcji toonext [Implementowanie synchronizacji reguły toolimit eksportu certyfikatu użytkownika atrybutu](#implementing-sync-rule-to-limit-export-of-usercertificate-attribute).

 * Zmniejsz liczbę hello wartości certyfikatu na powitania lokalnymi obiektu usługi Active Directory (co najwyżej 15) przez usunięcie wartości, które nie są już używane przez Twoją organizację. Jest to odpowiednie, jeśli rozrostu atrybutu hello jest spowodowany przez certyfikaty wygasły lub nieużywane. Można użyć hello [dostępne tutaj skrypt programu PowerShell](https://gallery.technet.microsoft.com/Remove-Expired-Certificates-0517e34f) toohelp Znajdź kopię zapasową i Usuń wygasłe certyfikaty w lokalnej usługi AD. Przed usunięciem hello certyfikaty, zalecane jest, sprawdź z administratorami infrastruktury w przypadku klucza publicznego hello w Twojej organizacji.

 * Konfigurowanie usługi Azure AD Connect tooexclude hello certyfikatu użytkownika atrybut przed wyeksportowane tooAzure AD. Ogólnie rzecz biorąc zaleca się tę opcję, ponieważ atrybut hello mogą być używane przez określonych scenariuszy tooenable usług Microsoft Online Services. W szczególności:
    * Hello atrybutu certyfikatu użytkownika w obiekcie użytkownika hello jest używany przez usługi Exchange Online i klientów programu Outlook komunikat podpisywania i szyfrowania. toolearn więcej informacji na temat tej funkcji można znaleźć tooarticle [S/MIME komunikatu podpisywania i szyfrowania](https://technet.microsoft.com/library/dn626158(v=exchg.150).aspx).

    * Witaj atrybutu certyfikatu użytkownika na obiekcie komputera hello jest używany przez usługi Azure AD tooallow systemu Windows 10 lokalnej urządzenia przyłączone do domeny tooconnect tooAzure AD. toolearn więcej informacji na temat tej funkcji można znaleźć tooarticle [połączyć tooAzure urządzeń przyłączonych do domeny AD dla systemu Windows 10 napotyka](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy).

## <a name="implementing-sync-rule-toolimit-export-of-usercertificate-attribute"></a>Implementowanie synchronizacji reguły toolimit eksportu certyfikatu użytkownika atrybutu
Błąd LargeObject hello tooresolve spowodowane hello atrybutu certyfikatu użytkownika, można zaimplementować regułę synchronizacji ruchu wychodzącego w programie Azure AD Connect, które eksportuje **zamiast hello rzeczywiste wartości dla obiektów z więcej niż 15 certyfikatu wartościwartościnull**. W tej sekcji opisano hello kroki wymagane tooimplement hello reguły synchronizacji dla **użytkownika** obiektów. Witaj kroki mogą być dostosowywane do **skontaktuj się z** i **komputera** obiektów.

> [!IMPORTANT]
> Eksportowanie wartości null powoduje usunięcie certyfikatów wartości wcześniej wyeksportowany pomyślnie tooAzure AD.

Podsumowanie czynności Hello jako:

1. Wyłączanie harmonogramu synchronizacji i sprawdź, że nie ma synchronizacji w toku.
3. Znajdź hello istniejącą regułę synchronizacji ruchu wychodzącego dla atrybutu certyfikatu użytkownika.
4. Utwórz regułę synchronizacji ruchu wychodzącego hello wymagane.
5. Sprawdź hello nową regułę synchronizacji do istniejącego obiektu z powodu błędu LargeObject.
6. Zastosuj hello nowych synchronizacji reguły tooremaining obiektów z powodu błędu LargeObject.
7. Sprawdź, nie wprowadzono żadnych zmian nieoczekiwany oczekiwania tooAzure toobe wyeksportowane AD.
8. Wyeksportuj hello zmiany tooAzure AD.
9. Włącz ponownie harmonogram synchronizacji.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>Krok 1. Wyłączanie harmonogramu synchronizacji i sprawdź, że nie ma synchronizacji w toku
Upewnij się, synchronizacja nie ma miejsce podczas pracy w środku hello Implementowanie synchronizacji nowe reguły tooavoid niezamierzone zmiany jest wyeksportowany tooAzure AD. Harmonogram synchronizacji wbudowanych hello toodisable:
1. Uruchom sesję programu PowerShell na powitania serwera Azure AD Connect.

2. Wyłącz zaplanowanej synchronizacji, uruchamiając polecenie cmdlet:`Set-ADSyncScheduler -SyncCycleEnabled $false`

> [!Note]
> Hello powyższych kroków są tylko odpowiednie toonewer wersje (1.1.xxx.x) programu Azure AD Connect z hello wbudowanych harmonogramu. Jeśli używasz starszej wersji (1.0.xxx.x) programu Azure AD Connect, która używa harmonogramu zadań systemu Windows lub korzystasz z własnego harmonogramu niestandardowego (nie wspólnej) tootrigger okresową synchronizację, należy toodisable je odpowiednio.

3. Uruchom hello **Menedżera usługi synchronizacji** przez przejście → tooSTART usługi synchronizacji.

4. Przejdź toohello **operacji** karcie i upewnij się, Brak operacji ze stanem *"w"toku.*

### <a name="step-2-find-hello-existing-outbound-sync-rule-for-usercertificate-attribute"></a>Krok 2. Znajdź hello istniejącą regułę synchronizacji ruchu wychodzącego dla atrybutu certyfikatu użytkownika
Powinien być istniejącą regułę synchronizacji, który jest włączona i skonfigurowana atrybutu userCertificate tooexport tooAzure obiekty użytkownika AD. Zlokalizuj tego toofind reguły synchronizacji limit jego **pierwszeństwo** i **zakresu filtru** konfiguracji:

1. Uruchom hello **Edytor reguł synchronizacji** przez przejście → tooSTART synchronizacji zasady edytora.

2. Skonfigurować filtry wyszukiwania hello hello następujące wartości:

    | Atrybut | Wartość |
    | --- | --- |
    | Kierunek |**Wychodzące** |
    | Typ obiektu MV |**Osoby** |
    | Łącznik |*Nazwa łącznika usługi Azure AD* |
    | Typ obiektu łącznika |**użytkownika** |
    | Atrybut MV |**certyfikatu użytkownika** |

3. Jeśli używasz OOB (out-of-box) synchronizacji reguły tooAzure AD connector tooexport userCertficiate atrybutu obiektów użytkownika, powinny zostać wyświetlone powitalne *"limit tooAAD — ExchangeOnline użytkownika"* reguły.
4. Zanotuj hello **pierwszeństwo** wartość ta reguła synchronizacji.
5. Wybierz regułę synchronizacji hello, a następnie kliknij przycisk **Edytuj**.
6. W hello *"Edytuj zastrzeżone potwierdzenie reguły"* podręczne okno dialogowe, kliknij przycisk **nr**. (Nie martw się, nie zamierzamy toomake reguły synchronizacji toothis zmiany).
7. Na ekranie powitania edycji wybierz hello **filtru Scoping** kartę.
8. Należy zanotować hello zakresu filtru konfiguracji. Jeśli używasz reguły synchronizacji OOB hello dokładnie należy **jedną grupę ustalania zakresu filtru zawierające dwie klauzule**, takie jak:

    | Atrybut | Operator | Wartość |
    | --- | --- | --- |
    | sourceObjectType | RÓWNOŚCI | Użytkownik |
    | cloudMastered | NOTEQUAL | True |

### <a name="step-3-create-hello-outbound-sync-rule-required"></a>Krok 3. Utwórz regułę synchronizacji ruchu wychodzącego hello wymagane
Witaj nową regułę synchronizacji musi mieć hello sam **zakresu filtru** i **wyższy priorytet** niż hello istniejącą regułę synchronizacji. Dzięki temu tego hello Nowa reguła synchronizacji ma zastosowanie toohello sam zestaw obiektów jako hello istniejącą regułę synchronizacji i zastąpienia hello istniejącej synchronizacji reguły hello atrybutu certyfikatu użytkownika. Reguła synchronizacji hello toocreate:
1. W hello Edytor reguł synchronizacji, kliknij przycisk hello **Dodaj nową regułę** przycisku.
2. W obszarze hello **kartę opis**, podaj hello następującej konfiguracji:

    | Atrybut | Wartość | Szczegóły |
    | --- | --- | --- |
    | Nazwa | *Podaj nazwę* | Np. *"Out tooAAD — niestandardowy zastąpienie dla certyfikatu użytkownika"* |
    | Opis | *Podaj opis* | Np. *"Jeśli certyfikatu użytkownika atrybut ma więcej niż 15 wartości, wyeksportuj NULL".* |
    | System połączony | *Wybierz hello łącznika usługi Azure AD* |
    | Połączony System typu obiektu | **użytkownika** | |
    | Typ obiektu Metaverse | **osoby** | |
    | Typ łącza | **Dołącz** | |
    | Priorytet | *Wybierz liczbę z zakresu od 1 do 99* | Witaj liczba wybrana nie mogą być używane przez żadną istniejącą regułę synchronizacji i ma mniejszą wartość (i w związku z tym wyższy priorytet) niż hello istniejącą regułę synchronizacji. |

3. Przejdź toohello **filtru Scoping** karcie i wdrożenie hello używa tego samego zakresu filtru hello istniejącej synchronizacji reguły.
4. Pomiń hello **dołączyć reguły** kartę.
5. Przejdź toohello **przekształcenia** karcie tooadd nowego transformacji przy użyciu następujących konfiguracji:

    | Atrybut | Wartość |
    | --- | --- |
    | Typ przepływu |**Wyrażenie** |
    | Atrybut TARGET |**certyfikatu użytkownika** |
    | Atrybut źródłowy |*Użyj powitania po wyrażeniu*:`IIF(IsNullOrEmpty([userCertificate]), NULL, IIF((Count([userCertificate])> 15),AuthoritativeNull,[userCertificate]))` |
    
6. Kliknij przycisk hello **Dodaj** reguły synchronizacji hello toocreate przycisku.

### <a name="step-4-verify-hello-new-sync-rule-on-an-existing-object-with-largeobject-error"></a>Krok 4. Sprawdź hello nową regułę synchronizacji do istniejącego obiektu z powodu błędu LargeObject
Jest to tooverify, który hello synchronizacji Reguła utworzona działa poprawnie na istniejącego obiektu AD z powodu błędu LargeObject przed zastosowaniem tooother obiektów:
1. Przejdź toohello **operacji** kartę w hello Synchronization Service Manager.
2. Wybierz hello ostatniej operacji tooAzure AD eksportowania i kliknij jeden z obiektów hello LargeObject błędów.
3.  Witaj właściwości obiektu obszaru łącznika wyskakujących ekranie kliknij na powitania **Podgląd** przycisku.
4. Na powitania Podgląd podręcznym wybierz opcję **pełnej synchronizacji** i kliknij przycisk **zatwierdzić Podgląd**.
5. Zamknij hello podgląd ekranu i hello właściwości obiektu obszaru łącznika ekranu.
6. Przejdź toohello **łączniki** kartę w hello Synchronization Service Manager.
7. Kliknij prawym przyciskiem myszy na powitania **usługi Azure AD** łącznik i wybierz **Uruchom...**
8. W oknie podręcznym uruchomić łącznik hello wybierz **wyeksportować** kroku i kliknij przycisk **OK**.
9. Poczekaj toocomplete tooAzure AD eksportowania i upewnij się, że nie było więcej LargeObject błędu tego określonego obiektu.

### <a name="step-5-apply-hello-new-sync-rule-tooremaining-objects-with-largeobject-error"></a>Krok 5. Zastosuj hello nowych synchronizacji reguły tooremaining obiektów z powodu błędu LargeObject
Po dodaniu reguły synchronizacji hello należy toorun krok pełnej synchronizacji na powitania łączniku usługi AD:
1. Przejdź toohello **łączniki** kartę w hello Synchronization Service Manager.
2. Kliknij prawym przyciskiem myszy na powitania **AD** łącznik i wybierz **Uruchom...**
3. W oknie podręcznym uruchomić łącznik hello wybierz **pełną synchronizację** kroku i kliknij przycisk **OK**.
4. Poczekaj, aż toocomplete kroku Pełna synchronizacja hello.
5. Powtórz hello powyżej kroki dla hello pozostałych łączniki AD, jeśli masz więcej niż jeden AD łączników. Wiele łączników są zazwyczaj wymagane, jeśli masz wiele katalogów lokalnych.

### <a name="step-6-verify-there-are-no-unexpected-changes-waiting-toobe-exported-tooazure-ad"></a>Krok 6. Sprawdź nie wprowadzono żadnych zmian nieoczekiwany oczekiwania tooAzure toobe wyeksportowane AD
1. Przejdź toohello **łączniki** kartę w hello Synchronization Service Manager.
2. Kliknij prawym przyciskiem myszy na powitania **usługi Azure AD** łącznik i wybierz **przestrzeni łącznika wyszukiwania**.
3. W oknie podręcznym przestrzeni łącznika wyszukiwania hello:
    1. Ustaw zakres zbyt**wyeksportować oczekujące**.
    2. Sprawdź wszystkie 3 pola wyboru, w tym **Dodaj**, **Modyfikuj** i **usunąć**.
    3. Kliknij przycisk **wyszukiwania** tooreturn przycisk wszystkie obiekty z zmian oczekujących tooAzure toobe wyeksportowane AD.
    4. Sprawdź, czy nie ma żadnych zmian nieoczekiwany. zmiany hello tooexamine dla danego obiektu, kliknij dwukrotnie hello obiektu.

### <a name="step-7-export-hello-changes-tooazure-ad"></a>Krok 7. Eksportuj hello zmiany tooAzure AD
tooexport hello zmiany tooAzure AD:
1. Przejdź toohello **łączniki** kartę w hello Synchronization Service Manager.
2. Kliknij prawym przyciskiem myszy na powitania **usługi Azure AD** łącznik i wybierz **Uruchom...**
4. W oknie podręcznym uruchomić łącznik hello wybierz **wyeksportować** kroku i kliknij przycisk **OK**.
5. Poczekaj, aż toocomplete tooAzure AD eksportowania i upewnij się, że nie ma żadnych błędów więcej LargeObject.

### <a name="step-8-re-enable-sync-scheduler"></a>Krok 8. Włącz ponownie harmonogram synchronizacji
Teraz, gdy hello problem zostanie rozwiązany, należy ponownie włączyć harmonogramu synchronizacji wbudowanych hello:
1. Uruchom sesję programu PowerShell.
2. Ponownie włączyć zaplanowanej synchronizacji, uruchamiając polecenie cmdlet:`Set-ADSyncScheduler -SyncCycleEnabled $true`

> [!Note]
> Hello powyższych kroków są tylko odpowiednie toonewer wersje (1.1.xxx.x) programu Azure AD Connect z hello wbudowanych harmonogramu. Jeśli używasz starszej wersji (1.0.xxx.x) programu Azure AD Connect, która używa harmonogramu zadań systemu Windows lub korzystasz z własnego harmonogramu niestandardowego (nie wspólnej) tootrigger okresową synchronizację, należy toodisable je odpowiednio.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

