---
title: "aaaImport danych z pliku do usługi Azure Machine Learning Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak plik tooupload dane szkoleniowe tooAzure Twojego dysku twardego Machine Learning Studio. Spowoduje to utworzenie modułu zestawu danych w obszarze roboczym hello."
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
ms.openlocfilehash: 636facd9042145382c953a1c75969149ede6f6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="0f6a7-105">Importowanie danych szkoleniowych z pliku na dysku twardym w usłudze Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="0f6a7-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="0f6a7-106">Dowiedz się, jak tooupload danych plików z toouse Twojego dysku twardego jako danych szkoleniowych w usłudze Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="0f6a7-106">Learn how tooupload a data file from your hard drive toouse as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="0f6a7-107">Importując plik danych hello masz modułu zestawu danych gotowe do użycia w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="0f6a7-107">By importing hello data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-tooimport-data-from-a-local-file"></a><span data-ttu-id="0f6a7-108">Kroki tooimport danych z pliku lokalnego</span><span class="sxs-lookup"><span data-stu-id="0f6a7-108">Steps tooimport data from a local file</span></span>
<span data-ttu-id="0f6a7-109">tooimport danych z lokalnego dysku twardego hello następujące:</span><span class="sxs-lookup"><span data-stu-id="0f6a7-109">tooimport data from a local hard drive, do hello following:</span></span>

1. <span data-ttu-id="0f6a7-110">Kliknij przycisk **+ nowy** u dołu okna Machine Learning Studio hello hello.</span><span class="sxs-lookup"><span data-stu-id="0f6a7-110">Click **+NEW** at hello bottom of hello Machine Learning Studio window.</span></span>
2. <span data-ttu-id="0f6a7-111">Wybierz **DATASET** i **z pliku lokalnego**.</span><span class="sxs-lookup"><span data-stu-id="0f6a7-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="0f6a7-112">W hello **przekazać nowy zestaw danych** okna dialogowego, przeglądania toohello pliku, który chcesz tooupload</span><span class="sxs-lookup"><span data-stu-id="0f6a7-112">In hello **Upload a new dataset** dialog, browse toohello file you want tooupload</span></span>
4. <span data-ttu-id="0f6a7-113">Wprowadź nazwę, identyfikowanie hello typu danych i opcjonalnie wprowadź opis.</span><span class="sxs-lookup"><span data-stu-id="0f6a7-113">Enter a name, identify hello data type, and optionally enter a description.</span></span> <span data-ttu-id="0f6a7-114">Opis jest zalecane — umożliwia toorecord żadnych właściwości hello dane mają tooremember, korzystając z danych hello w przyszłości hello informacje.</span><span class="sxs-lookup"><span data-stu-id="0f6a7-114">A description is recommended - it allows you toorecord any characteristics about hello data that you want tooremember when using hello data in hello future.</span></span>
5. <span data-ttu-id="0f6a7-115">Witaj wyboru **jest nowa wersja istniejący zestaw danych hello** pozwala tooupdate istniejący zestaw danych z nowych danych.</span><span class="sxs-lookup"><span data-stu-id="0f6a7-115">hello checkbox **This is hello new version of an existing dataset** allows you tooupdate an existing dataset with new data.</span></span> <span data-ttu-id="0f6a7-116">Kliknij to pole wyboru, a następnie wprowadź nazwę hello istniejący zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="0f6a7-116">Click this checkbox and then enter hello name of an existing dataset.</span></span>

![Przekaż nowy zestaw danych](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="0f6a7-118">Podczas przekazywania zobaczysz komunikat jest przekazywanego pliku.</span><span class="sxs-lookup"><span data-stu-id="0f6a7-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="0f6a7-119">Przekaż czas zależy od rozmiaru hello szybkości danych i hello usługi toohello połączenia.</span><span class="sxs-lookup"><span data-stu-id="0f6a7-119">Upload time depends on hello size of your data and hello speed of your connection toohello service.</span></span> <span data-ttu-id="0f6a7-120">Jeśli wiesz, że plik hello potrwa długo, można wykonać inne czynności w usłudze Machine Learning Studio, podczas oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="0f6a7-120">If you know hello file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="0f6a7-121">Powoduje zamknięcie przeglądarki hello jednak toofail przekazywania danych hello.</span><span class="sxs-lookup"><span data-stu-id="0f6a7-121">However, closing hello browser causes hello data upload toofail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="0f6a7-122">Moduł zestawu danych jest gotowy do użycia</span><span class="sxs-lookup"><span data-stu-id="0f6a7-122">Dataset module is ready for use</span></span>
<span data-ttu-id="0f6a7-123">Po przekazaniu plików dane są przechowywane w module zestawu danych i jest dostępne tooany eksperymentu w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="0f6a7-123">Once your data is uploaded, it's stored in a dataset module and is available tooany experiment in your workspace.</span></span>

<span data-ttu-id="0f6a7-124">Podczas edycji eksperyment, można znaleźć hello zestawy danych po utworzeniu hello **Moje zestawów danych** liście hello **zapisane zestawów danych** listy hello modułu palety.</span><span class="sxs-lookup"><span data-stu-id="0f6a7-124">When you're editing an experiment, you can find hello datasets you've created in hello **My Datasets** list under hello **Saved Datasets** list in hello module palette.</span></span> <span data-ttu-id="0f6a7-125">Możesz przeciągać i upuszczać dataset hello na kanwie eksperymentu hello należy toouse hello dataset do dalszej analizy i uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="0f6a7-125">You can drag and drop hello dataset onto hello experiment canvas when you want toouse hello dataset for further analytics and machine learning.</span></span>
