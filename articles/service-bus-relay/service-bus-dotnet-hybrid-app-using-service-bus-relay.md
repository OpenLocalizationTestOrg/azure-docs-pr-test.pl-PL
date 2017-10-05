---
title: "Hybrydowa aplikacja lokalna/w chmurze usługi Azure WCF Relay (platforma .NET) | Microsoft Docs"
description: "Dowiedz się, jak utworzyć hybrydową aplikację lokalną/w chmurze platformy .NET przy użyciu przekaźnika WCF platformy Azure."
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
ms.openlocfilehash: 366922a083b9d18ef50e04eb8b459d2725315e1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="114cd-103">Tworzenie hybrydowej aplikacji lokalnej/w chmurze platformy .NET przy użyciu przekaźnika WCF platformy Azure</span><span class="sxs-lookup"><span data-stu-id="114cd-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="114cd-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="114cd-104">Introduction</span></span>

<span data-ttu-id="114cd-105">Ten artykuł przedstawia sposób tworzenia hybrydowej aplikacji w chmurze przy użyciu platformy Microsoft Azure i programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="114cd-105">This article shows how to build a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="114cd-106">W tym samouczku założono, że nie masz wcześniejszego doświadczenia w używaniu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="114cd-106">The tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="114cd-107">W mniej niż 30 minut utworzysz aplikację korzystającą z wielu zasobów platformy Azure i działającą w chmurze.</span><span class="sxs-lookup"><span data-stu-id="114cd-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in the cloud.</span></span>

<span data-ttu-id="114cd-108">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="114cd-108">You will learn:</span></span>

* <span data-ttu-id="114cd-109">Jak utworzyć lub przystosować istniejącą usługę sieci Web do użytku przez rozwiązanie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="114cd-109">How to create or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="114cd-110">Jak za pomocą usługi Azure WCF Relay udostępniać dane między aplikacją platformy Azure a usługą sieci Web hostowaną w innym miejscu.</span><span class="sxs-lookup"><span data-stu-id="114cd-110">How to use the Azure WCF Relay service to share data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="114cd-111">Jak usługa Azure Relay pomaga w tworzeniu rozwiązań hybrydowych</span><span class="sxs-lookup"><span data-stu-id="114cd-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="114cd-112">Rozwiązania biznesowe zwykle składają się z kombinacji niestandardowego kodu napisanego w celu spełnienia nowych i unikatowych wymagań biznesowych oraz istniejących funkcjonalności dostarczonych przez już stosowane rozwiązania i systemy.</span><span class="sxs-lookup"><span data-stu-id="114cd-112">Business solutions are typically composed of a combination of custom code written to tackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="114cd-113">Architekci rozwiązań zaczynają stosować usługi w chmurze w celu łatwiejszej obsługi wymagań skali i obniżenia kosztów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="114cd-113">Solution architects are starting to use the cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="114cd-114">W ten sposób dowiadują się, że istniejące elementy zawartości usług, których chcieliby użyć jako bloków konstrukcyjnych dla swoich rozwiązań, znajdują się za firmową zaporą i są trudno dostępne dla rozwiązania w chmurze.</span><span class="sxs-lookup"><span data-stu-id="114cd-114">In doing so, they find that existing service assets they'd like to leverage as building blocks for their solutions are inside the corporate firewall and out of easy reach for access by the cloud solution.</span></span> <span data-ttu-id="114cd-115">Wiele wewnętrznych usług nie jest zbudowanych lub hostowanych w sposób umożliwiający ich łatwe uwidocznienie na krawędzi sieci firmowej.</span><span class="sxs-lookup"><span data-stu-id="114cd-115">Many internal services are not built or hosted in a way that they can be easily exposed at the corporate network edge.</span></span>

<span data-ttu-id="114cd-116">Usługa [Azure Relay](https://azure.microsoft.com/services/service-bus/) została zaprojektowana w celu bezpiecznego zapewniania dostępu do istniejących usług sieci Web Windows Communication Foundation (WCF) rozwiązaniom, które znajdują się poza firmą, bez konieczności wprowadzania istotnych zmian w infrastrukturze sieci firmowej.</span><span class="sxs-lookup"><span data-stu-id="114cd-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for the use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible to solutions that reside outside the corporate perimeter without requiring intrusive changes to the corporate network infrastructure.</span></span> <span data-ttu-id="114cd-117">Takie usługi przekazywania wciąż są hostowane wewnątrz istniejącego środowiska, ale delegują one nasłuchiwanie sesji i żądań przychodzących do usługi przekazywania hostowanej w chmurze.</span><span class="sxs-lookup"><span data-stu-id="114cd-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests to the cloud-hosted relay service.</span></span> <span data-ttu-id="114cd-118">Usługa Azure Relay chroni także te usługi przed nieautoryzowanym dostępem przy użyciu uwierzytelniania za pomocą [sygnatury dostępu współdzielonego](../service-bus-messaging/service-bus-sas.md) (SAS, Shared Access Signature).</span><span class="sxs-lookup"><span data-stu-id="114cd-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="114cd-119">Scenariusz rozwiązania</span><span class="sxs-lookup"><span data-stu-id="114cd-119">Solution scenario</span></span>
<span data-ttu-id="114cd-120">W tym samouczku utworzysz witrynę sieci Web ASP.NET, która umożliwi wyświetlanie listy produktów na stronie spisu produktów.</span><span class="sxs-lookup"><span data-stu-id="114cd-120">In this tutorial, you will create an ASP.NET website that enables you to see a list of products on the product inventory page.</span></span>

![][0]

<span data-ttu-id="114cd-121">W samouczku założono, że informacje o produktach znajdują się w istniejącym systemie lokalnym i uzyskujesz dostęp do tego systemu za pomocą usługi Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="114cd-121">The tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay to reach into that system.</span></span> <span data-ttu-id="114cd-122">Jest to symulowane przez usługę sieci Web, która działa w prostej aplikacji konsolowej i jest uzupełniana przez zestaw produktów w pamięci.</span><span class="sxs-lookup"><span data-stu-id="114cd-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="114cd-123">Będziesz w stanie uruchomić tę aplikację konsolową na własnym komputerze i wdrożyć rolę sieci Web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="114cd-123">You will be able to run this console application on your own computer and deploy the web role into Azure.</span></span> <span data-ttu-id="114cd-124">W ten sposób przekonasz się, że rola sieci Web działająca w centrum danych Azure rzeczywiście wywoła Twój komputer, mimo że prawie na pewno znajduje się on za przynajmniej jedną zaporą i warstwą translatora adresów sieciowych (NAT, network address translation).</span><span class="sxs-lookup"><span data-stu-id="114cd-124">By doing so, you will see how the web role running in the Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="114cd-125">Konfigurowanie środowiska deweloperskiego</span><span class="sxs-lookup"><span data-stu-id="114cd-125">Set up the development environment</span></span>

<span data-ttu-id="114cd-126">Przed rozpoczęciem tworzenia aplikacji dla platformy Azure pobierz potrzebne narzędzia i skonfiguruj swoje środowisko deweloperskie:</span><span class="sxs-lookup"><span data-stu-id="114cd-126">Before you can begin developing Azure applications, download the tools and set up your development environment:</span></span>

1. <span data-ttu-id="114cd-127">Zainstaluj zestaw Azure SDK dla platformy .NET ze [strony pobierania](https://azure.microsoft.com/downloads/) zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="114cd-127">Install the Azure SDK for .NET from the SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="114cd-128">W kolumnie **.NET** kliknij używaną wersję programu [Visual Studio](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="114cd-128">In the **.NET** column, click the version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="114cd-129">Czynności opisane w tym samouczku są wykonywane w programie Visual Studio 2015, ale można w ich przypadku korzystać z programu Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="114cd-129">The steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="114cd-130">Gdy zostanie wyświetlony monit o uruchomienie lub zapisanie instalatora, kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="114cd-130">When prompted to run or save the installer, click **Run**.</span></span>
4. <span data-ttu-id="114cd-131">W **Instalatorze platformy sieci Web** kliknij przycisk **Zainstaluj** i kontynuuj instalację.</span><span class="sxs-lookup"><span data-stu-id="114cd-131">In the **Web Platform Installer**, click **Install** and proceed with the installation.</span></span>
5. <span data-ttu-id="114cd-132">Po zakończeniu instalacji będziesz mieć do dyspozycji wszystkie narzędzia niezbędne do tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="114cd-132">Once the installation is complete, you will have everything necessary to start to develop the app.</span></span> <span data-ttu-id="114cd-133">Zestaw SDK zawiera narzędzia, które pozwalają w łatwy sposób tworzyć aplikacje dla platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="114cd-133">The SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="114cd-134">Tworzenie przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="114cd-134">Create a namespace</span></span>

<span data-ttu-id="114cd-135">Aby rozpocząć korzystanie z funkcji przekazywania na platformie Azure, należy najpierw utworzyć przestrzeń nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="114cd-135">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="114cd-136">Przestrzeń nazw zapewnia kontener określania zakresu na potrzeby adresowania zasobów platformy Azure w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="114cd-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="114cd-137">Postępuj zgodnie z [instrukcjami podanymi w tym miejscu](relay-create-namespace-portal.md), aby utworzyć przestrzeń nazw przekazywania.</span><span class="sxs-lookup"><span data-stu-id="114cd-137">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="114cd-138">Tworzenie serwera lokalnego</span><span class="sxs-lookup"><span data-stu-id="114cd-138">Create an on-premises server</span></span>

<span data-ttu-id="114cd-139">Najpierw utworzysz lokalny (pozorny) system katalogu produktów.</span><span class="sxs-lookup"><span data-stu-id="114cd-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="114cd-140">Będzie to dość proste. Możesz go traktować jako rzeczywisty lokalny system katalogu produktów z kompletną powierzchnią usług, którą próbujemy zintegrować.</span><span class="sxs-lookup"><span data-stu-id="114cd-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying to integrate.</span></span>

<span data-ttu-id="114cd-141">Ten projekt jest aplikacją konsolową programu Visual Studio i używa [pakietu NuGet usługi Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) w celu uwzględnienia bibliotek i ustawień konfiguracji usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="114cd-141">This project is a Visual Studio console application, and uses the [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) to include the Service Bus libraries and configuration settings.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="114cd-142">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="114cd-142">Create the project</span></span>

1. <span data-ttu-id="114cd-143">Korzystając z uprawnień administratora, uruchom program Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="114cd-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="114cd-144">W tym celu kliknij prawym przyciskiem myszy ikonę programu Visual Studio, a następnie kliknij pozycję **Uruchom jako administrator**.</span><span class="sxs-lookup"><span data-stu-id="114cd-144">To do so, right-click the Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="114cd-145">W menu **Plik** programu Visual Studio kliknij pozycję **Nowy**, a następnie kliknij pozycję **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="114cd-145">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="114cd-146">W sekcji **Zainstalowane szablony** obszaru **Visual C#** kliknij pozycję **Aplikacja konsolowa (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="114cd-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="114cd-147">W polu **Nazwa** wpisz nazwę **ProductsServer**:</span><span class="sxs-lookup"><span data-stu-id="114cd-147">In the **Name** box, type the name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="114cd-148">Kliknij przycisk **OK**, aby utworzyć projekt **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="114cd-148">Click **OK** to create the **ProductsServer** project.</span></span>
5. <span data-ttu-id="114cd-149">Jeśli masz już zainstalowany menedżer pakietów NuGet dla programu Visual Studio, przejdź do następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="114cd-149">If you have already installed the NuGet package manager for Visual Studio, skip to the next step.</span></span> <span data-ttu-id="114cd-150">W przeciwnym razie odwiedź stronę menedżera pakietów [NuGet][NuGet] i kliknij przycisk [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) (Zainstaluj menedżer pakietów NuGet).</span><span class="sxs-lookup"><span data-stu-id="114cd-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="114cd-151">Postępuj zgodnie z monitami, aby zainstalować menedżera pakietów NuGet, a następnie ponownie uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="114cd-151">Follow the prompts to install the NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="114cd-152">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt **ProductsServer**, a następnie kliknij polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="114cd-152">In Solution Explorer, right-click the **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="114cd-153">Kliknij kartę **Przeglądanie**, a następnie wyszukaj ciąg `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="114cd-153">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="114cd-154">Wybierz pakiet **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="114cd-154">Select the **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="114cd-155">Kliknij pozycję **Zainstaluj** i zaakceptuj warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="114cd-155">Click **Install**, and accept the terms of use.</span></span>

   ![][13]

   <span data-ttu-id="114cd-156">Zwróć uwagę na to, że wymagane zestawy klientów są teraz przywoływane.</span><span class="sxs-lookup"><span data-stu-id="114cd-156">Note that the required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="114cd-157">Dodaj nową klasę dla kontraktu produktu.</span><span class="sxs-lookup"><span data-stu-id="114cd-157">Add a new class for your product contract.</span></span> <span data-ttu-id="114cd-158">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt **ProductsServer** i kliknij polecenie **Dodaj**, a następnie kliknij pozycję **Klasa**.</span><span class="sxs-lookup"><span data-stu-id="114cd-158">In Solution Explorer, right-click the **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="114cd-159">W polu **Nazwa** wpisz nazwę **ProductsContract.cs**.</span><span class="sxs-lookup"><span data-stu-id="114cd-159">In the **Name** box, type the name **ProductsContract.cs**.</span></span> <span data-ttu-id="114cd-160">Następnie kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="114cd-160">Then click **Add**.</span></span>
10. <span data-ttu-id="114cd-161">W pliku **ProductsContract.cs** zastąp definicję przestrzeni nazw następującym kodem, który definiuje kontrakt dla usługi.</span><span class="sxs-lookup"><span data-stu-id="114cd-161">In **ProductsContract.cs**, replace the namespace definition with the following code, which defines the contract for the service.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define the data contract for the service
        [DataContract]
        // Declare the serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define the service contract.
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
11. <span data-ttu-id="114cd-162">W pliku Program.cs zastąp definicję przestrzeni nazw następującym kodem, który dodaje usługę profilu i jej hosta.</span><span class="sxs-lookup"><span data-stu-id="114cd-162">In Program.cs, replace the namespace definition with the following code, which adds the profile service and the host for it.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement the IProducts interface.
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

            // Display a message in the service console application
            // when the list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define the Main() function in the service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER to close");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. <span data-ttu-id="114cd-163">W Eksploratorze rozwiązań kliknij dwukrotnie plik **App.config**, aby otworzyć go w edytorze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="114cd-163">In Solution Explorer, double-click the **App.config** file to open it in the Visual Studio editor.</span></span> <span data-ttu-id="114cd-164">W dolnej części elementu `<system.ServiceModel>` (ale nadal w elemencie `<system.ServiceModel>`) dodaj poniższy kod XML.</span><span class="sxs-lookup"><span data-stu-id="114cd-164">At the bottom of the `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add the following XML code.</span></span> <span data-ttu-id="114cd-165">Koniecznie zastąp ciąg *yourServiceNamespace* nazwą Twojej przestrzeni nazw, a ciąg *yourKey* kluczem SAS, który został wcześniej pobrany z portalu:</span><span class="sxs-lookup"><span data-stu-id="114cd-165">Be sure to replace *yourServiceNamespace* with the name of your namespace, and *yourKey* with the SAS key you retrieved earlier from the portal:</span></span>

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
13. <span data-ttu-id="114cd-166">W pliku App.config w elemencie `<appSettings>` zastąp wartość parametrów połączenia parametrami połączenia, które zostały wcześniej uzyskane z portalu.</span><span class="sxs-lookup"><span data-stu-id="114cd-166">Still in App.config, in the `<appSettings>` element, replace the connection string value with the connection string you previously obtained from the portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="114cd-167">Naciśnij kombinację klawiszy **Ctrl+Shift+B** lub w menu **Kompilacja** kliknij pozycję **Kompiluj rozwiązanie**, aby skompilować aplikację i sprawdzić dokładność pracy wykonanej do tej pory.</span><span class="sxs-lookup"><span data-stu-id="114cd-167">Press **Ctrl+Shift+B** or from the **Build** menu, click **Build Solution** to build the application and verify the accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="114cd-168">Tworzenie aplikacji ASP.NET</span><span class="sxs-lookup"><span data-stu-id="114cd-168">Create an ASP.NET application</span></span>

<span data-ttu-id="114cd-169">W tej sekcji utworzysz prostą aplikację ASP.NET, która będzie wyświetlać dane pobrane z usługi produktów.</span><span class="sxs-lookup"><span data-stu-id="114cd-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="114cd-170">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="114cd-170">Create the project</span></span>

1. <span data-ttu-id="114cd-171">Upewnij się, że program Visual Studio jest uruchomiony z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="114cd-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="114cd-172">W menu **Plik** programu Visual Studio kliknij pozycję **Nowy**, a następnie kliknij pozycję **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="114cd-172">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="114cd-173">W sekcji **Zainstalowane szablony** w obszarze **Visual C#** kliknij pozycję **Aplikacja sieci Web programu ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="114cd-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="114cd-174">Nazwij projekt **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="114cd-174">Name the project **ProductsPortal**.</span></span> <span data-ttu-id="114cd-175">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="114cd-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="114cd-176">Na liście **Szablony ASP.NET** w oknie dialogowym **Nowa aplikacja sieci Web programu ASP.NET** kliknij pozycję **MVC**.</span><span class="sxs-lookup"><span data-stu-id="114cd-176">From the **ASP.NET Templates** list in the **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="114cd-177">Kliknij przycisk **Zmień uwierzytelnianie**.</span><span class="sxs-lookup"><span data-stu-id="114cd-177">Click the **Change Authentication** button.</span></span> <span data-ttu-id="114cd-178">W oknie dialogowym **Zmienianie uwierzytelniania** upewnij się, że pole wyboru **Bez uwierzytelniania** jest zaznaczone, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="114cd-178">In the **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="114cd-179">W tym samouczku wdrożysz aplikację, która nie wymaga logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="114cd-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="114cd-180">W oknie dialogowym **Nowa aplikacja sieci Web platformy ASP.NET** kliknij przycisk **OK**, aby utworzyć aplikację MVC.</span><span class="sxs-lookup"><span data-stu-id="114cd-180">Back in the **New ASP.NET Web Application** dialog, click **OK** to create the MVC app.</span></span>
8. <span data-ttu-id="114cd-181">Teraz musisz skonfigurować zasoby platformy Azure dla nowej aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="114cd-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="114cd-182">Postępuj zgodnie z instrukcjami znajdującymi się w [sekcji Publikowanie na platformie Azure tego artykułu](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="114cd-182">Follow the steps in the [Publish to Azure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="114cd-183">Następnie wróć do tego samouczka i przejdź do następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="114cd-183">Then, return to this tutorial and proceed to the next step.</span></span>
10. <span data-ttu-id="114cd-184">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy pozycję **Modele** i kliknij polecenie **Dodaj**, a następnie kliknij pozycję **Klasa**.</span><span class="sxs-lookup"><span data-stu-id="114cd-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="114cd-185">W polu **Nazwa** wpisz nazwę **Product.cs**.</span><span class="sxs-lookup"><span data-stu-id="114cd-185">In the **Name** box, type the name **Product.cs**.</span></span> <span data-ttu-id="114cd-186">Następnie kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="114cd-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-the-web-application"></a><span data-ttu-id="114cd-187">Modyfikowanie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="114cd-187">Modify the web application</span></span>

1. <span data-ttu-id="114cd-188">W pliku Product.cs w programie Visual Studio zastąp istniejącą definicję przestrzeni nazw następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="114cd-188">In the Product.cs file in Visual Studio, replace the existing namespace definition with the following code.</span></span>

   ```csharp
    // Declare properties for the products inventory.
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
2. <span data-ttu-id="114cd-189">W Eksploratorze rozwiązań rozwiń folder **Kontrolery**, a następnie kliknij dwukrotnie plik **HomeController.cs**, aby otworzyć go w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="114cd-189">In Solution Explorer, expand the **Controllers** folder, then double-click the **HomeController.cs** file to open it in Visual Studio.</span></span>
3. <span data-ttu-id="114cd-190">W pliku **HomeController.cs** zastąp istniejącą definicję przestrzeni nazw następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="114cd-190">In **HomeController.cs**, replace the existing namespace definition with the following code.</span></span>

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of the products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. <span data-ttu-id="114cd-191">W Eksploratorze rozwiązań rozwiń folder Views\Shared, a następnie kliknij dwukrotnie plik **_Layout.cshtml**, aby otworzyć go w edytorze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="114cd-191">In Solution Explorer, expand the Views\Shared folder, then double-click **_Layout.cshtml** to open it in the Visual Studio editor.</span></span>
5. <span data-ttu-id="114cd-192">Zamień wszystkie wystąpienia ciągu **My ASP.NET Application** na **LITWARE's Products**.</span><span class="sxs-lookup"><span data-stu-id="114cd-192">Change all occurrences of **My ASP.NET Application** to **LITWARE's Products**.</span></span>
6. <span data-ttu-id="114cd-193">Usuń linki **Home**, **About** oraz **Contact**.</span><span class="sxs-lookup"><span data-stu-id="114cd-193">Remove the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="114cd-194">W poniższym przykładzie usuń wyróżniony kod.</span><span class="sxs-lookup"><span data-stu-id="114cd-194">In the following example, delete the highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="114cd-195">W Eksploratorze rozwiązań rozwiń folder Views\Home, a następnie kliknij dwukrotnie plik **Index.cshtml**, aby otworzyć go w edytorze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="114cd-195">In Solution Explorer, expand the Views\Home folder, then double-click **Index.cshtml** to open it in the Visual Studio editor.</span></span> <span data-ttu-id="114cd-196">Zastąp całą zawartość pliku następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="114cd-196">Replace the entire contents of the file with the following code.</span></span>

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
8. <span data-ttu-id="114cd-197">Aby sprawdzić dokładność pracy wykonanej do tej pory, naciśnij kombinację klawiszy **Ctrl+Shift+B** w celu skompilowania projektu.</span><span class="sxs-lookup"><span data-stu-id="114cd-197">To verify the accuracy of your work so far, you can press **Ctrl+Shift+B** to build the project.</span></span>

### <a name="run-the-app-locally"></a><span data-ttu-id="114cd-198">Lokalne uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="114cd-198">Run the app locally</span></span>

<span data-ttu-id="114cd-199">Uruchom aplikację, aby sprawdzić, czy działa.</span><span class="sxs-lookup"><span data-stu-id="114cd-199">Run the application to verify that it works.</span></span>

1. <span data-ttu-id="114cd-200">Upewnij się, że projekt **ProductsPortal** jest aktywnym projektem.</span><span class="sxs-lookup"><span data-stu-id="114cd-200">Ensure that **ProductsPortal** is the active project.</span></span> <span data-ttu-id="114cd-201">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy nazwę projektu i wybierz polecenie **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="114cd-201">Right-click the project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="114cd-202">W programie Visual Studio naciśnij klawisz **F5**.</span><span class="sxs-lookup"><span data-stu-id="114cd-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="114cd-203">Aplikacja powinna uruchomić się w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="114cd-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-the-pieces-together"></a><span data-ttu-id="114cd-204">Składanie fragmentów</span><span class="sxs-lookup"><span data-stu-id="114cd-204">Put the pieces together</span></span>

<span data-ttu-id="114cd-205">Następny krok polega na połączeniu lokalnego serwera produktów z aplikacją ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="114cd-205">The next step is to hook up the on-premises products server with the ASP.NET application.</span></span>

1. <span data-ttu-id="114cd-206">Jeśli nie jest jeszcze otwarty, w programie Visual Studio ponownie otwórz projekt **ProductsPortal**, który został utworzony w sekcji [Tworzenie aplikacji ASP.NET](#create-an-aspnet-application).</span><span class="sxs-lookup"><span data-stu-id="114cd-206">If it is not already open, in Visual Studio re-open the **ProductsPortal** project you created in the [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="114cd-207">Podobnie jak w sekcji „Tworzenie serwera lokalnego” dodaj pakiet NuGet do odwołań projektu.</span><span class="sxs-lookup"><span data-stu-id="114cd-207">Similar to the step in the "Create an On-Premises Server" section, add the NuGet package to the project references.</span></span> <span data-ttu-id="114cd-208">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt **ProductsPortal**, a następnie kliknij polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="114cd-208">In Solution Explorer, right-click the **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="114cd-209">Wyszukaj ciąg „Service Bus”, a następnie wybierz element **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="114cd-209">Search for "Service Bus" and select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="114cd-210">Następnie zakończ instalację i zamknij to okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="114cd-210">Then complete the installation and close this dialog box.</span></span>
4. <span data-ttu-id="114cd-211">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt **ProductsPortal**, kliknij polecenie **Dodaj**, a następnie kliknij pozycję **Istniejący element**.</span><span class="sxs-lookup"><span data-stu-id="114cd-211">In Solution Explorer, right-click the **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="114cd-212">Przejdź do pliku **ProductsContract.cs** z projektu konsolowego **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="114cd-212">Navigate to the **ProductsContract.cs** file from the **ProductsServer** console project.</span></span> <span data-ttu-id="114cd-213">Kliknij, aby zaznaczyć plik ProductsContract.cs.</span><span class="sxs-lookup"><span data-stu-id="114cd-213">Click to highlight ProductsContract.cs.</span></span> <span data-ttu-id="114cd-214">Kliknij strzałkę w dół obok pozycji **Dodaj**, a następnie kliknij polecenie **Dodaj jako link**.</span><span class="sxs-lookup"><span data-stu-id="114cd-214">Click the down arrow next to **Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="114cd-215">W edytorze programu Visual Studio otwórz plik **HomeController.cs** i zastąp definicję przestrzeni nazw następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="114cd-215">Now open the **HomeController.cs** file in the Visual Studio editor and replace the namespace definition with the following code.</span></span> <span data-ttu-id="114cd-216">Koniecznie zastąp ciąg *yourServiceNamespace* nazwą Twojej przestrzeni nazw, a ciąg *yourKey* kluczem SAS.</span><span class="sxs-lookup"><span data-stu-id="114cd-216">Be sure to replace *yourServiceNamespace* with the name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="114cd-217">Dzięki temu klient będzie miał możliwość wywołania usługi lokalnej i zwrócenia wyniku wywołania.</span><span class="sxs-lookup"><span data-stu-id="114cd-217">This will enable the client to call the on-premises service, returning the result of the call.</span></span>

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
           // Declare the channel factory.
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
                   // Return a view of the products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. <span data-ttu-id="114cd-218">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy rozwiązanie **ProductsPortal** (upewnij się, że klikasz prawym przyciskiem myszy rozwiązanie, a nie projekt).</span><span class="sxs-lookup"><span data-stu-id="114cd-218">In Solution Explorer, right-click the **ProductsPortal** solution (make sure to right-click the solution, not the project).</span></span> <span data-ttu-id="114cd-219">Kliknij pozycję **Dodaj**, a następnie kliknij pozycję **Istniejący projekt**.</span><span class="sxs-lookup"><span data-stu-id="114cd-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="114cd-220">Przejdź do projektu **ProductsServer**, a następnie kliknij dwukrotnie plik rozwiązania **ProductsServer.csproj**, aby go dodać.</span><span class="sxs-lookup"><span data-stu-id="114cd-220">Navigate to the **ProductsServer** project, then double-click the **ProductsServer.csproj** solution file to add it.</span></span>
9. <span data-ttu-id="114cd-221">Serwer **ProductsServer** musi być uruchomiony, aby wyświetlić dane w aplikacji **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="114cd-221">**ProductsServer** must be running in order to display the data on **ProductsPortal**.</span></span> <span data-ttu-id="114cd-222">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy rozwiązanie **ProductsPortal** i kliknij polecenie **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="114cd-222">In Solution Explorer, right-click the **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="114cd-223">Wyświetli się okno dialogowe **Strony właściwości**.</span><span class="sxs-lookup"><span data-stu-id="114cd-223">The **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="114cd-224">Po lewej stronie kliknij pozycję **Projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="114cd-224">On the left side, click **Startup Project**.</span></span> <span data-ttu-id="114cd-225">Po prawej stronie kliknij pozycję **Wiele projektów startowych**.</span><span class="sxs-lookup"><span data-stu-id="114cd-225">On the right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="114cd-226">Upewnij się, że projekty **ProductsServer** i **ProductsPortal** są wymienione w tej kolejności i dla obu tych projektów ustawiono akcję **Uruchomienie**.</span><span class="sxs-lookup"><span data-stu-id="114cd-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as the action for both.</span></span>

      ![][25]

11. <span data-ttu-id="114cd-227">W oknie dialogowym **Właściwości** kliknij pozycję **Zależności projektu**, która znajduje się po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="114cd-227">Still in the **Properties** dialog box, click **Project Dependencies** on the left side.</span></span>
12. <span data-ttu-id="114cd-228">Na liście **Projekty** kliknij projekt **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="114cd-228">In the **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="114cd-229">Upewnij się, że projekt **ProductsPortal** nie jest wybrany.</span><span class="sxs-lookup"><span data-stu-id="114cd-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="114cd-230">Na liście **Projekty** kliknij projekt **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="114cd-230">In the **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="114cd-231">Upewnij się, że projekt **ProductsServer** jest wybrany.</span><span class="sxs-lookup"><span data-stu-id="114cd-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="114cd-232">W oknie dialogowym **Strony właściwości** kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="114cd-232">Click **OK** in the **Property Pages** dialog box.</span></span>

## <a name="run-the-project-locally"></a><span data-ttu-id="114cd-233">Lokalne uruchamianie projektu</span><span class="sxs-lookup"><span data-stu-id="114cd-233">Run the project locally</span></span>

<span data-ttu-id="114cd-234">Aby przetestować aplikację lokalnie, w programie Visual Studio naciśnij klawisz **F5**.</span><span class="sxs-lookup"><span data-stu-id="114cd-234">To test the application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="114cd-235">Serwer lokalny (**ProductsServer**) powinien uruchomić się jako pierwszy, a następnie aplikacja **ProductsPortal** powinna uruchomić się w oknie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="114cd-235">The on-premises server (**ProductsServer**) should start first, then the **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="114cd-236">Tym razem pojawi się spis produktów zawierający dane pobrane z lokalnego systemu usługi produktów.</span><span class="sxs-lookup"><span data-stu-id="114cd-236">This time, you will see that the product inventory lists data retrieved from the product service on-premises system.</span></span>

![][10]

<span data-ttu-id="114cd-237">Naciśnij przycisk **Odśwież** na stronie **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="114cd-237">Press **Refresh** on the **ProductsPortal** page.</span></span> <span data-ttu-id="114cd-238">Przy każdym odświeżeniu strony aplikacja serwera wyświetli komunikat podczas wywoływany metody `GetProducts()` z serwera **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="114cd-238">Each time you refresh the page, you'll see the server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="114cd-239">Zamknij obie aplikacje przed przejściem do następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="114cd-239">Close both applications before proceeding to the next step.</span></span>

## <a name="deploy-the-productsportal-project-to-an-azure-web-app"></a><span data-ttu-id="114cd-240">Wdrażanie projektu ProductsPortal w aplikacji sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="114cd-240">Deploy the ProductsPortal project to an Azure web app</span></span>

<span data-ttu-id="114cd-241">Następny krok polega na ponownym opublikowaniu frontonu projektu **ProductsPortal** aplikacji internetowej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="114cd-241">The next step is to republish the Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="114cd-242">Wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="114cd-242">Do the following:</span></span>

1. <span data-ttu-id="114cd-243">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt **ProductsPortal**, a następnie kliknij pozycję **Publikuj**.</span><span class="sxs-lookup"><span data-stu-id="114cd-243">In Solution Explorer, right-click the **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="114cd-244">Następnie kliknij pozycję **Publikuj** na stronie **Publikowanie**.</span><span class="sxs-lookup"><span data-stu-id="114cd-244">Then, click **Publish** on the **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="114cd-245">Gdy projekt sieci Web **ProductsPortal** zostanie automatycznie uruchomiony po wdrożeniu, w oknie przeglądarki może zostać wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="114cd-245">You may see an error message in the browser window when the **ProductsPortal** web project is automatically launched after the deployment.</span></span> <span data-ttu-id="114cd-246">Jest to oczekiwane. Błąd występuje, ponieważ aplikacja **ProductsServer** nie jest jeszcze uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="114cd-246">This is expected, and occurs because the **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="114cd-247">Skopiuj adres URL wdrożonej aplikacji sieci Web, ponieważ będzie potrzebny w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="114cd-247">Copy the URL of the deployed web app, as you will need the URL in the next step.</span></span> <span data-ttu-id="114cd-248">Ten adres URL możesz również uzyskać w oknie Działanie usługi Azure App Service w programie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="114cd-248">You can also obtain this URL from the Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="114cd-249">Zamknij okno przeglądarki, aby zatrzymać działającą aplikację.</span><span class="sxs-lookup"><span data-stu-id="114cd-249">Close the browser window to stop the running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="114cd-250">Ustawianie projektu ProductsPortal jako aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="114cd-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="114cd-251">Przed uruchomieniem aplikacji w chmurze musisz się upewnić, że aplikacja **ProductsPortal** jest uruchamiana z poziomu programu Visual Studio jako aplikacja sieci Web.</span><span class="sxs-lookup"><span data-stu-id="114cd-251">Before running the application in the cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="114cd-252">W programie Visual Studio kliknij prawym przyciskiem myszy projekt **ProductsPortal**, a następnie kliknij pozycję **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="114cd-252">In Visual Studio, right-click the **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="114cd-253">W lewej kolumnie kliknij pozycję **Sieć Web**.</span><span class="sxs-lookup"><span data-stu-id="114cd-253">In the left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="114cd-254">W sekcji **Akcja uruchamiania** kliknij przycisk **Początkowy adres URL** i w polu tekstowym wprowadź adres URL wcześniej wdrożonej aplikacji sieci Web, na przykład `http://productsportal1234567890.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="114cd-254">In the **Start Action** section, click the **Start URL** button, and in the text box enter the URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="114cd-255">W menu **Plik** programu Visual Studio kliknij polecenie **Zapisz wszystko**.</span><span class="sxs-lookup"><span data-stu-id="114cd-255">From the **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="114cd-256">W menu Kompilacja programu Visual Studio kliknij polecenie **Kompiluj ponownie rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="114cd-256">From the Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="114cd-257">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="114cd-257">Run the application</span></span>

1. <span data-ttu-id="114cd-258">Naciśnij klawisz F5, aby skompilować i uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="114cd-258">Press F5 to build and run the application.</span></span> <span data-ttu-id="114cd-259">Serwer lokalny (aplikacja konsolowa **ProductsServer**) powinien uruchomić się jako pierwszy, a następnie aplikacja **ProductsPortal** powinna uruchomić się w oknie przeglądarki, jak pokazano na poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="114cd-259">The on-premises server (the **ProductsServer** console application) should start first, then the **ProductsPortal** application should start in a browser window, as shown in the following screen shot.</span></span> <span data-ttu-id="114cd-260">Ponownie pojawi się spis produktów zawierający dane pobrane z lokalnego systemu usługi produktów, a dane zostaną wyświetlone w aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="114cd-260">Notice again that the product inventory lists data retrieved from the product service on-premises system, and displays that data in the web app.</span></span> <span data-ttu-id="114cd-261">Sprawdź adres URL, aby upewnić się, że aplikacja **ProductsPortal** działa w chmurze jako aplikacja sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="114cd-261">Check the URL to make sure that **ProductsPortal** is running in the cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="114cd-262">Aplikacja konsolowa **ProductsServer** musi działać i być w stanie udostępniać dane aplikacji **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="114cd-262">The **ProductsServer** console application must be running and able to serve the data to the **ProductsPortal** application.</span></span> <span data-ttu-id="114cd-263">Jeśli przeglądarka wyświetla komunikat o błędzie, zaczekaj kilka sekund, aż serwer **ProductsServer** zostanie załadowany i wyświetli następujący komunikat.</span><span class="sxs-lookup"><span data-stu-id="114cd-263">If the browser displays an error, wait a few more seconds for **ProductsServer** to load and display the following message.</span></span> <span data-ttu-id="114cd-264">Następnie naciśnij przycisk **Odśwież** w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="114cd-264">Then press **Refresh** in the browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="114cd-265">W przeglądarce naciśnij przycisk **Odśwież** na stronie **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="114cd-265">Back in the browser, press **Refresh** on the **ProductsPortal** page.</span></span> <span data-ttu-id="114cd-266">Przy każdym odświeżeniu strony aplikacja serwera wyświetli komunikat podczas wywoływany metody `GetProducts()` z serwera **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="114cd-266">Each time you refresh the page, you'll see the server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="114cd-267">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="114cd-267">Next steps</span></span>

<span data-ttu-id="114cd-268">Aby dowiedzieć się więcej na temat usługi Azure Relay, zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="114cd-268">To learn more about Azure Relay, see the following resources:</span></span>  

* [<span data-ttu-id="114cd-269">Co to jest usługa Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="114cd-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="114cd-270">Jak używać usługi Relay</span><span class="sxs-lookup"><span data-stu-id="114cd-270">How to use Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

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
