---
title: "Samouczek REST magistrali aaaService przy użyciu przekaźnika usługi Azure | Dokumentacja firmy Microsoft"
description: "Utworzyć prostą aplikację do hosta przekaźnika usługi Azure Service Bus, która uwidacznia interfejs REST."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a>Samouczek usługi Azure REST przekaźnika usługi WCF

W tym samouczku opisano, jak toobuild proste przekazywania Azure obsługiwania aplikacji, która uwidacznia interfejs REST. Interfejs REST umożliwia klientowi sieci web, takich jak przeglądarki sieci web, powitalne tooaccess interfejsów API usługi Service Bus za pośrednictwem protokołu HTTP żądania.

Witaj samouczku tooconstruct modelu programowania hello REST Windows Communication Foundation (WCF) usługi REST usługi Service Bus. Aby uzyskać więcej informacji, zobacz [Model programowania interfejsu REST usługi WCF](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) i [projektowanie i Implementowanie usług](/dotnet/framework/wcf/designing-and-implementing-services) w hello dokumentacji usługi WCF.

## <a name="step-1-create-a-namespace"></a>Krok 1. Tworzenie przestrzeni nazw

przy użyciu toobegin hello funkcji przekazywania na platformie Azure, musisz najpierw utworzyć przestrzeń nazw usługi. Przestrzeń nazw zapewnia kontener określania zakresu na potrzeby adresowania zasobów platformy Azure w aplikacji. Wykonaj hello [instrukcje w tym miejscu](relay-create-namespace-portal.md) toocreate przekazywania przestrzeni nazw.

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a>Krok 2: Definiowanie toouse kontraktu usługi WCF opartego na interfejsie REST, z przekaźnika usługi Azure

Podczas tworzenia usługi WCF na interfejsie REST należy zdefiniować kontrakt hello. kontrakt Hello Określa, jakie operacje hello obsługuje hosta. Operacja usługi może być rozumiana jako metoda usługi sieci Web. Kontrakty są tworzone przez definiowanie interfejsu C++, C# lub Visual Basic. Każda metoda w interfejsie hello odpowiada tooa określonej operacji usługi. Witaj [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) atrybutu musi być zastosowany tooeach interfejsu i hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) atrybut musi być zastosowany tooeach operacji. Jeśli metoda w interfejsie z atrybutem hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) nie ma hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), metoda nie jest uwidaczniana. Kod Hello używany do wykonywania tych zadań pokazano przykład Witaj hello procedury.

Witaj podstawowa różnica między kontraktu usługi WCF i kontrakt typu REST jest dodanie hello toohello właściwości [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx). Ta właściwość umożliwia toomap metody w metodę interfejsu tooa na powitania po drugiej stronie powitania interfejsu. W tym przypadku użyjemy [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink tooHTTP metody GET. Dzięki temu usługa Service Bus tooaccurately pobierać i interpretować polecenia wysyłane toohello interfejsu.

### <a name="toocreate-a-contract-with-an-interface"></a>toocreate kontrakt interfejsu

1. Otwórz program Visual Studio jako administrator: kliknij prawym przyciskiem myszy program hello hello **Start** menu, a następnie kliknij przycisk **Uruchom jako administrator**.
2. Utwórz nowy projekt aplikacji konsoli. Kliknij przycisk hello **pliku** menu i wybierz **nowy**, a następnie wybierz pozycję **projektu**. W hello **nowy projekt** okno dialogowe, kliknij przycisk **Visual C#**, wybierz pozycję hello **aplikacji konsoli** szablonu i nadaj mu nazwę **ImageListener**. Użyj domyślnej hello **lokalizacji**. Kliknij przycisk **OK** toocreate hello projektu.
3. W przypadku projektu C# program Visual Studio utworzy plik `Program.cs`. Ta klasa zawiera pustą `Main()` metody wymagane dla toobuild projekt aplikacji konsoli poprawnie.
4. Dodawanie odwołań tooService magistrali i **System.ServiceModel.dll** toohello projekcie, instalując pakiet NuGet usługi Service Bus hello. Ten pakiet automatycznie dodaje bibliotek usługi Service Bus toohello odwołania, a także hello WCF **System.ServiceModel**. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ImageListener** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**. Kliknij przycisk hello **Przeglądaj** , a następnie wyszukaj `Microsoft Azure Service Bus`. Kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.
5. Należy jawnie dodać odwołanie za**System.ServiceModel.Web.dll** toohello projektu:
   
    a. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **odwołania** folder hello folderu projektu, a następnie kliknij przycisk **Dodaj odwołanie**.
   
    b. W hello **Dodaj odwołanie** okna dialogowego kliknij hello **Framework** kartę na powitania po lewej stronie i w hello **wyszukiwania** wpisz **System.ServiceModel.Web** . Wybierz hello **System.ServiceModel.Web** pole wyboru, a następnie kliknij przycisk **OK**.
6. Dodaj następujące hello `using` instrukcje na początku pliku Program.cs hello hello.
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) jest hello przestrzeni nazw, która zapewnia dostęp programistyczny toobasic funkcji usługi WCF. Przekaźnik WCF używa wielu hello obiektów i atrybutów kontraktów usług WCF toodefine. W większości aplikacji przekaźnika użyjesz tej przestrzeni nazw. Podobnie [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) pomaga zdefiniować kanał hello jest obiektem hello służącym do komunikacji z przeglądarką sieci web Azure przekazywania i powitania klienta. Na koniec [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) zawiera typy hello, umożliwiające toocreate aplikacji sieci web.
7. Zmień nazwę hello `ImageListener` przestrzeni nazw zbyt**Microsoft.ServiceBus.Samples**.
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. Bezpośrednio po hello otwierania nawiasie klamrowym deklaracji przestrzeni nazw hello, zdefiniuj nowy interfejs o nazwie **IImageContract** i zastosować hello **ServiceContractAttribute** interfejs toohello atrybutu wartość `http://samples.microsoft.com/ServiceModel/Relay/`. Wartość przestrzeni nazw Hello różni się od przestrzeni nazw hello, używanej w całym zakresie hello kodu. Wartość przestrzeni nazw Hello jest używany jako unikatowy identyfikator dla tego kontraktu i powinna zawierać informacje o wersji. Aby uzyskać więcej informacji, zobacz [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498) (Obsługa wersji usług). Jawne określenie hello przestrzeni nazw zapobiega dodawaniu Nazwa kontraktu toohello hello domyślnej wartości przestrzeni nazw.
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. W ramach hello `IImageContract` interfejsu, Zadeklaruj metodę dla hello jednej operacji hello `IImageContract` ujawnia kontraktu w hello na interfejsie i Zastosuj hello `OperationContractAttribute` atrybutu metody toohello mają tooexpose w ramach publicznej hello magistrali kontrakt.
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. W hello **OperationContract** atrybutu, Dodaj hello **WebGet** wartości.
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    Grozi to umożliwia hello tooroute usługi przekazywania żądania HTTP GET zbyt`GetImage`i zwracać wartości hello tootranslate `GetImage` do odpowiedzi metody GETRESPONSE protokołu HTTP. Później w samouczku hello użyjesz tooaccess przeglądarki sieci web — metoda i toodisplay obraz powitania w przeglądarce hello.
11. Bezpośrednio po hello `IImageContract` definicji, Zadeklaruj kanał dziedziczący zarówno hello `IImageContract` i `IClientChannel` interfejsów.
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    Kanał jest obiektem usługi WCF hello za pośrednictwem której hello usługa i klient przekazują informacje tooeach innych. Później utworzysz kanał hello w aplikacji hosta. Azure przekazywania następnie używa tego kanału toopass hello żądania HTTP GET hello przeglądarki tooyour **GetImage** implementacji. Przekaźnik Hello używa również hello kanału tootake hello **GetImage** zwracać wartości i umożliwiło metody GETRESPONSE protokołu HTTP dla przeglądarki klienta hello.
12. Z hello **kompilacji** menu, kliknij przycisk **Kompiluj rozwiązanie** tooconfirm hello dokładność pracy wykonanej do tej pory.

### <a name="example"></a>Przykład
powitania po kod przedstawia podstawowy interfejs definiujący kontrakt usługi WCF przekazywania.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a>Krok 3: Implementowanie toouse kontraktu usługi WCF opartego na interfejsie REST usługi Service Bus
Tworzenie usługi typu REST usługi WCF przekazywania wymaga najpierw utworzyć kontrakt hello, który został zdefiniowany przy użyciu interfejsu. Witaj następnym krokiem jest tooimplement hello interfejsu. Obejmuje to tworzenie klasy o nazwie **ImageService** hello zdefiniowane przez użytkownika, który zawiera **IImageContract** interfejsu. Po zaimplementowaniu kontraktu hello, następnie należy skonfigurować interfejs hello przy użyciu pliku App.config. Witaj plik konfiguracji zawiera niezbędne informacje dotyczące aplikacji hello, takie jak nazwa hello hello usługi, nazwa hello hello kontraktu i typ hello protokołu, który jest używany toocommunicate z usługą przekazywania hello. Kod Hello używany do wykonywania tych zadań podano w przykład Witaj hello procedury.

Podobnie jak w poprzednich kroków hello, jest bardzo mało różnica między implementacją kontraktu typu REST i kontraktu usługi WCF przekazywania.

### <a name="tooimplement-a-rest-style-service-bus-contract"></a>kontrakt usługi Service Bus tooimplement typu REST
1. Utwórz nową klasę o nazwie **ImageService** bezpośrednio po definicji hello hello **IImageContract** interfejsu. Witaj **ImageService** klasa implementuje hello **IImageContract** interfejsu.
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    Podobne implementacje interfejsu tooother, można zaimplementować definicję hello w innym pliku. Jednak w tym samouczku implementacji hello jest wyświetlana w hello tego samego pliku jako hello definicja interfejsu i `Main()` metody.
2. Zastosuj hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) atrybutu toohello **IImageService** tooindicate klasy, która hello klasa jest implementacją kontraktu usługi WCF.
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    Jak wspomniano wcześniej, ta przestrzeń nazw nie jest tradycyjną przestrzenią nazw. Zamiast tego jest częścią architektury usługi WCF, która identyfikuje kontrakt hello hello. Aby uzyskać więcej informacji, zobacz hello [nazwy kontraktów danych](https://msdn.microsoft.com/library/ms731045.aspx) tematu w hello dokumentacji usługi WCF.
3. Dodaj projekt tooyour obrazów JPG.  
   
    Jest to obraz powitania usługa wyświetla w hello odbieranie przeglądarki. Kliknij prawym przyciskiem myszy projekt i kliknij polecenie **Dodaj**. Następnie kliknij pozycję **Istniejący element**. Użyj hello **Dodaj istniejący element** tooan toobrowse — okno dialogowe odpowiednie jpg, a następnie kliknij przycisk **Dodaj**.
   
    Podczas dodawania pliku hello, upewnij się, że **wszystkie pliki** w toohello dalej hello listy rozwijanej zostanie wybrany **nazwa pliku:** pola. Witaj pozostałej części tego samouczka przyjęto założenie, że hello nazwa obrazu hello to "image.jpg". Inny plik będzie mieć toorename hello obraz, lub zmień toocompensate Twojego kodu.
4. toomake się upewnić, że hello usługą można znaleźć plik obrazu hello, w **Eksploratora rozwiązań** kliknij prawym przyciskiem myszy plik obrazu hello, a następnie kliknij przycisk **właściwości**. W hello **właściwości** ustawić okienku **skopiuj tooOutput katalogu** za**Kopiuj, jeśli nowszy**.
5. Dodaj toohello odwołanie **System.Drawing.dll** toohello zestawu projektu, a także dodać następujące hello skojarzone `using` instrukcje.  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. W hello **ImageService** klasy, Dodaj hello następujących konstruktora, że obciążenie hello mapę bitową i przygotowuje toosend on toohello przeglądarki klienta.
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. Bezpośrednio po poprzednim kodzie hello Dodaj następujące hello **GetImage** metoda hello **ImageService** klasy tooreturn HTTP komunikat, który zawiera obraz powitania.
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    Ta implementacja używa **MemoryStream** tooretrieve hello obrazu i przygotowywania ich do przesyłania strumieniowego toohello przeglądarki. Go uruchamia hello strumieniowe w pozycji zero, deklaruje zawartość strumienia hello jako obraz jpeg i strumieni hello informacji.
8. Z hello **kompilacji** menu, kliknij przycisk **Kompiluj rozwiązanie**.

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a>toodefine hello konfigurację uruchamiania usługi sieci web hello usługi Service Bus
1. W **Eksploratora rozwiązań**, kliknij dwukrotnie **App.config** tooopen go w edytorze programu Visual Studio hello.
   
    Witaj **App.config** plik zawiera hello nazwy usługi, punkt końcowy (to znaczy hello lokalizację przekazywania Azure udostępnia dla klientów i hosty toocommunicate ze sobą) i powiązanie (typ hello protokół, który jest używany toocommunicate). Witaj główną różnicą jest ten punkt końcowy usługi hello skonfigurowane odwołuje się tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) powiązania.
2. Witaj `<system.serviceModel>` — element XML jest elementem usługi WCF, który definiuje co najmniej jedna usługa. W tym miejscu jest nazwa usługi hello toodefine używane i punktu końcowego. U dołu hello hello `<system.serviceModel>` elementu (ale nadal w ramach `<system.serviceModel>`), Dodaj `<bindings>` element, który ma powitania po zawartości. Definiuje hello powiązania używane w aplikacji hello. Można zdefiniować wiele powiązań, ale w tym samouczku definiowane jest tylko jedno.
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    Witaj poprzedni kod definiuje przekazywania WCF [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) powiązanie o **relayClientAuthenticationType** ustawić także**Brak**. To ustawienie wskazuje, że punkt końcowy korzystający z tego powiązania nie wymaga poświadczeń klienta.
3. Po hello `<bindings>` elementu, Dodaj `<services>` elementu. Podobnymi powiązaniami toohello, można zdefiniować wiele usług w pojedynczym pliku konfiguracji. Jednak w tym samouczku definiowana jest tylko jedna.
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    Ten krok obejmuje skonfigurowanie usługi, która będzie używana domyślna hello wcześniej zdefiniowany **webHttpRelayBinding**. Używa również domyślny hello **sbTokenProvider**, która jest zdefiniowana w hello następnego kroku.
4. Po hello `<services>` elementu, Utwórz `<behaviors>` element z powitania po zawartości, zastępując "element SAS_KEY" hello *sygnatura dostępu współdzielonego* klucza (SAS) uzyskanym wcześniej z hello [portalu Azure ][Azure portal].
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. Nadal w pliku App.config w hello `<appSettings>` elementu, Zastąp hello całego połączenia ciąg wartości z ciągu połączenia hello uzyskanym wcześniej z portalu hello. 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. Z hello **kompilacji** menu, kliknij przycisk **Kompiluj rozwiązanie** toobuild hello całego rozwiązania.

### <a name="example"></a>Przykład
Witaj poniższy kod przedstawia implementację kontraktu i usługi dla usługi opartego na interfejsie REST uruchomionej na magistrali usług przy użyciu hello hello **WebHttpRelayBinding** powiązania.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Witaj poniższy przykład przedstawia plik App.config hello skojarzonych z usługą hello.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a>Krok 4: Hostowanie toouse usługi WCF opartego na interfejsie REST hello Azure przekazywania
W tym kroku opisano, jak toorun sieci web usługi, przy użyciu aplikacji konsoli z przekaźnika usługi WCF. Pełna lista hello kod napisany w tym kroku podano w przykład Witaj hello procedury.

### <a name="toocreate-a-base-address-for-hello-service"></a>adres podstawowy usługi hello toocreate
1. W hello `Main()` deklaracji funkcji, tworzenie przestrzeni nazw hello zmiennej toostore projektu. Upewnij się, że tooreplace `yourNamespace` o nazwie hello hello nazw przekaźnika utworzonego wcześniej.
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    Usługa Service Bus używa hello nazwą Twojej przestrzeni nazw toocreate Unikatowy identyfikator URI.
2. Utwórz `Uri` wystąpienia dla adresu podstawowego hello hello usługi, która jest oparta na powitania przestrzeni nazw.
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a>toocreate i skonfigurować hosta usługi sieci web hello
* Utwórz hosta usługi sieci web hello przy użyciu hello adresu URI utworzonego wcześniej w tej sekcji.
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    host usługi Hello jest hello WCF obiekt, który tworzy hello aplikacji hosta. W tym przykładzie przekazuje hello typ hosta ma toocreate ( **ImageService**), a także hello adres, w którym chcesz tooexpose hello hosta aplikacji.

### <a name="toorun-hello-web-service-host"></a>host usługi sieci web hello toorun
1. Otwórz usługę hello.
   
    ```csharp
    host.Open();
    ```
    Usługa Hello jest teraz uruchomiona.
2. Wyświetla komunikat informujący, że usługa hello jest uruchomiona, i jak toostop hello usługi.
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. Po zakończeniu zamknij hosta usługi hello.
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a>Przykład
Hello poniższy przykład zawiera hello kontrakt usługi i implementację z poprzednich kroków w usłudze hello samouczek i hosty hello w aplikacji konsoli. Kompiluj powitania po kod do pliku wykonywalnego o nazwie ImageListener.exe.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a>Kompilowanie kodu hello
Po utworzeniu rozwiązania hello, hello następujących aplikacji hello toorun:

1. Naciśnij klawisz **F5**, lub Wyszukaj toohello lokalizacji pliku wykonywalnego (ImageListener\bin\Debug\ImageListener.exe), toorun hello usługi. Zachowaj hello aplikacja działa, ponieważ są wymagane tooperform hello następnego kroku.
2. Skopiuj i wklej adres hello z wiersza polecenia hello obraz powitania toosee przeglądarki.
3. Po zakończeniu naciśnij klawisz **Enter** w aplikacja hello tooclose w oknie wiersza polecenia hello.

## <a name="next-steps"></a>Następne kroki
Teraz gdy masz utworzoną aplikację, która używa przekaźnika usługi Service Bus hello, zobacz hello następujące artykuły toolearn więcej temat przekaźnika usługi Azure:

* [Omówienie architektury usługi Azure Service Bus](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [Omówienie usługi Azure Relay](relay-what-is-it.md)
* [Jak usługa z platformą .NET przekazywania toouse hello WCF](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
