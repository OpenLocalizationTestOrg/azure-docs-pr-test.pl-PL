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
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a>Wirtualne grodzenie powiadomień wypychanych przy użyciu usług Azure Notification Hubs i Bing Spatial Data
> [!NOTE]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).
> 
> 

Z tego samouczka dowiesz się, jak toodeliver oparte na lokalizacji wypychanie powiadomień przy użyciu usługi Azure Notification Hubs i Bing Spatial Data z wykorzystaniem aplikacji platformy uniwersalnej systemu Windows.

## <a name="prerequisites"></a>Wymagania wstępne
Najpierw i, należy upewnić się, że wszystkie hello oprogramowania i usług wstępne toomake:

* Program [Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) lub nowszy (można również użyć wersji [Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409)). 
* Najnowszą wersję hello [zestawu Azure SDK](https://azure.microsoft.com/downloads/). 
* [Konto Centrum deweloperów Map Bing](https://www.bingmapsportal.com/) (można utworzyć je bezpłatnie i skojarzyć z kontem Microsoft). 

## <a name="getting-started"></a>Wprowadzenie
Zacznijmy od utworzenia projektu hello. W programie Visual Studio utwórz nowy projekt typu **Pusta aplikacja (uniwersalna aplikacja systemu Windows)**.

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

Po zakończeniu tworzenia projektu hello powinien mieć kontroler powitania dla aplikacji hello. Teraz Skonfigurujmy wszystko pod kątem infrastruktury wirtualnego grodzenia hello. Ponieważ firma Microsoft będzie toouse, które usługi Bing dla tego, istnieje publiczny punkt końcowy interfejsu API REST, który pozwala nam tooquery określonego zakresu lokalizacji:

    http://spatial.virtualearth.net/REST/v1/data/

Konieczne będzie toospecify hello następujące parametry tooget go do pracy:

* **Identyfikator źródła danych** i **Nazwa źródła danych** — w interfejsie API Map Bing źródła danych zawierają różne metadane w zasobnikach, takie jak lokalizacje i godziny pracy. Możesz uzyskać więcej informacji na ten temat tutaj. 
* **Nazwa jednostki** — Witaj jednostki, której toouse jako punkt odniesienia dla powiadomienia hello. 
* **Klucz interfejsu API map Bing** — jest to hello klucz uzyskany wcześniej podczas tworzenia konta Centrum deweloperów Bing hello.

Dla każdego z powyższych elementów hello Poznajmy szczegółowo na powitania instalacji.

## <a name="setting-up-hello-data-source"></a>Konfigurowanie hello źródła danych
Możesz zrobić to w hello Centrum deweloperów map Bing. Po prostu kliknij **źródeł danych** w hello górnym pasku nawigacyjnym i wybierz **Zarządzanie źródłami danych**.

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

Jeśli wcześniej nie korzystano z interfejsu API map Bing, prawdopodobnie nie będzie żadnych źródeł danych nie istnieje, można utworzyć nowy, klikając na przekazywanie danych tooa źródło danych. Upewnij się, że możesz wypełnić wszystkie pola wymagane hello:

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

Użytkownik może się zastanawiać — co to jest plik danych hello i co należy przekazać? Dla celów hello ten test możemy użyć próbki hello opartego na potoku, który określa obszar waterfront Poznań hello:

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

Witaj powyżej reprezentuje następującą jednostkę:

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

Po prostu skopiuj i Wklej Powyższy ciąg hello do nowego pliku i zapisz go jako **NotificationHubsGeofence.pipe**, a następnie przekaż go w Centrum deweloperów Bing hello.

> [!NOTE]
> Może być zostanie wyświetlony monit o toospecify klucza hello **klucza głównego** różni się od hello **klucz zapytania**. Po prostu Utwórz nowy klucz przez hello pulpitu nawigacyjnego i Odśwież hello stronę przekazywania źródła danych.
> 
> 

Po przekazaniu pliku danych hello należy toomake Opublikuj hello źródła danych. 

Przejdź za**Zarządzanie źródłami danych**, jak opisano powyżej, Znajdź źródło danych na liście hello i wybierz polecenie **publikowania** w hello **akcje** kolumny. W nieco, powinny pojawić się źródła danych w hello **opublikowane źródła danych** karty:

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

Jeśli klikniesz przycisk **Edytuj**, możesz będą mogli toosee jeden rzut oka w nim wprowadzone lokalizacje:

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

W tym momencie hello portalu nie są wyświetlane hello granice dla wirtualnego ogrodzenia hello, że utworzyliśmy — potrzebne jest jedynie potwierdzenie, że określona lokalizacja hello znajduje się w odpowiedniej okolicy hello.

Masz teraz wszystkie wymagania hello hello źródła danych. Kliknij przycisk Szczegóły hello tooget na powitania adresu URL żądania dla wywołania interfejsu API hello, w Centrum deweloperów map Bing hello **źródeł danych** i wybierz **informacje o źródle danych**.

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

Witaj **adres URL zapytania** jest interesuje NAS tutaj. Jest to hello punkt końcowy, względem którego możemy wykonywać zapytania toocheck w czy hello urządzenie jest obecnie w granicach hello lokalizacji lub nie. tooperform to sprawdzić, należy po prostu tooexecute GET Wywołaj względem adresu URL zapytania hello z następujących parametrów dołączane hello:

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

W ten sposób określisz punkt docelowy uzyskany z urządzenia hello, a mapy Bing automatycznie wykonają hello obliczeń toosee czy znajduje się on w wirtualnym ogrodzeniu hello. Po wykonaniu żądania hello za pomocą przeglądarki (lub programu cURL), uzyskasz standardową odpowiedź w formacie JSON:

![](./media/notification-hubs-geofence/bing-maps-json.png)

Ta odpowiedź tylko wtedy, gdy hello punkt rzeczywiście znajduje się w wyznaczonych granicach hello. W przeciwnym razie otrzymasz pusty zasobnik **results**:

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a>Konfigurowanie aplikacji platformy uniwersalnej systemu Windows hello
Teraz, gdy mamy hello źródło danych jest gotowe, możemy rozpocząć pracę na powitania aplikacji platformy uniwersalnej systemu Windows, którą zainicjowano wcześniej.

Najpierw musimy włączyć usługi lokalizacji dla naszej aplikacji. toodo, kliknij dwukrotnie `Package.appxmanifest` w pliku **Eksploratora rozwiązań**.

![](./media/notification-hubs-geofence/vs-package-manifest.png)

Na karcie właściwości pakietu hello, która została otwarta, kliknij **możliwości** i upewnij się, że wybrano **lokalizacji**:

![](./media/notification-hubs-geofence/vs-package-location.png)

Możliwość lokalizacji hello jest zadeklarowana, Utwórz nowy folder w rozwiązaniu o nazwie `Core`i Dodaj nowy plik w nazwie `LocationHelper.cs`:

![](./media/notification-hubs-geofence/vs-location-helper.png)

Witaj `LocationHelper` samej klasy w tym momencie jest dosyć prosta — wszystkie robi zezwolić nam lokalizacji użytkownika hello tooobtain przy użyciu interfejsu API systemu hello:

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

Możesz przeczytać więcej na temat uzyskiwania hello lokalizacji użytkownika w aplikacji platformy uniwersalnej systemu Windows w oficjalne hello [dokumencie MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).

toocheck, który hello uzyskiwanie lokalizacji rzeczywiście działa, otwórz hello kodu strony, strony głównej (`MainPage.xaml.cs`). Utwórz nowy program obsługi zdarzeń dla hello `Loaded` zdarzenia w hello `MainPage` konstruktora:

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

Implementacja Hello hello obsługi zdarzeń wygląda następująco:

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

Zwróć uwagę, został zadeklarowany obsługi hello jako asynchroniczny ponieważ `GetCurrentLocation` jest oczekujący i dlatego wymaga toobe wykonywane w kontekście asynchronicznym. Ponadto ponieważ w pewnych okolicznościach możemy lokalizacją null (np. usługi lokalizacji hello są wyłączone lub aplikacji hello odmówiono uprawnienia tooaccess lokalizacji), należy się upewnić, że jest prawidłowo obsługiwane przy użyciu sprawdzania wartości null toomake.

Uruchamianie aplikacji hello. Zezwól na dostęp do lokalizacji:

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

Witaj po uruchomieniu aplikacji, powinny być stanie toosee hello współrzędnych w hello **dane wyjściowe** okno:

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

Teraz wiadomo, że pobieranie lokalizacji działa – możesz wolnego tooremove hello testowy — program obsługi zdarzeń Loaded, ponieważ firma Microsoft nie będzie już używany.

Witaj następnym krokiem jest toocapture zmiany lokalizacji. W tym Przejdź wstecz toohello `LocationHelper` klasy i dodać obsługi zdarzenia hello `PositionChanged`:

    geolocator.PositionChanged += Geolocator_PositionChanged;

Implementacja Hello spowoduje wyświetlenie współrzędnych lokalizacji hello w hello **dane wyjściowe** okno:

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a>Konfigurowanie hello wewnętrznej bazy danych
Pobierz hello [przykład zaplecza programu .NET z usługi GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). Po zakończeniu pobierania hello Otwórz hello `NotifyUsers` folder, a następnie — Witaj `NotifyUsers.sln` pliku.

Zestaw hello `AppBackend` projektu jako hello **projekt startowy** i uruchom je.

![](./media/notification-hubs-geofence/vs-startup-project.png)

Hello projektu jest już skonfigurowany toosend wypychania powiadomień tootarget urządzeń, dlatego potrzebujemy toodo tylko dwie czynności — wymienić hello ciąg połączenia na odpowiednie dla Centrum powiadomień hello i dodać granicę identyfikacji toosend hello powiadomienia tylko wtedy, gdy hello Użytkownik znajduje się w wirtualnym ogrodzeniu hello.

tooconfigure hello w ciągu połączenia, hello `Models` Otwórz folder `Notifications.cs`. Witaj `NotificationHubClient.CreateClientFromConnectionString` funkcji powinny zawierać hello informacje o Centrum powiadomień uzyskane w hello [Azure Portal](https://portal.azure.com) (Szukaj wewnątrz hello **zasady dostępu** bloku w  **Ustawienia**). Zapisz hello zaktualizowany plik konfiguracji.

Teraz potrzebujemy toocreate model dla wyniku interfejsu API map Bing hello. Witaj najprostszym toodo sposób, który jest kliknij prawym przyciskiem myszy na powitania `Models` folderu, **Dodaj** > **klasy**. Nadaj jej nazwę `GeofenceBoundary.cs`. Po zakończeniu skopiuj hello JSON z odpowiedzi hello interfejsu API, omówionej w pierwszej sekcji hello i w programie Visual Studio użyj **Edytuj** > **Wklej specjalne** > **Wklej dane JSON jako klasy**. 

W ten sposób Upewniamy się ten obiekt hello będzie można przeprowadzić deserializacji, dokładnie tak, jak zamierza. Wynikowy zestaw klas powinien wyglądać następująco:

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

Następnie otwórz plik `Controllers` > `NotificationsController.cs`. Potrzebujemy tootweak powitania po wywołaniu tooaccount hello docelową długość i szerokość geograficzną. Do tego, po prostu dodaj dwa sygnatury funkcji toohello ciągów — `latitude` i `longitude`.

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

Utwórz nową klasę w projekcie hello o nazwie `ApiHelper.cs` — użyjemy jej tooconnect tooBing toocheck punktu granic przecięcia. Zaimplementuj funkcję `IsPointWithinBounds` w następujący sposób:

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
> Upewnij się, że punkt końcowy hello interfejsu API toosubstitute o hello adresu URL zapytania uzyskanym wcześniej z hello Centrum deweloperów Bing (dotyczy klucza interfejsu API toohello). 
> 
> 

W przypadku wyników zapytania toohello to oznacza, że hello określony punkt znajduje się w granice hello hello wirtualnego ogrodzenia, dlatego zostanie zwrócona `true`. Jeśli nie są wyniki, Bing informuje NAS, czy punkt hello znajduje się poza hello wyszukiwania ramki, dlatego zostanie zwrócona `false`.

W `NotificationsController.cs`, Utwórz operację sprawdzania przed instrukcji switch hello:

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

W ten sposób hello powiadomienie jest wysyłane wyłącznie po hello punkt znajduje się w granicach hello.

## <a name="testing-push-notifications-in-hello-uwp-app"></a>Testowanie powiadomień wypychanych w aplikacji platformy uniwersalnej systemu Windows hello
Cofnięcie toohello aplikacji platformy uniwersalnej systemu Windows powinno być teraz możliwe tootest powiadomienia. W ramach hello `LocationHelper` klasy, Utwórz nową funkcję o nazwie `SendLocationToBackend`:

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
> Zamień hello `POST_URL` toohello lokalizację użytkownika wdrożonej aplikacji sieci web utworzonej w poprzedniej sekcji hello. Obecnie jest OK toorun ją lokalnie, ale podczas pracy nad wdrażania wersji publicznej, konieczne jest posiadanie toohost go przy użyciu zewnętrznego dostawcy.
> 
> 

Teraz upewnijmy się, że firma Microsoft zarejestrować aplikacji platformy uniwersalnej systemu Windows hello dla powiadomień wypychanych. W programie Visual Studio, kliknij **projektu** > **przechowywania** > **Skojarz aplikację ze sklepu hello**.

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

Po zalogowaniu konta dewelopera tooyour upewnij się, wybierz istniejącą aplikację lub Utwórz nową i skojarzyć z nią hello pakietu. 

Przejdź toohello Centrum deweloperów i otwórz hello aplikację, która właśnie utworzony. Kliknij pozycję **Usługi** > **Powiadomienia wypychane** > **Witryna usług Live**.

![](./media/notification-hubs-geofence/ms-live-services.png)

W witrynie hello Zanotuj hello **klucz tajny aplikacji** i hello **identyfikatora SID pakietu**. Konieczne będzie zarówno hello portalu Azure – Otwórz Centrum powiadomień, kliknij pozycję na **ustawienia** > **usługi powiadomień** > **systemu Windows (WNS)**i wprowadź informacje hello hello wymaganych pól.

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

Kliknij przycisk **Zapisz**.

Kliknij prawym przyciskiem myszy pozycję **Odwołania** w **Eksploratorze rozwiązań** i wybierz pozycje **Zarządzaj pakietami NuGet**. Firma Microsoft będzie tooadd toohello odwołania **biblioteki zarządzanej usługi Microsoft Azure Service Bus** — po prostu wyszukaj `WindowsAzure.Messaging.Managed` i dodaj go tooyour projektu.

![](./media/notification-hubs-geofence/vs-nuget.png)

Do celów testowych, możemy utworzyć hello `MainPage_Loaded` jeszcze raz program obsługi zdarzeń i Dodaj ten tooit fragment kodu:

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

Witaj powyżej rejestruje aplikacji hello hello Centrum powiadomień. Jesteś toogo gotowe! 

W `LocationHelper`, wewnątrz hello `Geolocator_PositionChanged` obsługi, można dodać fragment kodu, który będzie wymuszać umieszczanie lokalizacji hello w wirtualnym ogrodzeniu hello:

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

Ponieważ firma Microsoft nie są używane hello rzeczywiste współrzędne (które może nie być w granicach hello w chwili hello) i jest używany wstępnie zdefiniowane wartości testowe, zostanie wyświetlone powiadomienie po aktualizacji:

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a>Co dalej?
Istnieje kilka kroków trzeba toofollow w toohello dodanie powyżej toomake się, że rozwiązanie hello jest gotowe do produkcji.

Najpierw i, może być konieczne tooensure, że wirtualne ogrodzenia są dynamiczne. Będzie to wymagało dodatkowej pracy z hello interfejsu API Bing w kolejności toobe stanie tooupload nowych granic w ramach hello istniejącego źródła danych. Zapoznaj się hello [dokumentacji interfejsu API Bing przestrzennych danych usługi](https://msdn.microsoft.com/library/ff701734.aspx) Aby uzyskać więcej informacji na temat hello.

Po drugie, jako że dostarczania hello odbywa się toohello odpowiednich uczestników tooensure pracy można tootarget ich za pośrednictwem [znakowanie](notification-hubs-tags-segment-push-message.md).

w powyższym rozwiązaniu Hello opisano scenariusz, mogą mieć różnych platform docelowych, dlatego nie ograniczono możliwości specyficznych dla toosystem geofencing hello. Inaczej mówiąc, hello platformy uniwersalnej systemu Windows oferuje możliwości zbyt[wykryć wirtualne ogrodzenia prawo out-of--box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).

Aby uzyskać więcej informacji o możliwościach usługi Notification Hubs, odwiedź [portal dokumentacji](https://azure.microsoft.com/documentation/services/notification-hubs/).

