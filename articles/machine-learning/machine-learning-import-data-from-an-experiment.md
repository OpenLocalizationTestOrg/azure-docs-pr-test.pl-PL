---
title: "Importowanie danych do usługi Machine Learning Studio z innego eksperymentu | Dokumentacja firmy Microsoft"
description: "Jak zapisać danych szkoleniowych w usłudze Azure Machine Learning Studio i używać go w innym eksperymentu."
keywords: "Importowanie danych, danych, źródła danych, dane szkoleniowe"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 7da9dcec-5693-4bb6-8166-15904e7f75c3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: ecfa2110d0d51511ceb5bd07b730732ecfa2e9e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="import-your-data-into-azure-machine-learning-studio-from-another-experiment"></a><span data-ttu-id="57f2c-104">Importowanie danych do usługi Azure Machine Learning Studio z poziomu innego eksperymentu</span><span class="sxs-lookup"><span data-stu-id="57f2c-104">Import your data into Azure Machine Learning Studio from another experiment</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="57f2c-105">Będzie razy, kiedy należy podjąć pośrednich wyników z doświadczenia i użycie go jako część innego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="57f2c-105">There will be times when you'll want to take an intermediate result from one experiment and use it as part of another experiment.</span></span> <span data-ttu-id="57f2c-106">Aby to zrobić, należy zapisać modułu jako zestawu danych:</span><span class="sxs-lookup"><span data-stu-id="57f2c-106">To do this, you save the module as a dataset:</span></span>

1. <span data-ttu-id="57f2c-107">Kliknij przycisk dane wyjściowe moduł, który ma zostać zapisany jako zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="57f2c-107">Click the output of the module that you want to save as a dataset.</span></span>
2. <span data-ttu-id="57f2c-108">Kliknij przycisk **Zapisz jako zestawu danych**.</span><span class="sxs-lookup"><span data-stu-id="57f2c-108">Click **Save as Dataset**.</span></span>
3. <span data-ttu-id="57f2c-109">Po wyświetleniu monitu wprowadź nazwę i opis, który umożliwi łatwo identyfikować zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="57f2c-109">When prompted, enter a name and a description that would allow you to identify the dataset easily.</span></span>
4. <span data-ttu-id="57f2c-110">Kliknij przycisk **OK** znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="57f2c-110">Click the **OK** checkmark.</span></span>

<span data-ttu-id="57f2c-111">Po zakończeniu Zapisz zestaw danych będą dostępne do użycia w ramach każdego doświadczenia w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="57f2c-111">When the save finishes, the dataset will be available for use within any experiment in your workspace.</span></span> <span data-ttu-id="57f2c-112">Można znaleźć w **zapisane zestawów danych** listy na palecie modułów.</span><span class="sxs-lookup"><span data-stu-id="57f2c-112">You can find it in the **Saved Datasets** list in the module palette.</span></span>

