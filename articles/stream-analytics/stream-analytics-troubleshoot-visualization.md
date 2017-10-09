---
title: "aaaVisualize i rozwiązywać problemy dotyczące zadania usługi analiza strumienia | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toovisualize zadanie usługi Stream Analytics potoku dla Rozwiązywanie problemów przy użyciu funkcji diagram diagnostyki hello samoobsługi."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8a6715be601fdc47b8d9caf4112da161dad22618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="0b1ab-103">Tworzenie wizualizacji i rozwiązywanie problemów z zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="0b1ab-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="0b1ab-104">W Stream Analytics tak jak w przypadku innych technologii chmurowych rozwiązywania problemów jest czasami toolook potrzebne do dlaczego zadania nie tworzy hello oczekiwane dane wyjściowe (lub żadnych danych wyjściowych istotnego dla badania).</span><span class="sxs-lookup"><span data-stu-id="0b1ab-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed toolook into why a job does not produce hello expected output (or any output for that matter).</span></span> <span data-ttu-id="0b1ab-105">Pamiętając o tym Stream Analytics zapewnia możliwość hello do wizualizacji zadanie przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="0b1ab-105">With this in mind, Stream Analytics provides hello capability for visualizing a streaming job.</span></span> <span data-ttu-id="0b1ab-106">To jest również przydatne jako narzędzia do modelowania i ma powitania po stronie korzyści dla ludzi wymagających dokumentacji ich pracy.</span><span class="sxs-lookup"><span data-stu-id="0b1ab-106">This is also handy as a modeling tool and has hello side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="0b1ab-107">W wizualizacji hello są widoczne oraz zapytania hello panelu hello wejść, a następnie wszystkie dane wyjściowe hello konfigurować.</span><span class="sxs-lookup"><span data-stu-id="0b1ab-107">In hello visualization panel hello inputs are visible as well as hello query being executed and then all hello outputs configured.</span></span> <span data-ttu-id="0b1ab-108">Problemy z łącznością lub konfiguracją może okazać się bardziej, a można też przydatne toosee wizualną reprezentację danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0b1ab-108">Connectivity or configuration issues can become more apparent and it can also be helpful toosee a visual representation of your configuration.</span></span>

## <a name="using-hello-diagnosis-diagram-tool"></a><span data-ttu-id="0b1ab-109">Za pomocą narzędzia diagram diagnostyki hello</span><span class="sxs-lookup"><span data-stu-id="0b1ab-109">Using hello diagnosis diagram tool</span></span>
<span data-ttu-id="0b1ab-110">tooaccess tego wizualizatora, po prostu kliknij hello przycisk "Diagnostyki diagram" w hello bloku "Ustawienia" hello hello zadanie usługi Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="0b1ab-110">tooaccess this visualizer, simply click on hello “Diagnosis diagram” button in hello “Settings” blade of hello of hello Stream Analytics job.</span></span>

![Stream-Analytics-Troubleshoot-visualization-Diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="0b1ab-112">Co wejściowa i wyjściowa jest zaznaczony kolorami tooindicate hello bieżący stan tego składnika, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="0b1ab-112">Every input and output is color coded tooindicate hello current state of that component, as shown below.</span></span>

![Stream-Analytics-Troubleshoot-visualization-Input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="0b1ab-114">Gdy hello użytkownik chce toolook na pośrednie kroki toounderstand hello danych przepływu wzorców zapytań wewnątrz zadania, narzędziem hello zawiera widok podział hello hello zapytania do jej kroki składnika i hello sekwencja przepływu.</span><span class="sxs-lookup"><span data-stu-id="0b1ab-114">When hello user wants toolook at intermediate query steps toounderstand hello data flow patterns inside a job, hello visualization tool provides a view of hello breakdown of hello query into its component steps and hello flow sequence.</span></span> <span data-ttu-id="0b1ab-115">Kliknięcie na każdym etapie zapytania spowoduje wyświetlenie hello odpowiedniej sekcji w zapytaniu edycji okienku zgodnie z opisami.</span><span class="sxs-lookup"><span data-stu-id="0b1ab-115">Clicking on each query step will show hello corresponding section in a query editing pane as illustrated.</span></span> 

![Stream-Analytics-Troubleshoot-visualization-Intermediate-Steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="0b1ab-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0b1ab-117">Next steps</span></span>
* [<span data-ttu-id="0b1ab-118">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="0b1ab-118">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="0b1ab-119">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="0b1ab-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="0b1ab-120">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="0b1ab-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="0b1ab-121">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="0b1ab-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="0b1ab-122">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="0b1ab-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

