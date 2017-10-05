---
title: Tworzenie aplikacji sieci web platformy Azure podstawowe w IntelliJ | Dokumentacja firmy Microsoft
description: "Ten samouczek pokazuje, jak używać narzędzi Azure dla IntelliJ do utworzenia Hello World aplikacji sieci Web dla platformy Azure."
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 20b2c3d86f5bde9302647f345aa99b030d78613a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a>Tworzenie aplikacji sieci web platformy Azure podstawowe w IntelliJ
W tym samouczku przedstawiono sposób tworzenia i wdrażania podstawowej aplikacji Hello World na platformie Azure jako aplikacji sieci Web przy użyciu [narzędzi Azure dla IntelliJ]. Podstawowy przykład JSP jest widoczna dla uproszczenia, ale podobne kroki będzie odpowiednia dla serwlet Java, jakim jest dotyczy wdrożenia usługi Azure.

Po ukończeniu tego samouczka, aplikacja będzie wyglądać podobnie do poniższej ilustracji, podczas wyświetlania w przeglądarce sieci web:

![Przykładowa strona sieci Web][01]

## <a name="prerequisites"></a>Wymagania wstępne
* Java Developer Kit (JDK), v 1,8 lub nowszej.
* IntelliJ IDEA Ultimate Edition. Ten można pobrać z <https://www.jetbrains.com/idea/download/index.html>.
* Dystrybucji serwera sieci web opartych na języku Java lub serwera aplikacji takich jak [Apache Tomcat] lub [Jetty].
* Subskrypcję platformy Azure, która może zostać pobrany z <https://azure.microsoft.com/free/> lub <http://azure.microsoft.com/pricing/purchase-options/>.
* [narzędzi Azure dla IntelliJ]. Aby uzyskać informacje o instalowaniu zestawu narzędzi platformy Azure, zobacz [Instalowanie zestawu narzędzi platformy Azure dla IntelliJ].

## <a name="to-create-a-hello-world-application"></a>Do tworzenia aplikacji Hello World
Po pierwsze Zaczniemy tworzenia projektu języka Java.

1. Uruchom środowisko IntelliJ i kliknij przycisk **pliku** menu, następnie kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.
   
    ![Nowy projekt pliku][02]
2. W oknie dialogowym Nowy projekt, wybierz **Java**, następnie **aplikacji sieci Web**, a następnie kliknij przycisk **nowy** można dodać SDK projektu.
   
    ![Okno dialogowe Nowy projekt][03a]
   
3. Wybierz katalog macierzysty dla JDK — okno dialogowe, wybierz folder, w którym zainstalowano JDK użytkownika, a następnie kliknij przycisk **OK**. Kliknij przycisk **dalej** w oknie dialogowym Nowy projekt, aby kontynuować.
   
    ![Określ katalog macierzysty JDK][03b]
4. Do celów tego samouczka, nazwij projekt **Java sieci Web-App-na-Azure**, a następnie kliknij przycisk **Zakończ**.
   
    ![Okno dialogowe Nowy projekt][04]
5. W widoku Project Explorer IntelliJ firmy, rozwiń węzeł **Java sieci Web-App-na-Azure**, następnie rozwiń węzeł **web**, a następnie kliknij dwukrotnie **index.jsp**.
   
    ![Otwórz indeks strony][05c]
6. Po otwarciu pliku index.jsp w IntelliJ, Dodaj tekst do wyświetlenia dynamicznie **Hello World!** wewnątrz istniejącego elementu `<body>`. Zaktualizowana `<body>` zawartości powinien wyglądać następująco:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. Zapisz index.jsp.

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a>Aby wdrożyć aplikację na kontenerem aplikacji sieci Web Azure
Istnieje kilka metod, które można wdrożyć aplikację sieci web Java na platformie Azure. Ten samouczek zawiera opis jednego z najprostszą: aplikacja zostanie wdrożona do kontenera aplikacji sieci Web platformy Azure — żadnych typ projektu ani dodatkowe narzędzia są niezbędne. Zestaw JDK i oprogramowania kontenera sieci web będzie zostać dostarczony przez platformę Azure, a więc nie trzeba przekazać własny; potrzebna jest aplikacja sieci Web Java. W związku z tym proces publikowania aplikacji może zająć sekund, nie minut.

Przed opublikowaniem aplikacji, należy najpierw skonfigurować ustawienia modułu. Aby to zrobić, wykonaj następujące kroki:

1. W obszarze Eksplorator projektów w IntelliJ, kliknij prawym przyciskiem myszy **Java sieci Web-App-na-Azure** projektu. W menu kontekstowym kliknij **Otwórz ustawienia modułu**.

    ![Otwórz ustawienia modułu][05a]
2. Kiedy wyświetli się okno dialogowe struktury projektu:

   a. Kliknij przycisk **artefakty** na liście **ustawienia projektu**.
   b. Zmień nazwę artefaktów w **nazwa** , dzięki czemu nie zawiera spacji ani znaków specjalnych; jest to konieczne, ponieważ nazwa będzie używana w jednolity identyfikator zasobów (URI).
   c. Zmień **typu** do **aplikacji sieci Web: archiwum**.
   d. Kliknij przycisk **OK** aby zamknąć okno dialogowe struktury projektu.

    ![Otwórz ustawienia modułu][05b]

Po skonfigurowaniu ustawień modułu można opublikować aplikacji na platformie Azure przy użyciu następujących kroków:

1. W obszarze Eksplorator projektów w IntelliJ, kliknij prawym przyciskiem myszy **Java sieci Web-App-na-Azure** projektu. Po wyświetleniu menu kontekstowego wybierz **Azure**, a następnie kliknij przycisk **Publikuj jako aplikacji sieci Web platformy Azure...**
   
    ![Menu kontekstowe publikowania na platformie Azure][06]
2. Jeśli dany komputer nie ma już podpisany na platformie Azure z IntelliJ, pojawi się monit do logowania się do konta platformy Azure. (Jeśli masz wiele kont platformy Azure, niektóre monity podczas logowania w procesie mogą być wyświetlane więcej niż raz, nawet wtedy, gdy pojawią się one być takie same. W takim przypadku, postępuj zgodnie z logowania w instrukcjach).
   
    ![Azure dziennika w oknie dialogowym][07]
3. Po pomyślnym zarejestrowaniu do konta platformy Azure, **Zarządzaj subskrypcjami** dialogowym zostanie wyświetlona lista subskrypcji, które są skojarzone z poświadczeniami użytkownika. (Jeśli istnieje wiele subskrypcji wymieniono i chcesz używać konkretnego podzestawu z nich, może opcjonalnie Usuń zaznaczenie subskrypcje, do których nie chcesz używać.) Po zakończeniu wybierania subskrypcji, kliknij przycisk **Zamknij**.
   
    ![Zarządzanie subskrypcjami][08]
4. Gdy **Wdróż do kontenera aplikacji sieci Web Azure** zostanie wyświetlone okno dialogowe będzie ono żadnych kontenerów aplikacji sieci Web, które wcześniej zostały utworzone; Jeśli nie utworzono żadnych kontenerów, lista jest pusta.
   
    ![Kontenery aplikacji][09]
5. Kontenera aplikacji sieci Web Azure przed nie zostały utworzone lub jeśli chcesz opublikować aplikację do nowego kontenera, wykonaj następujące kroki. W przeciwnym razie wybierz kontener istniejących aplikacji sieci Web i przejdź do kroku 6 poniżej.
   
   1. Kliknij przycisk**+**
      
       ![Dodawanie aplikacji kontenera][10]
   2. **Nowy kontener aplikacji sieci Web** można wyświetlić okna dialogowego, które będzie służyć do następnych krokach.
      
       ![Nowy kontener aplikacji][11a]
   3. Wprowadź **Etykieta DNS** dla kontener aplikacji sieci Web; to będzie stanowić liścia Etykieta DNS adresu URL hosta aplikacji sieci web na platformie Azure. Należy pamiętać, że nazwa musi być dostępny i jest zgodna z wymaganiami nazewnictwa aplikację sieci Web Azure.
   4. W **kontener sieci Web** menu rozwijanego wybierz odpowiedniego oprogramowania dla aplikacji.
      
       Obecnie można wybrać z Tomcat 8 Tomcat 7 lub Jetty 9. Ostatnie dystrybucji wybranego oprogramowania, które będą udostępniane przez usługi Azure, a zostanie uruchomiony na ostatnie dystrybucji 8 JDK utworzone przez firmę Oracle i dostarczany przez platformę Azure.
   5. W **subskrypcji** menu rozwijanego Wybierz subskrypcję, którego chcesz użyć dla tego wdrożenia.
   6. W **grupy zasobów** menu rozwijanego wybierz grupę zasobów, z którą chcesz skojarzyć aplikację sieci Web. (Grup zasobów platformy azure umożliwiają grupowania powiązanych zasobów, tak aby na przykład je usunąć ze sobą.)
      
       Wybierz istniejącą grupę zasobów (jeśli) i Pomiń krok g poniżej lub wykonaj następujące kroki, aby utworzyć nową grupę zasobów:
      
      * Wybierz  **&lt; &lt; Utwórz nową grupę zasobów &gt; &gt;**  w **grupy zasobów** menu rozwijanego.
      * **Nową grupę zasobów** wyświetli się okno dialogowe:
        
          ![Nową grupę zasobów][12]
      * W **nazwa** pole tekstowe, określ nazwę nowej grupy zasobów.
      * W **Region** menu rozwijanego wybierz lokalizację dla grupy zasobów Centrum danych Azure.
      * Kliknij przycisk **OK**.
   7. **Planu usługi App Service** menu rozwijanego listy planów usługi aplikacji, które są skojarzone z wybranej grupy zasobów. (Plan usługi App Service określa informacje takie jak lokalizacja aplikacji sieci Web, warstwy cenowej i rozmiar wystąpienia obliczeniowe. Jeden Plan usługi App Service może służyć do wielu aplikacji sieci Web, dlatego jest obsługiwana oddzielnie od określonego wdrożenia aplikacji sieci Web.)
      
       Wybierz istniejący Plan usługi App Service (jeśli) i Pomiń krok h poniżej lub wykonaj następujące kroki, aby utworzyć nowy Plan usługi App Service:
      
      * Wybierz  **&lt; &lt; Utwórz nowy Plan usługi App Service &gt; &gt;**  w **planu usługi App Service** menu rozwijanego.
      * **Nowy Plan usługi App Service** wyświetli się okno dialogowe:
        
          ![Nowy Plan usługi aplikacji][13]
      * W **nazwa** pole tekstowe, określ nazwę planu usługi aplikacji.
      * W **lokalizacji** menu rozwijanego wybierz lokalizację dla planu Centrum odpowiednich danych Azure.
      * W **warstwy cenowej** menu rozwijanego wybierz odpowiednie ceny dla planu. Podczas testowania, możesz wybrać **wolne**.
      * W **rozmiar wystąpienia** menu rozwijanego, wybierz odpowiednie wystąpienie rozmiaru planu. Podczas testowania, możesz wybrać **małych**.
      * Kliknij przycisk **OK**.
   8. (Opcjonalnie) Domyślnie ostatnie dystrybucji Java 8 zostanie automatycznie wdrożone jako sieci maszyny wirtualnej Java na platformie Azure do kontener aplikacji sieci web. Można jednak wybrać inną wersję i dystrybucji maszyna JVM. Aby to zrobić, wykonaj następujące kroki:
      
      * Kliknij przycisk **JDK** karcie **nowy kontener aplikacji sieci Web** okno dialogowe.
      * Można wybrać jedną z następujących opcji:
        
        * Wdróż domyślne JDK, który jest oferowany na platformie Azure
        * Wdrażanie 3 strona JDK z listy rozwijanej JDKs dodatkowe, które są dostępne w systemie Azure
        * Wdrażanie niestandardowych JDK, które muszą być spakowane jako plik ZIP i albo publicznie dostępnych lub na koncie magazynu Azure
        
        ![Nowa karta JDK kontenera aplikacji][11b]
   9. Po zakończeniu wszystkich kroków opisanych powyżej, okno dialogowe nowy kontener aplikacji sieci Web powinien wyglądać poniższej ilustracji:
      
       ![Nowy kontener aplikacji][14]
   10. Kliknij przycisk **OK** aby zakończyć tworzenie użytkownika nowy kontener aplikacji sieci Web.
       
        Poczekaj kilka sekund na liście kontenery aplikacji sieci Web należy odświeżyć, a kontener aplikacji sieci web nowo utworzony powinny teraz być zaznaczone na liście.
6. Teraz można przystąpić do ukończenia pierwszego wdrożenia aplikacji sieci Web na platformie Azure; Kliknij przycisk **OK** do wdrożenia aplikacji do wybranego kontenera aplikacji sieci Web w języku Java. Domyślnie aplikacja zostanie wdrożona jako podkatalog serwera aplikacji. Sprawdź, czy ma to być wdrożony jako aplikacja główna **Wdróż głównym** wyboru przed kliknięciem przycisku **OK**.
   
    ![Wdrażanie na platformie Azure][15]
7. Następnie zostanie wyświetlony **dziennika aktywności platformy Azure** widoku, który wskazuje stan wdrożenia aplikacji sieci Web.
   
    ![Wskaźnik postępu][16]
   
    Proces wdrażania aplikacji sieci Web na platformie Azure powinien zająć tylko kilka sekund. Jeśli możesz już aplikacji, zobaczysz łącze o nazwie **opublikowano** w **stan** kolumny. Po kliknięciu łącza spowoduje przejście do strony głównej wdrożonej aplikacji sieci Web lub aby przejść do aplikacji sieci web służy kroki opisane w poniższej sekcji.

## <a name="browsing-to-your-web-app-on-azure"></a>Przeglądanie do aplikacji sieci Web na platformie Azure
Aby przejść do aplikacji sieci Web na platformie Azure, można użyć **Eksploratora Azure** widoku.

Jeśli **Eksploratora Azure** widoku nie jest jeszcze otwarty, otwórz go, klikając następnie **widoku** menu w IntelliJ, następnie kliknij przycisk **okna narzędzi**, a następnie kliknij przycisk  **Eksplorator usługi**. Jeśli dany system nie zostały wcześniej zarejestrowane, monit podczas wykonywania.

Gdy **Eksploratora Azure** zostanie wyświetlony widok, użyj wykonaj następujące kroki, aby przejść do aplikacji sieci Web: 

1. Rozwiń węzeł **Azure** węzła.
2. Rozwiń węzeł **aplikacje sieci Web** węzła. 
3. Kliknij prawym przyciskiem myszy odpowiednią aplikację sieci Web.
4. W menu kontekstowym kliknij **Otwórz w przeglądarce**.
   
    ![Przeglądanie aplikacji sieci Web][17]

## <a name="updating-your-web-app"></a>Aktualizowanie aplikacji sieci Web
Aktualizowanie istniejącej uruchamiania aplikacji sieci Web platformy Azure jest procesem szybkie i łatwe i dostępne są dwie opcje aktualizacji:

* Można aktualizować wdrażania istniejącej aplikacji sieci Web Java.
* Możesz opublikować aplikację Java dodatkowe do tego samego kontenera aplikacji sieci Web.

W obu przypadkach proces jest identyczne i zajmuje tylko kilka sekund:

1. W obszarze Eksplorator projektów IntelliJ kliknij prawym przyciskiem myszy aplikację Java, który chcesz zaktualizować, lub Dodaj do istniejącego kontenera aplikacji sieci Web.
2. Po wyświetleniu menu kontekstowego wybierz **Azure** , a następnie **Publikuj jako aplikacji sieci Web platformy Azure...**
3. Ponieważ użytkownik ma już zalogowany wcześniej, zostanie wyświetlona lista sieci kontenerów istniejących aplikacji sieci Web. Wybierz ten, który chcesz opublikować lub ponownie opublikować aplikację Java i kliknij przycisk **OK**.

Później, gdzie po kilku sekundach **dziennika aktywności platformy Azure** widoku wyświetli zaktualizowane wdrożenia jako **opublikowano** i będzie mógł zweryfikować zaktualizowane aplikacji w przeglądarce sieci web.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Uruchamianie, zatrzymywanie lub ponowne uruchamianie istniejących aplikacji sieci web
Aby rozpocząć lub zatrzymać istniejącego kontenera aplikacji sieci Web platformy Azure (w tym wszystkich wdrożonych aplikacji Java w nim), można użyć **Eksploratora Azure** widoku.

Jeśli **Eksploratora Azure** widoku nie jest jeszcze otwarty, otwórz go, klikając następnie **widoku** menu w IntelliJ, następnie kliknij przycisk **okna narzędzi**, a następnie kliknij przycisk  **Eksplorator usługi**. Jeśli dany system nie zostały wcześniej zarejestrowane, monit podczas wykonywania.

Gdy **Eksploratora Azure** zostanie wyświetlony widok, użyj wykonaj następujące kroki, aby uruchomić lub zatrzymać aplikacji sieci Web: 

1. Rozwiń węzeł **Azure** węzła.
2. Rozwiń węzeł **aplikacje sieci Web** węzła. 
3. Kliknij prawym przyciskiem myszy odpowiednią aplikację sieci Web.
4. W menu kontekstowym kliknij **Start**, **zatrzymać**, lub **ponownego uruchomienia**. Należy zauważyć, że opcji menu kontekstowe obsługujący, więc tylko zatrzymać uruchomionej aplikacji sieci web ani uruchomić aplikacji sieci web, która nie jest obecnie uruchomiona.
   
    ![Zatrzymać aplikacji sieci Web][18]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o zestawach narzędzi platformy Azure dla środowisk IDE języka Java, skorzystaj z następujących linków:

* [Azure zestawu narzędzi dla programu Eclipse]
  * [Installing the Azure Toolkit for Eclipse] (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)
  * [Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]
  * [What's New in the Azure Toolkit for Eclipse] (Co nowego w zestawie narzędzi platformy Azure dla środowiska Eclipse)
* [narzędzi Azure dla IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
  * [Instalowanie zestawu narzędzi platformy Azure dla IntelliJ] (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)
  * *Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ (w tym artykule)*
  * [What's New in the Azure Toolkit for IntelliJ] (Co nowego w zestawie narzędzi platformy Azure dla środowiska IntelliJ)

<a name="see-also"></a>

## <a name="see-also"></a>Zobacz też
Aby uzyskać więcej informacji o używaniu platformy Azure z językiem Java, zobacz [Azure Java Developer Center].

Aby uzyskać dodatkowe informacje dotyczące tworzenia aplikacji sieci Web platformy Azure, zobacz [Omówienie aplikacji sieci Web].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ../azure-toolkit-for-eclipse.md
[narzędzi Azure dla IntelliJ]: ../azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)
[Instalowanie zestawu narzędzi platformy Azure dla IntelliJ]: ../azure-toolkit-for-intellij-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)
[What's New in the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md (Co nowego w zestawie narzędzi platformy Azure dla środowiska Eclipse)
[What's New in the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md (Co nowego w zestawie narzędzi platformy Azure dla środowiska IntelliJ)

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Omówienie aplikacji sieci Web]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
