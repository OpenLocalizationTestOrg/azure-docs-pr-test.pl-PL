---
title: "aaaActive Directory Federation Services zarządzania i dostosowywania z programem Azure AD Connect | Dokumentacja firmy Microsoft"
description: "Zarządzanie usługami AD FS z usługi Azure AD Connect i dostosowywania AD FS logowania użytkowników z usługi Azure AD Connect i programu PowerShell."
keywords: "Usługi AD FS, usługi AD FS, usługi AD FS zarządzania AAD Connect, Connect, logowania, usługi AD FS dostosowanie, napraw federacyjnej relacji zaufania, usługi O365, jednostki uzależnionej"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a>Zarządzanie i dostosowania usług federacyjnych Active Directory przy użyciu usługi Azure AD Connect
W tym artykule opisano sposób toomanage i dostosować Active Directory Federation Services (AD FS) przy użyciu połączenia usługi Azure Active Directory (Azure AD). Zawiera również innych typowych zadań usług AD FS, że może być konieczne toodo do ukończenia konfiguracji farmy usług AD FS.

| Temat | Co obejmuje |
|:--- |:--- |
| **Zarządzanie usługami AD FS** | |
| [Napraw hello zaufania](#repairthetrust) |Jak toorepair hello federacyjnego zaufania z usługą Office 365. |
| [Utworzenie federacji z usługą Azure AD przy użyciu alternatywnego Identyfikatora logowania](#alternateid) | Konfigurowanie Federacji przy użyciu alternatywnego Identyfikatora logowania  |
| [Dodawanie serwera usług AD FS](#addadfsserver) |Jak tooexpand usług AD FS farmy dodatkowy serwer usług AD FS. |
| [Dodaj serwer Proxy aplikacji sieci Web usług AD FS](#addwapserver) |Jak tooexpand usług AD FS farmy dodatkowy serwer Proxy aplikacji sieci Web (WAP). |
| [Dodawanie domeny federacyjnej](#addfeddomain) |Jak tooadd domeny federacyjnej. |
| [Certyfikat SSL hello aktualizacji](active-directory-aadconnectfed-ssl-update.md)| Jak tooupdate hello SSL certyfikatów dla farmy usług AD FS. |
| **Dostosowywanie usług AD FS** | |
| [Dodać logo firmy lub ilustracji](#customlogo) |Sposób logowania usług AD FS toocustomize strony z firmowego logo i ilustracja. |
| [Dodaj opis logowania](#addsignindescription) |Jak opis strony tooadd logowania. |
| [Modyfikowanie reguł oświadczeń usług AD FS](#modclaims) |Jak toomodify usług AD FS oświadczeń dla różnych scenariuszy federacji. |

## <a name="manage-ad-fs"></a>Zarządzanie usługami AD FS
Za pomocą kreatora Połącz hello Azure AD, można wykonywać różne AD FS dotyczące zadania w programie Azure AD Connect z użytkownika minimalnej interwencji. Po zakończeniu instalowania usługi Azure AD Connect uruchomiony Kreator hello hello kreatora można uruchomić ponownie tooperform dodatkowe zadania.

## Napraw hello zaufania<a name=repairthetrust></a>
Można użyć usługi Azure AD Connect toocheck hello bieżącą kondycję hello usług AD FS i zaufania usługi Azure AD i podjąć odpowiednie działania toorepair hello zaufania. Wykonaj te kroki toorepair Azure AD i usług AD FS zaufania.

1. Wybierz **AAD naprawy i zaufania usług AD FS** z listy hello dodatkowe zadania.
   ![Napraw AAD i usług AD FS zaufania](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)

2. Na powitania **połączyć tooAzure AD** , podaj poświadczenia administratora globalnego dla usługi Azure AD i kliknij przycisk **dalej**.
   ![Połącz tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)

3. Na powitania **poświadczeń dostępu zdalnego** wprowadź poświadczenia hello hello administratora domeny.

   ![Poświadczenia dostępu zdalnego](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    Po kliknięciu **dalej**, Azure AD Connect sprawdza, czy certyfikat kondycji i zawiera wszystkie problemy.

    ![Stan certyfikatów](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    Witaj **tooconfigure gotowe** strony pokazuje hello listę działań, które będą wykonywane toorepair hello zaufania.

    ![Gotowe tooconfigure](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. Kliknij przycisk **zainstalować** toorepair hello zaufania.

> [!NOTE]
> Azure AD Connect może tylko naprawy lub ustawy o certyfikaty z podpisem własnym. Azure AD Connect nie może naprawić certyfikatów innych firm.

## Utworzenie federacji z usługą Azure AD przy użyciu AlternateID<a name=alternateid></a>
Zaleca się, że hello lokalnego Name(UPN) głównej nazwy użytkownika i chmury hello główna nazwa użytkownika są przechowywane hello takie same. Jeśli hello UPN lokalnymi używa nierutowalny domeny (np. Contoso.local) lub nie można zmienić powodu toolocal zależności aplikacji, zaleca się konfigurowanie alternatywnego identyfikatora. Alternatywnego Identyfikatora logowania umożliwia tooconfigure Obsługa logowania w którym użytkownicy mogą logować się przy użyciu atrybutu innego niż ich nazwy UPN, taki jak adres e-mail. Wybór Hello do głównej nazwy użytkownika w atrybut userPrincipalName toohello domyślne Azure AD Connect w usłudze Active Directory. Jeśli możesz wybrać inny atrybut główna nazwa użytkownika i Federacji przy użyciu usług AD FS, następnie Azure AD Connect konfiguracji usług AD FS dla alternatywny identyfikator. Poniżej przedstawiono przykład wybranie innego atrybutu główna nazwa użytkownika:

![Alternatywny identyfikator atrybutu zaznaczenia](media/active-directory-aadconnect-federation-management/attributeselection.png)

Konfigurowanie alternatywnego Identyfikatora logowania dla usług AD FS składa się z dwóch głównych czynności:
1. **Skonfiguruj hello prawidłowego zestawu wystawiania oświadczeń**: hello wystawiania oświadczeń reguły w jednostce uzależnionej hello Azure AD zaufania, są atrybutu UserPrincipalName hello wybrane toouse zmodyfikowane, jak hello alternatywny identyfikator użytkownika hello.
2. **Włącz alternatywnego Identyfikatora logowania w konfiguracji usług AD FS hello**: hello AD FS konfiguracji zostaną zmienione tak, aby usługi AD FS można wyszukiwać użytkowników w lasach odpowiednie hello przy użyciu hello alternatywnego identyfikatora. Ta konfiguracja jest obsługiwana dla usług AD FS w systemie Windows Server 2012 R2 (z KB2919355) lub nowszym. Jeśli serwery usług hello AD FS 2012 R2, Azure AD Connect sprawdza obecność hello hello wymagane KB. Jeśli hello KB nie zostanie wykryta, ostrzeżenie będzie wyświetlana po zakończeniu konfiguracji, jak pokazano poniżej:

    ![Ostrzeżenie dotyczące Brak KB na 2012 R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    toorectify hello konfiguracji w przypadku brakujących KB, zainstaluj hello wymagane [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) , a następnie napraw hello zaufania przy użyciu [napraw AAD i AD FS zaufania](#repairthetrust).

> [!NOTE]
> Aby uzyskać więcej informacji na toomanually alternateID i kroki konfigurowania, odczytać [Konfigurowanie alternatywnego Identyfikatora logowania](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)

## Dodawanie serwera usług AD FS<a name=addadfsserver></a>

> [!NOTE]
> Serwer tooadd usług AD FS, Azure AD Connect wymaga hello certyfikat PFX. W związku z tym tę operację mogą wykonać tylko wtedy, gdy hello AD FS farmy jest konfigurowana przy użyciu usługi Azure AD Connect.

1. Wybierz **wdrażanie dodatkowego serwera federacyjnego**i kliknij przycisk **dalej**.

   ![Serwer federacyjny dodatkowe](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. Na powitania **połączyć tooAzure AD** strony, wprowadź swoje poświadczenia administratora globalnego dla usługi Azure AD, a następnie kliknij przycisk **dalej**.

   ![Połącz tooAzure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. Podaj poświadczenia administratora domeny hello.

   ![Podane poświadczenia administratora domeny](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. Azure AD Connect pytanie o hasło hello hello pliku PFX, podane podczas konfigurowania nowej farmie serwerów usług AD FS z programem Azure AD Connect. Kliknij przycisk **wprowadź hasło** tooprovide hello hasło dla pliku PFX hello.

   ![Hasło certyfikatu](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Określ certyfikat SSL](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. Na powitania **serwery usług AD FS** wpisz nazwę serwera hello lub dodać toobe adres IP toohello AD FS farmy.

   ![Serwery usług AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. Kliknij przycisk **dalej**i wykonaj hello końcowego **Konfiguruj** strony. Po zakończeniu Azure AD Connect Dodawanie hello serwerów toohello AD FS farmy, będziesz mieć możliwość hello opcja tooverify hello łączności.

   ![Gotowe tooconfigure](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Zakończenie instalacji](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## Dodaj serwer AD FS WAP<a name=addwapserver></a>

> [!NOTE]
> tooadd serwerowi proxy aplikacji Azure AD Connect wymaga hello certyfikat PFX. W związku z tym można wykonać tylko tej operacji po skonfigurowaniu hello AD FS farmy przy użyciu usługi Azure AD Connect.

1. Wybierz **wdrażanie Proxy aplikacji sieci Web** z hello listę dostępnych zadań.

   ![Wdrożenie serwera Proxy aplikacji sieci Web](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. Podaj poświadczenia administratora globalnego usługi Azure hello.

   ![Połącz tooAzure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. Na powitania **certyfikat SSL określ** Podaj hello hasło dla pliku PFX hello podane podczas konfigurowania farmy usług hello AD FS z programem Azure AD Connect.
   ![Hasło certyfikatu](media/active-directory-aadconnect-federation-management/WapServer3.PNG)

    ![Określ certyfikat SSL](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. Dodaj powitania serwera toobe dodany jako serwer proxy. Ponieważ hello serwerowi proxy mogą nie być toohello przyłączone do domeny, Kreator hello poprosi o dodawany serwer toohello poświadczenia administracyjne.

   ![Poświadczenia administracyjne serwera](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. Na powitania **poświadczeń zaufania serwera Proxy** Podaj poświadczenia administracyjne tooconfigure hello proxy zaufania i dostępu do serwera podstawowego hello w farmie hello usług AD FS.

   ![Poświadczenia zaufania serwera proxy](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. Na powitania **tooconfigure gotowe** strony, Kreator hello listą hello akcje, które będą wykonywane.

   ![Gotowe tooconfigure](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. Kliknij przycisk **zainstalować** toofinish hello konfiguracji. Po ukończeniu konfiguracji hello hello kreatora daje hello tooverify opcji hello łączności toohello serwerów. Kliknij przycisk **Sprawdź** toocheck łączności.

   ![Zakończenie instalacji](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## Dodawanie domeny federacyjnej<a name=addfeddomain></a>

Jest łatwy tooadd toobe domeny Sfederowanych z usługą Azure AD za pomocą usługi Azure AD Connect. Azure AD Connect dodaje hello domeny dla Federacji i modyfikuje oświadczenia hello toocorrectly reguły odzwierciedlają hello wystawcy, jeśli masz wiele domen federacyjnych z usługą Azure AD.

1. tooadd domeny federacyjnej, wybierz hello zadań **Dodawanie kolejnej domeny usługi Azure AD**.

   ![Dodatkowe domeny usługi Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. Na następnej stronie powitania hello kreatora należy podać poświadczenia administratora globalnego powitania dla usługi Azure AD.

   ![Połącz tooAzure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. Na powitania **poświadczeń dostępu zdalnego** Podaj poświadczenia administratora domeny hello.

   ![Poświadczenia dostępu zdalnego](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. Na następnej stronie powitania Kreatora hello zawiera listę domen usługi Azure AD, które można było wykonać Federację lokalnego katalogu z. Wybierz domenę hello z listy hello.

   ![Domenowych Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    Po wybraniu domeny hello kreatora hello zawiera odpowiednie informacje o dalsze akcje, które hello Kreator będzie trwać i hello wpływ hello konfiguracji. W niektórych przypadkach w przypadku wybrania domeny, która jeszcze nie jest zweryfikowana w usłudze Azure AD, Kreator hello zapewnia informacje toohelp sprawdzisz hello domeny. Zobacz [tooAzure nazwa Twojej niestandardową domenę usługi Active Directory dodać](../active-directory-add-domain.md) więcej szczegółów.

5. Kliknij przycisk **Dalej**. Witaj **tooconfigure gotowe** strony hello Lista akcji, które wykona Azure AD Connect. Kliknij przycisk **zainstalować** toofinish hello konfiguracji.

   ![Gotowe tooconfigure](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> Użytkownicy z hello dodać musi być synchronizowany domeny federacyjnej, zanim będą oni mogli toologin tooAzure AD.

## <a name="ad-fs-customization"></a>Dostosowania usług AD FS
Witaj poniższe sekcje zawierają szczegółowe informacje o niektórych typowych zadań hello może mieć tooperform podczas dostosowywania strony logowania usług AD FS.

## Dodać logo firmy lub ilustracji<a name=customlogo></a>
toochange hello logo firmy hello, który jest wyświetlany na powitania **logowania** strony, należy użyć następującego polecenia cmdlet programu Windows PowerShell i składni hello.

> [!NOTE]
> Witaj zalecane wymiary hello logo to 260 x 35 przy rozdzielczości 96 dpi w pliku o rozmiarze nie większym niż 10 KB.

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> Witaj *TargetName* parametr jest wymagany. Witaj motyw domyślny publikowany z usługami AD FS nosi nazwę domyślny.

## Dodaj opis logowania<a name=addsignindescription></a>
tooadd toohello opisu strony logowania **strony logowania**, użyj następującego polecenia cmdlet programu Windows PowerShell i składni hello.

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## Modyfikowanie reguł oświadczeń usług AD FS<a name=modclaims></a>
Usługi AD FS obsługują język sformatowanego oświadczeń można użyć toocreate niestandardowych reguł oświadczeń. Aby uzyskać więcej informacji, zobacz [hello roli hello języka reguł oświadczeń](https://technet.microsoft.com/library/dd807118.aspx).

Witaj poniższych sekcjach opisano sposób można zapisać reguły niestandardowe dla niektórych scenariuszy, które są powiązane tooAzure AD i federacji usług AD FS.

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a>Warunkowe na wartość jest obecny w atrybucie hello niezmienialnego Identyfikatora
Azure AD Connect umożliwia określenie toobe atrybutu używany jako zakotwiczenie źródła, gdy obiekty są synchronizowane tooAzure AD. Jeśli wartość hello w atrybucie niestandardowym hello nie jest pusta, można tooissue niezmienne oświadczenie Identyfikatora.

Na przykład możesz wybrać pozycję **ms-ds-consistencyguid** jako atrybut hello zakotwiczenie źródła hello oraz wydawania **nazwę ImmutableID** jako **consistencyguid-ms-ds** w przypadku hello atrybut ma wartość na nim. Jeśli nie ma żadnej wartości dla atrybutu hello, **objectGuid** jako hello niezmienne identyfikatora. Zgodnie z opisem w następujących sekcji hello można konstruować hello zestaw niestandardowych reguł oświadczeń.

**Reguła 1: Atrybuty zapytania**

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

W tej regule, w przypadku badania wartości hello **ms-ds-consistencyguid** i **objectGuid** hello użytkownika z usługi Active Directory. Zmień nazwę odpowiedniego sklepu hello magazynu Nazwa tooan we wdrożeniu usług AD FS. Również zmienić hello oświadczeń tooa oświadczeń prawidłowego typu dla federacyjnym, zgodnie z definicją **objectGuid** i **consistencyguid-ms-ds**.

Ponadto za pomocą **dodać** i nie **problem**, unikać dodawania wychodzących problemem w przypadku jednostki hello i użyć hello wartości jako wartości pośrednich. Będzie wystawiać oświadczenia hello w regule nowsze po ustaleniu które toouse wartość jako hello niezmienne identyfikatora.

**Reguła 2: Sprawdź, czy consistencyguid-ms-ds istnieje hello użytkownika**

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

Ta zasada definiuje tymczasowe flagę o nazwie **idflag** który ustawiono zbyt**useguid** w przypadku nie **consistencyguid-ms-ds** wypełnione hello użytkownika. Witaj logiki to jest hello fakt, że usługi AD FS nie zezwala na puste oświadczeń. Dlatego po dodaniu http://contoso.com/ws/2016/02/identity/claims/objectguid oświadczeń i http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid w reguła 1 na końcu **msdsconsistencyguid** oświadczenia tylko wtedy, gdy wartość Hello jest wypełniana hello użytkownika. Jeśli go nie jest wypełnione, będzie mieć wartość pustą i odrzuca pochodzące od razu będzie widział usług AD FS. Wszystkie obiekty będą mieć **objectGuid**, więc roszczenie zawsze będą dostępne po wykonaniu reguła 1.

**Reguła 3: Wystawiać ms-ds-consistencyguid jako niezmienialnego Identyfikatora, jeśli jest obecny**

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

To jest niejawnie **Exist** Sprawdź. Jeśli istnieje wartość hello hello oświadczenia, następnie wystawiania, która jako niezmienialny hello identyfikator. Witaj poprzednim przykładzie użyto hello **nameidentifier** oświadczeń. Będziesz mieć toochange tego typu oświadczenia właściwe toohello dla Identyfikatora niezmienne hello w danym środowisku.

**Reguła 4: Jeśli consistencyGuid-ms-ds nie jest obecny Wystaw objectGuid jako niezmienialnego Identyfikatora**

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

W tej regule, sprawdzamy po prostu flagę tymczasowego hello **idflag**. Zdecyduj, czy oparta na oświadczeniach hello tooissue na jego wartość.

> [!NOTE]
> ważne jest sekwencji Hello tych zasad.

### <a name="sso-with-a-subdomain-upn"></a>Usługa rejestracji Jednokrotnej z poddomeny nazwy UPN
Możesz dodać więcej niż jeden toobe domeny federacyjnej przy użyciu usługi Azure AD Connect, zgodnie z opisem w [Dodaj nową domenę federacyjną](active-directory-aadconnect-federation-management.md#addfeddomain). Należy zmodyfikować oświadczenia głównej nazwy (UPN) użytkownika hello tak, aby hello identyfikator wystawcy odpowiada domeny głównej toohello i nie hello poddomen, ponieważ hello federacyjnych główny domeny obejmuje również hello podrzędnych.

Domyślnie reguł oświadczeń hello wystawcy Identyfikatora jest ustawiony jako:

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Oświadczenie Identyfikatora wystawcy domyślne](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

Hello domyślną regułę po prostu przyjmuje hello sufiks głównej nazwy użytkownika i używa go w Witaj wystawca identyfikator oświadczenia. Na przykład Jan jest użytkownikiem w sub.contoso.com i contoso.com jest Sfederowane przy użyciu usługi Azure AD. Jan wprowadza john@sub.contoso.com jako hello nazwy użytkownika podczas logowania tooAzure AD. Hello domyślne wystawcy identyfikator reguły oświadczeń w usługach AD FS obsługuje on powitania po sposób:

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

**Wartość oświadczenia:** http://sub.contoso.com/adfs/services/trust/

toohave tylko hello domenie głównej Witaj wystawca wartości oświadczenia, hello oświadczeń reguła toomatch hello następujące zmiany:

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [opcje logowania użytkowników](active-directory-aadconnect-user-signin.md).
