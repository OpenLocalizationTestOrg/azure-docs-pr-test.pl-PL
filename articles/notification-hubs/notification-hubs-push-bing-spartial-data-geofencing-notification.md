---
title: "powiadomienia wypychane odgrodzone aaaGeo przy użyciu usługi Azure Notification Hubs i Bing Spatial Data | Dokumentacja firmy Microsoft"
description: "Z tego samouczka dowiesz się, jak toodeliver oparte na lokalizacji wypychanie powiadomień przy użyciu usługi Azure Notification Hubs i Bing Spatial Data."
services: notification-hubs
documentationcenter: windows
keywords: powiadomienie wypychane, powiadomienia wypychane
author: dend
manager: yuaxu
editor: dend
ms.assetid: f41beea1-0d62-4418-9ffc-c9d70607a1b7
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/31/2016
ms.author: dendeli
ms.openlocfilehash: d6efe473537f2159240c53e780741f12619c045d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="19f7d-104">Wirtualne grodzenie powiadomień wypychanych przy użyciu usług Azure Notification Hubs i Bing Spatial Data</span><span class="sxs-lookup"><span data-stu-id="19f7d-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="19f7d-105">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="19f7d-105">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="19f7d-106">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="19f7d-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="19f7d-107">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span><span class="sxs-lookup"><span data-stu-id="19f7d-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="19f7d-108">Z tego samouczka dowiesz się, jak toodeliver oparte na lokalizacji wypychanie powiadomień przy użyciu usługi Azure Notification Hubs i Bing Spatial Data z wykorzystaniem aplikacji platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="19f7d-108">In this tutorial, you will learn how toodeliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19f7d-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="19f7d-109">Prerequisites</span></span>
<span data-ttu-id="19f7d-110">Najpierw i, należy upewnić się, że wszystkie hello oprogramowania i usług wstępne toomake:</span><span class="sxs-lookup"><span data-stu-id="19f7d-110">First and foremost, you need toomake sure that you have all hello software and service pre-requisites:</span></span>

* <span data-ttu-id="19f7d-111">Program [Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) lub nowszy (można również użyć wersji [Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409)).</span><span class="sxs-lookup"><span data-stu-id="19f7d-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="19f7d-112">Najnowszą wersję hello [zestawu Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="19f7d-112">Latest version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="19f7d-113">[Konto Centrum deweloperów Map Bing](https://www.bingmapsportal.com/) (można utworzyć je bezpłatnie i skojarzyć z kontem Microsoft).</span><span class="sxs-lookup"><span data-stu-id="19f7d-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="19f7d-114">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="19f7d-114">Getting Started</span></span>
<span data-ttu-id="19f7d-115">Zacznijmy od utworzenia projektu hello.</span><span class="sxs-lookup"><span data-stu-id="19f7d-115">Let’s start by creating hello project.</span></span> <span data-ttu-id="19f7d-116">W programie Visual Studio utwórz nowy projekt typu **Pusta aplikacja (uniwersalna aplikacja systemu Windows)**.</span><span class="sxs-lookup"><span data-stu-id="19f7d-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="19f7d-117">Po zakończeniu tworzenia projektu hello powinien mieć kontroler powitania dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="19f7d-117">Once hello project creation is complete, you should have hello harness for hello app itself.</span></span> <span data-ttu-id="19f7d-118">Teraz Skonfigurujmy wszystko pod kątem infrastruktury wirtualnego grodzenia hello.</span><span class="sxs-lookup"><span data-stu-id="19f7d-118">Now let’s set up everything for hello geo-fencing infrastructure.</span></span> <span data-ttu-id="19f7d-119">Ponieważ firma Microsoft będzie toouse, które usługi Bing dla tego, istnieje publiczny punkt końcowy interfejsu API REST, który pozwala nam tooquery określonego zakresu lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="19f7d-119">Because we are going toouse Bing services for this, there is a public REST API endpoint that allows us tooquery specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="19f7d-120">Konieczne będzie toospecify hello następujące parametry tooget go do pracy:</span><span class="sxs-lookup"><span data-stu-id="19f7d-120">You will need toospecify hello following parameters tooget it working:</span></span>

* <span data-ttu-id="19f7d-121">**Identyfikator źródła danych** i **Nazwa źródła danych** — w interfejsie API Map Bing źródła danych zawierają różne metadane w zasobnikach, takie jak lokalizacje i godziny pracy.</span><span class="sxs-lookup"><span data-stu-id="19f7d-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="19f7d-122">Możesz uzyskać więcej informacji na ten temat tutaj.</span><span class="sxs-lookup"><span data-stu-id="19f7d-122">You can read more about those here.</span></span> 
* <span data-ttu-id="19f7d-123">**Nazwa jednostki** — Witaj jednostki, której toouse jako punkt odniesienia dla powiadomienia hello.</span><span class="sxs-lookup"><span data-stu-id="19f7d-123">**Entity Name** – hello entity you want toouse as a reference point for hello notification.</span></span> 
* <span data-ttu-id="19f7d-124">**Klucz interfejsu API map Bing** — jest to hello klucz uzyskany wcześniej podczas tworzenia konta Centrum deweloperów Bing hello.</span><span class="sxs-lookup"><span data-stu-id="19f7d-124">**Bing Maps API Key** – this is hello key that you obtained earlier when you created hello Bing Dev Center account.</span></span>

<span data-ttu-id="19f7d-125">Dla każdego z powyższych elementów hello Poznajmy szczegółowo na powitania instalacji.</span><span class="sxs-lookup"><span data-stu-id="19f7d-125">Let’s do a deep-dive on hello setup for each of hello elements above.</span></span>

## <a name="setting-up-hello-data-source"></a><span data-ttu-id="19f7d-126">Konfigurowanie hello źródła danych</span><span class="sxs-lookup"><span data-stu-id="19f7d-126">Setting up hello data source</span></span>
<span data-ttu-id="19f7d-127">Możesz zrobić to w hello Centrum deweloperów map Bing.</span><span class="sxs-lookup"><span data-stu-id="19f7d-127">You can do it in hello Bing Maps Dev Center.</span></span> <span data-ttu-id="19f7d-128">Po prostu kliknij **źródeł danych** w hello górnym pasku nawigacyjnym i wybierz **Zarządzanie źródłami danych**.</span><span class="sxs-lookup"><span data-stu-id="19f7d-128">Simply click on **Data sources** in hello top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="19f7d-129">Jeśli wcześniej nie korzystano z interfejsu API map Bing, prawdopodobnie nie będzie żadnych źródeł danych nie istnieje, można utworzyć nowy, klikając na przekazywanie danych tooa źródło danych.</span><span class="sxs-lookup"><span data-stu-id="19f7d-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data tooa data source.</span></span> <span data-ttu-id="19f7d-130">Upewnij się, że możesz wypełnić wszystkie pola wymagane hello:</span><span class="sxs-lookup"><span data-stu-id="19f7d-130">Make sure you fill out all hello required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="19f7d-131">Użytkownik może się zastanawiać — co to jest plik danych hello i co należy przekazać?</span><span class="sxs-lookup"><span data-stu-id="19f7d-131">You might be wondering – what is hello data file and what should you be uploading?</span></span> <span data-ttu-id="19f7d-132">Dla celów hello ten test możemy użyć próbki hello opartego na potoku, który określa obszar waterfront Poznań hello:</span><span class="sxs-lookup"><span data-stu-id="19f7d-132">For hello purposes of this test, we can just use hello sample pipe-based that frames an area of hello San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="19f7d-133">Witaj powyżej reprezentuje następującą jednostkę:</span><span class="sxs-lookup"><span data-stu-id="19f7d-133">hello above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="19f7d-134">Po prostu skopiuj i Wklej Powyższy ciąg hello do nowego pliku i zapisz go jako **NotificationHubsGeofence.pipe**, a następnie przekaż go w Centrum deweloperów Bing hello.</span><span class="sxs-lookup"><span data-stu-id="19f7d-134">Simply copy and paste hello string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in hello Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="19f7d-135">Może być zostanie wyświetlony monit o toospecify klucza hello **klucza głównego** różni się od hello **klucz zapytania**.</span><span class="sxs-lookup"><span data-stu-id="19f7d-135">You might be prompted toospecify a new key for hello **Master Key** that is different from hello **Query Key**.</span></span> <span data-ttu-id="19f7d-136">Po prostu Utwórz nowy klucz przez hello pulpitu nawigacyjnego i Odśwież hello stronę przekazywania źródła danych.</span><span class="sxs-lookup"><span data-stu-id="19f7d-136">Simply create a new key through hello dashboard and refresh hello data source upload page.</span></span>
> 
> 

<span data-ttu-id="19f7d-137">Po przekazaniu pliku danych hello należy toomake Opublikuj hello źródła danych.</span><span class="sxs-lookup"><span data-stu-id="19f7d-137">Once you upload hello data file, you will need toomake sure that you publish hello data source.</span></span> 

<span data-ttu-id="19f7d-138">Przejdź za**Zarządzanie źródłami danych**, jak opisano powyżej, Znajdź źródło danych na liście hello i wybierz polecenie **publikowania** w hello **akcje** kolumny.</span><span class="sxs-lookup"><span data-stu-id="19f7d-138">Go too**Manage Data Sources**, just like we did above, find your data source in hello list and click on **Publish** in hello **Actions** column.</span></span> <span data-ttu-id="19f7d-139">W nieco, powinny pojawić się źródła danych w hello **opublikowane źródła danych** karty:</span><span class="sxs-lookup"><span data-stu-id="19f7d-139">In a bit, you should see your data source in hello **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="19f7d-140">Jeśli klikniesz przycisk **Edytuj**, możesz będą mogli toosee jeden rzut oka w nim wprowadzone lokalizacje:</span><span class="sxs-lookup"><span data-stu-id="19f7d-140">If you click **Edit**, you will be able toosee at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="19f7d-141">W tym momencie hello portalu nie są wyświetlane hello granice dla wirtualnego ogrodzenia hello, że utworzyliśmy — potrzebne jest jedynie potwierdzenie, że określona lokalizacja hello znajduje się w odpowiedniej okolicy hello.</span><span class="sxs-lookup"><span data-stu-id="19f7d-141">At this point, hello portal does not show you hello boundaries for hello geofence that we created – all we need is a confirmation that hello location specified is in hello right vicinity.</span></span>

<span data-ttu-id="19f7d-142">Masz teraz wszystkie wymagania hello hello źródła danych.</span><span class="sxs-lookup"><span data-stu-id="19f7d-142">Now you have all hello requirements for hello data source.</span></span> <span data-ttu-id="19f7d-143">Kliknij przycisk Szczegóły hello tooget na powitania adresu URL żądania dla wywołania interfejsu API hello, w Centrum deweloperów map Bing hello **źródeł danych** i wybierz **informacje o źródle danych**.</span><span class="sxs-lookup"><span data-stu-id="19f7d-143">tooget hello details on hello request URL for hello API call, in hello Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="19f7d-144">Witaj **adres URL zapytania** jest interesuje NAS tutaj.</span><span class="sxs-lookup"><span data-stu-id="19f7d-144">hello **Query URL** is what we’re after here.</span></span> <span data-ttu-id="19f7d-145">Jest to hello punkt końcowy, względem którego możemy wykonywać zapytania toocheck w czy hello urządzenie jest obecnie w granicach hello lokalizacji lub nie.</span><span class="sxs-lookup"><span data-stu-id="19f7d-145">This is hello endpoint against which we can execute queries toocheck whether hello device is currently within hello boundaries of a location or not.</span></span> <span data-ttu-id="19f7d-146">tooperform to sprawdzić, należy po prostu tooexecute GET Wywołaj względem adresu URL zapytania hello z następujących parametrów dołączane hello:</span><span class="sxs-lookup"><span data-stu-id="19f7d-146">tooperform this check, we simply need tooexecute a GET call against hello query URL, with hello following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="19f7d-147">W ten sposób określisz punkt docelowy uzyskany z urządzenia hello, a mapy Bing automatycznie wykonają hello obliczeń toosee czy znajduje się on w wirtualnym ogrodzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="19f7d-147">That way you're specifying a target point that we obtain from hello device and Bing Maps will automatically perform hello calculations toosee whether it is within hello geofence.</span></span> <span data-ttu-id="19f7d-148">Po wykonaniu żądania hello za pomocą przeglądarki (lub programu cURL), uzyskasz standardową odpowiedź w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="19f7d-148">Once you execute hello request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="19f7d-149">Ta odpowiedź tylko wtedy, gdy hello punkt rzeczywiście znajduje się w wyznaczonych granicach hello.</span><span class="sxs-lookup"><span data-stu-id="19f7d-149">This response only happens when hello point is actually within hello designated boundaries.</span></span> <span data-ttu-id="19f7d-150">W przeciwnym razie otrzymasz pusty zasobnik **results**:</span><span class="sxs-lookup"><span data-stu-id="19f7d-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a><span data-ttu-id="19f7d-151">Konfigurowanie aplikacji platformy uniwersalnej systemu Windows hello</span><span class="sxs-lookup"><span data-stu-id="19f7d-151">Setting up hello UWP application</span></span>
<span data-ttu-id="19f7d-152">Teraz, gdy mamy hello źródło danych jest gotowe, możemy rozpocząć pracę na powitania aplikacji platformy uniwersalnej systemu Windows, którą zainicjowano wcześniej.</span><span class="sxs-lookup"><span data-stu-id="19f7d-152">Now that we have hello data source ready, we can start working on hello UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="19f7d-153">Najpierw musimy włączyć usługi lokalizacji dla naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="19f7d-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="19f7d-154">toodo, kliknij dwukrotnie `Package.appxmanifest` w pliku **Eksploratora rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="19f7d-154">toodo this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="19f7d-155">Na karcie właściwości pakietu hello, która została otwarta, kliknij **możliwości** i upewnij się, że wybrano **lokalizacji**:</span><span class="sxs-lookup"><span data-stu-id="19f7d-155">In hello package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="19f7d-156">Możliwość lokalizacji hello jest zadeklarowana, Utwórz nowy folder w rozwiązaniu o nazwie `Core`i Dodaj nowy plik w nazwie `LocationHelper.cs`:</span><span class="sxs-lookup"><span data-stu-id="19f7d-156">As hello location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="19f7d-157">Witaj `LocationHelper` samej klasy w tym momencie jest dosyć prosta — wszystkie robi zezwolić nam lokalizacji użytkownika hello tooobtain przy użyciu interfejsu API systemu hello:</span><span class="sxs-lookup"><span data-stu-id="19f7d-157">hello `LocationHelper` class itself is fairly basic at this point – all it does is allow us tooobtain hello user location through hello system API:</span></span>

    using System;
    using System.Threading.Tasks;
    using Windows.Devices.Geolocation;

    namespace NotificationHubs.Geofence.Core
    {
        public class LocationHelper
        {
            private static readonly uint AppDesiredAccuracyInMeters = 10;

            public async static Task<Geoposition> GetCurrentLocation()
            {
                var accessStatus = await Geolocator.RequestAccessAsync();
                switch (accessStatus)
                {
                    case GeolocationAccessStatus.Allowed:
                        {
                            Geolocator geolocator = new Geolocator { DesiredAccuracyInMeters = AppDesiredAccuracyInMeters };

                            return await geolocator.GetGeopositionAsync();
                        }
                    default:
                        {
                            return null;
                        }
                }
            }

        }
    }

<span data-ttu-id="19f7d-158">Możesz przeczytać więcej na temat uzyskiwania hello lokalizacji użytkownika w aplikacji platformy uniwersalnej systemu Windows w oficjalne hello [dokumencie MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span><span class="sxs-lookup"><span data-stu-id="19f7d-158">You can read more about getting hello user’s location in UWP apps in hello official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="19f7d-159">toocheck, który hello uzyskiwanie lokalizacji rzeczywiście działa, otwórz hello kodu strony, strony głównej (`MainPage.xaml.cs`).</span><span class="sxs-lookup"><span data-stu-id="19f7d-159">toocheck that hello location acquisition is actually working, open hello code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="19f7d-160">Utwórz nowy program obsługi zdarzeń dla hello `Loaded` zdarzenia w hello `MainPage` konstruktora:</span><span class="sxs-lookup"><span data-stu-id="19f7d-160">Create a new event handler for hello `Loaded` event in hello `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="19f7d-161">Implementacja Hello hello obsługi zdarzeń wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="19f7d-161">hello implementation of hello event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="19f7d-162">Zwróć uwagę, został zadeklarowany obsługi hello jako asynchroniczny ponieważ `GetCurrentLocation` jest oczekujący i dlatego wymaga toobe wykonywane w kontekście asynchronicznym.</span><span class="sxs-lookup"><span data-stu-id="19f7d-162">Notice that we declared hello handler as async because `GetCurrentLocation` is awaitable, and therefore requires toobe executed in an async context.</span></span> <span data-ttu-id="19f7d-163">Ponadto ponieważ w pewnych okolicznościach możemy lokalizacją null (np. usługi lokalizacji hello są wyłączone lub aplikacji hello odmówiono uprawnienia tooaccess lokalizacji), należy się upewnić, że jest prawidłowo obsługiwane przy użyciu sprawdzania wartości null toomake.</span><span class="sxs-lookup"><span data-stu-id="19f7d-163">Also, because under certain circumstances we might end up with a null location (e.g. hello location services are disabled or hello application was denied permissions tooaccess location), we need toomake sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="19f7d-164">Uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="19f7d-164">Run hello application.</span></span> <span data-ttu-id="19f7d-165">Zezwól na dostęp do lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="19f7d-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="19f7d-166">Witaj po uruchomieniu aplikacji, powinny być stanie toosee hello współrzędnych w hello **dane wyjściowe** okno:</span><span class="sxs-lookup"><span data-stu-id="19f7d-166">Once hello application launches, you should be able toosee hello coordinates in hello **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="19f7d-167">Teraz wiadomo, że pobieranie lokalizacji działa – możesz wolnego tooremove hello testowy — program obsługi zdarzeń Loaded, ponieważ firma Microsoft nie będzie już używany.</span><span class="sxs-lookup"><span data-stu-id="19f7d-167">Now you know that location acquisition works – feel free tooremove hello test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="19f7d-168">Witaj następnym krokiem jest toocapture zmiany lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="19f7d-168">hello next step is toocapture location changes.</span></span> <span data-ttu-id="19f7d-169">W tym Przejdź wstecz toohello `LocationHelper` klasy i dodać obsługi zdarzenia hello `PositionChanged`:</span><span class="sxs-lookup"><span data-stu-id="19f7d-169">For that, let’s go back toohello `LocationHelper` class and add hello event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="19f7d-170">Implementacja Hello spowoduje wyświetlenie współrzędnych lokalizacji hello w hello **dane wyjściowe** okno:</span><span class="sxs-lookup"><span data-stu-id="19f7d-170">hello implementation will show hello location coordinates in hello **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a><span data-ttu-id="19f7d-171">Konfigurowanie hello wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="19f7d-171">Setting up hello backend</span></span>
<span data-ttu-id="19f7d-172">Pobierz hello [przykład zaplecza programu .NET z usługi GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="19f7d-172">Download hello [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="19f7d-173">Po zakończeniu pobierania hello Otwórz hello `NotifyUsers` folder, a następnie — Witaj `NotifyUsers.sln` pliku.</span><span class="sxs-lookup"><span data-stu-id="19f7d-173">Once hello download completes, open hello `NotifyUsers` folder, and subsequently – hello `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="19f7d-174">Zestaw hello `AppBackend` projektu jako hello **projekt startowy** i uruchom je.</span><span class="sxs-lookup"><span data-stu-id="19f7d-174">Set hello `AppBackend` project as hello **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="19f7d-175">Hello projektu jest już skonfigurowany toosend wypychania powiadomień tootarget urządzeń, dlatego potrzebujemy toodo tylko dwie czynności — wymienić hello ciąg połączenia na odpowiednie dla Centrum powiadomień hello i dodać granicę identyfikacji toosend hello powiadomienia tylko wtedy, gdy hello Użytkownik znajduje się w wirtualnym ogrodzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="19f7d-175">hello project is already configured toosend push notifications tootarget devices, so we’ll need toodo only two things – swap out hello right connection string for hello notification hub and add boundary identification toosend hello notification only when hello user is within hello geofence.</span></span>

<span data-ttu-id="19f7d-176">tooconfigure hello w ciągu połączenia, hello `Models` Otwórz folder `Notifications.cs`.</span><span class="sxs-lookup"><span data-stu-id="19f7d-176">tooconfigure hello connection string, in hello `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="19f7d-177">Witaj `NotificationHubClient.CreateClientFromConnectionString` funkcji powinny zawierać hello informacje o Centrum powiadomień uzyskane w hello [Azure Portal](https://portal.azure.com) (Szukaj wewnątrz hello **zasady dostępu** bloku w  **Ustawienia**).</span><span class="sxs-lookup"><span data-stu-id="19f7d-177">hello `NotificationHubClient.CreateClientFromConnectionString` function should contain hello information about your notification hub that you can get in hello [Azure Portal](https://portal.azure.com) (look inside hello **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="19f7d-178">Zapisz hello zaktualizowany plik konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="19f7d-178">Save hello updated configuration file.</span></span>

<span data-ttu-id="19f7d-179">Teraz potrzebujemy toocreate model dla wyniku interfejsu API map Bing hello.</span><span class="sxs-lookup"><span data-stu-id="19f7d-179">Now we need toocreate a model for hello Bing Maps API result.</span></span> <span data-ttu-id="19f7d-180">Witaj najprostszym toodo sposób, który jest kliknij prawym przyciskiem myszy na powitania `Models` folderu, **Dodaj** > **klasy**.</span><span class="sxs-lookup"><span data-stu-id="19f7d-180">hello easiest way toodo that is right-click on hello `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="19f7d-181">Nadaj jej nazwę `GeofenceBoundary.cs`.</span><span class="sxs-lookup"><span data-stu-id="19f7d-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="19f7d-182">Po zakończeniu skopiuj hello JSON z odpowiedzi hello interfejsu API, omówionej w pierwszej sekcji hello i w programie Visual Studio użyj **Edytuj** > **Wklej specjalne** > **Wklej dane JSON jako klasy**.</span><span class="sxs-lookup"><span data-stu-id="19f7d-182">Once done, copy hello JSON from hello API response that we discussed in hello first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="19f7d-183">W ten sposób Upewniamy się ten obiekt hello będzie można przeprowadzić deserializacji, dokładnie tak, jak zamierza.</span><span class="sxs-lookup"><span data-stu-id="19f7d-183">That way we ensure that hello object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="19f7d-184">Wynikowy zestaw klas powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="19f7d-184">Your resulting class set should resemble this:</span></span>

    namespace AppBackend.Models
    {
        public class Rootobject
        {
            public D d { get; set; }
        }

        public class D
        {
            public string __copyright { get; set; }
            public Result[] results { get; set; }
        }

        public class Result
        {
            public __Metadata __metadata { get; set; }
            public string EntityID { get; set; }
            public string Name { get; set; }
            public float Longitude { get; set; }
            public float Latitude { get; set; }
            public string Boundary { get; set; }
            public string Confidence { get; set; }
            public string Locality { get; set; }
            public string AddressLine { get; set; }
            public string AdminDistrict { get; set; }
            public string CountryRegion { get; set; }
            public string PostalCode { get; set; }
        }

        public class __Metadata
        {
            public string uri { get; set; }
        }
    }

<span data-ttu-id="19f7d-185">Następnie otwórz plik `Controllers` > `NotificationsController.cs`.</span><span class="sxs-lookup"><span data-stu-id="19f7d-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="19f7d-186">Potrzebujemy tootweak powitania po wywołaniu tooaccount hello docelową długość i szerokość geograficzną.</span><span class="sxs-lookup"><span data-stu-id="19f7d-186">We need tootweak hello Post call tooaccount for hello target longitude and latitude.</span></span> <span data-ttu-id="19f7d-187">Do tego, po prostu dodaj dwa sygnatury funkcji toohello ciągów — `latitude` i `longitude`.</span><span class="sxs-lookup"><span data-stu-id="19f7d-187">For that, simply add two strings toohello function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="19f7d-188">Utwórz nową klasę w projekcie hello o nazwie `ApiHelper.cs` — użyjemy jej tooconnect tooBing toocheck punktu granic przecięcia.</span><span class="sxs-lookup"><span data-stu-id="19f7d-188">Create a new class within hello project called `ApiHelper.cs` – we’ll use it tooconnect tooBing toocheck point boundary intersections.</span></span> <span data-ttu-id="19f7d-189">Zaimplementuj funkcję `IsPointWithinBounds` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="19f7d-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

    public class ApiHelper
    {
        public static readonly string ApiEndpoint = "{YOUR_QUERY_ENDPOINT}?spatialFilter=intersects(%27POINT%20({0}%20{1})%27)&$format=json&key={2}";
        public static readonly string ApiKey = "{YOUR_API_KEY}";

        public static bool IsPointWithinBounds(string longitude,string latitude)
        {
            var json = new WebClient().DownloadString(string.Format(ApiEndpoint, longitude, latitude, ApiKey));
            var result = JsonConvert.DeserializeObject<Rootobject>(json);
            if (result.d.results != null && result.d.results.Count() > 0)
            {
                return true;
            }
            else
            {
                return false;
            }
        }
    }

> [!NOTE]
> <span data-ttu-id="19f7d-190">Upewnij się, że punkt końcowy hello interfejsu API toosubstitute o hello adresu URL zapytania uzyskanym wcześniej z hello Centrum deweloperów Bing (dotyczy klucza interfejsu API toohello).</span><span class="sxs-lookup"><span data-stu-id="19f7d-190">Make sure toosubstitute hello API endpoint with hello query URL that you obtained earlier from hello Bing Dev Center (same applies toohello API key).</span></span> 
> 
> 

<span data-ttu-id="19f7d-191">W przypadku wyników zapytania toohello to oznacza, że hello określony punkt znajduje się w granice hello hello wirtualnego ogrodzenia, dlatego zostanie zwrócona `true`.</span><span class="sxs-lookup"><span data-stu-id="19f7d-191">If there are results toohello query, that means that hello specified point is within hello boundaries of hello geofence, so we return `true`.</span></span> <span data-ttu-id="19f7d-192">Jeśli nie są wyniki, Bing informuje NAS, czy punkt hello znajduje się poza hello wyszukiwania ramki, dlatego zostanie zwrócona `false`.</span><span class="sxs-lookup"><span data-stu-id="19f7d-192">If there are no results, Bing is telling us that hello point is outside hello lookup frame, so we return `false`.</span></span>

<span data-ttu-id="19f7d-193">W `NotificationsController.cs`, Utwórz operację sprawdzania przed instrukcji switch hello:</span><span class="sxs-lookup"><span data-stu-id="19f7d-193">Back in `NotificationsController.cs`, create a check right before hello switch statement:</span></span>

    if (ApiHelper.IsPointWithinBounds(longitude, latitude))
    {
        switch (pns.ToLower())
        {
            case "wns":
                //// Windows 8.1 / Windows Phone 8.1
                var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                // Windows 10 specific Action Center support
                toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                break;
        }
    }

<span data-ttu-id="19f7d-194">W ten sposób hello powiadomienie jest wysyłane wyłącznie po hello punkt znajduje się w granicach hello.</span><span class="sxs-lookup"><span data-stu-id="19f7d-194">That way, hello notification is only sent when hello point is within hello boundaries.</span></span>

## <a name="testing-push-notifications-in-hello-uwp-app"></a><span data-ttu-id="19f7d-195">Testowanie powiadomień wypychanych w aplikacji platformy uniwersalnej systemu Windows hello</span><span class="sxs-lookup"><span data-stu-id="19f7d-195">Testing push notifications in hello UWP app</span></span>
<span data-ttu-id="19f7d-196">Cofnięcie toohello aplikacji platformy uniwersalnej systemu Windows powinno być teraz możliwe tootest powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="19f7d-196">Going back toohello UWP app, we should now be able tootest notifications.</span></span> <span data-ttu-id="19f7d-197">W ramach hello `LocationHelper` klasy, Utwórz nową funkcję o nazwie `SendLocationToBackend`:</span><span class="sxs-lookup"><span data-stu-id="19f7d-197">Within hello `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

    public static async Task SendLocationToBackend(string pns, string userTag, string message, string latitude, string longitude)
    {
        var POST_URL = "http://localhost:8741/api/notifications?pns=" +
            pns + "&to_tag=" + userTag + "&latitude=" + latitude + "&longitude=" + longitude;

        using (var httpClient = new HttpClient())
        {
            try
            {
                await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                    System.Text.Encoding.UTF8, "application/json"));
            }
            catch (Exception ex)
            {
                Debug.WriteLine(ex.Message);
            }
        }
    }

> [!NOTE]
> <span data-ttu-id="19f7d-198">Zamień hello `POST_URL` toohello lokalizację użytkownika wdrożonej aplikacji sieci web utworzonej w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="19f7d-198">Swap hello `POST_URL` toohello location of your deployed web application that we created in hello previous section.</span></span> <span data-ttu-id="19f7d-199">Obecnie jest OK toorun ją lokalnie, ale podczas pracy nad wdrażania wersji publicznej, konieczne jest posiadanie toohost go przy użyciu zewnętrznego dostawcy.</span><span class="sxs-lookup"><span data-stu-id="19f7d-199">For now, it’s OK toorun it locally, but as you work on deploying a public version, you will need toohost it with an external provider.</span></span>
> 
> 

<span data-ttu-id="19f7d-200">Teraz upewnijmy się, że firma Microsoft zarejestrować aplikacji platformy uniwersalnej systemu Windows hello dla powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="19f7d-200">Let’s now make sure that we register hello UWP app for push notifications.</span></span> <span data-ttu-id="19f7d-201">W programie Visual Studio, kliknij **projektu** > **przechowywania** > **Skojarz aplikację ze sklepu hello**.</span><span class="sxs-lookup"><span data-stu-id="19f7d-201">In Visual Studio, click on **Project** > **Store** > **Associate app with hello store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="19f7d-202">Po zalogowaniu konta dewelopera tooyour upewnij się, wybierz istniejącą aplikację lub Utwórz nową i skojarzyć z nią hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="19f7d-202">Once you sign in tooyour developer account, make sure you select an existing app or create a new one and associate hello package with it.</span></span> 

<span data-ttu-id="19f7d-203">Przejdź toohello Centrum deweloperów i otwórz hello aplikację, która właśnie utworzony.</span><span class="sxs-lookup"><span data-stu-id="19f7d-203">Go toohello Dev Center and open hello app that you just created.</span></span> <span data-ttu-id="19f7d-204">Kliknij pozycję **Usługi** > **Powiadomienia wypychane** > **Witryna usług Live**.</span><span class="sxs-lookup"><span data-stu-id="19f7d-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="19f7d-205">W witrynie hello Zanotuj hello **klucz tajny aplikacji** i hello **identyfikatora SID pakietu**.</span><span class="sxs-lookup"><span data-stu-id="19f7d-205">On hello site, take note of hello **Application Secret** and hello **Package SID**.</span></span> <span data-ttu-id="19f7d-206">Konieczne będzie zarówno hello portalu Azure – Otwórz Centrum powiadomień, kliknij pozycję na **ustawienia** > **usługi powiadomień** > **systemu Windows (WNS)**i wprowadź informacje hello hello wymaganych pól.</span><span class="sxs-lookup"><span data-stu-id="19f7d-206">You will need both in hello Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter hello information in hello required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="19f7d-207">Kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="19f7d-207">Click on **Save**.</span></span>

<span data-ttu-id="19f7d-208">Kliknij prawym przyciskiem myszy pozycję **Odwołania** w **Eksploratorze rozwiązań** i wybierz pozycje **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="19f7d-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="19f7d-209">Firma Microsoft będzie tooadd toohello odwołania **biblioteki zarządzanej usługi Microsoft Azure Service Bus** — po prostu wyszukaj `WindowsAzure.Messaging.Managed` i dodaj go tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="19f7d-209">We will need tooadd a reference toohello **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it tooyour project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="19f7d-210">Do celów testowych, możemy utworzyć hello `MainPage_Loaded` jeszcze raz program obsługi zdarzeń i Dodaj ten tooit fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="19f7d-210">For testing purposes, we can create hello `MainPage_Loaded` event handler once again, and add this code snippet tooit:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="19f7d-211">Witaj powyżej rejestruje aplikacji hello hello Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="19f7d-211">hello above registers hello app with hello notification hub.</span></span> <span data-ttu-id="19f7d-212">Jesteś toogo gotowe!</span><span class="sxs-lookup"><span data-stu-id="19f7d-212">You are ready toogo!</span></span> 

<span data-ttu-id="19f7d-213">W `LocationHelper`, wewnątrz hello `Geolocator_PositionChanged` obsługi, można dodać fragment kodu, który będzie wymuszać umieszczanie lokalizacji hello w wirtualnym ogrodzeniu hello:</span><span class="sxs-lookup"><span data-stu-id="19f7d-213">In `LocationHelper`, inside hello `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put hello location inside hello geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="19f7d-214">Ponieważ firma Microsoft nie są używane hello rzeczywiste współrzędne (które może nie być w granicach hello w chwili hello) i jest używany wstępnie zdefiniowane wartości testowe, zostanie wyświetlone powiadomienie po aktualizacji:</span><span class="sxs-lookup"><span data-stu-id="19f7d-214">Because we are not passing hello real coordinates (which might not be within hello boundaries at hello moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="19f7d-215">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="19f7d-215">What’s next?</span></span>
<span data-ttu-id="19f7d-216">Istnieje kilka kroków trzeba toofollow w toohello dodanie powyżej toomake się, że rozwiązanie hello jest gotowe do produkcji.</span><span class="sxs-lookup"><span data-stu-id="19f7d-216">There are a couple of steps that you might need toofollow in addition toohello above toomake sure that hello solution is production-ready.</span></span>

<span data-ttu-id="19f7d-217">Najpierw i, może być konieczne tooensure, że wirtualne ogrodzenia są dynamiczne.</span><span class="sxs-lookup"><span data-stu-id="19f7d-217">First and foremost, you might need tooensure that geofences are dynamic.</span></span> <span data-ttu-id="19f7d-218">Będzie to wymagało dodatkowej pracy z hello interfejsu API Bing w kolejności toobe stanie tooupload nowych granic w ramach hello istniejącego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="19f7d-218">This will require some extra work with hello Bing API in order toobe able tooupload new boundaries within hello existing data source.</span></span> <span data-ttu-id="19f7d-219">Zapoznaj się hello [dokumentacji interfejsu API Bing przestrzennych danych usługi](https://msdn.microsoft.com/library/ff701734.aspx) Aby uzyskać więcej informacji na temat hello.</span><span class="sxs-lookup"><span data-stu-id="19f7d-219">Consult hello [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on hello subject.</span></span>

<span data-ttu-id="19f7d-220">Po drugie, jako że dostarczania hello odbywa się toohello odpowiednich uczestników tooensure pracy można tootarget ich za pośrednictwem [znakowanie](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="19f7d-220">Second, as you are working tooensure that hello delivery is done toohello right participants, you might want tootarget them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="19f7d-221">w powyższym rozwiązaniu Hello opisano scenariusz, mogą mieć różnych platform docelowych, dlatego nie ograniczono możliwości specyficznych dla toosystem geofencing hello.</span><span class="sxs-lookup"><span data-stu-id="19f7d-221">hello solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit hello geofencing toosystem-specific capabilities.</span></span> <span data-ttu-id="19f7d-222">Inaczej mówiąc, hello platformy uniwersalnej systemu Windows oferuje możliwości zbyt[wykryć wirtualne ogrodzenia prawo out-of--box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span><span class="sxs-lookup"><span data-stu-id="19f7d-222">That said, hello Universal Windows Platform offers capabilities too[detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="19f7d-223">Aby uzyskać więcej informacji o możliwościach usługi Notification Hubs, odwiedź [portal dokumentacji](https://azure.microsoft.com/documentation/services/notification-hubs/).</span><span class="sxs-lookup"><span data-stu-id="19f7d-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>

