---
title: "aaa.NET wielowarstwową aplikację przy użyciu usługi Azure Service Bus | Dokumentacja firmy Microsoft"
description: "Samouczek platformy .NET, która pomaga utworzyć aplikację wielowarstwową na platformie Azure, która używa toocommunicate kolejek usługi Service Bus między warstwami."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a>Aplikacja wielowarstwowa platformy .NET używająca kolejek usługi Azure Service Bus
## <a name="introduction"></a>Wprowadzenie
Tworzenie dla Microsoft Azure jest łatwy w użyciu programu Visual Studio i hello wolne zestawu Azure SDK dla platformy .NET. W tym samouczku przedstawiono hello kroki toocreate aplikacji, która używa wielu zasobów platformy Azure działa w środowisku lokalnym.

Dowiesz się hello następujące czynności:

* Jak tooenable komputera dla rozwoju platformy Azure za pomocą jednej pobrać i zainstalować.
* Jak toouse toodevelop programu Visual Studio dla platformy Azure.
* Jak toocreate wielowarstwową aplikację na platformie Azure przy użyciu ról sieci web i proces roboczy.
* W jaki sposób toocommunicate między warstwami przy użyciu kolejek usługi Service Bus.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

W tym samouczku możesz utworzyć i uruchomić aplikację wielowarstwową hello Azure w usłudze w chmurze. Fronton Hello jest roli sieci web platformy ASP.NET MVC i hello zaplecze rolę procesu roboczego, który korzysta z kolejki usługi Service Bus. Możesz utworzyć hello samą aplikację wielowarstwową z frontonu hello jako projekt sieci web, który jest wdrożony tooan witrynie systemu Azure zamiast usługi w chmurze. Możesz również wypróbować hello [.NET na lokalnej/w chmurze hybrydowej aplikacji](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) samouczka.

Witaj Poniższy zrzut ekranu przedstawia aplikacji hello ukończone.

![][0]

## <a name="scenario-overview-inter-role-communication"></a>Omówienie scenariusza: komunikacja między rolami
toosubmit zamówienie do przetworzenia hello frontonu składnik interfejsu użytkownika w roli sieć web hello musi współdziałać z logiką warstwy środkowej hello uruchomionej w roli procesu roboczego hello. W tym przykładzie użyto komunikatów usługi Service Bus hello komunikacji między warstwami hello.

Przy użyciu usługi Service Bus wysyłanie komunikatów między hello sieci web i warstwą środkową oddziela dwa składniki. Z kolei hello toodirect wiadomości (czyli TCP lub HTTP), warstwa sieci web nie łączy z warstwy środkowej toohello bezpośrednio; Zamiast tego wypycha jednostki pracy jako komunikaty do usługi Service Bus, która w niezawodny sposób je przechowuje do momentu hello Środkowa warstwa będzie gotowa tooconsume i przetwarzanie ich.

Usługa Service Bus zapewnia dwie jednostki toosupport obsługiwanych przez brokera komunikatów: kolejki i tematy. W przypadku kolejek każdy komunikat wysłane toohello kolejki jest używany przez jednego odbiorcę. Tematy obsługują wzorzec publikowania/subskrypcji hello w którym każdy opublikowany komunikat staje się dostępne tooa subskrypcji zarejestrowanej hello tematu. Każda subskrypcja logicznie zachowuje własną kolejkę komunikatów. Subskrypcje można również skonfigurować przy użyciu reguł filtrowania, ograniczających hello zestaw komunikatów przesyłany do toothose kolejki subskrypcji hello pasujące hello filtru. Witaj poniższym przykładzie użyto kolejek usługi Service Bus.

![][1]

Ten mechanizm komunikacji ma kilka zalet w stosunku do komunikatów bezpośrednich:

* **Rozdzielenie czasowe.** Z hello asynchroniczny wzorzec przesyłania komunikatów, producenci i konsumenci nie muszą być online na powitania tym samym czasie. Usługa Service Bus niezawodny sposób przechowuje komunikaty do momentu hello odbierająca jest gotowa do ich odebrania. Dzięki temu składniki hello toobe aplikacji hello rozproszonych rozłączone zarówno dobrowolnie, na przykład w celu przeprowadzenia konserwacji lub powodu tooa awarii składników, bez wywierania wpływu na system jako całość. Ponadto korzystanie z aplikacji hello może być konieczne toocome online pewnych porach dnia hello.
* **Wyrównywanie obciążenia.** W wielu aplikacjach obciążenie systemu różni się w czasie, gdy czas przetwarzania hello wymagany dla każdej jednostki pracy jest zwykle stały. Pośredniczenie producentami a konsumentami komunikatów z kolejki oznacza, że udostępniane tego hello korzystanie z aplikacji (proces roboczy hello) tylko potrzeb toobe tooaccommodate średni obciążenia, a nie obciążeniem szczytowym. głębokość kolejki hello Hello rośnie i zmniejsza się w zależności od zmian obciążenia przychodzącego hello. To jest zapisywany bezpośrednio oszczędność pieniędzy hello ilość obciążenia aplikacji hello wymagane tooservice infrastruktury.
* **Równoważenie obciążenia.** W miarę wzrostu obciążenia więcej procesów roboczych można dodać tooread z hello kolejki. Każdy komunikat jest przetwarzany przez tylko jeden z procesów roboczych hello. Ponadto to Równoważenie obciążenia oparte na ściąganiu umożliwia optymalnie wykorzystać maszyny procesów roboczych hello nawet wtedy, gdy maszyny procesów roboczych różnią się pod względem mocy przetwarzania, ponieważ każda będzie ściągać komunikaty własnych maksymalną szybkością. Ten wzorzec jest często nazywany hello *konkurujących konsumentów* wzorca.
  
  ![][2]

Hello w następujących sekcjach omówiono w nim hello kodu, który implementuje tę architekturę.

## <a name="set-up-hello-development-environment"></a>Konfigurowanie środowiska deweloperskiego hello
Przed rozpoczęciem tworzenia aplikacji platformy Azure Pobierz narzędzia hello i konfigurowanie środowiska deweloperskiego.

1. Zainstaluj hello Azure SDK dla platformy .NET z hello SDK [pliki do pobrania](https://azure.microsoft.com/downloads/).
2. W hello **.NET** kolumny, kliknij wersję hello [programu Visual Studio](http://www.visualstudio.com) używasz. Witaj czynnościach w ramach tego samouczka użyj programu Visual Studio 2015, ale współpracują oni również z programu Visual Studio 2017 r.
3. Gdy monit toorun lub zapisać hello Instalatora, kliknij przycisk **Uruchom**.
4. W hello **Instalatora platformy sieci Web**, kliknij przycisk **zainstalować** i kontynuować hello instalacji.
5. Po zakończeniu instalacji hello będzie mieć wszystko niezbędne toostart toodevelop hello aplikacji. Hello SDK zawiera narzędzia, które pozwalają w łatwy sposób tworzyć aplikacje platformy Azure w programie Visual Studio.

## <a name="create-a-namespace"></a>Tworzenie przestrzeni nazw
Witaj, następnym krokiem jest toocreate przestrzeni nazw usługi i uzyskiwanie klucza dostępu sygnatury dostępu Współdzielonego. Przestrzeń nazw wyznacza granice każdej aplikacji uwidacznianej za pośrednictwem usługi Service Bus. Klucz sygnatury dostępu Współdzielonego jest generowany przez system powitania po utworzeniu przestrzeni nazw. Hello kombinacja przestrzeni nazw i klucza sygnatury dostępu Współdzielonego zapewnia poświadczenia hello usługi Service Bus tooauthenticate dostępu tooan aplikacji.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a>Tworzenie roli sieci Web
W tej sekcji zostanie utworzony hello frontonu aplikacji. Najpierw należy utworzyć hello stron, które będą wyświetlane w aplikacji.
Następnie dodaj kod, który przesyła kolejki usługi Service Bus tooa elementów i wyświetla informacje o stanie dotyczące hello kolejki.

### <a name="create-hello-project"></a>Utwórz projekt hello
1. Korzystając z uprawnień administratora, uruchom program Visual Studio: kliknij prawym przyciskiem myszy hello **programu Visual Studio** ikonę programu, a następnie kliknij przycisk **Uruchom jako administrator**. Witaj emulatora obliczeń platformy Azure, omówiony w dalszej części tego artykułu, wymaga uruchomienia programu Visual Studio z uprawnieniami administratora.
   
   W programie Visual Studio na powitania **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.
2. W pozycji **Zainstalowane szablony** w obszarze **Visual C#** kliknij pozycję **Chmura**, a następnie kliknij pozycję **Usługa w chmurze Azure**. Nazwa projektu hello **MultiTierApp**. Następnie kliknij przycisk **OK**.
   
   ![][9]
3. Wśród ról platformy **.NET Framework 4.5** kliknij dwukrotnie pozycję **Role sieci Web ASP.NET**.
   
   ![][10]
4. Umieść kursor nad **WebRole1** w obszarze **rozwiązania usługi w chmurze Azure**, kliknij ikonę ołówka hello i Zmień nazwę roli sieci web hello zbyt**FrontendWebRole**. Następnie kliknij przycisk **OK**. (Upewnij się, że wpisana nazwa to „Frontend”, pisana przez małe „e”, a nie „FrontEnd”.)
   
   ![][11]
5. Z hello **nowy projekt ASP.NET** okno dialogowe, w hello **wybierz szablon** kliknij **MVC**.
   
   ![][12]
6. Nadal w hello **nowy projekt ASP.NET** okna dialogowego kliknij hello **Zmień uwierzytelnianie** przycisku. W hello **Zmień uwierzytelnianie** okno dialogowe, kliknij przycisk **bez uwierzytelniania**, a następnie kliknij przycisk **OK**. W tym samouczku wdrożysz aplikację, która nie wymaga logowania użytkownika.
   
    ![][16]
7. Po powrocie do hello **nowy projekt ASP.NET** okno dialogowe, kliknij przycisk **OK** toocreate hello projektu.
8. W **Eksploratora rozwiązań**, w hello **FrontendWebRole** projektu, kliknij prawym przyciskiem myszy **odwołania**, następnie kliknij przycisk **Zarządzaj pakietami NuGet**.
9. Kliknij przycisk hello **Przeglądaj** , a następnie wyszukaj `Microsoft Azure Service Bus`. Wybierz hello **WindowsAzure.ServiceBus** pakiet, kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.
   
   ![][13]
   
   Należy zauważyć, że ten hello wymagane zestawy klientów są teraz przywoływane i dodano kilka nowych plików kodu.
10. W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy pozycję **Modele** i kliknij pozycję **Dodaj**, następnie kliknij pozycję **Klasa**. W hello **nazwa** okno, nazwa typu hello **OnlineOrder.cs**. Następnie kliknij pozycję **Dodaj**.

### <a name="write-hello-code-for-your-web-role"></a>Pisanie kodu powitania dla roli sieci web
W tej sekcji utworzysz hello różne strony, które będą wyświetlane w aplikacji.

1. W pliku OnlineOrder.cs hello w programie Visual Studio Zastąp istniejącą definicję przestrzeni nazw hello następującego kodu:
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. W **Eksploratorze rozwiązań** kliknij dwukrotnie pozycję **Controllers\HomeController.cs**. Dodaj następujące hello **przy użyciu** instrukcji u góry hello hello pliku przestrzenie nazw hello tooinclude modelu utworzony, a także usługi Service Bus.
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. Również w pliku HomeController.cs hello w programie Visual Studio, Zastąp istniejącą definicję przestrzeni nazw z hello następującego kodu. Ten kod zawiera metody obsługi przesyłania hello elementów toohello kolejki.
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. Z hello **kompilacji** menu, kliknij przycisk **Kompiluj rozwiązanie** tootest hello dokładność pracy wykonanej do tej pory.
5. Teraz Utwórz widok hello hello `Submit()` została utworzona wcześniej. Kliknij prawym przyciskiem myszy w obrębie hello `Submit()` — metoda (przeciążenia hello `Submit()` który nie przyjmuje żadnych parametrów), a następnie wybierz pozycję **Dodaj widok**.
   
   ![][14]
6. Okno dialogowe tworzenia widoku hello. W hello **szablonu** wybierz **Utwórz**. W hello **klasa modelu** kliknij hello **OnlineOrder** klasy.
   
   ![][15]
7. Kliknij pozycję **Dodaj**.
8. Teraz Zmień nazwę hello wyświetlany w aplikacji. W **Eksploratora rozwiązań**, kliknij dwukrotnie **Views\Shared\\_Layout.cshtml** pliku tooopen go w edytorze programu Visual Studio hello.
9. Zamień wszystkie wystąpienia hasła **My ASP.NET Application** na hasło **LITWARE'S Products**.
10. Usuń hello **Home**, **o**, i **skontaktuj się z** łącza. Usuń hello wyróżniony kod:
    
    ![][28]
11. Na koniec zmodyfikuj hello przesłanie strony tooinclude niektóre informacje na temat hello kolejki. W **Eksploratora rozwiązań**, kliknij dwukrotnie **Views\Home\Submit.cshtml** pliku tooopen go w edytorze programu Visual Studio hello. Dodaj hello następującego wiersza po `<h2>Submit</h2>`. Na razie hello `ViewBag.MessageCount` jest pusta. Wypełnisz ją później.
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. Twój interfejs użytkownika został zaimplementowany. Możesz nacisnąć przycisk **F5** toorun aplikacji i upewnij się, że jej wygląd zgodnie z oczekiwaniami.
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a>Pisanie kodu hello składania kolejki usługi Service Bus tooa elementów
Teraz Dodaj kod przesyłający elementy tooa kolejki. Najpierw utwórz klasę, która zawiera informacje o połączeniu kolejki usługi Service Bus. Następnie zainicjuj połączenie z pliku Global.aspx.cs. Koniec zaktualizuj kod przesyłania hello, utworzony wcześniej w kolejki usługi Service Bus tooa HomeController.cs tooactually przesyłania elementów.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **FrontendWebRole** (kliknij prawym przyciskiem myszy projekt hello, nie hello roli). Kliknij pozycję **Dodaj**, a następnie kliknij pozycję **Klasa**.
2. Nazwa klasy hello **QueueConnector.cs**. Kliknij przycisk **Dodaj** toocreate hello klasy.
3. Teraz Dodaj kod, który hermetyzuje informacje o połączeniu hello i inicjuje kolejki usługi Service Bus tooa połączenia hello. Zastąp całą zawartość pliku QueueConnector.cs hello hello następującego kodu i wprowadź wartości w polach `your Service Bus namespace` (przestrzeni nazw) i `yourKey`, która jest hello **klucz podstawowy** uzyskanym wcześniej z hello Azure Portal.
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. Teraz upewnij się, że wywoływanie metody **Initialize** działa. W **Eksploratorze rozwiązań** kliknij dwukrotnie pozycję **Global.asax\Global.asax.cs**.
5. Dodaj następujące wiersz kodu na końcu hello hello hello **Application_Start** metody.
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. Na koniec zaktualizuj kod sieci web hello został utworzony wcześniej, aby przesłać elementy toohello kolejki. W **Eksploratorze rozwiązań** kliknij dwukrotnie pozycję **Controllers\HomeController.cs**.
7. Aktualizacja hello `Submit()` — metoda (hello przeciążenie, które nie przyjmuje żadnych parametrów) w następujący sposób wiadomość hello tooget liczba hello kolejki.
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. Aktualizacja hello `Submit(OnlineOrder order)` — metoda (hello przeciążenie, które przyjmuje jeden parametr) w następujący sposób toosubmit kolejność informacji toohello kolejki.
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. Teraz możesz uruchomić ponownie aplikację hello. Zwiększa liczbę wiadomości powitania zawsze przesyłania zamówienia.
   
   ![][18]

## <a name="create-hello-worker-role"></a>Tworzenie roli procesu roboczego hello
Teraz utworzysz hello roli procesu roboczego, który przetwarza zgłoszenia zamówień hello. W tym przykładzie użyto hello **roli proces roboczy z kolejką usługi Service Bus** szablon projektu Visual Studio. Witaj wymagane poświadczenia zostały już uzyskane z portalu hello.

1. Upewnij się, że nawiązano połączenie programu Visual Studio tooyour konto platformy Azure.
2. W programie Visual Studio w **Eksploratora rozwiązań** kliknij prawym przyciskiem myszy **ról** folder hello **MultiTierApp** projektu.
3. Kliknij pozycję **Dodaj**, a następnie kliknij pozycję **Nowy projekt roli procesu roboczego**. Witaj **Dodawanie nowego projektu roli** zostanie wyświetlone okno dialogowe.
   
   ![][26]
4. W hello **Dodawanie nowego projektu roli** okno dialogowe, kliknij przycisk **roli proces roboczy z kolejką usługi Service Bus**.
   
   ![][23]
5. W hello **nazwa** okno, nazwa projektu hello **OrderProcessingRole**. Następnie kliknij pozycję **Dodaj**.
6. Skopiuj parametry połączenia hello uzyskany w kroku 9 Schowka toohello sekcji "Tworzenie przestrzeni nazw usługi Service Bus" hello.
7. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **OrderProcessingRole** został utworzony w kroku 5 (Upewnij się, że prawym przyciskiem myszy **OrderProcessingRole** w obszarze **Ról**, a nie hello klasy). Następnie kliknij pozycję **Właściwości**.
8. Na powitania **ustawienia** kartę hello **właściwości** okno dialogowe, kliknij wewnątrz hello **wartość** pole **Microsoft.ServiceBus.ConnectionString**, a następnie wklej skopiowany w kroku 6 wartość punktu końcowego hello.
   
   ![][25]
9. Utwórz **OnlineOrder** klasy toorepresent hello zamówień ich przetwarzania z kolejki hello. Możesz ponownie użyć klasy, która została już utworzona. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **OrderProcessingRole** klasy (ikonę klasy powitania kliknij prawym przyciskiem myszy, nie hello roli). Kliknij pozycję **Dodaj**, a następnie kliknij pozycję **Istniejący element**.
10. Przeglądaj podfolderu toohello **FrontendWebRole\Models**, a następnie kliknij dwukrotnie **OnlineOrder.cs** tooadd on toothis projektu.
11. W **WorkerRole.cs**, zmień wartość hello hello **QueueName** zmienną z `"ProcessingQueue"` zbyt`"OrdersQueue"` pokazane na powitania następującego kodu.
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. Dodaj następujące hello za pomocą instrukcji u góry pliku WorkerRole.cs hello hello.
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. W hello `Run()` funkcja wewnątrz hello `OnMessage()` wywołać, Zastąp zawartość hello hello `try` klauzuli z hello następującego kodu.
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. Aplikacja hello została ukończona. Można przetestować pełnej aplikacji hello, klikając prawym przyciskiem myszy projekt MultiTierApp hello w Eksploratorze rozwiązań, wybierając **Ustaw jako projekt startowy**, a następnie naciśnij klawisz F5. Należy pamiętać, że liczba komunikatów nie zwiększa się, ponieważ hello roli procesu roboczego przetwarza elementy z kolejki hello i oznacza je jako ukończone. Można zobaczyć wyniki śledzenia hello swojej roli procesu roboczego, wyświetlając hello interfejs użytkownika emulatora obliczeń platformy Azure. Aby to zrobić, prawym przyciskiem myszy ikonę emulatora hello w obszarze powiadomień paska zadań hello i wybierając **Pokaż interfejs użytkownika emulatora obliczeń**.
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat usługi Service Bus, zobacz następujące zasoby hello:  

* [Dokumentacja usługi Azure Service Bus][sbdocs]  
* [Service Bus service page][sbacom] (Strona usługi Service Bus)  
* [Jak tooUse kolejek usługi Service Bus][sbacomqhowto]  

toolearn więcej informacji na temat wielowarstwowych scenariuszy, zobacz:  

* [Wielowarstwowa aplikacja platformy .NET korzystająca z tabel, kolejek i obiektów Blob magazynu][mutitierstorage]  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
