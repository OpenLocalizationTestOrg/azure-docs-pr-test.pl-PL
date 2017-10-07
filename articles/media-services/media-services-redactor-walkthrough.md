---
title: "aaaRedact krojów z przewodnikiem analizy multimediów Azure | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono instrukcje krok po kroku na temat toorun redakcyjne pełnego przepływu pracy przy użyciu usługi Azure Media Services Explorer (AMSE) i Azure Media Redactor Visualizer (narzędzie typu open source)."
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a>Redagowanie krojów z przewodnikiem analizy multimediów Azure

## <a name="overview"></a>Omówienie

**Azure Media Redactor** jest [analizy multimediów Azure](media-services-analytics-overview.md) procesor multimediów (MP) oferuje skalowalne krój redakcyjne w chmurze hello. Redakcyjne krój umożliwia możesz toomodify wideo w kolejności tooblur kroje wybrane osoby. Możesz toouse hello krój redakcyjne usługi w publicznych scenariusze bezpieczeństwa i nośnika wiadomości. Kilka minut najmniejszym zawiera wiele kroje może zająć godziny tooredact ręcznie, ale z tej usługi hello powierzchni procesu redakcyjne wymaga kilku prostych krokach. Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/blog/azure-media-redactor/) blogu.

Szczegółowe informacje o **Azure Media Redactor**, zobacz hello [omówienie redakcyjne krój](media-services-face-redaction.md) tematu.

W tym temacie przedstawiono instrukcje krok po kroku na temat toorun redakcyjne pełnego przepływu pracy przy użyciu usługi Azure Media Services Explorer (AMSE) i Azure Media Redactor Visualizer (narzędzie typu open source).

Witaj **Azure Media Redactor** pakiet administracyjny jest obecnie w przeglądzie. Jest ona dostępna w wszystkich publicznych regiony platformy Azure, a także centrach danych instytucji rządowych Stanów Zjednoczonych i Chinach. Ta wersja zapoznawcza jest obecnie bezpłatnie. W bieżącej wersji hello istnieje limit 10 minut na przetworzonych długość wideo.

Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blogu.

## <a name="azure-media-services-explorer-workflow"></a>Azure Media Services Explorer przepływu pracy

Witaj najprostszym tooget sposób pracy z Redactor jest narzędzie AMSE toouse hello typu open source w witrynie github. Możesz uruchomić uproszczony przepływu pracy za pośrednictwem **łączyć** tryb, jeśli nie wymagają dostępu toohello adnotacji json lub hello krój obrazów jpg.

### <a name="download-and-setup"></a>Pobierania i instalacji

1. Pobierz narzędzie AMSE hello [tutaj](https://github.com/Azure/Azure-Media-Services-Explorer).
1. Zaloguj się za tooyour konta usługi Media Services przy użyciu klucza usługi.

    Witaj tooobtain nazwę konta i informacje o kluczu, przejdź toohello [portalu Azure](https://portal.azure.com/) i wybierz konto usługi AMS. Wybierz ustawienia > klucze. Hello Zarządzaj kluczami w systemie windows zawiera nazwę konta hello i klucze podstawowe i pomocnicze hello jest wyświetlany. Skopiuj wartości hello nazwę konta i klucz podstawowy hello.

![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a>Najpierw przekazać — analizowanie tryb

1. Przekazywanie pliku multimediów za pośrednictwem zasobów –> przekazywania, lub za pośrednictwem operacji przeciągania i upuszczania. 
1. Kliknij prawym przyciskiem myszy i przetwarzanie pliku nośnika, przy użyciu analizy multimediów Azure Media Redactor –> –> Tryb analizy. 


![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

dane wyjściowe Hello będzie zawierać plik json adnotacje z danych lokalizacji krój, a także jpg każdego wykrytego powierzchni. 

![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a>Drugi przekazać — redagowanie tryb

1. Przekaż oryginalnego toohello zawartości wideo dane wyjściowe z pierwszym przebiegu hello i Ustaw jako podstawowy zasobów. 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. (Opcjonalnie) Przekaż plik "Dance_idlist.txt", który zawiera listę hello identyfikatory mają tooredact rozdzielone znakami nowego wiersza. 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. (Opcjonalnie) Należy każdego edycji toohello annotations.json pliku, takich jak zwiększenie hello ograniczający granice pola. 
4. Witaj zawartości wyjściowej z pierwszym przebiegu hello kliknij prawym przyciskiem myszy, wybierz hello Redactor i uruchom z hello **Redact** tryb. 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. Pobieranie i udostępnianie zasobów ostateczne dane wyjściowe zredagowanym hello. 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a>Azure Media Redactor wizualizatora typu open source narzędzia

Typu open source [narzędzie wizualizatora](https://github.com/Microsoft/azure-media-redactor-visualizer) jest uruchamiana z formatem adnotacje hello z analizy i przy użyciu danych wyjściowych hello deweloperzy toohelp zaprojektowane.

Po sklonować repozytorium hello, w projekcie hello toorun kolejności, konieczne będzie toodownload FFMPEG z ich [oficjalna witryna](https://ffmpeg.org/download.html).

Jeśli jesteś deweloperem hello tooparse JSON adnotacji danych w trakcie, poszukaj wewnątrz Models.MetaData przykłady kodu przykładowej.

### <a name="set-up-hello-tool"></a>Konfigurowanie narzędzia hello

1.  Pobieranie i tworzenie hello całego rozwiązania. 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  Pobierz FFMPEG z [tutaj](https://ffmpeg.org/download.html). Ten projekt pierwotnie został opracowany z wersji be1d324 (2016-10-04) z statycznego łączenia. 
3.  Skopiuj toohello ffmpeg.exe i ffprobe.exe tego samego folderu wyjściowego jako AzureMediaRedactor.exe. 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. Uruchom AzureMediaRedactor.exe. 

### <a name="use-hello-tool"></a>Użyj narzędzia hello

1. Przetwarzanie wideo na koncie usługi Azure Media Services z hello Redactor MP na tryb analizy. 
2. Pobierz hello oryginalny plik wideo i na wyjściu hello hello redakcyjne — analizowanie zadania. 
3. Uruchom aplikację wizualizatora hello i wybierz pliki hello powyżej. 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. Wyświetl podgląd pliku. SELECT, która zostanie skierowany chcieliby tooblur za pomocą paska bocznego hello na powitania prawo. 
    
    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  pole tekstowe dolnej Hello zaktualizuje krój hello identyfikatorów. Utwórz plik o nazwie "idlist.txt" te identyfikatory jako listę rozdzielone znakami nowego wiersza. 

    >[!NOTE]
    > Witaj idlist.txt powinny być zapisane w formacie ANSI. Można użyć toosave Notatnik w formacie ANSI.
    
6.  Przekazywanie zawartości wyjściowej toohello tego pliku z kroku 1. Przekaż hello wideo toothis oryginału również i Ustaw jako podstawowy zasobów. 
7.  Uruchom zadanie redakcyjne ten zasób z "Redact" Tryb tooget hello końcowego zredagowanym wideo. 

## <a name="next-steps"></a>Następne kroki 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Powiązane linki
[Przegląd analiz usługi Azure Media Services](media-services-analytics-overview.md)

[W trakcie analizy multimediów Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[Anonsowanie redakcyjne krój na potrzeby analizy multimediów Azure](https://azure.microsoft.com/blog/azure-media-redactor/)
