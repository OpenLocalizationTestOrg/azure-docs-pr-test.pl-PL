---
title: "aaaLearn o zasady zabezpieczeń Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Omówienie jak toorun aplikacji usługi Service Fabric, w obszarze kont zabezpieczeń lokalnych i systemu, w tym hello SetupEntry punktu, gdzie aplikacja musi tooperform niektóre uprzywilejowany akcji przed rozpoczęciem"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: mfussell
ms.openlocfilehash: f5afba69e09aa4f3c9efa4d3efc6995c813a1f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-security-policies-for-your-application"></a>Konfigurowanie zasad zabezpieczeń aplikacji
Za pomocą usługi Azure Service Fabric, można zabezpieczyć aplikacji uruchomionych w klastrze hello w obszarze konta innego użytkownika. Sieć szkieletowa usług pomaga również hello bezpiecznych zasobów, które są używane przez aplikacje w czasie hello wdrożenia na kontach użytkowników hello — na przykład, plików, katalogów i certyfikatów. Dzięki temu uruchamianie aplikacji, nawet w środowisku hostowanej udostępnionego bardziej bezpieczne od siebie nawzajem.

Domyślnie aplikacje sieci szkieletowej usług działać w ramach konta hello, działającą hello proces Fabric.exe. Usługi sieć szkieletowa dostępne są także możliwość hello toorun aplikacji w ramach konta użytkownika lokalnego lub konta system lokalny, które jest określone w manifeście aplikacji hello. Obsługiwany system lokalny typy kont to **LocalUser**, **NetworkService**, **Usługa lokalna**, i **LocalSystem**.

 Jeśli korzystasz z sieci szkieletowej usług w systemie Windows Server w centrum danych przy użyciu hello Autonomiczny Instalator rozszerzenia, można użyć konta domeny usługi Active Directory, łącznie z konta usług zarządzane przez grupę.

Można zdefiniować i Utwórz grupy użytkowników, dzięki czemu można dodać jeden lub więcej użytkowników toobe grupy tooeach zarządza się razem. Jest to przydatne, gdy jest wielu użytkowników do innej usługi, punkty wejścia i muszą toohave niektórych typowych uprawnień, które są dostępne na poziomie grupy hello.

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a>Konfigurowanie zasad powitania dla punktu wejścia instalacji usługi
Zgodnie z opisem w hello [model aplikacji](service-fabric-application-model.md), hello punktu wejścia instalacji **SetupEntryPoint**, to punkt wejścia uprzywilejowanych uruchamiane przy użyciu hello same poświadczenia jako sieci szkieletowej usług (zazwyczaj hello *NetworkService* konta) przed innymi punktu wejścia. plik wykonywalny Hello, który jest określony przez **punktu wejścia** jest zazwyczaj hello długotrwałe usługi hosta. Więc o punktu wejścia instalacji oddzielnych pozwala uniknąć konieczności hosta usługi hello toorun pliku wykonywalnego z wysokiego poziomu uprawnień przez dłuższy czas. Witaj wykonywalnego który **punktu wejścia** określa po zakończeniu **SetupEntryPoint** kończy się pomyślnie. Witaj Wynikowy proces jest monitorowane i ponownie uruchomione i ponownie rozpoczyna się od **SetupEntryPoint** Jeśli kiedykolwiek kończy lub ulegnie awarii.

następujące Hello to przykład manifestu usługi simple czy pokazuje hello SetupEntryPoint i hello główny punkt wejścia dla usługi hello.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>
  <ConfigPackage Name="Config" Version="1.0.0" />
</ServiceManifest>
```

### <a name="configure-hello-policy-by-using-a-local-account"></a>Konfigurowanie zasad hello za pomocą konta lokalnego
Po skonfigurowaniu hello usługi toohave punktu wejścia instalacji można zmienić uprawnienia zabezpieczeń hello, które zostanie uruchomiony w w manifeście aplikacji hello. Witaj poniższy przykład pokazuje, jak tooconfigure hello toorun usługi, w obszarze uprawnień konta użytkownika administrator.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupAdminUser" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupAdminUser">
            <MemberOf>
               <SystemGroup Name="Administrators" />
            </MemberOf>
         </User>
      </Users>
   </Principals>
</ApplicationManifest>
```

Najpierw utwórz **podmiotów** sekcji przy użyciu nazwy użytkownika, takie jak SetupAdminUser. Oznacza to, że użytkownik hello jest elementem członkowskim grupy hello Administratorzy systemu.

Następnie w obszarze hello **ServiceManifestImport** skonfiguruj tooapply zasad zbyt tego podmiotu zabezpieczeń**SetupEntryPoint**. To informuje usługi sieć szkieletowa który hello **MySetup.bat** uruchomieniu pliku, powinien być `RunAs` z uprawnieniami administratora. Biorąc pod uwagę, że masz *nie* zastosować zasady toohello główny punkt wejścia, kod hello w **MyServiceHost.exe** działa w systemie hello **NetworkService** konta. To konto domyślne hello, które wszystkich punktów wejścia usługi są uruchamiane jako.

Teraz Dodajmy hello pliku MySetup.bat toohello programu Visual Studio projektu tootest hello uprawnienia administratora. W programie Visual Studio kliknij prawym przyciskiem myszy projekt usługi hello i Dodaj nowy plik o nazwie MySetup.bat.

Następnie sprawdź, czy plik MySetup.bat hello jest uwzględniona w pakiecie usługi hello. Domyślnie nie jest. Wybierz plik hello, kliknij prawym przyciskiem myszy menu kontekstowe hello tooget i wybierz **właściwości**. Okno dialogowe właściwości hello, upewnij się, że **skopiuj tooOutput katalogu** ustawiono zbyt**Kopiuj, jeśli nowszy**. Zobacz hello następującego zrzutu ekranu.

![Visual Studio CopyToOutput SetupEntryPoint pliku wsadowego][image1]

Teraz Otwórz plik MySetup.bat hello i Dodaj hello następującego polecenia:

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

Następnie tworzenia i wdrażania hello rozwiązania tooa lokalny klaster projektowy. Po uruchomieniu usługi hello, jak pokazano w narzędziu Service Fabric Explorer, można zauważyć, że plik MySetup.bat hello zakończyła się pomyślnie na dwa sposoby. Otwórz wiersz polecenia programu PowerShell i wpisz:

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

Zanotuj nazwę hello hello węzła, gdy usługa hello została wdrożona i uruchomić w narzędziu Service Fabric Explorer — na przykład 2 węzła. Następnie przejdź toohello wystąpienia pracy folderu toofind hello out.txt pliku aplikacji pokazujący wartość hello **TestVariable**. Na przykład, jeśli ta usługa została wdrożonej tooNode 2, następnie przejdź toothis ścieżkę hello **MyApplicationType**:

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a>Konfigurowanie zasad hello przy użyciu konta systemu lokalnego
Często jest preferowana toorun hello uruchomienia skryptu przy użyciu konta systemu lokalnego, a nie konta administratora. Uruchamianie zasad RunAs hello jako członek grupy Administratorzy zwykle nie działa prawidłowo, ponieważ maszyny ma dostęp kontroli użytkownika (UAC) domyślnie włączone powitalne. W takich przypadkach **hello zaleca hello toorun SetupEntryPoint jako LocalSystem, zamiast jako grupa tooAdministrators dodano użytkownika lokalnego**. Witaj poniższy przykład przedstawia toorun SetupEntryPoint hello ustawienie jako system lokalny:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupLocalSystem" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupLocalSystem" AccountType="LocalSystem" />
      </Users>
   </Principals>
</ApplicationManifest>
```

## <a name="start-powershell-commands-from-a-setup-entry-point"></a>Uruchom polecenia programu PowerShell z punktu wejścia instalacji
toorun programu PowerShell z hello **SetupEntryPoint** punktu, możesz uruchomić **PowerShell.exe** w pliku wsadowego, który wskazuje tooa PowerShell plików. Najpierw należy dodać projekt usługi toohello plik programu PowerShell — na przykład **MySetup.ps1**. Pamiętaj tooset hello *Kopiuj, jeśli nowszy* właściwości, czy plik hello znajduje się również w pakiecie usługi hello. Witaj poniższy przykład przedstawia przykładowy plik partii, która rozpoczyna się plik programu PowerShell o nazwie MySetup.ps1, który określa zmienną środowiskową systemu o nazwie **TestVariable**.

Toostart MySetup.bat plik programu PowerShell:

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

W pliku programu PowerShell hello Dodaj powitania po tooset zmienną środowiskową systemu:

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> Domyślnie podczas uruchamiania pliku wsadowego hello wygląda w folderze aplikacji hello o nazwie **pracy** plików. W takim przypadku po uruchomieniu MySetup.bat chcemy tego hello toofind MySetup.ps1 w pliku hello sam folder, który jest aplikacji hello **pakietu kodu** folderu. toochange tego folderu, folder roboczy hello zestawu:
> 
> 

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    </ExeHost>
</SetupEntryPoint>
```

## <a name="use-console-redirection-for-local-debugging"></a>Użyj konsoli dla debugowania lokalnego
Czasami jest przydatne toosee dane wyjściowe konsoli hello uruchamiania skryptu na potrzeby debugowania. toodo, można ustawić zasad przekierowania konsoli, który zapisuje plik tooa wyjściowy hello. Witaj plik wyjściowy nosi nazwę folderu aplikacji napisanych toohello **dziennika** w węźle hello, gdzie aplikacja hello jest wdrożony i uruchom. (Zobacz gdzie toofind to w poprzedzających przykład hello.)

> [!WARNING]
> Nigdy nie używaj zasad przekierowania konsoli hello w aplikacji, która jest wdrożony w środowisku produkcyjnym, ponieważ może to mieć wpływ na powitania aplikacji w tryb failover. *Tylko* użyć tej funkcji dla rozwoju lokalnych i debugowania.  
> 
> 

Witaj poniższy przykład przedstawia przekierowywania konsoli hello ustawienie z wartością FileRetentionCount:

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

Jeśli zmienisz teraz hello MySetup.ps1 pliku toowrite **Echo** polecenie to zapisze plik wyjściowy toohello na potrzeby debugowania:

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

**Po debugowania skryptu, natychmiast usunąć te zasady przekierowania konsoli**.

## <a name="configure-a-policy-for-service-code-packages"></a>Konfigurowanie zasad dla pakietów kodu usługi
W poprzednich krokach hello, przedstawiono sposób tooapply tooSetupEntryPoint zasad RunAs. Oto bardziej szczegółowe w sposób toocreate różnych podmiotów zabezpieczeń, które mogą być stosowane jako usługi zasady.

### <a name="create-local-user-groups"></a>Tworzenie grup użytkowników lokalnych
Można zdefiniować i Utwórz grupy użytkowników pozwalają na użycie jednego lub więcej użytkowników toobe dodano grupę tooa. Jest to przydatne, jeśli jest wielu użytkowników do innej usługi, punkty wejścia i muszą toohave niektórych typowych uprawnień, które są dostępne na poziomie grupy hello. Witaj poniższy przykład przedstawia grupy lokalnej o nazwie **LocalAdminGroup** z uprawnieniami administratora. Dwóch użytkowników, Customer1 i Customer2, zostają członkami tej grupy lokalnej.

```xml
<Principals>
 <Groups>
   <Group Name="LocalAdminGroup">
     <Membership>
       <SystemGroup Name="Administrators"/>
     </Membership>
   </Group>
 </Groups>
  <Users>
     <User Name="Customer1">
        <MemberOf>
           <Group NameRef="LocalAdminGroup" />
        </MemberOf>
     </User>
    <User Name="Customer2">
      <MemberOf>
        <Group NameRef="LocalAdminGroup" />
      </MemberOf>
    </User>
  </Users>
</Principals>
```

### <a name="create-local-users"></a>Tworzenie użytkowników lokalnych
Można utworzyć użytkownika lokalnego, które mogą być używane toohelp bezpiecznego usługi aplikacji hello. Gdy **LocalUser** typ konta jest określone w sekcji podmiotów hello manifestu aplikacji hello, sieć szkieletowa usług tworzy lokalne konta użytkowników na komputerach, w której wdrażana jest aplikacja hello. Domyślnie te konta nie mają hello tej samej nazwy jak określone w aplikacji hello manifestu (na przykład Customer3 w hello następujące przykładowe). Zamiast tego są generowane dynamicznie i losowego hasła.

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

Jeśli aplikacja wymaga czy hello konto użytkownika i hasło być taka sama na wszystkich komputerach (na przykład uwierzytelnianie NTLM tooenable), hello manifestu klastra musi ustawić NTLMAuthenticationEnabled tootrue. Witaj manifestu klastra musi również określać NTLMAuthenticationPasswordSecret, który jest używany toogenerate hello tego samego hasła na wszystkich komputerach.

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a>Przypisz zasady toohello pakietów kodu usługi
Witaj **RunAsPolicy** sekcji **ServiceManifestImport** Określa konto hello z sekcji hello podmiotów zabezpieczeń, który ma być używane toorun pakiet kodu. Kodu manifestu pakietów z usługi hello również kojarzy z kontami użytkowników w sekcji podmiotów hello. Można to określić dla ustawienia hello lub punkty wejścia głównego, lub możesz określić `All` tooapply on tooboth. Witaj poniższy przykład przedstawia różne zasady są stosowane:

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

Jeśli **EntryPointType** nie zostanie określony, domyślnie hello jest zaznaczona tooEntryPointType = "Main". Określanie **SetupEntryPoint** jest szczególnie przydatne, gdy trzeba toorun pewnych operacji ustawienia wysokiego poziomu przy użyciu konta system. Kod obsługi rzeczywistych Hello można uruchamiany na koncie dolna uprawnień.

### <a name="apply-a-default-policy-tooall-service-code-packages"></a>Zastosowanie pakietów kodu usługi tooall domyślne zasady
Użyj hello **DefaultRunAsPolicy** toospecify sekcji domyślne konto użytkownika dla wszystkich pakietów kodu, które nie mają określonej **RunAsPolicy** zdefiniowane. Jeśli większość hello pakiety kodu, które są określone w manifeście usługi hello używany przez aplikację muszą toorun w obszarze hello tego samego użytkownika, powitalne aplikacji można zdefiniować tylko domyślnych zasad RunAs przy użyciu tego konta użytkownika. Witaj poniższy przykład określa, że jeśli pakiet kodu nie ma **RunAsPolicy** określony pakiet kodu hello należy uruchamiać w ramach hello **MyDefaultAccount** określone w sekcji podmiotów hello.

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a>Użyj grupy domeny usługi Active Directory lub użytkownika
W przypadku wystąpienia usługi Service Fabric, który został zainstalowany w systemie Windows Server przy użyciu hello Autonomiczny Instalator rozszerzenia można uruchomić usługi hello hello poświadczenia dla konta użytkownika lub grupy usługi Active Directory. To jest usługa Active Directory lokalnie w domenie, a nie z usługą Azure Active Directory (Azure AD). Przy użyciu użytkownika domeny lub grupy, można następnie dostęp do innych zasobów w domenie hello (na przykład udziałów plików), które ma odpowiednie uprawnienia.

Witaj poniższy przykład przedstawia użytkownika usługi Active Directory o nazwie *TestUser* z ich domeny o nazwie hasła szyfrowane przy użyciu certyfikatu *MyCert*. Można użyć hello `Invoke-ServiceFabricEncryptText` PowerShell polecenie toocreate hello tajny szyfrowania tekstu. Zobacz [Zarządzanie kluczy tajnych w aplikacji usługi Service Fabric](service-fabric-application-secret-management.md) szczegółowe informacje.

Klucz prywatny hello hello certyfikatu toodecrypt hello hasła toohello komputer lokalny należy wdrożyć przy użyciu metody poza pasmem (na platformie Azure jest za pośrednictwem usługi Azure Resource Manager). Następnie gdy usługa sieć szkieletowa wdraża hello usługi pakietu toohello maszyny, jest klucz tajny hello stanie toodecrypt i (wraz z nazwy użytkownika hello) uwierzytelniania za pomocą usługi Active Directory toorun w ramach tych poświadczeń.

```xml
<Principals>
  <Users>
    <User Name="TestUser" AccountType="DomainUser" AccountName="Domain\User" Password="[Put encrypted password here using MyCert certificate]" PasswordEncrypted="true" />
  </Users>
</Principals>
<Policies>
  <DefaultRunAsPolicy UserRef="TestUser" />
  <SecurityAccessPolicies>
    <SecurityAccessPolicy ResourceRef="MyCert" PrincipalRef="TestUser" GrantRights="Full" ResourceType="Certificate" />
  </SecurityAccessPolicies>
</Policies>
<Certificates>
```
### <a name="use-a-group-managed-service-account"></a>Użyj grupy zarządzane konto usługi.
W przypadku wystąpienia usługi Service Fabric, który został zainstalowany w systemie Windows Server przy użyciu hello Autonomiczny Instalator rozszerzenia można uruchomić usługi hello jako grupa kont usług zarządzanych (gMSA). Należy pamiętać, że jest to usługi Active Directory lokalnie w domenie, a nie z usługą Azure Active Directory (Azure AD). Za pomocą grupę nie jest hasłem ani zaszyfrowane hasło przechowywane w hello `Application Manifest`.

Witaj poniższy przykład przedstawia sposób toocreate konto usługi zarządzane przez grupę o nazwie *testu svc$*; sposób toodeploy zarządzania węzłów klastra toohello konta usługi; i jak tooconfigure hello głównej nazwy użytkownika.

##### <a name="prerequisites"></a>Wymagania wstępne.
- Witaj domeny musi mieć klucz główny KDS.
- Witaj domeny musi toobe w systemie Windows Server 2012 lub nowszego poziomu funkcjonalności.

##### <a name="example"></a>Przykład
1. Poproś administratora domeny usługi active directory Utwórz konto usługi zarządzane przez grupę przy użyciu hello `New-ADServiceAccount` apletu polecenia i upewnij się, że hello `PrincipalsAllowedToRetrieveManagedPassword` zawiera wszystkie węzły klastra sieci szkieletowej usług hello. Należy pamiętać, że `AccountName`, `DnsHostName`, i `ServicePrincipalName` muszą być unikatowe.
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. Na każdym z węzłów klastra sieci szkieletowej usług hello (na przykład `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), zainstalować i przetestować hello gMSA.
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. Skonfiguruj hello głównej nazwy użytkownika oraz hello RunAsPolicy tooreference hello użytkownika.
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="DomaingMSA"/>
      </Policies>
   </ServiceManifestImport>
  <Principals>
    <Users>
      <User Name="DomaingMSA" AccountType="ManagedServiceAccount" AccountName="domain\svc-Test$"/>
    </Users>
  </Principals>
</ApplicationManifest>
```

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a>Przypisać zasady zabezpieczeń dostępu dla punktów końcowych HTTP i HTTPS
Jeśli stosujesz usługi tooa zasad RunAs i manifestu usługi hello deklaruje punktu końcowego zasobów przy użyciu protokołu hello HTTP, musisz określić **SecurityAccessPolicy** tooensure, że porty przydzielone toothese punkty końcowe są prawidłowo Kontrola dostępu wyświetlane hello konto użytkownika Uruchom jako, które jest uruchamiana usługa hello. W przeciwnym razie **http.sys** nie ma dostępu do usługi toohello i uzyskać awarii przy wywołaniach z powitania klienta. Witaj następujący przykład dotyczy hello Customer1 tooan punkt końcowy konta o nazwie **EndpointName**, które zapewnia pełne prawa dostępu.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

Hello punktu końcowego protokołu HTTPS należy również mieć nazwę hello tooindicate hello certyfikatu tooreturn toohello klienta. Można to zrobić za pomocą **EndpointBindingPolicy**, z certyfikatem hello zdefiniowanej w sekcji certyfikaty w manifeście aplikacji hello.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a>Uaktualnianie wielu aplikacji z punktów końcowych https
Toobe należy zachować ostrożność nie toouse hello **tego samego portu** dla różnych wystąpień hello tej samej aplikacji przy użyciu protokołu http**s**. Przyczyna Hello jest, że sieć szkieletowa usług nie będzie możliwe tooupgrade hello certyfikatu dla jednego z wystąpień aplikacji hello. Na przykład, aplikacja 1 lub aplikacji 2 zarówno tooupgrade ich toocert cert 1, 2. W przypadku uaktualniania hello sieci szkieletowej usług może mieć wyczyścić rejestracji certyfikatu 1 hello przy użyciu składnika http.sys nawet hello jest nadal używa jej inna aplikacja. tooprevent, sieć szkieletowa usług wykryje, że istnieje już inne wystąpienie aplikacji zarejestrowanych na powitania portu z certyfikatem hello (z powodu toohttp.sys) i operacji hello kończy się niepowodzeniem.

Dlatego usługi sieć szkieletowa nie obsługuje uaktualnienia z dwóch różnych usług za pomocą **hello tego samego portu** w innej aplikacji wystąpień. Innymi słowy, nie można użyć hello sam certyfikat na różnych usług na powitania tego samego portu. Jeśli potrzebujesz toohave udostępnionej certyfikatów na powitania sam port, należy tooensure tego hello usług są umieszczane na kilka różnych maszyn z ograniczeń umieszczania. Lub należy wziąć pod uwagę przy użyciu portów dynamicznych sieci szkieletowej usług, jeśli to możliwe dla każdej usługi w każdego wystąpienia aplikacji. 

Jeśli widzisz uaktualnienia kończy się niepowodzeniem z protokołu https, błąd ostrzeżenie "hello interfejsu API serwera HTTP systemu Windows nie obsługuje wielu certyfikatów dla aplikacji, które współużytkują port".

## <a name="a-complete-application-manifest-example"></a>W przykładzie manifestu kompletna aplikacja
powitania po manifest aplikacji zawiera wiele hello różne ustawienia:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application3Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="Stateless1_InstanceCount" DefaultValue="-1" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
         <RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup" />
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed hello EndpointName is secured with https -->
        <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
     </Policies>
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="Stateless1">
         <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
   <Principals>
      <Groups>
         <Group Name="LocalAdminGroup">
            <Membership>
               <SystemGroup Name="Administrators" />
            </Membership>
         </Group>
      </Groups>
      <Users>
         <User Name="LocalAdmin">
            <MemberOf>
               <Group NameRef="LocalAdminGroup" />
            </MemberOf>
         </User>
         <!--Customer1 below create a local account that this service runs under -->
         <User Name="Customer1" />
         <User Name="MyDefaultAccount" AccountType="NetworkService" />
      </Users>
   </Principals>
   <Policies>
      <DefaultRunAsPolicy UserRef="LocalAdmin" />
   </Policies>
   <Certificates>
     <EndpointCertificate Name="Cert1" X509FindValue="FF EE E0 TT JJ DD JJ EE EE XX 23 4T 66 "/>
  </Certificates>
</ApplicationManifest>
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Następne kroki
* [Zrozumienie modelu aplikacji hello](service-fabric-application-model.md)
* [Określ zasoby w manifeście usługi](service-fabric-service-manifest-resources.md)
* [Wdrażanie aplikacji](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
