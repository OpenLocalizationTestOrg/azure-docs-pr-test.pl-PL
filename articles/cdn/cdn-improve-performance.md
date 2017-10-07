---
title: "aaaImprove wydajności przez kompresowanie plików w usłudze Azure CDN | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak transfer plików tooimprove szybkości i zwiększa wydajność obciążenia strony przez kompresowanie plików w usłudze Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a>Zwiększenie wydajności przez kompresowanie plików w usłudze Azure CDN
Jest to prosta i skuteczna metoda szybkości transferu plików tooimprove i zwiększyć strony obciążenia wydajność przez zmniejszenie rozmiaru pliku przed są wysyłane z serwera hello. Zmniejsza kosztów przepustowości i zapewnia bardziej odpowiednie dla użytkowników.

Istnieją dwa sposoby tooenable kompresji:

* W takim przypadku hello CDN przechodzą hello skompresowane pliki i dostarczać tooclients skompresowane pliki, które ich zażądać, można włączyć kompresję na serwerze pochodzenia.
* Można włączyć kompresję bezpośrednio w sieci CDN krawędzi serwerów, w których wielkość hello CDN kompresuje hello plików i obsługujących je tooend użytkowników, nawet jeśli nie są kompresowane przez powitania serwera źródłowego.

> [!IMPORTANT]
> Zmiany konfiguracji sieci CDN w warstwie podjąć pewne toopropagate czas za pośrednictwem sieci hello.  Aby uzyskać <b>Azure CDN from Akamai</b> profile, propagacji zazwyczaj kończy w obszarze jednej minuty.  Aby uzyskać <b>Azure CDN from Verizon</b> profile, zwykle widoczne zmiany w ciągu 90 minut.  Jeśli jest to powitania po raz pierwszy po skonfigurowaniu kompresji dla punktu końcowego CDN, należy rozważyć oczekuje się, że ustawienia kompresji hello zostaną rozpropagowane POP toohello przed rozpoczęciem rozwiązywania toobe 1 – 2 godz.
> 
> 

## <a name="enabling-compression"></a>Włączanie kompresji
> [!NOTE]
> Witaj warstwy standardowa i Premium CDN Podaj hello tę samą funkcjonalność kompresji, ale hello interfejs użytkownika różni się.  Aby uzyskać więcej informacji o różnicach hello warstwy standardowa i Premium usługi CDN, zobacz [Omówienie usługi Azure CDN](cdn-overview.md).
> 
> 

### <a name="standard-tier"></a>Warstwa standardowa
> [!NOTE]
> Ta sekcja dotyczy zbyt**Azure CDN Standard from Verizon** i **Azure CDN Standard from Akamai** profilów.
> 
> 

1. Strony profilu CDN hello kliknij punkt końcowy CDN hello mają toomanage.
   
    ![Punkty końcowe strony profilu CDN](./media/cdn-file-compression/cdn-endpoints.png)
   
    zostanie otwarta strona punktu końcowego CDN Hello.
2. Kliknij przycisk hello **Konfiguruj** przycisku.
   
    ![Przycisk Zarządzaj strony profilu CDN](./media/cdn-file-compression/cdn-config-btn.png)
   
    zostanie otwarta strona konfiguracji CDN Hello.
3. Włącz **kompresji**.
   
    ![Opcje kompresji CDN](./media/cdn-file-compression/cdn-compress-standard.png)
4. Użyj typów domyślnych hello lub zmodyfikuj listę hello usuwając lub dodając typów plików.
   
   > [!TIP]
   > Czas jest to możliwe, nie zaleca się tooapply toocompressed kompresji, takich jak ZIP, MP3, MP4, JPG itp.
   > 
   > 
5. Po wprowadzeniu zmian, kliknij przycisk hello **zapisać** przycisku.

### <a name="premium-tier"></a>Warstwa Premium
> [!NOTE]
> Ta sekcja dotyczy zbyt**Azure CDN Premium from Verizon** profilów.
> 
> 

1. Ze strony profilu CDN hello, kliknij przycisk hello **Zarządzaj** przycisku.
   
    ![Przycisk Zarządzaj strony profilu CDN](./media/cdn-file-compression/cdn-manage-btn.png)
   
    Otwiera portalu zarządzania Hello CDN.
2. Przesuń kursor myszy hello **HTTP dużych** kartę, a następnie przesuń kursor myszy hello **ustawienia pamięci podręcznej** wysuwane okno.  Polecenie **kompresji**.

    ![Wybieranie pliku kompresji](./media/cdn-file-compression/cdn-compress-select.png)
   
    Opcje kompresji są wyświetlane.
   
    ![Kompresja plików](./media/cdn-file-compression/cdn-compress-files.png)
3. Włącz kompresję, klikając hello **włączyć kompresji,** przycisk radiowy.  Wprowadź typy MIME hello mają toocompress jako listę rozdzielanych przecinkami (bez spacji) w hello **typów plików** pola tekstowego.
   
   > [!TIP]
   > Czas jest to możliwe, nie zaleca się tooapply toocompressed kompresji, takich jak ZIP, MP3, MP4, JPG itp. 
   > 
   > 
4. Po wprowadzeniu zmian, kliknij przycisk hello **aktualizacji** przycisku.

## <a name="compression-rules"></a>Reguły kompresji
Te tabele zawierają opis usługi Azure CDN kompresji zachowanie dla każdego scenariusza.

> [!IMPORTANT]
> Aby uzyskać **Azure CDN from Verizon** są kompresowane tylko odpowiednich plików (Standard i Premium).  toobe kwalifikuje się do kompresji, pliku, musi:
> 
> * Być większa niż 128 bajtów.
> * Być mniejszy niż 1 MB.
> 
> Aby uzyskać **Azure CDN from Akamai**, wszystkie pliki kwalifikują się do kompresji.
> 
> Dla wszystkich produktów Azure CDN, plik musi być typ MIME, który został [skonfigurowane kompresji](#enabling-compression).
> 
> **Usługi Azure CDN from Verizon** profile pomocy technicznej (Standard i Premium) **gzip** (GNU zip), **deflate**, **bzip2**, lub **br** kodowania (Brotli). Brotli kodowania, kompresji hello odbywa się tylko na powitania krawędzi. przeglądarka klienta Hello musi wysłać żądanie hello Brotli kodowania i zasobów skompresowany hello musi skompresowane po stronie źródła hello najpierw. 
>
>**Azure CDN from Akamai** profile obsługują tylko **gzip** kodowania.
> 
> **Azure CDN from Akamai** punkty końcowe zawsze żądania **gzip** pliki pochodzenia hello, niezależnie od tego, żądania klienta hello algorytmem. 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a>Kompresja wyłączona lub plik nie kwalifikuje się do kompresji
| Żądany format klienta (za pośrednictwem nagłówka Accept-Encoding) | Format pliku pamięci podręcznej | Klient toohello odpowiedzi CDN | Uwagi |
| --- | --- | --- | --- |
| Skompresowane |Skompresowane |Skompresowane | |
| Skompresowane |Nieskompresowanych |Nieskompresowanych | |
| Skompresowane |Nie w pamięci podręcznej |Skompresowane lub nieskompresowane |Zależy od źródła odpowiedzi |
| Nieskompresowanych |Skompresowane |Nieskompresowanych | |
| Nieskompresowanych |Nieskompresowanych |Nieskompresowanych | |
| Nieskompresowanych |Nie w pamięci podręcznej |Nieskompresowanych | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a>Kompresja włączona i pliku nie kwalifikuje się do kompresji
| Żądany format klienta (za pośrednictwem nagłówka Accept-Encoding) | Format pliku pamięci podręcznej | Klient toohello odpowiedzi CDN | Uwagi |
| --- | --- | --- | --- |
| Skompresowane |Skompresowane |Skompresowane |Transcodes CDN pomiędzy obsługiwanych formatów |
| Skompresowane |Nieskompresowanych |Skompresowane |CDN wykonuje kompresji |
| Skompresowane |Nie w pamięci podręcznej |Skompresowane |Jeśli punkt początkowy zwraca nieskompresowanych, CDN wykonuje kompresji.  **Usługi Azure CDN from Verizon** przekazuje hello nieskompresowanego pliku na pierwsze Żądanie hello, a następnie kompresuje i pamięci podręczne hello pliku dla kolejnych żądań.  Pliki z `Cache-Control: no-cache` nagłówka nigdy nie zostanie skompresowany. |
| Nieskompresowanych |Skompresowane |Nieskompresowanych |Dekompresja wykonuje CDN |
| Nieskompresowanych |Nieskompresowanych |Nieskompresowanych | |
| Nieskompresowanych |Nie w pamięci podręcznej |Nieskompresowanych | |

## <a name="media-services-cdn-compression"></a>Kompresja CDN usługi multimediów
Usługi multimediów w sieci CDN włączona punktów końcowych przesyłania strumieniowego, kompresji jest domyślnie włączona dla hello następujące typy zawartości: application/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, aplikacji/f4m + xml. Użytkownik nie Włączanie/wyłączanie kompresji hello wymienionych typów za pomocą hello portalu Azure.  

## <a name="see-also"></a>Zobacz też
* [Rozwiązywanie problemów związanych z kompresją pliku CDN](cdn-troubleshoot-compression.md)    

