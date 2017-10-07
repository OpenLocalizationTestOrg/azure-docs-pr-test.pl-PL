---
title: "aaaDedicated pojemności Machine Learning partii wykonywania usługi zadań | Dokumentacja firmy Microsoft"
description: "Omówienie usług partii zadań Azure Machine Learning zadań."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a>Azure usługa partia zadań dla zadania uczenia maszynowego

Machine Learning puli partii przetwarzania przewiduje hello usługi wykonywania wsadowego Azure maszyny Learning skalowalnego zarządzany przez klienta. Klasycznym przetwarzania wsadowego dla uczenia maszynowego odbywa się w środowisku wielodostępnym limity które hello liczbę współbieżnych zadań mogą przesyłać i zadania są umieszczane w kolejce na podstawie pierwszego w pierwszym poza. Ta niedokładność oznacza, że nie można dokładnie przewidzieć uruchomienia zadania.

Przetwarzanie wsadowe puli umożliwia pule toocreate, na których można przesłać zadania wsadowe. Możesz kontrolować rozmiar hello hello puli i przesłaniu zadania hello puli toowhich. Zadania usługi BES działa w własne przetwarzania, zapewniając miejsca przetwarzania przewidywalną wydajność i pule zasobów toocreate możliwości hello, które odpowiadają obciążenie toohello przesyłania.

## <a name="how-toouse-batch-pool-processing"></a>Jak toouse przetwarzania wsadowego puli

Przetwarzanie wsadowe puli konfiguracji nie jest obecnie dostępna za pośrednictwem hello portalu Azure. toouse puli partii przetwarzania, musi:

-   Wywołanie CSS toocreate konto puli partii i uzyskiwanie adresu URL usługi puli i klucz autoryzacji
-   Tworzenie nowego Menedżera zasobów na podstawie usługi sieci web i plan rozliczeniowy

toocreate Twojego konta, wywołaj obsługi klienta firmy Microsoft i pomocy technicznej (CSS) i podaj identyfikator subskrypcji. CSS będzie działać z możesz toodetermine hello odpowiednie pojemności dla danego scenariusza. CSS skonfiguruje konto z hello maksymalna liczba pul można tworzyć i hello maksymalną liczbę maszyn wirtualnych (VM), które można umieścić w każdej puli. Po skonfigurowaniu konta podano adres URL usługi puli i klucza autoryzacji.

Po utworzeniu konta, możesz użyć hello puli adres URL usługi i autoryzacji klucza tooperform puli zarządzania operacji w Twojej puli partii.

![Architektura usługi puli partii.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

Pule można utworzyć przez wywołanie metody operacji tworzenia puli hello na adres URL usługi puli hello tego tooyou CSS, pod warunkiem. Podczas tworzenia puli określić hello liczbę maszyn wirtualnych i adres URL hello swagger.json hello nowego Menedżera zasobów na podstawie usługi sieci web uczenie maszynowe. Ta usługa sieci web podano tooestablish hello rozliczeń skojarzenia. Hello usługi puli partii używa hello swagger.json tooassociate hello puli z plan rozliczeniowy. Można uruchamiać żadnych BES usługi sieci web, zarówno nowego Menedżera zasobów na podstawie i klasyczne, wybierz w puli hello.

Można użyć nowego Menedżera zasobów na podstawie usługi sieci web, ale należy pamiętać, że hello rozliczeń dla zadań hello są powiązane z hello plan rozliczeniowy skojarzone z tą usługą. Możesz toocreate usługi sieci web i rozliczeń nowy plan specjalnie z myślą o uruchomionych puli partii zadań.

Aby uzyskać więcej informacji na temat tworzenia usług sieci web, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

Po utworzeniu puli przesłać hello BES zadania za pomocą polecenia hello adresu URL żądania wsadowe usługi sieci web hello. Możesz wybrać toosubmit on tooa puli lub tooclassic przetwarzania wsadowego. toosubmit przetwarzania zadania tooBatch puli, Dodaj powitania po treści żądania przesłania zadania toohello parametru:

"AzureBatchPoolId": "&lt;puli identyfikator&gt;"

Jeśli nie zostanie dodany parametr hello, hello zadanie jest uruchamiane w środowisku procesu wsadowego klasycznego hello. Jeśli pula hello ma dostępne zasoby, hello zadania uruchamiania natychmiast. Hello pula nie ma wolnego zasobów, zadanie jest w kolejce do momentu zasób jest dostępny.

Jeśli okaże się regularnie osiągnąć pojemności hello z pulami, czy należy zwiększenia wydajności, można wywołać CSS i pracować z reprezentatywny tooincrease przydziałami.

Przykładowe żądanie:

https://ussouthcentral.Services.azureml.NET/Subscriptions/80c77c7674ba4c8c82294c3b2957990c/Services/9fe659022c9747e3b9b7b923c3830623/Jobs?API-Version=2.0

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a>Uwagi dotyczące korzystania z przetwarzania wsadowego puli

Przetwarzanie wsadowe puli jest zawsze włączone usługą płatną i wymaga który tooassociate go za pomocą Menedżera zasobów na podstawie plan rozliczeniowy. Rozliczenie jest przeprowadzane tylko hello liczbę godzin obliczeń puli hello jest uruchomiony; niezależnie od hello liczba zadania są uruchamiane w tej puli czasu. Po utworzeniu puli rozliczenie jest hello godziny obliczeń dla poszczególnych maszyn wirtualnych w puli hello aż do usunięcia puli hello, nawet jeśli w puli hello są uruchomione żadne zadania wsadowego. Rozliczeń dla maszyn wirtualnych hello rozpoczyna się po zakończeniu ich inicjowania obsługi administracyjnej i zatrzymywana, gdy zostały usunięte. Można użyć dowolnego z planami hello na powitania [Machine Learning — cennik strony](https://azure.microsoft.com/pricing/details/machine-learning/).

Przykład rozliczeń:

Jeśli z maszyn wirtualnych 2. Utwórz pulę partii i usuń go po 24 godzinach planu rozliczeniowego obciąża 48 godzin obliczeń; niezależnie od tego, ile zadania zostały uruchomione w tym okresie.

Tworzenie puli partii z 4 maszynami wirtualnymi, usuń go po 12 godzinach planu rozliczeniowego jest również zaksięgowana 48 godzin obliczeń.

Firma Microsoft zaleca sondowania toodetermine stan zadania hello, po ukończeniu zadania. Po zakończeniu operacji uruchamiania wszystkich zadań ma wywoływać hello numer hello tooset operacji zmiany rozmiaru puli maszyn wirtualnych w hello toozero puli. Gdy krótka puli zasobów i należy toocreate nowej puli, na przykład toobill z innego planu rozliczeniowego, można usunąć puli hello zamiast tego po wszystkich zadań zakończeniu pracy.


| **Korzystanie z puli partii podczas przetwarzania**    | **Użyj klasycznego partii podczas przetwarzania**  |
|---|---|
|Należy toorun dużej liczby zadań<br>Lub<br/>Należy tooknow, że Twoje zadania będą uruchamiane natychmiast<br/>Lub<br/>Należy gwarantowanej przepustowości. Na przykład konieczne toorun liczba zadań w określonym przedziale czasu, a chcesz tooscale limit Twojego toomeet zasoby obliczeniowe potrzeb.    | Użytkownicy korzystający z kilku zadań<br/>I<br/> Nie trzeba natychmiast hello toorun zadania |
