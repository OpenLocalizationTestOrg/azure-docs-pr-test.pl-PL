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
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a>Tworzenie hybrydowej aplikacji lokalnej/w chmurze platformy .NET przy użyciu przekaźnika WCF platformy Azure
## <a name="introduction"></a>Wprowadzenie

W tym artykule opisano, jak toobuild hybrydowego chmury aplikacji Microsoft Azure i programu Visual Studio. Hello samouczka przyjęto założenie, że nie masz wcześniejszego doświadczenia korzysta z platformy Azure. W mniej niż 30 minut będą miały aplikacji, która korzysta z wielu zasobów platformy Azure i w chmurze hello.

Dowiesz się:

* Jak toocreate lub dostosowanie istniejącej usługi sieci web do użytku przez rozwiązanie sieci web.
* Jak toouse hello Azure WCF przekaźnika usługi tooshare danych między aplikacją platformy Azure i usługi sieci web hostowaną w innym miejscu.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a>Jak usługa Azure Relay pomaga w tworzeniu rozwiązań hybrydowych

Rozwiązania biznesowe zwykle składają się z kombinacji niestandardowego kodu napisanego tootackle nowy i wymagań biznesowych oraz istniejących funkcjonalności dostarczonych przez rozwiązania i systemy, które zostały już wdrożone.

Architekci rozwiązań zaczynają toouse hello chmury w celu łatwiejszej obsługi wymagań skali i obniżenia kosztów operacyjnych. W ten sposób znajduje się istniejące elementy zawartości usług chciałby tooleverage jako bloków konstrukcyjnych dla swoich rozwiązań zaporą firmową hello i poza łatwo osiągnąć przez rozwiązanie chmury hello dostępu. Wiele wewnętrznych usług nie są wbudowane lub hostowanych w taki sposób, że ich łatwe uwidocznienie na krawędzi sieci firmowej hello.

[Azure przekazywania](https://azure.microsoft.com/services/service-bus/) zaprojektowano pod kątem hello przypadek użycia podjęcia istniejących usług sieci web Windows Communication Foundation (WCF) i mogą być usług bezpiecznie dostępne toosolutions, który znajduje się poza firmą hello bez konieczności Infrastruktura sieci firmowej toohello niepożądanych zmian. Takie usługi przekaźnika wciąż są hostowane wewnątrz istniejącego środowiska, ale delegują one nasłuchiwanie przychodzących sesji i żądań toohello hostowanych w chmurze usługi przekazywania danych. Usługa Azure Relay chroni także te usługi przed nieautoryzowanym dostępem przy użyciu uwierzytelniania za pomocą [sygnatury dostępu współdzielonego](../service-bus-messaging/service-bus-sas.md) (SAS, Shared Access Signature).

## <a name="solution-scenario"></a>Scenariusz rozwiązania
W tym samouczku utworzysz witrynę sieci Web programu ASP.NET, umożliwiającą toosee listy produktów na stronie spisu produktów hello.

![][0]

Samouczek Hello założono, że zawierają informacje o produkcie systemu lokalnego i używa tooreach przekazywania Azure do tego systemu. Jest to symulowane przez usługę sieci Web, która działa w prostej aplikacji konsolowej i jest uzupełniana przez zestaw produktów w pamięci. Będzie można stanie toorun tę aplikację konsolową na własnym komputerze i wdrożyć rolę sieci web hello na platformie Azure. W ten sposób przekonasz się jak rola sieci web hello działająca w hello centrum danych Azure rzeczywiście wywoła komputera, mimo że prawie na pewno będą znajdować się za co najmniej jedną zaporą i warstwę translatora adresów sieciowych adres komputera.

## <a name="set-up-hello-development-environment"></a>Konfigurowanie środowiska deweloperskiego hello

Przed rozpoczęciem tworzenia aplikacji platformy Azure Pobierz narzędzia hello i konfigurowanie środowiska programowania:

1. Zainstaluj hello Azure SDK dla platformy .NET z hello SDK [pliki do pobrania](https://azure.microsoft.com/downloads/).
2. W hello **.NET** kolumny, kliknij wersję hello [programu Visual Studio](http://www.visualstudio.com) używasz. Witaj czynnościach w ramach tego samouczka użyj programu Visual Studio 2015, ale współpracują oni również z programu Visual Studio 2017 r.
3. Gdy monit toorun lub zapisać hello Instalatora, kliknij przycisk **Uruchom**.
4. W hello **Instalatora platformy sieci Web**, kliknij przycisk **zainstalować** i kontynuować hello instalacji.
5. Po zakończeniu instalacji hello będzie mieć wszystko niezbędne toostart toodevelop hello aplikacji. Hello SDK zawiera narzędzia, które pozwalają w łatwy sposób tworzyć aplikacje platformy Azure w programie Visual Studio.

## <a name="create-a-namespace"></a>Tworzenie przestrzeni nazw

przy użyciu toobegin hello funkcji przekazywania na platformie Azure, musisz najpierw utworzyć przestrzeń nazw usługi. Przestrzeń nazw zapewnia kontener określania zakresu na potrzeby adresowania zasobów platformy Azure w aplikacji. Wykonaj hello [instrukcje w tym miejscu](relay-create-namespace-portal.md) toocreate przekazywania przestrzeni nazw.

## <a name="create-an-on-premises-server"></a>Tworzenie serwera lokalnego

Najpierw utworzysz lokalny (pozorny) system katalogu produktów. Będzie on dość proste; Możesz można traktować jako rzeczywisty lokalny system katalogu produktów z kompletną powierzchnią usług próbujemy toointegrate.

Ten projekt jest aplikacją konsoli programu Visual Studio i używa hello [pakietu NuGet usługi Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello bibliotek usługi Service Bus i ustawień konfiguracji.

### <a name="create-hello-project"></a>Utwórz projekt hello

1. Korzystając z uprawnień administratora, uruchom program Microsoft Visual Studio. tak, kliknij prawym przyciskiem myszy ikonę programu Visual Studio hello toodo, a następnie kliknij przycisk **Uruchom jako administrator**.
2. W programie Visual Studio na powitania **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.
3. W sekcji **Zainstalowane szablony** obszaru **Visual C#** kliknij pozycję **Aplikacja konsolowa (.NET Framework)**. W hello **nazwa** okno, nazwa typu hello **ProductsServer**:

   ![][11]
4. Kliknij przycisk **OK** toocreate hello **ProductsServer** projektu.
5. Jeśli użytkownik zainstalował już hello Menedżera pakietów NuGet dla programu Visual Studio, Pomiń toohello następnego kroku. W przeciwnym razie odwiedź stronę menedżera pakietów [NuGet][NuGet] i kliknij przycisk [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) (Zainstaluj menedżer pakietów NuGet). Wykonaj tooinstall monity hello hello Menedżera pakietów NuGet, a następnie ponownie uruchom program Visual Studio.
6. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ProductsServer** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.
7. Kliknij przycisk hello **Przeglądaj** , a następnie wyszukaj `Microsoft Azure Service Bus`. Wybierz hello **WindowsAzure.ServiceBus** pakietu.
8. Kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.

   ![][13]

   Należy zauważyć, że ten hello wymagane zestawy klientów są teraz przywoływane.
8. Dodaj nową klasę dla kontraktu produktu. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ProductsServer** projekt i kliknij przycisk **Dodaj**, a następnie kliknij przycisk **klasy**.
9. W hello **nazwa** okno, nazwa typu hello **ProductsContract.cs**. Następnie kliknij pozycję **Dodaj**.
10. W **ProductsContract.cs**, Zastąp definicję przestrzeni nazw hello hello następującego kodu, który definiuje kontrakt hello hello usługi.

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
11. W pliku Program.cs Zastąp definicję przestrzeni nazw hello hello następującego kodu, który dodaje hello profilu usługi i hello hosta.

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
12. W Eksploratorze rozwiązań kliknij dwukrotnie hello **App.config** pliku tooopen go w edytorze programu Visual Studio hello. U dołu hello hello `<system.ServiceModel>` elementu (ale nadal w ramach `<system.ServiceModel>`), Dodaj hello następującego kodu XML. Należy się tooreplace *yourServiceNamespace* o nazwie hello przestrzeni nazw, i *yourKey* kluczem sygnatury dostępu Współdzielonego hello został wcześniej pobrany z portalu hello:

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
13. Nadal w pliku App.config w hello `<appSettings>` elementu, Zastąp wartości parametrów połączenia hello przy użyciu parametrów połączenia hello uzyskanym wcześniej z portalu hello.

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. Naciśnij klawisz **Ctrl + Shift + B** lub hello **kompilacji** menu, kliknij przycisk **Kompiluj rozwiązanie** toobuild hello aplikacji i sprawdź hello dokładność pracy wykonanej do tej pory.

## <a name="create-an-aspnet-application"></a>Tworzenie aplikacji ASP.NET

W tej sekcji utworzysz prostą aplikację ASP.NET, która będzie wyświetlać dane pobrane z usługi produktów.

### <a name="create-hello-project"></a>Utwórz projekt hello

1. Upewnij się, że program Visual Studio jest uruchomiony z uprawnieniami administratora.
2. W programie Visual Studio na powitania **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.
3. W sekcji **Zainstalowane szablony** w obszarze **Visual C#** kliknij pozycję **Aplikacja sieci Web programu ASP.NET (.NET Framework)**. Nazwa projektu hello **ProductsPortal**. Następnie kliknij przycisk **OK**.

   ![][15]

4. Z hello **szablony ASP.NET** liście hello **nowej aplikacji sieci Web ASP.NET** okna dialogowego, kliknij przycisk **MVC**.

   ![][16]

6. Kliknij przycisk hello **Zmień uwierzytelnianie** przycisku. W hello **Zmień uwierzytelnianie** okna dialogowego Sprawdź, czy **bez uwierzytelniania** jest zaznaczone, a następnie kliknij przycisk **OK**. W tym samouczku wdrożysz aplikację, która nie wymaga logowania użytkownika.

    ![][18]

7. Po powrocie do hello **nowej aplikacji sieci Web ASP.NET** okna dialogowego, kliknij przycisk **OK** toocreate hello MVC aplikacji.
8. Teraz musisz skonfigurować zasoby platformy Azure dla nowej aplikacji sieci Web. Wykonaj kroki hello hello [publikowania tooAzure sekcji tego artykułu](../app-service-web/app-service-web-get-started-dotnet.md). Następnie wróć toothis samouczka i przejdź toohello następnego kroku.
10. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy pozycję **Modele** i kliknij polecenie **Dodaj**, a następnie kliknij pozycję **Klasa**. W hello **nazwa** okno, nazwa typu hello **Product.cs**. Następnie kliknij pozycję **Dodaj**.

    ![][17]

### <a name="modify-hello-web-application"></a>Modyfikowanie aplikacji sieci web hello

1. W pliku Product.cs hello w programie Visual Studio Zastąp istniejącą definicję przestrzeni nazw hello hello następującego kodu.

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
2. W Eksploratorze rozwiązań rozwiń hello **kontrolerów** folder, a następnie kliknij dwukrotnie hello **HomeController.cs** pliku tooopen go w programie Visual Studio.
3. W **HomeController.cs**, Zastąp istniejącą definicję przestrzeni nazw hello hello następującego kodu.

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
4. W Eksploratorze rozwiązań rozwiń hello Views\Shared folder, a następnie kliknij dwukrotnie **_Layout.cshtml** tooopen go w edytorze programu Visual Studio hello.
5. Zmień wszystkie wystąpienia **Moja aplikacja platformy ASP.NET** za**LITWARE's Products**.
6. Usuń hello **Home**, **o**, i **skontaktuj się z** łącza. Poniższy przykład hello usunięcie hello wyróżniony kod.

    ![][41]

7. W Eksploratorze rozwiązań rozwiń hello Views\Home folder, a następnie kliknij dwukrotnie **Index.cshtml** tooopen go w edytorze programu Visual Studio hello. Zastąp całą zawartość pliku hello hello hello następującego kodu.

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
8. tooverify hello dokładność pracy wykonanej do tej pory, naciśnij klawisz **Ctrl + Shift + B** toobuild hello projektu.

### <a name="run-hello-app-locally"></a>Uruchamianie aplikacji hello lokalnie

Uruchom tooverify aplikacji hello, który działa.

1. Upewnij się, że **ProductsPortal** jest hello aktywnego projektu. Kliknij prawym przyciskiem myszy nazwę projektu hello w Eksploratorze rozwiązań i wybierz **Ustaw jako projekt startowy**.
2. W programie Visual Studio naciśnij klawisz **F5**.
3. Aplikacja powinna uruchomić się w przeglądarce.

   ![][21]

## <a name="put-hello-pieces-together"></a>Składanie fragmentów hello

Witaj następnym krokiem jest toohook się hello na lokalnego serwera produktów z hello aplikacji ASP.NET.

1. Jeśli jeszcze nie jest otwarty w programie Visual Studio ponownie otwórz hello **ProductsPortal** projekt utworzony w hello [tworzenie aplikacji ASP.NET](#create-an-aspnet-application) sekcji.
2. Podobne krok toohello w sekcji "Tworzenie serwera lokalnego" hello, Dodaj hello NuGet toohello projekt będzie odwoływał się pakiet. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ProductsPortal** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.
3. Wyszukaj "Service Bus" i wybierz hello **WindowsAzure.ServiceBus** elementu. Następnie ukończyć powitalnych instalację i zamknąć to okno dialogowe.
4. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ProductsPortal** projektu, a następnie kliknij przycisk **Dodaj**, następnie **istniejący element**.
5. Przejdź toohello **ProductsContract.cs** pliku z hello **ProductsServer** projekt konsoli. Kliknij przycisk toohighlight ProductsContract.cs. Kliknij przycisk hello Strzałka w dół obok zbyt**Dodaj**, następnie kliknij przycisk **Dodaj jako Link**.

   ![][24]

6. Teraz Otwórz hello **HomeController.cs** w edytorze programu Visual Studio hello i Zastąp definicję przestrzeni nazw hello hello następującego kodu. Należy się tooreplace *yourServiceNamespace* hello nazwą swojej przestrzeni nazw usługi i *yourKey* kluczem sygnatury dostępu Współdzielonego. Spowoduje to włączenie powitania klienta toocall hello Usługa lokalna, zwracając wynik hello hello wywołania.

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
7. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ProductsPortal** rozwiązań (Upewnij się, że tooright kliknięciem hello rozwiązanie, nie hello projektu). Kliknij pozycję **Dodaj**, a następnie kliknij pozycję **Istniejący projekt**.
8. Przejdź toohello **ProductsServer** projektu, a następnie kliknij dwukrotnie hello **ProductsServer.csproj** tooadd pliku rozwiązania go.
9. **ProductsServer** musi być uruchomiona w kolejności toodisplay hello danych na **ProductsPortal**. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ProductsPortal** rozwiązanie i kliknij przycisk **właściwości**. Witaj **strony właściwości** zostanie wyświetlone okno dialogowe.
10. Na powitania po lewej stronie, kliknij przycisk **projekt startowy**. Na powitania po prawej stronie, kliknij przycisk **wiele projektów startowych**. Upewnij się, że **ProductsServer** i **ProductsPortal** są wymienione w tej kolejności z **Start** Ustaw jako hello akcji dla obu.

      ![][25]

11. Nadal w hello **właściwości** okno dialogowe, kliknij przycisk **zależności projektu** na powitania po lewej stronie.
12. W hello **projekty** kliknij **ProductsServer**. Upewnij się, że projekt **ProductsPortal** nie jest wybrany.
13. W hello **projekty** kliknij **ProductsPortal**. Upewnij się, że projekt **ProductsServer** jest wybrany.

    ![][26]

14. Kliknij przycisk **OK** w hello **strony właściwości** okno dialogowe.

## <a name="run-hello-project-locally"></a>Uruchom projekt hello lokalnie

tootest hello aplikację lokalnie, w programie Visual Studio naciśnij klawisz **F5**. serwer lokalny Hello (**ProductsServer**) powinien uruchomić się jako pierwszy, a następnie hello **ProductsPortal** aplikacja powinna uruchomić się w oknie przeglądarki. Teraz, pojawi się spis produktów hello list dane pobrane z hello produktu usługi lokalnego systemu.

![][10]

Naciśnij klawisz **Odśwież** na powitania **ProductsPortal** strony. Każdym odświeżeniu strony hello, zobaczysz hello aplikacja serwera wyświetli komunikat po `GetProducts()` z **ProductsServer** jest wywoływana.

Zamknąć obie aplikacje przed kontynuowaniem toohello następnego kroku.

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a>Wdrażanie hello ProductsPortal projektu tooan aplikacji sieci web Azure

Witaj, następnym krokiem jest aplikacja sieci Web Azure hello toorepublish **ProductsPortal** frontonu. Witaj, po:

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ProductsPortal** projektu, a następnie kliknij przycisk **publikowania**. Następnie kliknij przycisk **publikowania** na powitania **publikowania** strony.

  > [!NOTE]
  > Zobaczysz komunikat o błędzie w oknie przeglądarki powitania po hello **ProductsPortal** projektu sieci web zostanie automatycznie uruchomiony po wdrożeniu hello. To jest oczekiwany i występuje, ponieważ hello **ProductsServer** aplikacji nie jest jeszcze uruchomiona.
>
>

2. Adres URL hello kopiowania hello wdrożonych aplikacji sieci web, ponieważ będzie potrzebny URL hello w następnym kroku hello. W oknie działanie usługi Azure App Service hello w programie Visual Studio, mogą również uzyskać ten adres URL:

  ![][9]

3. Zamknij hello przeglądarki okna toostop hello uruchomiona aplikacja.

### <a name="set-productsportal-as-web-app"></a>Ustawianie projektu ProductsPortal jako aplikacji sieci Web

Przed działającej aplikacji hello w chmurze hello, upewnij się, że **ProductsPortal** jest uruchamiana z poziomu programu Visual Studio jako aplikacji sieci web.

1. W programie Visual Studio, kliknij prawym przyciskiem myszy hello **ProductsPortal** projektu, a następnie kliknij przycisk **właściwości**.
2. W lewej kolumnie powitania kliknij **Web**.
3. W hello **Akcja uruchamiania** kliknij hello **początkowy adres URL** przycisk, a w polu tekstowym hello wprowadź adres URL hello z wcześniej wdrożonej aplikacji sieci web; na przykład `http://productsportal1234567890.azurewebsites.net/`.

    ![][27]

4. Z hello **pliku** menu programu Visual Studio kliknij **Zapisz wszystko**.
5. W menu kompilacji hello w programie Visual Studio, kliknij **Kompiluj ponownie rozwiązanie**.

## <a name="run-hello-application"></a>Uruchamianie aplikacji hello

1. Naciśnij klawisz F5 toobuild i uruchamianie aplikacji hello. Hello lokalnego serwera (hello **ProductsServer** aplikacji konsoli) powinien uruchomić się jako pierwszy, a następnie hello **ProductsPortal** aplikacji powinna uruchomić się w oknie przeglądarki, jak pokazano w po ekranie powitania Zrzut. Zwróć uwagę ponownie ten spis produktów hello wyświetla dane pobrane z hello produktu usługi lokalnego systemu, a dane zostaną wyświetlone w aplikacji sieci web hello. Sprawdź, czy toomake adres URL hello który **ProductsPortal** działa w chmurze hello jako aplikacji sieci web platformy Azure.

   ![][1]

   > [!IMPORTANT]
   > Witaj **ProductsServer** aplikacji konsoli musi być uruchomiony i może tooserve hello danych toohello **ProductsPortal** aplikacji. Jeśli przeglądarka hello jest wyświetlany błąd, zaczekaj kilka sekund dla **ProductsServer** tooload i hello wyświetlania następującego komunikatu. Następnie naciśnij klawisz **Odśwież** w przeglądarce hello.
   >
   >

   ![][37]
2. Wstecz w przeglądarce hello, naciśnij klawisz **Odśwież** na powitania **ProductsPortal** strony. Każdym odświeżeniu strony hello, zobaczysz hello aplikacja serwera wyświetli komunikat po `GetProducts()` z **ProductsServer** jest wywoływana.

    ![][38]

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat przekaźnika usługi Azure, zobacz hello następujące zasoby:  

* [Co to jest usługa Azure Relay?](relay-what-is-it.md)  
* [Sposób przekazywania toouse](service-bus-dotnet-how-to-use-relay.md)  

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
