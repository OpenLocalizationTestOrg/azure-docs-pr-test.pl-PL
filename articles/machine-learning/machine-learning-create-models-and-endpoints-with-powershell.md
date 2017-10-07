---
title: "aaaCreate wielu modeli z doświadczenia | Dokumentacja firmy Microsoft"
description: "Użyj programu PowerShell toocreate wielu modeli uczenia maszynowego i sieci web punktów końcowych usługi z hello samego algorytmu, ale szkolenia różnych zestawów danych."
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a>Tworzenie wielu modeli usługi Machine Learning i punktów końcowych usługi sieci Web na podstawie jednego eksperymentu przy użyciu programu PowerShell
W tym miejscu jest to powszechny problem learning maszyny: mają wiele modeli, które mają hello toocreate tego samego przepływu pracy szkolenia i użyj hello samego algorytmu, ale ma szkolenia różnych zestawów danych, jako dane wejściowe. W tym artykule opisano sposób toodo to na dużą skalę w usłudze Azure Machine Learning Studio za pomocą tylko jednego eksperymentu.

Załóżmy na przykład, że właścicielem firmy franchisingowe roweru globalnego dzierżawy. Ma toobuild zażąda wynajem hello toopredict modelu regresji na podstawie historycznych danych. Masz 1000 lokalizacje dzierżawa między Witaj świecie i zostały zebrane zestawu danych dla każdej lokalizacji, która zawiera ważne funkcje, takie jak dzień, godzina pogodą i ruchu, który jest tooeach określonej lokalizacji.

Można uczenia modelu raz we wszystkich lokalizacjach za pomocą scalonych wersji wszystkich hello zestawów danych. Jednak ponieważ każdy z lokalizacji ma unikatowy środowiska, lepszym rozwiązaniem może być tootrain modelu regresji oddzielnie dla każdej lokalizacji za pomocą hello zestawu danych. W ten sposób każdy uczonego modelu może potrwać do konta hello magazynu różne rozmiary, woluminu, geography, wypełniania, ruch roweru przyjaznego środowiska, *itp.*.

Może to być hello najlepszym rozwiązaniem, ale nie chcesz, aby z każdą z nich reprezentujący unikatową lokalizację toocreate 1000 szkolenia eksperymentów w usłudze Azure Machine Learning. Oprócz jest utrudnione zadań, należy również wydaje się bardzo mało wydajne, ponieważ wszystkie hello tego samego składników z wyjątkiem hello szkolenia dataset musi każdego eksperymentu.

Na szczęście, firma Microsoft może to zrobić przy użyciu hello [ponownego trenowania interfejsu API uczenia maszynowego Azure](machine-learning-retrain-models-programmatically.md) i automatyzowanie zadań hello z [programu PowerShell usługi Azure Machine Learning](machine-learning-powershell-module.md).

> [!NOTE]
> toomake naszej próbki szybsze, firma Microsoft będzie zmniejszyć hello liczba lokalizacji z too10 1000. Ale hello tego samego zasadami i procedurami zastosować too1, lokalizacje 000. Hello jedyna różnica polega na tym, że jeśli tootrain z 1000 zestawów danych prawdopodobnie potrzebna będzie toothink uruchomionych hello następujące skrypty programu PowerShell równolegle. Jak toodo, która wykracza poza zakres tego artykułu, ale hello można znaleźć przykłady PowerShell wielowątkowości na powitania Internet.  
> 
> 

## <a name="set-up-hello-training-experiment"></a>Konfigurowanie eksperyment uczenia hello
Zamierzamy toouse przykład [eksperyment uczenia](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) który mamy już utworzone w hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Otwórz tego eksperymentu w Twojej [Azure Machine Learning Studio](https://studio.azureml.net) obszaru roboczego.

> [!NOTE]
> W kolejności toofollow wraz z tego przykładu możesz toouse standardowe obszaru roboczego, a nie wolnego obszaru roboczego. Możemy utworzyć jeden punkt końcowy dla każdego klienta — dla wszystkich punktów końcowych 10 - i standardowe obszaru roboczego będzie wymagają od wolnego obszaru roboczego jest ograniczona too3 punktów końcowych. Jeśli masz tylko obszar roboczy wolne, po prostu Zmodyfikuj skrypty hello poniżej tooallow tylko 3 lokalizacji.
> 
> 

używa eksperymentu Hello **i zaimportuj dane** modułu tooimport hello szkolenia w zestawie danych *customer001.csv* z kontem magazynu platformy Azure. Załóżmy, że firma Microsoft zbierane szkolenia zestawów danych z wszystkich lokalizacji wynajem roweru i zapisał je w hello sam lokalizacji magazynu obiektów blob z nazwami plików od *rentalloc001.csv* za*rentalloc10.csv* .

![Obraz](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

Należy pamiętać, że **wyjście usługi sieci Web** moduł został dodany toohello **Train Model** modułu.
Po wdrożeniu tego eksperymentu jako usługę sieci web punktu końcowego hello skojarzone z tym produktem wyjściowym zwróci hello uczonego modelu w formacie hello pliku .ilearner.

Należy również zauważyć, że skonfigurowanie parametr usługi sieci web dla adresu URL hello tego hello **i zaimportuj dane** korzysta z modułu. Dzięki temu nam toouse hello parametru toospecify szkolenia poszczególnych zestawów danych tootrain hello modelu dla każdej lokalizacji.
Istnieją inne sposoby firma Microsoft może mieć zostało to zrobione, takich jak za pomocą zapytania SQL z danych tooget parametr usługi sieci web z bazy danych SQL Azure lub po prostu **wprowadzania usługi sieci Web** usługi sieci web toopass modułu w toohello zestawu danych.

![Obraz](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

Teraz umożliwia uruchamianie tego eksperymentu uczenia przy użyciu wartości domyślnej hello *rental001.csv* jako hello zestawu danych szkoleniowych. Podczas przeglądania danych wyjściowych hello hello **Evaluate** modułu (kliknij hello wyjściowy i wybierz **wizualizacja**), zostanie wyświetlony, uzyskujemy zadowalający wydajność *AUC* = 0,91. W tym momencie mamy toodeploy gotowe usługi sieci web poza tym eksperyment uczenia.

## <a name="deploy-hello-training-and-scoring-web-services"></a>Wdrażanie hello szkolenia i oceniania usług sieci web
toodeploy hello szkolenia usługi sieci web, kliknij przycisk hello **ustawić usługę sieci Web** poniżej hello roboczego eksperymentu i wybrać **wdrażanie usługi sieci Web**. Wywołania tej usługi sieci web "" roweru wynajem szkolenia".

Teraz potrzebujemy toodeploy hello oceniania usługi sieci web.
toodo, możemy kliknąć **ustawić usługę sieci Web** poniżej hello obszar roboczy i wybierz **predykcyjnej usługi sieci Web**. Spowoduje to utworzenie oceniania eksperymentu.
Potrzebujemy toomake kilka toomake niewielkich dostosowań pracy jako usługi sieci web, takie jak usunięcie kolumny etykiety hello "cnt" z hello dane wejściowe i ograniczanie identyfikator wystąpienia hello hello dane wyjściowe tooonly i hello odpowiadającego przewidzieć wartość.

toosave, który działa, możesz po prostu otworzyć hello [eksperyment predykcyjny](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) w hello galerii, który jest już przygotowane.

Usługa sieci web hello toodeploy uruchomić eksperyment predykcyjny hello, następnie kliknij przycisk hello **wdrażanie usługi sieci Web** znajdujący się poniżej hello kanwy. Nazwa hello oceniania usługi sieci web "Roweru wynajem oceniania" ".

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a>Tworzenie punktów końcowych usługi sieci web identyczne 10 przy użyciu programu PowerShell
Ta usługa sieci web jest dostarczany z domyślnego punktu końcowego. Ale nie jesteśmy jako zainteresowana hello domyślnego punktu końcowego, ponieważ nie można zaktualizować. Co należy toodo jest toocreate 10 dodatkowych punktów końcowych, po jednej dla każdej lokalizacji. Firma Microsoft to zrobić przy użyciu programu PowerShell.

Po pierwsze skonfigurowanie naszego środowiska PowerShell:

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

Następnie uruchom następujące polecenia programu PowerShell hello:

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

Teraz utworzona 10 punktów końcowych i wszystkie zawierają hello ćwiczenie uczonego modelu w tym samym *customer001.csv*. Można je wyświetlić w portalu zarządzania Azure hello.

![Obraz](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a>Zaktualizuj hello punkty końcowe toouse oddzielne szkolenia danych przy użyciu programu PowerShell
Witaj następnym krokiem jest punkty końcowe hello tooupdate z modelami jednoznacznie ćwiczenie poszczególnych danych każdego klienta. Jednak najpierw musimy tooproduce tych modeli z hello **roweru wynajem szkolenia** usługi sieci web. Przejdź wstecz toohello **roweru wynajem szkolenia** usługi sieci web. Potrzebujemy toocall punktu końcowego usługi BES 10 razy z 10 szkolenia różnych zestawów danych w kolejności tooproduce 10 różne modele. Użyjemy hello **InovkeAmlWebServiceBESEndpoint** toodo polecenia cmdlet programu PowerShell to.

Należy również tooprovide poświadczenia dla konta magazynu obiektów blob do `$configContent`, to znaczy, w polach hello `AccountName`, `AccountKey` i `RelativeLocation`. Witaj `AccountName` może być jedną z nazwy konta, jak pokazano w hello **klasycznego portalu zarządzania Azure** (*magazynu* kartę). Po kliknięciu na koncie magazynu, jego `AccountKey` można znaleźć, naciskając klawisz hello **Zarządzaj kluczami dostępu** u dołu hello i kopiowanie hello *podstawowy klucz dostępu*. Witaj `RelativeLocation` jest hello ścieżki względnej tooyour magazynu przechowywania nowego modelu. Na przykład ścieżka hello `hai/retrain/bike_rental/` w skrypcie hello poniżej punktów tooa kontener o nazwie `hai`, i `/retrain/bike_rental/` znajdują się podfoldery. Obecnie nie można utworzyć podfoldery za pośrednictwem portalu hello interfejsu użytkownika, ale istnieją [kilka eksploratory usługi Storage Azure](../storage/common/storage-explorers.md) umożliwiającą toodo tak. Zalecane jest utworzenie nowego kontenera w hello toostore Twojego magazynu nowe modele przeszkolone (.ilearner pliki) w następujący sposób: na stronie magazynu, kliknij hello **Dodaj** znajdujący się u dołu hello i nadaj mu nazwę `retrain`. Podsumowując, skrypt toohello niezbędne zmiany hello poniżej odnoszą się zbyt`AccountName`, `AccountKey` i `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> punkt końcowy usługi BES Hello jest hello obsługiwany tylko tryb dla tej operacji. Rekordy zasobów nie może służyć do tworzenia modeli przeszkolone.
> 
> 

Jak pokazano powyżej, zamiast tworzenia 10 różnych BES zadania konfiguracji json plików, firma Microsoft dynamicznie zamiast tego utwórz Ciąg konfiguracyjny hello i umieść go toohello *jobConfigString* parametru hello  **InvokeAmlWebServceBESEndpoint** polecenia cmdlet, ponieważ nie istnieje naprawdę tookeep nie potrzeby kopiowania na dysku.

Jeśli wszystko odbędzie się poprawnie, po chwili powinno być widoczne 10 plików .ilearner, z *model001.ilearner* za*model010.ilearner*, na Twoim koncie magazynu Azure. Teraz jest gotowy tooupdate naszych 10 oceniania sieci web punkty końcowe usługi przy użyciu tych modeli przy użyciu hello **AmlWebServiceEndpoint poprawki** polecenia cmdlet programu PowerShell. Ponownie należy pamiętać, że firma Microsoft tylko poprawki z systemem innym niż domyślne punkty końcowe hello, utworzonego programowo wcześniej.

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

To powinno być ono uruchomione stosunkowo szybko. Po zakończeniu wykonywania hello, firma Microsoft będzie pomyślnie utworzono 10 punktów końcowych usługi sieci web predykcyjnych, każda z nich zawiera uczonego modelu jednoznacznie ćwiczenie hello zestawu danych tooa określonych wynajem lokalizacji, z eksperyment pojedynczego szkolenia. tooverify, możesz spróbować wywoływania tych punktów końcowych przy użyciu hello **InvokeAmlWebServiceRRSEndpoint** polecenia cmdlet, zapewnienie im z hello same dane wejściowe i wyniki prognozowania różnych toosee należy oczekiwać od modele hello są uczone z szkolenia różnych zestawów.

## <a name="full-powershell-script"></a>Pełna skrypt programu PowerShell
Oto lista hello hello pełny kod źródłowy:

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
