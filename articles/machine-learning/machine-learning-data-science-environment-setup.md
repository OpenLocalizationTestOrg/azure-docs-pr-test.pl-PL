---
title: "Konfigurowanie środowisk nauki danych na platformie Azure | Dokumentacja firmy Microsoft"
description: "Ustawienia danych środowisk nauki na platformie Azure do użycia w procesie nauki danych zespołu."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 481cfa6a-7ea3-46ac-b0f9-2e3982c37153
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: bradsev
ms.openlocfilehash: 4f2f66288428aa0aa41abb40ce0e43c4848543ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-data-science-environments-for-use-in-the-team-data-science-process"></a><span data-ttu-id="003c3-103">Konfigurowanie środowisk analizy danych do użytku w zespołowym przetwarzaniu danych dla celów naukowych</span><span class="sxs-lookup"><span data-stu-id="003c3-103">Set up data science environments for use in the Team Data Science Process</span></span>
<span data-ttu-id="003c3-104">Proces nauki danych zespołu używa różnych środowiskach nauki danych do przechowywania, przetwarzania i analizy danych.</span><span class="sxs-lookup"><span data-stu-id="003c3-104">The Team Data Science Process uses various data science environments for the storage, processing, and analysis of data.</span></span> <span data-ttu-id="003c3-105">Obejmują one magazynu obiektów Blob Azure, maszyny wirtualne platformy Azure, klastry usługi HDInsight (Hadoop) i obszarów roboczych usługi Azure Machine Learning kilku typów.</span><span class="sxs-lookup"><span data-stu-id="003c3-105">They include Azure Blob Storage, several types of Azure virtual machines, HDInsight (Hadoop) clusters, and Azure Machine Learning workspaces.</span></span> <span data-ttu-id="003c3-106">Decyzja o poszczególnych środowisk do użycia zależy od typu i ilość danych, aby być modelowane i docelowej dla tych danych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="003c3-106">The decision about which environment to use depends on the type and quantity of data to be modeled and the target destination for that data in the cloud.</span></span> 

* <span data-ttu-id="003c3-107">Aby uzyskać wskazówki dotyczące pytań, na które należy wziąć pod uwagę podczas tworzenia tej decyzji, zobacz [planowanie Your Azure Learning danych nauki środowiska maszyny](machine-learning-data-science-plan-your-environment.md).</span><span class="sxs-lookup"><span data-stu-id="003c3-107">For guidance on questions to consider when making this decision, see [Plan Your Azure Machine Learning Data Science Environment](machine-learning-data-science-plan-your-environment.md).</span></span> 
* <span data-ttu-id="003c3-108">Dla katalogu niektóre scenariusze mogą wystąpić podczas wykonywania zaawansowane metody analizy, zobacz [scenariusze dotyczące procesu nauki danych zespołu](machine-learning-data-science-plan-sample-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="003c3-108">For a catalog of some of the scenarios you might encounter when doing advanced analytics, see [Scenarios for the Team Data Science Process](machine-learning-data-science-plan-sample-scenarios.md)</span></span>

<span data-ttu-id="003c3-109">To menu łącza do tematów opisujących sposób konfigurowania różnych środowiskach nauki danych używanych przez proces nauki danych Team.</span><span class="sxs-lookup"><span data-stu-id="003c3-109">This menu links to topics that describe how to set up the various data science environments used by the Team Data Science Process.</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="003c3-110">**Microsoft danych nauki maszyny wirtualnej (DSVM)** jest również dostępny jako obraz maszyny wirtualnej platformy Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="003c3-110">The **Microsoft Data Science Virtual Machine (DSVM)** is also available as an Azure virtual machine (VM) image.</span></span> <span data-ttu-id="003c3-111">Ta maszyna wirtualna jest wstępnie zainstalowane i skonfigurowane z kilku popularnych narzędzi, które są często używane do analizy danych i uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="003c3-111">This VM is pre-installed and configured with several popular tools that are commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="003c3-112">DSVM jest dostępna w systemach Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="003c3-112">The DSVM is available on both Windows and Linux.</span></span> <span data-ttu-id="003c3-113">Aby uzyskać więcej informacji, zobacz [wprowadzenie do opartej na chmurze danych nauki maszyny wirtualnej systemu Linux i Windows](machine-learning-data-science-virtual-machine-overview.md).</span><span class="sxs-lookup"><span data-stu-id="003c3-113">For further information, see [Introduction to the cloud-based Data Science Virtual Machine for Linux and Windows](machine-learning-data-science-virtual-machine-overview.md).</span></span>

