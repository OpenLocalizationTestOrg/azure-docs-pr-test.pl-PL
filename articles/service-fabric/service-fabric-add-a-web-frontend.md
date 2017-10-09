---
title: "aaaCreate frontonu sieci web dla aplikacji sieci szkieletowej usług Azure przy użyciu platformy ASP.NET Core | Dokumentacja firmy Microsoft"
description: "Udostępnianie sieci web toohello aplikacji sieci szkieletowej usług za pomocą platformy ASP.NET Core projektu i komunikacja między usługami komunikacji za pośrednictwem komunikacji zdalnej usługi."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a>Tworzenie frontonu sieci web usługi aplikacji przy użyciu platformy ASP.NET Core
Domyślnie usługi sieć szkieletowa usług Azure nie udostępniają toohello publiczny interfejs sieci web. tooexpose klientów tooHTTP funkcji aplikacji, masz toocreate sieci web projektu tooact jako punkt wejścia, a następnie komunikować się z tooyour występują poszczególnych usług.

W tym samouczku będziemy uruchomienia instalacji gdzie możemy przerwał pracę w hello [tworzenie pierwszej aplikacji w programie Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) samouczka i Dodaj usługę sieci web platformy ASP.NET Core przed hello usługi stanowej licznika. Jeśli jeszcze nie możesz wrócić do poprzedniej strony i najpierw kroków opisanych w tym samouczku.

## <a name="set-up-your-environment-for-aspnet-core"></a>Konfigurowanie środowiska dla platformy ASP.NET Core

Należy toofollow programu Visual Studio 2017 wraz z tego samouczka. Dowolna wersja będzie wykonywać. 

 - [Zainstaluj program Visual Studio 2017 r.](https://www.visualstudio.com/)

toodevelop aplikacji platformy ASP.NET Core Service Fabric, powinny mieć powitania po obciążeń zainstalowane:
 - **Programowanie Azure** (w obszarze *sieci Web & chmurze*)
 - **ASP.NET i sieć web development** (w obszarze *sieci Web & chmurze*)
 - **Programowanie wieloplatformowych .NET core** (w obszarze *inne procesami*)

>[!Note] 
>Witaj .NET Core tools dla programu Visual Studio 2015 są już aktualizowany, jednak są nadal przy użyciu programu Visual Studio 2015, konieczne będzie toohave [.NET Core VS 2015 narzędzi Preview 2](https://www.microsoft.com/net/download/core) zainstalowane.

## <a name="add-an-aspnet-core-service-tooyour-application"></a>Dodawanie aplikacji ASP.NET Core tooyour usługi
Platformy ASP.NET Core to platforma programistyczna lekka międzyplatformowa sieci web można używać nowoczesnych toocreate interfejsu użytkownika sieci web i interfejsów API sieci web. 

Dodajmy istniejącej aplikacji tooour projektu interfejsu API sieci Web platformy ASP.NET.

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **usług** poziomu projekt aplikacji hello i wybierz polecenie **Dodaj > Nowa usługa sieci szkieletowej usług**.
   
    ![Dodawanie nowej usługi tooan istniejącej aplikacji][vs-add-new-service]
2. Na powitania **Tworzenie usługi** wybierz pozycję **platformy ASP.NET Core** i nadaj mu nazwę.
   
    ![Wybieranie usługi sieci web ASP.NET w oknie dialogowym hello nowej usługi][vs-new-service-dialog]

3. Witaj następnej strony zawiera zestaw platformy ASP.NET Core szablonów projektu. Należy pamiętać, że te są hello sama usługa ze środowiskiem uruchomieniowym usługi sieć szkieletowa hello hello wyborów, że można zobaczyć został utworzony projekt platformy ASP.NET Core poza aplikacją sieci szkieletowej usług z małej ilości tooregister dodatkowy kod. W tym samouczku, wybierz **interfejsu API sieci Web**. Jednak możesz zastosować hello tego samego pojęcia toobuilding aplikacji sieci web pełna.
   
    ![Wybieranie typu projektu programu ASP.NET][vs-new-aspnet-project-dialog]
   
    Po utworzeniu projektu interfejsu API sieci Web powinien mieć dwie usługi aplikacji. Kontynuując toobuild aplikacji, można dodać więcej usług w hello dokładnie tak samo. Każdy może być niezależnie określonej wersji, jak i uaktualnionych.

## <a name="run-hello-application"></a>Uruchamianie aplikacji hello
tooget zorientować się, co możemy wykonane, umożliwia wdrażanie nowej aplikacji hello i podejmij zapewnia przyjrzeć się hello domyślne zachowanie hello szablonu interfejsu API platformy ASP.NET Core sieci Web.

1. Naciśnij klawisz F5 w programie Visual Studio toodebug hello aplikacji.
2. Po zakończeniu wdrożenia programu Visual Studio uruchamia głównego toohello przeglądarki z hello usługi interfejsu API sieci Web ASP.NET. Hello Web API platformy ASP.NET Core szablonu nie udostępniają domyślne zachowanie dla elementu głównego hello, więc powinna zostać wyświetlona w przeglądarce hello błąd 404.
3. Dodaj `/api/values` toohello lokalizacji w przeglądarce hello. Wywołuje to hello `Get` metody na powitania ValuesController hello szablonu interfejsu API sieci Web. Zwraca odpowiedź domyślna hello dostarczone przez szablon hello — tablicy JSON, który zawiera dwa ciągi:
   
    ![Wartości domyślne zwrócony z interfejsu API platformy ASP.NET Core sieci Web szablonu][browser-aspnet-template-values]
   
    Hello koniec samouczka hello ta strona wyświetli hello najbardziej aktualną wartość licznika z naszej usługi stanowej zamiast hello domyślne parametry.

## <a name="connect-hello-services"></a>Połączenie usług hello
Sieć szkieletowa usług oferuje pełną elastyczność w sposób komunikowania się z usługami reliable services. Wewnątrz aplikacji konieczne może być usług, które są dostępne za pośrednictwem protokołu TCP, innych usług, które są dostępne za pośrednictwem interfejsu API REST protokołu HTTP i nadal innych usług, które są dostępne za pośrednictwem gniazda sieci web. W tle na dostępne opcje hello oraz kompromisy hello zaangażowany, zobacz [komunikacji z usługami](service-fabric-connect-and-communicate-with-services.md). W tym samouczku używamy [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), podany w hello zestawu SDK.

W hello podejście Service Remoting (zaprojektowany na zdalnych wywołań procedur lub RPC) można zdefiniować jako hello publicznego kontraktu usługi hello tooact interfejsu. Następnie należy użyć tego toogenerate interfejsu klasy serwera proxy do interakcji z usługą hello.

### <a name="create-hello-remoting-interface"></a>Tworzenie interfejsu usług zdalnych hello
Zacznijmy od utworzenia tooact interfejsu hello jako kontraktu hello między usługi stanowej hello i innych usług, w tym wielkość hello projektu sieci web platformy ASP.NET Core. Ten interfejs musi być współużytkowane przez wszystkie usługi, które go używają toomake wywołania RPC, dlatego utworzymy własnego projektu biblioteki klas.

1. W Eksploratorze rozwiązań kliknij rozwiązanie prawym przyciskiem myszy i wybierz polecenie **Dodaj** > **nowy projekt**.

2. Wybierz hello **Visual C#** wpisu w hello lewego okienka nawigacji i wybierz opcję hello **biblioteki klas** szablonu. Upewnij się, ta wersja .NET Framework hello ustawiono zbyt**4.5.2**.
   
    ![Tworzenie projektu interfejsu usługi stanowej][vs-add-class-library-project]

3. Zainstaluj hello **Microsoft.ServiceFabric.Services.Remoting** pakietu NuGet. Wyszukaj **Microsoft.ServiceFabric.Services.Remoting** w hello NuGet pakietu manager, a następnie zainstaluj go dla wszystkich projektów w rozwiązaniu hello korzystających Service Remoting, w tym:
   - Projekt biblioteki klas Hello, który zawiera hello interfejsu usługi
   - projekt usługi Stateful Hello
   - Witaj projekt usługi sieci web platformy ASP.NET Core
   
    ![Dodawanie pakietu NuGet usługi hello][vs-services-nuget-package]

4. W bibliotece klas hello, Tworzenie interfejsu z jedną metodę `GetCountAsync`, i rozszerzenie interfejsu hello `Microsoft.ServiceFabric.Services.Remoting.IService`. interfejsu usług zdalnych Hello musi pochodzić od tooindicate tego interfejsu, jest interfejsem Service Remoting.
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-hello-interface-in-your-stateful-service"></a>Implementowanie interfejsu hello w usłudze stanowe
Teraz, gdy zdefiniowaniu hello interfejsu, potrzebujemy tooimplement w usługi stanowej hello.

1. W usłudze stanowe dodać projektu biblioteki klas toohello odwołania, zawierający hello interfejsu.
   
    ![Dodawanie odwołania projektu biblioteki klas toohello w hello usługi stanowej][vs-add-class-library-reference]
2. Zlokalizuj hello klasy, która dziedziczy `StatefulService`, takich jak `MyStatefulService`i rozszerzyć ją tooimplement hello `ICounter` interfejsu.
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. Teraz wdrożyć hello pojedynczej metody, która jest zdefiniowana w hello `ICounter` interfejsu `GetCountAsync`.
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a>Udostępnianie hello usługi stanowej przy użyciu odbiornika usługi zdalne usługi
Z hello `ICounter` interfejsu zaimplementowanego, ostatnim krokiem hello jest kanał komunikacyjny Service Remoting hello tooopen. Usługi stanowej, Usługa Service Fabric realizuje z możliwością przesłonięcia metody o nazwie `CreateServiceReplicaListeners`. Przy użyciu tej metody można określić odbiorników komunikacji, na podstawie typu hello komunikacji mają tooenable dla usługi.

> [!NOTE]
> wywoływana jest metoda równoważne Hello otwierania usług toostateless kanał komunikacji `CreateServiceInstanceListeners`.

W takim przypadku możemy zastąpić istniejący hello `CreateServiceReplicaListeners` — metoda i zapewnić wystąpienie `ServiceRemotingListener`, co powoduje z punktem końcowym które jest wywoływane z klientów za pośrednictwem `ServiceProxy`.  

Witaj `CreateServiceRemotingListener` — metoda rozszerzenia na powitania `IService` interfejs umożliwiający tooeasily utworzyć `ServiceRemotingListener` przy użyciu wszystkich ustawień domyślnych. toouse tej metody rozszerzenia, upewnij się, masz hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` zaimportowane przestrzeni nazw. 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a>Witaj ServiceProxy klasy toointeract za pomocą usługi hello
Nasza usługa stanowa jest teraz gotowy tooreceive ruchu z innych usług za pośrednictwem wywołania RPC. Związku z czym jej pozostaje polega na dodaniu hello toocommunicate kodu z nim z hello usługi sieci web ASP.NET.

1. W projekcie platformy ASP.NET, należy dodać odwołanie do biblioteki klas toohello zawierający hello `ICounter` interfejsu.

2. Wcześniej dodane hello **Microsoft.ServiceFabric.Services.Remoting** projektu ASP.NET toohello pakietu NuGet. Ten pakiet zawiera hello `ServiceProxy` klasy, które zostaną użyte usługi stanowej toohello wywołuje toomake RPC. Upewnij się, że ten pakiet NuGet jest zainstalowane na powitania projekt usługi sieci web platformy ASP.NET Core.

4. W hello **kontrolerów** folder, otwórz hello `ValuesController` klasy. Należy pamiętać, że hello `Get` metoda obecnie tylko zwraca tablicę ustalony ciąg "wartość1" i "wartość2"--odpowiadającego widzieliśmy wcześniej w przeglądarce hello. Zastąp tę implementację hello następującego kodu:
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    pierwszy wiersz kodu Hello jest hello klucz. toocreate hello ICounter proxy toohello usługi stanowej, należy tooprovide dwa rodzaje informacji: Nazwa partycji identyfikator i hello hello usługi.
   
    Można użyć partycjonowania usługi stanowej tooscale przez podzielenie ich stan w różnych zasobników, oparte na kluczu zdefiniowana, takich jak identyfikator klienta lub kod pocztowy. W naszym prostej aplikacji hello usługi stanowej ma tylko jedną partycję, tak hello klucza nie ma znaczenia. Dowolny klawisz, który podasz doprowadzi toohello tej samej partycji. toolearn więcej informacji na temat partycjonowania usług, zobacz [jak toopartition niezawodne usługi sieć szkieletowa usług](service-fabric-concepts-partitioning.md).
   
    Nazwa usługi Hello jest identyfikatorem URI hello formularza w sieci szkieletowej: /&lt;nazwa_aplikacji&gt;/&lt;service_name&gt;.
   
    Z tych dwóch rodzajów informacji usługi sieć szkieletowa może jednoznacznie zidentyfikować maszyny hello, które powinny być wysyłane żądania. Witaj `ServiceProxy` klasa również bezproblemowo obsługuje hello na wtedy, gdy wystąpi awaria maszyny hello, który jest hostem partycji usługi stanowej hello i inną maszynę musi być awansowana tootake jego miejscu. Ta warstwa abstrakcji udostępnia pisania hello toodeal kod klienta z innymi usługami znacznie prostsze.
   
    Po mamy powitania serwera proxy, po prostu Wywołaj firma Microsoft hello `GetCountAsync` metodę i zwraca jego wynik.

5. Naciśnij klawisz F5, ponownie toorun hello zmodyfikował aplikację. Jako przed, Visual Studio automatycznie uruchamia hello przeglądarki toohello katalog główny projektu sieci web hello. Dodaj ścieżkę "interfejsu api/values" hello, a powinien zostać wyświetlony hello zwrócił bieżącą wartość licznika.
   
    ![wartość licznika stanowe Hello wyświetlany w przeglądarce hello][browser-aspnet-counter-value]
   
    Odśwież przeglądarkę hello okresowo toosee hello licznika wartość aktualizacji.

## <a name="kestrel-and-weblistener"></a>Kestrel i WebListener

Witaj domyślnego serwera sieci web platformy ASP.NET Core, znany jako Kestrel, jest [nie są obecnie obsługiwane za obsługę ruchu internetowego bezpośredniego](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel). W związku z tym hello szablonu usługi bezstanowej platformy ASP.NET Core dla sieci szkieletowej usług używa [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) domyślnie. 

toolearn więcej informacji na temat Kestrel i WebListener w usługach sieci szkieletowej usług można znaleźć zbyt[platformy ASP.NET Core w usługach niezawodnej usługi sieć szkieletowa](service-fabric-reliable-services-communication-aspnetcore.md).

## <a name="connecting-tooa-reliable-actor-service"></a>Łączenie usługi niezawodnego aktora tooa
Ten samouczek koncentruje się na dodanie frontonu sieci web, które komunikowały się z usługi stanowej. Można jednak wykonać bardzo podobne tooactors tootalk modelu. Podczas tworzenia projektu niezawodnego aktora Visual Studio automatycznie generuje projektu interfejsu. Można tego interfejsu toogenerate proxy aktora w toocommunicate projektu sieci web hello z aktorem hello. kanał komunikacyjny Hello jest dostarczany automatycznie. Więc nie trzeba toodo wszystko to odpowiednik tooestablishing `ServiceRemotingListener` jak dla usługi stanowej hello w tym samouczku.

## <a name="how-web-services-work-on-your-local-cluster"></a>Jak działają usługi sieci web w klastrze lokalnym
Ogólnie rzecz biorąc można wdrożyć dokładnie hello tej samej sieci szkieletowej usług aplikacji tooa wielu maszyny klastra, że można wdrożyć w klastrze lokalnym i można zdecydowanie pewność, że działa zgodnie z oczekiwaniami. Jest to spowodowane klaster lokalny jest po prostu konfigurację pięcioma węzłami, w której jest zwinięty tooa jednego komputera.

Po przejściu do usługi tooweb, istnieje jednak jeden nuance klucza. Gdy klaster znajduje się za usługą równoważenia obciążenia, jak ma na platformie Azure, musi zapewnić, że usługi sieci web są wdrażane na każdym komputerze od modułu równoważenia obciążenia powitania po prostu okrężne ruchu między maszynami hello. Można to zrobić przez ustawienie hello `InstanceCount` hello usługi toohello specjalne wartości "-1".

Z kolei po uruchomieniu usługi sieci web lokalnie, należy tooensure tego tylko jedno wystąpienie usługi hello jest uruchomiona. W przeciwnym razie wystąpiły konflikty z wielu procesów, które nasłuchują na powitania sama ścieżka i portu. W związku z tym liczba wystąpień usługi sieci web hello należy ustawić także wartość "1" dla wdrożenia lokalnego.

toolearn tooconfigure różne wartości dla innego środowiska, zobacz temat [Zarządzanie parametry aplikacji dla wielu środowiskach](service-fabric-manage-multiple-environment-app-configuration.md).

## <a name="next-steps"></a>Następne kroki
Teraz, gdy masz z przodu web przechodzili zestaw aplikacji z platformy ASP.NET Core, Dowiedz się więcej o [platformy ASP.NET Core w usługach niezawodnej usługi sieć szkieletowa](service-fabric-reliable-services-communication-aspnetcore.md) dla dobrej znajomości sposobu platformy ASP.NET Core współpracuje z sieci szkieletowej usług.

Następnie [Dowiedz się więcej o komunikacji z usługami](service-fabric-connect-and-communicate-with-services.md) ogólnie tooget a pełny obraz z jak usługi komunikacji działa w sieci szkieletowej usług.

Po utworzeniu dobrą znajomością działania komunikacji usług [utworzyć klaster na platformie Azure i wdrażanie aplikacji chmury toohello](service-fabric-cluster-creation-via-portal.md).

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
