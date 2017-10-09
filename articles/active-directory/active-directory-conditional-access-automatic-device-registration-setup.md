---
title: "aaaHow tooconfigure automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Konfigurowanie sieci tooregister urządzeń przyłączonych do domeny systemu Windows automatycznie i w trybie dyskretnym usłudze Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 6a1aab753f5456ed06ba7979ab05f70f29b4ddee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a>Jak tooconfigure automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia w usłudze Azure Active Directory

toouse [dostępu warunkowego opartego na urządzenia usługi Azure Active Directory](active-directory-conditional-access-azure-portal.md), komputer musi być zarejestrowana w usłudze Azure Active Directory (Azure AD). Można uzyskać listę zarejestrowanych urządzeń w Twojej organizacji za pomocą hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) polecenia cmdlet w hello [modułu programu PowerShell usługi Azure Active Directory](/powershell/azure/install-msonlinev1?view=azureadps-2.0). 

Ten artykuł zawiera kroki hello konfigurowania hello automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny z usługą Azure AD w organizacji.


Aby uzyskać więcej informacji na temat:

- Funkcja dostępu warunkowego, zobacz [dostępu warunkowego opartego na urządzenia usługi Azure Active Directory](active-directory-conditional-access-azure-portal.md). 
- Urządzenia Windows 10 w pracy hello i doświadczeń hello rozszerzone po zarejestrowaniu w usłudze Azure AD, zobacz [systemu Windows 10 dla przedsiębiorstw hello: używanie urządzeń do pracy](active-directory-azureadjoin-windows10-devices-overview.md).
- Windows 10 Enterprise E3 w dostawcy usług Kryptograficznych, zobacz hello [systemu Windows 10 Enterprise E3 w dostawcy usług Kryptograficznych — omówienie](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).


## <a name="before-you-begin"></a>Przed rozpoczęciem

Przed rozpoczęciem konfigurowania hello automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny w danym środowisku, należy zapoznać się z hello obsługiwane scenariusze i hello ograniczenia.  

czytelność hello tooimprove opisy hello, w tym temacie używa powitania po termin: 

- **Urządzenia z systemem Windows bieżącego** -określenie to odnosi się toodomain przyłączone do urządzeń z systemem Windows 10 lub Windows Server 2016.
- **Urządzenia z systemem Windows niższego poziomu** -określenie to odnosi się tooall **obsługiwane** przyłączonych do domeny urządzenia z systemem Windows, które nie są uruchomione systemu Windows 10 ani Windows Server 2016.  


### <a name="windows-current-devices"></a>Bieżący urządzeń z systemem Windows

- Dla urządzeń z systemem Windows hello pulpitu systemu operacyjnego, zaleca się użycie systemu Windows 10 Anniversary aktualizacji (w wersji 1607) lub nowszym. 
- Witaj rejestracji urządzeń z systemem Windows bieżącego **jest** obsługiwane w niefederacyjnych środowiskach, takich jak konfiguracje synchronizacji skrótu hasła.  


### <a name="windows-down-level-devices"></a>Urządzenia z systemem Windows niższego poziomu

- obsługiwane są następujące urządzenia z systemem Windows niższego poziomu Hello:
    - Windows 8.1
    - Windows 7
    - Windows Server 2012 R2
    - Windows Server 2012
    - Windows Server 2008 R2
- Witaj rejestracji urządzeń z systemem Windows niższego poziomu **jest** obsługiwane w środowiskach niefederacyjnych za pośrednictwem bezproblemowe rejestracji jednokrotnej [Azure Active Directory bezproblemowe logowanie jednokrotne](https://aka.ms/hybrid/sso).
- Witaj rejestracji urządzeń z systemem Windows niższego poziomu **nie jest** obsługiwane na urządzeniach przy użyciu profilów mobilnych. Jeśli używasz mobilnego profile i ustawienia, należy użyć systemu Windows 10.



## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem włączenie hello automatyczną rejestrację urządzeń przyłączonych do domeny w organizacji, należy toomake się, że są uruchomione zaktualizowanej wersji programu Azure AD connect.

Azure AD Connect:

- Przechowuje hello skojarzenie hello konta komputera w sieci lokalnej Active Directory (AD) i hello obiekt urządzenia w usłudze Azure AD. 
- Umożliwia urządzeniu innych powiązanych funkcji, takich jak Windows Hello dla firm.



## <a name="configuration-steps"></a>Kroki konfiguracji

Ten temat zawiera kroki hello wymagane we wszystkich scenariuszach typowej konfiguracji.  
Użyj powitania po tooget tabeli omówienie hello kroki, które są wymagane dla danego scenariusza:  



| Kroki                                      | Synchronizacja skrótów bieżące i hasło systemu Windows | Bieżącego systemu Windows i Federacji | Niższego poziomu z systemem Windows |
| :--                                        | :-:                                    | :-:                            | :-:                |
| Krok 1: Konfigurowanie punktu połączenia usługi | ![Zaznacz][1]                            | ![Zaznacz][1]                    | ![Zaznacz][1]        |
| Krok 2: Skonfiguruj wystawiania oświadczeń           |                                        | ![Zaznacz][1]                    | ![Zaznacz][1]        |
| Krok 3: Włącz urządzenia z systemem innym niż Windows 10      |                                        |                                | ![Zaznacz][1]        |
| Krok 4: Wdrażanie formantu i wdrożenia     | ![Zaznacz][1]                            | ![Zaznacz][1]                    | ![Zaznacz][1]        |
| Krok 5: Sprawdzanie zarejestrowanych urządzeń          | ![Zaznacz][1]                            | ![Zaznacz][1]                    | ![Zaznacz][1]        |



## <a name="step-1-configure-service-connection-point"></a>Krok 1: Konfigurowanie punktu połączenia usługi

obiekt (SCP) punktu połączenia usługi Hello jest używany przez urządzenia podczas hello rejestracji toodiscover informacje o dzierżawy usługi Azure AD. W lokalnej usługi Active Directory (AD) obiekt SCP hello hello automatyczną rejestrację urządzeń przyłączonych do domeny muszą istnieć w hello nazewnictwa kontekstu partycji konfiguracji komputera hello lasu. Istnieje tylko jeden kontekście nazewnictwa konfiguracji w każdym lesie. W konfiguracji obejmującego wiele lasów usługi Active Directory punkt połączenia z usługą hello musi istnieć we wszystkich lasach środowiska zawierającego komputery przyłączone do domeny.

Można użyć hello [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) polecenia cmdlet tooretrieve hello kontekście nazewnictwa konfiguracji w lesie.  

Dla lasu z nazwą domeny usługi Active Directory hello *fabrikam.com*, jest w kontekście nazewnictwa konfiguracji hello:

`CN=Configuration,DC=fabrikam,DC=com`

W lesie obiekt hello punkt połączenia usługi dla rejestracji automatycznej hello urządzeń przyłączonych do domeny znajduje się na:  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

W zależności od tego, jak zostały wdrożone usługi Azure AD Connect obiektu SCP hello może zostały już skonfigurowane.
Można sprawdzić istnienia obiektu hello hello i pobrać wartości odnajdywania hello przy użyciu hello następującego skryptu programu Windows PowerShell: 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

Witaj **$scp. Słowa kluczowe** dane wyjściowe zawierają informacje o dzierżawy hello Azure AD, na przykład:

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

Jeśli punkt połączenia usługi hello nie istnieje, można go utworzyć, uruchamiając hello `Initialize-ADSyncDomainJoinedComputerSync` polecenia cmdlet na serwerze programu Azure AD Connect. Poświadczenia administratora przedsiębiorstwa jest wymagana toorun tego polecenia cmdlet.  
polecenia cmdlet Hello:

- Tworzy punkt połączenia z usługą hello w lesie usługi Active Directory hello Azure AD Connect jest połączona z. 
- Wymaga toospecify hello `AdConnectorAccount` parametru. To jest konto hello, która jest skonfigurowana jako usługi Active Directory connector konta w usłudze Azure AD connect. 


Witaj poniższy skrypt pokazuje przykład za pomocą polecenia cmdlet hello. W tym skrypcie `$aadAdminCred = Get-Credential` wymaga tootype nazwę użytkownika. Potrzebna jest nazwa użytkownika hello tooprovide format nazwy podmiotu zabezpieczeń (UPN) użytkownika hello (`user@example.com`). 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

Witaj `Initialize-ADSyncDomainJoinedComputerSync` polecenia cmdlet:

- Używa hello moduł środowiska PowerShell usługi Active Directory, który korzysta z usługi Active Directory w sieci Web uruchomiony na kontrolerze domeny. Usługi sieci Web w usłudze Active Directory jest obsługiwana na kontrolerach domeny z systemem Windows Server 2008 R2 lub nowszej.
- Jest obsługiwana tylko przez hello **MSOnline PowerShell w wersji modułu 1.1.166.0**. toodownload ten moduł służy [łącze](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).   

Dla kontrolerów domeny z systemem Windows Server 2008 lub starszej wersji należy użyć skryptu hello poniżej punktu połączenia usługi hello toocreate.

W konfiguracji wielu lasów należy użyć hello następującego skryptu toocreate hello punkt połączenia z usługą w każdym lesie, w którym istnieje komputerów:
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a>Krok 2: Skonfiguruj wystawiania oświadczeń

W federacyjnych Azure konfiguracji AD urządzeń zależą od usługi Active Directory Federation Services (AD FS) lub 3 strona tooAzure tooauthenticate usługi federacyjnej AD lokalnymi. Urządzenia uwierzytelniania tooget tooregister tokenu dostępu przed hello usługi Azure Active Directory urządzenia rejestracji (urządzeń DRS Azure).

Systemu Windows, które urządzenia bieżące uwierzytelniania przy użyciu zintegrowanego uwierzytelniania systemu Windows tooan active WS-Trust punktu końcowego (w wersji 1.3 lub 2005) obsługiwanych przez usługę federacyjną lokalne powitania.

> [!NOTE]
> Korzystając z usług AD FS, albo **adfs/services/zaufania/13/windowstransport** lub **adfs/services/zaufania/2005/windowstransport** musi być włączona. Jeśli używasz powitania serwera Proxy sieci Web uwierzytelniania, również upewnić się, czy ten punkt końcowy został opublikowany za pośrednictwem serwera proxy hello. Widać, jakie punkty końcowe są włączane za pośrednictwem konsoli zarządzania usług AD FS hello w obszarze **usługi > punkty końcowe**.
>
>Jeśli nie masz jako lokalnej usługi federacyjnej usług AD FS, wykonaj hello instrukcje użytkownika czy obsługę protokołu WS-Trust 1.3 lub punkty końcowe 2005, a te są publikowane za pomocą pliku wymiany metadanych (MEX) hello toomake dostawcy.

Hello następujące oświadczeń musi istnieć w tokenie hello odebrane przez usługi rejestracji urządzeń usługi Azure dla toocomplete rejestracji urządzenia. Usługi rejestracji urządzeń usługi Azure utworzy obiekt urządzenia w usłudze Azure AD, niektóre z tych informacji, która jest następnie używane przez obiekt urządzenia hello nowo utworzony tooassociate Azure AD Connect z hello komputera konta lokalnego.

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

Jeśli masz więcej niż jedną nazwę zweryfikowanej domeny należy hello tooprovide następujące oświadczenie dla komputerów:

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

Jeśli są już wystawiania oświadczeń nazwę ImmutableID (np. alternatywnego Identyfikatora logowania) należy tooprovide jedno oświadczenie odpowiednie dla komputerów:

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

Następujące sekcje hello można znaleźć informacje o:
 
- wartości Hello Każde oświadczenie ma
- Jak definicji będzie wyglądać w usługach AD FS

Definicja Hello pomaga tooverify czy wartości hello są obecne, lub jeśli potrzebujesz toocreate je.

> [!NOTE]
> Jeśli nie używasz usług AD FS dla lokalnego serwera federacyjnego, postępuj zgodnie z dostawcą instrukcje toocreate hello odpowiednia konfiguracja tooissue tych oświadczeń.

### <a name="issue-account-type-claim"></a>Problem konta typu oświadczenia

**`http://schemas.microsoft.com/ws/2012/01/accounttype`**— To oświadczenie musi zawierać wartość **DJ**, które identyfikują urządzenie hello jako komputer przyłączony do domeny. W usługach AD FS można dodawać reguł przekształcania wystawiania, która wygląda następująco:

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a>Wystawiać objectGUID hello komputera konta lokalnego

**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**— To oświadczenie musi zawierać hello **objectGUID** wartość hello lokalnego konta komputera. W usługach AD FS można dodawać reguł przekształcania wystawiania, która wygląda następująco:

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a>Wystawiać objectSID hello komputera konta lokalnego

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**— To oświadczenie musi zawierać hello hello **objectSid** wartość hello lokalnego konta komputera. W usługach AD FS można dodawać reguł przekształcania wystawiania, która wygląda następująco:

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a>Wystawiać issuerID dla komputera, gdy wiele zweryfikować nazwy domeny w usłudze Azure AD

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**— To oświadczenie musi zawierać hello URI Uniform Resource Identifier () dowolnego hello zweryfikować nazwy domeny, które uzyskuj hello lokalnej wystawiania tokenu hello Federacji (AD FS lub strona 3). W usługach AD FS można dodać reguły przekształcania wystawiania, które wyglądają jak hello tych poniżej w tej kolejności po hello tych powyżej. Należy pamiętać reguły hello problem tooexplicitly jedną regułę dla użytkowników jest konieczne. W poniższych reguł hello dodawany jest pierwsza reguła identyfikacji użytkownika, a uwierzytelnianie komputera.

    @RuleName = "Issue account type with hello value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


W powyższym oświadczeń hello

- `$<domain>`jest adres URL hello AD FS usługi
- `<verified-domain-name>`jest to symbol zastępczy należy tooreplace z jednym z nazwy domeny zweryfikowane w usłudze Azure AD



Aby uzyskać więcej informacji o nazwach zweryfikowanej domeny, zobacz [tooAzure nazwy domeny niestandardowej usługi Active Directory dodać](active-directory-add-domain.md).  
tooget listę domeny zweryfikowane firmy, można użyć hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) polecenia cmdlet. 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a>Wystawiać nazwę ImmutableID dla komputera, gdy istnieje jeden dla użytkowników (np. alternatywny logowania identyfikatora)

**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**— To oświadczenie musi zawierać prawidłową wartość dla komputerów. W usługach AD FS można utworzyć reguły przekształcania wystawiania w następujący sposób:

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a>Reguły przekształcania wystawiania pomocnika skryptu toocreate hello AD FS

Hello poniższy skrypt pomaga z hello tworzenie wystawiania hello przekształcenie reguł opisanych powyżej.

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a>Uwagi 

- Ten skrypt dołącza hello zasady toohello istniejących zasad. Nie uruchamiaj skryptu hello dwukrotnie ponieważ hello zestaw reguł zostanie dodany dwa razy. Upewnij się, że odpowiednie nie istnieją żadne reguły tych oświadczeń (warunkach hello odpowiedniego) przed ponownym uruchomieniem hello skryptu.

- Jeśli masz wiele zweryfikowanej domeny nazw (jak pokazano w portalu usługi Azure AD hello lub przy użyciu polecenia cmdlet Get-MsolDomains hello), należy ustawić wartość hello **$multipleVerifiedDomainNames** w hello skryptu zbyt**$true**. Upewnij się również usunięcie istniejących oświadczenie issuerid został utworzony przez program Azure AD Connect lub za pomocą innych środków. Oto przykład dla tej reguły:


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- Jeśli już wystawiły **nazwę ImmutableID** oświadczenia dla kont użytkowników, należy ustawić wartość hello **$immutableIDAlreadyIssuedforUsers** w hello skryptu zbyt**$true**.

## <a name="step-3-enable-windows-down-level-devices"></a>Krok 3: Włącz urządzeń z systemem Windows niższego poziomu

Jeśli niektóre urządzenia przyłączone do domeny z systemem Windows niższego poziomu urządzeń, należy:

- Skonfigurować zasadę usługi Azure AD tooenable urządzenia tooregister użytkowników.
 
- Konfigurowanie sieci lokalnej federacyjnych usługi tooissue oświadczeń toosupport **zintegrowane uwierzytelnianie systemu Windows (IWA)** w czasie rejestracji urządzenia.
 
- Dodaj hello Azure AD urządzenia uwierzytelniania punktu końcowego toohello lokalnego intranetu stref, które monituje tooavoid certyfikatu podczas uwierzytelniania urządzenia hello.

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a>Ustawienie zasad w usłudze Azure AD tooenable urządzenia tooregister użytkowników

tooregister urządzeń niższego poziomu z systemem Windows, należy upewnić się, że hello ustawienie użytkowników tooallow tooregister urządzeń w usłudze Azure AD jest ustawiony toomake. W portalu Azure hello możesz znaleźć tego ustawienia:

`Azure Active Directory > Users and groups > Device settings`
    
Witaj następujące zasady muszą mieć wartość zbyt**wszystkie**: **użytkownicy mogą zarejestrować swoje urządzenia w usłudze Azure AD**

![Rejestrowanie urządzeń](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a>Konfigurowanie usługi federacyjnej lokalnej 

Lokalne usługi federacyjnej musi obsługiwać wystawiającego hello **authenticationmehod** i **wiaormultiauthn** toohello usługi Azure AD jednostki uzależnionej zawierający żądania oświadczeń podczas odbierania uwierzytelniania resouce_params parametr o wartości zakodowanej, jak pokazano poniżej:

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

Jeśli takie żądanie pochodzi, usługa federacyjna lokalne powitania musi uwierzytelnić użytkownika hello przy użyciu zintegrowanego uwierzytelniania systemu Windows i na sukces, należy wygenerować hello następujące dwa oświadczenia:

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

W usługach AD FS należy dodać tej metody uwierzytelniania hello przekazuje do reguł przekształcania wystawiania.  

**tooadd tej reguły:**

1. W konsoli zarządzania hello AD FS Przejdź zbyt`AD FS > Trust Relationships > Relying Party Trusts`.
2. Kliknij prawym przyciskiem myszy hello platformą tożsamości programu Microsoft Office 365 obiekt jednostki uzależnionej zaufania, a następnie wybierz **Edycja reguł oświadczeń**.
3. Na powitania **reguły przekształcania wystawiania** wybierz opcję **Dodaj regułę**.
4. W hello **reguły oświadczeń** szablon z listy wybierz **wysyłanie oświadczeń przy użyciu reguły niestandardowej**.
5. Wybierz **dalej**.
6. W hello **nazwy reguły oświadczeń** wpisz **reguły oświadczeń metody uwierzytelniania**.
7. W hello **reguły oświadczeń** okno, hello typu następujące reguły:

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. Na serwerze federacyjnym, wpisz polecenie programu PowerShell hello poniżej po zastąpieniu  **\<RPObjectName\>**  z nazwą hello do obiektu jednostki uzależnionej strony dla obiekt zaufania jednostki uzależnionej strony usługi Azure AD. Ten obiekt zwykle nosi nazwę **Microsoft Office 365 tożsamość platformy**.
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a>Dodaj hello Azure AD urządzenia uwierzytelniania punktu końcowego toohello lokalny Intranet strefy

certyfikat tooavoid monity podczas tooAzure AD, możesz wypchnąć tooyour zasady urządzeń przyłączonych do domeny hello tooadd następującego adresu URL toohello lokalny intranet w programie Internet Explorer uwierzytelniania użytkowników w rejestrze urządzeń:

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a>Krok 4: Wdrażanie formantu i wdrożenia

Po zakończeniu kroków hello wymagane urządzeń przyłączonych do domeny są gotowe tooautomatically rejestru z usługą Azure AD. Wszystkich przyłączonych do domeny urządzeń z systemem Windows 10 Anniversary Update i Windows Server 2016 automatycznie zarejestrować w usłudze Azure AD na urządzeniu ponownego uruchomienia lub logowania użytkownika. Zarejestrować nowe urządzenia z usługą Azure AD, gdy hello urządzenie zostanie uruchomione ponownie, po zakończeniu operacji przyłączania do domeny hello.

Urządzenia, które zostały wcześniej dołączone tooAzure AD (na przykład w usłudze Intune) przejścia zbyt"*przyłączonych do domeny, zarejestrowane w usłudze AAD*"; jednak zajmuje trochę czasu, zanim ten proces toocomplete dla wszystkich urządzeń powodu normalny toohello Przepływ działania domeny i użytkownika.

### <a name="remarks"></a>Uwagi

- Można użyć zasad grupy obiektu toocontrol hello wdrażanie automatycznej rejestracji systemu Windows 10 i Windows Server 2016 komputerów przyłączonych do domeny.

- Aktualizacja systemu Windows 10 listopada 2015 automatycznie rejestruje z usługą Azure AD **tylko** Jeśli obiekt zasad grupy hello wdrożenia jest ustawiona.

- toorollout hello automatyczną rejestrację komputerów z systemem Windows niższego poziomu, można wdrożyć [pakiet Instalatora Windows](#windows-installer-packages-for-non-windows-10-computers) toocomputers wybrany.

- Jeśli wypychanych urządzeń przyłączonych do domeny tooWindows 8.1 obiektu zasad grupy hello rejestracji zostanie podjęta próba; jednak zaleca się, że używasz hello [pakiet Instalatora Windows](#windows-installer-packages-for-non-windows-10-computers) tooregister wszystkich urządzeń z systemem Windows niższego poziomu. 

### <a name="create-a-group-policy-object"></a>Utwórz obiekt zasad grupy 

Wdrażanie hello toocontrol automatycznej rejestracji bieżącego komputerów z systemem Windows, należy wdrożyć hello **rejestrować komputery przyłączone do domeny jako urządzenia** urządzeń toohello obiektu zasad grupy ma tooregister. Na przykład można wdrożyć jednostki organizacyjnej tooan zasad hello lub tooa grupy zabezpieczeń.

**tooset hello zasad:**

1. Otwórz **Menedżera serwera**, a następnie przejdź zbyt`Tools > Group Policy Management`.
2. Przejdź toohello domeny węzła, który odpowiada toohello domenie rejestracji automatycznej tooactivate bieżącego komputerów z systemem Windows.
3. Kliknij prawym przyciskiem myszy **obiektów zasad grupy**, a następnie wybierz **nowy**.
4. Wpisz nazwę obiektu zasad grupy. Na przykład *tooAzure automatycznej rejestracji AD*. Kliknij przycisk **OK**.
5. Kliknij prawym przyciskiem myszy nowy obiekt zasad grupy, a następnie wybierz **Edytuj**.
6. Przejdź za**Konfiguracja komputera** > **zasady** > **Szablony administracyjne** > **systemu Windows Składniki** > **Rejestracja urządzenia**. Kliknij prawym przyciskiem myszy **rejestrować komputery przyłączone do domeny jako urządzenia**, a następnie wybierz **Edytuj**.
   
   > [!NOTE]
   > Ten szablon zasad grupy została zmieniona z wcześniejszych wersji hello konsoli zarządzania zasadami grupy. Jeśli używasz starszej wersji konsoli hello Przejdź zbyt`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`. 

7. Wybierz **włączone**, a następnie wybierz **Zastosuj**.
8. Kliknij przycisk **OK**.
9. Łącze hello lokalizacji tooa obiektu zasad grupy wybranych przez użytkownika. Na przykład można je połączyć tooa określonej jednostce organizacyjnej. Możesz również można połączyć go tooa określonej grupy zabezpieczeń komputerów, które automatycznie zarejestrować w usłudze Azure AD. tooset te zasady dla wszystkich przyłączonych do domeny systemu Windows 10 i Windows Server 2016 komputerów w organizacji link hello zasad grupy obiektu toohello domeny.

### <a name="windows-installer-packages-for-non-windows-10-computers"></a>Pakietów Instalatora Windows na komputerach z systemem innym niż Windows 10

tooregister przyłączonych do domeny z systemem Windows niższego poziomu komputerów w środowisku federacyjnym można pobrać i zainstalować te pakiet Instalatora Windows (msi) z Centrum pobierania w hello [firmy Microsoft dla komputerów z systemem innym niż Windows 10Dołączdomiejscapracy](https://www.microsoft.com/en-us/download/details.aspx?id=53554) strony.

Można wdrożyć pakiet hello przy użyciu system dystrybucji oprogramowania, takich jak System Center Configuration Manager. Witaj pakietu obsługuje hello standardowej instalacji dyskretnej opcje z hello *quiet* parametru. System Center Configuration Manager Current Branch oferuje dodatkowe korzyści z wcześniejszych wersji, takich jak hello możliwości tootrack ukończyć rejestracji. Aby uzyskać więcej informacji, zobacz [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).

Instalator Hello utworzenie zaplanowanego zadania, w systemie hello, który jest uruchamiany w kontekście użytkownika hello. zadanie Hello jest wyzwalane, gdy hello użytkownik loguje się tooWindows. zadanie Hello dyskretnie rejestruje hello urządzenia z usługą Azure AD przy użyciu poświadczeń użytkownika powitania po uwierzytelnieniu przy użyciu zintegrowanego uwierzytelniania systemu Windows. toosee hello zaplanowanego zadania, w urządzeniu hello przejść za**Microsoft** > **dołączania**, a następnie przejdź toohello Biblioteka Harmonogramu zadań.

## <a name="step-5-verify-registered-devices"></a>Krok 5: Sprawdzanie zarejestrowanych urządzeń

Pomyślnie zarejestrowanych urządzeń w Twojej organizacji można sprawdzić za pomocą hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) polecenia cmdlet w hello [modułu programu PowerShell usługi Azure Active Directory](/powershell/azure/install-msonlinev1?view=azureadps-2.0).

dane wyjściowe tego polecenia cmdlet Hello zawiera urządzenia zarejestrowane w usłudze Azure AD. tooget wszystkie urządzenia, użyj hello **— wszystkie** parametr, a następnie filtr ich przy użyciu hello **deviceTrustType** właściwości. Przyłączony do domeny urządzenia mają wartość **przyłączonych do domeny**.

## <a name="next-steps"></a>Następne kroki

* [Automatycznej rejestracji urządzeń — często zadawane pytania](active-directory-device-registration-faq.md)
* [Rozwiązywanie problemów z automatyczną rejestrację domeny przyłączone tooAzure komputery AD — Windows 10 i Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)
* [Rozwiązywanie problemów z automatyczną rejestrację domeny przyłączone tooAzure komputery AD — z systemem innym niż Windows 10](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [Dostęp warunkowy do usługi Azure Active Directory](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
