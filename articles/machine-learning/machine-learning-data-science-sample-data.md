---
title: "Przykładowe dane w kontenerów obiektów blob platformy Azure, programu SQL Server i program Hive tabel | Dokumentacja firmy Microsoft"
description: "Jak eksplorować dane przechowywane w różnych enviromnents platformy Azure."
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
ms.openlocfilehash: 0683be564a88ef54882e8d882d196851ecac243d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="e7750-103"><a name="heading"></a>Przykładowe dane w kontenerów obiektów blob platformy Azure, programu SQL Server i program Hive tabel</span><span class="sxs-lookup"><span data-stu-id="e7750-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="e7750-104">Ten dokument linki do tematów, który opisano przykładowe dane, które są przechowywane w jednym z trzech różnych lokalizacji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="e7750-104">This document links to topics that covers how to sample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="e7750-105">**Dane w kontenerze obiektów blob platformy Azure** jest próbkowany przez programowo ją pobrać i następnie pobierania próbek z przykładowy kod języka Python.</span><span class="sxs-lookup"><span data-stu-id="e7750-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="e7750-106">**Dane programu SQL Server** jest próbkować za pomocą programy SQL i język programowania Python.</span><span class="sxs-lookup"><span data-stu-id="e7750-106">**SQL Server data** is sampled using both SQL and the Python Programming Language.</span></span> 
* <span data-ttu-id="e7750-107">**Dane tabeli hive** jest próbkować za pomocą zapytań programu Hive.</span><span class="sxs-lookup"><span data-stu-id="e7750-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="e7750-108">Następujące **menu** linki do tematów opisujących sposób próbkowania danych z każdej z tych środowisk magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="e7750-108">The following **menu** links to the topics that describe how to sample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="e7750-109">To zadanie próbkowania jest krokiem w [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="e7750-109">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="e7750-110">**Dlaczego przykładowe dane?**</span><span class="sxs-lookup"><span data-stu-id="e7750-110">**Why sample data?**</span></span>

<span data-ttu-id="e7750-111">Jeśli zestaw danych, które mają być analizowanie jest duży, zazwyczaj jest dobrym rozwiązaniem w dół przykładowych danych, aby zmniejszyć jego rozmiar mniejsze, ale reprezentatywny i łatwiejsze w zarządzaniu.</span><span class="sxs-lookup"><span data-stu-id="e7750-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="e7750-112">To ułatwia zrozumienie danych, badanie i inżynieria funkcji.</span><span class="sxs-lookup"><span data-stu-id="e7750-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="e7750-113">Swoją rolę w procesie Analytics Cortana jest umożliwienie szybkiego prototypy funkcji przetwarzania danych i modeli uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="e7750-113">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

