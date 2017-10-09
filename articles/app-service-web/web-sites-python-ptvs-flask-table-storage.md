---
title: "aaaFlask i Azure Table Storage na platformie Azure za pomocą narzędzia Python Tools 2.2 for Visual Studio"
description: "Dowiedz się jak toouse hello narzędzi Python Tools dla Visual Studio toocreate aplikacji sieci web platformy Flask, która przechowuje dane w magazynie tabel platformy Azure i wdróż je tooAzure aplikacji usługi sieci Web aplikacji."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: d8e70a29-aca1-4010-95f5-cfe769e3be06
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1a09d4cc78078a00492ba4fe7e2075df96fb0380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a>Flask i magazynu tabel platformy Azure na platformie Azure przy użyciu narzędzi Python Tools 2.2 for Visual Studio
W tym samouczku użyjemy [narzędzi Python Tools for Visual Studio] toocreate prostą sonduje aplikacji sieci web przy użyciu jednej z hello PTVS przykładowe szablony. W tym samouczku jest również dostępny jako [wideo](https://www.youtube.com/watch?v=qUtZWtPwbTk).

aplikacji sieci web sond Hello definiuje abstrakcję do repozytorium, więc można łatwo przełączać się między różnymi typami repozytoriów (w pamięci, magazynu tabel Azure, MongoDB).

Dowiesz się, jak konto toocreate magazynu Azure, jak tooconfigure hello toouse aplikacji sieci web Azure Table Storage i jak toopublish hello aplikacji sieci web zbyt[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

Zobacz hello [Centrum deweloperów języka Python] więcej artykułów o programowaniu aplikacji sieci Web usługi aplikacji Azure z narzędziami PTVS przy użyciu Bottle, Flask i Django oraz sieci web z usługami bazy danych MongoDB, Magazyn tabel Azure, MySQL i bazy danych SQL. Gdy ten artykuł dotyczy usługi App Service, hello kroki są podobne do programowania [usługi w chmurze Azure].

## <a name="prerequisites"></a>Wymagania wstępne
* Visual Studio 2015
* [Python Tools 2.2 for Visual Studio]
* [Python Tools 2.2 for Visual Studio przykładów VSIX]
* [Azure SDK Tools for VS 2015]
* [32-bitowe środowisko Python w wersji 2.7] lub [32-bitowe środowisko Python w wersji 3.4]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="create-hello-project"></a>Utwórz hello projektu
W tej sekcji utworzymy projektu programu Visual Studio przy użyciu przykładowego szablonu. Firma Microsoft będzie utworzyć środowisko wirtualne i zainstalujesz wymagane pakiety. Następnie zostanie uruchomiony aplikacji hello lokalnie za pomocą hello domyślne w pamięci repozytorium.

1. W programie Visual Studio wybierz pozycje **Plik**, **Nowy projekt**.
2. Szablony projektu z hello Hello [Python Tools 2.2 for Visual Studio przykładów VSIX] są dostępne w ramach **Python**, **przykłady**. Wybierz **projektu sieci Web platformy Flask sond** i kliknij przycisk OK toocreate hello projektu.
   
     ![Okno dialogowe Nowy projekt](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. Pakiety zewnętrzne zostanie wyświetlony monit o tooinstall będzie. Wybierz pozycję **Zainstaluj w środowisku wirtualnym**.
   
     ![Okno dialogowe Pakiety zewnętrzne](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. Wybierz **Python 2.7** lub **języka Python 3.4** jako podstawowy interpreter hello.
   
     ![Okno dialogowe Dodawanie środowiska wirtualnego](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. Upewnij się, że aplikacja hello działa, naciskając `F5`. Domyślnie aplikacja hello używa repozytorium w pamięci, które nie wymaga żadnej konfiguracji. Wszystkie dane zostaną utracone, gdy serwer sieci web hello jest zatrzymana.
6. Kliknij przycisk **tworzenie przykładowej ankiety**, kliknij ankietę i Zagłosuj.
   
     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a>Utwórz konto magazynu platformy Azure
operacje magazynu toouse, potrzebne jest konto magazynu Azure. Można utworzyć konta magazynu, wykonując następujące kroki.

1. Zaloguj się do hello [Azure Portal](https://portal.azure.com/).
2. Kliknij przycisk hello **nowy** ikony na górze hello rogu hello portalu, kliknij przycisk **dane i magazyn** > **konta magazynu**. Polecenie **Utwórz**, nadaj unikatową nazwę konta magazynu hello i utworzyć nową [grupy zasobów](../azure-resource-manager/resource-group-overview.md) dla niego.
   
      ![Szybkie tworzenie](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    Po utworzeniu konta magazynu hello hello **powiadomienia** przycisk będzie flash zielona **Powodzenie** i bloku konto magazynu hello jest otwarty tooshow należy toohello nowy zasób grupy utworzony.
3. Kliknij przycisk hello **klucze dostępu** część w bloku konto magazynu hello. Zanotuj nazwę konta hello i klucz1 hello.
   
      ![Klucze](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    Projekt w następnej sekcji hello są wymagane tooconfigure tej informacji.

## <a name="configure-hello-project"></a>Skonfiguruj hello projektu
W tej sekcji skonfigurujemy naszej aplikacji toouse hello konta magazynu, którą właśnie utworzyliśmy. Zajmiemy się tym, jak tooobtain ustawienia połączenia z hello portalu Azure. Następnie aplikacja hello zostanie uruchomiony lokalnie.

1. W programie Visual Studio, kliknij prawym przyciskiem myszy węzeł projektu w Eksploratorze rozwiązań i wybierz **właściwości**. Polecenie hello **debugowania** kartę.
   
     ![Ustawienia debugowania projektu](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. Ustaw wartości hello wymagane przez aplikację hello w zmiennych środowiskowych **polecenia Debug serwera**, **środowiska**.
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   Spowoduje to ustawienie zmiennych środowiskowych hello podczas możesz **Rozpocznij debugowanie**. Toobe zmienne hello ustawić podczas możesz **uruchomić bez debugowania**, hello zestaw takie same wartości w obszarze **uruchamiania polecenia serwera** również.
   
   Alternatywnie można zdefiniować zmienne środowiskowe za pomocą Panelu sterowania systemu Windows hello. Jest lepszym rozwiązaniem, jeśli chcesz tooavoid przechowywania poświadczeń w kodzie źródłowym / pliku projektu. Należy pamiętać, że konieczne będzie toorestart programu Visual Studio dla nowego środowiska hello wartości toobe toohello dostępnych aplikacji.
3. Kod Hello implementuje repozytorium Azure Table Storage hello jest **models/azuretablestorage.py**. Zobacz hello [dokumentacji] Aby uzyskać więcej informacji na temat toouse usługi tabel w języku Python.
4. Uruchamianie aplikacji hello z `F5`. Ankieta utworzona za pomocą **tworzenie przykładowej ankiety** i hello dane przesłane podczas głosowania zostaną zserializowane w magazynu tabel platformy Azure.
   
   > [!NOTE]
   > Hello środowiska wirtualnego Python 2.7 może spowodować wyjątek podziału w programie Visual Studio.  Naciśnij klawisz `F5` toocontinue ładowania hello projektu sieci web.
   > 
   > 
5. Przeglądaj toohello **o** tooverify strony, która aplikacja hello używa hello **Azure Table Storage** repozytorium.
   
     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a>Eksploruj hello Azure Table Storage
Jest łatwy tooview i edytowanie tabel do przechowywania Eksploratorze chmury w programie Visual Studio. W tej sekcji użyjemy Eksploratora serwera tooview hello zawartość tabel aplikacji hello ankiety.

> [!NOTE]
> Wymaga to Microsoft Azure Tools toobe zainstalowane, które są dostępne jako część hello [zestawu Azure SDK dla platformy .NET].
> 
> 

1. Otwórz **Cloud Explorer**. Rozwiń węzeł **kont magazynu**, konta magazynu, następnie **tabel**.
   
     ![Eksplorator chmury](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. Kliknij dwukrotnie hello **sond** lub **opcji** tabeli tooview hello zawartości tabeli hello w oknie dokumentu, a także dodawanie/usuwanie/edytowanie jednostek.
   
     ![Wyniki zapytania w tabeli](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a>Publikowanie tooAzure aplikacji sieci web hello usługi aplikacji
Hello Azure .NET SDK udostępnia toodeploy łatwy sposób tooAzure aplikacji sieci web usługi aplikacji.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz **publikowania**.
   
     ![Okno dialogowe Publikowanie w sieci Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. Kliknij pozycję **Microsoft Azure Web Apps**.
3. Polecenie **nowy** toocreate nowej aplikacji sieci web.
4. Wypełnij następujące pola hello i kliknij przycisk **Utwórz**.
   
   * **Nazwa aplikacji sieci Web**
   * **Plan usługi App Service**
   * **Grupa zasobów**
   * **Region**
   * Pozostaw **serwera bazy danych** ustawić także**bazy danych**
5. Zaakceptuj wszystkie inne ustawienia domyślne i kliknij przycisk **Opublikuj**.
6. Przeglądarki sieci web zostanie otwarty toohello opublikowana aplikacja sieci web. Jeśli przeglądania toohello o stronie zostanie wyświetlone, korzysta z hello **w pamięci** repozytorium, nie hello **Azure Table Storage** repozytorium.
   
   Jest to spowodowane hello zmienne środowiskowe nie są ustawione na powitania wystąpienia aplikacji sieci Web w usłudze Azure App Service, więc używa hello domyślne wartości podanych w tym **settings.py**.

## <a name="configure-hello-web-apps-instance"></a>Skonfiguruj hello wystąpienie aplikacji sieci Web
W tej sekcji skonfigurujemy zmiennych środowiskowych dla hello wystąpienia aplikacji sieci Web.

1. W [portalu Azure](https://portal.azure.com), otwarcie bloku aplikacji sieci web hello klikając **Przeglądaj** > **usługi aplikacji** > Nazwa aplikacji sieci web.
2. W bloku aplikacja sieci web, kliknij przycisk **wszystkie ustawienia**, następnie kliknij przycisk **ustawienia aplikacji**.
3. Przewiń w dół toohello **ustawień aplikacji** sekcji i ustawiać wartości hello **REPOZYTORIUM\_nazwa**, **MAGAZYNU\_nazwa** i  **Magazyn\_klucza** zgodnie z opisem w hello **projektu hello Konfiguruj** powyższej sekcji.
   
     ![Ustawienia aplikacji](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. Kliknij przycisk **Zapisz**. Po otrzymaniu powiadomienia hello czy hello zmiany zostały zastosowane, kliknij **Przeglądaj** z głównego bloku aplikacja sieci Web hello.
5. Powinny pojawić się pracy aplikacji sieci web hello zgodnie z oczekiwaniami, za pomocą hello **Azure Table Storage** repozytorium.
   
   Gratulacje!
   
     ![Przeglądarka internetowa](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a>Następne kroki
Wykonaj te toolearn łącza więcej informacji na temat narzędzi Python Tools for Visual Studio, Flask i Azure Table Storage.

* [Dokumentacja narzędzi Python Tools for Visual Studio]
  * [Projekty sieci Web]
  * [Projekty usługi w chmurze]
  * [Debugowanie zdalne na platformie Microsoft Azure]
* [Dokumentacja platformy flask]
* [Azure Storage]
* [Zestaw Azure SDK dla środowiska Python]
* [Jak tooUse hello usługi Magazyn tabel w języku Python]

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Centrum deweloperów języka Python]: /develop/python/
[usługi w chmurze Azure]: ../cloud-services/cloud-services-python-ptvs.md
[dokumentacji]:../cosmos-db/table-storage-how-to-use-python.md
[Jak tooUse hello usługi Magazyn tabel w języku Python]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[zestawu Azure SDK dla platformy .NET]: http://azure.microsoft.com/downloads/
[narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio przykładów VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?linkid=518003
[32-bitowe środowisko Python w wersji 2.7]: http://go.microsoft.com/fwlink/?LinkId=517190
[32-bitowe środowisko Python w wersji 3.4]: http://go.microsoft.com/fwlink/?LinkId=517191
[Dokumentacja narzędzi Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Dokumentacja platformy flask]: http://flask.pocoo.org/
[Debugowanie zdalne na platformie Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projekty sieci Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projekty usługi w chmurze]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure Storage]: http://azure.microsoft.com/documentation/services/storage/
[Zestaw Azure SDK dla środowiska Python]: https://github.com/Azure/azure-sdk-for-python
