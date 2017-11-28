---
title: aaaAzure przekazywania WCF hybrydowych w lokalnej/w chmurze aplikacji (.NET) | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate .NET na lokalnej/w chmurze hybrydowej aplikacji przy użyciu przekaźnika usługi WCF Azure."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="dbc01-103">Tworzenie hybrydowej aplikacji lokalnej/w chmurze platformy .NET przy użyciu przekaźnika WCF platformy Azure</span><span class="sxs-lookup"><span data-stu-id="dbc01-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="dbc01-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="dbc01-104">Introduction</span></span>

<span data-ttu-id="dbc01-105">W tym artykule opisano, jak toobuild hybrydowego chmury aplikacji Microsoft Azure i programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dbc01-105">This article shows how toobuild a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="dbc01-106">Hello samouczka przyjęto założenie, że nie masz wcześniejszego doświadczenia korzysta z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dbc01-106">hello tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="dbc01-107">W mniej niż 30 minut będą miały aplikacji, która korzysta z wielu zasobów platformy Azure i w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="dbc01-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in hello cloud.</span></span>

<span data-ttu-id="dbc01-108">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="dbc01-108">You will learn:</span></span>

* <span data-ttu-id="dbc01-109">Jak toocreate lub dostosowanie istniejącej usługi sieci web do użytku przez rozwiązanie sieci web.</span><span class="sxs-lookup"><span data-stu-id="dbc01-109">How toocreate or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="dbc01-110">Jak toouse hello Azure WCF przekaźnika usługi tooshare danych między aplikacją platformy Azure i usługi sieci web hostowaną w innym miejscu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-110">How toouse hello Azure WCF Relay service tooshare data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="dbc01-111">Jak usługa Azure Relay pomaga w tworzeniu rozwiązań hybrydowych</span><span class="sxs-lookup"><span data-stu-id="dbc01-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="dbc01-112">Rozwiązania biznesowe zwykle składają się z kombinacji niestandardowego kodu napisanego tootackle nowy i wymagań biznesowych oraz istniejących funkcjonalności dostarczonych przez rozwiązania i systemy, które zostały już wdrożone.</span><span class="sxs-lookup"><span data-stu-id="dbc01-112">Business solutions are typically composed of a combination of custom code written tootackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="dbc01-113">Architekci rozwiązań zaczynają toouse hello chmury w celu łatwiejszej obsługi wymagań skali i obniżenia kosztów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="dbc01-113">Solution architects are starting toouse hello cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="dbc01-114">W ten sposób znajduje się istniejące elementy zawartości usług chciałby tooleverage jako bloków konstrukcyjnych dla swoich rozwiązań zaporą firmową hello i poza łatwo osiągnąć przez rozwiązanie chmury hello dostępu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-114">In doing so, they find that existing service assets they'd like tooleverage as building blocks for their solutions are inside hello corporate firewall and out of easy reach for access by hello cloud solution.</span></span> <span data-ttu-id="dbc01-115">Wiele wewnętrznych usług nie są wbudowane lub hostowanych w taki sposób, że ich łatwe uwidocznienie na krawędzi sieci firmowej hello.</span><span class="sxs-lookup"><span data-stu-id="dbc01-115">Many internal services are not built or hosted in a way that they can be easily exposed at hello corporate network edge.</span></span>

<span data-ttu-id="dbc01-116">[Azure przekazywania](https://azure.microsoft.com/services/service-bus/) zaprojektowano pod kątem hello przypadek użycia podjęcia istniejących usług sieci web Windows Communication Foundation (WCF) i mogą być usług bezpiecznie dostępne toosolutions, który znajduje się poza firmą hello bez konieczności Infrastruktura sieci firmowej toohello niepożądanych zmian.</span><span class="sxs-lookup"><span data-stu-id="dbc01-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for hello use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible toosolutions that reside outside hello corporate perimeter without requiring intrusive changes toohello corporate network infrastructure.</span></span> <span data-ttu-id="dbc01-117">Takie usługi przekaźnika wciąż są hostowane wewnątrz istniejącego środowiska, ale delegują one nasłuchiwanie przychodzących sesji i żądań toohello hostowanych w chmurze usługi przekazywania danych.</span><span class="sxs-lookup"><span data-stu-id="dbc01-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests toohello cloud-hosted relay service.</span></span> <span data-ttu-id="dbc01-118">Usługa Azure Relay chroni także te usługi przed nieautoryzowanym dostępem przy użyciu uwierzytelniania za pomocą [sygnatury dostępu współdzielonego](../service-bus-messaging/service-bus-sas.md) (SAS, Shared Access Signature).</span><span class="sxs-lookup"><span data-stu-id="dbc01-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="dbc01-119">Scenariusz rozwiązania</span><span class="sxs-lookup"><span data-stu-id="dbc01-119">Solution scenario</span></span>
<span data-ttu-id="dbc01-120">W tym samouczku utworzysz witrynę sieci Web programu ASP.NET, umożliwiającą toosee listy produktów na stronie spisu produktów hello.</span><span class="sxs-lookup"><span data-stu-id="dbc01-120">In this tutorial, you will create an ASP.NET website that enables you toosee a list of products on hello product inventory page.</span></span>

![][0]

<span data-ttu-id="dbc01-121">Samouczek Hello założono, że zawierają informacje o produkcie systemu lokalnego i używa tooreach przekazywania Azure do tego systemu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-121">hello tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay tooreach into that system.</span></span> <span data-ttu-id="dbc01-122">Jest to symulowane przez usługę sieci Web, która działa w prostej aplikacji konsolowej i jest uzupełniana przez zestaw produktów w pamięci.</span><span class="sxs-lookup"><span data-stu-id="dbc01-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="dbc01-123">Będzie można stanie toorun tę aplikację konsolową na własnym komputerze i wdrożyć rolę sieci web hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="dbc01-123">You will be able toorun this console application on your own computer and deploy hello web role into Azure.</span></span> <span data-ttu-id="dbc01-124">W ten sposób przekonasz się jak rola sieci web hello działająca w hello centrum danych Azure rzeczywiście wywoła komputera, mimo że prawie na pewno będą znajdować się za co najmniej jedną zaporą i warstwę translatora adresów sieciowych adres komputera.</span><span class="sxs-lookup"><span data-stu-id="dbc01-124">By doing so, you will see how hello web role running in hello Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="dbc01-125">Konfigurowanie środowiska deweloperskiego hello</span><span class="sxs-lookup"><span data-stu-id="dbc01-125">Set up hello development environment</span></span>

<span data-ttu-id="dbc01-126">Przed rozpoczęciem tworzenia aplikacji platformy Azure Pobierz narzędzia hello i konfigurowanie środowiska programowania:</span><span class="sxs-lookup"><span data-stu-id="dbc01-126">Before you can begin developing Azure applications, download hello tools and set up your development environment:</span></span>

1. <span data-ttu-id="dbc01-127">Zainstaluj hello Azure SDK dla platformy .NET z hello SDK [pliki do pobrania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="dbc01-127">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="dbc01-128">W hello **.NET** kolumny, kliknij wersję hello [programu Visual Studio](http://www.visualstudio.com) używasz.</span><span class="sxs-lookup"><span data-stu-id="dbc01-128">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="dbc01-129">Witaj czynnościach w ramach tego samouczka użyj programu Visual Studio 2015, ale współpracują oni również z programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="dbc01-129">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="dbc01-130">Gdy monit toorun lub zapisać hello Instalatora, kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-130">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="dbc01-131">W hello **Instalatora platformy sieci Web**, kliknij przycisk **zainstalować** i kontynuować hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="dbc01-131">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="dbc01-132">Po zakończeniu instalacji hello będzie mieć wszystko niezbędne toostart toodevelop hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dbc01-132">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="dbc01-133">Hello SDK zawiera narzędzia, które pozwalają w łatwy sposób tworzyć aplikacje platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dbc01-133">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="dbc01-134">Tworzenie przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="dbc01-134">Create a namespace</span></span>

<span data-ttu-id="dbc01-135">przy użyciu toobegin hello funkcji przekazywania na platformie Azure, musisz najpierw utworzyć przestrzeń nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="dbc01-135">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="dbc01-136">Przestrzeń nazw zapewnia kontener określania zakresu na potrzeby adresowania zasobów platformy Azure w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dbc01-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="dbc01-137">Wykonaj hello [instrukcje w tym miejscu](relay-create-namespace-portal.md) toocreate przekazywania przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="dbc01-137">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="dbc01-138">Tworzenie serwera lokalnego</span><span class="sxs-lookup"><span data-stu-id="dbc01-138">Create an on-premises server</span></span>

<span data-ttu-id="dbc01-139">Najpierw utworzysz lokalny (pozorny) system katalogu produktów.</span><span class="sxs-lookup"><span data-stu-id="dbc01-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="dbc01-140">Będzie on dość proste; Możesz można traktować jako rzeczywisty lokalny system katalogu produktów z kompletną powierzchnią usług próbujemy toointegrate.</span><span class="sxs-lookup"><span data-stu-id="dbc01-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying toointegrate.</span></span>

<span data-ttu-id="dbc01-141">Ten projekt jest aplikacją konsoli programu Visual Studio i używa hello [pakietu NuGet usługi Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello bibliotek usługi Service Bus i ustawień konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="dbc01-141">This project is a Visual Studio console application, and uses hello [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello Service Bus libraries and configuration settings.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="dbc01-142">Utwórz projekt hello</span><span class="sxs-lookup"><span data-stu-id="dbc01-142">Create hello project</span></span>

1. <span data-ttu-id="dbc01-143">Korzystając z uprawnień administratora, uruchom program Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dbc01-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="dbc01-144">tak, kliknij prawym przyciskiem myszy ikonę programu Visual Studio hello toodo, a następnie kliknij przycisk **Uruchom jako administrator**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-144">toodo so, right-click hello Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="dbc01-145">W programie Visual Studio na powitania **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-145">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="dbc01-146">W sekcji **Zainstalowane szablony** obszaru **Visual C#** kliknij pozycję **Aplikacja konsolowa (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="dbc01-147">W hello **nazwa** okno, nazwa typu hello **ProductsServer**:</span><span class="sxs-lookup"><span data-stu-id="dbc01-147">In hello **Name** box, type hello name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="dbc01-148">Kliknij przycisk **OK** toocreate hello **ProductsServer** projektu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-148">Click **OK** toocreate hello **ProductsServer** project.</span></span>
5. <span data-ttu-id="dbc01-149">Jeśli użytkownik zainstalował już hello Menedżera pakietów NuGet dla programu Visual Studio, Pomiń toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="dbc01-149">If you have already installed hello NuGet package manager for Visual Studio, skip toohello next step.</span></span> <span data-ttu-id="dbc01-150">W przeciwnym razie odwiedź stronę menedżera pakietów [NuGet][NuGet] i kliknij przycisk [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) (Zainstaluj menedżer pakietów NuGet).</span><span class="sxs-lookup"><span data-stu-id="dbc01-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="dbc01-151">Wykonaj tooinstall monity hello hello Menedżera pakietów NuGet, a następnie ponownie uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dbc01-151">Follow hello prompts tooinstall hello NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="dbc01-152">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ProductsServer** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-152">In Solution Explorer, right-click hello **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="dbc01-153">Kliknij przycisk hello **Przeglądaj** , a następnie wyszukaj `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="dbc01-153">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="dbc01-154">Wybierz hello **WindowsAzure.ServiceBus** pakietu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-154">Select hello **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="dbc01-155">Kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="dbc01-155">Click **Install**, and accept hello terms of use.</span></span>

   ![][13]

   <span data-ttu-id="dbc01-156">Należy zauważyć, że ten hello wymagane zestawy klientów są teraz przywoływane.</span><span class="sxs-lookup"><span data-stu-id="dbc01-156">Note that hello required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="dbc01-157">Dodaj nową klasę dla kontraktu produktu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-157">Add a new class for your product contract.</span></span> <span data-ttu-id="dbc01-158">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ProductsServer** projekt i kliknij przycisk **Dodaj**, a następnie kliknij przycisk **klasy**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-158">In Solution Explorer, right-click hello **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="dbc01-159">W hello **nazwa** okno, nazwa typu hello **ProductsContract.cs**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-159">In hello **Name** box, type hello name **ProductsContract.cs**.</span></span> <span data-ttu-id="dbc01-160">Następnie kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-160">Then click **Add**.</span></span>
10. <span data-ttu-id="dbc01-161">W **ProductsContract.cs**, Zastąp definicję przestrzeni nazw hello hello następującego kodu, który definiuje kontrakt hello hello usługi.</span><span class="sxs-lookup"><span data-stu-id="dbc01-161">In **ProductsContract.cs**, replace hello namespace definition with hello following code, which defines hello contract for hello service.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. <span data-ttu-id="dbc01-162">W pliku Program.cs Zastąp definicję przestrzeni nazw hello hello następującego kodu, który dodaje hello profilu usługi i hello hosta.</span><span class="sxs-lookup"><span data-stu-id="dbc01-162">In Program.cs, replace hello namespace definition with hello following code, which adds hello profile service and hello host for it.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. <span data-ttu-id="dbc01-163">W Eksploratorze rozwiązań kliknij dwukrotnie hello **App.config** pliku tooopen go w edytorze programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="dbc01-163">In Solution Explorer, double-click hello **App.config** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="dbc01-164">U dołu hello hello `<system.ServiceModel>` elementu (ale nadal w ramach `<system.ServiceModel>`), Dodaj hello następującego kodu XML.</span><span class="sxs-lookup"><span data-stu-id="dbc01-164">At hello bottom of hello `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add hello following XML code.</span></span> <span data-ttu-id="dbc01-165">Należy się tooreplace *yourServiceNamespace* o nazwie hello przestrzeni nazw, i *yourKey* kluczem sygnatury dostępu Współdzielonego hello został wcześniej pobrany z portalu hello:</span><span class="sxs-lookup"><span data-stu-id="dbc01-165">Be sure tooreplace *yourServiceNamespace* with hello name of your namespace, and *yourKey* with hello SAS key you retrieved earlier from hello portal:</span></span>

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. <span data-ttu-id="dbc01-166">Nadal w pliku App.config w hello `<appSettings>` elementu, Zastąp wartości parametrów połączenia hello przy użyciu parametrów połączenia hello uzyskanym wcześniej z portalu hello.</span><span class="sxs-lookup"><span data-stu-id="dbc01-166">Still in App.config, in hello `<appSettings>` element, replace hello connection string value with hello connection string you previously obtained from hello portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="dbc01-167">Naciśnij klawisz **Ctrl + Shift + B** lub hello **kompilacji** menu, kliknij przycisk **Kompiluj rozwiązanie** toobuild hello aplikacji i sprawdź hello dokładność pracy wykonanej do tej pory.</span><span class="sxs-lookup"><span data-stu-id="dbc01-167">Press **Ctrl+Shift+B** or from hello **Build** menu, click **Build Solution** toobuild hello application and verify hello accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="dbc01-168">Tworzenie aplikacji ASP.NET</span><span class="sxs-lookup"><span data-stu-id="dbc01-168">Create an ASP.NET application</span></span>

<span data-ttu-id="dbc01-169">W tej sekcji utworzysz prostą aplikację ASP.NET, która będzie wyświetlać dane pobrane z usługi produktów.</span><span class="sxs-lookup"><span data-stu-id="dbc01-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="dbc01-170">Utwórz projekt hello</span><span class="sxs-lookup"><span data-stu-id="dbc01-170">Create hello project</span></span>

1. <span data-ttu-id="dbc01-171">Upewnij się, że program Visual Studio jest uruchomiony z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="dbc01-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="dbc01-172">W programie Visual Studio na powitania **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-172">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="dbc01-173">W sekcji **Zainstalowane szablony** w obszarze **Visual C#** kliknij pozycję **Aplikacja sieci Web programu ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="dbc01-174">Nazwa projektu hello **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-174">Name hello project **ProductsPortal**.</span></span> <span data-ttu-id="dbc01-175">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="dbc01-176">Z hello **szablony ASP.NET** liście hello **nowej aplikacji sieci Web ASP.NET** okna dialogowego, kliknij przycisk **MVC**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-176">From hello **ASP.NET Templates** list in hello **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="dbc01-177">Kliknij przycisk hello **Zmień uwierzytelnianie** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dbc01-177">Click hello **Change Authentication** button.</span></span> <span data-ttu-id="dbc01-178">W hello **Zmień uwierzytelnianie** okna dialogowego Sprawdź, czy **bez uwierzytelniania** jest zaznaczone, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-178">In hello **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="dbc01-179">W tym samouczku wdrożysz aplikację, która nie wymaga logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dbc01-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="dbc01-180">Po powrocie do hello **nowej aplikacji sieci Web ASP.NET** okna dialogowego, kliknij przycisk **OK** toocreate hello MVC aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dbc01-180">Back in hello **New ASP.NET Web Application** dialog, click **OK** toocreate hello MVC app.</span></span>
8. <span data-ttu-id="dbc01-181">Teraz musisz skonfigurować zasoby platformy Azure dla nowej aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="dbc01-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="dbc01-182">Wykonaj kroki hello hello [publikowania tooAzure sekcji tego artykułu](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="dbc01-182">Follow hello steps in hello [Publish tooAzure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="dbc01-183">Następnie wróć toothis samouczka i przejdź toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="dbc01-183">Then, return toothis tutorial and proceed toohello next step.</span></span>
10. <span data-ttu-id="dbc01-184">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy pozycję **Modele** i kliknij polecenie **Dodaj**, a następnie kliknij pozycję **Klasa**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="dbc01-185">W hello **nazwa** okno, nazwa typu hello **Product.cs**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-185">In hello **Name** box, type hello name **Product.cs**.</span></span> <span data-ttu-id="dbc01-186">Następnie kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-hello-web-application"></a><span data-ttu-id="dbc01-187">Modyfikowanie aplikacji sieci web hello</span><span class="sxs-lookup"><span data-stu-id="dbc01-187">Modify hello web application</span></span>

1. <span data-ttu-id="dbc01-188">W pliku Product.cs hello w programie Visual Studio Zastąp istniejącą definicję przestrzeni nazw hello hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-188">In hello Product.cs file in Visual Studio, replace hello existing namespace definition with hello following code.</span></span>

   ```csharp
    // Declare properties for hello products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. <span data-ttu-id="dbc01-189">W Eksploratorze rozwiązań rozwiń hello **kontrolerów** folder, a następnie kliknij dwukrotnie hello **HomeController.cs** pliku tooopen go w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dbc01-189">In Solution Explorer, expand hello **Controllers** folder, then double-click hello **HomeController.cs** file tooopen it in Visual Studio.</span></span>
3. <span data-ttu-id="dbc01-190">W **HomeController.cs**, Zastąp istniejącą definicję przestrzeni nazw hello hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-190">In **HomeController.cs**, replace hello existing namespace definition with hello following code.</span></span>

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. <span data-ttu-id="dbc01-191">W Eksploratorze rozwiązań rozwiń hello Views\Shared folder, a następnie kliknij dwukrotnie **_Layout.cshtml** tooopen go w edytorze programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="dbc01-191">In Solution Explorer, expand hello Views\Shared folder, then double-click **_Layout.cshtml** tooopen it in hello Visual Studio editor.</span></span>
5. <span data-ttu-id="dbc01-192">Zmień wszystkie wystąpienia **Moja aplikacja platformy ASP.NET** za**LITWARE's Products**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-192">Change all occurrences of **My ASP.NET Application** too**LITWARE's Products**.</span></span>
6. <span data-ttu-id="dbc01-193">Usuń hello **Home**, **o**, i **skontaktuj się z** łącza.</span><span class="sxs-lookup"><span data-stu-id="dbc01-193">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="dbc01-194">Poniższy przykład hello usunięcie hello wyróżniony kod.</span><span class="sxs-lookup"><span data-stu-id="dbc01-194">In hello following example, delete hello highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="dbc01-195">W Eksploratorze rozwiązań rozwiń hello Views\Home folder, a następnie kliknij dwukrotnie **Index.cshtml** tooopen go w edytorze programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="dbc01-195">In Solution Explorer, expand hello Views\Home folder, then double-click **Index.cshtml** tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="dbc01-196">Zastąp całą zawartość pliku hello hello hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-196">Replace hello entire contents of hello file with hello following code.</span></span>

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. <span data-ttu-id="dbc01-197">tooverify hello dokładność pracy wykonanej do tej pory, naciśnij klawisz **Ctrl + Shift + B** toobuild hello projektu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-197">tooverify hello accuracy of your work so far, you can press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="run-hello-app-locally"></a><span data-ttu-id="dbc01-198">Uruchamianie aplikacji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="dbc01-198">Run hello app locally</span></span>

<span data-ttu-id="dbc01-199">Uruchom tooverify aplikacji hello, który działa.</span><span class="sxs-lookup"><span data-stu-id="dbc01-199">Run hello application tooverify that it works.</span></span>

1. <span data-ttu-id="dbc01-200">Upewnij się, że **ProductsPortal** jest hello aktywnego projektu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-200">Ensure that **ProductsPortal** is hello active project.</span></span> <span data-ttu-id="dbc01-201">Kliknij prawym przyciskiem myszy nazwę projektu hello w Eksploratorze rozwiązań i wybierz **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-201">Right-click hello project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="dbc01-202">W programie Visual Studio naciśnij klawisz **F5**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="dbc01-203">Aplikacja powinna uruchomić się w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="dbc01-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-hello-pieces-together"></a><span data-ttu-id="dbc01-204">Składanie fragmentów hello</span><span class="sxs-lookup"><span data-stu-id="dbc01-204">Put hello pieces together</span></span>

<span data-ttu-id="dbc01-205">Witaj następnym krokiem jest toohook się hello na lokalnego serwera produktów z hello aplikacji ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="dbc01-205">hello next step is toohook up hello on-premises products server with hello ASP.NET application.</span></span>

1. <span data-ttu-id="dbc01-206">Jeśli jeszcze nie jest otwarty w programie Visual Studio ponownie otwórz hello **ProductsPortal** projekt utworzony w hello [tworzenie aplikacji ASP.NET](#create-an-aspnet-application) sekcji.</span><span class="sxs-lookup"><span data-stu-id="dbc01-206">If it is not already open, in Visual Studio re-open hello **ProductsPortal** project you created in hello [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="dbc01-207">Podobne krok toohello w sekcji "Tworzenie serwera lokalnego" hello, Dodaj hello NuGet toohello projekt będzie odwoływał się pakiet.</span><span class="sxs-lookup"><span data-stu-id="dbc01-207">Similar toohello step in hello "Create an On-Premises Server" section, add hello NuGet package toohello project references.</span></span> <span data-ttu-id="dbc01-208">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ProductsPortal** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-208">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="dbc01-209">Wyszukaj "Service Bus" i wybierz hello **WindowsAzure.ServiceBus** elementu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-209">Search for "Service Bus" and select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="dbc01-210">Następnie ukończyć powitalnych instalację i zamknąć to okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="dbc01-210">Then complete hello installation and close this dialog box.</span></span>
4. <span data-ttu-id="dbc01-211">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ProductsPortal** projektu, a następnie kliknij przycisk **Dodaj**, następnie **istniejący element**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-211">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="dbc01-212">Przejdź toohello **ProductsContract.cs** pliku z hello **ProductsServer** projekt konsoli.</span><span class="sxs-lookup"><span data-stu-id="dbc01-212">Navigate toohello **ProductsContract.cs** file from hello **ProductsServer** console project.</span></span> <span data-ttu-id="dbc01-213">Kliknij przycisk toohighlight ProductsContract.cs.</span><span class="sxs-lookup"><span data-stu-id="dbc01-213">Click toohighlight ProductsContract.cs.</span></span> <span data-ttu-id="dbc01-214">Kliknij przycisk hello Strzałka w dół obok zbyt**Dodaj**, następnie kliknij przycisk **Dodaj jako Link**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-214">Click hello down arrow next too**Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="dbc01-215">Teraz Otwórz hello **HomeController.cs** w edytorze programu Visual Studio hello i Zastąp definicję przestrzeni nazw hello hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-215">Now open hello **HomeController.cs** file in hello Visual Studio editor and replace hello namespace definition with hello following code.</span></span> <span data-ttu-id="dbc01-216">Należy się tooreplace *yourServiceNamespace* hello nazwą swojej przestrzeni nazw usługi i *yourKey* kluczem sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="dbc01-216">Be sure tooreplace *yourServiceNamespace* with hello name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="dbc01-217">Spowoduje to włączenie powitania klienta toocall hello Usługa lokalna, zwracając wynik hello hello wywołania.</span><span class="sxs-lookup"><span data-stu-id="dbc01-217">This will enable hello client toocall hello on-premises service, returning hello result of hello call.</span></span>

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare hello channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. <span data-ttu-id="dbc01-218">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ProductsPortal** rozwiązań (Upewnij się, że tooright kliknięciem hello rozwiązanie, nie hello projektu).</span><span class="sxs-lookup"><span data-stu-id="dbc01-218">In Solution Explorer, right-click hello **ProductsPortal** solution (make sure tooright-click hello solution, not hello project).</span></span> <span data-ttu-id="dbc01-219">Kliknij pozycję **Dodaj**, a następnie kliknij pozycję **Istniejący projekt**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="dbc01-220">Przejdź toohello **ProductsServer** projektu, a następnie kliknij dwukrotnie hello **ProductsServer.csproj** tooadd pliku rozwiązania go.</span><span class="sxs-lookup"><span data-stu-id="dbc01-220">Navigate toohello **ProductsServer** project, then double-click hello **ProductsServer.csproj** solution file tooadd it.</span></span>
9. <span data-ttu-id="dbc01-221">**ProductsServer** musi być uruchomiona w kolejności toodisplay hello danych na **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-221">**ProductsServer** must be running in order toodisplay hello data on **ProductsPortal**.</span></span> <span data-ttu-id="dbc01-222">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ProductsPortal** rozwiązanie i kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-222">In Solution Explorer, right-click hello **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="dbc01-223">Witaj **strony właściwości** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="dbc01-223">hello **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="dbc01-224">Na powitania po lewej stronie, kliknij przycisk **projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-224">On hello left side, click **Startup Project**.</span></span> <span data-ttu-id="dbc01-225">Na powitania po prawej stronie, kliknij przycisk **wiele projektów startowych**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-225">On hello right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="dbc01-226">Upewnij się, że **ProductsServer** i **ProductsPortal** są wymienione w tej kolejności z **Start** Ustaw jako hello akcji dla obu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as hello action for both.</span></span>

      ![][25]

11. <span data-ttu-id="dbc01-227">Nadal w hello **właściwości** okno dialogowe, kliknij przycisk **zależności projektu** na powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="dbc01-227">Still in hello **Properties** dialog box, click **Project Dependencies** on hello left side.</span></span>
12. <span data-ttu-id="dbc01-228">W hello **projekty** kliknij **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-228">In hello **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="dbc01-229">Upewnij się, że projekt **ProductsPortal** nie jest wybrany.</span><span class="sxs-lookup"><span data-stu-id="dbc01-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="dbc01-230">W hello **projekty** kliknij **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-230">In hello **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="dbc01-231">Upewnij się, że projekt **ProductsServer** jest wybrany.</span><span class="sxs-lookup"><span data-stu-id="dbc01-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="dbc01-232">Kliknij przycisk **OK** w hello **strony właściwości** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="dbc01-232">Click **OK** in hello **Property Pages** dialog box.</span></span>

## <a name="run-hello-project-locally"></a><span data-ttu-id="dbc01-233">Uruchom projekt hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="dbc01-233">Run hello project locally</span></span>

<span data-ttu-id="dbc01-234">tootest hello aplikację lokalnie, w programie Visual Studio naciśnij klawisz **F5**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-234">tootest hello application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="dbc01-235">serwer lokalny Hello (**ProductsServer**) powinien uruchomić się jako pierwszy, a następnie hello **ProductsPortal** aplikacja powinna uruchomić się w oknie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="dbc01-235">hello on-premises server (**ProductsServer**) should start first, then hello **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="dbc01-236">Teraz, pojawi się spis produktów hello list dane pobrane z hello produktu usługi lokalnego systemu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-236">This time, you will see that hello product inventory lists data retrieved from hello product service on-premises system.</span></span>

![][10]

<span data-ttu-id="dbc01-237">Naciśnij klawisz **Odśwież** na powitania **ProductsPortal** strony.</span><span class="sxs-lookup"><span data-stu-id="dbc01-237">Press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="dbc01-238">Każdym odświeżeniu strony hello, zobaczysz hello aplikacja serwera wyświetli komunikat po `GetProducts()` z **ProductsServer** jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="dbc01-238">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="dbc01-239">Zamknąć obie aplikacje przed kontynuowaniem toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="dbc01-239">Close both applications before proceeding toohello next step.</span></span>

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a><span data-ttu-id="dbc01-240">Wdrażanie hello ProductsPortal projektu tooan aplikacji sieci web Azure</span><span class="sxs-lookup"><span data-stu-id="dbc01-240">Deploy hello ProductsPortal project tooan Azure web app</span></span>

<span data-ttu-id="dbc01-241">Witaj, następnym krokiem jest aplikacja sieci Web Azure hello toorepublish **ProductsPortal** frontonu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-241">hello next step is toorepublish hello Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="dbc01-242">Witaj, po:</span><span class="sxs-lookup"><span data-stu-id="dbc01-242">Do hello following:</span></span>

1. <span data-ttu-id="dbc01-243">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ProductsPortal** projektu, a następnie kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-243">In Solution Explorer, right-click hello **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="dbc01-244">Następnie kliknij przycisk **publikowania** na powitania **publikowania** strony.</span><span class="sxs-lookup"><span data-stu-id="dbc01-244">Then, click **Publish** on hello **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="dbc01-245">Zobaczysz komunikat o błędzie w oknie przeglądarki powitania po hello **ProductsPortal** projektu sieci web zostanie automatycznie uruchomiony po wdrożeniu hello.</span><span class="sxs-lookup"><span data-stu-id="dbc01-245">You may see an error message in hello browser window when hello **ProductsPortal** web project is automatically launched after hello deployment.</span></span> <span data-ttu-id="dbc01-246">To jest oczekiwany i występuje, ponieważ hello **ProductsServer** aplikacji nie jest jeszcze uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="dbc01-246">This is expected, and occurs because hello **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="dbc01-247">Adres URL hello kopiowania hello wdrożonych aplikacji sieci web, ponieważ będzie potrzebny URL hello w następnym kroku hello.</span><span class="sxs-lookup"><span data-stu-id="dbc01-247">Copy hello URL of hello deployed web app, as you will need hello URL in hello next step.</span></span> <span data-ttu-id="dbc01-248">W oknie działanie usługi Azure App Service hello w programie Visual Studio, mogą również uzyskać ten adres URL:</span><span class="sxs-lookup"><span data-stu-id="dbc01-248">You can also obtain this URL from hello Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="dbc01-249">Zamknij hello przeglądarki okna toostop hello uruchomiona aplikacja.</span><span class="sxs-lookup"><span data-stu-id="dbc01-249">Close hello browser window toostop hello running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="dbc01-250">Ustawianie projektu ProductsPortal jako aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="dbc01-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="dbc01-251">Przed działającej aplikacji hello w chmurze hello, upewnij się, że **ProductsPortal** jest uruchamiana z poziomu programu Visual Studio jako aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="dbc01-251">Before running hello application in hello cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="dbc01-252">W programie Visual Studio, kliknij prawym przyciskiem myszy hello **ProductsPortal** projektu, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-252">In Visual Studio, right-click hello **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="dbc01-253">W lewej kolumnie powitania kliknij **Web**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-253">In hello left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="dbc01-254">W hello **Akcja uruchamiania** kliknij hello **początkowy adres URL** przycisk, a w polu tekstowym hello wprowadź adres URL hello z wcześniej wdrożonej aplikacji sieci web; na przykład `http://productsportal1234567890.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="dbc01-254">In hello **Start Action** section, click hello **Start URL** button, and in hello text box enter hello URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="dbc01-255">Z hello **pliku** menu programu Visual Studio kliknij **Zapisz wszystko**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-255">From hello **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="dbc01-256">W menu kompilacji hello w programie Visual Studio, kliknij **Kompiluj ponownie rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="dbc01-256">From hello Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="dbc01-257">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="dbc01-257">Run hello application</span></span>

1. <span data-ttu-id="dbc01-258">Naciśnij klawisz F5 toobuild i uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="dbc01-258">Press F5 toobuild and run hello application.</span></span> <span data-ttu-id="dbc01-259">Hello lokalnego serwera (hello **ProductsServer** aplikacji konsoli) powinien uruchomić się jako pierwszy, a następnie hello **ProductsPortal** aplikacji powinna uruchomić się w oknie przeglądarki, jak pokazano w po ekranie powitania Zrzut.</span><span class="sxs-lookup"><span data-stu-id="dbc01-259">hello on-premises server (hello **ProductsServer** console application) should start first, then hello **ProductsPortal** application should start in a browser window, as shown in hello following screen shot.</span></span> <span data-ttu-id="dbc01-260">Zwróć uwagę ponownie ten spis produktów hello wyświetla dane pobrane z hello produktu usługi lokalnego systemu, a dane zostaną wyświetlone w aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="dbc01-260">Notice again that hello product inventory lists data retrieved from hello product service on-premises system, and displays that data in hello web app.</span></span> <span data-ttu-id="dbc01-261">Sprawdź, czy toomake adres URL hello który **ProductsPortal** działa w chmurze hello jako aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dbc01-261">Check hello URL toomake sure that **ProductsPortal** is running in hello cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="dbc01-262">Witaj **ProductsServer** aplikacji konsoli musi być uruchomiony i może tooserve hello danych toohello **ProductsPortal** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dbc01-262">hello **ProductsServer** console application must be running and able tooserve hello data toohello **ProductsPortal** application.</span></span> <span data-ttu-id="dbc01-263">Jeśli przeglądarka hello jest wyświetlany błąd, zaczekaj kilka sekund dla **ProductsServer** tooload i hello wyświetlania następującego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="dbc01-263">If hello browser displays an error, wait a few more seconds for **ProductsServer** tooload and display hello following message.</span></span> <span data-ttu-id="dbc01-264">Następnie naciśnij klawisz **Odśwież** w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="dbc01-264">Then press **Refresh** in hello browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="dbc01-265">Wstecz w przeglądarce hello, naciśnij klawisz **Odśwież** na powitania **ProductsPortal** strony.</span><span class="sxs-lookup"><span data-stu-id="dbc01-265">Back in hello browser, press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="dbc01-266">Każdym odświeżeniu strony hello, zobaczysz hello aplikacja serwera wyświetli komunikat po `GetProducts()` z **ProductsServer** jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="dbc01-266">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="dbc01-267">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dbc01-267">Next steps</span></span>

<span data-ttu-id="dbc01-268">toolearn więcej informacji na temat przekaźnika usługi Azure, zobacz hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="dbc01-268">toolearn more about Azure Relay, see hello following resources:</span></span>  

* [<span data-ttu-id="dbc01-269">Co to jest usługa Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="dbc01-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="dbc01-270">Sposób przekazywania toouse</span><span class="sxs-lookup"><span data-stu-id="dbc01-270">How toouse Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png
