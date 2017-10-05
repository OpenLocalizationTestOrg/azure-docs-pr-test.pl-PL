---
title: "Utwórz Hello World usługą w chmurze dla platformy Azure w programie Eclipse"
description: "Dowiedz się, jak utworzyć prostą aplikację Hello World przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse."
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
ms.openlocfilehash: 9b31f0faeb6ee7b5e7b8fe3a1f2827133d6188e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-hello-world-cloud-service-for-azure-in-eclipse"></a>Utwórz Hello World usługą w chmurze dla platformy Azure w programie Eclipse
Poniższych krokach przedstawiono sposób tworzenia i wdrażania prostą aplikację JSP na platformie Azure przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse. Przykład JSP jest widoczna dla uproszczenia, ale bardzo podobne kroki będzie odpowiednia dla serwlet Java, jakim jest dotyczy wdrożenia usługi Azure.

Aplikacja będzie wyglądać podobnie do poniższej:

![][ic600360]

## <a name="prerequisites"></a>Wymagania wstępne
* Java Developer Kit (JDK), v 1.7 lub nowszej.
* Zaćmienie-IDE for Java EE Developers indygo lub nowszej. Ten można pobrać z <http://www.eclipse.org/downloads/>.
* Dystrybucja serwera sieci web opartych na języku Java lub serwera aplikacji, takich jak Apache Tomcat, GlassFish, serwer aplikacji JBoss, Jetty lub IBM® WebSphere® aplikacji Server Liberty Core.
* Subskrypcję platformy Azure, która może zostać pobrany z <http://azure.microsoft.com/pricing/purchase-options/>.
* Zestaw narzędzi platformy Azure dla programu Eclipse. Aby uzyskać więcej informacji, zobacz [instalowaniu zestawu narzędzi platformy Azure dla programu Eclipse][Installing the Azure Toolkit for Eclipse].

## <a name="to-create-a-hello-world-application"></a>Do tworzenia aplikacji Hello World
Po pierwsze Zaczniemy tworzenia projektu języka Java.

1. Uruchom środowisko Eclipse, a następnie w menu kliknij **pliku**, kliknij przycisk **nowy**, a następnie kliknij przycisk **dynamiczny projekt sieci Web**. (Jeśli nie widzisz **dynamiczny projekt sieci Web** wymienione jako projekt dostępne po kliknięciu przycisku **pliku**, **nowy**, następnie wykonaj następujące czynności: kliknij **pliku**, kliknij przycisk **nowy**, kliknij przycisk **projektu...** , rozwiń węzeł **Web**, kliknij przycisk **dynamiczny projekt sieci Web**i kliknij przycisk **dalej**.)

1. Do celów tego samouczka, nazwij projekt **MyHelloWorld**. (Upewnij się, możesz użyć tej nazwy, kolejne kroki w tym samouczku oczekiwać nosić MyHelloWorld pliku WAR). Na ekranie pojawi się podobny do następującego:

   ![][ic589576]

1. Kliknij przycisk **Zakończ**.

1. W widoku Eksplorator projektów w środowisku Eclipse, rozwiń węzeł **MyHelloWorld**. Kliknij prawym przyciskiem myszy folder **WebContent**, kliknij polecenie **New** (Nowy), a następnie kliknij polecenie **JSP File** (Plik JSP).

1. W **New JSP File** okna dialogowego, nazwa pliku **index.jsp**. Zachowaj folder nadrzędny **MyHelloWorld/WebContent**, jak pokazano poniżej:

   ![][ic659262]

1. W **wybierz szablon JSP** okna dialogowego do celów tego samouczka wybierz **New JSP File (html)** i kliknij przycisk **Zakończ**.

1. Po otwarciu pliku index.jsp w środowisku Eclipse Dodaj tekst do wyświetlenia dynamicznie **Hello World!** wewnątrz istniejącego elementu `<body>`. Zaktualizowana `<body>` zawartość powinna być widoczna w następujący sposób:
   ```
   <body>
   <b><% out.println("Hello World!"); %></b>
   </body>
   ```
1. Zapisz index.jsp.

## <a name="to-deploy-your-application-to-azure-the-quick-and-simple-way"></a>Aby wdrożyć aplikację na platformie Azure, szybki i łatwy sposób
Jak ma się rozpocząć testowanie aplikacji sieci web Java, można użyć następujących skrótów wypróbowanie bezpośrednio w chmurze Azure.

1. W Eksploratorze projektu w programie Eclipse kliknij **MyHelloWorld**.

2. Na pasku narzędzi Eclipse kliknij **publikowania** przycisk listy rozwijanej, a następnie kliknij przycisk **Publikuj jako usługa w chmurze Azure**

   ![][publishDropdownButton]

3. Jeśli nie utworzono projektu wdrożenia usługi Azure dla tej aplikacji przed publikowania tej aplikacji na platformie Azure po raz pierwszy, projektu wdrożenia usługi Azure jest tworzony automatycznie. Powinny pojawić się następujący wiersz, która wyświetla również pakiet JDK i serwera aplikacji, które będą automatycznie wdrażane do uruchamiania aplikacji.

   ![][ic789598]
   
   Takie podejście skrótów umożliwia szybki i łatwy sposób przetestować aplikację na platformie Azure, bez konieczności konfigurowania określonego serwera lub JDK, który różni się od wartości domyślne. Jeśli są zadowalające wartości domyślne, możesz kliknąć **OK** do wykonaj następujące kroki.
   Jednak jeśli chcesz zmienić zestaw JDK lub serwera aplikacji do użycia na potrzeby aplikacji, możesz to zrobić później, edytując projektu wdrożenia usługi Azure, który został utworzony automatycznie lub klikając **anulować** teraz i Odczyt  **Projekty o wdrożenia usługi Azure** tego samouczka.

4. W **publikowania na platformie Azure** okna dialogowego:

   1. Jeśli nie ma żadnych subskrypcji, aby wybrać w **subskrypcji** listy jeszcze, wykonaj następujące kroki, aby zaimportować informacje o subskrypcji:
      1. Kliknij przycisk **Import z pliku ustawień publikowania**.
      2. W **importu informacji o subskrypcji** okna dialogowego, kliknij przycisk **Pobierz plik ustawień publikowania**. Jeśli użytkownik nie jest jeszcze zalogowany do konta platformy Azure, pojawi się zalogować. Następnie zostanie wyświetlony monit, aby zapisać Azure pliku ustawień publikowania. Zapisz go na komputerze lokalnym.
      3. Nadal **importu informacji o subskrypcji** okna dialogowego, kliknij przycisk **Przeglądaj** przycisk Wybierz plik ustawień publikowania lokalnie zapisany w poprzednim kroku, a następnie kliknij przycisk **Otwórz**. Na ekranie powinien wyglądać podobnie do następującego:![][ic644267]
      4. Kliknij przycisk **OK**.
   2. Aby uzyskać **subskrypcji**, wybierz subskrypcję, która ma zostać użyta dla danego wdrożenia.
   3. Aby uzyskać **konta magazynu**, wybierz konto magazynu, który ma zostać użyty, lub kliknij przycisk **nowy** Aby utworzyć nowe konto magazynu.
   4. Dla **nazwa usługi**, wybierz usługę w chmurze, który ma zostać użyty, lub kliknij przycisk **nowy** Aby utworzyć nową usługę w chmurze.
   5. Aby uzyskać **docelowego systemu operacyjnego**, wybierz wersję systemu operacyjnego, który ma być używany dla danego wdrożenia.
   6. Aby uzyskać **środowiska docelowego**, dla celów tego samouczka wybierz **przemieszczania**. (Jeśli wszystko jest gotowe do wdrożenia do produkcji witryny, zostanie zmieniona na **produkcji**.)
   7. Opcjonalnie: Upewnij się, że **zastąpienie poprzedniego wdrożenia** jest zaznaczony, jeśli chcesz, aby nowe wdrożenie do automatycznego zastępowania poprzedniego wdrożenia. Po włączeniu tej opcji spowoduje nie środowisko "409 Konflikt" problemy podczas publikowania w tej samej lokalizacji.
      Należy pamiętać, że **publikowania na platformie Azure** okno dialogowe zawiera sekcja **dostępu zdalnego**. Domyślnie nie włączono dostępu zdalnego i nie będzie nie włączyć w tym przykładzie. Aby włączyć dostęp zdalny, należy wprowadzić nazwę użytkownika i hasło do użycia podczas zdalnego logowania. Aby uzyskać więcej informacji na temat usługi dostępu zdalnego, zobacz [włączenie dostępu zdalnego we wdrożeniach Azure w programie Eclipse][Enabling Remote Access for Azure Deployments in Eclipse].
      Twoje **publikowania na platformie Azure** wyświetli się okno dialogowe podobne do następujących:![][ic719488]

5. Kliknij przycisk **publikowania** do publikowania w środowisku przemieszczania.

   Po wyświetleniu monitu, aby wykonać kompilację pełne, kliknij przycisk **tak**. Może to potrwać kilka minut dla pierwszej kompilacji.
   **Dziennika aktywności platformy Azure** będą wyświetlane w sekcji Widoki programu Eclipse na kartach.
   ![][ic719489]Można użyć tego dziennika, jak również **konsoli** widok, aby wyświetlić postęp wdrażania. Alternatywą jest logować się do [portalu zarządzania Azure][Azure Management Portal]i użyj **usługi w chmurze** sekcji, aby monitorować stan.

6. Wdrożenie po pomyślnym wdrożeniu, **dziennika aktywności platformy Azure** będzie wyświetlany stan **opublikowano**. Kliknij przycisk **opublikowano**, jak pokazano na poniższej ilustracji i w przeglądarce zostanie otwarty wystąpienia wdrożenia.

   ![][ic719490]

Ponieważ to wdrożenie w środowisku przemieszczania, nazwa DNS będzie w formie http://&lt;*guid*&gt;. cloudapp.net i będzie adres URL zawiera nazwę DNS i sufiksu dla aplikacji. Na przykład http://447564652c20426f6220526f636b7321.cloudapp.net/MyHelloWorld. ( **MyHelloWorld** fragment jest rozróżniana wielkość liter.) Można również sprawdzić nazwę DNS, jeśli kliknij nazwę wdrożenia w portalu zarządzania platformy Azure (w ramach usługi w chmurze części portalu zarządzania).

Mimo tego przewodnika była wdrożenia do środowiska pomostowego, wdrożenia do produkcji opisano te same kroki, z wyjątkiem w **publikowania na platformie Azure** okno dialogowe, wybierz opcję **produkcji** zamiast **Przemieszczania** dla **środowiska docelowego**. Adres URL na podstawie nazwy DNS w wybranych zamiast identyfikatora GUID jako używaną na potrzeby przemieszczania powoduje wdrożenia do produkcji.

> [!WARNING]
> W tym momencie wdrożonej aplikacji w chmurze platformy Azure. Jednak przed kontynuowaniem należy pamiętać, że wdrożonej aplikacji, nawet jeśli nie jest uruchomiona, będą nadal naliczane czas rozliczeniowy dla Twojej subskrypcji. Dlatego bardzo ważne jest usunięcie niechcianych wdrożeń z subskrypcją platformy Azure.
> 
> 

## <a name="about-azure-deployment-projects"></a>Projekty wdrażania platformy Azure — informacje
Aby można było wdrożyć co najmniej jednej aplikacji Java na platformie Azure, projektu wdrożenia usługi Azure jest wymagane. Odtwarzania rolę "pakietu", które aplikacje muszą być ujęte w celu opublikowania na platformie Azure.

Oprócz informacji o aplikacji, projektu wdrożenia usługi Azure zawiera także informacje o innych najważniejsze składniki wdrożenia, przede wszystkim: kontener serwera aplikacji do uruchomienia aplikacji sieci web w i środowiska uruchomieniowego języka Java można uruchomić ją na. Azure obsługuje dużej liczby środowisk uruchomieniowych Java i serwerów aplikacji Java, które są dostępne.

Chociaż w przykładzie podanym w tym miejscu jest znacznie uproszczone na potrzeby edukacyjne, projektu wdrożenia usługi Azure może również zawierać inne ważne informacje o konfiguracji umożliwia utworzenie prawie arbitralnie złożonych, skalowalnych i wysokiej dostępności usługi w chmurze wielowarstwową z aplikacjami. Można włączyć **koligacji sesji ("trwałe sesje")**, **szybkie buforowanie**, **odciążanie protokołu SSL**, **zapory/port routingu**, **dostępu zdalnego**i wiele innych zaawansowanych funkcji.

Jeśli udało Ci się ukończyć poprzednią sekcję w tym samouczku ("Aby wdrożyć aplikację na platformie Azure, szybki i łatwy sposób"), zostanie wyświetlona nowego projektu wdrożenia usługi Azure w obszarze Eksplorator projektów wygenerowany automatycznie i o nazwie " **MyHelloWorld_onAzure**".

Można również uruchomieniu tego samouczka najpierw Tworzenie pustego wdrożenia usługi Azure projektu samodzielnie, a następnie dodając użytkownika aplikacji do niego. Jest już proces, ale zapewniając większą kontrolę nad początkowej konfiguracji od początku.

Aby utworzyć nowy projekt wdrożenia usługi Azure od początku, kliknij przycisk **nowy projekt wdrożenia usługi Azure** przycisk ![][ic710876].

Niezależnie od tego, czy są Praca z już istniejącego projektu wdrożenia usługi Azure i tworzenia od początku, jesteś można zmienić jej ustawienia konfiguracji i składniki, takie jak zestaw JDK lub serwera aplikacji, równie łatwo w dowolnym momencie.

Aby zmienić JDK, lub serwera aplikacji lub na liście aplikacji w istniejącego projektu wdrożenia usługi Azure:

1. Rozwiń węzeł projektu (np. **MyHelloWorld_onAzure**) w obszarze Eksplorator projektów

2. Kliknij prawym przyciskiem myszy **WorkerRole1**

3. Rozwiń węzeł **Azure** podmenu w menu kontekstowym

4. Kliknij przycisk **konfiguracji serwera**

Niezależnie od tego czy można uruchomić te kroki konfiguracji serwera, edytując istniejącego projektu wdrożenia usługi Azure, jak pokazano powyżej lub tworzenia nowej od początku, pojawi się ten sam typ okien dialogowych, umożliwiając konfigurowanie JDK, serwera i aplikacji składniki. Aby dowiedzieć się więcej na zmienianie ustawień w tych okien dialogowych, na przykład zmienić JDK, serwera aplikacji i dodać lub usunąć aplikacji w ramach wdrożenia, zobacz [właściwości konfiguracji serwera] [ Server configuration properties] artykuł.

## <a name="windows-only-to-deploy-your-application-to-the-compute-emulator"></a>Tylko w systemie Windows: Aby wdrożyć aplikację na emulator obliczeń

> [!NOTE]
> Emulator usługi Azure jest dostępna tylko w systemie Windows. Jeśli używasz systemu operacyjnego innego niż Windows, należy pominąć tę sekcję.
> 
> 

Po utworzeniu nowego projektu wdrożenia usługi Azure wykonanie kroków opisanych wcześniej, tj. niejawnie przez publikowanie aplikacji na platformie Azure, JDK oraz aplikacji serwerów zostały skonfigurowane dla chmury, ale nie dla lokalnych emulacji. Aby przygotować projektu do testowania w lokalnym emulatorze, wykonaj następujące kroki:

1. W Eksploratorze projektu w programie Eclipse kliknij **MyHelloWorld_onAzure**.

2. Kliknij prawym przyciskiem myszy **WorkerRole1**.

3. Rozwiń węzeł **Azure** podmenu w menu kontekstowym.

4. Kliknij przycisk **konfiguracji serwera**.

5. Na **JDK** karcie, sprawdź, czy zestaw narzędzi zawiera wstępnie skonfigurowane domyślne lokalnego JDK dla Ciebie. Jeśli nie lub jeśli chcesz zmienić domyślne zakładanego, upewnij się, że **testowania lokalnie na użytek JDK z podanej ścieżki pliku** jest zaznaczone pole wyboru i określono lokalizację instalacji JDK, który ma być używany. Jeśli chcesz zmienić, kliknij przycisk **Przeglądaj** przycisk i za pomocą kontroli przeglądania, wybierz lokalizację katalogu JDK do użycia.

6. Kliknij przycisk **serwera** kartę.

7. W **ścieżki serwera lokalnego** pole tekstowe w dolnej części okna dialogowego, wprowadź ścieżkę serwera zainstalowane lokalnie, który jest zgodny z typem i numer wersji głównej wybrany w górnej części okna dialogowego, w obszarze serwer  **Wdrażanie serwera tego typu** wyboru. Jeśli chcesz użyć innego typu lub wersji głównej serwera aplikacji, należy najpierw zmienić zaznaczenia w pole wyboru.

8. Kliknij przycisk **OK**.

9. Na pasku narzędzi Eclipse kliknij **uruchamianie w emulatorze Azure** przycisku ![][ic710879]. Jeśli **uruchamianie w emulatorze Azure** przycisk nie jest włączona, upewnij się, że **MyHelloWorld_onAzure** wybrano w obszarze Eksplorator projektów programu Eclipse na i upewnij się, że Eksplorator projektów programu Eclipse na ma fokus, ponieważ bieżący okno. Zostanie najpierw uruchomić pełnej kompilacji projektu i uruchom aplikację sieci web Java w emulatorze obliczeń. (Należy pamiętać, że w zależności od charakterystyki wydajności komputera, tworzenia pierwszej kompilacji może potrwać od kilku sekund do kilku minut, ale kolejne kompilacje otrzyma szybciej.) Po ukończeniu pierwszego kroku kompilacji, pojawi się monit przez kontroli konta użytkownika (UAC) systemu Windows umożliwia to polecenie, aby wprowadzić zmiany w komputerze. Kliknij przycisk **Yes** (Tak).

> [!IMPORTANT]
> Jeśli nie zostanie wyświetlony monit kontroli konta użytkownika, sprawdź na pasku zadań systemu Windows dla ikony funkcji Kontrola konta użytkownika i kliknij ją najpierw. Czasami funkcji Kontrola konta użytkownika wiersza nie jest wyświetlany jako okno najwyższego poziomu, ale jest widoczny tylko jako ikony na pasku zadań.
> 
> 

1. Przejrzyj wyniki emulatora obliczeń interfejsu użytkownika w celu ustalenia, czy istnieją problemy z projektu. W zależności od zawartości wdrożenia może potrwać kilka minut dla aplikacji pełni uruchomić emulatora obliczeń.

2. Uruchom przeglądarkę i użyj adresu URL `http://localhost:8080/MyHelloWorld` jako adresu ( `MyHelloWorld` część adresu URL jest rozróżniana wielkość liter). Powinna zostać wyświetlona aplikacja MyHelloWorld (dane wyjściowe index.jsp), podobnie do poniższej ilustracji:

   ![][ic589579]

Gdy wszystko będzie gotowe zatrzymać Twojej aplikacji w emulatorze obliczeń, w pasku narzędzi Eclipse kliknij **zresetować emulatora usługi Azure** przycisku ![][ic710880].

## <a name="to-delete-your-deployment"></a>Aby usunąć wdrożenia
Aby usunąć wdrożenia w ramach zestawu narzędzi platformy Azure dla programu Eclipse, upewnij się, że **MyHelloWorld_onAzure** jest wybrane w obszarze Eksplorator projektów w środowisku Eclipse, upewnij się, bieżące okno skupić się, a następnie kliknij przycisk maEksploratorprojektówprogramuEclipse **Cofnij publikowanie** przycisku ![][ic710883], na pasku narzędzi Eclipse. (Może wykonać tę samą operację, klikając prawym przyciskiem myszy **MyHelloWorld_onAzure** w obszarze Eksplorator projektów w środowisku Eclipse, klikając pozycję **Azure** , a następnie klikając polecenie **Undeploy z chmury Azure**.) Spowoduje to wyświetlenie **Cofnij publikowanie projektu platformy Azure** okna dialogowego.

![][ic719491]

Wybierz usługę subskrypcji i w chmurze, która zawiera wdrożenia, wybierz wdrożenie, które chcesz usunąć, a następnie kliknij przycisk **Cofnij publikowanie**.

(Jest to alternatywa dla użycia zestawu narzędzi do usunięcia wdrożenia do użycia **usługi w chmurze** części portalu zarządzania Azure: Przejdź do wdrożenia, zaznacz go, a następnie kliknij przycisk **usunąć** przycisk. Spowoduje to zatrzymanie i wdrożenie zostanie usunięte. Jeśli chcesz tylko wdrożenia i nie można go usunąć, kliknij przycisk **zatrzymać** przycisk zamiast **usunąć** przycisku, ale jak wspomniano powyżej, jeśli wdrożenie nie zostaną usunięte, rozliczeniowy opłaty będą nadal naliczane dla danego wdrożenia, nawet jeśli nie został zatrzymany).

## <a name="see-also"></a>Zobacz też
[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]

[Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse][Installing the Azure Toolkit for Eclipse] 

[What's New in Azure zestawu narzędzi dla programu Eclipse][What's New in the Azure Toolkit for Eclipse]

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Role Properties]: http://go.microsoft.com/fwlink/?LinkID=699525
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Enabling Remote Access for Azure Deployments in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699538
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Server configuration properties]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

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
