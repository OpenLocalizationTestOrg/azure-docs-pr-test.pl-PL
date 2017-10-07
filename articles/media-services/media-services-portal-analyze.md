---
title: "aaaAnalyze przy użyciu nośnika hello portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym temacie omówiono sposób tooprocess multimediów procesory multimediów usługi analiza multimediów (MP) przy użyciu hello portalu Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a>Analiza multimediów przy użyciu hello portalu Azure
> [!NOTE]
> toocomplete tego samouczka jest potrzebne konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

## <a name="overview"></a>Omówienie
Azure Media Services Analytics to kolekcja składników mowy i obrazu (w skali przedsiębiorstwa, zgodności i zabezpieczeń globalne), które ułatwiają przydatnych wyników analiz tooderive organizacjom i przedsiębiorstwom podstawie posiadanych plików wideo. Aby uzyskać bardziej szczegółowe omówienie usługi Azure Media Services Analytics zobacz [to](media-services-analytics-overview.md) tematu. 

W tym temacie omówiono sposób tooprocess multimediów procesory multimediów usługi analiza multimediów (MP) przy użyciu hello portalu Azure. Pakiety MP analizy multimediów tworzą pliki MP4 lub pliki w formacie JSON. Plik MP4 utworzony przez procesor multimediów można pobrać progresywnie hello pliku. Plik JSON utworzony przez procesor multimediów można pobrać pliku hello z hello magazynu obiektów blob platformy Azure. 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a>Wybierz zasób, które mają tooanalyze
1. W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.
2. W hello **ustawienia** wybierz **zasoby**.  
   .
    ![Analizowanie plików wideo](./media/media-services-portal-analyze/media-services-portal-analyze001.png)
3. Wybierz hello zawartości, który chcesz hello tooanalyze i naciśnij klawisz **Analizuj** przycisku.
   
    ![Analizowanie plików wideo](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. W hello **procesu multimedialnej z analizy multimediów** okna, wybierz hello procesora. 
   
    rest Hello artykułu hello wyjaśnia, dlaczego i w jaki sposób toouse każdego procesora. 
5. Naciśnij klawisz **Utwórz** toohello uruchomić zadanie.

## <a name="azure-media-indexer"></a>Azure Media Indexer
Witaj **Azure Media indeksatora** procesor multimediów umożliwia toomake plików multimedialnych i zawartości można wyszukiwać, również generowanie zamkniętego śledzi podpisów. Tej sekcji szczegółowo opisano niektóre opcje, które można określić dla tego pakietu administracyjnego.

![Analizowanie plików wideo](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a>Język
Witaj w pliku multimedialnym hello toobe języka naturalnego. Na przykład w języku angielskim i hiszpańskim. 

### <a name="captions"></a>Podpisy
Można wybrać formatu podpisu, który zostanie wygenerowane z zawartości. Zadania indeksowania mogą generować pliki napisów w hello następujących formatów:  

* **SAMI**
* **TTML**
* **WebVTT**

Zamkniętych plikach podpis (DW) w tych formatach może być używane toomake audio i wideo pliki dostępny toopeople niepełnosprawne przesłuchanie.

### <a name="aib-file"></a>Plik AIB
Wybierz tę opcję, jeśli takie jak pliku Blob indeksu Audio hello toogenerate do użytku z będzie można hello niestandardowych IFilter serwera SQL. Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blogu.

### <a name="keywords"></a>Słowa kluczowe
Wybierz tę opcję, jeśli chcesz toogenerate pliku XML słów kluczowych. Ten plik zawiera słowa kluczowe wyodrębnione z zawartości mowy hello, częstotliwości i przesunięcia informacje.

### <a name="job-name"></a>Nazwa zadania
Przyjazna nazwa umożliwia identyfikowanie hello zadania. [To](media-services-portal-check-job-progress.md) artykule opisano, jak można monitorować postęp hello zadania. 

### <a name="output-file"></a>Plik wyjściowy
Przyjazna nazwa umożliwia zidentyfikowanie hello zawartości danych wyjściowych. 

## <a name="azure-media-hyperlapse"></a>Azure Media Hyperlapse
Azure Media Hyperlapse jest MP tworzącą smooth czas, jaki upłynął wideo z pierwszą osobą lub akcji aparatu zawartości.  Aby uzyskać więcej informacji, zobacz [ten](media-services-hyperlapse-content.md) temat. Tej sekcji szczegółowo opisano niektóre opcje, które można określić dla tego pakietu administracyjnego.

![Analizowanie plików wideo](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a>Szybkość
Określ szybkość hello z których toospeed się hello wejściowy plik wideo. dane wyjściowe Hello jest stabilnych i czas, jaki upłynął dobór hello wejściowy plik wideo.

### <a name="job-name"></a>Nazwa zadania
Przyjazna nazwa umożliwia identyfikowanie hello zadania. [To](media-services-portal-check-job-progress.md) artykule opisano, jak można monitorować postęp hello zadania. 

### <a name="output-file"></a>Plik wyjściowy
Przyjazna nazwa umożliwia zidentyfikowanie hello zawartości danych wyjściowych. 

## <a name="azure-media-face-detector"></a>Azure Media Face Detector
Witaj **Azure Media krój detektora** procesor multimediów (MP) pozwala toocount, przeniesień Śledź i nawet miernika odbiorców udziału i reakcji za pośrednictwem twarzy. Ta usługa zawiera dwie funkcje: 

* **Wykrywanie twarzy na obrazie**
  
    Wykrywanie twarzy na obrazie znajduje i śledzi człowieka kroje w pliku wideo. Wiele powierzchni mogą być wykrywane i następnie śledzenia przechodzą wokół, hello czas i lokalizację metadane zwrócony w pliku JSON. Podczas śledzenia podejmie toogive spójne toohello identyfikator sam stają przed podczas osoby hello jest przenoszenia na ekranie, nawet jeśli są zablokowane lub pozostaw krótko hello ramki.
  
  > [!NOTE]
  > Tej usługi nie przeprowadza rozpoznawanie twarzy. Osoba, która pozostawia ramki hello lub staje się blokować dla zbyt długo będzie mógł skorzystać z nowym Identyfikatorem gdy zwracają.
  > 
  > 
* **Wykrywanie emocji**
  
    Wykrywanie emocji jest opcjonalnym składnikiem hello procesor multimediów wykrywania twarzy na obrazie, które zwraca analizy na wiele atrybutów emocjonalne kroje hello wykryte, w tym szczęście, sadness, obawy i gniew. 

![Analizowanie plików wideo](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a>Tryb wykrywania
Jeden z następujących trybów hello można przez procesor hello:

* wykrywanie twarzy na obrazie
* na powierzchni emocji wykrywania
* wykrywanie emocji agregacji

### <a name="job-name"></a>Nazwa zadania
Przyjazna nazwa umożliwia identyfikowanie hello zadania. [To](media-services-portal-check-job-progress.md) artykule opisano, jak można monitorować postęp hello zadania. 

### <a name="output-file"></a>Plik wyjściowy
Przyjazna nazwa umożliwia zidentyfikowanie hello zawartości danych wyjściowych. 

## <a name="azure-media-motion-detector"></a>Azure Media Motion Detector
Witaj **czujnik ruchu Azure Media** nośnika procesora (MP) umożliwia tooefficiently można zidentyfikować sekcje zawierają informacje przydatne w wideo w innym przypadku długich i procesu. Wykrywanie ruchu może służyć na statycznych aparatu materiał tooidentify sekcje wideo hello gdzie występuje ruchu. Generuje plik JSON zawierający metadane z sygnatury czasowe i hello ograniczenia regionu, w którym wystąpiło zdarzenie hello.

Docelowe do źródła wideo zabezpieczeń, ta technologia jest możliwe toocategorize ruchu na odpowiednie zdarzenia i fałszywych alarmów, takie jak cieni i zmian oświetlenia. Dzięki temu można toogenerate alertów zabezpieczeń z aparatu fotograficznego źródła danych bez otrzymywania wiadomości-śmieci nieskończone zdarzenia nie ma znaczenia, będąc chwil stanie tooextract płynących z bardzo długi nadzoru wideo.

![Analizowanie plików wideo](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a>Azure Media Video Thumbnails
Tego procesora mogą pomóc tworzyć podsumowania długich filmów wideo, wybierając automatycznie interesujące wstawki z hello źródła wideo. Jest to przydatne, należy tooprovide szybki przegląd tooexpect które długie wideo. Aby uzyskać szczegółowe informacje i przykłady, zobacz [tooCreate miniatur wideo multimediów Azure Użyj podsumowań wideo](media-services-video-summarization.md)

![Analizowanie plików wideo](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a>Nazwa zadania
Przyjazna nazwa umożliwia identyfikowanie hello zadania. [To](media-services-portal-check-job-progress.md) artykule opisano, jak można monitorować postęp hello zadania. 

### <a name="output-file"></a>Plik wyjściowy
Przyjazna nazwa umożliwia zidentyfikowanie hello zawartości danych wyjściowych. 

## <a name="next-steps"></a>Następne kroki
Ścieżki szkoleniowe dotyczące usługi Media widoku.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

