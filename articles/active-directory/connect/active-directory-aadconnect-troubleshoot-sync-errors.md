---
title: "Azure AD Connect: Rozwiązywanie problemów z błędami podczas synchronizacji | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak tootroubleshoot błędów napotkanych podczas synchronizacji z programem Azure AD Connect."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 2209d5ce-0a64-447b-be3a-6f06d47995f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: af262dfe95d686e34697454c0dfe8b4a6d8693c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-errors-during-synchronization"></a>Rozwiązywanie problemów z błędami podczas synchronizacji
Podczas synchronizowania danych tożsamości z tooAzure Windows Server Active Directory (AD DS) do usługi Active Directory (Azure AD), mogą wystąpić błędy. Ten artykuł zawiera omówienie różnych typów błędów synchronizacji, niektóre hello możliwe scenariusze spowodować tych błędów i potencjalne błędy hello toofix sposobów. Ten artykuł zawiera hello typowych błędów i może nie obejmować wszystkich możliwych błędów hello.

 W tym artykule przyjęto czytnik hello jest zapoznać się z podstawowej hello [projektu usługi Azure AD i Azure AD Connect](active-directory-aadconnect-design-concepts.md).

Witaj najnowszej wersji programu Azure AD Connect \(sierpnia 2016 lub nowszego\), raportu błędów synchronizacji jest dostępna w hello [Azure Portal](https://aka.ms/aadconnecthealth) jako część usługi Azure AD Connect Health dla synchronizacji.

Od 1 września 2016 [Azure Active Directory zduplikowany atrybut odporności](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) funkcja zostanie włączona domyślnie dla wszystkich hello *nowe* usługi Azure Active Directory dzierżaw. Ta funkcja będą automatycznie włączone dla istniejących dzierżawców w hello kolejnych miesięcy.

Azure AD Connect przeprowadza 3 typy operacji z zapewnia synchronizację katalogów hello: Import, synchronizacji i eksportowanie. Błędy może odbywać się we wszystkich operacjach hello. W tym artykule skupiono się głównie na błędy podczas eksportowania tooAzure AD.

## <a name="errors-during-export-tooazure-ad"></a>Błędy podczas eksportowania tooAzure AD
Po sekcji opisano różne typy synchronizacji błędów, które mogą wystąpić podczas hello eksportu operacji tooAzure AD przy użyciu hello łącznika usługi Azure AD. Ten łącznik można zidentyfikować przez format nazwy hello jest "contoso. *onmicrosoft.com*".
Błędy podczas eksportowania tooAzure AD wskazują tej operacji hello \(Dodawanie, aktualizowanie i usuwanie itp.\) próba przy użyciu usługi Azure AD Connect \(aparatu synchronizacji\) w usłudze Azure Active Directory nie powiodło się.

![Omówienie błędy eksportu](./media/active-directory-aadconnect-troubleshoot-sync-errors/Export_Errors_Overview_01.png)

## <a name="data-mismatch-errors"></a>Błędy niezgodność typów danych
### <a name="invalidsoftmatch"></a>InvalidSoftMatch
#### <a name="description"></a>Opis
* Gdy programu Azure AD Connect \(aparatu synchronizacji\) powoduje, że usługi Azure Active Directory tooadd lub aktualizacji dla obiektów, usługi Azure AD dopasowań hello obiekt przychodzące za pomocą hello **sourceAnchor** atrybutu toohello  **nazwę immutableId** atrybutu obiektów w usłudze Azure AD. Nosi nazwę tego dopasowania **twardych odpowiada**.
* Podczas usługi Azure AD **nie znajdzie** każdy obiekt, który odpowiada hello **nazwę immutableId** atrybut o hello **sourceAnchor** atrybut przychodzące obiektu hello przed zainicjowaniem obsługi administracyjnej Nowy obiekt, nastąpi powrót toouse hello ProxyAddresses oraz UserPrincipalName atrybutów toofind dopasowania. Nosi nazwę tego dopasowania **nietrwałego odpowiada**. Hello nietrwałego dopasowanie jest zaprojektowana toomatch obiektów znajduje się już w usłudze Azure AD (które biorą się w usłudze Azure AD) hello nowych obiektów jest dodać/zaktualizować podczas synchronizacji reprezentujących hello tej samej jednostki (użytkownicy, grupy) lokalnie.
* **InvalidSoftMatch** błąd występuje, gdy hello twardych dopasowania nie znajdzie dowolnego zgodnego obiektu **i** nietrwałego dopasowania znajduje dopasowywania obiektu, ale ten obiekt ma wartość inną *nazwę immutableId* niż hello przychodzące obiektu *SourceAnchor*, sugerujące, że hello dopasowywanie obiektu była synchronizowana z innym obiektem z lokalnie usługi Active Directory.

Innymi słowy, aby toowork nietrwałego dopasowania hello, toobe obiektu hello soft dopasowane do nie ma żadnej wartości dla hello *nazwę immutableId*. Jeśli dowolne obiekty z *nazwę immutableId* zestawu z wartością kończy się niepowodzeniem hello hello twardych dopasowanie, ale spełniającą soft-match kryteria, hello Operacja spowodowałaby InvalidSoftMatch błąd synchronizacji.

Usługa Azure Active Directory, schemat nie zezwala na co najmniej dwa obiekty toohave hello tę samą wartość hello następujące atrybuty. \(To nie jest kompletną listą.\)

* ProxyAddresses
* userPrincipalName
* onPremisesSecurityIdentifier
* Identyfikator obiektu

> [!NOTE]
> [Azure AD odporności atrybut zduplikowany atrybut](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) również jest rozwijane funkcji jako zachowanie domyślne hello Azure Active Directory.  Dzięki usłudze Azure AD bardziej odporne w sposób hello obsługi zduplikowanych ProxyAddresses UserPrincipalName atrybutów i obecnych w lokalnych AD zmniejszy hello liczba błędów synchronizacji zostały odebrane przez Azure AD Connect (a także innych klientów synchronizacji) środowiska. Ta funkcja nie błędy hello dublowania. Dlatego hello danych musi nadal toobe stałej. Ale umożliwia inicjowanie obsługi administracyjnej nowych obiektów, które w przeciwnym razie jest blokowane zainicjowanie obsługi powodu wartości tooduplicated w usłudze Azure AD. Zmniejsza to także hello liczba błędów synchronizacji zwrócił toohello klienta synchronizacji.
> Ta funkcja jest włączona dla Twojej dzierżawy, nie będą widzieć błędy synchronizacji InvalidSoftMatch hello występujące podczas inicjowania obsługi administracyjnej nowych obiektów.
>
>

#### <a name="example-scenarios-for-invalidsoftmatch"></a>Przykładowe scenariusze dotyczące InvalidSoftMatch
1. Co najmniej dwa obiekty, które powitalne tę samą wartość atrybutu ProxyAddresses istnieje w na lokalnej usługi Active Directory. Tylko jeden z nich jest wprowadzenie administracyjnie w usłudze Azure AD.
2. Dwa lub więcej obiektów z hello na tę samą wartość userPrincipalName istnieje w lokalnych usługi Active Directory. Tylko jeden z nich jest wprowadzenie administracyjnie w usłudze Azure AD.
3. Obiekt został dodany w hello na lokalnej usługi Active Directory z hello takie same wartości atrybutu ProxyAddresses co istniejący obiekt w usłudze Azure Active Directory. Obiekt Hello dodany lokalnie nie zainicjowano pobierania w usłudze Azure Active Directory.
4. Obiekt został dodany w lokalnie usługi Active Directory z hello takie same wartości atrybutu userPrincipalName jak konto w usłudze Azure Active Directory. Obiekt Hello jest wprowadzenie nieudostępniane w usłudze Azure Active Directory.
5. Zsynchronizowane konta został przeniesiony z lasem A tooForest B. Azure AD Connect (aparatem synchronizacji) została używa hello toocompute atrybut ObjectGUID SourceAnchor. Po przeniesieniu lasu hello wartość hello hello SourceAnchor różni się. Nowy obiekt Hello (z lasem B) kończy się niepowodzeniem toosync z hello istniejący obiekt w usłudze Azure AD.
6. Zsynchronizowano obiektu został przypadkowo usunięty z na lokalnej usługi Active Directory i nowy obiekt został utworzony w usłudze Active Directory dla hello sama jednostka (na przykład użytkownik) bez usuwania hello konta w usłudze Azure Active Directory. toosync z istniejącego obiektu usługi Azure AD hello Hello nowe konto, nie powiedzie się.
7. Azure AD Connect zostało odinstalowane i ponownie. Podczas ponownej instalacji hello inny atrybut, została wybrana jako hello SourceAnchor. Wszystkie obiekty hello, które wcześniej były zsynchronizowane zatrzymać synchronizację z powodu błędu InvalidSoftMatch.

#### <a name="example-case"></a>Przykład przypadek:
1. **Robert Smith** jest zsynchronizowany użytkownika w usłudze Azure Active Directory z na lokalnych usługi Active Directory dla *contoso.com*
2. Robert Smith **UserPrincipalName** jest ustawiony jako  **bobs@contoso.com** .
3. **"abcdefghijklmnopqrstuv =="** jest hello **SourceAnchor** obliczane przy użyciu usługi Azure AD Connect przy użyciu Bob Smith **objectGUID** z na lokalnej usługi Active Directory, który jest hello **nazwę immutableId** Nowak Bob w usłudze Azure Active Directory.
4. Robert ma również następujące wartości hello **proxyAddresses** atrybutu:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
5. Nowy użytkownik **Taylora Bob**, są dodawane toohello na lokalnej usługi Active Directory.
6. Robert Taylora **UserPrincipalName** jest ustawiony jako  **bobt@contoso.com** .
7. **"abcdefghijkl0123456789 ==" "** jest hello **sourceAnchor** obliczane przy użyciu usługi Azure AD Connect przy użyciu Taylora Bob **objectGUID** z na lokalnych usługi Active Directory. Robert Taylora obiektu nie została jeszcze zsynchronizowane tooAzure usługi Active Directory.
8. Taylora Roberta, który ma następujące wartości dla atrybutu proxyAddresses hello hello
   * smtp:bobt@contoso.com
   * smtp:bob.taylor@contoso.com
   * **smtp:bob@contoso.com**
9. Podczas synchronizacji Azure AD Connect hello Dodawanie Roberta Taylora w na lokalnej usługi Active Directory rozpozna i poproś Azure AD toomake hello tej samej zmiany.
10. Usługi Azure AD najpierw zostanie wykonana twarde dopasowania. Oznacza to, umożliwia wyszukiwanie w przypadku dowolnego obiektu o nazwę immutableId hello równy zbyt "abcdefghijkl0123456789 ==". Dopasowanie twardych zakończy się niepowodzeniem, zgodnie z żadnego innego obiektu w usłudze Azure AD nie odniesie tego nazwę immutableId.
11. Usługi Azure AD następnie podejmie próbę dopasowania toosoft Bob Taylora. Oznacza to umożliwia wyszukiwanie, jeśli występuje dowolny obiekt toohello równy proxyAddresses trzy wartości, w tymsmtp:bob@contoso.com
12. Usługi Azure AD będą odnalezienie obiektu Bob Smith toomatch hello soft-match. Ale ten obiekt zawiera wartość hello nazwę immutableId = "abcdefghijklmnopqrstuv ==". co oznacza ten obiekt został zsynchronizowany z innego obiektu z lokalnie usługi Active Directory. W związku z tym usługi Azure AD nie soft-match te obiekty i powoduje **InvalidSoftMatch** błąd synchronizacji.

#### <a name="how-toofix-invalidsoftmatch-error"></a>Jak toofix InvalidSoftMatch błąd
Witaj Najczęstszym powodem hello błąd InvalidSoftMatch jest dwa obiekty o różnych SourceAnchor \(nazwę immutableId\) mają takie same wartości dla atrybutów hello ProxyAddresses i/lub UserPrincipalName, które są używane podczas hello hello Proces Soft-match w usłudze Azure AD. W kolejności toofix hello nieprawidłowy nietrwałego dopasowania

1. Zidentyfikuj hello zduplikowane proxyAddresses, userPrincipalName lub innych wartość atrybutu, który powoduje błąd hello. Również zidentyfikowanie dwa \(lub więcej\) obiekty są związane z konfliktem hello w. Witaj raportu generowanych przez [Azure AD Connect Health dla synchronizacji](https://aka.ms/aadchsyncerrors) mogą ułatwić identyfikację hello dwóch obiektów.
2. Zidentyfikuj obiektu, który powinno być kontynuowane toohave hello zduplikowane wartości i obiektu, który nie powinien.
3. Usuń hello zduplikowane wartości z obiektu hello, które nie powinny mieć tę wartość. Należy pamiętać, należy hello zmiany w katalogu hello której pochodzi z obiektu hello. W niektórych przypadkach może być konieczne toodelete jeden z obiektów hello w konflikcie.
4. Jeśli wprowadzono zmiany w hello lokalnie AD hello pozwolić, aby zmienić hello synchronizacji Azure AD Connect.

Należy pamiętać, że raport o błędzie synchronizacji w ramach usługi Azure AD Connect Health do celów synchronizacji jest aktualizowany co 30 minut i zawiera błędy hello hello najnowsze próby synchronizacji.

> [!NOTE]
> Nazwę ImmutableId, zgodnie z definicją, nie należy zmieniać w hello istnienia obiektu hello. Jeśli usługa Azure AD Connect nie zostało skonfigurowane z niektórych scenariuszy hello pamiętać z hello powyżej listy, może się okazać w sytuacji, gdy Azure AD Connect oblicza inną wartość hello SourceAnchor dla obiekt hello AD czy reprezentuje hello tej samej jednostki (tego samego użytkownika / Grupowanie i kontaktów itp.) mający mają toocontinue przy użyciu istniejącego obiektu AD platformy Azure.
>
>

#### <a name="related-articles"></a>Pokrewne artykuły
* [Zduplikowane lub nieprawidłowe atrybuty zapobieganie synchronizacji katalogów w usłudze Office 365](https://support.microsoft.com/en-us/kb/2647098)

### <a name="objecttypemismatch"></a>ObjectTypeMismatch
#### <a name="description"></a>Opis
Jeśli usługi Azure AD próbuje toosoft dopasowania dwa obiekty, jest to możliwe, że dwa obiekty o różnych "typu obiektu" (na przykład użytkownikiem, grupą, skontaktuj się z itp.) mają takie same wartości hello atrybuty używane dopasowanie nietrwałego hello tooperform hello. Jak duplikatów tych atrybutów jest niedozwolone w usłudze Azure AD, hello operacji może spowodować błąd synchronizacji "ObjectTypeMismatch".

#### <a name="example-scenarios-for-objecttypemismatch-error"></a>Przykładowe scenariusze dla błędu ObjectTypeMismatch
* Grupy zabezpieczeń włączoną obsługę poczty jest tworzony w usłudze Office 365. Administrator dodaje nowego użytkownika lub kontaktu w lokalnie AD (które nie zsynchronizowała jeszcze tooAzure AD) z samą wartość dla atrybutu ProxyAddresses hello co hello usługi Office 365 hello grupy.

#### <a name="example-case"></a>Przykład case
1. Administrator tworzy nową grupę zabezpieczeń z włączoną obsługę poczty w usłudze Office 365 dla działu podatku hello i udostępnia adres e-mail jako tax@contoso.com. W ten sposób hello ProxyAddresses atrybutu dla tej grupy o wartości hello**smtp:tax@contoso.com**
2. Nowy użytkownik nie przyłączy Contoso.com i utworzeniu konta dla użytkownika hello lokalnie z proxyAddress hello jako**smtp:tax@contoso.com**
3. Gdy usługa Azure AD Connect zsynchronizuje hello nowego konta użytkownika, otrzyma błąd "ObjectTypeMismatch" hello.

#### <a name="how-toofix-objecttypemismatch-error"></a>Jak toofix ObjectTypeMismatch błąd
Najbardziej typową przyczyną błędu ObjectTypeMismatch hello Hello jest hello samą wartość dla atrybutu ProxyAddresses hello dwa obiekty innego typu (użytkownikiem, grupą, skontaktuj się z itp.). W kolejności toofix hello ObjectTypeMismatch:

1. Zidentyfikuj hello zduplikowane proxyAddresses (lub inne atrybuty) to jest powodując błąd hello wartości. Również zidentyfikowanie dwa \(lub więcej\) obiekty są związane z konfliktem hello w. Witaj raportu generowanych przez [Azure AD Connect Health dla synchronizacji](https://aka.ms/aadchsyncerrors) mogą ułatwić identyfikację hello dwóch obiektów.
2. Zidentyfikuj obiektu, który powinno być kontynuowane toohave hello zduplikowane wartości i obiektu, który nie powinien.
3. Usuń hello zduplikowane wartości z obiektu hello, które nie powinny mieć tę wartość. Należy pamiętać, należy hello zmiany w katalogu hello której pochodzi z obiektu hello. W niektórych przypadkach może być konieczne toodelete jeden z obiektów hello w konflikcie.
4. Jeśli wprowadzono zmiany w hello lokalnie AD hello pozwolić, aby zmienić hello synchronizacji Azure AD Connect. Raport o błędzie synchronizacji w ramach usługi Azure AD Connect Health dla synchronizacji aktualizowany co 30 minut i zawiera błędy hello hello najnowsze próby synchronizacji.

## <a name="duplicate-attributes"></a>Duplikowanie atrybutów
### <a name="attributevaluemustbeunique"></a>AttributeValueMustBeUnique
#### <a name="description"></a>Opis
Usługa Azure Active Directory, schemat nie zezwala na co najmniej dwa obiekty toohave hello tę samą wartość hello następujące atrybuty. To każdego obiektu w usłudze Azure AD jest wymuszone toohave unikatowe wartości tych atrybutów w podanym wystąpieniu.

* ProxyAddresses
* userPrincipalName

Jeśli Azure AD Connect podejmuje tooadd nowy obiekt lub zaktualizować istniejący obiekt z wartością hello powyżej atrybutów, który jest już przypisany tooanother obiektu w usłudze Azure Active Directory, operacja hello powoduje błąd synchronizacji "AttributeValueMustBeUnique" hello.

#### <a name="possible-scenarios"></a>Możliwe scenariusze:
1. Zduplikowana wartość jest już zsynchronizowane obiektu tooan przypisane, który powoduje konflikt z innym obiektem zsynchronizowane.

#### <a name="example-case"></a>Przykład przypadek:
1. **Robert Smith** jest zsynchronizowany użytkownika w usłudze Azure Active Directory z na lokalnych usługi Active Directory dla domeny contoso.com
2. Robert Smith **UserPrincipalName** lokalnie jest ustawiony jako  **bobs@contoso.com** .
3. Robert ma również następujące wartości hello **proxyAddresses** atrybutu:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
4. Nowy użytkownik **Taylora Bob**, są dodawane toohello na lokalnej usługi Active Directory.
5. Robert Taylora **UserPrincipalName** jest ustawiony jako  **bobt@contoso.com** .
6. **Robert Taylora** ma następujące wartości hello hello **ProxyAddresses** atrybutu i. smtp:bobt@contoso.comII. smtp:bob.taylor@contoso.com
7. Obiektu Taylora Roberta, który jest synchronizowany z usługą Azure AD pomyślnie.
8. Administrator decyzję tooupdate Bob Taylora **ProxyAddresses** atrybut o hello następujące wartości: i. **smtp:bob@contoso.com**
9. Usługi Azure AD będzie podejmować tooupdate Bob Taylora obiektu w usłudze Azure AD z hello powyżej wartości, ale czy operacja zakończy się niepowodzeniem jako wartość ProxyAddresses przypisano już tooBob Smith, co spowoduje błąd "AttributeValueMustBeUnique".

#### <a name="how-toofix-attributevaluemustbeunique-error"></a>Jak toofix AttributeValueMustBeUnique błąd
Witaj Najczęstszym powodem hello błąd AttributeValueMustBeUnique jest dwa obiekty o różnych SourceAnchor \(nazwę immutableId\) mają takie same wartości hello ProxyAddresses i/lub atrybuty UserPrincipalName hello. W kolejności toofix AttributeValueMustBeUnique błąd

1. Zidentyfikuj hello zduplikowane proxyAddresses, userPrincipalName lub innych wartość atrybutu, który powoduje błąd hello. Również zidentyfikowanie dwa \(lub więcej\) obiekty są związane z konfliktem hello w. Witaj raportu generowanych przez [Azure AD Connect Health dla synchronizacji](https://aka.ms/aadchsyncerrors) mogą ułatwić identyfikację hello dwóch obiektów.
2. Zidentyfikuj obiektu, który powinno być kontynuowane toohave hello zduplikowane wartości i obiektu, który nie powinien.
3. Usuń hello zduplikowane wartości z obiektu hello, które nie powinny mieć tę wartość. Należy pamiętać, należy hello zmiany w katalogu hello której pochodzi z obiektu hello. W niektórych przypadkach może być konieczne toodelete jeden z obiektów hello w konflikcie.
4. Jeśli wprowadzono zmiany w hello lokalnie AD hello pozwolić, aby zmienić tooget błąd hello stałej hello synchronizacji Azure AD Connect.

#### <a name="related-articles"></a>Pokrewne artykuły
-[Zduplikowane lub nieprawidłowe atrybuty zapobieganie synchronizacji katalogów w usłudze Office 365](https://support.microsoft.com/en-us/kb/2647098)

## <a name="data-validation-failures"></a>Błędy sprawdzania poprawności danych
### <a name="identitydatavalidationfailed"></a>IdentityDataValidationFailed
#### <a name="description"></a>Opis
Usługa Azure Active Directory wymusza różne ograniczenia na powitania samych danych przed zezwoleniem na tym toobe danych zapisany w katalogu hello. Jest to tooensure, które użytkownicy końcowi mogą uzyskiwać najlepsze możliwe środowiska hello podczas korzystania z aplikacji hello, które są zależne od tych danych.

#### <a name="scenarios"></a>Scenariusze
a. wartość atrybutu UserPrincipalName Hello jest nieprawidłowy lub nieobsługiwany znaków.
b. Atrybut UserPrincipalName Hello nie jest zgodna z wymaganym formatem hello.

#### <a name="how-toofix-identitydatavalidationfailed-error"></a>Jak toofix IdentityDataValidationFailed błąd
a. Upewnij się, że ten atrybut userPrincipalName hello ma obsługiwane znaki i wymagany format.

#### <a name="related-articles"></a>Pokrewne artykuły
* [Przygotowanie tooprovision użytkowników za pomocą tooOffice synchronizacji katalogu 365](https://support.office.com/en-us/article/Prepare-to-provision-users-through-directory-synchronization-to-Office-365-01920974-9e6f-4331-a370-13aea4e82b3e)

### <a name="federateddomainchangeerror"></a>FederatedDomainChangeError
#### <a name="description"></a>Opis
Określone tak, którego wynikiem jest **"FederatedDomainChangeError"** błąd synchronizacji, gdy sufiks hello UserPrincipalName użytkownika zostanie zmieniona z jednej domeny federacyjnej tooanother domeny federacyjnej.

#### <a name="scenarios"></a>Scenariusze
Zsynchronizowane użytkownika sufiks UserPrincipalName hello został zmieniony z jednej domeny federacyjnej tooanother domeny federacyjnej lokalnie. Na przykład *UserPrincipalName = bob@contoso.com*  został zmieniony zbyt*UserPrincipalName = bob@fabrikam.com* .

#### <a name="example"></a>Przykład
1. Robert Smith, konta dla domeny Contoso.com, pobiera dodany jako nowego użytkownika w usłudze Active Directory z hello UserPrincipalNamebob@contoso.com
2. Robert przenosi tooa różnych dzielenia contoso.com o nazwie Fabrikam.com i jego UserPrincipalName zostanie zmieniona.toobob@fabrikam.com
3. Domeny contoso.com jak również fabrikam.com są Sfederowanych domen w usłudze Azure Active Directory.
4. UserPrincipalName Roberta nie zostanie zaktualizowana i powoduje błąd synchronizacji "FederatedDomainChangeError".

#### <a name="how-toofix"></a>Jak toofix
Jeśli sufiks UserPrincipalName użytkownika została zaktualizowana z bob @**contoso.com** toobob @**fabrikam.com**, gdzie oba **contoso.com** i **fabrikam.com** są **Sfederowanych domen**, należy wykonać te kroki toofix hello synchronizacji błąd

1. Zaktualizuj UserPrincipalName hello użytkownika w usłudze Azure AD z bob@contoso.com toobob@contoso.onmicrosoft.com. Możesz użyć następującego polecenia programu PowerShell z modułu Azure AD PowerShell hello hello:`Set-MsolUserPrincipalName -UserPrincipalName bob@contoso.com -NewUserPrincipalName bob@contoso.onmicrosoft.com`
2. Zezwalaj na synchronizację tooattempt cyklu synchronizacji hello dalej. Wykonanie synchronizacji czasu zakończy się pomyślnie i spowoduje zaktualizowanie hello UserPrincipalName Bob toobob@fabrikam.com zgodnie z oczekiwaniami.

#### <a name="related-articles"></a>Pokrewne artykuły
* [Zmiany nie są synchronizowane przez narzędzie do synchronizacji usługi Azure Active Directory powitania po zmianie hello UPN toouse konto użytkownika innej domeny federacyjnej](https://support.microsoft.com/en-us/help/2669550/changes-aren-t-synced-by-the-azure-active-directory-sync-tool-after-you-change-the-upn-of-a-user-account-to-use-a-different-federated-domain)

## <a name="largeobject"></a>LargeObject
### <a name="description"></a>Opis
Gdy atrybut przekracza dozwolony limit rozmiaru, limit długości lub ustawiony przez schemat usługi Active Directory Azure limit liczby hello, hello Operacja synchronizacji powoduje hello **LargeObject** lub **ExceededAllowedLength** błąd synchronizacji. Zazwyczaj ten błąd występuje dla hello następujące atrybuty

* userCertificate
* userSMIMECertificate
* thumbnailPhoto
* proxyAddresses

### <a name="possible-scenarios"></a>Możliwe scenariusze
1. Atrybut certyfikatu użytkownika Roberta jest przechowywanie zbyt wiele tooBob certyfikaty przypisane. Mogą one obejmować starsze, wygasłe certyfikaty. nienaruszalne ograniczenie Hello jest 15 certyfikatów. Aby uzyskać więcej informacji na jak błędy LargeObject toohandle z certyfikatu użytkownika atrybutu, należy odwoływać się tooarticle [LargeObject obsługi błędów spowodowanych przez atrybut certyfikatu użytkownika](active-directory-aadconnectsync-largeobjecterror-usercertificate.md).
2. Atrybut userSMIMECertificate Roberta jest przechowywanie zbyt wiele tooBob certyfikaty przypisane. Mogą one obejmować starsze, wygasłe certyfikaty. nienaruszalne ograniczenie Hello jest 15 certyfikatów.
3. ThumbnailPhoto Roberta ustawić w usłudze Active Directory jest zbyt duży toobe synchronizowane w usłudze Azure AD.
4. Podczas automatycznego wypełniania hello ProxyAddresses atrybutu w usłudze Active Directory obiekt ma zbyt wiele ProxyAddresses przypisane.

### <a name="how-toofix"></a>Jak toofix
1. Upewnij się, że ten atrybut hello powoduje błąd hello mieści się w hello dozwolone ograniczenia.

## <a name="related-links"></a>Powiązane linki
* [Znajdź obiekty usługi Active Directory w Centrum administracyjne usługi Active Directory](https://technet.microsoft.com/library/dd560661.aspx)
* [Jak tooquery usługi Azure Active Directory dla obiekt przy użyciu programu PowerShell usługi Azure Active Directory](https://msdn.microsoft.com/library/azure/jj151815.aspx)
