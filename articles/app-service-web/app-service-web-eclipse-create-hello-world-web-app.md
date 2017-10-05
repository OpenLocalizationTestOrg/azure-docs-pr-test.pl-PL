---
title: "Tworzenie aplikacji sieci web platformy Azure podstawowe za pomocą programu Eclipse | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak używać zestawu narzędzi platformy Azure dla programu Eclipse do tworzenia Hello World aplikacji sieci Web dla platformy Azure."
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
ms.openlocfilehash: 683d6828546995a4dc60d8cac0669f356501c723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a>Tworzenie aplikacji sieci web platformy Azure podstawowe za pomocą programu Eclipse
W tym samouczku przedstawiono sposób tworzenia i wdrażania podstawowej aplikacji Hello World na platformie Azure jako aplikacji sieci Web przy użyciu [zestawu narzędzi platformy Azure dla programu Eclipse]. Podstawowy przykład JSP jest widoczna dla uproszczenia, ale podobne kroki będzie odpowiednia dla serwlet Java, jakim jest dotyczy wdrożenia usługi Azure.

Po ukończeniu tego samouczka, aplikacja będzie wyglądać podobnie do poniższej ilustracji, podczas wyświetlania w przeglądarce sieci web:

![Podgląd Hello World aplikacji][01]

## <a name="prerequisites"></a>Wymagania wstępne
* Java Developer Kit (JDK), v 1,8 lub nowszej.
* Zaćmienie-IDE for Java EE Developers Luna lub nowszym. Ten można pobrać z <http://www.eclipse.org/downloads/>.
* Dystrybucji serwera sieci web opartych na języku Java lub serwera aplikacji takich jak [Apache Tomcat] lub [Jetty].
* Subskrypcję platformy Azure, która może zostać pobrany z <https://azure.microsoft.com/free/> lub <http://azure.microsoft.com/pricing/purchase-options/>.
* [zestawu narzędzi platformy Azure dla programu Eclipse]. Aby uzyskać informacje o instalowaniu zestawu narzędzi platformy Azure, zobacz [instalowaniu zestawu narzędzi platformy Azure dla programu Eclipse].

## <a name="to-create-a-hello-world-application"></a>Do tworzenia aplikacji Hello World
Po pierwsze Zaczniemy tworzenia projektu języka Java.

1. Uruchom środowisko Eclipse, a następnie w menu kliknij **pliku**, kliknij przycisk **nowy**, a następnie kliknij przycisk **dynamiczny projekt sieci Web**. (Jeśli nie widzisz **dynamiczny projekt sieci Web** wymienione jako projekt dostępne po kliknięciu przycisku **pliku** i **nowy**, następnie wykonaj następujące czynności: kliknij **pliku**, kliknij przycisk **nowy**, kliknij przycisk **projektu...** , rozwiń węzeł **Web**, kliknij przycisk **dynamiczny projekt sieci Web**i kliknij przycisk **dalej**.)
2. Do celów tego samouczka, nazwij projekt **MyWebApp**. Na ekranie pojawi się podobny do następującego:
   
    ![Tworzenie nowego projektu sieci Web dynamiczne][02]
3. Kliknij przycisk **Zakończ**.
4. W widoku Eksplorator projektów w środowisku Eclipse, rozwiń węzeł **MyWebApp**. Kliknij prawym przyciskiem myszy folder **WebContent**, kliknij polecenie **New** (Nowy), a następnie kliknij polecenie **JSP File** (Plik JSP).
5. W **New JSP File** okno dialogowe, nazwa pliku **index.jsp**, przechowuj folder nadrzędny jako **MyWebApp/WebContent**, a następnie kliknij przycisk **dalej**.
6. W **wybierz szablon JSP** okno dialogowe do celów tego samouczka wybierz **New JSP File (html)**, a następnie kliknij przycisk **Zakończ**.
7. Po otwarciu pliku index.jsp w środowisku Eclipse Dodaj tekst do wyświetlenia dynamicznie **Hello World!** wewnątrz istniejącego elementu `<body>`. Zaktualizowana `<body>` zawartości powinien wyglądać następująco:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. Zapisz index.jsp.

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a>Aby wdrożyć aplikację na kontenerem aplikacji sieci Web Azure
Istnieje kilka metod, które można wdrożyć aplikację sieci web Java na platformie Azure. Ten samouczek zawiera opis jednego z najprostszą: aplikacja zostanie wdrożona do kontenera aplikacji sieci Web platformy Azure — żadnych typ projektu ani dodatkowe narzędzia są niezbędne. Zestaw JDK i oprogramowania kontenera sieci web będzie zostać dostarczony przez platformę Azure, a więc nie trzeba przekazać własny; potrzebna jest aplikacja sieci Web Java. W związku z tym proces publikowania aplikacji może zająć sekund, nie minut.

1. W obszarze Eksplorator projektów w środowisku Eclipse, kliknij prawym przyciskiem myszy **MyWebApp**.
2. W menu kontekstowego wybierz **Azure**, następnie kliknij przycisk **Publikuj jako aplikacji sieci Web platformy Azure...**
   
    ![Publikowanie aplikacji sieci Web jako platformy Azure][03]
   
    Alternatywnie podczas projektu aplikacji sieci web wybrano w obszarze Eksplorator projektów, można kliknąć **publikowania** rozwijany przycisk na pasku narzędzi i wybierz **Publikuj jako aplikacji sieci Web Azure** stamtąd:
   
    ![Publikowanie aplikacji sieci Web jako platformy Azure][14]
3. Jeśli dany komputer nie ma już podpisany na platformie Azure z Eclipse, pojawi się monit do logowania się do konta platformy Azure:
   
    ![Azure logowania — okno dialogowe][04]
   
    Jeśli masz wiele kont platformy Azure, niektóre monity podczas logowania w procesie mogą być wyświetlane więcej niż raz, nawet wtedy, gdy pojawią się one być takie same. W takim przypadku należy kontynuować po znaku w instrukcjach.
4. Po pomyślnym zarejestrowaniu do konta platformy Azure, **Zarządzaj subskrypcjami** dialogowym zostanie wyświetlona lista subskrypcji, które są skojarzone z poświadczeniami użytkownika. Jeśli istnieje wiele subskrypcji na liście i chcesz używać konkretnego podzestawu z nich, może opcjonalnie Usuń zaznaczenie pola te, które chcesz użyć. Po zakończeniu wybierania subskrypcji, kliknij przycisk **Zamknij**.
   
    ![Zarządzaj subskrypcjami, okno dialogowe][05]
5. Gdy **Wdróż do kontenera aplikacji sieci Web Azure** zostanie wyświetlone okno dialogowe będzie ono żadnych kontenerów aplikacji sieci Web, które wcześniej zostały utworzone; Jeśli nie utworzono żadnych kontenerów, lista jest pusta.
   
    ![Wdróż do okna dialogowego kontenera aplikacji sieci Web Azure][06]
6. Kontenera aplikacji sieci Web Azure przed nie zostały utworzone lub jeśli chcesz opublikować aplikację do nowego kontenera, wykonaj następujące kroki. W przeciwnym razie wybierz kontener istniejących aplikacji sieci Web i przejdź do kroku 7 poniżej.
   
   1. Kliknij przycisk **nowych...**
      
       ![Wdróż do okna dialogowego kontenera aplikacji sieci Web Azure][15]
   2. **Nowy kontener aplikacji sieci Web** wyświetli się okno dialogowe:
      
       ![Okno dialogowe nowy kontener aplikacji sieci Web][07a]
   3. Wprowadź **Etykieta DNS** dla kontener aplikacji sieci Web; to będzie stanowić liścia Etykieta DNS adresu URL hosta aplikacji sieci web na platformie Azure. (Należy pamiętać, że nazwa musi być dostępny i jest zgodna z wymaganiami nazewnictwa aplikację sieci Web Azure).
   4. W **kontener sieci Web** menu rozwijanego wybierz odpowiedniego oprogramowania dla aplikacji.
      
       Obecnie można wybrać z Tomcat 8 Tomcat 7 lub Jetty 9. Ostatnie dystrybucji wybranego oprogramowania, które będą udostępniane przez usługi Azure, a zostanie uruchomiony na ostatnie dystrybucji 8 JDK utworzone przez firmę Oracle i dostarczany przez platformę Azure.
   5. W **subskrypcji** menu rozwijanego Wybierz subskrypcję, którego chcesz użyć dla tego wdrożenia.
   6. W **grupy zasobów** menu rozwijanego wybierz grupę zasobów, z którą chcesz skojarzyć aplikację sieci Web. (Grup zasobów platformy azure umożliwiają grupowania powiązanych zasobów, tak aby na przykład je usunąć ze sobą.)
      
       Wybierz istniejącą grupę zasobów (jeśli) i Pomiń krok g poniżej lub użyć następującego te kroki, aby utworzyć nową grupę zasobów:
      
      * Kliknij przycisk **nowych...**
      * **Nową grupę zasobów** wyświetli się okno dialogowe:
        
          ![Okno dialogowe nowej grupy zasobów][08]
      * W **nazwa** pole tekstowe, określ nazwę nowej grupy zasobów.
      * W **Region** menu rozwijanego wybierz lokalizację dla grupy zasobów Centrum danych Azure.
      * OPCJONALNIE: Domyślnie ostatnie dystrybucji Java 8 będzie wdrażana za Azure automatycznie do kontener aplikacji sieci web jako sieci maszyny wirtualnej Java. Jednak można określić inną wersję i dystrybucji maszyna JVM, jeśli aplikacja sieci Web wymaga. Aby określić zestaw JDK dla aplikacji sieci Web, kliknij przycisk **JDK** i wybierz jedną z następujących opcji:
        
        * **Wdróż domyślne JDK oferowane przez usługę Azure Web Apps**: Ta opcja zostanie wdrożona ostatnie dystrybucji Java 8.
        * **Wdrażanie 3 strona JDK dostępnych na platformie Azure**: tę opcję można wybrać z listy JDKs, które są udostępniane przez Microsoft Azure.
        * **Wdrażanie własnych JDK z tej lokalizacji pobierania**: Ta opcja umożliwia określenie własnych dystrybucji JDK, które muszą być spakowane jako plik ZIP i przekazać do lokalizacji publicznej pobierania lub kontem magazynu platformy Azure, dla którego masz dostęp.
          
          ![Okno dialogowe nowy kontener aplikacji sieci Web][07b]
   7. Kliknij przycisk **OK**.
   8. **Planu usługi App Service** menu rozwijanego listy planów usługi aplikacji, które są skojarzone z wybranej grupy zasobów. (Planów usługi aplikacji określają informacje takie jak lokalizacja aplikacji sieci Web, warstwy cenowej i rozmiar wystąpienia obliczeniowe. Jeden Plan usługi App Service może służyć do wielu aplikacji sieci Web, dlatego jest obsługiwana oddzielnie od określonego wdrożenia aplikacji sieci Web.)
      
       Wybierz istniejący Plan usługi App Service (jeśli) i Pomiń krok h poniżej lub użyć następującego tych kroków można utworzyć planu usługi aplikacji:
      
      * Kliknij przycisk **nowych...**
      * **Nowy Plan usługi App Service** wyświetli się okno dialogowe:
        
          ![Okno dialogowe Nowy Plan usługi App Service][09]
      * W **nazwa** pole tekstowe, określ nazwę planu usługi aplikacji.
      * W **lokalizacji** menu rozwijanego wybierz lokalizację dla planu Centrum odpowiednich danych Azure.
      * W **warstwy cenowej** menu rozwijanego wybierz odpowiednie ceny dla planu. Podczas testowania, możesz wybrać **wolne**.
      * W **rozmiar wystąpienia** menu rozwijanego, wybierz odpowiednie wystąpienie rozmiaru planu. Podczas testowania, możesz wybrać **małych**.
   9. Po zakończeniu wszystkich kroków opisanych powyżej, okno dialogowe nowy kontener aplikacji sieci Web powinien wyglądać poniższej ilustracji:
      
       ![Okno dialogowe nowy kontener aplikacji sieci Web][10]
   10. Kliknij przycisk **OK** aby zakończyć tworzenie użytkownika nowy kontener aplikacji sieci Web.
       
        Poczekaj kilka sekund na liście kontenery aplikacji sieci Web należy odświeżyć, a kontener aplikacji sieci web nowo utworzony powinny teraz być zaznaczone na liście.
7. Teraz można przystąpić do ukończenia pierwszego wdrożenia aplikacji sieci Web na platformie Azure:
   
    ![Wdróż do okna dialogowego kontenera aplikacji sieci Web Azure][11]
   
    Kliknij przycisk **OK** do wdrożenia aplikacji do wybranego kontenera aplikacji sieci Web w języku Java.
   
    Domyślnie aplikacja zostanie wdrożona jako podkatalog serwera aplikacji. Sprawdź, czy ma to być wdrożony jako aplikacja główna **Wdróż głównym** wyboru przed kliknięciem przycisku **OK**.
8. Następnie zostanie wyświetlony **dziennika aktywności platformy Azure** widoku, który wskazuje stan wdrożenia aplikacji sieci Web.
   
    ![Dziennik aktywności platformy Azure][12]
   
    Proces wdrażania aplikacji sieci Web na platformie Azure powinien zająć tylko kilka sekund. Jeśli możesz już aplikacji, zobaczysz łącze o nazwie **opublikowano** w **stan** kolumny. Po kliknięciu łącza go spowoduje przejście do strony głównej wdrożonej aplikacji sieci Web.

## <a name="updating-your-web-app"></a>Aktualizowanie aplikacji sieci Web
Aktualizowanie istniejącej uruchamiania aplikacji sieci Web platformy Azure jest procesem szybkie i łatwe i dostępne są dwie opcje aktualizacji:

* Można aktualizować wdrażania istniejącej aplikacji sieci Web Java.
* Możesz opublikować aplikację Java dodatkowe do tego samego kontenera aplikacji sieci Web.

W obu przypadkach proces jest identyczne i zajmuje tylko kilka sekund:

1. W obszarze Eksplorator projektów programu Eclipse kliknij prawym przyciskiem myszy aplikację Java, który chcesz zaktualizować, lub Dodaj do istniejącego kontenera aplikacji sieci Web.
2. Po wyświetleniu menu kontekstowego wybierz **Azure** , a następnie **Publikuj jako aplikacji sieci Web platformy Azure...**
3. Ponieważ użytkownik ma już zalogowany wcześniej, zostanie wyświetlona lista sieci kontenerów istniejących aplikacji sieci Web. Wybierz ten, który chcesz opublikować lub ponownie opublikować aplikację Java i kliknij przycisk **OK**.

Później, gdzie po kilku sekundach **dziennika aktywności platformy Azure** widoku wyświetli zaktualizowane wdrożenia jako **opublikowano** i będzie mógł zweryfikować zaktualizowane aplikacji w przeglądarce sieci web.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Uruchamianie, zatrzymywanie lub ponowne uruchamianie istniejących aplikacji sieci web
Aby rozpocząć lub zatrzymać istniejącego kontenera aplikacji sieci Web platformy Azure (w tym wszystkich wdrożonych aplikacji Java w nim), można użyć **Eksploratora Azure** widoku.

Jeśli **Eksploratora Azure** widoku nie jest jeszcze otwarty, otwórz go, klikając następnie **okna** menu w środowisku Eclipse, następnie kliknij przycisk **Pokaż widok**, następnie **innych...** , następnie **Azure**, a następnie kliknij przycisk **Eksploratora Azure**. Jeśli dany system nie zostały wcześniej zarejestrowane, monit podczas wykonywania.

Gdy **Eksploratora Azure** zostanie wyświetlony widok, użyj wykonaj następujące kroki, aby uruchomić lub zatrzymać aplikacji sieci Web: 

1. Rozwiń węzeł **Azure** węzła.
2. Rozwiń węzeł **aplikacje sieci Web** węzła. 
3. Kliknij prawym przyciskiem myszy odpowiednią aplikację sieci Web.
4. W menu kontekstowym kliknij **Start**, **zatrzymać**, lub **ponownego uruchomienia**. Należy zauważyć, że opcji menu kontekstowe obsługujący, więc tylko zatrzymać uruchomionej aplikacji sieci web ani uruchomić aplikacji sieci web, która nie jest obecnie uruchomiona.
   
    ![Zatrzymanie istniejącej aplikacji sieci Web][13]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o zestawach narzędzi platformy Azure dla środowisk IDE języka Java, skorzystaj z następujących linków:

* [zestawu narzędzi platformy Azure dla programu Eclipse]
  * [instalowaniu zestawu narzędzi platformy Azure dla programu Eclipse] (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)
  * *Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse (w tym artykule)*
  * [What's New in the Azure Toolkit for Eclipse] (Co nowego w zestawie narzędzi platformy Azure dla środowiska Eclipse)
* [Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
  * [Installing the Azure Toolkit for IntelliJ] (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)
  * [Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]
  * [What's New in the Azure Toolkit for IntelliJ] (Co nowego w zestawie narzędzi platformy Azure dla środowiska IntelliJ)

Aby uzyskać więcej informacji o używaniu platformy Azure z językiem Java, zobacz [Azure Java Developer Center].

Aby uzyskać dodatkowe informacje dotyczące tworzenia aplikacji sieci Web platformy Azure, zobacz [Omówienie aplikacji sieci Web].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[zestawu narzędzi platformy Azure dla programu Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[instalowaniu zestawu narzędzi platformy Azure dla programu Eclipse]: ../azure-toolkit-for-eclipse-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)
[Installing the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)
[What's New in the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md (Co nowego w zestawie narzędzi platformy Azure dla środowiska Eclipse)
[What's New in the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md (Co nowego w zestawie narzędzi platformy Azure dla środowiska IntelliJ)

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
