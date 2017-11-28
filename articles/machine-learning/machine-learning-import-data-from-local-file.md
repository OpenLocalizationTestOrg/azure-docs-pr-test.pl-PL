---
title: "Importowanie danych z pliku do usługi Azure Machine Learning Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak można przekazać pliku danych szkoleniowych z dysku twardego do usługi Azure Machine Learning Studio. Spowoduje to utworzenie modułu zestawu danych w obszarze roboczym."
keywords: "Importowanie danych, formatu danych, typy danych, źródła danych, dane szkoleniowe"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: c0dd9e90-23c4-4f64-8b8f-489ad79f047b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: 18010864160ceb2d76aea37196e6944bbe426457
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="9a9a0-105">Importowanie danych szkoleniowych z pliku na dysku twardym w usłudze Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="9a9a0-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="9a9a0-106">Dowiedz się, jak można przekazać plik danych z dysku twardego do użycia jako danych szkoleniowych w usłudze Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="9a9a0-106">Learn how to upload a data file from your hard drive to use as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="9a9a0-107">Przez zaimportowanie pliku danych, masz modułu zestawu danych gotowe do użycia w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="9a9a0-107">By importing the data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-to-import-data-from-a-local-file"></a><span data-ttu-id="9a9a0-108">Kroki w celu importowania danych z pliku lokalnego</span><span class="sxs-lookup"><span data-stu-id="9a9a0-108">Steps to import data from a local file</span></span>
<span data-ttu-id="9a9a0-109">Importowanie danych z lokalnego dysku twardego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9a9a0-109">To import data from a local hard drive, do the following:</span></span>

1. <span data-ttu-id="9a9a0-110">Kliknij przycisk **+ nowy** u dołu okna Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="9a9a0-110">Click **+NEW** at the bottom of the Machine Learning Studio window.</span></span>
2. <span data-ttu-id="9a9a0-111">Wybierz **DATASET** i **z pliku lokalnego**.</span><span class="sxs-lookup"><span data-stu-id="9a9a0-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="9a9a0-112">W **przekazać nowy zestaw danych** okno dialogowe, przejdź do pliku, który chcesz przekazać</span><span class="sxs-lookup"><span data-stu-id="9a9a0-112">In the **Upload a new dataset** dialog, browse to the file you want to upload</span></span>
4. <span data-ttu-id="9a9a0-113">Wprowadź nazwę, określ typ danych i opcjonalnie wprowadź opis.</span><span class="sxs-lookup"><span data-stu-id="9a9a0-113">Enter a name, identify the data type, and optionally enter a description.</span></span> <span data-ttu-id="9a9a0-114">Opis jest zalecane — umożliwia zarejestrowanie żadnych właściwości o danych, które chcesz Pamiętaj przy użyciu danych w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="9a9a0-114">A description is recommended - it allows you to record any characteristics about the data that you want to remember when using the data in the future.</span></span>
5. <span data-ttu-id="9a9a0-115">Pole wyboru **jest nowa wersja istniejący zestaw danych** pozwala zaktualizować istniejący zestaw danych o nowych danych.</span><span class="sxs-lookup"><span data-stu-id="9a9a0-115">The checkbox **This is the new version of an existing dataset** allows you to update an existing dataset with new data.</span></span> <span data-ttu-id="9a9a0-116">Kliknij to pole wyboru, a następnie wprowadź nazwę istniejącego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="9a9a0-116">Click this checkbox and then enter the name of an existing dataset.</span></span>

![Przekaż nowy zestaw danych](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="9a9a0-118">Podczas przekazywania zobaczysz komunikat jest przekazywanego pliku.</span><span class="sxs-lookup"><span data-stu-id="9a9a0-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="9a9a0-119">Przekaż czas zależy od rozmiaru danych i prędkości połączenia z usługą.</span><span class="sxs-lookup"><span data-stu-id="9a9a0-119">Upload time depends on the size of your data and the speed of your connection to the service.</span></span> <span data-ttu-id="9a9a0-120">Jeśli wiesz, że plik zostanie zająć dużo czasu, można wykonać inne czynności w usłudze Machine Learning Studio, podczas oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="9a9a0-120">If you know the file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="9a9a0-121">Powoduje zamknięcie przeglądarki jednak przekazywania danych zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="9a9a0-121">However, closing the browser causes the data upload to fail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="9a9a0-122">Moduł zestawu danych jest gotowy do użycia</span><span class="sxs-lookup"><span data-stu-id="9a9a0-122">Dataset module is ready for use</span></span>
<span data-ttu-id="9a9a0-123">Po przekazaniu plików dane są przechowywane w module zestawu danych i jest dostępny dla każdego doświadczenia w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="9a9a0-123">Once your data is uploaded, it's stored in a dataset module and is available to any experiment in your workspace.</span></span>

<span data-ttu-id="9a9a0-124">Podczas edycji eksperyment, można znaleźć zestawy danych zostały utworzone w **Moje zestawów danych** w obszarze **zapisane zestawów danych** listy na palecie modułów.</span><span class="sxs-lookup"><span data-stu-id="9a9a0-124">When you're editing an experiment, you can find the datasets you've created in the **My Datasets** list under the **Saved Datasets** list in the module palette.</span></span> <span data-ttu-id="9a9a0-125">Możesz przeciągać i upuszczać zestawu danych do obszaru roboczego eksperymentu, jeśli chcesz używać zestawu danych do dalszej analizy i uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="9a9a0-125">You can drag and drop the dataset onto the experiment canvas when you want to use the dataset for further analytics and machine learning.</span></span>
