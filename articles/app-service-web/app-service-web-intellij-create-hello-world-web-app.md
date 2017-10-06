---
title: w aplikacji sieci web platformy Azure podstawowe w IntelliJ aaaCreate | Dokumentacja firmy Microsoft
description: "Ten samouczek pokazuje, jak toouse hello Azure zestawu narzędzi dla IntelliJ toocreate aplikacji Hello World sieci Web dla platformy Azure."
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
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a>Tworzenie aplikacji sieci web platformy Azure podstawowe w IntelliJ
Ten samouczek pokazuje, jak toocreate i wdrażania podstawowych tooAzure aplikacji Hello World jako aplikacji sieci Web przy użyciu hello [narzędzi Azure dla IntelliJ]. Podstawowy przykład JSP jest widoczna dla uproszczenia, ale podobne kroki będzie odpowiednia dla serwlet Java, jakim jest dotyczy wdrożenia usługi Azure.

Po ukończeniu tego samouczka, aplikacja będzie wyglądać podobnie toohello następującej ilustracji, podczas wyświetlania w przeglądarce sieci web:

![Przykładowa strona sieci Web][01]

## <a name="prerequisites"></a>Wymagania wstępne
* Java Developer Kit (JDK), v 1,8 lub nowszej.
* IntelliJ IDEA Ultimate Edition. Ten można pobrać z <https://www.jetbrains.com/idea/download/index.html>.
* Dystrybucji serwera sieci web opartych na języku Java lub serwera aplikacji takich jak [Apache Tomcat] lub [Jetty].
* Subskrypcję platformy Azure, która może zostać pobrany z <https://azure.microsoft.com/free/> lub <http://azure.microsoft.com/pricing/purchase-options/>.
* Witaj [narzędzi Azure dla IntelliJ]. Informacje o instalowaniu hello zestawu narzędzi platformy Azure, zobacz [hello Instalowanie narzędzi Azure dla IntelliJ].

## <a name="toocreate-a-hello-world-application"></a>toocreate aplikacji Hello World
Po pierwsze Zaczniemy tworzenia projektu języka Java.

1. Uruchom środowisko IntelliJ i kliknij przycisk hello **pliku** menu, następnie kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.
   
    ![Nowy projekt pliku][02]
2. Okno dialogowe Nowy projekt hello, wybierz **Java**, następnie **aplikacji sieci Web**, a następnie kliknij przycisk **nowy** tooadd SDK projektu.
   
    ![Okno dialogowe Nowy projekt][03a]
   
3. W hello Wybieranie katalogu macierzystego dla okna dialogowego JDK, wybierz hello zainstalowanym JDK z folderu, a następnie kliknij przycisk **OK**. Kliknij przycisk **dalej** w toocontinue okno dialogowe Nowy projekt hello.
   
    ![Określ katalog macierzysty JDK][03b]
4. Do celów tego samouczka, nazwa projektu hello **Java sieci Web-App-na-Azure**, a następnie kliknij przycisk **Zakończ**.
   
    ![Okno dialogowe Nowy projekt][04]
5. W widoku Project Explorer IntelliJ firmy, rozwiń węzeł **Java sieci Web-App-na-Azure**, następnie rozwiń węzeł **web**, a następnie kliknij dwukrotnie **index.jsp**.
   
    ![Otwórz indeks strony][05c]
6. Po otwarciu pliku index.jsp w IntelliJ dodatek do wyświetlania tekstu toodynamically **Hello World!** w ramach istniejącego hello `<body>` elementu. Zaktualizowana `<body>` zawartość powinna wyglądać hello poniższy przykład:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. Zapisz index.jsp.

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy Twojego tooan aplikacji kontenera aplikacji sieci Web Azure
Istnieje kilka metod, które można wdrożyć tooAzure aplikacji sieci web Java. Ten samouczek zawiera opis jednego z hello najprostszym: aplikacja będzie tooan wdrożony kontener aplikacji sieci Web platformy Azure — żadnych typ projektu ani dodatkowe narzędzia są niezbędne. Hello JDK i hello kontenera oprogramowanie dla sieci web zostanie zostać dostarczony przez platformę Azure, więc nie ma żadnych tooupload potrzeby własne; potrzebna jest aplikacja sieci Web Java. W związku z tym hello proces publikowania aplikacji może zająć sekund, nie minut.

Przed opublikowaniem aplikacji, należy najpierw tooconfigure ustawienia modułu. toodo tak, użycie hello następujące kroki:

1. W obszarze Eksplorator projektów w IntelliJ, kliknij prawym przyciskiem myszy hello **Java sieci Web-App-na-Azure** projektu. Po wyświetleniu menu kontekstowe powitania kliknij **Otwórz ustawienia modułu**.

    ![Otwórz ustawienia modułu][05a]
2. Gdy zostanie wyświetlone okno dialogowe hello struktury projektu:

   a. Kliknij przycisk **artefakty** liście hello **ustawienia projektu**.
   b. Nazwa artefaktu hello zmian w hello **nazwa** , dzięki czemu nie zawiera spacji ani znaków specjalnych; jest to konieczne, ponieważ nazwa hello będą używane w hello jednolity identyfikator zasobów (URI).
   c. Zmień hello **typu** za**aplikacji sieci Web: archiwum**.
   d. Kliknij przycisk **OK** tooclose hello struktury projektu okno dialogowe.

    ![Otwórz ustawienia modułu][05b]

Po skonfigurowaniu ustawień modułu można opublikować tooAzure Twojej aplikacji za pomocą hello następujące kroki:

1. W obszarze Eksplorator projektów w IntelliJ, kliknij prawym przyciskiem myszy hello **Java sieci Web-App-na-Azure** projektu. Po wyświetleniu menu kontekstowe hello zaznacz **Azure**, a następnie kliknij przycisk **Publikuj jako aplikacji sieci Web platformy Azure...**
   
    ![Menu kontekstowe publikowania na platformie Azure][06]
2. Jeśli dany komputer nie ma już podpisany na platformie Azure z IntelliJ, będzie zostanie wyświetlony monit o toosign do konta platformy Azure. (Jeśli masz wiele kont platformy Azure, część hello monity podczas logowania hello w procesie mogą być wyświetlane więcej niż raz, nawet wtedy, gdy pojawią się one toobe hello takie same. W takim przypadku należy kontynuować toofollow hello logowania w instrukcjach.)
   
    ![Azure dziennika w oknie dialogowym][07]
3. Po pomyślnym zarejestrowaniu do konta platformy Azure, hello **Zarządzaj subskrypcjami** dialogowym zostanie wyświetlona lista subskrypcji, które są skojarzone z poświadczeniami użytkownika. (Jeśli istnieje wiele wymienionych subskrypcji i chcesz toowork z konkretnego podzestawu z nich, może opcjonalnie Usuń zaznaczenie hello subskrypcji nie mają toouse.) Po zakończeniu wybierania subskrypcji, kliknij przycisk **Zamknij**.
   
    ![Zarządzanie subskrypcjami][08]
4. Gdy hello **wdrażanie tooAzure kontenera aplikacji sieci Web** zostanie wyświetlone okno dialogowe będzie ono żadnych kontenerów aplikacji sieci Web, które wcześniej zostały utworzone; Jeśli nie utworzono żadnych kontenerów, hello lista jest pusta.
   
    ![Kontenery aplikacji][09]
5. Jeśli nie utworzono kontener aplikacji sieci Web Azure przed lub jeśli chcesz toopublish Twojej aplikacji tooa nowy kontener, użyj hello następujące kroki. W przeciwnym razie wybierz kontener istniejących aplikacji sieci Web i pominąć toostep 6 poniżej.
   
   1. Kliknij przycisk**+**
      
       ![Dodawanie aplikacji kontenera][10]
   2. Witaj **nowy kontener aplikacji sieci Web** można wyświetlić okna dialogowego, który będzie używany dla hello obok kilku kroków.
      
       ![Nowy kontener aplikacji][11a]
   3. Wprowadź **Etykieta DNS** dla kontener aplikacji sieci Web; to będzie stanowić etykietę DNS liścia hello hello hosta adres URL aplikacji sieci web na platformie Azure. Należy pamiętać, że nazwa hello musi być dostępny i jest zgodna z wymaganiami dotyczącymi nazw aplikacji sieci Web tooAzure.
   4. W hello **kontener sieci Web** menu rozwijanego, wybierz hello odpowiedniego oprogramowania dla aplikacji.
      
       Obecnie można wybrać z Tomcat 8 Tomcat 7 lub Jetty 9. Ostatnie dystrybucji oprogramowania hello wybrane będą udostępniane przez usługi Azure, a zostanie uruchomiony na ostatnie dystrybucji 8 JDK utworzone przez firmę Oracle i dostarczany przez platformę Azure.
   5. W hello **subskrypcji** menu rozwijanego, wybierz hello subskrypcję toouse dla tego wdrożenia.
   6. W hello **grupy zasobów** menu rozwijane i wybierz hello grupy zasobów, z którą chcesz tooassociate aplikacji sieci Web. (Zezwalaj grup zasobów platformy azure możesz toogroup powiązane ze sobą zasoby, tak, aby na przykład je usunąć ze sobą.)
      
       Można wybrać istniejącą grupę zasobów (jeśli) i Pomiń toostep g poniżej lub użyj hello następujące kroki toocreate nową grupę zasobów:
      
      * Wybierz  **&lt; &lt; Utwórz nową grupę zasobów &gt; &gt;**  w hello **grupy zasobów** menu rozwijanego.
      * Witaj **nową grupę zasobów** wyświetli się okno dialogowe:
        
          ![Nową grupę zasobów][12]
      * W hello hello **nazwa** pole tekstowe, określ nazwę nowej grupy zasobów.
      * W hello hello **Region** menu rozwijanego wybierz hello odpowiednie usługi Azure data center lokalizację dla grupy zasobów.
      * Kliknij przycisk **OK**.
   7. Witaj **planu usługi App Service** hello planów usługi aplikacji, które są skojarzone z hello wybrana grupa zasobów zawiera menu rozwijanego. (Plan usługi App Service określa informacje, takie jak lokalizacja hello aplikacji sieci Web, hello warstwa cenowa i rozmiar wystąpienia obliczeniowe hello. Jeden Plan usługi App Service może służyć do wielu aplikacji sieci Web, dlatego jest obsługiwana oddzielnie od określonego wdrożenia aplikacji sieci Web.)
      
       Można wybrać istniejący Plan usługi App Service (jeśli) i Pomiń h toostep poniżej, lub użyj hello następujące kroki toocreate planu usługi aplikacji:
      
      * Wybierz  **&lt; &lt; Utwórz nowy Plan usługi App Service &gt; &gt;**  w hello **planu usługi App Service** menu rozwijanego.
      * Witaj **nowy Plan usługi App Service** wyświetli się okno dialogowe:
        
          ![Nowy Plan usługi aplikacji][13]
      * W hello hello **nazwa** pole tekstowe, określ nazwę planu usługi aplikacji.
      * W hello hello **lokalizacji** menu rozwijanego wybierz hello odpowiednie usługi Azure data center lokalizacji dla planu hello.
      * W hello hello **warstwy cenowej** menu rozwijanego, wybierz odpowiednie ceny dla planu hello hello. Podczas testowania, możesz wybrać **wolne**.
      * W hello hello **rozmiar wystąpienia** menu rozwijanego, hello wybierz odpowiednie wystąpienie rozmiar hello planu. Podczas testowania, możesz wybrać **małych**.
      * Kliknij przycisk **OK**.
   8. (Opcjonalnie) Domyślnie ostatnie dystrybucji Java 8 będą automatycznie wdrażane jako sieci maszyny wirtualnej Java przez kontener aplikacji sieci web Azure tooyour. Można jednak wybrać inną wersję i dystrybucji hello maszyny JVM. toodo tak, użycie hello następujące kroki:
      
      * Kliknij przycisk hello **JDK** kartę w hello **nowy kontener aplikacji sieci Web** okno dialogowe.
      * Można wybrać jedną z hello następujące opcje:
        
        * Wdróż domyślne hello JDK, który jest oferowany na platformie Azure
        * Wdrażanie 3 strona JDK z listy rozwijanej JDKs dodatkowe, które są dostępne w systemie Azure
        * Wdrażanie niestandardowych JDK, które muszą być spakowane jako plik ZIP i albo publicznie dostępnych lub na koncie magazynu Azure
        
        ![Nowa karta JDK kontenera aplikacji][11b]
   9. Po wykonaniu wszystkich hello powyżej kroki, okno dialogowe nowy kontener aplikacji sieci Web hello powinien wyglądać hello następującej ilustracji:
      
       ![Nowy kontener aplikacji][14]
   10. Kliknij przycisk **OK** tworzenie hello toocomplete Twojego nowego kontenera aplikacji sieci Web.
       
        Zaczekaj kilka sekund hello lista toobe kontenery sieci Web aplikacji hello odświeżyć, a kontener aplikacji sieci web nowo utworzony powinny teraz być zaznaczone na liście hello.
6. Wszystko jest teraz gotowy toocomplete hello początkowe wdrożenie tooAzure Twojej aplikacji sieci Web; Kliknij przycisk **OK** toodeploy Twojego toohello aplikacji Java wybrany kontener aplikacji sieci Web. Domyślnie aplikacja zostanie wdrożona jako podkatalog serwera aplikacji hello. Jeśli chcesz toobe wdrożony jako aplikacja główna hello, sprawdź hello **wdrażanie tooroot** wyboru przed kliknięciem przycisku **OK**.
   
    ![Wdrażanie tooAzure][15]
7. Następnie powinna zostać wyświetlona hello **dziennika aktywności platformy Azure** widoku, który będzie wskazywać hello stan wdrożenia aplikacji sieci Web.
   
    ![Wskaźnik postępu][16]
   
    Hello proces wdrażania tooAzure Twojej aplikacji sieci Web powinien zająć tylko kilka sekund toocomplete. Jeśli możesz już aplikacji, zobaczysz łącze o nazwie **opublikowano** w hello **stan** kolumny. Po kliknięciu łącza hello potrwa strony głównej aplikacji sieci Web tooyour wdrożona lub hello czynności można użyć w następującej aplikacji sieci web tooyour toobrowse sekcji hello.

## <a name="browsing-tooyour-web-app-on-azure"></a>Przeglądanie tooyour aplikacji sieci Web na platformie Azure
tooyour toobrowse aplikacji sieci Web na platformie Azure, można użyć hello **Eksploratora Azure** widoku.

Jeśli hello **Eksploratora Azure** widoku nie jest jeszcze otwarty, otwórz go, klikając następnie **widoku** menu w IntelliJ, następnie kliknij przycisk **okna narzędzi**, a następnie kliknij przycisk  **Eksplorator usługi**. Jeśli dany system nie zostały wcześniej zarejestrowane, go spowoduje wyświetlenie monitu toodo tak.

Gdy hello **Eksploratora Azure** zostanie wyświetlony widok, użyj wykonaj te kroki toobrowse tooyour aplikacji sieci Web: 

1. Rozwiń węzeł hello **Azure** węzła.
2. Rozwiń węzeł hello **aplikacje sieci Web** węzła. 
3. Kliknij prawym przyciskiem myszy hello żądana aplikacji sieci Web.
4. Po wyświetleniu menu kontekstowe powitania kliknij **Otwórz w przeglądarce**.
   
    ![Przeglądanie aplikacji sieci Web][17]

## <a name="updating-your-web-app"></a>Aktualizowanie aplikacji sieci Web
Aktualizowanie istniejącej uruchamiania aplikacji sieci Web platformy Azure jest procesem szybkie i łatwe i dostępne są dwie opcje aktualizacji:

* Można aktualizować hello wdrażania istniejącej aplikacji sieci Web Java.
* Możesz opublikować dodatkowe toohello aplikacji Java tego samego kontenera aplikacji sieci Web.

W obu przypadkach procesu hello jest identyczne i zajmuje tylko kilka sekund:

1. W obszarze Eksplorator projektów IntelliJ hello kliknij prawym przyciskiem myszy aplikacji Java hello mają tooupdate lub Dodaj tooan istniejącego kontenera aplikacji sieci Web.
2. Po wyświetleniu menu kontekstowe hello zaznacz **Azure** , a następnie **Publikuj jako aplikacji sieci Web platformy Azure...**
3. Ponieważ użytkownik ma już zalogowany wcześniej, zostanie wyświetlona lista sieci kontenerów istniejących aplikacji sieci Web. Wybierz hello mają toopublish lub ponownie opublikować kliknięcia tooand aplikacji Java **OK**.

Hello później za kilka sekund **dziennika aktywności platformy Azure** widoku wyświetli zaktualizowane wdrożenia jako **opublikowano** i będą mogli tooverify zaktualizowane aplikacji w przeglądarce sieci web.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Uruchamianie, zatrzymywanie lub ponowne uruchamianie istniejących aplikacji sieci web
toostart lub zatrzymać istniejącego kontenera aplikacji sieci Web platformy Azure (w tym wszystkich aplikacji Java hello wdrożone w nim), możesz użyć hello **Eksploratora Azure** widoku.

Jeśli hello **Eksploratora Azure** widoku nie jest jeszcze otwarty, otwórz go, klikając następnie **widoku** menu w IntelliJ, następnie kliknij przycisk **okna narzędzi**, a następnie kliknij przycisk  **Eksplorator usługi**. Jeśli dany system nie zostały wcześniej zarejestrowane, go spowoduje wyświetlenie monitu toodo tak.

Gdy hello **Eksploratora Azure** zostanie wyświetlony widok, użyj wykonaj te kroki toostart lub Zatrzymaj aplikację sieci Web: 

1. Rozwiń węzeł hello **Azure** węzła.
2. Rozwiń węzeł hello **aplikacje sieci Web** węzła. 
3. Kliknij prawym przyciskiem myszy hello żądana aplikacji sieci Web.
4. Po wyświetleniu menu kontekstowe powitania kliknij **Start**, **zatrzymać**, lub **ponownego uruchomienia**. Należy zauważyć, że hello menu opcji kontekstu obsługujący, więc tylko zatrzymać uruchomionej aplikacji sieci web ani uruchomić aplikacji sieci web, która nie jest obecnie uruchomiona.
   
    ![Zatrzymać aplikacji sieci Web][18]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat hello narzędzi Azure dla języka Java IDEs Zobacz hello następującego łącza:

* [Azure zestawu narzędzi dla programu Eclipse]
  * [Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]
  * [Nowości w hello zestawu narzędzi platformy Azure dla programu Eclipse]
* [narzędzi Azure dla IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
  * [hello Instalowanie narzędzi Azure dla IntelliJ]
  * *Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ (w tym artykule)*
  * [Nowości w hello Azure Toolkit for IntelliJ]

<a name="see-also"></a>

## <a name="see-also"></a>Zobacz też
Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center].

Aby uzyskać dodatkowe informacje dotyczące tworzenia aplikacji sieci Web platformy Azure, zobacz hello [Omówienie aplikacji sieci Web].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ../azure-toolkit-for-eclipse.md
[narzędzi Azure dla IntelliJ]: ../azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[hello Instalowanie narzędzi Azure dla IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Nowości w hello zestawu narzędzi platformy Azure dla programu Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Nowości w hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

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
