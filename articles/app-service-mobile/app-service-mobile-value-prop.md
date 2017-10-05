---
title: "Informacje o funkcji Mobile Apps w usłudze Azure App Service"
description: "Dowiedz się, jakie korzyści z usługi App Service można osiągać podczas pracy z aplikacjami mobilnymi w przedsiębiorstwie."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: 4e96cb9d-a632-4cf6-8219-0810d8ade3f9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: ac35ff9fe1c5f315c4de08de951f505627ec412b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <span data-ttu-id="f3083-103"><a name="getting-started"> </a>Informacje o funkcji Mobile Apps w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f3083-103"><a name="getting-started"> </a>About Mobile Apps in Azure App Service</span></span>
<span data-ttu-id="f3083-104">Usługa Azure App Service to oferta w pełni zarządzanej [platformy jako usługi](https://azure.microsoft.com/overview/what-is-paas/) (PaaS) dla profesjonalnych deweloperów.</span><span class="sxs-lookup"><span data-stu-id="f3083-104">Azure App Service is a fully managed [platform as a service](https://azure.microsoft.com/overview/what-is-paas/) (PaaS) offering for professional developers.</span></span> <span data-ttu-id="f3083-105">Usługa ta oferuje bogaty zestaw funkcji na potrzeby scenariuszy internetowych, mobilnych i dotyczących integracji.</span><span class="sxs-lookup"><span data-stu-id="f3083-105">The service brings a rich set of capabilities to web, mobile, and integration scenarios.</span></span> 

<span data-ttu-id="f3083-106">Funkcja Mobile Apps usługi Azure App Service oferuje deweloperom w przedsiębiorstwach oraz integratorom systemów platformę służącą do tworzenia aplikacji mobilnych, która jest wysoko skalowalna i dostępna globalnie.</span><span class="sxs-lookup"><span data-stu-id="f3083-106">The Mobile Apps feature of Azure App Service gives enterprise developers and system integrators a mobile-application development platform that's highly scalable and globally available.</span></span>

![Wizualne omówienie funkcji Mobile Apps](./media/app-service-mobile-value-prop/overview.png)

## <a name="why-mobile-apps"></a><span data-ttu-id="f3083-108">Dlaczego warto korzystać z usługi Mobile Apps?</span><span class="sxs-lookup"><span data-stu-id="f3083-108">Why Mobile Apps?</span></span>
<span data-ttu-id="f3083-109">Przy użyciu funkcji Mobile Apps można:</span><span class="sxs-lookup"><span data-stu-id="f3083-109">With the Mobile Apps feature, you can:</span></span>

* <span data-ttu-id="f3083-110">**Kompilować aplikacje natywne i międzyplatformowe** — bez względu na to, czy kompilujesz natywne aplikacje dla systemów iOS, Android i Windows, czy też międzyplatformowe aplikacje platform Xamarin lub Cordova (PhoneGap), możesz korzystać z usługi App Service za pośrednictwem natywnych zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="f3083-110">**Build native and cross-platform apps**: Whether you're building native iOS, Android, and Windows apps or cross-platform Xamarin or Cordova (PhoneGap) apps, you can take advantage of App Service by using native SDKs.</span></span>
* <span data-ttu-id="f3083-111">**Nawiązywać połączenia z systemami przedsiębiorstwa** — dzięki funkcji Mobile Apps można w ciągu kilku minut dodać opcję logowania firmowego oraz nawiązywać połączenia z zasobami przedsiębiorstwa lokalnie lub w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f3083-111">**Connect to your enterprise systems**: With the Mobile Apps feature, you can add corporate sign-in in minutes, and connect to your enterprise on-premises or cloud resources.</span></span>
* <span data-ttu-id="f3083-112">**Kompilować aplikacje gotowe do działania w trybie offline z opcją synchronizacji danych** — aby personel mobilny mógł pracować wydajniej, należy skompilować aplikacje działające w trybie offline, a następnie po nawiązaniu łączności za pomocą usługi Mobile Apps synchronizować w tle dane z dowolnych źródeł danych przedsiębiorstwa lub interfejsów API oprogramowania jako usługi (SaaS).</span><span class="sxs-lookup"><span data-stu-id="f3083-112">**Build offline-ready apps with data sync**: Make your mobile workforce more productive by building apps that work offline, and use Mobile Apps to sync data in the background when connectivity is present with any of your enterprise data sources or software as a service (SaaS) APIs.</span></span>
* <span data-ttu-id="f3083-113">**Wypychać powiadomienia do milionów użytkowników w ciągu sekund** — można kontaktować się z klientami dzięki błyskawicznym powiadomieniom wypychanym z dowolnego urządzenia, spersonalizowanym zgodnie z ich potrzebami i wysyłanym w odpowiednim czasie.</span><span class="sxs-lookup"><span data-stu-id="f3083-113">**Push notifications to millions in seconds**: Engage your customers with instant push notifications on any device, personalized to their needs and sent when the time is right.</span></span>

## <a name="mobile-apps-features"></a><span data-ttu-id="f3083-114">Funkcje Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="f3083-114">Mobile Apps features</span></span>
<span data-ttu-id="f3083-115">Następujące funkcje są ważnymi elementami tworzenia aplikacji mobilnych z obsługą chmury:</span><span class="sxs-lookup"><span data-stu-id="f3083-115">The following features are important to cloud-enabled mobile development:</span></span>

* <span data-ttu-id="f3083-116">**Uwierzytelnianie i autoryzacja** — wybieraj z coraz dłuższej listy dostawców tożsamości, obejmującej usługę Azure Active Directory na potrzeby uwierzytelniania w przedsiębiorstwie, a także dostawców sieci społecznościowych, takich jak Facebook, Google, Twitter i konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f3083-116">**Authentication and authorization**: Select from an ever-growing list of identity providers, including Azure Active Directory for enterprise authentication, plus social providers such as Facebook, Google, Twitter, and Microsoft accounts.</span></span> <span data-ttu-id="f3083-117">Funkcja Mobile Apps udostępnia usługę OAuth 2.0 dla każdego dostawcy.</span><span class="sxs-lookup"><span data-stu-id="f3083-117">Mobile Apps offers an OAuth 2.0 service for each provider.</span></span> <span data-ttu-id="f3083-118">Można również zintegrować zestaw SDK dla dostawcy tożsamości, aby korzystać z funkcji specyficznych dla tego dostawcy.</span><span class="sxs-lookup"><span data-stu-id="f3083-118">You can also integrate the SDK for the identity provider for provider-specific functionality.</span></span>

    <span data-ttu-id="f3083-119">Dowiedz się więcej na temat naszych [authentication features].</span><span class="sxs-lookup"><span data-stu-id="f3083-119">Discover more about our [authentication features].</span></span>

* <span data-ttu-id="f3083-120">**Dostęp do danych**: funkcja Mobile Apps oferuje współpracujące z urządzeniami przenośnymi źródło danych OData v3 połączone z usługą Azure SQL Database lub lokalnym serwerem SQL.</span><span class="sxs-lookup"><span data-stu-id="f3083-120">**Data access**: Mobile Apps provides a mobile-friendly OData v3 data source that's linked to Azure SQL Database or an on-premises SQL server.</span></span> <span data-ttu-id="f3083-121">Ponieważ ta usługa może opierać się na platformie Entity Framework, możesz łatwo zintegrować ją z innymi dostawcami danych NoSQL i SQL, w tym [Azure Table Storage], MongoDB i [Azure Cosmos DB], a także dostawcami interfejsów API SaaS, takimi jak Office 365 i Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="f3083-121">Because this service can be based on Entity Framework, you can easily integrate with other NoSQL and SQL data providers, including [Azure Table storage], MongoDB, [Azure Cosmos DB], and SaaS API providers such as Office 365 and Salesforce.com.</span></span>

* <span data-ttu-id="f3083-122">**Synchronizacja w trybie offline**: nasze zestawy SDK klientów ułatwiają tworzenie niezawodnych i dynamicznych aplikacji mobilnych, które korzystają z zestawu danych w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="f3083-122">**Offline sync**: Our client SDKs make it easy to build robust and responsive mobile applications that operate with an offline dataset.</span></span> <span data-ttu-id="f3083-123">Ten zestaw danych można automatycznie zsynchronizować z danymi zaplecza, uwzględniając obsługę rozwiązywania konfliktów.</span><span class="sxs-lookup"><span data-stu-id="f3083-123">You can sync this dataset automatically with the back-end data, including conflict-resolution support.</span></span>

  <span data-ttu-id="f3083-124">Dowiedz się więcej na temat naszych [funkcje związane z danymi].</span><span class="sxs-lookup"><span data-stu-id="f3083-124">Discover more about our [data features].</span></span>

* <span data-ttu-id="f3083-125">**Powiadomienia wypychane**: nasze zestawy SDK klientów są bezproblemowo integrowane z możliwościami rejestracji w usłudze Azure Notification Hubs, co umożliwia wysyłanie powiadomień wypychanych do milionów użytkowników jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="f3083-125">**Push notifications**: Our client SDKs integrate seamlessly with the registration capabilities of Azure Notification Hubs, so you can send push notifications to millions of users simultaneously.</span></span>

  <span data-ttu-id="f3083-126">Dowiedz się więcej na temat naszych [funkcje powiadomień wypychanych].</span><span class="sxs-lookup"><span data-stu-id="f3083-126">Discover more about our [push notification features].</span></span>

* <span data-ttu-id="f3083-127">**Zestawy SDK klientów**: oferujemy kompletny pakiet zestawów SDK klientów, które obsługują tworzenie aplikacji natywnych ([iOS], [Android] i [Windows]), międzyplatformowych ([Xamarin.iOS i Xamarin.Android], [Xamarin.Forms]) i hybrydowych ([Apache Cordova]).</span><span class="sxs-lookup"><span data-stu-id="f3083-127">**Client SDKs**: We provide a complete set of client SDKs that cover native development ([iOS], [Android], and [Windows]), cross-platform development ([Xamarin.iOS and Xamarin.Android], [Xamarin.Forms]), and hybrid application development ([Apache Cordova]).</span></span> <span data-ttu-id="f3083-128">Każdy zestaw SDK klienta jest dostępny z licencją MIT i jest rozwiązaniem typu open source.</span><span class="sxs-lookup"><span data-stu-id="f3083-128">Each client SDK is available with an MIT license and is open source.</span></span>

## <a name="azure-app-service-features"></a><span data-ttu-id="f3083-129">Funkcje usługi Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f3083-129">Azure App Service features</span></span>
<span data-ttu-id="f3083-130">Poniższe funkcje platformy są przydatne w przypadku witryn produkcyjnych aplikacji mobilnych:</span><span class="sxs-lookup"><span data-stu-id="f3083-130">The following platform features are useful for mobile production sites:</span></span>

* <span data-ttu-id="f3083-131">**Skalowanie automatyczne**: usługa App Service pozwala szybko skalować w górę lub w poziomie, a co za tym idzie — obsługiwać dowolne przychodzące obciążenia klientów.</span><span class="sxs-lookup"><span data-stu-id="f3083-131">**Autoscaling**: With App Service, you can quickly scale up or scale out to handle any incoming customer load.</span></span> <span data-ttu-id="f3083-132">Ręcznie wybierz liczbę i rozmiar maszyn wirtualnych lub skonfiguruj skalowanie automatyczne, aby skalować zaplecze aplikacji mobilnej w oparciu o obciążenie lub harmonogram.</span><span class="sxs-lookup"><span data-stu-id="f3083-132">Manually select the number and size of VMs, or set up autoscaling to scale your mobile-app back end based on load or schedule.</span></span>

  <span data-ttu-id="f3083-133">Dowiedz się więcej na temat [skalowania automatycznego].</span><span class="sxs-lookup"><span data-stu-id="f3083-133">Discover more about [autoscaling].</span></span>

* <span data-ttu-id="f3083-134">**Środowiska przejściowe**: usługa App Service może uruchamiać wiele wersji witryny, co umożliwia testowanie A/B, testowanie w środowisku produkcyjnym jako część większego planu metodyki DevOps oraz miejscowe wdrażanie przejściowe nowego zaplecza.</span><span class="sxs-lookup"><span data-stu-id="f3083-134">**Staging environments**: App Service can run multiple versions of your site, so you can perform A/B testing, test in production as part of a larger DevOps plan, and do in-place staging of a new back end.</span></span>

  <span data-ttu-id="f3083-135">Dowiedz się więcej na temat [środowiska przejściowe].</span><span class="sxs-lookup"><span data-stu-id="f3083-135">Discover more about [staging environments].</span></span>

* <span data-ttu-id="f3083-136">**Ciągłe wdrażanie**: usługę App Service można zintegrować z typowymi systemami zarządzania łańcuchem zaopatrzenia SCM, umożliwiając w ten sposób automatyczne wdrażanie nowej wersji zaplecza przez wypchnięcie do gałęzi systemu SCM.</span><span class="sxs-lookup"><span data-stu-id="f3083-136">**Continuous deployment**: App Service can integrate with common supply chain management (SCM) systems, so you can automatically deploy a new version of your back end by pushing to a branch of your SCM system.</span></span>

  <span data-ttu-id="f3083-137">Dowiedz się więcej na temat [opcje wdrożenia].</span><span class="sxs-lookup"><span data-stu-id="f3083-137">Discover more about [deployment options].</span></span>

* <span data-ttu-id="f3083-138">**Praca w sieci wirtualnej**: usługa App Service może nawiązywać połączenia z zasobami lokalnymi przy użyciu sieci wirtualnej, usługi Azure ExpressRoute lub połączeń hybrydowych.</span><span class="sxs-lookup"><span data-stu-id="f3083-138">**Virtual networking**: App Service can connect to on-premises resources by using virtual network, Azure ExpressRoute, or hybrid connections.</span></span>

  <span data-ttu-id="f3083-139">Dowiedz się więcej na temat [połączenia hybrydowe], [sieci wirtualnych] i [ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="f3083-139">Discover more about [hybrid connections], [virtual networks], and [ExpressRoute].</span></span>

* <span data-ttu-id="f3083-140">**Środowiska izolowane i dedykowane**: usługę App Service można uruchamiać w dedykowanym, w pełni izolowanym środowisku, aby bezpiecznie pracować z aplikacjami usługi Azure App Service na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="f3083-140">**Isolated and dedicated environments**: You can run App Service in a fully isolated and dedicated environment for securely running Azure App Service apps at high scale.</span></span> <span data-ttu-id="f3083-141">To środowisko jest idealne w przypadku obciążeń aplikacji wymagających dużej skali, izolacji lub bezpiecznego dostępu do sieci.</span><span class="sxs-lookup"><span data-stu-id="f3083-141">This environment is ideal for application workloads that require high scale, isolation, or secure network access.</span></span>

  <span data-ttu-id="f3083-142">Dowiedz się więcej na temat [środowisk usługi App Service].</span><span class="sxs-lookup"><span data-stu-id="f3083-142">Discover more about [App Service environments].</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3083-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f3083-143">Next steps</span></span>

<span data-ttu-id="f3083-144">Aby rozpocząć pracę z funkcją Mobile Apps w usłudze Azure App Service, wykonaj kroki samouczka z [wprowadzeniem].</span><span class="sxs-lookup"><span data-stu-id="f3083-144">To get started with Mobile Apps in Azure App Service, complete the [getting started] tutorial.</span></span> <span data-ttu-id="f3083-145">Samouczek zawiera podstawowe informacje na temat tworzenia wybranego klienta i zaplecza mobilnego.</span><span class="sxs-lookup"><span data-stu-id="f3083-145">The tutorial covers the basics of producing a mobile back end and client of your choice.</span></span> <span data-ttu-id="f3083-146">Obejmuje on również zagadnienia, takie jak integrowanie uwierzytelniania, synchronizacji w trybie offline i powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="f3083-146">It also covers integrating authentication, offline sync, and push notifications.</span></span> <span data-ttu-id="f3083-147">Kroki samouczka można wykonać wielokrotnie, jeden raz dla każdej aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="f3083-147">You can complete the tutorial multiple times, once for each client application.</span></span>

<span data-ttu-id="f3083-148">Aby uzyskać więcej informacji o funkcji Mobile Apps, zapoznaj się z naszą [mapą nauki].</span><span class="sxs-lookup"><span data-stu-id="f3083-148">For more information about Mobile Apps, review our [learning map].</span></span>
<span data-ttu-id="f3083-149">Aby uzyskać więcej informacji o platformie Azure App Service, zobacz temat [Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="f3083-149">For more information about the Azure App Service platform, see [Azure App Service].</span></span>

<!-- URLs. -->
[Migrate your mobile service to App Service]: app-service-mobile-migrating-from-mobile-services.md
[Azure App Service]: ../app-service/app-service-value-prop-what-is.md
[wprowadzeniem]: app-service-mobile-ios-get-started.md
[Azure Table Storage]:../cosmos-db/table-storage-how-to-use-dotnet.md
[Azure Cosmos DB]: ../cosmos-db/documentdb-get-started.md
[authentication features]: ./app-service-mobile-auth.md
[funkcje związane z danymi]: ./app-service-mobile-offline-data-sync.md
[funkcje powiadomień wypychanych]: ../notification-hubs/notification-hubs-push-notification-overview.md
[iOS]: ./app-service-mobile-ios-how-to-use-client-library.md
[Android]: ./app-service-mobile-android-how-to-use-client-library.md
[Windows]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.iOS i Xamarin.Android]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.Forms]: ./app-service-mobile-xamarin-forms-get-started.md
[Apache Cordova]: ./app-service-mobile-cordova-how-to-use-client-library.md
[skalowania automatycznego]: ../app-service-web/web-sites-scale.md
[środowiska przejściowe]: ../app-service-web/web-sites-staged-publishing.md
[opcje wdrożenia]: ../app-service-web/web-sites-deploy.md
[połączenia hybrydowe]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[sieci wirtualnych]: ../app-service-web/web-sites-integrate-with-vnet.md
[ExpressRoute]: ../app-service-web/app-service-app-service-environment-network-configuration-expressroute.md
[środowisk usługi App Service]: ../app-service-web/app-service-app-service-environment-intro.md
[mapą nauki]: https://azure.microsoft.com/en-us/documentation/learning-paths/appservice-mobileapps/
