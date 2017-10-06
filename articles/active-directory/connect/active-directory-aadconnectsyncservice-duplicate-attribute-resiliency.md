---
title: "aaaIdentity synchronizacji i zduplikowany atrybut odporności | Dokumentacja firmy Microsoft"
description: "Nowe zachowanie jak toohandle obiekty z nazwy UPN lub ProxyAddress konflikty podczas synchronizacji katalogów za pomocą usługi Azure AD Connect."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 537a92b7-7a84-4c89-88b0-9bce0eacd931
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.openlocfilehash: e27dcbf9d71f83fa9566cae2fd99350297d1cd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="identity-synchronization-and-duplicate-attribute-resiliency"></a>Synchronizacja tożsamości i odporność względem zduplikowanych atrybutów
Zduplikowany atrybut odporności to funkcja usługi Azure Active Directory, która wyeliminuje tarcie spowodowane **UserPrincipalName** i **ProxyAddress** powoduje konflikt podczas uruchamiania narzędzi synchronizacji firmy Microsoft.

Te atrybuty są zwykle wymagane toobe unikatowy we wszystkich **użytkownika**, **grupy**, lub **skontaktuj się z** obiektów w danej dzierżawy usługi Azure Active Directory.

> [!NOTE]
> Tylko użytkownicy mają nazwy UPN.
> 
> 

nowe zachowanie Hello, że ta funkcja umożliwia hello chmury część hello procesu synchronizacji, w związku z tym jest klient niezależny i zastosowanie w przypadku każdego produktu synchronizacji firmy Microsoft, w tym Azure AD Connect, narzędzia DirSync i MIM + łącznika. ogólny termin Hello "client synchronizacji" jest używany w toorepresent tego dokumentu, jednego z tych produktów.

## <a name="current-behavior"></a>Aktualny efekt
W przypadku próby tooprovision nowy obiekt z wartością nazwy UPN lub ProxyAddress, który narusza ograniczenie unikatowości. ta, Azure Active Directory blokuje ten obiekt, utworzenie. Podobnie jeśli nazwy UPN lub ProxyAddress nieunikatowy jest aktualizowany obiekt, hello aktualizacji nie powiedzie się. Hello inicjowania obsługi administracyjnej próba lub aktualizacji próba zostanie ponowiona przez klienta synchronizacji hello na każdy cykl eksportowania i kontynuuje toofail, dopóki hello konflikt nie zostanie rozwiązany. Błąd e-mail raport jest generowany po każdej próbie i jest rejestrowany błąd przez powitania klienta synchronizacji.

## <a name="behavior-with-duplicate-attribute-resiliency"></a>Zachowanie w przypadku odporności zduplikowany atrybut
Zamiast całkowicie niepowodzeniem tooprovision lub zaktualizowania obiektu z atrybutem zduplikowane usługi Azure Active Directory "poddaje kwarantannie" hello zduplikowany atrybut, który mógłby naruszyć hello ograniczenie unikatowości. Jeśli ten atrybut jest wymagany do inicjowania obsługi, takie jak UserPrincipalName, usługa hello przypisuje wartość symbolu zastępczego. format Hello tych wartości tymczasowej  
"***<OriginalPrefix>+ < 4DigitNumber > @<InitialTenantDomain>. onmicrosoft.com***".  
Jeśli atrybut hello nie jest wymagane, takich jak **ProxyAddress**, po prostu poddaje kwarantannie atrybutu konflikt hello Azure Active Directory i kontynuuje tworzenie obiektów hello lub aktualizacji.

Po poddawania atrybutu hello, informacje o konflikt hello są wysyłane w hello sam błąd raport e-mail używany w zachowaniu starych hello. Te informacje jest wyświetlany tylko w raporcie o błędach hello jeden raz, w przypadku hello kwarantanny nie nadal toobe zarejestrowanych w przyszłości wiadomości e-mail. Ponadto ponieważ hello eksportu dla tego obiektu zakończyła się pomyślnie, powitania klienta synchronizacji nie rejestruje błąd i spełnia nie hello ponów próbę utworzenia / operacja przy kolejnej synchronizacji cykli aktualizacji.

toosupport to zachowanie nowy atrybut zostało dodane toohello użytkowników, grup i skontaktuj się z obiektu klasy:  
**DirSyncProvisioningErrors**

Jest to wielokrotne wartości atrybutu, który jest używany toostore hello powodujące konflikt atrybutów, które naruszyłoby ograniczenie unikatowości hello powinny one zostać dodane normalnie. Zadanie czasomierza w tle została włączona w usłudze Azure Active Directory z systemem toolook co godzinę dla zduplikowany atrybut konfliktów, które zostały rozwiązane i automatycznie usuwa atrybuty hello z kwarantanny.

### <a name="enabling-duplicate-attribute-resiliency"></a>Włączaniu odporności zduplikowany atrybut
Zduplikowany atrybut odporności będzie hello nowe zachowanie we wszystkich dzierżaw usługi Azure Active Directory. Na będzie domyślnie dla wszystkich dzierżawców, które włączony synchronizacja powitania po raz pierwszy 22 sierpnia 2016 lub nowszy. Dzierżawcy włączone synchronizacji wcześniejszych toothis data ma hello funkcja jest włączona w partiach. Wdrożenia rozpocznie się we wrześniu 2016 r i poczty e-mail zostanie wysłane powiadomienie tooeach dzierżawy techniczne powiadomień kontakt z określonej daty hello, gdy funkcja hello zostanie włączona.

> [!NOTE]
> Gdy włączono zduplikowany atrybut odporności nie można wyłączyć.

toocheck, jeśli funkcja hello jest włączona dla Twojej dzierżawy, możesz to zrobić przez pobranie najnowszej wersji hello hello modułu programu PowerShell usługi Azure Active Directory i systemem:

`Get-MsolDirSyncFeatures -Feature DuplicateUPNResiliency`

`Get-MsolDirSyncFeatures -Feature DuplicateProxyAddressResiliency`

> [!NOTE]
> Nie jest już funkcja MsolDirSyncFeature zestaw polecenia cmdlet tooproactively Włącz hello zduplikowany atrybut odporności przed jest włączona dla Twojej dzierżawy. Funkcja hello stanie tootest toobe, konieczne będzie toocreate nową dzierżawę usługi Azure Active Directory.

## <a name="identifying-objects-with-dirsyncprovisioningerrors"></a>Identyfikowania obiektów z DirSyncProvisioningErrors
Są obecnie dwie metody tooidentify obiektów, które mają błędy te konflikty właściwości tooduplicate, programu PowerShell usługi Azure Active Directory i hello portalu administratora usługi Office 365. Brak planów tooextend tooadditional portalu na podstawie raportowania w programie hello w przyszłości.

### <a name="azure-active-directory-powershell"></a>Azure Active Directory PowerShell
Hello poleceń cmdlet programu PowerShell w tym temacie, aby uzyskać następujące hello jest spełnionych:

* Wszystkie hello następującego polecenia cmdlet jest uwzględniana wielkość liter.
* Witaj **— ErrorCategory PropertyConflict** zawsze musi być uwzględniony. Nie ma obecnie żadnych innych typów, z **ErrorCategory**, ale może to zostać rozszerzona w przyszłości hello.

Po pierwsze, Rozpoczynanie pracy przez uruchomienie **Connect MsolService** i wprowadzić poświadczenia administratora dzierżawy.

Następnie należy użyć hello następujące polecenia cmdlet i operatory błędy tooview na różne sposoby:

1. [Wyświetl wszystkie](#see-all)
2. [Według typu właściwości](#by-property-type)
3. [Wartości powodujące konflikt](#by-conflicting-value)
4. [Za pomocą wyszukiwania ciągu](#using-a-string-search)
5. [Sortowane](#sorted)
6. [Ograniczona ilość lub wszystkie](#in-a-limited-quantity-or-all)

#### <a name="see-all"></a>Zobacz wszystkie
Po nawiązaniu połączenia toosee ogólną listę atrybutów inicjowania obsługi błędów w dzierżawie powitalnych Uruchom:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict`

Daje to wynik, podobnie jak poniżej hello:  
 ![Get-MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "Get MsolDirSyncProvisioningError")  

#### <a name="by-property-type"></a>Według typu właściwości
błędy toosee przez typ właściwości, Dodaj hello **- PropertyName** flagę hello **UserPrincipalName** lub **ProxyAddresses** argumentu:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName UserPrincipalName`

Lub

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName ProxyAddresses`

#### <a name="by-conflicting-value"></a>Wartości powodujące konflikt
toosee błędy dotyczące konkretnej właściwości tooa dodać hello **- PropertyValue** flagi (**- PropertyName** musi być również używane podczas dodawania tej flagi):

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyValue User@domain.com -PropertyName UserPrincipalName`

#### <a name="using-a-string-search"></a>Za pomocą wyszukiwania ciągu
toodo wyszukiwania szeroki ciąg Użyj hello **parametru - Wyszukiwany_ciąg** flagi. Może być używany niezależnie od wszystkich hello powyżej flagi, z wyjątkiem hello **- ErrorCategory PropertyConflict**, który jest zawsze wymagane:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -SearchString User`

#### <a name="in-a-limited-quantity-or-all"></a>Ograniczona ilość lub wszystkie
1. **MaxResults <Int>**  mogą być używane toolimit hello zapytania tooa określoną liczbę wartości.
2. **Wszystkie** może być tooensure używanych w przypadku hello, że istnieje dużej liczby błędów pobierane są wszystkie wyniki.

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -MaxResults 5`

## <a name="office-365-admin-portal"></a>Portal administracyjny usługi Office 365
Błędy synchronizacji katalogu można wyświetlić w Centrum administracyjnym usługi Office 365 hello. Witaj raportu w portalu wyświetla tylko hello usługi Office 365 **użytkownika** obiektów, które mają te błędy. Nie są wyświetlane informacje o konfliktach między **grup** i **kontaktów**.

![Aktywni użytkownicy](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "aktywni użytkownicy")

Aby uzyskać instrukcje jak błędy synchronizacji katalogu tooview hello usługi Office 365 admin Centrum, zobacz [zidentyfikować błędy synchronizacji katalogu w usłudze Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067).

### <a name="identity-synchronization-error-report"></a>Raport o błędzie synchronizacji tożsamości
Obiekt z konfliktem zduplikowany atrybut jest obsługiwany z to nowe zachowanie, w których powiadomienie jest uwzględniona w standard hello tożsamości raport o błędzie synchronizacji poczty e-mail, która jest wysyłana toohello powiadomień technicznych skontaktuj się z hello dzierżawcy. Istnieje jednak ważne zmiany w tym zachowaniu. W ciągu ostatnich hello informacje o konflikt zduplikowany atrybut czy uwzględniane w raporcie każdej kolejny błąd, dopóki hello konflikt został rozwiązany. Z to nowe zachowanie hello powiadomienie o błędzie dla danego konfliktu wystąpić tylko raz — w czasie hello atrybutów powodujące konflikt hello jest poddawane kwarantannie.

Oto przykład jakie powiadomienia e-mail hello wygląda konfliktu ProxyAddress:  
    ![Aktywni użytkownicy](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "aktywni użytkownicy")  

## <a name="resolving-conflicts"></a>Rozwiązywanie konfliktów
Rozwiązywanie problemów z taktyk strategii i rozwiązania błędów powinna różnią się od sposób hello w przeszłości hello zostały obsługi błędów zduplikowany atrybut. Hello jedyną różnicą jest przeszukiwanie zadanie czasomierza hello za pomocą dzierżawy hello na powitania po stronie usługi tooautomatically dodawania atrybutu hello w obiekcie prawidłowego toohello zapytania po hello konflikt został rozwiązany.

Witaj artykule przedstawiono różne strategie rozwiązywania problemów i rozwiązania: [zduplikowane lub nieprawidłowe atrybuty zapobieganie synchronizacji katalogów w usłudze Office 365](https://support.microsoft.com/kb/2647098).

## <a name="known-issues"></a>Znane problemy
Żadna z tych znanych problemów powoduje spadek utracie lub usługi danych. Niektóre z nich są estetycznych, inne spowodować standardu "*wstępne odporności*" zduplikowany atrybut toobe błędów zgłoszonych zamiast poddawania hello konflikt atrybutów, a druga spowoduje, że niektóre błędy toorequire bardzo ręcznego konfigurowania.

**Zachowanie rdzeni:**

1. Obiekty z określonym atrybutem konfiguracje nadal tooreceive eksportu błędy jako atrybuty min. toohello zduplikowane kwarantanną.  
   Na przykład:
   
    a. Nowy użytkownik jest tworzony w usłudze AD za pomocą nazwy UPN  **Joe@contoso.com**  i ProxyAddress**smtp:Joe@contoso.com**
   
    b. Witaj właściwości tego obiektu powodują konflikt z istniejącą grupę, gdzie jest ProxyAddress  **SMTP:Joe@contoso.com** .
   
    c. Podczas eksportu **konflikt ProxyAddress** zamiast hello konflikt atrybuty poddane kwarantannie, zostanie zgłoszony błąd. Operacja Hello jest ponowiona po każdym cyklu kolejnej synchronizacji, ponieważ miałoby to miejsce przed włączeniem funkcji ochrony hello.
2. Jeśli są tworzone dwie grupy lokalnej z hello sam adres SMTP, co kończy się niepowodzeniem tooprovision hello pierwszej próbie ze standardowym zduplikowane **ProxyAddress** błędu. Jednak zduplikowaną wartość hello jest prawidłowo kwarantannie na powitania następnego cyklu synchronizacji.

**Raport portalu Office**:

1. Witaj szczegółowy komunikat o błędzie dla dwóch obiektów w zestawie konflikt nazwy UPN jest hello takie same. Oznacza to, że oba miały ich nazwy UPN zmienić / poddane kwarantannie, gdy w rzeczywistości tylko jeden z nich ma wszystkie dane zmienione.
2. Hello szczegółowy komunikat o błędzie dla konflikt nazwy UPN zawiera hello displayName niewłaściwy dla użytkownika, który miał ich nazwy UPN zmienić kwarantannie. Na przykład:
   
    a. **Użytkownik A** synchronizuje pierwszy z **UPN = User@contoso.com** .
   
    b. **Użytkownik B** jest synchronizowany toobe próba się dalej z **UPN = User@contoso.com** .
   
    c. **Użytkownik B** zbyt zmiany nazwy UPN **User1234@contoso.onmicrosoft.com**  i  **User@contoso.com**  dodaniu zbyt**DirSyncProvisioningErrors**.
   
    d. komunikat o błędzie Hello dla **użytkownika B** powinny wskazywać, że **użytkownika A** ma już  **User@contoso.com**  jako nazwy UPN, ale zawiera **użytkownika B** własnych Nazwa wyświetlana.

**Raport o błędzie synchronizacji tożsamości**:

łącze Hello *kroki dotyczące tooresolve ten problem* jest nieprawidłowy:  
    ![Aktywni użytkownicy](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "aktywni użytkownicy")  

Powinny wskazywać zbyt[https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency).

## <a name="see-also"></a>Zobacz też
* [Synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
* [Zidentyfikuj błędy synchronizacji katalogu w usłudze Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)

