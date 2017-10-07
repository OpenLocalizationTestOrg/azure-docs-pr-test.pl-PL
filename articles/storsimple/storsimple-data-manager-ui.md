---
title: "aaaMicrosoft interfejsu użytkownika Menedżera danych StorSimple Azure | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toouse usługi Menedżer StorSimple danych interfejsu użytkownika (podglądzie prywatnym)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b0ee12b3e495400b54e48eb1a98c68b1af2e5f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-using-hello-storsimple-data-manager-service-ui-private-preview"></a>Zarządzanie przy użyciu usługi Menedżer StorSimple danych hello interfejsu użytkownika (podglądzie prywatnym)

W tym artykule opisano sposób korzystania hello transformacji danych tooperform interfejsu użytkownika Menedżera danych StorSimple na danych znajdujących się na powitania urządzeń z serii StorSimple 8000. Witaj przekształcone dane może następnie być zużyte przez innych usług Azure, takich jak usługi Azure Media Services, Azure HDInsight uczenie maszynowe Azure i usługi Azure Search. 


## <a name="use-storsimple-data-transformation"></a>Za pomocą przekształcania danych StorSimple

Witaj StorSimple Data Manager jest hello zasobów, w którym można wdrożyć transformacji danych. Hello usługi Data Transformation umożliwia przenoszenie danych z programu StorSimple lokalnymi urządzeniami tooblobs w magazynie Azure. W związku z tym w przepływie pracy należy toospecify hello szczegóły dotyczące danych urządzenia i hello StorSimple odsetek, które mają konta magazynu toohello toomove.

### <a name="create-a-storsimple-data-manager-service"></a>Utwórz usługę Menedżer StorSimple danych

Wykonaj następujące kroki toocreate usługi Menedżer StorSimple danych hello.

1. toocreate usługi Menedżer StorSimple danych, przejdź zbyt[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)

2. Kliknij przycisk hello  **+**  ikony, jak i wyszukiwania StorSimple Data Manager. Kliknij opcję usługi Menedżer StorSimple danych, a następnie kliknij przycisk **Utwórz**.

3. Po włączeniu subskrypcji do tworzenia tej usługi zostanie wyświetlony powitania po bloku.

    ![Utwórz zasób menedżerów danych StorSimple](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. Wprowadź dane wejściowe hello i kliknij przycisk **Utwórz**. Witaj określona lokalizacja powinna być hello jedną, która przechowuje kont magazynu i usługi Menedżer StorSimple. Obecnie są obsługiwane tylko w regionach zachodnie stany USA i Europa Zachodnia. W związku z tym Twojej usługi Menedżer StorSimple, usługa Data Manager i hello skojarzone konto magazynu powinny być w poprzednim hello obsługiwane regiony. Trwa około minuty toocreate hello usługi.

### <a name="create-a-data-transformation-job-definition"></a>Tworzenie definicji zadania przekształcania danych

W ramach usługi Menedżer StorSimple danych należy toocreate definicji zadania przekształcania danych. Definicji zadania określa szczegóły hello dane, które planuje się do konta magazynu w hello formatu macierzystego. 

Wykonaj następujące kroki toocreate nowej definicji zadania przekształcania danych hello.

1.  Przejdź toohello utworzoną usługę. Kliknij przycisk **+ definicji zadania**.

    ![Kliknij pozycję + definicji zadania](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. Otwiera nowy blok definicji zadania Hello. Nadaj nazwę definicja zadania, a następnie kliknij przycisk **źródła**. W hello **Konfigurowanie źródła danych** bloku, określ szczegóły hello urządzenia StorSimple i hello dane.

    ![Tworzenie definicji zadania](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. Ponieważ jest to nowa usługa Data Manager, są skonfigurowane nie repozytoria danych. tooadd Menedżera StorSimple jako repozytorium danych, kliknij przycisk **Dodaj nowe** w hello danych repozytorium z listy rozwijanej, a następnie kliknij przycisk **Dodaj repozytorium danych**.

4. Wybierz **serii StorSimple 8000 Menedżera** jako repozytorium hello typu, a następnie wprowadź właściwości hello Twojej **Menedżer StorSimple**. Dla hello **identyfikator zasobu** pole, należy numer hello tooenter przed hello **:** w kluczu rejestracji hello Menedżera StorSimple.

    ![Utwórz źródło danych](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  Kliknij przycisk **OK** po zakończeniu. Spowoduje to zapisanie danych repozytorium, a ten Menedżer StorSimple mogą być ponownie używane w innych definicje zadań bez konieczności ponownego wprowadzania tych parametrów. Trwa kilka sekund po kliknięciu **OK** dla hello tooshow Menedżer StorSimple się w hello listy rozwijanej.

6.  W hello **Konfigurowanie źródła danych** bloku, wprowadź nazwę urządzenia hello i hello nazwa woluminu, zawierający dane zainteresowań.

7.  W hello **filtru** podsekcji, wprowadź katalog główny hello zawierającego dane odsetek (w tym polu powinny rozpoczynać się od `\`). Można również dodać wszystkie filtry plików.

8.  Usługa przekształcania danych Hello działa na dane hello spoczywa się toohello Azure za pomocą migawki. Podczas wykonywania tego zadania, można tootake kopii zapasowej każdorazowo to zadanie jest uruchamiane (toowork na najnowszych danych) lub toouse hello ostatniego istniejącej kopii zapasowej w chmurze hello (Jeśli pracujesz nad niektórych danych archiwalnych).

    ![Nowe szczegóły źródła danych](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. Następnie ustawień obiektu docelowego hello muszą toobe skonfigurowany. Istnieją 2 typy elementów docelowych obsługiwanych — kont usługi Azure Storage i Azure Media Services. Wybieranie kont magazynu tooput pliki do obiektów blob w tym kontem. Wybierz konta usługi media services pliki tooput do zasobów na tym koncie. Ponownie potrzebujemy tooadd repozytorium. Z listy rozwijanej hello, wybierz **Dodaj nowe** , a następnie **skonfigurować ustawienia**.

    ![Utwórz ujścia danych](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. W tym miejscu można wybrać typ hello ma tooadd i hello innych parametrów skojarzonych z repozytorium hello repozytorium. W obu przypadkach kolejki magazynu jest tworzony podczas hello zadanie jest uruchamiane. Jest ona wypełniana przy użyciu komunikatów dotyczących przekształconych obiektów blob, gdy będą gotowe. Nazwa Hello tej kolejki jest hello taka sama jak nazwa hello hello definicji zadania. W przypadku wybrania **Media Services** jako typ repozytorium hello, następnie możesz też wprowadzić poświadczenia konta magazynu gdy kolejka hello jest tworzona.

    ![Nowe szczegóły ujścia danych](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. Po dodaniu repozytorium danych hello (która zajmuje kilka sekund), można znaleźć w listy rozwijanej hello w hello repozytorium hello **nazwa konta docelowego**.  Wybierz element docelowy hello, które są potrzebne.

12. Kliknij przycisk **OK** definicji zadania hello toocreate. Definicja zadania jest teraz skonfigurowane. Można użyć tej definicji zadania wiele razy za pośrednictwem hello interfejsu użytkownika.

    ![Dodawanie nowej definicji zadania](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-hello-job-definition"></a>Uruchom hello definicji zadania

Jeśli potrzebne jest toomove dane z konta magazynu toohello StorSimple, który został określony w definicji zadania hello, konieczne będzie tooinvoke go. Podczas zmieniania parametry hello każdorazowego wywołania zadania hello charakteryzuje się pewną elastycznością. Witaj obejmuje następujące czynności:

1. Wybierz usługę Menedżer StorSimple danych i przejść za**monitorowanie**. Kliknij przycisk **Uruchom teraz**.

    ![Wyzwalacz definicji zadania](./media/storsimple-data-manager-ui/run-now.png)

2. Wybierz hello definicji zadania, które mają toorun. Kliknij przycisk **parametrów uruchomieniowych** toomodify wszystkie ustawienia, które mają toochange wykonywania tego zadania.

    ![Uruchom zadania, ustawienia](./media/storsimple-data-manager-ui/run-settings.png)

3. Kliknij przycisk **OK** , a następnie kliknij przycisk **Uruchom** toolaunch swoją pracę. toomonitor tego zadania, przejdź toohello **zadania** strony w Menedżera StorSimple danych.

    ![Lista zadań i stanu](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. W przypadku dodawania toomonitoring w hello **zadania** bloku można również wykrywać w kolejce magazynu hello, gdy wiadomość zostanie dodany za każdym razem, gdy plik zostanie przeniesiony z konta magazynu toohello StorSimple.


## <a name="next-steps"></a>Następne kroki

[Użyj zestawu SDK .NET toolaunch Menedżer StorSimple danych zadania](storsimple-data-manager-dotnet-jobs.md).
