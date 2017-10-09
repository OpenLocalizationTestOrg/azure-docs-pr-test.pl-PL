---
title: "Krok 1: Tworzenie obszaru roboczego usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Krok 1 hello opracowanie wskazówki rozwiązanie predykcyjne: Dowiedz się, jak tooset się nowy obszar roboczy usługi Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b3c97e3d-16ba-4e42-9657-2562854a1e04
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 93d2e240826db9768e85b00cab0eb62510b4efb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="a68f2-103">Przewodnik, krok 1. Tworzenie obszaru roboczego usługi Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a68f2-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="a68f2-104">To jest pierwszy etap wskazówki hello hello [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="a68f2-104">This is hello first step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="a68f2-105">**Tworzenie obszaru roboczego usługi Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="a68f2-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="a68f2-106">Przekazywanie istniejących danych</span><span class="sxs-lookup"><span data-stu-id="a68f2-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="a68f2-107">Tworzenie nowego eksperymentu</span><span class="sxs-lookup"><span data-stu-id="a68f2-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="a68f2-108">Nauczanie i Ewaluacja modeli hello</span><span class="sxs-lookup"><span data-stu-id="a68f2-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="a68f2-109">Wdrażanie usługi sieci Web hello</span><span class="sxs-lookup"><span data-stu-id="a68f2-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="a68f2-110">Witaj dostępu do usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="a68f2-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs toobe updated toorefer toohello new way of creating workspaces in hello Ibiza portal -->

<span data-ttu-id="a68f2-111">toouse Machine Learning Studio, należy toohave obszaru roboczego programu Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="a68f2-111">toouse Machine Learning Studio, you need toohave a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="a68f2-112">Ten obszar roboczy zawiera narzędzia hello należy toocreate, zarządzania i publikowania eksperymentów.</span><span class="sxs-lookup"><span data-stu-id="a68f2-112">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>  

<!--
## toocreate a workspace
1. Sign in toohello [Azure classic portal](https://manage.windowsazure.com).
2. In hello  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On hello **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="a68f2-113">Hello administratora dla subskrypcji platformy Azure musi toocreate hello roboczym, a następnie dodaj możesz jako właściciela lub współautora.</span><span class="sxs-lookup"><span data-stu-id="a68f2-113">hello administrator for your Azure subscription needs toocreate hello workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="a68f2-114">Aby uzyskać więcej informacji, zobacz [tworzenie i udostępnianie obszaru roboczego uczenia maszynowego Azure](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="a68f2-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="a68f2-115">Po utworzeniu obszaru roboczego usługi Machine Learning Studio Otwórz ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span><span class="sxs-lookup"><span data-stu-id="a68f2-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="a68f2-116">Jeśli masz więcej niż jeden obszar roboczy, można wybrać obszar roboczy hello na powitania narzędzi w hello prawym górnym rogu okna hello.</span><span class="sxs-lookup"><span data-stu-id="a68f2-116">If you have more than one workspace, you can select hello workspace in hello toolbar in hello upper-right corner of hello window.</span></span>

![Wybierz obszar roboczy w Studio][2]

> [!TIP]
> <span data-ttu-id="a68f2-118">Jeśli wprowadzono właściciela obszaru roboczego hello, można udostępniać eksperymenty hello pracy przez zapraszanie innych toohello obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="a68f2-118">If you were made an owner of hello workspace, you can share hello experiments you're working on by inviting others toohello workspace.</span></span> <span data-ttu-id="a68f2-119">Można to zrobić w usłudze Machine Learning Studio na powitania **ustawienia** strony.</span><span class="sxs-lookup"><span data-stu-id="a68f2-119">You can do this in Machine Learning Studio on hello **SETTINGS** page.</span></span> <span data-ttu-id="a68f2-120">Wystarczy hello konta Microsoft lub konta organizacyjnego dla każdego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a68f2-120">You just need hello Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="a68f2-121">Na powitania **ustawienia** kliknij przycisk **użytkowników**, następnie kliknij przycisk **ZAPROSIĆ użytkowników więcej** u dołu okna hello hello.</span><span class="sxs-lookup"><span data-stu-id="a68f2-121">On hello **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at hello bottom of hello window.</span></span>
> 
> 

- - -
<span data-ttu-id="a68f2-122">**Następnie: [przekazywanie istniejących danych](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="a68f2-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
