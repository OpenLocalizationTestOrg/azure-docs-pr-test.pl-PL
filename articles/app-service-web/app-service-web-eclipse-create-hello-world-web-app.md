---
title: "Zaćmienie-aaaCreate aplikacji sieci web platformy Azure podstawowe przy użyciu | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak toouse hello zestawu narzędzi platformy Azure dla programu Eclipse toocreate aplikacji Hello World sieci Web dla platformy Azure."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: b2f42e0e7a5b98760ec02fab2fc38f9f07b1156b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a>Tworzenie aplikacji sieci web platformy Azure podstawowe za pomocą programu Eclipse
Ten samouczek pokazuje, jak toocreate i wdrażania podstawowych tooAzure aplikacji Hello World jako aplikacji sieci Web przy użyciu hello [zestawu narzędzi platformy Azure dla programu Eclipse]. Podstawowy przykład JSP jest widoczna dla uproszczenia, ale podobne kroki będzie odpowiednia dla serwlet Java, jakim jest dotyczy wdrożenia usługi Azure.

Po ukończeniu tego samouczka, aplikacja będzie wyglądać podobnie toohello następującej ilustracji, podczas wyświetlania w przeglądarce sieci web:

![Podgląd Hello World aplikacji][01]

## <a name="prerequisites"></a>Wymagania wstępne
* Java Developer Kit (JDK), v 1,8 lub nowszej.
* Zaćmienie-IDE for Java EE Developers Luna lub nowszym. Ten można pobrać z <http://www.eclipse.org/downloads/>.
* Dystrybucji serwera sieci web opartych na języku Java lub serwera aplikacji takich jak [Apache Tomcat] lub [Jetty].
* Subskrypcję platformy Azure, która może zostać pobrany z <https://azure.microsoft.com/free/> lub <http://azure.microsoft.com/pricing/purchase-options/>.
* Witaj [zestawu narzędzi platformy Azure dla programu Eclipse]. Informacje o instalowaniu hello zestawu narzędzi platformy Azure, zobacz [hello Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse].

## <a name="toocreate-a-hello-world-application"></a>toocreate aplikacji Hello World
Po pierwsze Zaczniemy tworzenia projektu języka Java.

1. Uruchom środowisko Eclipse, a następnie w menu powitania kliknij **pliku**, kliknij przycisk **nowy**, a następnie kliknij przycisk **dynamiczny projekt sieci Web**. (Jeśli nie widzisz **dynamiczny projekt sieci Web** wymienione jako projekt dostępne po kliknięciu przycisku **pliku** i **nowy**, następnie hello następujące: kliknij **pliku**, kliknij przycisk **nowy**, kliknij przycisk **projektu...** , rozwiń węzeł **Web**, kliknij przycisk **dynamiczny projekt sieci Web**i kliknij przycisk **dalej**.)
2. Do celów tego samouczka, nazwa projektu hello **MyWebApp**. Na ekranie pojawi się podobne toohello następujące:
   
    ![Tworzenie nowego projektu sieci Web dynamiczne][02]
3. Kliknij przycisk **Zakończ**.
4. W widoku Eksplorator projektów w środowisku Eclipse, rozwiń węzeł **MyWebApp**. Kliknij prawym przyciskiem myszy folder **WebContent**, kliknij polecenie **New** (Nowy), a następnie kliknij polecenie **JSP File** (Plik JSP).
5. W hello **New JSP File** okno dialogowe, nazwa pliku hello **index.jsp**, przechowuj folder nadrzędny hello jako **MyWebApp/WebContent**, a następnie kliknij przycisk **dalej**.
6. W hello **wybierz szablon JSP** okno dialogowe do celów tego samouczka wybierz **New JSP File (html)**, a następnie kliknij przycisk **Zakończ**.
7. Po otwarciu pliku index.jsp w środowisku Eclipse Dodaj tekst toodynamically wyświetlania **Hello World!** w ramach istniejącego hello `<body>` elementu. Zaktualizowana `<body>` zawartość powinna wyglądać hello poniższy przykład:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. Zapisz index.jsp.

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy Twojego tooan aplikacji kontenera aplikacji sieci Web Azure
Istnieje kilka metod, które można wdrożyć tooAzure aplikacji sieci web Java. Ten samouczek zawiera opis jednego z hello najprostszym: aplikacja będzie tooan wdrożony kontener aplikacji sieci Web platformy Azure — żadnych typ projektu ani dodatkowe narzędzia są niezbędne. Hello JDK i hello kontenera oprogramowanie dla sieci web zostanie zostać dostarczony przez platformę Azure, więc nie ma żadnych tooupload potrzeby własne; potrzebna jest aplikacja sieci Web Java. W związku z tym hello proces publikowania aplikacji może zająć sekund, nie minut.

1. W obszarze Eksplorator projektów w środowisku Eclipse, kliknij prawym przyciskiem myszy **MyWebApp**.
2. W menu kontekstowym hello, wybierz **Azure**, następnie kliknij przycisk **Publikuj jako aplikacji sieci Web platformy Azure...**
   
    ![Publikowanie aplikacji sieci Web jako platformy Azure][03]
   
    Alternatywnie podczas projektu aplikacji sieci web jest zaznaczone hello Eksplorator projektów, można kliknąć hello **publikowania** rozwijany przycisk na powitania narzędzi i wybierz **Publikuj jako aplikacji sieci Web Azure** stamtąd:
   
    ![Publikowanie aplikacji sieci Web jako platformy Azure][14]
3. Jeśli dany komputer nie ma już podpisany na platformie Azure z Eclipse, będzie toosign zostanie wyświetlony monit o do konta platformy Azure:
   
    ![Azure logowania — okno dialogowe][04]
   
    Jeśli masz wiele kont platformy Azure, zaloguj się niektóre hello monity podczas hello procesu mogą być wyświetlane więcej niż raz, nawet wtedy, gdy pojawią się one toobe hello takie same. W takim przypadku należy kontynuować, następujące hello logowania instrukcje.
4. Po pomyślnym zarejestrowaniu do konta platformy Azure, hello **Zarządzaj subskrypcjami** dialogowym zostanie wyświetlona lista subskrypcji, które są skojarzone z poświadczeniami użytkownika. Jeśli istnieje wiele wymienionych subskrypcji i chcesz toowork z konkretnego podzestawu z nich, może opcjonalnie Usuń zaznaczenie pola hello mają toouse z nich. Po zakończeniu wybierania subskrypcji, kliknij przycisk **Zamknij**.
   
    ![Zarządzaj subskrypcjami, okno dialogowe][05]
5. Gdy hello **wdrażanie tooAzure kontenera aplikacji sieci Web** zostanie wyświetlone okno dialogowe będzie ono żadnych kontenerów aplikacji sieci Web, które wcześniej zostały utworzone; Jeśli nie utworzono żadnych kontenerów, hello lista jest pusta.
   
    ![Wdrażanie tooAzure kontenera aplikacji sieci Web, okno dialogowe][06]
6. Jeśli nie utworzono kontener aplikacji sieci Web Azure przed lub jeśli chcesz toopublish Twojej aplikacji tooa nowy kontener, użyj hello następujące kroki. W przeciwnym razie wybierz kontener istniejących aplikacji sieci Web i pominąć toostep 7 poniżej.
   
   1. Kliknij przycisk **nowych...**
      
       ![Wdrażanie tooAzure kontenera aplikacji sieci Web, okno dialogowe][15]
   2. Witaj **nowy kontener aplikacji sieci Web** wyświetli się okno dialogowe:
      
       ![Okno dialogowe nowy kontener aplikacji sieci Web][07a]
   3. Wprowadź **Etykieta DNS** dla kontener aplikacji sieci Web; to będzie stanowić etykietę DNS liścia hello hello hosta adres URL aplikacji sieci web na platformie Azure. (Należy zauważyć, że nazwa hello musi być dostępny i jest zgodna z wymaganiami dotyczącymi nazw aplikacji sieci Web tooAzure).
   4. W hello **kontener sieci Web** menu rozwijanego, wybierz hello odpowiedniego oprogramowania dla aplikacji.
      
       Obecnie można wybrać z Tomcat 8 Tomcat 7 lub Jetty 9. Ostatnie dystrybucji oprogramowania hello wybrane będą udostępniane przez usługi Azure, a zostanie uruchomiony na ostatnie dystrybucji 8 JDK utworzone przez firmę Oracle i dostarczany przez platformę Azure.
   5. W hello **subskrypcji** menu rozwijanego, wybierz hello subskrypcję toouse dla tego wdrożenia.
   6. W hello **grupy zasobów** menu rozwijane i wybierz hello grupy zasobów, z którą chcesz tooassociate aplikacji sieci Web. (Zezwalaj grup zasobów platformy azure możesz toogroup powiązane ze sobą zasoby, tak, aby na przykład je usunąć ze sobą.)
      
       Można wybrać istniejącą grupę zasobów (jeśli) i Pomiń toostep g poniżej lub hello Użyj następującego te kroki toocreate nową grupę zasobów:
      
      * Kliknij przycisk **nowych...**
      * Witaj **nową grupę zasobów** wyświetli się okno dialogowe:
        
          ![Okno dialogowe nowej grupy zasobów][08]
      * W hello hello **nazwa** pole tekstowe, określ nazwę nowej grupy zasobów.
      * W hello hello **Region** menu rozwijanego wybierz hello odpowiednie usługi Azure data center lokalizację dla grupy zasobów.
      * OPCJONALNIE: Domyślnie ostatnie dystrybucji Java 8 będą wdrażane przez platformę Azure automatycznie tooyour kontenera aplikacji sieci web jako sieci maszyny wirtualnej Java. Jednak można określić inną wersję i dystrybucji hello JVM, jeśli aplikacja sieci Web wymaga. Witaj toospecify JDK dla aplikacji sieci Web, kliknij przycisk hello **JDK** i wybierz jedną z hello następujące opcje:
        
        * **Wdróż domyślne hello JDK oferowane przez usługę Azure Web Apps**: Ta opcja zostanie wdrożona ostatnie dystrybucji Java 8.
        * **Wdrażanie 3 strona JDK dostępnych na platformie Azure**: Ta opcja umożliwia toochoose z listy hello JDKs, które są udostępniane przez Microsoft Azure.
        * **Wdrażanie własnych JDK z tej lokalizacji pobierania**: Ta opcja umożliwia toospecify własne dystrybucji JDK, które muszą być spakowane jako plik ZIP i przekazać tooeither lokalizacji pobierania publicznie dostępnych lub magazynu Azure konta, dla którego należy masz dostęp.
          
          ![Okno dialogowe nowy kontener aplikacji sieci Web][07b]
   7. Kliknij przycisk **OK**.
   8. Witaj **planu usługi App Service** hello planów usługi aplikacji, które są skojarzone z hello wybrana grupa zasobów zawiera menu rozwijanego. (Informacje, takie jak lokalizacja hello aplikacji sieci Web, hello warstwa cenowa i rozmiar wystąpienia obliczeniowe hello Określ planów usługi aplikacji. Jeden Plan usługi App Service może służyć do wielu aplikacji sieci Web, dlatego jest obsługiwana oddzielnie od określonego wdrożenia aplikacji sieci Web.)
      
       Można wybrać istniejący Plan usługi App Service (jeśli) i Pomiń h toostep poniżej, lub użyj powitania po toocreate te kroki, planu usługi aplikacji:
      
      * Kliknij przycisk **nowych...**
      * Witaj **nowy Plan usługi App Service** wyświetli się okno dialogowe:
        
          ![Okno dialogowe Nowy Plan usługi App Service][09]
      * W hello hello **nazwa** pole tekstowe, określ nazwę planu usługi aplikacji.
      * W hello hello **lokalizacji** menu rozwijanego wybierz hello odpowiednie usługi Azure data center lokalizacji dla planu hello.
      * W hello hello **warstwy cenowej** menu rozwijanego, wybierz odpowiednie ceny dla planu hello hello. Podczas testowania, możesz wybrać **wolne**.
      * W hello hello **rozmiar wystąpienia** menu rozwijanego, hello wybierz odpowiednie wystąpienie rozmiar hello planu. Podczas testowania, możesz wybrać **małych**.
   9. Po wykonaniu wszystkich hello powyżej kroki, okno dialogowe nowy kontener aplikacji sieci Web hello powinien wyglądać hello następującej ilustracji:
      
       ![Okno dialogowe nowy kontener aplikacji sieci Web][10]
   10. Kliknij przycisk **OK** tworzenie hello toocomplete Twojego nowego kontenera aplikacji sieci Web.
       
        Zaczekaj kilka sekund hello lista toobe kontenery sieci Web aplikacji hello odświeżyć, a kontener aplikacji sieci web nowo utworzony powinny teraz być zaznaczone na liście hello.
7. Wszystko jest teraz gotowy toocomplete hello początkowe wdrożenie tooAzure Twojej aplikacji sieci Web:
   
    ![Wdrażanie tooAzure kontenera aplikacji sieci Web, okno dialogowe][11]
   
    Kliknij przycisk **OK** toodeploy Twojego toohello aplikacji Java wybrany kontener aplikacji sieci Web.
   
    Domyślnie aplikacja zostanie wdrożona jako podkatalog serwera aplikacji hello. Jeśli chcesz toobe wdrożony jako aplikacja główna hello, sprawdź hello **wdrażanie tooroot** wyboru przed kliknięciem przycisku **OK**.
8. Następnie powinna zostać wyświetlona hello **dziennika aktywności platformy Azure** widoku, który będzie wskazywać hello stan wdrożenia aplikacji sieci Web.
   
    ![Dziennik aktywności platformy Azure][12]
   
    Hello proces wdrażania tooAzure Twojej aplikacji sieci Web powinien zająć tylko kilka sekund toocomplete. Jeśli możesz już aplikacji, zobaczysz łącze o nazwie **opublikowano** w hello **stan** kolumny. Po kliknięciu łącza hello spowoduje przejście strony głównej aplikacji sieci Web tooyour wdrożone.

## <a name="updating-your-web-app"></a>Aktualizowanie aplikacji sieci Web
Aktualizowanie istniejącej uruchamiania aplikacji sieci Web platformy Azure jest procesem szybkie i łatwe i dostępne są dwie opcje aktualizacji:

* Można aktualizować hello wdrażania istniejącej aplikacji sieci Web Java.
* Możesz opublikować dodatkowe toohello aplikacji Java tego samego kontenera aplikacji sieci Web.

W obu przypadkach procesu hello jest identyczne i zajmuje tylko kilka sekund:

1. W obszarze Eksplorator projektów programu Eclipse hello kliknij prawym przyciskiem myszy aplikacji Java hello mają tooupdate lub Dodaj tooan istniejącego kontenera aplikacji sieci Web.
2. Po wyświetleniu menu kontekstowe hello zaznacz **Azure** , a następnie **Publikuj jako aplikacji sieci Web platformy Azure...**
3. Ponieważ użytkownik ma już zalogowany wcześniej, zostanie wyświetlona lista sieci kontenerów istniejących aplikacji sieci Web. Wybierz hello mają toopublish lub ponownie opublikować kliknięcia tooand aplikacji Java **OK**.

Hello później za kilka sekund **dziennika aktywności platformy Azure** widoku wyświetli zaktualizowane wdrożenia jako **opublikowano** i będą mogli tooverify zaktualizowane aplikacji w przeglądarce sieci web.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Uruchamianie, zatrzymywanie lub ponowne uruchamianie istniejących aplikacji sieci web
toostart lub zatrzymać istniejącego kontenera aplikacji sieci Web platformy Azure (w tym wszystkich aplikacji Java hello wdrożone w nim), możesz użyć hello **Eksploratora Azure** widoku.

Jeśli hello **Eksploratora Azure** widoku nie jest jeszcze otwarty, otwórz go, klikając następnie **okna** menu w środowisku Eclipse, następnie kliknij przycisk **Pokaż widok**, następnie **innych...** , następnie **Azure**, a następnie kliknij przycisk **Eksploratora Azure**. Jeśli dany system nie zostały wcześniej zarejestrowane, go spowoduje wyświetlenie monitu toodo tak.

Gdy hello **Eksploratora Azure** zostanie wyświetlony widok, użyj wykonaj te kroki toostart lub Zatrzymaj aplikację sieci Web: 

1. Rozwiń węzeł hello **Azure** węzła.
2. Rozwiń węzeł hello **aplikacje sieci Web** węzła. 
3. Kliknij prawym przyciskiem myszy hello żądana aplikacji sieci Web.
4. Po wyświetleniu menu kontekstowe powitania kliknij **Start**, **zatrzymać**, lub **ponownego uruchomienia**. Należy zauważyć, że hello menu opcji kontekstu obsługujący, więc tylko zatrzymać uruchomionej aplikacji sieci web ani uruchomić aplikacji sieci web, która nie jest obecnie uruchomiona.
   
    ![Zatrzymanie istniejącej aplikacji sieci Web][13]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat hello narzędzi Azure dla języka Java IDEs Zobacz hello następującego łącza:

* [zestawu narzędzi platformy Azure dla programu Eclipse]
  * [hello Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse]
  * *Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse (w tym artykule)*
  * [Nowości w hello zestawu narzędzi platformy Azure dla programu Eclipse]
* [Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
  * [Instalowanie hello Azure Toolkit for IntelliJ]
  * [Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]
  * [Nowości w hello Azure Toolkit for IntelliJ]

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center].

Aby uzyskać dodatkowe informacje dotyczące tworzenia aplikacji sieci Web platformy Azure, zobacz hello [Omówienie aplikacji sieci Web].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[zestawu narzędzi platformy Azure dla programu Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[hello Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Instalowanie hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Nowości w hello zestawu narzędzi platformy Azure dla programu Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Nowości w hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Omówienie aplikacji sieci Web]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
