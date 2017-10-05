---
title: "Wirtualne grodzenie powiadomień wypychanych przy użyciu usług Azure Notification Hubs i Bing Spatial Data | Microsoft Docs"
description: "Korzystając z tego samouczka, dowiesz się, jak dostarczać powiadomienia wypychane oparte na lokalizacji przy użyciu usług Azure Notification Hubs i Bing Spatial Data."
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
ms.openlocfilehash: b2a84e0479aac9ded08bb64e1ea20ddee6636cce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="97ba6-104">Wirtualne grodzenie powiadomień wypychanych przy użyciu usług Azure Notification Hubs i Bing Spatial Data</span><span class="sxs-lookup"><span data-stu-id="97ba6-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="97ba6-105">Do wykonania kroków tego samouczka potrzebne jest aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="97ba6-105">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="97ba6-106">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="97ba6-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="97ba6-107">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span><span class="sxs-lookup"><span data-stu-id="97ba6-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="97ba6-108">Korzystając z tego samouczka, dowiesz się, jak dostarczać powiadomienia wypychane oparte na lokalizacji przy użyciu usług Azure Notification Hubs i Bing Spatial Data z wykorzystaniem aplikacji platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="97ba6-108">In this tutorial, you will learn how to deliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97ba6-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="97ba6-109">Prerequisites</span></span>
<span data-ttu-id="97ba6-110">Najpierw upewnij się, że spełniono wszystkie wymagania wstępne dotyczące oprogramowania i usług:</span><span class="sxs-lookup"><span data-stu-id="97ba6-110">First and foremost, you need to make sure that you have all the software and service pre-requisites:</span></span>

* <span data-ttu-id="97ba6-111">Program [Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) lub nowszy (można również użyć wersji [Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409)).</span><span class="sxs-lookup"><span data-stu-id="97ba6-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="97ba6-112">Najnowsza wersja zestawu [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="97ba6-112">Latest version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="97ba6-113">[Konto Centrum deweloperów Map Bing](https://www.bingmapsportal.com/) (można utworzyć je bezpłatnie i skojarzyć z kontem Microsoft).</span><span class="sxs-lookup"><span data-stu-id="97ba6-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="97ba6-114">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="97ba6-114">Getting Started</span></span>
<span data-ttu-id="97ba6-115">Zacznijmy od utworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="97ba6-115">Let’s start by creating the project.</span></span> <span data-ttu-id="97ba6-116">W programie Visual Studio utwórz nowy projekt typu **Pusta aplikacja (uniwersalna aplikacja systemu Windows)**.</span><span class="sxs-lookup"><span data-stu-id="97ba6-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="97ba6-117">Po zakończeniu tworzenia projektu uzyskasz dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97ba6-117">Once the project creation is complete, you should have the harness for the app itself.</span></span> <span data-ttu-id="97ba6-118">Teraz skonfigurujmy wszystko pod kątem infrastruktury wirtualnego grodzenia.</span><span class="sxs-lookup"><span data-stu-id="97ba6-118">Now let’s set up everything for the geo-fencing infrastructure.</span></span> <span data-ttu-id="97ba6-119">Ponieważ w tym celu użyjemy usług Bing, istnieje publiczny punkt końcowy interfejsu API REST umożliwiający wykonywanie zapytań dotyczących określonego zakresu lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="97ba6-119">Because we are going to use Bing services for this, there is a public REST API endpoint that allows us to query specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="97ba6-120">Należy określić następujące parametry, aby przygotować go do pracy:</span><span class="sxs-lookup"><span data-stu-id="97ba6-120">You will need to specify the following parameters to get it working:</span></span>

* <span data-ttu-id="97ba6-121">**Identyfikator źródła danych** i **Nazwa źródła danych** — w interfejsie API Map Bing źródła danych zawierają różne metadane w zasobnikach, takie jak lokalizacje i godziny pracy.</span><span class="sxs-lookup"><span data-stu-id="97ba6-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="97ba6-122">Możesz uzyskać więcej informacji na ten temat tutaj.</span><span class="sxs-lookup"><span data-stu-id="97ba6-122">You can read more about those here.</span></span> 
* <span data-ttu-id="97ba6-123">**Nazwa jednostki** — jednostka, która ma być używana jako punkt odniesienia dla powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="97ba6-123">**Entity Name** – the entity you want to use as a reference point for the notification.</span></span> 
* <span data-ttu-id="97ba6-124">**Klucz interfejsu API Map Bing** — to jest klucz uzyskany wcześniej podczas tworzenia konta Centrum deweloperów Bing.</span><span class="sxs-lookup"><span data-stu-id="97ba6-124">**Bing Maps API Key** – this is the key that you obtained earlier when you created the Bing Dev Center account.</span></span>

<span data-ttu-id="97ba6-125">Poznajmy szczegółowo sposób konfiguracji poszczególnych elementów wymienionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="97ba6-125">Let’s do a deep-dive on the setup for each of the elements above.</span></span>

## <a name="setting-up-the-data-source"></a><span data-ttu-id="97ba6-126">Konfigurowanie źródła danych</span><span class="sxs-lookup"><span data-stu-id="97ba6-126">Setting up the data source</span></span>
<span data-ttu-id="97ba6-127">W tym celu można użyć Centrum deweloperów Map Bing.</span><span class="sxs-lookup"><span data-stu-id="97ba6-127">You can do it in the Bing Maps Dev Center.</span></span> <span data-ttu-id="97ba6-128">Kliknij pozycję **Źródła danych** na górnym pasku nawigacyjnym i wybierz pozycję **Zarządzaj źródłami danych**.</span><span class="sxs-lookup"><span data-stu-id="97ba6-128">Simply click on **Data sources** in the top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="97ba6-129">Jeśli wcześniej nie korzystano z interfejsu API Map Bing, prawdopodobnie nie będą istnieć żadne źródła danych, dlatego możesz utworzyć nowe, klikając pozycję Przekaż dane do źródła danych.</span><span class="sxs-lookup"><span data-stu-id="97ba6-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data to a data source.</span></span> <span data-ttu-id="97ba6-130">Wypełnij wszystkie wymagane pola:</span><span class="sxs-lookup"><span data-stu-id="97ba6-130">Make sure you fill out all the required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="97ba6-131">Możliwe, że zastanawiasz się, co to jest plik danych i co należy przekazać?</span><span class="sxs-lookup"><span data-stu-id="97ba6-131">You might be wondering – what is the data file and what should you be uploading?</span></span> <span data-ttu-id="97ba6-132">Na potrzeby tego testu możemy użyć przykładowego pliku opartego na potoku, który określa obszar nabrzeża San Francisco:</span><span class="sxs-lookup"><span data-stu-id="97ba6-132">For the purposes of this test, we can just use the sample pipe-based that frames an area of the San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="97ba6-133">Powyższy kod reprezentuje następującą jednostkę:</span><span class="sxs-lookup"><span data-stu-id="97ba6-133">The above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="97ba6-134">Po prostu skopiuj i wklej powyższy ciąg do nowego pliku i zapisz go jako **NotificationHubsGeofence.pipe**, a następnie przekaż go do Centrum deweloperów Bing.</span><span class="sxs-lookup"><span data-stu-id="97ba6-134">Simply copy and paste the string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in the Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="97ba6-135">Może zostać wyświetlony monit o określenie nowego klucza dla właściwości **Klucz główny**, który różni się od właściwości **Klucz zapytania**.</span><span class="sxs-lookup"><span data-stu-id="97ba6-135">You might be prompted to specify a new key for the **Master Key** that is different from the **Query Key**.</span></span> <span data-ttu-id="97ba6-136">Po prostu utwórz nowy klucz przy użyciu pulpitu nawigacyjnego i odśwież stronę przekazywania źródła danych.</span><span class="sxs-lookup"><span data-stu-id="97ba6-136">Simply create a new key through the dashboard and refresh the data source upload page.</span></span>
> 
> 

<span data-ttu-id="97ba6-137">Po przekazaniu pliku danych opublikuj źródło danych.</span><span class="sxs-lookup"><span data-stu-id="97ba6-137">Once you upload the data file, you will need to make sure that you publish the data source.</span></span> 

<span data-ttu-id="97ba6-138">Przejdź do obszaru **Zarządzanie źródłami danych**, jak opisano powyżej, znajdź źródło danych na liście i kliknij polecenie **Publikuj** w kolumnie **Akcje**.</span><span class="sxs-lookup"><span data-stu-id="97ba6-138">Go to **Manage Data Sources**, just like we did above, find your data source in the list and click on **Publish** in the **Actions** column.</span></span> <span data-ttu-id="97ba6-139">Po chwili źródło danych powinno zostać wyświetlone na karcie **Opublikowane źródła danych**:</span><span class="sxs-lookup"><span data-stu-id="97ba6-139">In a bit, you should see your data source in the **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="97ba6-140">Jeśli klikniesz pozycję **Edytuj** możesz łatwo przeglądać wprowadzone lokalizacje:</span><span class="sxs-lookup"><span data-stu-id="97ba6-140">If you click **Edit**, you will be able to see at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="97ba6-141">W tym momencie w portalu nie są wyświetlane granice utworzonego wirtualnego ogrodzenia — potrzebne jest jedynie potwierdzenie, że określona lokalizacja znajduje się w odpowiedniej okolicy.</span><span class="sxs-lookup"><span data-stu-id="97ba6-141">At this point, the portal does not show you the boundaries for the geofence that we created – all we need is a confirmation that the location specified is in the right vicinity.</span></span>

<span data-ttu-id="97ba6-142">Teraz wszystkie wymagania dotyczące źródła danych zostały spełnione.</span><span class="sxs-lookup"><span data-stu-id="97ba6-142">Now you have all the requirements for the data source.</span></span> <span data-ttu-id="97ba6-143">Aby uzyskać szczegółowe informacje dotyczące adresu URL żądania dla wywołania interfejsu API, w Centrum deweloperów Map Bing kliknij pozycję **Źródła danych** i wybierz pozycję **Informacje o źródle danych**.</span><span class="sxs-lookup"><span data-stu-id="97ba6-143">To get the details on the request URL for the API call, in the Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="97ba6-144">Interesuje nas tutaj wartość właściwości **Adres URL zapytania**.</span><span class="sxs-lookup"><span data-stu-id="97ba6-144">The **Query URL** is what we’re after here.</span></span> <span data-ttu-id="97ba6-145">To jest punkt końcowy, względem którego możemy wykonywać zapytania, aby sprawdzić, czy urządzenie znajduje się obecnie w granicach lokalizacji, czy nie.</span><span class="sxs-lookup"><span data-stu-id="97ba6-145">This is the endpoint against which we can execute queries to check whether the device is currently within the boundaries of a location or not.</span></span> <span data-ttu-id="97ba6-146">Aby to sprawdzić, należy wykonać wywołanie GET dla adresu URL zapytania z dołączonymi następującymi parametrami:</span><span class="sxs-lookup"><span data-stu-id="97ba6-146">To perform this check, we simply need to execute a GET call against the query URL, with the following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="97ba6-147">W ten sposób określisz punkt docelowy uzyskany z urządzenia, a Mapy Bing automatycznie wykonają obliczenia w celu sprawdzenia, czy znajduje się on w wirtualnym ogrodzeniu.</span><span class="sxs-lookup"><span data-stu-id="97ba6-147">That way you're specifying a target point that we obtain from the device and Bing Maps will automatically perform the calculations to see whether it is within the geofence.</span></span> <span data-ttu-id="97ba6-148">Po wykonaniu żądania przy użyciu przeglądarki (lub programu cURL), uzyskasz standardową odpowiedź w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="97ba6-148">Once you execute the request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="97ba6-149">Ta odpowiedź jest wysyłana tylko wtedy, gdy punkt rzeczywiście znajduje się w wyznaczonych granicach.</span><span class="sxs-lookup"><span data-stu-id="97ba6-149">This response only happens when the point is actually within the designated boundaries.</span></span> <span data-ttu-id="97ba6-150">W przeciwnym razie otrzymasz pusty zasobnik **results**:</span><span class="sxs-lookup"><span data-stu-id="97ba6-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-the-uwp-application"></a><span data-ttu-id="97ba6-151">Konfigurowanie aplikacji platformy uniwersalnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="97ba6-151">Setting up the UWP application</span></span>
<span data-ttu-id="97ba6-152">Teraz, gdy źródło danych jest gotowe, możemy rozpocząć pracę nad aplikacją platformy uniwersalnej systemu Windows, którą zainicjowano wcześniej.</span><span class="sxs-lookup"><span data-stu-id="97ba6-152">Now that we have the data source ready, we can start working on the UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="97ba6-153">Najpierw musimy włączyć usługi lokalizacji dla naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97ba6-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="97ba6-154">W tym celu kliknij dwukrotnie plik `Package.appxmanifest` w **Eksploratorze rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="97ba6-154">To do this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="97ba6-155">Na karcie właściwości pakietu, która została otwarta, kliknij pozycję **Możliwości** i wybierz pozycję **Lokalizacja**:</span><span class="sxs-lookup"><span data-stu-id="97ba6-155">In the package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="97ba6-156">Po zadeklarowaniu możliwości korzystania z lokalizacji utwórz nowy folder w rozwiązaniu o nazwie `Core` i dodaj do niego nowy plik o nazwie `LocationHelper.cs`:</span><span class="sxs-lookup"><span data-stu-id="97ba6-156">As the location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="97ba6-157">Klasa `LocationHelper` jest obecnie dosyć prosta — umożliwia jedynie uzyskiwanie lokalizacji użytkownika przy użyciu interfejsu API systemu:</span><span class="sxs-lookup"><span data-stu-id="97ba6-157">The `LocationHelper` class itself is fairly basic at this point – all it does is allow us to obtain the user location through the system API:</span></span>

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

<span data-ttu-id="97ba6-158">Więcej informacji o uzyskiwaniu lokalizacji użytkownika w aplikacjach platformy uniwersalnej systemu Windows można uzyskać w oficjalnym [dokumencie MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span><span class="sxs-lookup"><span data-stu-id="97ba6-158">You can read more about getting the user’s location in UWP apps in the official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="97ba6-159">Aby sprawdzić, czy uzyskiwanie lokalizacji rzeczywiście działa, otwórz stronę kodu strony głównej (`MainPage.xaml.cs`).</span><span class="sxs-lookup"><span data-stu-id="97ba6-159">To check that the location acquisition is actually working, open the code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="97ba6-160">Utwórz nowy program obsługi zdarzeń dla zdarzenia `Loaded` w konstruktorze `MainPage`:</span><span class="sxs-lookup"><span data-stu-id="97ba6-160">Create a new event handler for the `Loaded` event in the `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="97ba6-161">Implementacja programu obsługi zdarzeń wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="97ba6-161">The implementation of the event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="97ba6-162">Zwróć uwagę, że program obsługi został zadeklarowany jako asynchroniczny, ponieważ metoda `GetCurrentLocation` obsługuje instrukcję await, dlatego wymaga wykonywania w kontekście asynchronicznym.</span><span class="sxs-lookup"><span data-stu-id="97ba6-162">Notice that we declared the handler as async because `GetCurrentLocation` is awaitable, and therefore requires to be executed in an async context.</span></span> <span data-ttu-id="97ba6-163">Ponadto w pewnych okolicznościach możemy uzyskać lokalizację o wartości null (np. usługi lokalizacji zostały wyłączone lub aplikacji odmówiono uprawnień do uzyskiwania dostępu do lokalizacji), dlatego musimy upewnić się, że zapewniona jest prawidłowa obsługa przy użyciu sprawdzania wartości null.</span><span class="sxs-lookup"><span data-stu-id="97ba6-163">Also, because under certain circumstances we might end up with a null location (e.g. the location services are disabled or the application was denied permissions to access location), we need to make sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="97ba6-164">Uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="97ba6-164">Run the application.</span></span> <span data-ttu-id="97ba6-165">Zezwól na dostęp do lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="97ba6-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="97ba6-166">Po uruchomieniu aplikacji współrzędne powinny być widoczne w oknie **Dane wyjściowe**:</span><span class="sxs-lookup"><span data-stu-id="97ba6-166">Once the application launches, you should be able to see the coordinates in the **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="97ba6-167">Teraz wiesz, że pobieranie lokalizacji działa. Możesz usunąć testowy program obsługi zdarzeń Loaded, ponieważ nie będzie już używany.</span><span class="sxs-lookup"><span data-stu-id="97ba6-167">Now you know that location acquisition works – feel free to remove the test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="97ba6-168">Następnym krokiem jest przechwytywanie zmian lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="97ba6-168">The next step is to capture location changes.</span></span> <span data-ttu-id="97ba6-169">W tym celu wróć do klasy `LocationHelper` i dodaj program obsługi zdarzeń `PositionChanged`:</span><span class="sxs-lookup"><span data-stu-id="97ba6-169">For that, let’s go back to the `LocationHelper` class and add the event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="97ba6-170">Implementacja spowoduje wyświetlenie współrzędnych lokalizacji w oknie **Dane wyjściowe**:</span><span class="sxs-lookup"><span data-stu-id="97ba6-170">The implementation will show the location coordinates in the **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-the-backend"></a><span data-ttu-id="97ba6-171">Konfigurowanie zaplecza</span><span class="sxs-lookup"><span data-stu-id="97ba6-171">Setting up the backend</span></span>
<span data-ttu-id="97ba6-172">Pobierz [przykład zaplecza programu .NET z usługi GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="97ba6-172">Download the [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="97ba6-173">Po zakończeniu pobierania otwórz folder `NotifyUsers`, a następnie otwórz plik `NotifyUsers.sln`.</span><span class="sxs-lookup"><span data-stu-id="97ba6-173">Once the download completes, open the `NotifyUsers` folder, and subsequently – the `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="97ba6-174">Ustaw projekt `AppBackend` jako **Projekt startowy**, a następnie uruchom go.</span><span class="sxs-lookup"><span data-stu-id="97ba6-174">Set the `AppBackend` project as the **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="97ba6-175">Projekt jest już skonfigurowany do wysyłania powiadomień wypychanych do urządzeń docelowych, dlatego musimy wykonać tylko dwie czynności — zmienić parametry połączenia na odpowiednie dla centrum powiadomień i dodać identyfikację granic, aby powiadomienie było wysyłane tylko wtedy, gdy użytkownik znajduje się w wirtualnym ogrodzeniu.</span><span class="sxs-lookup"><span data-stu-id="97ba6-175">The project is already configured to send push notifications to target devices, so we’ll need to do only two things – swap out the right connection string for the notification hub and add boundary identification to send the notification only when the user is within the geofence.</span></span>

<span data-ttu-id="97ba6-176">Aby skonfigurować parametry połączenia, w folderze `Models` otwórz plik `Notifications.cs`.</span><span class="sxs-lookup"><span data-stu-id="97ba6-176">To configure the connection string, in the `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="97ba6-177">Funkcja `NotificationHubClient.CreateClientFromConnectionString` powinna zawierać informacje o centrum powiadomień uzyskane w witrynie [Azure Portal](https://portal.azure.com) (w bloku **Zasady dostępu** w obszarze **Ustawienia**).</span><span class="sxs-lookup"><span data-stu-id="97ba6-177">The `NotificationHubClient.CreateClientFromConnectionString` function should contain the information about your notification hub that you can get in the [Azure Portal](https://portal.azure.com) (look inside the **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="97ba6-178">Zapisz zaktualizowany plik konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="97ba6-178">Save the updated configuration file.</span></span>

<span data-ttu-id="97ba6-179">Teraz należy utworzyć model dla wyniku interfejsu API Map Bing.</span><span class="sxs-lookup"><span data-stu-id="97ba6-179">Now we need to create a model for the Bing Maps API result.</span></span> <span data-ttu-id="97ba6-180">W tym celu najłatwiej kliknąć prawym przyciskiem myszy folder `Models`, a następnie polecenie **Dodaj** > **Klasa**.</span><span class="sxs-lookup"><span data-stu-id="97ba6-180">The easiest way to do that is right-click on the `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="97ba6-181">Nadaj jej nazwę `GeofenceBoundary.cs`.</span><span class="sxs-lookup"><span data-stu-id="97ba6-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="97ba6-182">Po zakończeniu skopiuj kod JSON z odpowiedzi interfejsu API omówionej w pierwszej sekcji, a następnie w programie Visual Studio użyj polecenia **Edytuj** > **Wklej specjalne** > **Wklej dane JSON jako klasy**.</span><span class="sxs-lookup"><span data-stu-id="97ba6-182">Once done, copy the JSON from the API response that we discussed in the first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="97ba6-183">W ten sposób upewniamy się, że obiekt zostanie zdeserializowany dokładnie w zamierzony sposób.</span><span class="sxs-lookup"><span data-stu-id="97ba6-183">That way we ensure that the object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="97ba6-184">Wynikowy zestaw klas powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="97ba6-184">Your resulting class set should resemble this:</span></span>

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

<span data-ttu-id="97ba6-185">Następnie otwórz plik `Controllers` > `NotificationsController.cs`.</span><span class="sxs-lookup"><span data-stu-id="97ba6-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="97ba6-186">Musimy dostosować wywołanie metody POST, aby uwzględnić docelową długość i szerokość geograficzną.</span><span class="sxs-lookup"><span data-stu-id="97ba6-186">We need to tweak the Post call to account for the target longitude and latitude.</span></span> <span data-ttu-id="97ba6-187">W tym celu po prostu dodaj dwa ciągi do sygnatury funkcji — `latitude` i `longitude`.</span><span class="sxs-lookup"><span data-stu-id="97ba6-187">For that, simply add two strings to the function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="97ba6-188">Utwórz nową klasę w projekcie o nazwie `ApiHelper.cs`. Zostanie ona użyta do połączenia z usługą Bing w celu sprawdzenia puntów przecięcia granic.</span><span class="sxs-lookup"><span data-stu-id="97ba6-188">Create a new class within the project called `ApiHelper.cs` – we’ll use it to connect to Bing to check point boundary intersections.</span></span> <span data-ttu-id="97ba6-189">Zaimplementuj funkcję `IsPointWithinBounds` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="97ba6-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

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
> <span data-ttu-id="97ba6-190">Zastąp punkt końcowy interfejsu API adresem URL zapytania uzyskanym wcześniej z Centrum deweloperów Bing (to samo dotyczy klucza interfejsu API).</span><span class="sxs-lookup"><span data-stu-id="97ba6-190">Make sure to substitute the API endpoint with the query URL that you obtained earlier from the Bing Dev Center (same applies to the API key).</span></span> 
> 
> 

<span data-ttu-id="97ba6-191">Jeśli uzyskano wyniki zapytania, oznacza to, że określony punkt znajduje się w granicach wirtualnego ogrodzenia, dlatego zostanie zwrócona wartość `true`.</span><span class="sxs-lookup"><span data-stu-id="97ba6-191">If there are results to the query, that means that the specified point is within the boundaries of the geofence, so we return `true`.</span></span> <span data-ttu-id="97ba6-192">Jeśli nie ma wyników, usługa Bing informuje nas, że punkt znajduje się poza obszarem wyszukiwania, dlatego zostanie zwrócona wartość `false`.</span><span class="sxs-lookup"><span data-stu-id="97ba6-192">If there are no results, Bing is telling us that the point is outside the lookup frame, so we return `false`.</span></span>

<span data-ttu-id="97ba6-193">W pliku `NotificationsController.cs` utwórz operację sprawdzania przed instrukcją switch:</span><span class="sxs-lookup"><span data-stu-id="97ba6-193">Back in `NotificationsController.cs`, create a check right before the switch statement:</span></span>

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

<span data-ttu-id="97ba6-194">W ten sposób powiadomienia będą wysyłane tylko wtedy, gdy punkt znajduje się w granicach.</span><span class="sxs-lookup"><span data-stu-id="97ba6-194">That way, the notification is only sent when the point is within the boundaries.</span></span>

## <a name="testing-push-notifications-in-the-uwp-app"></a><span data-ttu-id="97ba6-195">Testowanie powiadomień wypychanych w aplikacji platformy uniwersalnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="97ba6-195">Testing push notifications in the UWP app</span></span>
<span data-ttu-id="97ba6-196">Po powrocie do aplikacji platformy uniwersalnej systemu Windows powinno być teraz możliwe przetestowanie powiadomień.</span><span class="sxs-lookup"><span data-stu-id="97ba6-196">Going back to the UWP app, we should now be able to test notifications.</span></span> <span data-ttu-id="97ba6-197">W klasie `LocationHelper` utwórz nową funkcję o nazwie `SendLocationToBackend`:</span><span class="sxs-lookup"><span data-stu-id="97ba6-197">Within the `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

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
> <span data-ttu-id="97ba6-198">Zastąp wartość zmiennej `POST_URL` lokalizacją wdrożonej aplikacji sieci Web utworzonej w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="97ba6-198">Swap the `POST_URL` to the location of your deployed web application that we created in the previous section.</span></span> <span data-ttu-id="97ba6-199">Teraz możesz uruchomić aplikację lokalnie, ale podczas wdrażania wersji publicznej należy skorzystać z hostingu zewnętrznego dostawcy.</span><span class="sxs-lookup"><span data-stu-id="97ba6-199">For now, it’s OK to run it locally, but as you work on deploying a public version, you will need to host it with an external provider.</span></span>
> 
> 

<span data-ttu-id="97ba6-200">Teraz zarejestrujmy aplikację platformy uniwersalnej systemu Windows na potrzeby powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="97ba6-200">Let’s now make sure that we register the UWP app for push notifications.</span></span> <span data-ttu-id="97ba6-201">W programie Visual Studio kliknij pozycję **Projekt** > **Magazyn** > **Skojarz aplikację z magazynem**.</span><span class="sxs-lookup"><span data-stu-id="97ba6-201">In Visual Studio, click on **Project** > **Store** > **Associate app with the store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="97ba6-202">Po zalogowaniu się do konta dewelopera wybierz istniejącą aplikację lub utwórz nową i skojarz z nią pakiet.</span><span class="sxs-lookup"><span data-stu-id="97ba6-202">Once you sign in to your developer account, make sure you select an existing app or create a new one and associate the package with it.</span></span> 

<span data-ttu-id="97ba6-203">Przejdź do Centrum deweloperów i otwórz utworzoną wcześniej aplikację.</span><span class="sxs-lookup"><span data-stu-id="97ba6-203">Go to the Dev Center and open the app that you just created.</span></span> <span data-ttu-id="97ba6-204">Kliknij pozycję **Usługi** > **Powiadomienia wypychane** > **Witryna usług Live**.</span><span class="sxs-lookup"><span data-stu-id="97ba6-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="97ba6-205">W witrynie zanotuj **Klucz tajny aplikacji** i **Identyfikator SID pakietu**.</span><span class="sxs-lookup"><span data-stu-id="97ba6-205">On the site, take note of the **Application Secret** and the **Package SID**.</span></span> <span data-ttu-id="97ba6-206">Obie wartości będą potrzebne w witrynie Azure Portal. Otwórz centrum powiadomień, kliknij pozycję **Ustawienia** > **Usługi powiadomień** > **Windows (WNS)** i wprowadź informacje w wymaganych polach.</span><span class="sxs-lookup"><span data-stu-id="97ba6-206">You will need both in the Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter the information in the required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="97ba6-207">Kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="97ba6-207">Click on **Save**.</span></span>

<span data-ttu-id="97ba6-208">Kliknij prawym przyciskiem myszy pozycję **Odwołania** w **Eksploratorze rozwiązań** i wybierz pozycje **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="97ba6-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="97ba6-209">Musimy dodać odwołanie do **biblioteki zarządzanej usługi Microsoft Azure Service Bus**. Wyszukaj pakiet `WindowsAzure.Messaging.Managed` i dodaj go do projektu.</span><span class="sxs-lookup"><span data-stu-id="97ba6-209">We will need to add a reference to the **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it to your project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="97ba6-210">W celach testowych możemy ponownie utworzyć program obsługi zdarzeń `MainPage_Loaded` i dodać do niego następujący fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="97ba6-210">For testing purposes, we can create the `MainPage_Loaded` event handler once again, and add this code snippet to it:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays the registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="97ba6-211">Powyższy kod rejestruje aplikację w centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="97ba6-211">The above registers the app with the notification hub.</span></span> <span data-ttu-id="97ba6-212">Gotowe!</span><span class="sxs-lookup"><span data-stu-id="97ba6-212">You are ready to go!</span></span> 

<span data-ttu-id="97ba6-213">W elemencie `LocationHelper` w programie obsługi `Geolocator_PositionChanged` możesz dodać fragment kodu, który będzie wymuszać umieszczanie lokalizacji w wirtualnym ogrodzeniu:</span><span class="sxs-lookup"><span data-stu-id="97ba6-213">In `LocationHelper`, inside the `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put the location inside the geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="97ba6-214">Ponieważ nie są używane rzeczywiste współrzędne (które mogą obecnie znajdować się poza granicami), lecz wstępnie zdefiniowane wartości testowe, po aktualizacji zostanie wyświetlone powiadomienie:</span><span class="sxs-lookup"><span data-stu-id="97ba6-214">Because we are not passing the real coordinates (which might not be within the boundaries at the moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="97ba6-215">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="97ba6-215">What’s next?</span></span>
<span data-ttu-id="97ba6-216">Istnieje kilka kroków, których wykonanie może być konieczne, oprócz przedstawionych powyżej, aby upewnić się, że rozwiązanie jest gotowe do zastosowania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="97ba6-216">There are a couple of steps that you might need to follow in addition to the above to make sure that the solution is production-ready.</span></span>

<span data-ttu-id="97ba6-217">Najpierw należy upewnić się, że wirtualne ogrodzenia są dynamiczne.</span><span class="sxs-lookup"><span data-stu-id="97ba6-217">First and foremost, you might need to ensure that geofences are dynamic.</span></span> <span data-ttu-id="97ba6-218">To wymaga dodatkowej pracy z interfejsem API Bing w celu umożliwienia przekazywania nowych granic w ramach istniejącego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="97ba6-218">This will require some extra work with the Bing API in order to be able to upload new boundaries within the existing data source.</span></span> <span data-ttu-id="97ba6-219">Aby uzyskać więcej informacji na ten temat, zapoznaj się z [dokumentacją interfejsu API usług Bing Spatial Data Services](https://msdn.microsoft.com/library/ff701734.aspx).</span><span class="sxs-lookup"><span data-stu-id="97ba6-219">Consult the [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on the subject.</span></span>

<span data-ttu-id="97ba6-220">Upewniając się, że powiadomienia są dostarczane do odpowiednich uczestników, warto adresować je przy użyciu [tagów](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="97ba6-220">Second, as you are working to ensure that the delivery is done to the right participants, you might want to target them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="97ba6-221">W powyższym rozwiązaniu opisano scenariusz, w którym może występować wiele różnych platform, dlatego nie ograniczono wirtualnego grodzenia do możliwości specyficznych dla określonego systemu.</span><span class="sxs-lookup"><span data-stu-id="97ba6-221">The solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit the geofencing to system-specific capabilities.</span></span> <span data-ttu-id="97ba6-222">Jednak platforma uniwersalna systemu Windows oferuje wbudowane możliwości [wykrywania wirtualnych ogrodzeń](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span><span class="sxs-lookup"><span data-stu-id="97ba6-222">That said, the Universal Windows Platform offers capabilities to [detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="97ba6-223">Aby uzyskać więcej informacji o możliwościach usługi Notification Hubs, odwiedź [portal dokumentacji](https://azure.microsoft.com/documentation/services/notification-hubs/).</span><span class="sxs-lookup"><span data-stu-id="97ba6-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>

