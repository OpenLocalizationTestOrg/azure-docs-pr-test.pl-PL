---
title: "aaaAzure interfejsu API zarządzania — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Dowiedz się, że hello odpowiedzi na pytania toocommon wzorców i najlepsze rozwiązania w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 9e7cdf1b881a4dfed4bd2cfd7fbb4994f48b5f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-faqs"></a>Często zadawane pytania usługi Azure API Management
Pobieranie toocommon hello odpowiedzi na pytania, wzorców i najlepsze rozwiązania dotyczące usługi Azure API Management.

## <a name="contact-us"></a>Skontaktuj się z nami
* [Jak można żądanie zespołu Microsoft Azure API Management hello pytanie?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question)


## <a name="frequently-asked-questions"></a>Często zadawane pytania
* [Co to znaczy, gdy funkcja jest w wersji zapoznawczej?](#what-does-it-mean-when-a-feature-is-in-preview)
* [Jak można zabezpieczyć hello połączenia między hello interfejsu API zarządzania bramą i Moje usług zaplecza](#how-can-i-secure-the-connection-between-the-api-management-gateway-and-my-back-end-services)
* [Jak skopiować Moje zarządzanie interfejsami API wystąpienie tooa nowe wystąpienie usługi?](#how-do-i-copy-my-api-management-service-instance-to-a-new-instance)
* [Może zarządzać Mój wystąpienie interfejsu API zarządzania programowo?](#can-i-manage-my-api-management-instance-programmatically)
* [Jak dodać grupę Administratorzy toohello użytkowników?](#how-do-i-add-a-user-to-the-administrators-group)
* [Dlaczego jest zasad hello, że ma być tooadd niedostępne w edytorze zasad hello?](#why-is-the-policy-that-i-want-to-add-unavailable-in-the-policy-editor)
* [Jak używać wersji interfejsu API w usłudze API Management?](#how-do-i-use-api-versioning-in-api-management)
* [Jak skonfigurować wiele środowisk w jednego interfejsu API?](#how-do-i-set-up-multiple-environments-in-a-single-api)
* [Czy można używać protokołu SOAP z interfejsu API zarządzania?](#can-i-use-soap-with-api-management)
* [To jest hello interfejsu API zarządzania bramy IP address stała? Można jej używać w regułach zapory?](#is-the-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules)
* [Z zabezpieczeniami usług AD FS można skonfigurować serwera autoryzacji OAuth 2.0?](#can-i-configure-an-oauth-20-authorization-server-with-adfs-security)
* [Jakie metody routingu zarządzanie interfejsami API używa w lokalizacjach geograficznych toomultiple wdrożenia?](#what-routing-method-does-api-management-use-in-deployments-to-multiple-geographic-locations)
* [Można użyć toocreate szablonu usługi Azure Resource Manager wystąpienia usługi API Management?](#can-i-use-an-azure-resource-manager-template-to-create-an-api-management-service-instance)
* [Czy można użyć certyfikatu SSL z podpisem własnym dla wewnętrznej?](#can-i-use-a-self-signed-ssl-certificate-for-a-back-end)
* [Dlaczego uzyskać wystąpił błąd uwierzytelniania podczas tooclone repozytorium GIT?](#why-do-i-get-an-authentication-failure-when-i-try-to-clone-a-git-repository)
* [Zarządzanie interfejsami API działa z Azure ExpressRoute?](#does-api-management-work-with-azure-expressroute)
* [Dlaczego, po wdrożeniu usługi API Management do nich, jest wymagamy dedykowanych podsieci w stylu Menedżera zasobów sieci wirtualnych?](#why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them)
* [Co to jest rozmiar minimalny podsieci hello potrzebne podczas wdrażania interfejsu API zarządzania w sieci Wirtualnej?](#what-is-the-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet)
* [Z jednej tooanother subskrypcji można przenieść usługi API Management?](#can-i-move-an-api-management-service-from-one-subscription-to-another)
* [Czy istnieją ograniczenia dotyczące lub znane problemy z importowaniem Moje interfejsu API?](#are-there-restrictions-on-or-known-issues-with-importing-my-api)

### <a name="how-can-i-ask-hello-microsoft-azure-api-management-team-a-question"></a>Jak można żądanie zespołu Microsoft Azure API Management hello pytanie?
Użytkownik może skontaktuj się z nami za pomocą jednej z następujących opcji:

* Opublikuj swoje pytania w naszym [forum API Management MSDN](https://social.msdn.microsoft.com/forums/azure/home?forum=azureapimgmt).
* Wyślij wiadomość e-mail zbyt<mailto:apimgmt@microsoft.com>.
* Wyślij żądanie funkcji w hello [forum opinii Azure](https://feedback.azure.com/forums/248703-api-management).

### <a name="what-does-it-mean-when-a-feature-is-in-preview"></a>Co to znaczy, gdy funkcja jest w wersji zapoznawczej?
Funkcja jest w wersji zapoznawczej, oznacza, że firma Microsoft jest aktywnie o opinie na jak działa funkcja hello dla Ciebie. Funkcja w wersji zapoznawczej jest funkcjonalnie ukończone, ale jest możliwe, że wybierzemy podziału, zmiany w odpowiedzi toocustomer opinii. Zaleca się, że nie są zależne od funkcji, która jest w wersji zapoznawczej w środowisku produkcyjnym. Jeśli masz opinię na funkcje w wersji zapoznawczej, prosimy o kontakt za pomocą jednego z hello opcje kontaktu w [jak I poproś zespołu Microsoft Azure API Management hello pytanie?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question).

### <a name="how-can-i-secure-hello-connection-between-hello-api-management-gateway-and-my-back-end-services"></a>Jak można zabezpieczyć hello połączenia między hello interfejsu API zarządzania bramą i Moje usług zaplecza
Istnieje kilka opcji toosecure hello połączenie między bramą usługi API Management hello i usługi zaplecza. Możesz:

* Użyj uwierzytelniania podstawowego HTTP. Aby uzyskać więcej informacji, zobacz [ustawień skonfiguruj interfejsu API](api-management-howto-create-apis.md#configure-api-settings).
* Używa wzajemnego uwierzytelniania SSL, zgodnie z opisem w [jak toosecure zaplecza usług przy użyciu wstępnego uwierzytelniania certyfikatu klienta w usłudze Azure API Management](api-management-howto-mutual-certificates.md).
* Użyj listę dozwolonych podobnej IP w usłudze zaplecza. Jeśli masz standardowa lub Premium wystąpienia interfejsu API zarządzania warstwy hello adres IP bramy hello pozostaje stała. Tooallow z listy dozwolonych adresów IP można ustawić ten adres IP. Możesz uzyskać adres IP hello wystąpienia interfejsu API zarządzania na powitania pulpitu nawigacyjnego w portalu Azure hello.
* Połącz z interfejsu API zarządzania wystąpienia tooan sieci wirtualnej platformy Azure.

### <a name="how-do-i-copy-my-api-management-service-instance-tooa-new-instance"></a>Jak skopiować Moje zarządzanie interfejsami API wystąpienie tooa nowe wystąpienie usługi?
Istnieje kilka opcji, jeśli chcesz, aby toocopy zarządzanie interfejsami API wystąpienie tooa nowe wystąpienie. Możesz:

* Użyj hello kopii zapasowej i przywracania funkcji w usłudze API Management. Aby uzyskać więcej informacji, zobacz [jak tooimplement odzyskiwania po awarii przy użyciu usługi Kopia zapasowa i przywracanie w usłudze Azure API Management](api-management-howto-disaster-recovery-backup-restore.md).
* Tworzenie własnych kopii zapasowej i przywracania funkcji przy użyciu hello [interfejsu API REST zarządzania interfejsu API](https://msdn.microsoft.com/library/azure/dn776326.aspx). Użyj hello toosave interfejsu API REST i przywrócić hello jednostek z hello wystąpienie usługi, które chcesz.
* Pobierz hello konfiguracji usługi przy użyciu narzędzia Git, a następnie przekaż tooa nowe wystąpienie. Aby uzyskać więcej informacji, zobacz [jak toosave i skonfigurować konfiguracji usługi Zarządzanie interfejsami API za pomocą narzędzia Git](api-management-configuration-repository-git.md).

### <a name="can-i-manage-my-api-management-instance-programmatically"></a>Może zarządzać Mój wystąpienie interfejsu API zarządzania programowo?
Tak, można zarządzać zarządzanie interfejsami API programowo przy użyciu:

* Witaj [interfejsu API REST zarządzania interfejsu API](https://msdn.microsoft.com/library/azure/dn776326.aspx).
* Witaj [SDK biblioteki zarządzania usługi Microsoft Azure ApiManagement](http://aka.ms/apimsdk).
* Witaj [wdrożenie usługi](https://msdn.microsoft.com/library/mt619282.aspx) i [Zarządzanie usługami](https://msdn.microsoft.com/library/mt613507.aspx) poleceń cmdlet programu PowerShell.

### <a name="how-do-i-add-a-user-toohello-administrators-group"></a>Jak dodać grupę Administratorzy toohello użytkowników?
Oto, jak można dodać do grupy Administratorzy toohello użytkowników:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Przejdź toohello grupę zasobów, która znajduje się wystąpienie interfejsu API zarządzania hello ma tooupdate.
3. Zarządzanie interfejsami API przypisywanie hello **interfejsu Api zarządzania współautora** użytkownika toohello roli.

Teraz hello nowo dodanych współautora za pomocą programu Azure PowerShell [poleceń cmdlet](https://msdn.microsoft.com/library/mt613507.aspx). Oto jak toosign w jako administrator:

1. Użyj hello `Login-AzureRmAccount` toosign polecenia cmdlet w.
2. Ustaw hello kontekstu toohello subskrypcji z usługi hello przy użyciu `Set-AzureRmContext -SubscriptionID <subscriptionGUID>`.
3. Pobierz pojedynczy adres URL logowania za pomocą `Get-AzureRmApiManagementSsoToken -ResourceGroupName <rgName> -Name <serviceName>`.
4. Użyj hello adresu URL tooaccess hello portalu administratora.

### <a name="why-is-hello-policy-that-i-want-tooadd-unavailable-in-hello-policy-editor"></a>Dlaczego jest zasad hello, że ma być tooadd niedostępne w edytorze zasad hello?
Jeśli zasady hello, które mają się tooadd nieaktywne lub cieniowania w edytorze zasad hello, można się, że jest w niewłaściwym zakresie hello hello zasad. Każda instrukcja zasad jest przeznaczona dla toouse w określonych zakresach i sekcje zasad. sekcje zasad hello tooreview i zakresy dla zasad, zobacz użycia zasad hello sekcji [zasad interfejsu API zarządzania](https://msdn.microsoft.com/library/azure/dn894080.aspx).

### <a name="how-do-i-use-api-versioning-in-api-management"></a>Jak używać wersji interfejsu API w usłudze API Management?
Masz kilka opcji toouse interfejsu API wersji w usłudze API Management:

* W usłudze API Management można skonfigurować różne wersje toorepresent interfejsów API. Na przykład może mieć dwóch różnych interfejsów API, MyAPIv1 i MyAPIv2. Wersja hello hello Deweloper chce toouse wybrać dewelopera.
* Możesz również skonfigurować interfejsu API z adresu URL usługi, który nie zawiera wersji segmentu, na przykład https://my.api. Następnie należy skonfigurować segment wersji na każdej operacji [ponowne zapisywanie adresów URL](https://msdn.microsoft.com/library/azure/dn894083.aspx#RewriteURL) szablonu. Na przykład masz operacji o [szablon adresu URL](api-management-howto-add-operations.md#url-template) o nazwie/Resource i [ponowne zapisywanie adresów URL](api-management-howto-add-operations.md#rewrite-url-template) o nazwie szablonu/v1/zasobów. Możesz zmienić wartość segmentu wersji hello osobno dla każdej operacji.
* Jeśli chcesz tookeep segment wersji "domyślne" w adresie URL usługi hello interfejsu API, wybranej operacji, ustawić zasady, które używa hello [Ustaw usługę zaplecza](https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBackendService) ścieżka żądania zaplecza hello toochange zasad.

### <a name="how-do-i-set-up-multiple-environments-in-a-single-api"></a>Jak skonfigurować wiele środowisk w jednego interfejsu API?
tooset się wielu środowiskach, na przykład środowiska testowego i środowiska produkcyjnego, w jednym interfejsie API, dostępne są dwie opcje. Możesz:

* Interfejsy API innego hosta, na hello tej samej dzierżawy.
* Host hello tych samych interfejsów API w różnym dzierżawcom.

### <a name="can-i-use-soap-with-api-management"></a>Czy można używać protokołu SOAP z interfejsu API zarządzania?
[Przekazywanie protokołu SOAP](http://blogs.msdn.microsoft.com/apimanagement/2016/10/13/soap-pass-through/) obsługi jest teraz dostępna. Administratorzy mogą importować hello WSDL usługi SOAP, a zarządzanie interfejsami API Azure utworzy frontonu protokołu SOAP. Dokumentację portalu dla deweloperów, konsoli testu, zasad i analiza będą dostępne dla usług SOAP.

### <a name="is-hello-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules"></a>To jest hello interfejsu API zarządzania bramy IP address stała? Można jej używać w regułach zapory?
Na powitania warstwy standardowa i Premium hello publicznego adresu IP (VIP) dzierżawcy interfejsu API zarządzania hello jest statyczna hello czas ich istnienia hello dzierżawy, z pewnymi wyjątkami. Witaj zmiany adresu IP w takiej sytuacji:

* Usługa Hello jest usunięty i ponownie utworzona.
* Subskrypcja usługi Hello jest [zawieszone](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) lub [ostrzeżona](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) (na przykład w przypadku nonpayment), a następnie przywrócone.
* Możesz dodać lub usunąć sieci wirtualnej platformy Azure (tylko na powitania deweloperów i warstwy Premium można użyć sieci wirtualnej).

W przypadku wdrożeń w przypadku zmiany adresu regionalnych hello Jeśli hello region jest vacated, a następnie przywrócone (możesz użyć w przypadku wdrożenia tylko w warstwie Premium hello).

Dzierżawcy warstwy Premium, skonfigurowane na potrzeby wdrażania w przypadku przypisano jeden publiczny adres IP dla regionu.

Na stronie powitania dzierżawy hello portalu Azure, możesz uzyskać adres IP (lub adresy we wdrożeniu w przypadku).

### <a name="can-i-configure-an-oauth-20-authorization-server-with-ad-fs-security"></a>Z zabezpieczeniami usług AD FS można skonfigurować serwera autoryzacji OAuth 2.0?
toolearn tooconfigure serwera autoryzacji OAuth 2.0 z zabezpieczeń usługi Active Directory Federation Services (AD FS), zobacz temat [za pomocą usług AD FS w usłudze API Management](https://phvbaars.wordpress.com/2016/02/06/using-adfs-in-api-management/).

### <a name="what-routing-method-does-api-management-use-in-deployments-toomultiple-geographic-locations"></a>Jakie metody routingu zarządzanie interfejsami API używa w lokalizacjach geograficznych toomultiple wdrożenia?
Zarządzanie interfejsami API używa hello [wydajności Metoda routingu ruchu](../traffic-manager/traffic-manager-routing-methods.md#priority) w lokalizacjach geograficznych toomultiple wdrożeń. Ruch przychodzący jest routingiem toohello najbliższego bramy interfejsu API. Jeśli jeden region przejdzie do trybu offline, ruch przychodzący jest automatycznie routingiem toohello dalej najbliższego bramy. Dowiedz się więcej na temat metody routingu w [metody routingu ruchu Menedżera](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="can-i-use-an-azure-resource-manager-template-toocreate-an-api-management-service-instance"></a>Można użyć toocreate szablonu usługi Azure Resource Manager wystąpienia usługi API Management?
Tak. Zobacz hello [usługi Azure API Management](http://aka.ms/apimtemplate) szablony szybkiego startu.

### <a name="can-i-use-a-self-signed-ssl-certificate-for-a-back-end"></a>Czy można użyć certyfikatu SSL z podpisem własnym dla wewnętrznej?
Tak. Oto, jak toouse podpisem Secure Sockets Layer (SSL) certyfikatu dla wewnętrznej:

1. Utwórz [zaplecza](https://msdn.microsoft.com/library/azure/dn935030.aspx) jednostek przy użyciu interfejsu API zarządzania.
2. Zestaw hello **skipCertificateChainValidation** właściwości zbyt**true**.
3. Jeśli nie ma już tooallow certyfikaty z podpisem własnym, Usuń hello jednostki wewnętrznej bazy danych lub ustaw hello **skipCertificateChainValidation** właściwości zbyt**false**.

### <a name="why-do-i-get-an-authentication-failure-when-i-try-tooclone-a-git-repository"></a>Dlaczego uzyskać wystąpił błąd uwierzytelniania podczas tooclone repozytorium Git?
Jeśli używasz Menedżera poświadczeń Git lub próbujesz tooclone repozytorium Git przy użyciu programu Visual Studio, może działać na znany problem z okna dialogowego hello poświadczeń systemu Windows. Hello — okno dialogowe ogranicza długość hasła too127 znaków, a jego obcina hasło wygenerowane Microsoft hello. Pracujemy nad skrócenie hello hasła. Na razie użyj tooclone Git Bash repozytorium Git.

### <a name="does-api-management-work-with-azure-expressroute"></a>Zarządzanie interfejsami API działa z Azure ExpressRoute?
Tak. Zarządzanie interfejsami API działa usługa Azure ExpressRoute.

### <a name="why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them"></a>Dlaczego, po wdrożeniu usługi API Management do nich, jest wymagamy dedykowanych podsieci w stylu Menedżera zasobów sieci wirtualnych?
konieczność dedykowanych podsieci Hello interfejsu API zarządzania pochodzi z hello fakt, jest zbudowany na (Warstwa 1 PAAS) klasycznego modelu wdrożenia. Możemy wdrożyć w sieci Wirtualnej Menedżera zasobów (Warstwa 2), są toothat skutków. Witaj klasycznego modelu wdrożenia na platformie Azure nie są ściśle powiązane ze hello modelu Resource Manager i dlatego w przypadku utworzenia zasobu w warstwie V2, warstwy V1 hello nie wiesz i problemów może się zdarzyć, takich jak zarządzanie interfejsami API w trakcie toouse adresu IP, który został już przydzielony tooa karty Sieciowej (oparta na V2).
więcej informacji na temat różnica modeli Classic i Menedżera zasobów Azure można znaleźć zbyt toolearn[różnica w modelach wdrażania](../azure-resource-manager/resource-manager-deployment-model.md).

### <a name="what-is-hello-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet"></a>Co to jest rozmiar minimalny podsieci hello potrzebne podczas wdrażania interfejsu API zarządzania w sieci Wirtualnej?
wymagany rozmiar minimalny podsieci Hello toodeploy jest zarządzanie interfejsami API [/29](../virtual-network/virtual-networks-faq.md#configuration), który jest rozmiar minimalny podsieci hello Azure obsługuje.

### <a name="can-i-move-an-api-management-service-from-one-subscription-tooanother"></a>Z jednej tooanother subskrypcji można przenieść usługi API Management?
Tak. toolearn, zobacz temat [przenoszenia zasobów tooa nową grupę zasobów lub subskrypcji](../azure-resource-manager/resource-group-move-resources.md).

### <a name="are-there-restrictions-on-or-known-issues-with-importing-my-api"></a>Czy istnieją ograniczenia dotyczące lub znane problemy z importowaniem Moje interfejsu API?
[Znane problemy i ograniczenia](api-management-api-import-restrictions.md) dla Otwórz API(Swagger) WSDL i WADL formaty.
