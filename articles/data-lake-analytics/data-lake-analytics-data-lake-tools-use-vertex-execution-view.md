---
title: "Witaj aaaUse widoku wykonania wierzchołka w narzędzi Data Lake Tools dla programu Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello zadania usługi Data Lake Analytics tooexam widoku wykonania wierzchołka."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="64925-103">Użyj widoku wykonania wierzchołka hello w narzędzi Data Lake Tools dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="64925-103">Use hello Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="64925-104">Dowiedz się, jak toouse hello zadania usługi Data Lake Analytics tooexam widoku wykonania wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="64925-104">Learn how toouse hello Vertex Execution View tooexam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64925-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="64925-105">Prerequisites</span></span>

<span data-ttu-id="64925-106">Należy podstawową wiedzę na temat przy użyciu narzędzi Data Lake Tools dla Visual Studio skryptu toodevelop U-SQL.</span><span class="sxs-lookup"><span data-stu-id="64925-106">You need basic knowledge of using Data Lake Tools for Visual Studio toodevelop U-SQL script.</span></span>  <span data-ttu-id="64925-107">Zobacz [samouczek: tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="64925-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-hello-vertex-execution-view"></a><span data-ttu-id="64925-108">Otwórz hello widoku wykonania wierzchołka</span><span class="sxs-lookup"><span data-stu-id="64925-108">Open hello Vertex Execution View</span></span>
<span data-ttu-id="64925-109">Otwórz zadania skryptu U-SQL w narzędzi Data Lake Tools dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="64925-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="64925-110">Kliknij przycisk **widoku wykonania wierzchołka** hello dole po lewej stronie ekranu.</span><span class="sxs-lookup"><span data-stu-id="64925-110">Click **Vertex Execution View** in hello bottom left corner.</span></span> <span data-ttu-id="64925-111">Zostanie wyświetlony monit o tooload profile może być najpierw i może potrwać pewien czas w zależności od połączenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="64925-111">You may be prompted tooload profiles first and it can take some time depending on your network connectivity.</span></span>

![Widoku wykonania wierzchołka narzędzi Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="64925-113">Zrozumienie widoku wykonania wierzchołka</span><span class="sxs-lookup"><span data-stu-id="64925-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="64925-114">Witaj, widoku wykonania wierzchołka ma trzy części:</span><span class="sxs-lookup"><span data-stu-id="64925-114">hello Vertex Execution View has three parts:</span></span>

![Widoku wykonania wierzchołka narzędzi Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="64925-116">Witaj **selektora wierzchołków** na powitania po lewej stronie umożliwia wybrania wierzchołków przez funkcje (takie jak pierwszych 10 danych do odczytu, lub wybierz etapem).</span><span class="sxs-lookup"><span data-stu-id="64925-116">hello **Vertex selector** on hello left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="64925-117">Jeden z filtrów najbardziej często używanych hello jest toosee hello **wierzchołków ścieżkę krytyczną**.</span><span class="sxs-lookup"><span data-stu-id="64925-117">One of hello most commonly-used filters is toosee hello **vertices on critical path**.</span></span> <span data-ttu-id="64925-118">Witaj **ścieżkę krytyczną** hello łańcuch najdłuższym wierzchołków zadania skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="64925-118">hello **Critical path** is hello longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="64925-119">Ścieżkę krytyczną hello opis przydaje się do optymalizacji zadaniach sprawdzając, które wierzchołek ma najdłużej hello.</span><span class="sxs-lookup"><span data-stu-id="64925-119">Understanding hello critical path is useful for optimizing your jobs by checking which vertex takes hello longest time.</span></span>
  
![Widoku wykonania wierzchołka narzędzi Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="64925-121">Witaj górnej w okienku zostaną wyświetlone hello **bieżący stan wszystkich wierzchołków hello**.</span><span class="sxs-lookup"><span data-stu-id="64925-121">hello top center pane shows hello **running status of all hello vertices**.</span></span>
  
![Widoku wykonania wierzchołka narzędzi Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="64925-123">Witaj dołu w środkowym okienku przedstawia informacje o każdy wierzchołek:</span><span class="sxs-lookup"><span data-stu-id="64925-123">hello bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="64925-124">Nazwa procesu: Nazwa hello hello wierzchołków wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="64925-124">Process Name: hello name of hello vertex instance.</span></span> <span data-ttu-id="64925-125">Składa się z różnych części w Nazwa etapu | VertexName | VertexRunInstance.</span><span class="sxs-lookup"><span data-stu-id="64925-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="64925-126">Na przykład wierzchołków [62] .v1 hello SV7_Split oznacza hello drugi działającego wystąpienia (.v1, indeksem rozpoczynającym się od 0) liczby wierzchołków 62 w SV7_Split etapu.</span><span class="sxs-lookup"><span data-stu-id="64925-126">For example, hello SV7_Split[62].v1 vertex stands for hello second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="64925-127">Całkowita odczytu danych/Written: hello danych została odczytana/zapisana przez ten wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="64925-127">Total Data Read/Written: hello data was read/written by this vertex.</span></span>
* <span data-ttu-id="64925-128">Stan Stan/wyjścia: hello stan końcowy po zakończeniu hello wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="64925-128">State/Exit Status: hello final status when hello vertex is ended.</span></span>
* <span data-ttu-id="64925-129">Typu wystąpił błąd i kodu zakończenia: błąd hello hello wierzchołków nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="64925-129">Exit Code/Failure Type: hello error when hello vertex failed.</span></span>
* <span data-ttu-id="64925-130">Tworzenie Przyczyna: Dlaczego wierzchołków hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="64925-130">Creation Reason: Why hello vertex was created.</span></span>
* <span data-ttu-id="64925-131">Zasobów opóźnienia/procesu opóźnienia/NC kolejki opóźnienia: hello czas poświęcony na powitania wierzchołków toowait zasobów, tooprocess danych i toostay w kolejce hello.</span><span class="sxs-lookup"><span data-stu-id="64925-131">Resource Latency/Process Latency/PN Queue Latency: hello time taken for hello vertex toowait for resources, tooprocess data, and toostay in hello queue.</span></span>
* <span data-ttu-id="64925-132">Identyfikator GUID procesu/Twórcy: Identyfikator GUID bieżącej wierzchołków uruchomionych hello lub twórcy.</span><span class="sxs-lookup"><span data-stu-id="64925-132">Process/Creator GUID: GUID for hello current running vertex or its creator.</span></span>
* <span data-ttu-id="64925-133">Wersja: hello N-ty percentyl wystąpienie hello systemem wierzchołków (hello systemu zaplanować nowych wystąpień wierzchołek dla wiele przyczyn, na przykład przejścia w tryb failover obliczeniowe nadmiarowość itp.)</span><span class="sxs-lookup"><span data-stu-id="64925-133">Version: hello N-th instance of hello running vertex (hello system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="64925-134">Utworzona wersja czasu.</span><span class="sxs-lookup"><span data-stu-id="64925-134">Version Created Time.</span></span>
* <span data-ttu-id="64925-135">Utwórz początkowy czas i proces w kolejce czas i proces początkowy czas i proces Complete przetworzyć czasu: po uruchomieniu hello wierzchołków procesu tworzenia; podczas procesu wierzchołków hello uruchamiania tooqueue; gdy hello niektórych uruchamia proces wierzchołka; gdy hello niektórych wierzchołków zostanie ukończona.</span><span class="sxs-lookup"><span data-stu-id="64925-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when hello vertex process starts creation; when hello vertex process starts tooqueue; when hello certain vertex process starts; when hello certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64925-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="64925-136">Next steps</span></span>
* <span data-ttu-id="64925-137">informacje diagnostyczne toolog, zobacz [uzyskiwanie dostępu do dzienników diagnostycznych dla usługi Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="64925-137">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="64925-138">toosee bardziej złożonego zapytania, zobacz [witryny sieci Web analizowanie dzienników przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="64925-138">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="64925-139">Zobacz szczegóły zadania tooview, [użyj przeglądarki zadania i widok zadań dla zadania usługi Azure Data lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="64925-139">tooview job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
