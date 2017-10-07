---
title: 'Azure AD Connect: Historia wersji | Dokumentacja firmy Microsoft'
description: "Ten artykuł zawiera listę wszystkich wersji programu Azure AD Connect i Azure AD Sync"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ef2797d7-d440-4a9a-a648-db32ad137494
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b55e0f2d426e34ceef9869d5a6d1b0956d8bd076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-version-release-history"></a>Azure AD Connect: Historia wersji
Zespół usługi Azure Active Directory (Azure AD) Hello regularnie aktualizuje Azure AD Connect z nowych funkcji. Nie wszystkie dodatki są stosowane tooall odbiorców.

W tym artykule jest zaprojektowana toohelp korzystać ze śledzenia wersji hello, które zostały wydane i toounderstand tego, czy należy tooupdate toohello najnowsza wersja lub nie.

Jest to lista Tematy pokrewne:


Temat |  Szczegóły
--------- | --------- |
Kroki tooupgrade z usługi Azure AD Connect | Różne metody zbyt[uaktualnianie z poprzedniej wersji toohello najnowszych](active-directory-aadconnect-upgrade-previous-version.md) wersji Azure AD Connect.
Wymagane uprawnienia | Aby uzyskać wymagane uprawnienia tooapply aktualizacji, zobacz [konta i uprawnienia](./active-directory-aadconnect-accounts-permissions.md#upgrade).
Do pobrania| [Pobieranie programu Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="115610"></a>1.1.561.0
Stanu: 2017 23 lipca

### <a name="azure-ad-connect"></a>Program Azure AD Connect

#### <a name="fixed-issue"></a>Rozwiązany problem

* Rozwiązano problem powodujący reguły synchronizacji out-of-box hello "limit tooAD - użytkownika nazwę ImmutableId" toobe usunięte:

  * Witaj problem występuje, gdy jest uaktualnienie programu Azure AD Connect, lub gdy hello opcji zadań *Konfiguracja synchronizacji aktualizacji* w hello Azure AD Connect Kreator jest używany tooupdate usługi Azure AD Connect synchronizacji konfiguracji.
  
  * Ta reguła synchronizacji jest stosowane toocustomers, kto włączył hello [msDS-ConsistencyGuid jako funkcja zakotwiczenie źródła](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). Ta funkcja została wprowadzona w wersji 1.1.524.0 i po. Po usunięciu reguły synchronizacji hello Azure AD Connect nie będzie można wypełnić lokalnymi atrybutu ms-DS-ConsistencyGuid AD z hello wartość atrybut ObjectGuid. Nie zapobiega nowi użytkownicy z aprowizowany do usługi Azure AD.
  
  * poprawka Hello gwarantuje, że tej reguły synchronizacji hello nie zostaną usunięte podczas uaktualniania, lub zmianę konfiguracji, tak długo, jak funkcja hello jest włączona. Dla istniejących klientów, które zostały objęte tym problemem, hello poprawka również gwarantuje, że tej reguły synchronizacji hello zostanie dodany ponownie, po uaktualnieniu wersji toothis programu Azure AD Connect.

* Rozwiązano problem powodujący reguły synchronizacji out-of-box toohave pierwszeństwo wartość, która jest mniejsza niż 100:

  * Ogólnie rzecz biorąc pierwszeństwo wartości 0 - 99 są zarezerwowane dla reguły synchronizacji niestandardowych. Podczas uaktualniania hello wartości pierwszeństwo reguły synchronizacji out-of-box to zmian reguły synchronizacji tooaccommodate zaktualizowane. Ze względu na problem toothis reguły synchronizacji out-of-box można przypisać priorytet wartość, która jest mniejsza niż 100.
  
  * poprawka Hello zapobiega hello problem podczas uaktualniania. Jednak nie są przywracane hello pierwszeństwo wartości dla istniejących klientów, którzy została dotknięta hello problem. Oddzielna poprawka zostanie podany w przyszłych toohelp hello z hello przywracania.

* Rozwiązano problem w przypadku gdy hello [ekran domeny i jednostki Organizacyjnej filtrowania](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) w hello Azure AD Connect jest wyświetlany Kreator *synchronizowanie wszystkich domen i jednostek organizacyjnych* opcję jako wybrany, nawet jeśli filtrowanie na podstawie jednostki Organizacyjnej jest włączona.

*   Rozwiązano problem z tym spowodowane hello [ekranu Konfigurowanie partycji katalogu](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) w hello tooreturn Synchronization Service Manager wystąpił błąd, jeśli hello *Odśwież* kliknięciu przycisku. komunikat o błędzie Hello *"Napotkano błąd podczas odświeżania domeny: toocast obiektu typu"System.Collections.ArrayList"tootype" Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject."* Witaj błąd występuje, gdy został dodany nowej domeny AD tooan istniejącego lasu usługi AD i próbujesz tooupdate Azure AD Connect przy użyciu hello przycisk Odśwież.

#### <a name="new-features-and-improvements"></a>Nowe funkcje i ulepszenia

* [Funkcja aktualizacji automatycznych](active-directory-aadconnect-feature-automatic-upgrade.md) został rozwinięte toosupport klientom Witaj następujące konfiguracje:
  * Włączono funkcję zapisywania zwrotnego urządzeń hello.
  * Włączeniu funkcji zapisywania zwrotnego grupy hello.
  * Witaj, instalacja nie jest ustawień ekspresowych lub uaktualnienie narzędzia DirSync.
  * Masz więcej niż 100 000 obiektów w magazynie metaverse hello.
  * Łączysz toomore niż jednym lesie. Instalacja ekspresowa łączy tylko tooone lasu.
  * Witaj konta łącznika usługi AD nie jest już hello domyślnego MSOL_ konta.
  * Serwer Hello jest ustawiony toobe w trybie przejściowym.
  * Włączono funkcję zapisywania zwrotnego użytkowników hello.
  
  >[!NOTE]
  >rozszerzenia zakresu Hello hello automatyczne uaktualnienie funkcji ma wpływ na klientów z programem Azure AD Connect kompilacji 1.1.105.0 i po. Jeśli nie chcesz, aby toobe serwera programu Azure AD Connect, automatycznie uaktualnione, należy uruchomić poniższe polecenie cmdlet na serwerze programu Azure AD Connect: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Aby uzyskać więcej informacji na temat Włączanie i wyłączanie automatycznego uaktualnienia można znaleźć tooarticle [Azure AD Connect: automatyczne uaktualnianie](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115580"></a>1.1.558.0
Stan: Nie będzie publikowana. Zmiany w tej kompilacji są uwzględnione w wersji 1.1.561.0.

### <a name="azure-ad-connect"></a>Program Azure AD Connect

#### <a name="fixed-issue"></a>Rozwiązany problem

* Rozwiązano problem powodujący hello synchronizacji out-of-box reguły "poza tooAD - użytkownika nazwę ImmutableId" toobe usuwane podczas aktualizacji konfiguracji filtrowania opartego na jednostce Organizacyjnej. Ta reguła synchronizacji jest wymagany dla hello [msDS-ConsistencyGuid jako funkcja zakotwiczenie źródła](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).

* Rozwiązano problem w przypadku gdy hello [ekran domeny i jednostki Organizacyjnej filtrowania](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) w hello Azure AD Connect jest wyświetlany Kreator *synchronizowanie wszystkich domen i jednostek organizacyjnych* opcję jako wybrany, nawet jeśli filtrowanie na podstawie jednostki Organizacyjnej jest włączona.

*   Rozwiązano problem z tym spowodowane hello [ekranu Konfigurowanie partycji katalogu](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) w hello tooreturn Synchronization Service Manager wystąpił błąd, jeśli hello *Odśwież* kliknięciu przycisku. komunikat o błędzie Hello *"Napotkano błąd podczas odświeżania domeny: toocast obiektu typu"System.Collections.ArrayList"tootype" Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject."* Witaj błąd występuje, gdy został dodany nowej domeny AD tooan istniejącego lasu usługi AD i próbujesz tooupdate Azure AD Connect przy użyciu hello przycisk Odśwież.

#### <a name="new-features-and-improvements"></a>Nowe funkcje i ulepszenia

* [Funkcja aktualizacji automatycznych](active-directory-aadconnect-feature-automatic-upgrade.md) został rozwinięte toosupport klientom Witaj następujące konfiguracje:
  * Włączono funkcję zapisywania zwrotnego urządzeń hello.
  * Włączeniu funkcji zapisywania zwrotnego grupy hello.
  * Witaj, instalacja nie jest ustawień ekspresowych lub uaktualnienie narzędzia DirSync.
  * Masz więcej niż 100 000 obiektów w magazynie metaverse hello.
  * Łączysz toomore niż jednym lesie. Instalacja ekspresowa łączy tylko tooone lasu.
  * Witaj konta łącznika usługi AD nie jest już hello domyślnego MSOL_ konta.
  * Serwer Hello jest ustawiony toobe w trybie przejściowym.
  * Włączono funkcję zapisywania zwrotnego użytkowników hello.
  
  >[!NOTE]
  >rozszerzenia zakresu Hello hello automatyczne uaktualnienie funkcji ma wpływ na klientów z programem Azure AD Connect kompilacji 1.1.105.0 i po. Jeśli nie chcesz, aby toobe serwera programu Azure AD Connect, automatycznie uaktualnione, należy uruchomić poniższe polecenie cmdlet na serwerze programu Azure AD Connect: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Aby uzyskać więcej informacji na temat Włączanie i wyłączanie automatycznego uaktualnienia można znaleźć tooarticle [Azure AD Connect: automatyczne uaktualnianie](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115570"></a>1.1.557.0
Stanu: 2017 lipca

>[!NOTE]
>Ta kompilacja nie jest dostępna toocustomers za pomocą hello Azure AD Connect automatycznego uaktualnienia funkcji.

### <a name="azure-ad-connect"></a>Program Azure AD Connect

#### <a name="fixed-issue"></a>Rozwiązany problem
* Rozwiązano problem z poleceniem cmdlet hello Initialize-ADSyncDomainJoinedComputerSync powodujący hello zweryfikowanej domeny skonfigurowane na powitania istniejącej usługi połączenia punktu obiektu toobe zmienione, nawet jeśli jest nadal prawidłowa domena. Ten problem występuje, gdy dzierżawy usługi Azure AD ma więcej niż jeden zweryfikowanych domen, które mogą służyć do konfigurowania punktu połączenia usługi hello.

#### <a name="new-features-and-improvements"></a>Nowe funkcje i ulepszenia
* Zapisywanie zwrotne haseł jest teraz dostępna do podglądu z chmury Microsoft Azure dla instytucji rządowych i Niemczech Microsoft Cloud. Aby uzyskać więcej informacji o obsłudze usługi Azure AD Connect hello wystąpień innej usługi, można znaleźć tooarticle [Azure AD Connect: uwagi dotyczące wystąpienia](active-directory-aadconnect-instances.md).

* polecenie cmdlet Hello Initialize-ADSyncDomainJoinedComputerSync ma teraz nowe opcjonalny parametr o nazwie AzureADDomain. Ten parametr umożliwia określenie, które zweryfikować używane podczas konfigurowania punktu połączenia usługi hello toobe domeny.

### <a name="pass-through-authentication"></a>Uwierzytelnianie przekazywane

#### <a name="new-features-and-improvements"></a>Nowe funkcje i ulepszenia
* Nazwa Hello agenta hello wymagany na potrzeby uwierzytelniania przekazywanego została zmieniona z *łącznika serwera Proxy w aplikacji pakietu Microsoft Azure AD* za*agenta programu Microsoft Azure AD Connect uwierzytelniania*.

* Włączanie uwierzytelniania przekazywanego już domyślnie włączone synchronizacji skrótu hasła.


## <a name="115530"></a>1.1.553.0
Stan: Czerwiec 2017

> [!IMPORTANT]
> Brak schematu i synchronizacji reguły wprowadzone w tej kompilacji. Azure AD Connect usługi synchronizacji wyzwoli pełny Import i pełną synchronizację czynności po uaktualnieniu. Szczegółowe informacje o zmianach hello są opisane poniżej. tootemporarily odroczenie pełny Import i pełną synchronizację czynności po uaktualnieniu, zapoznaj się tooarticle [jak toodefer pełnej synchronizacji po uaktualnieniu](active-directory-aadconnect-upgrade-previous-version.md#how-to-defer-full-synchronization-after-upgrade).
>
>

### <a name="azure-ad-connect-sync"></a>Azure AD Connect Sync

#### <a name="known-issue"></a>Znany problem
* Istnieje problem, który ma wpływ na klientów, którzy korzystają z [filtrowanie na podstawie jednostki Organizacyjnej](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) z synchronizacji Azure AD Connect. Po przejściu toohello [strony domeny i jednostki Organizacyjnej filtrowania](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) w Kreatorze hello Azure AD Connect oczekuje hello następujące zachowanie:
  * Jeśli włączono filtrowanie na podstawie jednostki Organizacyjnej hello **synchronizacji wybranych domen i jednostek organizacyjnych** opcja jest zaznaczona.
  * W przeciwnym razie hello **synchronizowanie wszystkich domen i jednostek organizacyjnych** opcja jest zaznaczona.

Witaj problem wynika, że jest tym hello **synchronizowanie wszystkich domen i jednostek organizacyjnych opcja** jest zawsze zaznaczone, po uruchomieniu kreatora hello.  Dzieje się tak nawet, jeśli wcześniej skonfigurowano filtrowanie oparte na jednostce Organizacyjnej. Przed zapisaniem zmian konfiguracji AAD Connect, upewnij się, że hello **synchronizować wybranych domen i jednostek organizacyjnych opcja** i Potwierdź, że wszystkie jednostki organizacyjne, które wymagają toosynchronize są ponownie włączona. W przeciwnym razie filtrowanie na podstawie jednostki Organizacyjnej zostanie wyłączone.

#### <a name="fixed-issues"></a>Rozwiązane problemy

* Rozwiązano problem z zapisywaniem zwrotnym haseł, umożliwiający Azure AD administratora tooreset hello hasło lokalne AD uprzywilejowane konto użytkownika. Hello problem występuje, gdy Azure AD Connect jest uprawnienie hello resetowania hasła za pośrednictwem hello uprzywilejowane konto. Witaj problem został rozwiązany w tej wersji programu Azure AD Connect, nie zezwalając Azure AD administratora tooreset hello hasło dowolnego lokalnego AD uprzywilejowane konto użytkownika, chyba że hello administrator jest hello właściciela tego konta. Aby uzyskać więcej informacji, zobacz zbyt[Security Advisory 4033453](https://technet.microsoft.com/library/security/4033453).

* Rozwiązano problem powiązane toohello [msDS-ConsistencyGuid jako zakotwiczenie źródła](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) funkcji, w którym Azure AD Connect nie zapisywania zwrotnego tooon lokalne są atrybutu msDS-ConsistencyGuid AD. Hello problem występuje w przypadku lokalnego wielu lasów usługi AD dodane tooAzure AD Connect i hello *tożsamości użytkowników istnieją w wielu opcji katalogów* jest zaznaczone. W przypadku takiej konfiguracji reguły synchronizacji wynikowe hello nie należy wypełniać atrybutu sourceAnchorBinary hello w hello Metaverse. Atrybut sourceAnchorBinary Hello jest używany jako atrybut źródłowy hello atrybutu msDS-ConsistencyGuid. W związku z tym atrybutu ms-DSConsistencyGuid toohello zapisywania zwrotnego nie występuje. problem hello toofix, następujące reguły synchronizacji zostały zaktualizowane tooensure, który hello atrybutu sourceAnchorBinary w hello Metaverse zawsze jest wypełniana:
  * W z usługi AD - InetOrgPerson AccountEnabled.xml
  * W z usługi AD - wstawić InetOrgPerson
  * W z usługi AD - AccountEnabled.xml użytkownika
  * W z usługi AD - wstawić użytkownika
  * W z usługi AD - użytkownika dołączyć SOAInAAD.xml

* Wcześniej, nawet jeśli hello [msDS-ConsistencyGuid jako zakotwiczenie źródła](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) funkcja nie jest włączona, hello "limit tooAD — użytkownika nazwę ImmutableId" reguła synchronizacji nadal jest dodawana tooAzure AD Connect. efekt Hello jest niegroźne i nie powoduje zapisywanie zwrotne toooccur atrybutu msDS-ConsistencyGuid. pomyłek tooavoid tooensure, który hello reguła synchronizacji jest dodawane tylko po włączeniu funkcji hello dodano logikę.

* Rozwiązano problem powodujący toofail synchronizacji skrótów haseł z zdarzenie błędu 611. Ten problem występuje, gdy jedna lub więcej domen, kontrolerów zostały usunięte z lokalnej usługi AD. Na końcu hello cyklu synchronizacji haseł, hello pliku cookie synchronizacji wystawione przez lokalny AD zawiera identyfikatory wywołania hello usunięte kontrolerów domeny z numerów USN (Update Sequence Number) wartość 0. Witaj Menedżera synchronizacji haseł jest toopersist synchronizacji plik cookie zawierający USN wartość 0 i kończy się niepowodzeniem z zdarzenie błędu 611. Podczas następnej synchronizacji hello cykl, hello Menedżera synchronizacji haseł powtórnych hello ostatniej synchronizacji utrwalonego pliku cookie, który nie zawiera numeru USN równą 0. Powoduje to hello identycznych zmian hasła toobe zsynchronizowane. Z tej poprawki hello Menedżera synchronizacji haseł są utrwalane w pliku cookie synchronizacji hello poprawnie.

* Wcześniej nawet jeśli automatyczne uaktualnienie zostało wyłączone za pomocą polecenia cmdlet hello ADSyncAutoUpgrade zestawu, hello proces automatycznego uaktualniania okresowo nadal toocheck do uaktualnienia i zależy od kalectwa toohonor Instalator hello pobrane. Z tej poprawki hello proces automatycznego uaktualniania nie sprawdza, czy uaktualnienie okresowo. poprawka Hello automatycznie jest stosowana, gdy po wykonaniu uaktualnienia Instalatora dla tej wersji Azure AD Connect.

#### <a name="new-features-and-improvements"></a>Nowe funkcje i ulepszenia

* Wcześniej, hello [msDS-ConsistencyGuid jako zakotwiczenie źródła](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) funkcja była toonew dostępne tylko w przypadku wdrożeń. Teraz jest dostępne tooexisting wdrożeń. Więcej szczegółów:
  * tooaccess hello funkcji, uruchom kreatora Połącz hello Azure AD, a następnie wybierz hello *zakotwiczenie źródła aktualizacji* opcji.
  * Ta opcja jest tylko wdrożenia widoczne tooexisting używających objectGuid jako atrybut sourceAnchor.
  * Podczas konfigurowania opcji hello, hello Kreator sprawdza, czy stan hello atrybutu msDS-ConsistencyGuid hello w lokalnej usługi Active Directory. Jeśli atrybut hello nie jest skonfigurowana dla dowolnego obiektu użytkownika w katalogu hello, Kreator hello używa hello msDS-ConsistencyGuid jako atrybut sourceAnchor hello. Jeśli atrybut hello jest skonfigurowany w co najmniej jeden obiekt użytkownika w katalogu hello, Kreator hello zawiera atrybut hello jest używany przez inne aplikacje i nie nadaje się jako atrybut sourceAnchor i nie zezwala na powitania zakotwiczenie źródła zmiany tooproceed. Jeśli masz pewność, że ten atrybut hello nie jest używana przez istniejące aplikacje, należy toocontact pomocy technicznej Aby uzyskać informacje dotyczące sposobu toosuppress hello błędu.

* Określonych zbyt**userCertificate** atrybutu na obiekty urządzeń, Azure teraz AD Connect szuka wartości certyfikaty wymagane dla [łączenie urządzeń przyłączonych do domeny tooAzure AD środowisko systemu Windows 10](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy) i odfiltrowuje rest hello przed synchronizacją tooAzure AD. tooenable, którego to zachowanie, zasada synchronizacji out-of-box hello "Out tooAAD - urządzenie Dołącz SOAInAD" został zaktualizowany.

* Azure AD Connect teraz obsługuje funkcję zapisywania zwrotnego z usługą Exchange Online **cloudPublicDelegates** atrybutu lokalnego tooon AD **publicDelegates** atrybutu. Dzięki temu hello scenariusz, gdzie skrzynki pocztowej programu Exchange Online może zostać przydzielony toousers prawa SendOnBehalfTo z lokalnymi skrzynek pocztowych programu Exchange. toosupport tej funkcji, Nowa reguła synchronizacji out-of-box "limit tooAD — PublicDelegates hybrydowego programu Exchange użytkownika funkcji zapisywania zwrotnego" został dodany. Ta reguła synchronizacji jest dodawane tylko tooAzure AD Connect po włączeniu funkcji hybrydowym programu Exchange.

*   Azure AD Connect obsługuje teraz Synchronizowanie hello **altRecipient** atrybutów z usługi Azure AD. toosupport tę zmianę, reguły synchronizacji out-of-box zostały zaktualizowane przepływ atrybutów tooinclude hello wymagane:
  * W z usługi Active Directory — Exchange użytkownika
  * Limit tooAAD — ExchangeOnline użytkownika
  
* Witaj **cloudSOAExchMailbox** atrybut w hello Metaverse wskazuje, czy dany użytkownik ma pocztowa usługi Exchange Online. Definicję został zaktualizowany tooinclude dodatkowe usługi Exchange Online RecipientDisplayTypes jako takie urządzenia i sali konferencyjnej skrzynek pocztowych. tooenable tej zmiany definicji hello hello cloudSOAExchMailbox atrybutu, który znajduje się w obszarze reguły synchronizacji out-of-box "W z usługi AAD — użytkownika hybrydowym programu Exchange", został zaktualizowany od:

```
CBool(IIF(IsNullOrEmpty([cloudMSExchRecipientDisplayType]),NULL,BitAnd([cloudMSExchRecipientDisplayType],&amp;HFF) = 0))
```

... toohello następujące czynności:

```
CBool(
  IIF(IsPresent([cloudMSExchRecipientDisplayType]),(
    IIF([cloudMSExchRecipientDisplayType]=0,True,(
      IIF([cloudMSExchRecipientDisplayType]=2,True,(
        IIF([cloudMSExchRecipientDisplayType]=7,True,(
          IIF([cloudMSExchRecipientDisplayType]=8,True,(
            IIF([cloudMSExchRecipientDisplayType]=10,True,(
              IIF([cloudMSExchRecipientDisplayType]=16,True,(
                IIF([cloudMSExchRecipientDisplayType]=17,True,(
                  IIF([cloudMSExchRecipientDisplayType]=18,True,(
                    IIF([cloudMSExchRecipientDisplayType]=1073741824,True,(
                       IF([cloudMSExchRecipientDisplayType]=1073741840,True,False)))))))))))))))))))),False))

```

* Witaj dodano następujące zestaw funkcji X509Certificate2 zgodnego do tworzenia wartości certyfikatu toohandle wyrażenia reguły synchronizacji w atrybucie certyfikatu użytkownika hello:

    ||||
    | --- | --- | --- |
    |CertSubject|CertIssuer|CertKeyAlgorithm|
    |CertSubjectNameDN|CertIssuerOid|CertNameInfo|
    |CertSubjectNameOid|CertIssuerDN|IsCert|
    |CertFriendlyName|certThumbprint|CertExtensionOids|
    |CertFormat|CertNotAfter|CertPublicKeyOid|
    |CertSerialNumber|CertNotBefore|CertPublicKeyParametersOid|
    |CertVersion|CertSignatureAlgorithmOid|Wybierz pozycję|
    |CertKeyAlgorithmParams|CertHashString|gdzie|
    |||Z|

* Następujące zmiany schematu zostały wprowadzone tooallow klientów toocreate niestandardowych reguł tooflow sAMAccountName, domainNetBios i domainFQDN dla grupy obiektów, a także distinguishedName obiektów użytkownika:

  * Schemat tooMV zostały dodane następujące atrybuty:
    * Grupa: Nazwa konta
    * Grupa: domainNetBios
    * Grupa: domainFQDN
    * Osoba: distinguishedName

  * Dodano następujące atrybuty tooAzure schematu w łączniku usługi AD:
    * Grupa: OnPremisesSamAccountName
    * Grupa: Nazwa NetBIOS
    * Grupa: NazwaDomenyDNS
    * Użytkownik: OnPremisesDistinguishedName

* Hello skryptu apletu polecenia ADSyncDomainJoinedComputerSync ma teraz nowe opcjonalny parametr o nazwie AzureEnvironment. Parametr Hello jest używany toospecify, które hello region odpowiedniego dzierżawcy usługi Azure Active Directory znajduje się w. Prawidłowe wartości to:
  * AzureCloud (ustawienie domyślne)
  * AzureChinaCloud
  * AzureGermanyCloud
  * USGovernment
 
* Zaktualizowano toouse Edytor reguł synchronizacji Join (zamiast udostępniania) hello domyślną wartość typu łącza podczas tworzenia reguły synchronizacji.

### <a name="ad-fs-management"></a>Zarządzanie usługami AD FS

#### <a name="issues-fixed"></a>Problemy z stałej

* Następujące adresy URL są nowe WS-Federation punkty końcowe wynikające z usługi Azure AD tooimprove odporność awarii uwierzytelniania i będą dodane lokalnych tooon odpowiedzi strony konfiguracji relacji zaufania usług AD FS:
  * https://ests.Login.microsoftonline.com/Login.srf
  * https://stamp2.Login.microsoftonline.com/Login.srf
  * https://ccs.Login.microsoftonline.com/Login.srf
  * https://ccs-sdf.Login.microsoftonline.com/Login.srf
  
* Rozwiązano problem powodujący wartość oświadczenia niepoprawne toogenerate usług AD FS dla IssuerID. Witaj problem występuje w przypadku wielu zweryfikowanych domen dzierżawy hello Azure AD i sufiks domeny hello toogenerate atrybut userPrincipalName hello hello IssuerID oświadczenia jest co najmniej 3 poziomy głębokości (na przykład johndoe@us.contoso.com). Witaj problem został rozwiązany przez zaktualizowanie hello wyrażenie regularne używane przez reguły oświadczeń hello.

#### <a name="new-features-and-improvements"></a>Nowe funkcje i ulepszenia
* Wcześniej funkcja Zarządzanie certyfikatami programu AD FS hello udostępniane przez usługi Azure AD Connect można używać tylko z farmy usług AD FS zarządzanych za pomocą usługi Azure AD Connect. Teraz funkcja hello z farmy usług AD FS, które nie są zarządzane za pomocą usługi Azure AD Connect.

## <a name="115240"></a>1.1.524.0
Zwolnione: 2017 maja

> [!IMPORTANT]
> Brak schematu i synchronizacji reguły wprowadzone w tej kompilacji. Azure AD Connect usługi synchronizacji wyzwoli pełny Import i pełną synchronizację czynności po uaktualnieniu. Szczegółowe informacje o zmianach hello są opisane poniżej.
>
>

**Rozwiązane problemy:**

Synchronizacja programu Azure AD Connect

* Rozwiązano problem powodujący automatyczne uaktualnienie toooccur na powitania serwera Azure AD Connect, nawet jeśli klient ma wyłączone hello funkcji przy użyciu polecenia cmdlet Set-ADSyncAutoUpgrade hello. Ta poprawka hello automatyczne uaktualnienie proces na serwerze hello nadal sprawdza, czy uaktualnienie okresowo, ale hello pobrany Instalator będzie honorować hello konfiguracja automatycznego uaktualnienia.
* Podczas uaktualniania w miejscu narzędzia DirSync Azure AD Connect tworzy toobe konta usługi dla usługi Azure AD używane przez łącznik hello Azure AD dla synchronizacji z usługą Azure AD. Po utworzeniu konta hello Azure AD Connect jest uwierzytelniany w usłudze Azure AD przy użyciu konta hello. Czasami, uwierzytelnianie nie powiedzie się z powodu przejściowych problemów, co z kolei powoduje, że toofail uaktualnienia narzędzia DirSync w miejscu z powodu błędu *"Wystąpił błąd podczas wykonywania zadań Konfiguruj AAD Sync: AADSTS50034: toosign do tej aplikacji hello konta należy dodać katalog xxx.onmicrosoft.com toohello."* odporność hello tooimprove uaktualnienia narzędzia DirSync, Azure AD Connect teraz ponowi próbę hello uwierzytelniania kroku.
* Wystąpił problem z kompilacją 443 powodujący toosucceed uaktualnienia narzędzia DirSync w miejscu, ale nie zostaną utworzone profile uruchamiania wymagane do synchronizacji katalogów. Naprawianie logiki znajduje się w tej kompilacji programu Azure AD Connect. Po uaktualnieniu klienta kompilacji toothis Azure AD Connect wykrywa brak profilów uruchamiania i tworzy je.
* Rozwiązano problem powodujący toostart toofail procesu synchronizacji haseł z 6900 identyfikator zdarzenia i błąd *"Element o takim samym kluczu został już dodany hello"*. Ten problem występuje, gdy aktualizacja filtrowania partycji konfiguracji tooinclude AD konfiguracji jednostki Organizacyjnej. Ten problem, synchronizacja haseł teraz przetworzyć toofix synchronizuje zmiany hasła z tylko partycji domeny AD. Partycje niezwiązanego z domeną, takie jak partycja konfiguracji są pomijane.
* Podczas instalacji ekspresowej, Azure AD Connect tworzy lokalne usługi AD DS konto używane przez toocommunicate łącznika hello AD z lokalnymi toobe AD. Poprzednio hello konto zostało utworzone z flagą PASSWD_NOTREQD hello ustawioną na powitania atrybut kontroli konta użytkownika i losowe hasło jest ustawiony na powitania konta. Teraz Azure AD Connect jawnie usuwa flagę PASSWD_NOTREQD hello, po hello hasła jest ustawiony na powitania konta.
* Rozwiązano problem powodujący toofail uaktualnienia narzędzia DirSync z powodu błędu *"do kontroli nastąpiło zakleszczenie w programie sql server które tooacquire w trakcie blokady aplikacji"* gdy atrybut mailNickname hello znajduje się w hello schematu usług AD lokalnymi, ale nie jest ograniczone toohello klasy obiektów użytkowników usługi AD.
* Stały, problem powodujący tooautomatically funkcji zapisywania zwrotnego urządzeń można wyłączyć, gdy administrator aktualizuje konfiguracji synchronizacji usługi Azure AD Connect przy użyciu Kreatora Azure AD Connect. Jest to spowodowane wyboru wstępnych wykonywania kreatora hello Konfiguracja hello do zapisywania zwrotnego istniejących urządzeń w lokalnej usłudze AD i hello sprawdzenie nie powiedzie się. poprawka Hello jest tooskip hello wyboru jeśli zapisu zwrotnego urządzeń jest już włączone wcześniej.
* tooconfigure filtrowania jednostki Organizacyjnej, można użyć Kreator Azure AD Connect hello lub hello Menedżera usługi synchronizacji. Wcześniej, korzystając z filtrowania hello Azure AD Connect kreatora tooconfigure jednostki Organizacyjnej, nowe jednostki organizacyjne utworzone później są dołączone do synchronizacji katalogów. Jeśli nie chcesz, aby nowe toobe jednostek organizacyjnych uwzględnione, należy skonfigurować jednostkę Organizacyjną filtrowanie przy użyciu hello Synchronization Service Manager. Teraz można osiągnąć hello takie samo zachowanie Kreator Azure AD Connect.
* Rozwiązano problem powodujący procedur składowanych wymagane przez utworzone na podstawie schematu hello hello instalowanie administratora, a nie w schemacie dbo hello toobe Azure AD Connect.
* Rozwiązano problem powodujący atrybutu TrackingId hello zwrócony przez toobe usługi Azure AD, które zostały pominięte w hello dzienniki zdarzeń serwera usługi AAD Connect. Witaj problem występuje, gdy Azure AD Connect odbiera komunikat przekierowania z usługi Azure AD i Azure AD Connect jest podany punkt końcowy toohello tooconnect. Hello TrackingId jest używany przez pracowników działu pomocy technicznej toocorrelate z dziennikami po stronie usługi podczas rozwiązywania problemów.
* Azure AD Connect odbierze błąd LargeObject z usługi Azure AD, Azure AD Connect generuje zdarzenia EventID 6941 i komunikat *"hello elastycznie obiektu jest zbyt duży. Przytnij hello liczbę wartości atrybutów dla tego obiektu."* Na powitania sam czas, Azure AD Connect również generuje mylących zdarzenia EventID 6900 i komunikat *"Microsoft.Online.Coexistence.ProvisionRetryException: toocommunicate z systemu Windows hello usługi Azure Active Directory."* toominimize pomyłek, Azure już AD Connect generuje hello ostatnie zdarzenie, gdy zostanie odebrany błąd LargeObject.
* Rozwiązano problem powodujący hello toobecome Menedżera usługi synchronizacji odpowiadać podczas próby konfiguracji hello tooupdate ogólny łącznik LDAP.

**Nowe funkcje/ulepszenia:**

Synchronizacja programu Azure AD Connect
* Synchronizacja zmian reguły — hello następujące zmiany reguły synchronizacji zostały wdrożone:
  * Zestaw reguł synchronizacji zaktualizowany domyślny toonot atrybuty eksportu **userCertificate** i **userSMIMECertificate** Jeśli hello atrybutów ma więcej niż 15 wartości.
  * Atrybuty AD **identyfikator pracownika** i **msExchBypassModerationLink** znajdują się teraz w zestawie reguł synchronizacji domyślne hello.
  * Atrybut AD **fotografii** została usunięta z domyślnego zestawu reguł synchronizacji.
  * Dodaje **preferredDataLocation** toohello Metaverse schematu i schematu łącznika usługi AAD. Klienci, którzy mają niestandardowe tooupdate obu atrybutów w usłudze Azure AD można zaimplementować tak synchronizacji toodo reguły. toofind więcej informacji na temat atrybutu hello można znaleźć w sekcji tooarticle [synchronizacja programu Azure AD Connect: jak toomake toohello zmiany domyślnej konfiguracji — Włączanie synchronizacji PreferredDataLocation](active-directory-aadconnectsync-change-the-configuration.md#enable-synchronization-of-preferreddatalocation).
  * Dodaje **userType** toohello Metaverse schematu i schematu łącznika usługi AAD. Klienci, którzy mają niestandardowe tooupdate obu atrybutów w usłudze Azure AD można zaimplementować tak synchronizacji toodo reguły.

* Azure AD Connect teraz automatycznie włącza hello użycie atrybutu ConsistencyGuid jako atrybut zakotwiczenia źródła hello lokalnymi obiektami usługi AD. Ponadto, Azure AD Connect wypełnia hello ConsistencyGuid atrybutu o wartości atrybut objectGuid hello, jeśli jest pusty. Ta funkcja jest tylko odpowiednie toonew wdrożenia. toofind więcej informacji na temat tej funkcji można znaleźć w sekcji tooarticle [Azure AD Connect: zagadnienia dotyczące — przy użyciu msDS-ConsistencyGuid jako sourceAnchor projektowania](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).
* Nowe, rozwiązywanie problemów z polecenia cmdlet Invoke-ADSyncDiagnostics został dodany toohelp diagnozowanie synchronizacji skrótu hasła problemy związane z. Informacji o używaniu hello polecenia cmdlet, można znaleźć w temacie tooarticle [Rozwiązywanie problemów z synchronizacją hasła z synchronizacji Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-troubleshoot-password-synchronization).
* Azure AD Connect teraz obsługuje Synchronizowanie folderu publicznego Mail-Enabled obiektów z lokalnej usługi AD tooAzure AD. Można włączyć funkcję hello za pomocą Kreatora Azure AD Connect w funkcji opcjonalnych. toofind więcej informacji na temat tej funkcji można znaleźć tooarticle [Office 365 katalogu na podstawie krawędzi blokuje obsługę lokalnej poczty włączone folderów publicznych](https://blogs.technet.microsoft.com/exchange/2017/05/19/office-365-directory-based-edge-blocking-support-for-on-premises-mail-enabled-public-folders).
* Azure AD Connect wymaga toosynchronize konta usług AD DS z lokalnej usługi AD. Wcześniej Jeśli zainstalowana Azure AD Connect w trybie hello Express, można podać poświadczenia konta administratora przedsiębiorstwa hello i Azure AD Connect utworzyć wymagane konta hello usług AD DS. Jednak do instalacji niestandardowej i dodawania istniejącego wdrożenia tooan lasów, było wymagane tooprovide hello konta usług AD DS zamiast tego. Teraz masz również hello opcja tooprovide hello poświadczeń konta administratora przedsiębiorstwa podczas instalacji niestandardowej i pozwolić, aby utworzyć wymagane konto usługi AD DS hello Azure AD Connect.
* Azure AD Connect obsługuje teraz SQL AOA. Przed zainstalowaniem usługi Azure AD Connect, należy włączyć SQL AOA. Podczas instalacji Azure AD Connect wykrywa, czy podane wystąpienie programu SQL hello jest włączone dla SQL AOA. Po włączeniu SQL AOA Azure dalsze AD Connect danych liczbowych czy SQL AOA jest skonfigurowany toouse synchronicznego lub asynchronicznego replikacji. Podczas konfigurowania hello odbiornika grupy dostępności, zaleca się ustawienie hello RegisterAllProvidersIP właściwości too0. Jest to spowodowane Azure AD Connect aktualnie używa programu SQL Native Client tooconnect tooSQL i SQL Native Client nie obsługuje użycia hello właściwości MultiSubNetFailover.
* Jeśli używasz LocalDB jako hello bazy danych dla serwera programu Azure AD Connect i osiągnęła swój limit rozmiaru 10 GB, hello Usługa synchronizacji nie można uruchomić. Wcześniej należy tooperform ShrinkDatabase operacji na powitania LocalDB tooreclaim wystarczającej ilości miejsca dla bazy danych dla hello toostart usługi synchronizacji. Po której, użyj hello toodelete Menedżera usługi synchronizacji uruchomić tooreclaim historii więcej miejsca na bazy danych. Teraz można użyć toopurge polecenia cmdlet Start-ADSyncPurgeRunHistory uruchomiony historyczne dane z bazy danych LocalDB tooreclaim DB obszaru. Ponadto to polecenie cmdlet obsługuje tryb offline (określając hello — parametr w trybie offline) może być używana, jeśli hello Usługa synchronizacji nie jest uruchomiona. Uwaga: hello w trybie offline można tylko jeśli hello Usługa synchronizacji nie jest uruchomiona i hello baza danych używana jest LocalDB.
* wymagana tooreduce hello ilość miejsca do magazynowania, Azure AD Connect teraz kompresuje szczegóły błędu synchronizacji przed ich zapisaniem w LocalDB/baz danych. Podczas uaktualniania z wersji starszej wersji toothis Azure AD Connect, Azure AD Connect przeprowadza jednorazowe kompresji na istniejące informacje o błędzie synchronizacji.
* Wcześniej po zaktualizowaniu konfiguracji filtrowania jednostki Organizacyjnej, użytkownik musi ręcznie uruchomić pełny import tooensure istniejące obiekty są poprawnie uwzględniony/wykluczony z synchronizacji katalogów. Teraz, Azure AD Connect automatycznie wyzwala pełny import podczas następnej synchronizacji hello cyklu. Dalsze, pełny import jest tylko łączniki zastosowane toohello AD hello aktualizacja dotyczy. Uwaga: To ulepszenie jest tooOU odpowiednie filtrowanie aktualizacji zostało nawiązane przy użyciu tylko kreatora hello Azure AD Connect. Nie jest stosowane tooOU filtrowania aktualizacji, które zostało nawiązane przy użyciu hello Menedżera usługi synchronizacji.
* Poprzednio filtrowanie na podstawie grupy obsługuje użytkowników, grup i skontaktuj się z tylko obiekty. Teraz filtrowanie na podstawie grupy obsługuje również obiektów komputerów.
* Wcześniej można usunąć przestrzeni łącznika danych bez konieczności wyłączania harmonogramu synchronizacji Azure AD Connect. Teraz hello usuwania hello bloki Menedżera usługi synchronizacji danych przestrzeni łącznika, jeśli wykryje, że harmonogramu hello jest włączone. Co więcej ostrzeżenie jest zwracana tooinform klientów o utracie danych, usunięcie hello dane przestrzeni łącznika.
* Wcześniej musisz wyłączyć przekształcania programu PowerShell dla usługi Azure AD Connect kreatora toorun poprawnie. Ten problem zostanie rozwiązany częściowo. Można włączyć przekształcania programu PowerShell, korzystając z konfiguracji synchronizacji toomanage Kreator Azure AD Connect. Jeśli używasz konfiguracji usług AD FS toomanage Kreator Azure AD Connect, należy wyłączyć przekształcania programu PowerShell.



## <a name="114860"></a>1.1.486.0
Wydanie: Kwietnia 2017

**Rozwiązane problemy:**
* Rozwiązany problem hello, gdzie Azure AD Connect nie zostaną zainstalowane pomyślnie w zlokalizowanej wersji systemu Windows Server.

## <a name="114840"></a>1.1.484.0
Wydanie: Kwietnia 2017

**Znane problemy:**

* Ta wersja programu Azure AD Connect nie zostaną zainstalowane pomyślnie, jeśli spełnione są wszystkie warunki hello następujące warunki:
   1. Wykonywana albo instalacji narzędzia DirSync w miejscu świeże lub uaktualniania programu Azure AD Connect.
   2. Używasz zlokalizowanej wersji systemu Windows Server, w którym nazwa hello wbudowanej grupy administratorów na serwerze hello jest "Administratorzy".
   3. Używasz hello domyślnego programu SQL Server 2012 Express LocalDB, zainstalowane z programem Azure AD Connect zamiast podając własne pełne SQL.

**Rozwiązane problemy:**

Synchronizacja programu Azure AD Connect
* Rozwiązano problem, na którym hello harmonogramu synchronizacji pomija krok synchronizacji całego hello jeden lub więcej łączników braku profilu uruchamiania dla tego kroku synchronizacji. Na przykład ręcznie dodawać łącznik bez tworzenia Import zmian profilu uruchamiania go za pomocą hello Synchronization Service Manager. Ta poprawka gwarantuje, że ten harmonogram synchronizacji hello nadal toorun Import zmian dla innych łączników.
* Rozwiązano problem, w którym hello usługi synchronizacji natychmiastowe zatrzymanie przetwarzania profilu uruchamiania, gdy jest napotka jakiś problem, jeden z kroków hello Uruchom. Ta poprawka gwarantuje, że hello pomija usługi synchronizacji, które krok zostanie uruchomiony i kontynuuje tooprocess hello rest. Na przykład masz Import zmian, uruchom profilu dla użytkownika łącznika usługi AD z wielu kroków wykonywania (po jednej dla każdego lokalnej domeny usługi AD). Witaj Usługa synchronizacji zostanie uruchomiony Import zmian z hello inne domeny AD nawet wtedy, gdy jeden z nich ma problemy z połączeniem sieciowym.
* Rozwiązano problem powodujący toobe aktualizacji łącznika usługi Azure AD hello pominięte podczas automatycznego uaktualnienia.
* Rozwiązano problem tego przyczyny usługi Azure AD Connect tooincorrectly określają, czy hello serwer jest kontrolerem domeny podczas instalacji, który powoduje, że Wyłącz narzędzie DirSync toofail uaktualnienia.
* Stały, problem powodujący DirSync toonot uaktualnienia w miejscu utworzyć any Uruchom profilu hello łącznika usługi Azure AD.
* Rozwiązano problem, w którym interfejs użytkownika Menedżera usługi synchronizacji hello przestaje odpowiadać podczas próby tooconfigure ogólny łącznik LDAP.

Zarządzanie usługami AD FS
* Rozwiązano problem, w której Kreator Azure AD Connect hello zakończy się niepowodzeniem, jeśli węzeł podstawowy hello AD FS został przeniesiony tooanother serwera.

Usługa rejestracji Jednokrotnej pulpitu
* Rozwiązano problem hello Kreator Azure AD Connect, w którym hello ekranu logowania nie umożliwia włączenia funkcji logowania jednokrotnego pulpitu, jeśli została wybrana opcja synchronizacji haseł możliwość logowania podczas instalacji nowego.

**Nowe funkcje/ulepszenia:**

Synchronizacja programu Azure AD Connect
* Synchronizacji Azure AD Connect obsługuje teraz hello przy użyciu wirtualnego konta usługi, zarządzane konta usługi i konto usługi zarządzane przez grupę jako swojego konta usługi. Dotyczy to toonew instalacji programu Azure tylko AD Connect. Po zainstalowaniu programu Azure AD Connect:
    * Domyślnie Kreator Azure AD Connect spowoduje utworzenie wirtualnego konta usługi i używa go jako swojego konta usługi.
    * Jeśli instalujesz na kontrolerze domeny, Azure AD Connect powraca tooprevious zachowanie, gdy zostanie utworzone konto użytkownika domeny i używa go jako swojego konta usługi.
    * Hello domyślne zachowanie można przesłonić, udostępniając jedno z następujących hello:
      * Konto usługi zarządzane przez grupę
      * Zarządzane konto usługi
      * Konto użytkownika domeny
      * Konto użytkownika lokalnego
* Wcześniej po uaktualnieniu tooa nowej kompilacji programu Azure AD Connect zawierający łączniki aktualizacji lub zmian reguły synchronizacji, Azure AD Connect wyzwoli cyklu pełnej synchronizacji. Teraz Azure AD Connect selektywnie wyzwala pełny Import krok tylko dla łączników o aktualizacji i pełną synchronizację tylko dla łączników o zmian reguły synchronizacji.
* Wcześniej hello progu usuwania eksportu ma zastosowanie tylko tooexports, które są uruchamiane za pośrednictwem hello harmonogramu synchronizacji. Eksporty tooinclude ręcznie wyzwalane przez powitania klienta przy użyciu hello Synchronization Service Manager jest rozszerzona funkcja hello.
* Na dzierżawy usługi Azure AD jest konfiguracji usługi, która wskazuje, czy funkcja synchronizacji haseł jest włączone dla dzierżawy. Wcześniej jest łatwe toobe konfiguracji usługi hello niepoprawnie skonfigurowany przy użyciu usługi Azure AD Connect, jeśli masz aktywnego i serwerze tymczasowym. Teraz, Azure AD Connect będzie podejmować konfiguracji usługi hello tookeep zgodne z aktywnych tylko serwera Azure AD Connect.
* Azure AD Connect, Kreator teraz wykrywa i zwraca ostrzeżenie, jeśli lokalnej usługi AD nie ma Kosz usługi AD włączone.
* Wcześniej tooAzure eksportu AD upłynie limit czasu i kończy się niepowodzeniem, jeśli hello łączny rozmiar obiektów hello w partii hello przekracza określony próg. Teraz hello usługi synchronizacji ponów tooresend hello obiektów w oddzielnych, krótszych partiach po napotkaniu hello problem.
* Zarządzanie kluczami usługi synchronizacji aplikacji Hello został usunięty z Menu Start systemu Windows. Zarządzanie klucza szyfrowania będą obsługiwane za pośrednictwem interfejsu wiersza polecenia przy użyciu miiskmu.exe toobe. Informacje o zarządzaniu klucz szyfrowania, zobacz tooarticle [klucza szyfrowania programu Abandoning hello Azure AD Connect synchronizacji](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-change-serviceacct-pass#abandoning-the-azure-ad-connect-sync-encryption-key).
* Wcześniej Jeśli zmienisz hasło konta usługi synchronizacji Azure AD Connect hello hello usługi synchronizacji nie będą mogli start poprawnie dopiero po porzucone hello klucza szyfrowania i ponownie zainicjować hasło konta usługi synchronizacji Azure AD Connect hello. Teraz to nie jest już wymagane.

Usługa rejestracji Jednokrotnej pulpitu

* Kreator Azure AD Connect nie wymaga już otwarte na powitania sieci podczas konfigurowania uwierzytelniania przekazywanego i logowania jednokrotnego pulpitu toobe 9090 portu. Wyłącznie port 443 jest wymagana. 

## <a name="114430"></a>1.1.443.0
Wydanie: 2017 marca

**Rozwiązane problemy:**

Synchronizacja programu Azure AD Connect
* Rozwiązano problem, co powoduje toofail Kreator Azure AD Connect, jeśli nazwa wyświetlana hello hello łącznika usługi Azure AD nie zawiera hello onmicrosoft.com początkowej domenie przypisane toohello usługi Azure AD dzierżawy.
* Rozwiązano problem, co powoduje, że podczas tworzenia bazy danych tooSQL połączenia, gdy hello hasło konta usługi synchronizacji hello zawiera znaki specjalne, takich jak apostrof, dwukropek i miejsca toofail Kreator Azure AD Connect.
* Rozwiązano problem, co powoduje, że błąd powitania "hello dimage ma kotwicy, który jest inny niż obraz powitania" toooccur na serwerze programu Azure AD Connect w tryb przejściowy, po tymczasowo wykluczono lokalnego AD obiektu synchronizowanie i włączone go ponownie Trwa synchronizowanie.
* Rozwiązano problem, co powoduje, że błąd hello toooccur "zlokalizowana nazwa Wyróżniająca obiektu hello jest Fantom" na serwerze programu Azure AD Connect w tryb przejściowy, po tymczasowo wykluczono lokalnego AD obiektu synchronizowanie i włączone go ponownie do synchronizowania.

Zarządzanie usługami AD FS
* Rozwiązano problem której Kreator Azure AD Connect nie Zaktualizuj konfigurację usług AD FS i ustaw hello prawo oświadczenia na powitania zaufanie jednostki uzależnionej, po skonfigurowaniu alternatywnego Identyfikatora logowania.
* Rozwiązano problem w przypadku toocorrectly dojścia AD FS serwerów, których konta usługi są skonfigurowane przy użyciu formatu userPrincipalName zamiast formatu sAMAccountName Kreator Azure AD Connect.

Uwierzytelnianie przekazywane
* Rozwiązano problem, co powoduje toofail Kreator Azure AD Connect, jeśli wybrano opcję przekazywane za pośrednictwem uwierzytelniania, ale rejestracji jego łącznika nie powiedzie się.
* Rozwiązano problem, co powoduje, że usługa Azure AD Connect, sprawdzanie poprawności toobypass kreatora na wybrany, gdy jest włączona funkcja logowania jednokrotnego pulpitu metoda logowania.

Resetowanie hasła
* Rozwiązano problem, co może spowodować hello Azure AAD Connect serwera toonot próba toore-połączenia, jeśli połączenie hello został przerwany przez zapory lub serwera proxy.

**Nowe funkcje/ulepszenia:**

Synchronizacja programu Azure AD Connect
* Polecenie cmdlet Get-ADSyncScheduler teraz zwraca nową właściwość typu Boolean o nazwie SyncCycleInProgress. Jeśli hello zwrócił wartość ma wartość true, oznacza to, że występuje cykl zaplanowanej synchronizacji w toku.
* Folderu docelowego dla instalacji usługi Azure AD Connect i dzienniki Instalatora zostały przeniesione z plików dziennika toohello %localappdata%\AADConnect too%programdata%\AADConnect tooimprove ułatwień dostępu.

Zarządzanie usługami AD FS
* Dodano obsługę aktualizacji certyfikat SSL usług AD FS farmy.
* Dodano obsługę zarządzania usługą AD FS 2016.
* Możesz teraz określić istniejącą grupę (grupy zarządzanych kont usług), podczas instalacji usług AD FS.
* Można teraz skonfigurować algorytmu SHA-256 jako hello algorytmu wyznaczania wartości skrótu podpisu dla zaufania jednostki uzależnionej usługi Azure AD.

Resetowanie hasła
* Wprowadzono ulepszenia tooallow hello produktu toofunction w środowiskach z bardziej rygorystyczne reguły zapory.
* Połączenie lepszą niezawodność tooAzure usługi Service Bus.

## <a name="113800"></a>1.1.380.0
Wydanie: Grudnia 2016

**Rozwiązany problem:**

* W tej kompilacji brakuje problem stałego hello gdzie hello issuerid reguł oświadczeń dla usługi Active Directory Federation Services (AD FS).

>[!NOTE]
>Ta kompilacja nie jest dostępna toocustomers za pomocą hello Azure AD Connect automatycznego uaktualnienia funkcji.

## <a name="113710"></a>1.1.371.0
Wydanie: Grudnia 2016

**Znany problem:**

* w tej kompilacji brakuje reguły oświadczeń issuerid powitania dla usług AD FS. reguły oświadczeń issuerid Hello jest wymagany, jeśli są federowanie wielu domen z usługi Azure Active Directory (Azure AD). Jeśli używasz usługi Azure AD Connect toomanage lokalnego wdrożenia usług AD FS, uaktualnianie kompilacji toothis usuwa istniejącą regułę oświadczeń issuerid hello z konfiguracji programu AD FS. Witaj problem można obejść przez dodanie reguły oświadczeń issuerid powitania po hello instalacja/aktualizacja. Szczegółowe informacje na temat dodawania hello issuerid oświadczenia reguły, znajduje się w artykule toothis w [Obsługa wielu domen do federowania w usłudze Azure AD](active-directory-aadconnect-multiple-domains.md).

**Rozwiązany problem:**

* Jeśli Port 9090 nie jest otwarty dla połączenia wychodzącego hello, hello Azure AD Connect instalacji lub uaktualniania zakończy się niepowodzeniem.

>[!NOTE]
>Ta kompilacja nie jest dostępna toocustomers za pomocą hello Azure AD Connect automatycznego uaktualnienia funkcji.

## <a name="113700"></a>1.1.370.0
Wydanie: Grudnia 2016

**Znane problemy:**

* w tej kompilacji brakuje reguły oświadczeń issuerid powitania dla usług AD FS. reguły oświadczeń issuerid Hello jest wymagany, jeśli są federowanie wielu domen z usługą Azure AD. Jeśli używasz usługi Azure AD Connect toomanage lokalnego wdrożenia usług AD FS, uaktualnianie kompilacji toothis usuwa istniejącą regułę oświadczeń issuerid hello z konfiguracji programu AD FS. Hello problem można obejść przez dodanie reguły oświadczeń issuerid powitania po instalacja/aktualizacja. Aby uzyskać więcej informacji na temat dodawania issuerid reguł oświadczeń, znajduje się w artykule toothis w [Obsługa wielu domen do federowania w usłudze Azure AD](active-directory-aadconnect-multiple-domains.md).
* Port 9090 musi być otwarte toocomplete wychodzącego instalacji.

**Nowe funkcje:**

* Uwierzytelniania przekazywanego (wersja zapoznawcza).

>[!NOTE]
>Ta kompilacja nie jest dostępna toocustomers za pomocą hello Azure AD Connect automatycznego uaktualnienia funkcji.

## <a name="113430"></a>1.1.343.0
Wydanie: Listopada 2016

**Znany problem:**

* w tej kompilacji brakuje reguły oświadczeń issuerid powitania dla usług AD FS. reguły oświadczeń issuerid Hello jest wymagany, jeśli są federowanie wielu domen z usługą Azure AD. Jeśli używasz usługi Azure AD Connect toomanage lokalnego wdrożenia usług AD FS, uaktualnianie kompilacji toothis usuwa istniejącą regułę oświadczeń issuerid hello z konfiguracji programu AD FS. Hello problem można obejść przez dodanie reguły oświadczeń issuerid powitania po instalacja/aktualizacja. Aby uzyskać więcej informacji na temat dodawania issuerid reguł oświadczeń, znajduje się w artykule toothis w [Obsługa wielu domen do federowania w usłudze Azure AD](active-directory-aadconnect-multiple-domains.md).

**Rozwiązane problemy:**

* Czasami zainstalowaniu programu Azure AD Connect nie działa, ponieważ jest toocreate konto Usługa lokalna, którego hasło spełnia hello poziom złożoności określone przez zasady haseł hello organizacji.
* Rozwiązano problem, w którym sprzężenia reguły są nie ponownie oceniane po obiektu w przestrzeni łącznika hello jednocześnie staje się poza zakresem dla jednego dołączyć regułę i stać się w zakresie dla innej. Może to nastąpić, jeśli istnieje co najmniej dwa reguł sprzężenia, których warunki sprzężenia wzajemnie się wykluczają.
* Rozwiązano problem, w której reguły synchronizacji ruchu przychodzącego (z usługi Azure AD), które nie zawierają zasady sprzężenia, nie są przetwarzane, gdy mają niższe wartości pierwszeństwa niż zawierających zasady sprzężenia.

**Ulepszenia:**

* Dodano obsługę zainstalowaniu programu Azure AD Connect w systemie Windows Server 2016 Standard lub nowszego.
* Dodano obsługę programu Azure AD Connect przy użyciu programu SQL Server 2016 jako hello zdalnej bazy danych.

## <a name="112810"></a>1.1.281.0
Wydanie: Sierpnia 2016

**Rozwiązane problemy:**

* Interwał toosync zmiany dopiero po miejsce po hello zakończeniu następnego cyklu synchronizacji.
* Kreator Azure AD Connect nie akceptuje konto usługi Azure AD, którego nazwa użytkownika, który rozpoczyna się od znaku podkreślenia (\_).
* Konto usługi Azure AD hello tooauthenticate Kreator Azure AD Connect nie powiedzie się, jeśli hasło konta hello zawiera zbyt wiele znaków specjalnych. Komunikat o błędzie "toovalidate poświadczenia. Wystąpił nieoczekiwany błąd." jest zwracany.
* Odinstalowywanie serwera na potrzeby przemieszczania powoduje wyłączenie synchronizacji haseł w dzierżawie usługi Azure AD i powoduje toofail synchronizacji haseł z aktywnego serwera.
* Synchronizacja haseł nie powiedzie się w przypadkach zdarza po nie skrót hasła przechowywane na powitania użytkownika.
* Po włączeniu trybu przejściowego serwera Azure AD Connect funkcji zapisywania zwrotnego haseł nie jest tymczasowo wyłączone.
* Kreator Azure AD Connect nie są wyświetlane, synchronizacja haseł rzeczywiste hello i konfiguracji funkcji zapisywania zwrotnego haseł, gdy serwer jest w trybie przejściowym. Zawsze przedstawia on je jako wyłączone.
* Synchronizacji toopassword zmian konfiguracji i zapisywania zwrotnego haseł nie są zachowywane przez Kreator Azure AD Connect, gdy serwer jest w trybie przejściowym.

**Ulepszenia:**

* Czy jest możliwe toosuccessfully start nowy cykl synchronizacji lub nie, należy zaktualizować hello Start ADSyncSyncCycle tooindicate polecenia cmdlet.
* Cykl synchronizacji tooterminate polecenia cmdlet dodano hello Stop-ADSyncSyncCycle i operacji, znajdujących się obecnie w toku.
* Cykl synchronizacji tooterminate polecenia cmdlet zaktualizowane hello Stop-ADSyncScheduler i operacji, znajdujących się obecnie w toku.
* Podczas konfigurowania [rozszerzenia katalogów](active-directory-aadconnectsync-feature-directory-extensions.md) w Kreator Azure AD Connect, teraz być zaznaczone atrybut typu "Teletex ciągu" hello Azure AD.

## <a name="111890"></a>1.1.189.0
Wydanie: Czerwca 2016 r.

**Rozwiązane problemy i ulepszenia:**

* Teraz można zainstalować na serwerze zgodne ze standardem FIPS Azure AD Connect.
  * Aby synchronizować hasła, zobacz [synchronizacji haseł i FIPS](active-directory-aadconnectsync-implement-password-synchronization.md#password-synchronization-and-fips).
* Rozwiązano problem, w którym nazwa NetBIOS nie można rozpoznać toohello nazwy FQDN w hello łącznika usługi Active Directory.

## <a name="111800"></a>1.1.180.0
Wydanie: Maj 2016

**Nowe funkcje:**

* Ostrzeżenie i pomaga zweryfikować domeny, jeśli nie zostało to zrobić przez uruchomienie programu Azure AD Connect.
* Dodano obsługę [Niemcy Microsoft Cloud](active-directory-aadconnect-instances.md#microsoft-cloud-germany).
* Dodano obsługę najnowszych hello [chmury Microsoft Azure dla instytucji rządowych](active-directory-aadconnect-instances.md#microsoft-azure-government-cloud) infrastruktury z nowymi wymaganiami adresu URL.

**Rozwiązane problemy i ulepszenia:**

* Dodano toohello filtrowania toomake Edytor reguł synchronizacji go łatwo toofind reguły synchronizacji.
* Zwiększona wydajność podczas usuwania przestrzeni łącznika.
* Rozwiązano problem, gdy hello tego samego obiektu został usunięty i dodany hello sam Uruchom (zwane delete/add).
* Wyłączone synchronizacji już reguły włączające zawierają obiekty i Odśwież atrybuty schematu katalogu lub uaktualniania.

## <a name="111300"></a>1.1.130.0
Wydanie: Kwietnia 2016

**Nowe funkcje:**

* Dodano obsługę atrybuty wielowartościowe zbyt[rozszerzenia katalogów](active-directory-aadconnectsync-feature-directory-extensions.md).
* Dodano obsługę więcej zmian konfiguracji dla [automatyczne uaktualnianie](active-directory-aadconnect-feature-automatic-upgrade.md) toobe kwalifikuje się do uaktualnienia.
* Dodane niektóre polecenia cmdlet dla [harmonogramu niestandardowego](active-directory-aadconnectsync-feature-scheduler.md#custom-scheduler).

## <a name="111190"></a>1.1.119.0
Wydanie: Marca 2016

**Rozwiązane problemy:**

* Wprowadzone się, że instalacja ekspresowa nie można użyć w systemie Windows Server 2008 (pre-R2), ponieważ synchronizacja hasła nie jest obsługiwana w tym systemie operacyjnym.
* Uaktualnienie z narzędzia DirSync z konfiguracją niestandardowego filtru nie działają zgodnie z oczekiwaniami.
* Podczas uaktualniania tooa nowszą wersją istnieją zmiany konfiguracji toohello, pełny import/synchronizacji nie powinny zostać zaplanowane.

## <a name="111100"></a>1.1.110.0
Wydanie: Lutego 2016

**Rozwiązane problemy:**

* Uaktualnienie z wcześniejszych wersjach nie działa, jeśli instalacja hello nie jest w folderze C:\Program Files domyślnym hello.
* Jeśli po zainstalowaniu wyczyść **Uruchom proces synchronizacji hello** końcem hello Kreatora instalacji hello uruchomiony Kreator instalacji powitania po raz drugi nie dają hello harmonogramu.
* Witaj harmonogramu nie działa zgodnie z oczekiwaniami na serwerach, w których hello US en format daty i godziny nie jest używany. Zostanie również zablokować `Get-ADSyncScheduler` tooreturn prawidłowego czasu.
* Jeśli zainstalowano wcześniejszych wersji programu Azure AD Connect z usługami AD FS jako hello opcji logowania i uaktualniania, Kreator instalacji hello nie można uruchomić ponownie.

## <a name="111050"></a>1.1.105.0
Wydanie: Lutego 2016

**Nowe funkcje:**

* [Automatyczne uaktualnianie](active-directory-aadconnect-feature-automatic-upgrade.md) funkcji Express ustawienia klientów.
* Obsługa hello administratora globalnego przy użyciu usługi Azure Multi-Factor Authentication i Privileged Identity Management w Kreatorze instalacji hello.
  * Należy tooallow tooalso Twojego serwera proxy Zezwalaj toohttps://secure.aadcdn.microsoftonline-p.com ruch, jeśli używane jest uwierzytelnianie wieloskładnikowe.
  * Należy listy zaufanych witryn tooyour https://secure.aadcdn.microsoftonline-p.com tooadd pracy tooproperly usługi Multi-Factor Authentication.
* Zezwalaj na zmienianie metody logowania użytkownika powitania po wstępnej instalacji.
* Zezwalaj na [domenę i jednostkę Organizacyjną filtrowania](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) hello Kreatora instalacji. Dzięki temu, łączenie tooforests, w którym nie wszystkie domeny są dostępne.
* [Harmonogram](active-directory-aadconnectsync-feature-scheduler.md) korzysta z wbudowanej w toohello aparatu synchronizacji.

**Funkcje awansowana z tooGA podglądu:**

* [Zapisywanie zwrotne urządzeń](active-directory-aadconnect-feature-device-writeback.md).
* [Rozszerzenia katalogów](active-directory-aadconnectsync-feature-directory-extensions.md).

**Nowe funkcje w wersji zapoznawczej:**

* Witaj nowego domyślnego cyklu synchronizacji interwał wynosi 30 minut. Używane toobe trzy godziny dla wszystkich wcześniejszych wersjach. Dodaje obsługę toochange hello [harmonogramu](active-directory-aadconnectsync-feature-scheduler.md) zachowanie.

**Rozwiązane problemy:**

* Hello Sprawdź, czy strona domen DNS zawsze nie rozpoznał hello domen.
* Wyświetla monit o poświadczenia administratora domeny, podczas konfigurowania usług AD FS.
* Witaj w lokalnym kont usługi AD nie są rozpoznawane przez Kreatora instalacji hello, jeśli znajduje się w domenie z innego drzewa DNS niż hello domeny głównej.

## <a name="1091310"></a>1.0.9131.0
Wydanie: Grudnia 2015 r.

**Rozwiązane problemy:**

* Synchronizacja haseł może nie działać po zmianie hasła w usługach domenowych w usłudze Active Directory (AD DS), ale działa w przypadku ustawienia hasła.
* Jeśli masz serwer proxy tooAzure uwierzytelniania, który AD może zakończyć się niepowodzeniem podczas instalacji lub uaktualniania zostało anulowane na stronie konfiguracji hello.
* Uaktualnianie z poprzedniej wersji programu Azure AD Connect przy użyciu pełnego wystąpienia programu SQL Server kończy się niepowodzeniem, jeśli nie jesteś administratorem systemu (SA) programu SQL Server.
* Uaktualnianie z poprzedniej wersji programu Azure AD Connect ze zdalnym serwerem SQL zawiera hello błędu "baza danych ADSync SQL tooaccess hello".

## <a name="1091250"></a>1.0.9125.0
Wydanie: Listopad 2015

**Nowe funkcje:**

* Można ponownie skonfigurować usługi AD FS tooAzure AD zaufania.
* Można odświeżyć hello schemat usługi Active Directory i ponownie wygenerować reguły synchronizacji.
* Można wyłączyć reguły synchronizacji.
* Można zdefiniować "AuthoritativeNull" jako literału nowej reguły synchronizacji.

**Nowe funkcje w wersji zapoznawczej:**

* [Azure AD Connect Health dla synchronizacji](../connect-health/active-directory-aadconnect-health-sync.md).
* Obsługa [usług domenowych Azure AD](../active-directory-passwords-update-your-own-password.md) synchronizacji haseł.

**Nowy scenariusz obsługiwane:**

* Obsługuje wiele lokalnej organizacji programu Exchange. Aby uzyskać więcej informacji, zobacz [hybrydowych wdrożeń z wieloma lasami usługi Active Directory](https://technet.microsoft.com/library/jj873754.aspx).

**Rozwiązane problemy:**

* Problemy z synchronizacją hasła:
  * Obiekt został przeniesiony z zakresem jest poza zakresem tooin nie będzie miał jego hasło zsynchronizowane. W tym jednostki Organizacyjnej i filtrowanie atrybutów.
  * Wybranie nowego tooinclude jednostki Organizacyjnej w synchronizacji nie wymaga synchronizacji pełnej hasła.
  * Po włączeniu wyłączony użytkownik nie synchronizuje hasła hello.
  * Kolejka ponownych prób Hello hasło to nieskończoność i poprzednich limit 5000 toobe obiektów wycofane hello został usunięty.
* Nie można tooconnect tooActive katalogu z poziomem funkcjonalności lasu systemu Windows Server 2016.
* Grupa hello nie jest w stanie toochange służy do filtrowania grupy po początkowej instalacji hello.
* Nie tworzy nowy profil użytkownika, na serwerze usługi Azure AD Connect hello dla każdego użytkownika podczas zmiany hasła z włączoną zapisywania zwrotnego haseł.
* Nie można toouse długich liczb całkowitych wartości zakresy reguły synchronizacji.
* pole wyboru Hello "zapisu zwrotnego urządzeń" był wyłączony, jeśli ma kontrolerów domeny jest nieosiągalny.

## <a name="1086670"></a>1.0.8667.0
Wydanie: Sierpień 2015

**Nowe funkcje:**

* Hello Azure AD Connect, Kreator instalacji jest teraz zlokalizowane tooall języki systemu Windows Server.
* Dodano obsługę konta odblokowanie przy użyciu usługi Azure AD zarządzania hasłami.

**Rozwiązane problemy:**

* Kreator instalacji usługi Azure AD Connect ulegnie awarii, jeśli inny użytkownik będzie nadal występować, zamiast hello osoba pierwszego uruchomienia instalacji hello instalacji.
* Jeśli poprzednie dezinstalacji programu Azure AD Connect nie prawidłowo toouninstall synchronizacji Azure AD Connect, nie jest możliwe tooreinstall.
* Nie można zainstalować usługi Azure AD Connect przy użyciu instalacji ekspresowej, jeśli użytkownik hello nie jest w domenie głównej lasu hello hello lub użycie innej niż angielska wersji usługi Active Directory.
* Jeśli nie można rozpoznać hello FQDN hello konta użytkownika usługi Active Directory, jest wyświetlany mylących komunikat o błędzie "Nie powiodło się toocommit hello schematu".
* Jeśli konto hello używane na powitania łącznika usługi Active Directory została zmieniona poza hello kreatora, Kreator hello nie powiedzie się w kolejnych uruchomieniach.
* Azure AD Connect nie czasami tooinstall na kontrolerze domeny.
* Nie można włączać i wyłączać "Tryb przejściowy", jeśli zostały dodane atrybuty rozszerzenia.
* Zapisywanie zwrotne haseł kończy się niepowodzeniem w niektórych konfiguracjach ze względu na nieprawidłowe hasło na powitania łącznika usługi Active Directory.
* Nie można uaktualnić narzędzia DirSync, jeśli nazwa wyróżniająca (DN) jest używana w filtrowanie atrybutów.
* Nadmiernego użycia procesora CPU przy użyciu resetowania hasła.

**Funkcje usunięte w wersji zapoznawczej:**

* Funkcja w wersji zapoznawczej Hello [zapisu zwrotnego użytkowników](active-directory-aadconnect-feature-preview.md#user-writeback) tymczasowo usunięto oparte na opinie klientów w wersji zapoznawczej. Zostanie ona dodana ponownie później po rozwiązaliśmy hello podane opinii.

## <a name="1086410"></a>1.0.8641.0
Wydanie: Czerwiec 2015

**Początkowa wersja programu Azure AD Connect.**

Zmienione nazwy z usługi Azure AD Sync tooAzure AD Connect.

**Nowe funkcje:**

* [Ustawienia ekspresowe](active-directory-aadconnect-get-started-express.md) instalacji
* Można [skonfigurować usługi AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs)
* Można [uaktualnianie z narzędzia DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md)
* [Zapobieganie przypadkowemu usuwaniu](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)
* Wprowadzono [Tryb przejściowy](active-directory-aadconnectsync-operations.md#staging-mode)

**Nowe funkcje w wersji zapoznawczej:**

* [Zapisywanie zwrotne użytkowników](active-directory-aadconnect-feature-preview.md#user-writeback)
* [Zapisywanie zwrotne grup](active-directory-aadconnect-feature-preview.md#group-writeback)
* [Zapisywanie zwrotne urządzeń](active-directory-aadconnect-feature-device-writeback.md)
* [Rozszerzenia katalogów](active-directory-aadconnect-feature-preview.md)

## <a name="104940501"></a>1.0.494.0501
Wydanie: Maj 2015

**Nowe wymaganie:**

* Azure AD Sync wymaga teraz toobe wersji 4.5.1 .NET Framework hello zainstalowane.

**Rozwiązane problemy:**

* Zapisywanie zwrotne haseł z usługi Azure AD kończy się niepowodzeniem z powodu błędu połączenia usługi Azure Service Bus.

## <a name="104910413"></a>1.0.491.0413
Wydanie: Kwietnia 2015 r.

**Rozwiązane problemy i ulepszenia:**

* Witaj łącznika usługi Active Directory nie usuwa poprawnie przetworzyć Jeśli włączono Kosza hello i jest wiele domen w lesie hello.
* udoskonalono Hello wydajność operacji importu hello łącznika usługi Azure Active Directory.
* Gdy grupa przekroczyła limit członkostwa hello (domyślnie hello limit jest ustawiony too50, 000 obiektów), Usunięto grupę hello w usłudze Azure Active Directory. O nowe zachowania hello hello grupa nie zostanie usunięta, zostanie zgłoszony błąd i nowe zmiany członkostwa nie są eksportowane.
* Nie można zainicjować obsługi nowego obiektu, jeśli przemieszczanego Usuń z hello jest już w tej samej nazwy domeny znajdujących się w przestrzeni łącznika hello.
* Niektóre obiekty są oznaczone dla synchronizacji podczas synchronizacji różnicowej, nawet jeśli nie została zmieniona na obiekt hello przemieszczane.
* Wymuszanie synchronizacji haseł spowoduje również usunięcie hello preferowane listy kontrolerów domeny.
* CSExportAnalyzer ma problemy z niektórych stanów obiektów.

**Nowe funkcje:**

* Sprzężenia mogą teraz łączyć za "" typ obiektu w hello MV.

## <a name="104850222"></a>1.0.485.0222
Wydanie: Luty 2015

**Ulepszenia:**

* Ulepszone importowanie wydajności.

**Rozwiązane problemy:**

* Synchronizacja haseł honoruje hello cloudFiltered atrybut, który jest używany przez filtrowanie atrybutów. Obiekty filtrowane nie są już w zakresie synchronizacji haseł.
* W rzadkich sytuacji, gdy topologia hello miały dla wielu kontrolerów domeny synchronizacja haseł nie działa.
* Włączono "Zatrzymana server" podczas importowania z łącznika usługi Azure AD hello po zarządzania urządzeniami w usłudze Azure AD/usługi Intune.
* Dołączenie obce podmioty zabezpieczeń (FSP) z wielu domen w tym samym lesie, spowoduje wystąpienie błędu niejednoznaczne sprzężenia.

## <a name="104751202"></a>1.0.475.1202
Wydanie: Z grudnia 2014

**Nowe funkcje:**

* Synchronizacja haseł z filtrowanie na podstawie atrybutu jest teraz obsługiwane. Aby uzyskać więcej informacji, zobacz [synchronizacji haseł za pomocą filtrowania](active-directory-aadconnectsync-configure-filtering.md).
* atrybut msDS-identyfikatora ExternalDirectoryObjectID Hello są zapisywane tooActive katalogu. Ta funkcja dodaje obsługę aplikacji usługi Office 365. Używa protokołu OAuth2 tooaccess Online i lokalnego skrzynek pocztowych w ramach wdrożenia hybrydowego programu Exchange.

**Rozwiązane problemy uaktualnienia:**

* Nowsza wersja hello Asystenta logowania jest dostępna na powitania serwera.
* Ścieżka instalacji niestandardowej została używane tooinstall Azure AD Sync.
* Nieprawidłowy niestandardowy sprzężenia kryterium bloki hello uaktualnienia.

**Inne poprawki:**

* Stały hello szablonów dla pakietu Office Pro Plus.
* Problemy z instalacją stałym spowodowane przez użytkownika o nazwach zaczynających łącznikiem.
* Stałe powoduje utratę hello sourceAnchor ustawienie podczas uruchamiania Kreatora instalacji powitania po raz drugi.
* Stały śledzenia zdarzeń systemu Windows, aby synchronizować hasła.

## <a name="104701023"></a>1.0.470.1023
Wydanie: Października 2014 r.

**Nowe funkcje:**

* Synchronizację haseł z wieloma lokalnymi usługi Active Directory tooAzure AD.
* Instalacja zlokalizowanego interfejsu użytkownika tooall języki systemu Windows Server.

**Uaktualnianie z GA aplikacja AADSync 1.0**

Jeśli masz już zainstalowany program Azure AD Sync, ma jednego dodatkowego kroku masz tootake w przypadku, gdy zmieniono dowolne reguły synchronizacji out-of-box hello. Po uaktualnieniu wersji toohello 1.0.470.1023 hello reguły synchronizacji, które zostały zmodyfikowane są zduplikowane. Dla każdej reguły synchronizacji zmodyfikowane hello następujące:

1.  Znajdź reguły synchronizacji hello zmodyfikowano i zanotuj hello zmiany.
* Usuń regułę synchronizacji hello.
* Znajdź hello nową synchronizacji regułę, która jest tworzona przez program Azure AD Sync, a następnie Zastosuj ponownie zmiany hello.

**Uprawnienia dla hello konta usługi Active Directory**

Witaj konta usługi Active Directory musi mieć przyznane skrótów haseł hello stanie tooread toobe dodatkowe uprawnienia z usługi Active Directory. toogrant uprawnienia Hello są nazywane "Replikowanie zmiany katalogu" i "Directory replikacji zmian wszystkie". Skrótów haseł hello stanie tooread toobe wymagane są obie uprawnienia.

## <a name="104190911"></a>1.0.419.0911
Wydanie: Września 2014

**Początkowa wersja programu Azure AD Sync.**

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
