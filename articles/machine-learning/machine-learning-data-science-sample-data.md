---
title: "aaaSample danych na platformie Azure blob kontenerów, SQL Server i program Hive tabel | Dokumentacja firmy Microsoft"
description: "Jak tooexplore dane przechowywane w różnych enviromnents platformy Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5a5295b59fa02f91da680fc7495a92ca135e26c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="40f16-103"><a name="heading"></a>Przykładowe dane w kontenerów obiektów blob platformy Azure, programu SQL Server i program Hive tabel</span><span class="sxs-lookup"><span data-stu-id="40f16-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="40f16-104">Ten dokument zawiera linki tootopics, który obejmuje jak toosample dane przechowywane w jednym z trzech różnych lokalizacji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="40f16-104">This document links tootopics that covers how toosample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="40f16-105">**Dane w kontenerze obiektów blob platformy Azure** jest próbkowany przez programowo ją pobrać i następnie pobierania próbek z przykładowy kod języka Python.</span><span class="sxs-lookup"><span data-stu-id="40f16-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="40f16-106">**Dane programu SQL Server** jest próbkować za pomocą programy SQL i hello języka programowania Python.</span><span class="sxs-lookup"><span data-stu-id="40f16-106">**SQL Server data** is sampled using both SQL and hello Python Programming Language.</span></span> 
* <span data-ttu-id="40f16-107">**Dane tabeli hive** jest próbkować za pomocą zapytań programu Hive.</span><span class="sxs-lookup"><span data-stu-id="40f16-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="40f16-108">następujące Hello **menu** łączy toohello tematach opisano sposób toosample danych z każdej z tych środowisk magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="40f16-108">hello following **menu** links toohello topics that describe how toosample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="40f16-109">To zadanie próbkowania jest etapem hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="40f16-109">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="40f16-110">**Dlaczego przykładowe dane?**</span><span class="sxs-lookup"><span data-stu-id="40f16-110">**Why sample data?**</span></span>

<span data-ttu-id="40f16-111">Jeśli planujesz tooanalyze dataset hello jest duży, zazwyczaj jest to dobrze hello toodown przykładowych danych tooreduce jego rozmiar tooa mniejsze, ale reprezentatywny i łatwiejsze w zarządzaniu.</span><span class="sxs-lookup"><span data-stu-id="40f16-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="40f16-112">To ułatwia zrozumienie danych, badanie i inżynieria funkcji.</span><span class="sxs-lookup"><span data-stu-id="40f16-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="40f16-113">Swoją rolę w hello Cortana Analytics procesu jest szybkie tworzenie prototypów tooenable hello przetwarzania danych funkcji i modeli uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="40f16-113">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

