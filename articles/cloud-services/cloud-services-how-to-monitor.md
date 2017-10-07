---
title: "toomonitor aaaHow usługi w chmurze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor usługi w chmurze przy użyciu hello klasycznego portalu Azure."
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: 5c48d2fb-b8ea-420f-80df-7aebe2b66b1b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2015
ms.author: adegeo
ms.openlocfilehash: ee98c56e0b98b85d75a5c1d796800069c4f06d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-cloud-services"></a>W jaki sposób tooMonitor usług w chmurze
[!INCLUDE [disclaimer](../../includes/disclaimer.md)]

Można monitorować `key` metryki wydajności dla usług w chmurze w hello klasycznego portalu Azure. Można ustawić hello poziom monitorowania toominimal i pełne dla każdej usługi roli i dostosowanie hello Wyświetla monitorowania. Pełne monitorowania dane są przechowywane na koncie magazynu są dostępne spoza portalu hello. 

Wyświetla monitorowania w hello klasycznego portalu Azure są konfigurowane w dużej. Można wybrać metryki hello ma toomonitor liście metryki hello na powitania **Monitor** strony, na które można wybrać tooplot metryk, które na wykresach metryki na powitania **Monitor** strony i hello pulpitu nawigacyjnego. 

## <a name="concepts"></a>Pojęcia
Domyślnie minimalnym monitorowania jest podawany nową usługę w chmurze za pomocą liczników wydajności zebranych z systemu operacyjnego hosta hello w wystąpieniach ról hello (maszyn wirtualnych). metryki minimalnego Hello są ograniczone tooCPU procent, dane w, danych wychodzących, przepływność odczytu dysku i przepływność zapisu dysku. Konfigurując pełnego monitorowania może otrzymywać dodatkowe metryki na podstawie danych wydajności w maszynach wirtualnych hello (wystąpienia roli). metryki pełne Hello Włącz analizę bliżej problemów występujących podczas działania aplikacji.

Domyślnie dane licznika wydajności z wystąpień roli jest próbkowany i przekazywane z hello wystąpienia roli co 3 minut. Po włączeniu pełnego monitorowania, dane licznika wydajności raw hello są agregowane dla każdego wystąpienia roli, a w wystąpieniach ról dla każdej roli częstotliwością wynoszącą 5 minut, godzinę i 12 godzin. Witaj zagregowane dane są przeczyszczane po 10 dni.

Po włączeniu pełnego monitorowania hello zagregowane dane monitorowania są przechowywane w tabelach na koncie magazynu. tooenable pełne monitorowania dla roli, należy skonfigurować parametry połączenia diagnostyki, które łączy toohello konta magazynu. Można użyć różnych kont magazynu dla różnych ról.

Włączenie pełnego monitorowania zwiększa koszty magazynowania powiązanych toodata magazynowania, transfer danych i transakcje magazynu. Minimalny monitorowania nie wymaga konta magazynu. Hello danych dla metryki hello, które są dostępne na minimalnym poziomie monitorowania hello nie są przechowywane na koncie magazynu, nawet w przypadku ustawienia monitorowania poziomu tooverbose hello.

## <a name="how-to-configure-monitoring-for-cloud-services"></a>Porady: Konfigurowanie monitorowania dla usług w chmurze
Użyj hello następujące procedury tooconfigure pełne lub minimalnym monitorowanie hello klasycznego portalu Azure. 

### <a name="before-you-begin"></a>Przed rozpoczęciem
* Utwórz *klasycznego* hello toostore konta magazynu danych monitorowania. Można użyć różnych kont magazynu dla różnych ról. Aby uzyskać więcej informacji, zobacz [jak toocreate konta magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* Włącz diagnostyki Azure dla role usługi w chmurze. Zobacz [Konfigurowanie diagnostyki dla usługi w chmurze](cloud-services-dotnet-diagnostics.md).

Upewnij się, że parametry połączenia diagnostyki hello są dostępne w konfiguracji roli hello. Nie można włączyć pełne monitorowania do czasu włączenia diagnostyki Azure i obejmują parametry połączenia diagnostyki w konfiguracji roli hello.   

> [!NOTE]
> Projektach przeznaczonych dla 2.5 zestawu SDK platformy Azure nie zawiera automatycznie parametry połączenia diagnostyki hello hello szablonu projektu. Aby projekty te należy toomanually Dodaj konfiguracji roli toohello ciąg hello diagnostyki połączenia.
> 
> 

**toomanually Dodaj konfigurację tooRole ciąg połączenia diagnostyki**

1. Otwórz hello projektu usługi w chmurze w programie Visual Studio
2. Kliknij dwukrotnie hello **roli** tooopen hello projektanta rolę i wybierz hello **ustawienia** kartę
3. Wyszukaj ustawienie o nazwie **Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**. 
4. Jeśli to ustawienie nie jest obecny, kliknij na powitania **Dodaj ustawienie** tooadd przycisk go toohello konfiguracji i zmień typ hello nowe ustawienie zbyt hello**ConnectionString**
5. Ustawianie wartości hello hello ciąg połączenia, klikając hello **...**  przycisku. Spowoduje to otwarcie okna dialogowego, dzięki czemu tooselect konta magazynu.
   
    ![Ustawienia programu Visual Studio](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioDiagnosticsConnectionString.png)

### <a name="toochange-hello-monitoring-level-tooverbose-or-minimal"></a>Witaj toochange monitorowania poziomu tooverbose lub minimalnego
1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com/), otwórz hello **Konfiguruj** strony dla wdrożenia usługi w chmurze hello.
2. W **poziom**, kliknij przycisk **pełne** lub **minimalnego**. 
3. Kliknij pozycję **Zapisz**.

Po włączeniu pełnego monitorowania powinny zacząć się wyświetlać hello monitorowania danych w hello klasycznego portalu Azure w ciągu godziny hello.

dane licznika wydajności raw Hello i zagregowane dane monitorowania są przechowywane na koncie magazynu hello w tabelach kwalifikowana przez identyfikator wdrożenia hello hello ról. 

## <a name="how-to-receive-alerts-for-cloud-service-metrics"></a>Porady: otrzymywać alerty dotyczące metryk usługi w chmurze
Możesz otrzymywać alerty oparte na monitorowanie metryki usługi w chmurze. Na powitania **usług zarządzania** strony hello klasycznego portalu Azure, można utworzyć tootrigger reguły alertu gdy zostanie wybrana Metryka hello osiągnie wartości, który określisz. Możesz również toohave wiadomości e-mail wysyłane po wyzwoleniu alertu hello. Aby uzyskać więcej informacji, zobacz [porady: odbieranie powiadomień o alertach i Zarządzaj zasadami alertów w usłudze Azure](http://go.microsoft.com/fwlink/?LinkId=309356).

## <a name="how-to-add-metrics-toohello-metrics-table"></a>Porady: Dodawanie tabeli metryki toohello metryk
1. W hello [klasycznego portalu Azure](http://manage.windowsazure.com/), otwórz hello **Monitor** strony hello usłudze w chmurze.
   
    Domyślnie hello metryki tabeli przedstawia podzbiór hello dostępne metryki. Witaj ilustracji przedstawiono hello domyślne pełne metryki dla usługi w chmurze, co jest ograniczona toohello dane licznika wydajności pamięć\dostępna pamięć (MB), dane zagregowane na poziomie roli hello. Użyj **dodać metryki** tooselect dodatkowe agregacji i toomonitor metryki poziomu roli w hello klasycznego portalu Azure.
   
    ![Pełny ekran](./media/cloud-services-how-to-monitor/CloudServices_DefaultVerboseDisplay.png)
2. Tabela tooadd metryki toohello metryki:
   
   1. Kliknij przycisk **dodać metryki** tooopen **wybrać metryki**, przedstawiono poniżej.
      
       pierwszy Metryka dostępne Hello jest rozwinięty tooshow opcje, które są dostępne. Dla każdego metryki opcję top hello Wyświetla zagregowane dane monitorowania dla wszystkich ról. Ponadto można wybrać poszczególnych ról toodisplay danych.
      
       ![Dodaj metryk](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics.png)
   2. tooselect toodisplay metryk
      
      * Kliknij przycisk hello Strzałka w dół przez hello metryki tooexpand hello opcje monitorowania.
      * Hello zaznacz pole wyboru dla każdej monitorowania opcję toodisplay.
        
        Można wyświetlić się metryki too50 hello metryki tabeli.
        
        > [!TIP]
        > W ramach monitorowania pełne hello metryki lista może zawierać dziesiątki metryki. toodisplay paska przewijania, umieść kursor nad hello prawej stronie powitania — okno dialogowe. Lista hello toofilter, kliknij ikonę wyszukiwania hello i wprowadź tekst w polu wyszukiwania hello, jak pokazano poniżej.
        > 
        > 
        
        ![Dodaj wyszukiwanie metryk](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics_Search.png)
3. Po wybraniu metryki, kliknij przycisk OK (znacznikiem wyboru).
   
    Hello wybranego metryki są dodawane toohello metryki tabeli, jak pokazano poniżej.
   
    ![Monitor metryk](./media/cloud-services-how-to-monitor/CloudServices_Monitor_UpdatedMetrics.png)
4. toodelete Metryka z tabeli metryki hello, kliknij przycisk tooselect metryki hello, a następnie kliknij przycisk **usunąć Metryka**. (Wyświetlane są tylko **usunąć Metryka** Jeśli masz wybraną metryką.)

### <a name="tooadd-custom-metrics-toohello-metrics-table"></a>tooadd metryki niestandardowe toohello metryki tabeli
Witaj **pełne** monitorowania poziomu zawiera listę domyślne metryki, które można monitorować na powitania portalu. Ponadto toothese można monitorować ani metryki niestandardowe zdefiniowane przez aplikację za pośrednictwem portalu hello liczników wydajności.

Witaj następujących krokach przyjęto założenie, że włączono **pełne** poziom monitorowania i skonfigurowano w Twojej aplikacji toocollect i transfer niestandardowe liczniki wydajności. 

toodisplay hello niestandardowe liczniki wydajności w hello portalu wymagana konfiguracja hello tooupdate w wad formantu kontenera:

1. Otwórz hello wad formantu kontenera obiektów blob na koncie magazynu diagnostyki. Możesz użyć programu Visual Studio lub innych toodo Eksploratora magazynu to.
   
    ![W Eksploratorze serwera programu Visual Studio](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioBlobExplorer.png)
2. Przejdź do ścieżki obiektu blob hello przy użyciu wzorca hello **DeploymentId/RoleName/RoleInstance** toofind hello konfiguracji dla swojego wystąpienia roli. 
   
    ![Eksplorator usługi Storage programu Visual Studio](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioStorage.png)
3. Pobierz plik konfiguracji hello wystąpienia roli i zaktualizować je tooinclude wszelkie niestandardowe liczniki wydajności. Na przykład toomonitor *Bajty zapisu dysku/s* dla hello *dysku C* Dodaj hello w obszarze **PerformanceCounters\Subscriptions** węzła
   
    ```xml
    <PerformanceCounterConfiguration>
    <CounterSpecifier>\LogicalDisk(C:)\Disk Write Bytes/sec</CounterSpecifier>
    <SampleRateInSeconds>180</SampleRateInSeconds>
    </PerformanceCounterConfiguration>
    ```
4. Zapisz zmiany hello oraz przekazywania hello konfiguracji pliku wstecz toohello zastępowanie tej samej lokalizacji hello istniejący plik w obiekcie blob hello.
5. Przełącz tryb tooVerbose w hello Azure Konfiguracja portalu klasycznego. Jeśli jesteś w trybie informacji pełnej już masz tootoggle tooverbose toominimal i z powrotem.
6. Licznik wydajności niestandardowych Hello będą teraz dostępne w hello **dodać metryki** okno dialogowe. 

## <a name="how-to-customize-hello-metrics-chart"></a>Porady: dostosowywanie hello metryki wykresu
1. W tabeli metryki hello wybierz się too6 tooplot metryki na wykresie metryki hello. tooselect metryki, kliknij pole wyboru hello jego lewej strony. tooremove Metryka z wykresu metryki hello, wyczyść jej pole wyboru w hello metryki tabeli.
   
    Po wybraniu metryki tabeli metryki hello metryki hello są dodawane toohello metryki wykresu. Na ekranie wąskie **n więcej** listy rozwijanej zawiera nagłówki metryk, które nie pasują do wyświetlania hello.
2. tooswitch między wyświetlaniem względne wartości (końcowa wartość tylko dla każdego metryki) i wartości bezwzględne (oś Y wyświetlana), wybierz względną lub bezwzględną u góry hello hello wykresu.
   
    ![Względna lub bezwzględna](./media/cloud-services-how-to-monitor/CloudServices_Monitor_RelativeAbsolute.png)
3. toochange hello czasu zakresu hello metryki wykres Wyświetla, wybierz godzinę, 24 godzin lub dni 7 u góry hello hello wykresu.
   
    ![Monitor okres wyświetlania](./media/cloud-services-how-to-monitor/CloudServices_Monitor_DisplayPeriod.png)
   
    Na wykresie metryki pulpitu nawigacyjnego hello metoda hello kreślenia metryki różni się. Standardowy zestaw metryki jest dostępna, i metryki zostały dodane lub usunięte przez wybranie hello metryki nagłówka.

### <a name="toocustomize-hello-metrics-chart-on-hello-dashboard"></a>Wykres metryki hello toocustomize na powitania pulpitu nawigacyjnego
1. Otwórz pulpit nawigacyjny hello hello usłudze w chmurze.
2. Dodaj lub usuń metryki z wykresu hello:
   
   * tooplot nowe pole wyboru hello metryki, wybierz pozycję metryki hello w nagłówkach wykresu hello. Na ekranie wąskie, kliknij przycisk hello strzałkę przez  ***n* ? metryki** tooplot obszar nagłówka metryki hello wykresu nie można wyświetlić.
   * toodelete metrykę, które są kreślone na wykresie hello hello wyczyść pole wyboru obok jej nagłówek.
   
3. Przełączanie między **względną** i **bezwzględne** Wyświetla.
4. Wybierz godzinę, 24 godzin lub 7 dni toodisplay danych.

## <a name="how-to-access-verbose-monitoring-data-outside-hello-azure-classic-portal"></a>Porady: dostęp do pełnych danych monitorowania poza hello klasycznego portalu Azure
Pełne dane monitorowania są przechowywane w tabelach na kontach magazynu hello określonych dla każdej roli. Dla każdego wdrożenia usługi chmury sześciu tabele są tworzone dla roli hello. Dwie tabele są tworzone dla każdej (5 minut, godzinę i 12 godzin). Jeden z tych tabel przechowuje agregacji na poziomie roli; Witaj innych agregacji magazynów tabeli dla wystąpień roli. 

nazwy tabeli Hello mają hello następującego formatu:

```
WAD*deploymentID*PT*aggregation_interval*[R|RI]Table
```

Gdzie:

* *deploymentID* jest hello przypisany do wdrożenia usługi chmury toohello identyfikator GUID
* *aggregation_interval* = 5 M, 1 H lub 12 H
* agregacji na poziomie roli = R
* agregacji dla wystąpień roli = RI

Na przykład hello następujących tabel będzie przechowywać pełne dane monitorowania zagregowane na 1 godzinę:

```
WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRTable (hourly aggregations for hello role)

WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRITable (hourly aggregations for role instances)
```
