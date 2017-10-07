---
title: "aaaUnderstand tożsamości Azure | Dokumentacja firmy Microsoft"
description: "Uzyskaj podstawową wiedzę na temat warunków rozwiązania tożsamości Microsoft Azure, pojęcia i zalecenia dotyczące możesz toomake hello najlepsze tożsamości ładu decyzja dla danej organizacji."
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/17/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4d9c90bd7a6bcc9637be3107998f9da5bd4cbdae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-identity-solutions"></a>Zrozumienie Azure tożsamościach
Microsoft Azure Active Directory (Azure AD) to rozwiązanie chmury zarządzania tożsamościami i dostępem, który udostępnia usługi katalogowe, Zarządzanie tożsamościami i zarządzania dostępem do aplikacji. Usługi Azure AD szybko [umożliwia logowanie jednokrotne (SSO)](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-sso) too1, 000 wstępnie zintegrowanych aplikacji handlowych i niestandardowych w hello [galerii aplikacji Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/). Wiele z tych aplikacji prawdopodobnie już używasz usługi Office 365, witryny Salesforce.com, pola, usługi ServiceNow i produktu Workday.

Jeden katalog usługi Azure AD jest automatycznie kojarzony z subskrypcją platformy Azure, podczas jego tworzenia. Jako hello tożsamości usługi na platformie Azure następnie usługi Azure AD zapewnia wszystkie Zarządzanie tożsamościami i funkcji kontroli dostępu do zasobów w chmurze. Tych zasobów może zawierać użytkowników, aplikacji i grup dla poszczególnych dzierżawców (organizacja), pokazane na powitania po diagramu:

![Usługa Azure Active Directory](./media/understand-azure-identity-solutions/azure-ad.png)

Microsoft Azure oferuje kilka sposobów tooleverage tożsamości jako usługa (IDaaS) o różnej złożoności toomeet potrzeby poszczególnych organizacji. Witaj dalszej części tego artykułu pomaga w zrozumieniu terminologii podstawowe tożsamość platformy Azure i pojęć, a także zalecenia dotyczące możesz toomake hello najlepszym wyborem hello opcje.

## <a name="terms-tooknow"></a>Warunki tooknow

Przed podjęciem decyzji na rozwiązanie tożsamość platformy Azure dla organizacji, należy podstawową wiedzę na temat warunków hello najczęściej używanych w przypadku usług tożsamość platformy Azure.

|Tooknow termin| Opis|
|-----|-----|
|Subskrypcja platformy Azure |Subskrypcje są używane toopay dla usług w chmurze Azure i zwykle połączonego tooa karty kredytowej. Może mieć kilka subskrypcji, ale może być trudne tooshare zasobów między subskrypcjami.|
|Dzierżawą platformy Azure | Dzierżawa usługi Azure AD jest reprezentatywna dla pojedynczej organizacji. Jest dedykowany zaufanych wystąpienie usługi Azure AD, który jest automatycznie tworzony, gdy organizacja rejestruje się w subskrypcji usługi chmury firmy Microsoft, takich jak Azure, Intune lub usługi Office 365. Dzierżawcy mogą uzyskać dostęp tooservices w dedykowanym środowisku (pojedynczej dzierżawy) lub współużytkowanego środowiska z innymi organizacjami (wielodostępnej).|
|Katalog usługi Azure AD | Poszczególne dzierżawy Azure zawierają Azure dedykowanym, zaufany katalog AD, która zawiera użytkowników, grup i aplikacji hello dzierżawy. Jest używane tooperform funkcje zarządzania tożsamościami i dostępem do zasobów dzierżawy. Ponieważ unikatowego katalogu usługi Azure AD jest automatycznie aprowizowanego toorepresent organizacji, po utworzeniu konta dla usługi w chmurze Microsoft Azure, Microsoft Intune lub usługi Office 365, czasami zobaczysz warunki hello *dzierżawy*, *Usługi azure AD*, i *katalog usługi Azure AD* używane zamiennie. |
|Domena niestandardowa | Po utworzeniu najpierw konta dla subskrypcji usługi Microsoft cloud, dzierżawy (organizacja) używa *. onmicrosoft.com* nazwy domeny. Jednak większość organizacji mają nazwy domeny, które są używane toodo działalności biznesowej i że użytkownicy końcowi korzystanie z zasobów firmy tooaccess. Można dodać użytkownika domeny niestandardowej nazwy tooAzure AD tak, aby hello nazwa domeny jest tooyour znanych użytkowników, takich jak  *alice@contoso.com*  zamiast  *alice@contoso.onmicrosoft.com* . |
|Konto Azure AD | Są to tożsamości, które są tworzone za pomocą usługi Azure AD lub innej usługi chmury firmy Microsoft, takich jak Office 365. Są one przechowywane w usłudze Azure AD i dostępny tooany subskrypcji usług w chmurze hello organizacji. |
|Administratorem subskrypcji platformy Azure| administrator konta Hello jest hello, kto utworzył konto na lub zakupiono hello subskrypcji platformy Azure. Mogą używać hello [Centrum konta](https://account.windowsazure.com/Home/Index) tooperform różne zadania zarządzania, takich jak tworzyć subskrypcje, anulowanie subskrypcji, zmienić hello rozliczeń dla subskrypcji lub zmień hello administratora usługi. |
|Administrator globalny usługi Azure AD | Administratorzy globalni usługi Azure AD ma funkcje administracyjne tooall usługi Azure AD pełny dostęp. Hello osoby, która zarejestruje się w subskrypcji usługi Microsoft cloud automatycznie staje się administratorem globalnym domyślnie. Może mieć więcej niż jednego administratora globalnego, ale wyłącznie administratorzy globalni mogą przypisywać każdą z [hello innych ról administratora](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) toousers. |
|Konto Microsoft | Konta Microsoft (utworzone przez Ciebie do użytku osobistego) podaj dostępu zorientowane na tooconsumer produktów firmy Microsoft i usługami w chmurze, takich jak Outlook (usługi Hotmail), OneDrive, Xbox LIVE lub usługi Office 365. Te tożsamości są tworzone i przechowywane w hello Microsoft konta system obsługi tożsamości konsumentów firmy Microsoft.|
|Konta służbowe | Konta służbowe (wystawiony przez administratora dla firm/uczelni Użyj) zapewniają dostęp tooenterprise biznesowej usług chmurowych firmy Microsoft, takich jak Azure, Intune lub usługi Office 365.|


## <a name="concepts-toounderstand"></a>Pojęcia dotyczące toounderstand

Teraz, znając hello tożsamość platformy Azure podstawowe warunki można należy dowiedzieć się więcej o tych pojęć tożsamość platformy Azure, które ułatwiają podjęcie decyzji usługi świadomych tożsamość platformy Azure.

|Toounderstand koncepcji |Opis|
|-----|-----|
|[Jak subskrypcje platformy Azure są kojarzone z usługą Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-how-subscriptions-associated-directory) |Każda subskrypcja platformy Azure ma relację zaufania z usługi Azure AD directory tooauthenticate użytkowników, usług i urządzeń. *Wiele subskrypcji może ufać katalogu hello tej samej usługi Azure AD, ale subskrypcji będą ufać tylko jeden katalog usługi Azure AD*. Relacja zaufania między różni się od relacji hello, która subskrypcji z innych zasobów platformy Azure (witrynami sieci Web, baz danych i tak dalej), które przypominają bardziej podrzędne zasoby subskrypcji. Jeśli subskrypcja wygaśnie, dostęp tooresources skojarzone z subskrypcją hello innego niż Azure AD również zatrzymywany. Jednak hello Azure AD directory pozostanie na platformie Azure, dzięki czemu można skojarzyć z nim inną subskrypcję i kontynuować toomanage zasoby dzierżawcy.|
|[Jak Azure AD licencjonowania działania](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-get-started-azure-portal) | Gdy zakupu lub uaktywnianie Enterprise Mobility Suite, Azure AD Premium i Azure AD podstawowa, katalog jest aktualizowane hello subskrypcji, w tym okresie ważności i Przedpłata licencji. Po hello subskrypcja jest aktywna, można zarządza Administratorzy globalni usługi Azure AD i używane przez licencjonowani użytkownicy hello usługi. Informacji o subskrypcji, w tym hello liczby przydzielonych lub dostępnych licencji, jest dostępna w portalu Azure z hello hello **usługi Azure Active Directory** > **licencji** bloku. To jest również hello najlepsze miejsce toomanage przypisaniami licencji.|
|[Oparta na rolach kontrola dostępu w hello portalu Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)|Azure opartej na rolach kontroli dostępu (RBAC) zapewnia precyzyjne zarządzanie dostępem do zasobów platformy Azure. Zbyt wiele uprawnienia można ujawnić i tooattackers konta. Za mało uprawnienia oznacza, że pracownicy nie można pobrać ich pracować wydajnie. Przy użyciu funkcji RBAC, można udzielać pracownikom hello dokładne uprawnienia, których potrzebują oparte na trzy podstawowe role stosowane tooall grup zasobów: właściciela, współautora, czytnika. Można również utworzyć zapasowej too2, 000 własny [niestandardowe role RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles) toomeet swoich potrzeb. |
|[Tożsamość hybrydowa](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)|Tożsamość hybrydowa jest osiągane dzięki integracji z lokalnymi Windows Server Active Directory (AD DS) przy użyciu usługi Azure AD [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect). Dzięki temu tooprovide wspólną tożsamością dla użytkowników usługi Office 365, Azure i aplikacjami lokalnymi lub aplikacji SaaS zintegrowanych z usługą Azure AD. Tożsamość hybrydowa można skutecznie rozszerzanie lokalnego środowiska chmury toohello tożsamościami i dostępem.|

### <a name="hello-difference-between-windows-server-ad-ds-and-azure-ad"></a>Różnica Hello systemu Windows Server AD DS i Azure AD
Zarówno usługi Azure Active Directory (Azure AD) i lokalnej usługi Active Directory (usługi domenowe Active Directory lub usług AD DS) są systemy, które przechowują dane katalogów i zarządzania komunikacją między użytkownikami i zasobów, w tym procesami logowania użytkowników, uwierzytelniania i wyszukiwania w katalogu.

Jeśli już znasz z lokalnego systemu Windows serwera usług domenowych Active Directory (AD DS), po raz pierwszy wprowadzone w systemie Windows 2000 Server, a następnie prawdopodobnie rozumiesz podstawowe pojęcia hello tożsamości usługi. Jednak jest również toounderstand ważne, czy usługi Azure AD nie jest po prostu kontrolerem domeny w chmurze hello. Jest to całkowicie nowa sposób zapewnienia tożsamości jako usługa (IDaaS) na platformie Azure wymaga to całkowicie nowa sposób planowania toofully objęło oparte na chmurze możliwości i chronić organizację przed współczesnych zagrożeń. 

Usługi AD DS to rola serwera w systemie Windows Server, co oznacza, że można wdrożyć na fizycznych lub maszynach wirtualnych. Ma strukturę hierarchiczną oparte na X.500. Lokalizowanie obiektów, może być interakcji z przy użyciu protokołu LDAP, a przede wszystkim używa protokołu Kerberos do uwierzytelniania używa DNS. Active Directory umożliwia jednostek organizacyjnych (OU) i obiektów zasad grupy (GPO) Ponadto toojoining maszyny toohello domeny i relacje zaufania są tworzone między domenami.

IT zabezpieczył ich granicznej zabezpieczeń dla lat za pomocą usług AD DS, ale przedsiębiorstw nowoczesny, obwodowej bez obsługi potrzeb tożsamości dla pracowników, klienci i partnerzy wymagają nowej płaszczyzny formantu. Usługi Azure AD jest tej płaszczyzny kontroli tożsamości. Zabezpieczeń został przeniesiony poza hello firmowej zapory toohello chmury, jeśli usługi Azure AD chroni dostępu i zasobów firmy, podając jedną wspólną tożsamość użytkowników (lokalnie lub w chmurze hello). Dzięki temu Twojej toosecurely elastyczność hello użytkowników aplikacji hello dostępu potrzebują tooget pracy z prawie każdego urządzenia. Formanty ochrony bezproblemowe danych opartych na ryzyko, obsługiwane przez możliwości usługi machine learning szczegółowe raporty, podawane są również tej IT firmy tookeep potrzeb danych.

Usługi Azure AD to usługa katalogowa publicznego wielu klientów, co oznacza, że w ramach usługi Azure AD można utworzyć dzierżawy dla serwerów w chmurze i aplikacje, takie jak usługi Office 365. Użytkownicy i grupy są tworzone w płaskiej strukturze bez jednostek organizacyjnych i obiektów zasad grupy. Uwierzytelnianie jest przeprowadzane za pośrednictwem protokołów, takich jak SAML, WS-Federation i OAuth. Jest możliwe tooquery usługi Azure AD, ale zamiast LDAP należy użyć interfejsu API REST wywołuje interfejs API Graph usługi AD. Te wszystkie pracy za pośrednictwem protokołu HTTP i HTTPS.

### <a name="extend-office-365-management-and-security-capabilities"></a>Rozszerzyć możliwości zarządzania i zabezpieczeń usługi Office 365
Już używasz usługi Office 365? Twoje przekształcania cyfrowego można przyspieszyć przez rozszerzanie wbudowanych możliwości usługi Office 365 z usługą Azure AD toosecure wszystkich zasobów, włączanie bezpiecznego wydajności dla całej pracowników. Gdy używasz usługi Azure AD, oprócz możliwości tooOffice 365, można zabezpieczyć portfela całej aplikacji z jedną tożsamość, która umożliwia logowanie jednokrotne dla wszystkich aplikacji. Możesz rozszerzyć możliwości dostępu warunkowego, nie tylko na podstawie lokalizacji stanu, ale użytkownika, urządzenia, aplikacji i również ryzyko. Możliwości usługi Multi-Factor authentication (MFA) podaj dodatkową ochronę, gdy zajdzie taka potrzeba. Będzie uzyskanie dodatkowych nadzoru uprawnień użytkownika i zapewnienia dostępu administracyjnego na żądanie, w czasie. Użytkownicy są bardziej wydajni i utworzyć mniej biletów pomocy technicznej, Dziękujemy toohello samoobsługi możliwości usługi Azure AD zapewnia takie jak zresetować zapomniane hasła, żądania dostępu do aplikacji oraz tworzenie grup i zarządzanie nimi.

> [!TIP]
> Chcesz toolearn więcej o korzystaniu z usługi Azure AD identity zarządzania z usługi Office 365? [Pobierz hello e-book](https://info.microsoft.com/Extend-Office-365-security-with-EMS.html).

## <a name="microsoft-azure-identity-solutions"></a>Tożsamości na platformie Microsoft Azure

Microsoft Azure oferuje kilka sposobów toomanage tożsamości użytkowników czy są one obsługiwane pełni lokalnie, tylko w hello chmury, lub nawet innym między nimi. Możliwe opcje: Zrób usług AD DS (DIY) w Azure, Azure Active Directory (Azure AD), tożsamość hybrydowa i usługi domenowe Azure AD.

### <a name="do-it-yourself-diy-ad-ds"></a>Zrób (DIY) AD DS
Dla firm, które wymagają niewielkie rozmiary w chmurze hello **Zrób usług AD DS (DIY)** na platformie Azure mogą być używane. Ta opcja obsługuje wiele scenariuszy systemu Windows Server AD DS, które dobrze nadają się do wdrażania maszyn wirtualnych (VM) na platformie Azure. Na przykład można utworzyć maszyny Wirtualnej platformy Azure jako kontroler domeny z systemem w odległych centrum danych, które jest połączone toohello sieci zdalnej. Tam hello maszyny Wirtualnej może być możliwe toosupport żądania uwierzytelniania od zdalnych użytkowników i poprawić wydajność uwierzytelniania. Ta opcja jest również nadają się jako substitute stosunkowo ekonomicznych toootherwise kosztowne awaryjnego odzyskiwania lokacji, udostępniając niewielkiej liczby kontrolerów domeny i jednej sieci wirtualnych na platformie Azure. Na koniec możesz konieczne toodeploy aplikacji na platformie Azure, takich jak SharePoint, który wymaga systemu Windows Server AD DS, ale ma nie zależności w sieci lokalnej hello lub hello firmy Windows Server Active Directory. W takim przypadku można wdrożyć odizolowanym lesie na wymagania dotyczące platformy Azure toomeet hello programu SharePoint farmy serwerów. Również obsługiwał toodeploy sieci aplikacji, które wymagają sieci lokalnej toohello łączności i hello lokalnej usługi Active Directory.

### <a name="azure-active-directory-azure-ad"></a>Azure Active Directory (Azure AD)
**Azure AD autonomiczny** jest całkowicie opartej na chmurze zarządzania tożsamościami i dostępem jako rozwiązaniem Service (IDaaS). Usługi Azure AD zapewnia niezawodny zestaw funkcji toomanage użytkowników i grup. Pomaga zabezpieczyć tooon dostępu lokalnego i w chmurze, aplikacji, takich jak usługi sieci web firmy Microsoft, takich jak usługi Office 365 i wiele oprogramowania firmy Microsoft jako aplikacje usługi (SaaS). Usługi Azure AD jest dostarczany w trzech wersjach: bezpłatne, Basic i Premium. Usługi Azure AD zwiększa wydajność organizacji i zwiększa zabezpieczeń poza hello obwodowej zapory tooa nowego formantu płaszczyzny chroniona przez uczenie maszynowe Azure i inne zaawansowane funkcje zabezpieczeń.

### <a name="hybrid-identity"></a>Tożsamość hybrydowa
Zamiast wybór między lokalnymi lub tożsamościach oparte na chmurze, wiele planowania do przodu dyrektorzy działu informatyki i firm, które zaczęli przewidywanie kierunek długoterminowe firmy rozszerzania lokalnych katalogów toohello chmury za pomocą **tożsamość hybrydowa** rozwiązania. Tożsamość hybrydowa uzyskać tożsamość prawdziwie globalna i rozwiązanie do zarządzania dostępu, który udostępnia bezpieczne i produktywności użytkowników aplikacji toohello musi toodo swoich zadań.

> [!TIP]
> więcej informacji o toolearn jak dyrektorzy działu informatyki wprowadzonych usługi Azure Active Directory centralnej częścią strategii IT, Pobierz hello [tooAzure przewodnik dyrektorów usługi Active Directory](https://aka.ms/AzureADCIOGuide).

### <a name="azure-ad-domain-services"></a>Azure AD Domain Services
**Usługi domenowe Azure AD** zapewnia oparte na chmurze opcja toouse usług AD DS lekką kontrolkę konfiguracji maszyny Wirtualnej platformy Azure i toomeet sposób wymogów dotyczących lokalnego tożsamości sieci projektowanie i testowanie aplikacji. Usługi domenowe Azure AD nie ma toolift i przesunięcia lokalnej tooAzure infrastruktury usług AD DS maszyn wirtualnych zarządzanych przez usługi domenowe Azure AD. Zamiast tego hello maszynach wirtualnych platformy Azure w domenach zarządzanych powinny być używane toosupport hello programowanie, testowania i przenoszenie aplikacji lokalnych, które wymagają chmury toohello metod uwierzytelniania usług AD DS.

## <a name="common-scenarios-and-recommendations"></a>Typowe scenariusze i zalecenia

Oto kilka typowych scenariuszy tożsamościami i dostępem na podstawie zaleceń toowhich opcji tożsamość platformy Azure może być najbardziej właściwa dla każdego.

|Scenariusza z tożsamością| Zalecenie|
|-----|-----|
|Moja organizacja wprowadził dużych inwestycji w usłudze Active Directory lokalnego systemu Windows Server, ale chcemy tooextend tożsamości toohello chmury.| Witaj najczęściej używane rozwiązanie tożsamość platformy Azure jest [tożsamość hybrydowa](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview). Jeśli zostały już wprowadzone inwestycji w lokalnej instalacji usług AD DS, można z łatwością rozszerzyć chmury toohello tożsamości za pomocą usługi Azure AD Connect.|
|Moja firma powstał w chmurze hello i mamy nie inwestycji w lokalnych rozwiązaniach tożsamości.| [Usługa Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) jest najlepszym wyborem hello dla firm tylko w chmurze bez lokalnej inwestycji.|
|Potrzebuję lekkie maszyny Wirtualnej Azure konfiguracji i kontroli toomeet wymogów dotyczących lokalnego tożsamości do tworzenia aplikacji i testowania.|[Usługi domenowe Azure AD](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-overview) jest dobrym rozwiązaniem, jeśli potrzebny toouse usług AD DS lekką kontrolkę konfiguracji maszyny Wirtualnej platformy Azure lub szukasz toodevelop lub migracji chmury toohello aplikacji starszy, obsługujący katalogu lokalnego.|  
|Potrzebuję toosupport kilka maszyn wirtualnych na platformie Azure, ale mojej firmy jest nadal silnie zainwestowały w lokalnej Active Directory (AD DS).|Użyj [DIY usług AD DS](https://msdn.microsoft.com/library/azure/jj156090.aspx) toouse maszynach wirtualnych platformy Azure, gdy należy toosupport kilka maszyn wirtualnych i ma duże usług AD DS inwestycji lokalnej. |

## <a name="where-can-i-learn-more"></a>Gdzie można dowiedzieć się więcej?
Mamy wiele możliwości toohelp online doskonałe zasoby, które użytkownik pozna wszystkie informacje dotyczące usługi Azure AD. Poniżej przedstawiono listę tooget dużą artykuły, możesz uruchomić:

* [Włączanie katalogu dla hybrydowego zarządzania za pomocą usługi Azure AD Connect](active-directory-aadconnect.md)
* [Dodatkowe zabezpieczenia kiedykolwiek połączonych świata](../multi-factor-authentication/multi-factor-authentication.md)
* [Automatyzowanie Inicjowanie obsługi użytkowników i anulowania zastrzeżenia tooSaaS aplikacji za pomocą usługi Azure Active Directory](active-directory-saas-app-provisioning.md)
* [Wprowadzenie do raportów usługi Azure AD](active-directory-reporting-getting-started.md)
* [Zarządzanie haseł z dowolnego miejsca](active-directory-passwords.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Automatyzowanie Inicjowanie obsługi użytkowników i anulowania zastrzeżenia tooSaaS aplikacji za pomocą usługi Azure Active Directory](active-directory-saas-app-provisioning.md)
* [Jak tooprovide bezpiecznego dostępu zdalnego tooon lokalnej aplikacji](active-directory-application-proxy-get-started.md)
* [Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory](active-directory-manage-groups.md)
* [Co to jest licencjonowania usługi Microsoft Azure Active Directory?](active-directory-licensing-what-is.md)
* [Jak odnajdywać niezatwierdzone aplikacje w chmurze używanych mojej organizacji](active-directory-cloudappdiscovery-whatis.md)

## <a name="next-steps"></a>Następne kroki

Znasz koncepcji tożsamość platformy Azure i tooyou dostępne opcje hello program hello następujące zasoby tooget uruchomiona implementującej hello opcji wybrany:

[Dowiedz się więcej o tożsamościach hybrydowe platformy Azure](https://docs.microsoft.com/azure/active-directory/choose-hybrid-identity-solution)

[Dowiedz się więcej w środowisku Azure koncepcji](https://aka.ms/aad-poc)

[Wdrażanie usługi Azure AD w środowisku produkcyjnym](https://aka.ms/aad-onboard)
