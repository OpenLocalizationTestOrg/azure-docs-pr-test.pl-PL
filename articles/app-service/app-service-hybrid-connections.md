---
title: "AAA \"połączeń hybrydowych w usłudze Azure App Service | Dokumentacja firmy Microsoft\""
description: "Jak toocreate i użycia zasobów tooaccess połączeń hybrydowych w różnych sieciach"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 66774bde-13f5-45d0-9a70-4e9536a4f619
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/22/2017
ms.author: ccompy
ms.openlocfilehash: 61d58068ab0a7c803019e3f0e92bde4273d1a053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-hybrid-connections"></a>Połączenia hybrydowe usługi aplikacji Azure #

## <a name="overview"></a>Omówienie ##

Połączenia hybrydowe jest zarówno usługa na platformie Azure, jak i funkcja hello Azure App Service.  Jako usługa ma użycia i możliwości poza tymi, które można wykorzystać w hello Azure App Service.  więcej informacji na temat połączeń hybrydowych i ich użycia poza hello Azure App Service można uruchomić w tym miejscu toolearn [połączeń hybrydowych przekaźnika usługi Azure][HCService]

W usłudze Azure App Service hello połączeń hybrydowych może być używane tooaccess zasobów aplikacji w innych sieciach. Zapewnia dostęp z punkt końcowy aplikacji tooan aplikacji.  Tooaccess alternatywnych możliwości nie umożliwia aplikacji.  Jak używane w hello App Service, każde połączenie hybrydowe są powiązane z tooa jednego hosta i portu kombinacji TCP.  Oznacza to, że tego punktu końcowego połączenia hybrydowe hello może być dowolnego systemu operacyjnego i aplikacji pod warunkiem że czy osiągnięto port nasłuchiwania protokołu TCP. Połączeń hybrydowych znasz lub zależy, jakie protokół aplikacji hello jest lub co chcesz uzyskać dostęp.  Po prostu zapewnia dostęp do sieci.  


## <a name="how-it-works"></a>Jak to działa ##
Funkcja połączenia hybrydowe Hello składa się z dwóch wychodzący tooService przekaźnik magistrali.  Brak połączenia z biblioteki na hoście hello, gdy aplikacja działa w usłudze aplikacji hello i następnie istnieje połączenie z hello Manager(HCM) połączenia hybrydowe tooService magistrali przekazywania.  usługi przekazywania, który można wdrożyć w ramach hosting sieci hello jest Hello HCM 

Za pomocą hello dwa połączone połączenia aplikacja ma tooa tunelu TCP stałej kombinacja hosta: port. na powitania drugiej stronie powitania HCM.  połączenie Hello używa protokołu TLS 1.2, zabezpieczeń i klucze sygnatury dostępu Współdzielonego dla uwierzytelniania/autoryzacji.    

![][1]

Gdy aplikacja wysyła żądanie DNS, które odpowiadają punktu końcowego połączenia hybrydowego Konfigurowanie, a następnie ruch wychodzący TCP hello nastąpi przekierowanie w dół hello połączenia hybrydowego.  

> [!NOTE]
> Oznacza to, że należy spróbować tooalways Użyj nazwy DNS dla połączenia hybrydowego.  Niektóre oprogramowanie klienckie nie wyszukiwania DNS, jeśli zamiast tego punktu końcowego hello korzysta z adresu IP.
>
>

Istnieją dwa typy połączeń hybrydowych było możliwe, hello nowych połączeń hybrydowych mogą używać jako usługa przekaźnika usługi Azure, które hello starsze połączeń hybrydowych BizTalk.  Hello starsze połączeń hybrydowych BizTalk są określonego tooas klasycznego połączeń hybrydowych w portalu hello.  Ma więcej informacji w dalszej części tego dokumentu o nich.

### <a name="app-service-hybrid-connection-benefits"></a>Korzyści połączenia hybrydowe usługi aplikacji ###

Istnieje wiele korzyści toohello hybrydowego połączenia możliwości, w tym

- Aplikacje mogą bezpiecznie uzyskiwać dostęp do systemów lokalnych i usług bezpiecznie
- Funkcja Hello nie wymaga dostępnym punkcie końcowym internet
- jest szybkie i łatwe tooset w górę  
- Kombinacja pojedynczego hosta: port. tooa, która jest elementem znakomity zabezpieczeń odpowiada każdego połączenia hybrydowego
- zwykle nie wymaga luk Zapora połączenia hello są wszystkie wychodzących za pośrednictwem portów standardowe sieci web
- ponieważ funkcja hello jest również oznacza, że jest używany przez aplikację i hello technologii używanych przez punkt końcowy hello języka toohello o niesprecyzowanym poziom sieci
- może być używany w wielu sieciach z jednej aplikacji tooprovide dostępu 

### <a name="things-you-cannot-do-with-hybrid-connections"></a>Czynności, które nie można wykonywać z połączeń hybrydowych ###

Istnieje kilka rzeczy, które nie można wykonać za pomocą połączeń hybrydowych było możliwe, i zawierają:

- zainstalowanie dysku
- przy użyciu protokołu UDP
- Uzyskiwanie dostępu do TCP na podstawie usług, które używają portów dynamicznych, takie jak FTP w trybie pasywnym lub w trybie pasywnym rozszerzone
- Obsługa protokołu LDAP, ponieważ czasami wymaga protokołu UDP
- Obsługa Active Directory

## <a name="adding-and-creating-a-hybrid-connection-in-your-app"></a>Dodawanie i tworzenie połączenia hybrydowego w aplikacji ##

Można tworzyć połączeń hybrydowych było możliwe za pośrednictwem portalu aplikacji hello lub z portalu hello połączenia hybrydowego.  Zdecydowanie zaleca się używanie hello toocreate portalu aplikacji hello połączeń hybrydowych mają toouse z aplikacją.  toocreate połączenie hybrydowe Przejdź toohello [portalu Azure] [ portal] i przejdź do hello interfejsu użytkownika dla aplikacji.  Wybierz **sieci > skonfiguruj punkty końcowe połączenia hybrydowego**.  W tym miejscu można wyświetlić hello połączeń hybrydowych, które są skonfigurowane przy użyciu aplikacji  

![][2]

tooadd nowe połączenie hybrydowe, kliknij przycisk Dodaj połączenie hybrydowe.  Witaj interfejsu użytkownika, który zostaje otwarty zawiera listę połączeń hybrydowych hello, które zostały już utworzone.  tooadd co najmniej jeden z nich tooyour aplikacji, kliknij na powitania te mają i naciśnij **Dodaj wybrane połączenie hybrydowe**.  

![][3]

Toocreate nowe połączenie hybrydowe, kliknij przycisk **Utwórz nowe połączenie hybrydowe**.  W tym miejscu można określić: 

- Nazwa punktu końcowego
- Nazwa hosta punktu końcowego
- Port punktu końcowego
- przestrzeń nazw magistrali usług mają toouse

![][4]

Co połączenia hybrydowego jest wiązana tooa przestrzeń nazw magistrali usług i każda przestrzeń nazw magistrali usług jest w region platformy Azure.  Jest ważne tootry i użyj przestrzeni nazw w magistrali usługi hello tym samym regionie co aplikacja tak opóźnienia sieci powstaniu tooavoid.

Jeśli chcesz tooremove połączenie hybrydowe z aplikacji, kliknij prawym przyciskiem go i wybierz **rozłączenia**.  

Po dodaniu aplikacji sieci web tooyour połączenie hybrydowe można wyświetlić szczegółowe informacje na jego, po prostu kliknij go.  

![][5]

## <a name="hybrid-connections-and-app-service-plans"></a>Połączenia hybrydowe i planów usługi aplikacji ##

Witaj tylko połączeń hybrydowych było możliwe, możesz teraz wprowadzić są hello nowych połączeń hybrydowych było możliwe.  Tylko są dostępne w Basic, Standard i Premium izolowany cennik jednostki SKU.  Brak toohello limity powiązane cenową planu.  

| Cennik planu | Liczba połączeń hybrydowych można używać w planie hello |
|----|----|
| Podstawowa | 5 |
| Standardowa | 25 |
| Premium | 200 |
| Izolowane | 200 |

Ponieważ istnieją ograniczenia planu usługi App Service jest również interfejsu użytkownika w hello Plan usługi aplikacji, który pokazuje, jak wiele połączeń hybrydowych są używane i jakie aplikacje.  

![][6]

Podobnie jak z widokiem aplikacji hello, można wyświetlić szczegółowe informacje na połączenie hybrydowe, klikając go.  We właściwościach hello tutaj pokazano wszystkie informacje hello miały w widoku aplikacji hello jest widoczne, ale można również sprawdzić, jak wiele innych aplikacji hello tego samego planu usługi App Service korzystają z tego połączenia hybrydowego.

![][7]

Gdy istnieje limit liczby hello punkty końcowe połączenia hybrydowego, które mogą być używane w planie usługi aplikacji, każde połączenie hybrydowe używane można w dowolnej liczby aplikacji w tym planie usługi aplikacji.  To toosay gdyby 1 połączenia hybrydowego używany w 5 osobnych aplikacji w mojej planu usługi App Service, która jest nadal tylko 1 połączenia hybrydowego.

Brak dodatkowych kosztów połączeń toohybrid poza trwa tylko w Basic, Standard, Premium lub izolowane jednostki SKU.  Dla informacji o cenach połączenia hybrydowe przejdź tutaj: [cennik usługi Service Bus][sbpricing].

## <a name="hybrid-connection-manager"></a>Menedżera połączeń hybrydowych ##

Aby toowork połączeń hybrydowych należy agenta przekazywania w sieci hello, który jest hostem punktu końcowego połączenia hybrydowego.  Agent przekazywania jest nazywany hello Menedżera połączeń hybrydowych (HCM).  To narzędzie można pobrać z hello **sieci > skonfiguruj punkty końcowe połączenia hybrydowego** interfejsu użytkownika dostępne z aplikacji w hello [portalu Azure][portal].  

To narzędzie jest uruchamiane w systemie Windows server 2008 R2 i nowszych wersjach systemu Windows.  Po zainstalowaniu hello HCM działa jako usługa.  Ta usługa łączy przekaźnik magistrali usług tooAzure oparte na punktach końcowych hello skonfigurowane.  Witaj połączenia z hello HCM są wychodzących tooports 80 i 443.    

Witaj HCM ma tooconfigure interfejsu użytkownika go.  Po hello HCM jest zainstalowana można uzupełnić hello interfejsu użytkownika, uruchamiając hello HybridConnectionManagerUi.exe, który znajduje się w katalogu instalacyjnego hello Menedżera połączeń hybrydowych.  Jest także łatwo osiągnął w systemie Windows 10, wpisując *interfejsu użytkownika Menedżera połączeń hybrydowych* w polu wyszukiwania.  

Po uruchomieniu HCM interfejsu użytkownika, powitalne hello po pierwsze można znaleźć jest tabelę, która zawiera listę wszystkich połączeń hybrydowych hello, które zostały skonfigurowane dla tego wystąpienia hello HCM.  Jeśli chcesz toomake wszelkie zmiany, konieczne będzie tooauthenticate z platformy Azure. 

tooadd jeden lub więcej połączeń hybrydowych tooyour HCM:

1. Uruchom hello HCM interfejsu użytkownika
1. Kliknij przycisk Konfiguruj innego połączenia hybrydowego![][8]

1. Zaloguj się przy użyciu konta platformy Azure
1. Wybieranie subskrypcji
1. Kliknij na powitania połączeń hybrydowych ma to toorelay HCM![][9]

1. Klikanie pozycji Zapisz.

W tym momencie zostanie wyświetlony połączeń hybrydowych hello dodane.  Można również kliknij połączenie hybrydowe hello skonfigurowane i zobaczyć szczegółowe informacje dotyczące połączenia hello.

![][10]

HCM toobe toosupport stanie hello hybrydowego połączeń jest skonfigurowany z musi:

- TCP tooAzure dostępu przez porty 80 i 443
- Punkt końcowy protokołu TCP dostępu toohello hybrydowego połączenia
- możliwość toodo DNS wyszukiwań na powitania hosta punktu końcowego i przestrzeni nazw magistrali usług azure hello

Witaj HCM obsługuje zarówno nowych połączeń hybrydowych, jak i hello starsze BizTalk połączeń hybrydowych było możliwe.

### <a name="redundancy"></a>Nadmiarowość ###

Każdy HCM może obsługiwać wiele połączeń hybrydowych.  Ponadto każde połączenie hybrydowe danego mogą być obsługiwane przez wiele HCMs.  zachowanie domyślne Hello jest tooround działania okrężnego ruchu między hello skonfigurowane HCMs dla dowolnego danego punktu końcowego.  Jeśli chcesz wysokiej dostępności połączeń hybrydowych z sieci, po prostu utworzyć wystąpienia wielu HCMs na oddzielnych komputerach. 

### <a name="manually-adding-a-hybrid-connection"></a>Ręcznie dodać połączenie hybrydowe ###

Jeśli chcesz ktoś poza toohost Twojej subskrypcji dla połączenia hybrydowe danego wystąpienia HCM, można udostępniać je hello parametry połączenia bramy hello połączenia hybrydowego.  Zobacz ten we właściwościach hello połączenia hybrydowe w hello [portalu Azure][portal]. toouse, że ciąg znaków, kliknij przycisk hello **ręcznie skonfigurować** przycisk na powitania HCM i Wklej parametry połączenia bramy hello.


## <a name="troubleshooting"></a>Rozwiązywanie problemów ##

Podczas połączenia hybrydowe została skonfigurowana z uruchomioną aplikację i istnieje co najmniej jeden HCM, który ma skonfigurowane połączenie hybrydowe, a następnie dowiesz się, stan hello **połączony** w portalu hello.  Jeśli nie powiedzieć **połączony** oznacza to, że aplikacja nie działa lub Twoje HCM nie może połączyć się tooAzure na porty 80 i 443.  

podstawowym powodem Hello, że klienci nie mogą łączyć tootheir punktu końcowego jest ponieważ hello punkt końcowy został określony przy użyciu adresu IP zamiast nazwy DNS.  Jeśli aplikacja nie może połączyć się hello żądanego punktu końcowego i adres IP jest używany, Przełącz toousing nazwy DNS, która jest prawidłowa na hoście hello, w którym hello HCM jest uruchomiona.  Inne rzeczy toocheck to tego hello nazwy DNS rozpoznaje poprawnie na hoście hello gdzie hello HCM działa i że ma łączności z hosta hello, w którym hello HCM działa punktu końcowego połączenia hybrydowe toohello.  

W hello usługi aplikacji, która może być wywoływany z konsoli hello o nazwie tcpping znajduje się narzędziem.  To narzędzie można stwierdzić, jeśli masz punkt końcowy protokołu TCP tooa dostępu, ale właściwość nie określa, czy masz dostęp do punktu końcowego połączenia hybrydowe dla tooa.  W przypadku używania w konsoli hello względem punktu końcowego połączenia hybrydowe, pomyślne polecenie ping tylko informuje czy masz połączenie hybrydowe skonfigurowane dla twojej aplikacji, który używa tej kombinacji hosta: port.  

## <a name="biztalk-hybrid-connections"></a>Połączenia hybrydowe BizTalk ##

Wyłącz tworzenie połączenia hybrydowego BizTalk toofurther został zamknięty Hello starsze możliwości usług BizTalk — wersja połączeń hybrydowych było możliwe.  Nadal korzystać z istniejących połączeń hybrydowych BizTalk z aplikacjami, ale należy zmigrować toohello nowej usługi.  Witaj zalet hello nową usługę BizTalk hello w wersji należą:

- żadne dodatkowe konto usług BizTalk — wersja nie jest wymagane
- Protokół TLS to 1.2 zamiast 1.0 jak połączeń hybrydowych BizTalk
- Komunikacja odbywa się za pośrednictwem portów 80 i 443 przy użyciu tooreach nazwy DNS Azure zamiast adresów IP i zakres dodatkowych inne porty.  

tooadd BizTalk hybrydowego połączenia tooyour aplikacji, aplikacji tooyour Przejdź w hello [portalu Azure] [ portal] i kliknij przycisk **sieci > skonfiguruj punkty końcowe połączenia hybrydowego**.  W tabeli połączeń hybrydowych Classic powitania kliknij **Dodaj połączenie hybrydowe klasycznego**.  W tym miejscu zostanie wyświetlona lista połączeń hybrydowych BizTalk.  


<!--Image references-->
[1]: ./media/app-service-hybrid-connections/hybridconn-connectiondiagram.png
[2]: ./media/app-service-hybrid-connections/hybridconn-portal.png
[3]: ./media/app-service-hybrid-connections/hybridconn-addhc.png
[4]: ./media/app-service-hybrid-connections/hybridconn-createhc.png
[5]: ./media/app-service-hybrid-connections/hybridconn-properties.png
[6]: ./media/app-service-hybrid-connections/hybridconn-aspproperties.png
[7]: ./media/app-service-hybrid-connections/hybridconn-hcm.png
[8]: ./media/app-service-hybrid-connections/hybridconn-hcmadd.png
[9]: ./media/app-service-hybrid-connections/hybridconn-hcmadded.png
[10]: ./media/app-service-hybrid-connections/hybridconn-hcmdetails.png

<!--Links-->
[HCService]: http://docs.microsoft.com/azure/service-bus-relay/relay-hybrid-connections-protocol/
[portal]: http://portal.azure.com/
[oldhc]: http://docs.microsoft.com/azure/biztalk-services/integration-hybrid-connection-overview/
[sbpricing]: http://azure.microsoft.com/pricing/details/service-bus/

