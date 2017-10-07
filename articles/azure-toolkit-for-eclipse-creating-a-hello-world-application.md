---
title: "aaaCreate Hello World usługi w chmurze dla platformy Azure w programie Eclipse"
description: "Dowiedz się, jak toocreate proste using aplikacji Hello World hello zestawu narzędzi platformy Azure dla programu Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 7262e705-59d6-43ce-b888-29a21c8e0cb7
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: dfb81374aaf78e933c0bf83a1dbd98023801491a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-hello-world-cloud-service-for-azure-in-eclipse"></a>Utwórz Hello World usługą w chmurze dla platformy Azure w programie Eclipse
Witaj poniższej procedurze pokazano, jak toocreate i wdrażania podstawowych tooAzure aplikację JSP przy użyciu hello Azure zestawu narzędzi dla programu Eclipse. Przykład JSP jest widoczna dla uproszczenia, ale bardzo podobne kroki będzie odpowiednia dla serwlet Java, jakim jest dotyczy wdrożenia usługi Azure.

Aplikacja Hello będzie wyglądać podobnie toohello następujące:

![][ic600360]

## <a name="prerequisites"></a>Wymagania wstępne
* Java Developer Kit (JDK), v 1.7 lub nowszej.
* Zaćmienie-IDE for Java EE Developers indygo lub nowszej. Ten można pobrać z <http://www.eclipse.org/downloads/>.
* Dystrybucja serwera sieci web opartych na języku Java lub serwera aplikacji, takich jak Apache Tomcat, GlassFish, serwer aplikacji JBoss, Jetty lub IBM® WebSphere® aplikacji Server Liberty Core.
* Subskrypcję platformy Azure, która może zostać pobrany z <http://azure.microsoft.com/pricing/purchase-options/>.
* Witaj zestawu narzędzi platformy Azure dla programu Eclipse. Aby uzyskać więcej informacji, zobacz [hello Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse][Installing hello Azure Toolkit for Eclipse].

## <a name="toocreate-a-hello-world-application"></a>toocreate aplikacji Hello World
Po pierwsze Zaczniemy tworzenia projektu języka Java.

1. Uruchom środowisko Eclipse, a następnie w menu powitania kliknij **pliku**, kliknij przycisk **nowy**, a następnie kliknij przycisk **dynamiczny projekt sieci Web**. (Jeśli nie widzisz **dynamiczny projekt sieci Web** wymienione jako projekt dostępne po kliknięciu przycisku **pliku**, **nowy**, następnie hello następujące: kliknij **pliku**, kliknij przycisk **nowy**, kliknij przycisk **projektu...** , rozwiń węzeł **Web**, kliknij przycisk **dynamiczny projekt sieci Web**i kliknij przycisk **dalej**.)

1. Do celów tego samouczka, nazwa projektu hello **MyHelloWorld**. (Upewnij się, możesz użyć tej nazwy, kolejne kroki w tym samouczku oczekiwać Twojej toobe pliku WAR o nazwie MyHelloWorld). Na ekranie pojawi się podobne toohello następujące:

   ![][ic589576]

1. Kliknij przycisk **Zakończ**.

1. W widoku Eksplorator projektów w środowisku Eclipse, rozwiń węzeł **MyHelloWorld**. Kliknij prawym przyciskiem myszy folder **WebContent**, kliknij polecenie **New** (Nowy), a następnie kliknij polecenie **JSP File** (Plik JSP).

1. W hello **New JSP File** okno dialogowe, nazwa pliku hello **index.jsp**. Zachowaj folder nadrzędny hello **MyHelloWorld/WebContent**w sposób pokazany poniżej hello:

   ![][ic659262]

1. W hello **wybierz szablon JSP** okna dialogowego do celów tego samouczka wybierz **New JSP File (html)** i kliknij przycisk **Zakończ**.

1. Po otwarciu pliku index.jsp hello w środowisku Eclipse Dodaj tekst toodynamically wyświetlania **Hello World!** w ramach istniejącego hello `<body>` elementu. Zaktualizowana `<body>` zawartość powinna być widoczna jako hello następujące czynności:
   ```
   <body>
   <b><% out.println("Hello World!"); %></b>
   </body>
   ```
1. Zapisz index.jsp.

## <a name="toodeploy-your-application-tooazure-hello-quick-and-simple-way"></a>toodeploy Twojego tooAzure aplikacji, hello szybki i łatwy sposób
Jak masz Java tootest gotowy aplikacji sieci web, możesz użyć powitania po tootry skrótów, jego limit bezpośrednio na hello Azure w chmurze.

1. W Eksploratorze projektu w programie Eclipse kliknij **MyHelloWorld**.

2. Na pasku narzędzi Eclipse powitania kliknij hello **publikowania** przycisk listy rozwijanej, a następnie kliknij przycisk **Publikuj jako usługa w chmurze Azure**

   ![][publishDropdownButton]

3. Jeśli nie utworzono projektu wdrożenia usługi Azure dla tej aplikacji przed tooAzure tej aplikacji na powitania publikują po raz pierwszy, projektu wdrożenia usługi Azure jest tworzony automatycznie. Powinna zostać wyświetlona toorun hello wierszu, po czym wyświetla również hello JDK pakietów i aplikacji serwera, który zostanie automatycznie wdrożona aplikacja.

   ![][ic789598]
   
   Takie podejście skrótów pozwala tootest szybka i łatwa metoda aplikacji na platformie Azure bez konieczności tooconfigure określonego serwera lub JDK, który różni się od wartości domyślne hello. Jeśli są zadowalające hello wartości domyślne, możesz kliknąć **OK** toocontinue z hello następujące kroki.
   Jednak jeśli chcesz toochange hello JDK lub toouse serwera aplikacji dla aplikacji, możesz to zrobić później, edytując hello projektu wdrożenia usługi Azure, który został utworzony automatycznie lub klikając **anulować** teraz i Odczyt Witaj **wdrożenia o Azure projektów sekcji** tego samouczka.

4. W hello **publikowania tooAzure** okna dialogowego:

   1. Jeśli w hello nie tooselect żadne subskrypcje **subskrypcji** listy jeszcze, wykonaj te kroki tooimport informacji o subskrypcji:
      1. Kliknij przycisk **Import z pliku ustawień publikowania**.
      2. W hello **importu informacji o subskrypcji** okna dialogowego, kliknij przycisk **Pobierz plik ustawień publikowania**. Jeśli użytkownik nie jest jeszcze zalogowany do konta platformy Azure, będzie zostanie wyświetlony monit o toolog w. Następnie zostanie wyświetlony monit pliku ustawień publikowania toosave platformy Azure. Zapisz tooyour komputera lokalnego.
      3. Nadal w hello **importu informacji o subskrypcji** okna dialogowego, kliknij przycisk hello **Przeglądaj** przycisku, wybierz hello lokalnie zapisany w poprzednim kroku hello plik ustawień publikowania, a następnie kliknij przycisk  **Otwórz**. Na ekranie powinien wyglądać podobnie toohello następujące:![][ic644267]
      4. Kliknij przycisk **OK**.
   2. Aby uzyskać **subskrypcji**, wybierz subskrypcję hello, która ma zostać użyta dla danego wdrożenia.
   3. Aby uzyskać **konta magazynu**, wybierz konto magazynu hello mają toouse lub kliknij przycisk **nowy** toocreate nowe konto magazynu.
   4. Dla **nazwa usługi**, wybierz usługę w chmurze hello mają toouse lub kliknij przycisk **nowy** toocreate nową usługę w chmurze.
   5. Dla **docelowego systemu operacyjnego**, wybierz pozycję hello wersja systemu operacyjnego hello mają toouse dla danego wdrożenia.
   6. Aby uzyskać **środowiska docelowego**, dla celów tego samouczka wybierz **przemieszczania**. (Jeśli wszystko jest gotowe toodeploy tooyour produkcji lokacji, użytkownik zmieni to zbyt**produkcji**.)
   7. Opcjonalnie: Upewnij się, że **zastąpienie poprzedniego wdrożenia** jest zaznaczony, jeśli chcesz, aby Twoje nowe tooautomatically wdrożenia Zastąp hello poprzedniego wdrożenia. Po włączeniu tej opcji, nie będzie nie środowisko "409 Konflikt" problemy podczas publikowania toohello tej samej lokalizacji.
      Należy pamiętać, że hello **publikowania tooAzure** okno dialogowe zawiera sekcja **dostępu zdalnego**. Domyślnie nie włączono dostępu zdalnego i nie będzie nie włączyć w tym przykładzie. tooenable dostępu zdalnego, należy wpisać toouse nazwę i hasło użytkownika podczas logowania się zdalnie. Aby uzyskać więcej informacji na temat usługi dostępu zdalnego, zobacz [włączenie dostępu zdalnego we wdrożeniach Azure w programie Eclipse][Enabling Remote Access for Azure Deployments in Eclipse].
      Twoje **publikowania tooAzure** podobne toohello poniżej zostanie wyświetlone okno dialogowe:![][ic719488]

5. Kliknij przycisk **publikowania** środowiska przemieszczania toohello toopublish.

   Gdy zostanie wyświetlony monit o tooperform pełnej kompilacji, kliknij przycisk **tak**. Może to potrwać kilka minut hello pierwszej kompilacji.
   **Dziennika aktywności platformy Azure** będą wyświetlane w sekcji Widoki programu Eclipse na kartach.
   ![][ic719489]Użytkownik może użyć tego dziennika, a także hello **konsoli** wyświetlić postęp hello toosee wdrożenia. Alternatywą jest toolog w toohello [portalu zarządzania Azure][Azure Management Portal]i użyj hello **usługi w chmurze** sekcji toomonitor hello stanu.

6. Wdrożenie po pomyślnym wdrożeniu, hello **dziennika aktywności platformy Azure** będzie wyświetlany stan **opublikowano**. Kliknij przycisk **opublikowano**, jak pokazano w powitania po obrazu i przeglądarce zostanie otwarty wystąpienia wdrożenia.

   ![][ic719490]

Ponieważ to tooa wdrożenia, w środowisku przemieszczania, nazwa DNS hello będzie http:// formularza hello&lt;*guid*&gt;. cloudapp.net i adres URL hello będzie zawierać hello nazwy DNS i sufiksu dla aplikacji. Na przykład http://447564652c20426f6220526f636b7321.cloudapp.net/MyHelloWorld. (hello **MyHelloWorld** fragment jest rozróżniana wielkość liter.) Możesz również sprawdzić hello DNS nazwy kliknięcie nazwy wdrożenia hello w hello portalu zarządzania platformy Azure (w ramach części usługi w chmurze hello hello portalu zarządzania).

Mimo tego przewodnika była dla toohello wdrożenia, w środowisku przemieszczania, tooproduction wdrożenia następuje hello tych samych kroków, z wyjątkiem w hello **publikowania tooAzure** okno dialogowe, wybierz opcję **produkcji** zamiast **przemieszczania** dla hello **środowiska docelowego**. Adres URL na podstawie nazwy DNS hello wybranym zamiast identyfikatora GUID jako używaną na potrzeby przemieszczania powoduje tooproduction wdrożenia.

> [!WARNING]
> W tym momencie wdrożono chmury toohello aplikacji Azure. Jednak przed kontynuowaniem należy pamiętać, że wdrożonej aplikacji, nawet jeśli nie jest uruchomiona, będą nadal tooaccrue czas rozliczeniowy dla Twojej subskrypcji. Dlatego bardzo ważne jest usunięcie niechcianych wdrożeń z subskrypcją platformy Azure.
> 
> 

## <a name="about-azure-deployment-projects"></a>Projekty wdrażania platformy Azure — informacje
W celu toodeploy co najmniej jeden tooAzure aplikacji Java, projektu wdrożenia platformy Azure jest wymagana. Odtwarzania hello roli hello "pakietu", który aplikacje muszą toobe otoczona w kolejności toobe opublikowana na platformie Azure.

Oprócz hello informacji o aplikacji, projektu wdrożenia usługi Azure zawiera także informacje o innych najważniejsze składniki wdrożenia, przede wszystkim: hello toorun kontenera serwera aplikacji w aplikacji sieci web i hello Java runtime toorun go na serwerze. Azure obsługuje dużej liczby środowisk uruchomieniowych Java i serwerów aplikacji Java, które są dostępne.

Mimo że przykład Witaj używane w tym miejscu jest znacznie uproszczone na potrzeby edukacyjne, projektu wdrożenia usługi Azure może również zawierać inne ważne informacje o konfiguracji umożliwia toocreate prawie arbitralnie złożonych, skalowalnych i wysokiej dostępności usługi w chmurze wielowarstwową z aplikacjami. Można włączyć **koligacji sesji ("trwałe sesje")**, **szybkie buforowanie**, **odciążanie protokołu SSL**, **zapory/port routingu**, **dostępu zdalnego**i wiele innych zaawansowanych funkcji.

Jeśli udało Ci się ukończyć hello w poprzedniej sekcji tego samouczka ("toodeploy Twojego tooAzure aplikacji, hello szybki i łatwy sposób"), zostanie wyświetlona nowego projektu wdrożenia usługi Azure w hello Eksplorator projektów wygenerowany automatycznie i o nazwie " **MyHelloWorld_onAzure**".

Można również uruchomieniu tego samouczka najpierw Tworzenie pustego wdrożenia usługi Azure projektu samodzielnie, a następnie dodając tooit Twojej aplikacji. Jest już proces, ale zapewniając większą kontrolę nad konfiguracji początkowej powitania od początku hello.

toocreate nowego projektu wdrożenia usługi Azure od początku, kliknij przycisk hello **nowy projekt wdrożenia usługi Azure** przycisk ![][ic710876].

Niezależnie od tego, czy są Praca z już istniejącego projektu wdrożenia usługi Azure i tworzenia od początku, są możliwe toochange jego ustawienia konfiguracji i składniki, takie jak hello JDK lub równie łatwo hello serwera aplikacji, w dowolnym momencie.

Witaj toochange JDK, lub serwera aplikacji hello lub listy aplikacji hello w istniejącego projektu wdrożenia usługi Azure:

1. Rozwiń węzeł projektu hello (np. **MyHelloWorld_onAzure**) w hello Eksplorator projektów

2. Kliknij prawym przyciskiem myszy **WorkerRole1**

3. Rozwiń węzeł hello **Azure** podmenu w menu kontekstowym hello

4. Kliknij przycisk **konfiguracji serwera**

Bez względu na to czy te kroki konfiguracji serwera jest uruchomiona, edytując istniejącego projektu wdrożenia usługi Azure, jak pokazano powyżej lub tworzenia nowej od początku, zobaczysz hello tego samego rodzaju okien dialogowych, dzięki czemu tooconfigure Twojego JDK serwera i aplikacji składniki. toolearn więcej jak toochange hello ustawienia w tych okien dialogowych, na przykład toochange hello JDK, hello serwera aplikacji i dodawanie lub usuwanie aplikacji we wdrożeniu, zobacz hello [właściwości konfiguracji serwera] [ Server configuration properties] artykułu.

## <a name="windows-only-toodeploy-your-application-toohello-compute-emulator"></a>Tylko w systemie Windows: toodeploy emulator obliczeń toohello Twojej aplikacji

> [!NOTE]
> Hello Azure emulator jest dostępna tylko w systemie Windows. Jeśli używasz systemu operacyjnego innego niż Windows, należy pominąć tę sekcję.
> 
> 

Po utworzeniu nowego projektu wdrożenia usługi Azure hello wykonaj czynności opisane wcześniej, tj. niejawnie publikując Twojej tooAzure aplikacji hello JDK i skonfigurowano serwerów aplikacji hello chmury, ale nie dla lokalnych emulacji. tooprepare projektu do testowania w lokalnym emulatorze hello, wykonaj następujące kroki:

1. W Eksploratorze projektu w programie Eclipse kliknij **MyHelloWorld_onAzure**.

2. Kliknij prawym przyciskiem myszy **WorkerRole1**.

3. Rozwiń węzeł hello **Azure** podmenu w menu kontekstowym hello.

4. Kliknij przycisk **konfiguracji serwera**.

5. Na powitania **JDK** karcie, sprawdź, czy zestaw narzędzi hello ma wstępnie skonfigurowane domyślne lokalnego JDK dla Ciebie. Jeśli nie lub hello toochange zakłada, że wartości domyślne, upewnij się, że hello **Użyj hello JDK z podanej ścieżki pliku do testowania lokalnie** jest zaznaczone pole wyboru, a określono hello JDK lokalizacja instalacji, które mają toouse. Jeśli chcesz toochange, kliknij przycisk hello **Przeglądaj** i za pomocą kontroli przeglądania hello, wybrać lokalizację katalogu hello hello JDK toouse.

6. Kliknij przycisk hello **serwera** kartę.

7. W hello **ścieżki serwera lokalnego** pole tekstowe u dołu hello powitalne okno dialogowe, wprowadź ścieżkę powitania serwera zainstalowane lokalnie, zgodny typ hello i numer wersji głównej wybrany u góry hello powitalne okno dialogowe, w obszarze Serwer hello Witaj **wdrożenie serwera tego typu** wyboru. Jeśli chcesz toouse innego typu lub wersji głównej serwera aplikacji hello, należy najpierw zmienić hello zaznaczenia w pole wyboru.

8. Kliknij przycisk **OK**.

9. Na pasku narzędzi Eclipse powitania kliknij hello **uruchamianie w emulatorze Azure** przycisku ![][ic710879]. Jeśli hello **uruchamianie w emulatorze Azure** przycisk nie jest włączona, upewnij się, że **MyHelloWorld_onAzure** wybrano w obszarze Eksplorator projektów programu Eclipse na i upewnij się, że Eksplorator projektów programu Eclipse na ma fokus jako hello bieżące okno. Będzie to pierwszego uruchomienia pełnej kompilacji projektu, a następnie uruchom aplikację sieci web Java w hello emulatora obliczeń. (Należy pamiętać, że w zależności od charakterystyki wydajności komputera, tworzenia pierwszej kompilacji hello może potrwać od kilku sekund tooa kilka minut, ale kolejne kompilacje otrzyma szybciej.) Po ukończeniu pierwszego kroku kompilacji hello, zostanie wyświetlony monit o tooallow kontroli konta użytkownika (UAC) systemu Windows toomake tego polecenia zostanie zmieniona tooyour komputera. Kliknij przycisk **Yes** (Tak).

> [!IMPORTANT]
> Jeśli nie widzisz wyboru monitu, UAC hello hello zadań systemu Windows hello ikony funkcji Kontrola konta użytkownika i kliknij ją najpierw. Czasami hello monit kontroli konta użytkownika nie jest wyświetlany jako okno najwyższego poziomu, ale jest widoczny tylko jako ikony na pasku zadań.
> 
> 

1. Sprawdź dane wyjściowe hello toodetermine interfejs użytkownika emulatora obliczeń hello, jeśli występują problemy z projektu. W zależności od zawartości hello wdrożenia może upłynąć kilka minut dla Twojego toobe aplikacji, w pełni uruchomiona w ramach hello emulatora obliczeń.

2. Uruchom przeglądarkę i użyj adresu URL hello `http://localhost:8080/MyHelloWorld` jako adres hello (hello `MyHelloWorld` część adresu URL hello jest rozróżniana wielkość liter). Powinny pojawić się Twojej aplikacji MyHelloWorld (hello dane wyjściowe index.jsp), podobne toohello po obrazu:

   ![][ic589579]

Gotowe toostop aplikacji w programie emulatora obliczeń hello w pasku narzędzi Eclipse hello, kliknij przycisk hello **zresetować emulatora usługi Azure** przycisku ![][ic710880].

## <a name="toodelete-your-deployment"></a>toodelete wdrożenia
toodelete wdrożenia w ramach hello zestawu narzędzi platformy Azure dla programu Eclipse, upewnij się, że **MyHelloWorld_onAzure** jest zaznaczona, w obszarze Eksplorator projektów w środowisku Eclipse, upewnij się, hello Eksplorator projektów programu Eclipse ma hello bieżące okno skupić się, a następnie kliknij przycisk Witaj **Cofnij publikowanie** przycisku ![][ic710883], na pasku narzędzi Eclipse hello. (Możesz to zrobić hello tę samą operację, klikając prawym przyciskiem myszy **MyHelloWorld_onAzure** w obszarze Eksplorator projektów w środowisku Eclipse, klikając pozycję **Azure** , a następnie klikając polecenie **Undeploy z chmury Azure**.) Spowoduje to wyświetlenie hello **Cofnij publikowanie projektu platformy Azure** okna dialogowego.

![][ic719491]

Wybierz usługę subskrypcji i w chmurze hello zawierający Twoje wdrożenia, wybierz hello wdrożenia mają toodelete, a następnie kliknij przycisk **Cofnij publikowanie**.

(Alternatywne toousing hello toolkit toodelete hello wdrożenia jest toouse hello **usługi w chmurze** sekcji hello Azure Management Portal: Przejdź tooyour wdrożenia, zaznacz go, a następnie kliknij hello **usunąć** przycisku. Spowoduje to zatrzymanie i wdrożenie zostanie usunięte, hello. Tylko wdrożenia hello toostop i nie można go usunąć, kliknij przycisk hello **zatrzymać** przycisk zamiast hello **usunąć** przycisku, ale jak już wspomniano powyżej, jeśli nie usuniesz hello wdrożenia będzie rozliczana opłat nadal tooaccrue dla danego wdrożenia, nawet jeśli nie został zatrzymany).

## <a name="see-also"></a>Zobacz też
[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]

[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse][Installing hello Azure Toolkit for Eclipse] 

[Nowości w hello zestawu narzędzi platformy Azure dla programu Eclipse][What's New in hello Azure Toolkit for Eclipse]

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Role Properties]: http://go.microsoft.com/fwlink/?LinkID=699525
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Enabling Remote Access for Azure Deployments in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699538
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Server configuration properties]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic589576]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589576.png
[ic589579]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589579.png
[ic600360]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic600360.png
[ic644267]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic644267.png
[ic659262]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic659262.png
[ic710876]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710876.png
[ic710879]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710879.png
[ic710880]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710880.png
[ic710882]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710882.png
[ic710883]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710883.png
[ic719488]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719488.png
[ic719489]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719489.png
[ic719490]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719490.png
[ic719491]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719491.png
[ic789598]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic789598.png
[publishDropdownButton]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/publishDropdownButton.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690944.aspx -->
