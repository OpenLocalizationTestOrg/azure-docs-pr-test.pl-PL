---
title: "Krok 1: Tworzenie obszaru roboczego usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Krok 1 opracowanie wskazówki rozwiązanie predykcyjne: Dowiedz się, jak skonfigurować nowy obszar roboczy usługi Azure Machine Learning Studio."
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
ms.openlocfilehash: 8ca42ef8f5314866301f5c9e93caa90dc837a66e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="b3115-103">Przewodnik, krok 1. Tworzenie obszaru roboczego usługi Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b3115-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="b3115-104">Jest to pierwsze tego przewodnika, [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="b3115-104">This is the first step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="b3115-105">**Tworzenie obszaru roboczego usługi Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="b3115-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="b3115-106">Przekazywanie istniejących danych</span><span class="sxs-lookup"><span data-stu-id="b3115-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="b3115-107">Tworzenie nowego eksperymentu</span><span class="sxs-lookup"><span data-stu-id="b3115-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="b3115-108">Nauczanie i ocena modeli</span><span class="sxs-lookup"><span data-stu-id="b3115-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="b3115-109">Wdrażanie usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="b3115-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="b3115-110">Dostęp do usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="b3115-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs to be updated to refer to the new way of creating workspaces in the Ibiza portal -->

<span data-ttu-id="b3115-111">Aby korzystać z usługi Machine Learning Studio, należy mieć obszaru roboczego programu Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="b3115-111">To use Machine Learning Studio, you need to have a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="b3115-112">Ten obszar roboczy zawiera narzędzia potrzebne do tworzenia, zarządzania i opublikować eksperymentów.</span><span class="sxs-lookup"><span data-stu-id="b3115-112">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>  

<!--
## To create a workspace
1. Sign in to the [Azure classic portal](https://manage.windowsazure.com).
2. In the  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On the **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="b3115-113">Administrator dla subskrypcji platformy Azure musi utworzyć obszaru roboczego, a następnie dodać możesz jako właściciela lub współautora.</span><span class="sxs-lookup"><span data-stu-id="b3115-113">The administrator for your Azure subscription needs to create the workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="b3115-114">Aby uzyskać więcej informacji, zobacz [tworzenie i udostępnianie obszaru roboczego uczenia maszynowego Azure](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="b3115-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="b3115-115">Po utworzeniu obszaru roboczego usługi Machine Learning Studio Otwórz ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span><span class="sxs-lookup"><span data-stu-id="b3115-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="b3115-116">Jeśli masz więcej niż jeden obszar roboczy, można wybrać obszar roboczy na pasku narzędzi w prawym górnym rogu okna.</span><span class="sxs-lookup"><span data-stu-id="b3115-116">If you have more than one workspace, you can select the workspace in the toolbar in the upper-right corner of the window.</span></span>

![Wybierz obszar roboczy w Studio][2]

> [!TIP]
> <span data-ttu-id="b3115-118">Jeśli wprowadzono właściciela obszaru roboczego, można udostępniać eksperymentów, nad którymi pracuje przez zapraszanie innych osób do obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="b3115-118">If you were made an owner of the workspace, you can share the experiments you're working on by inviting others to the workspace.</span></span> <span data-ttu-id="b3115-119">Można to zrobić w usłudze Machine Learning Studio na **ustawienia** strony.</span><span class="sxs-lookup"><span data-stu-id="b3115-119">You can do this in Machine Learning Studio on the **SETTINGS** page.</span></span> <span data-ttu-id="b3115-120">Wystarczy konta Microsoft lub konta organizacyjnego dla każdego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b3115-120">You just need the Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="b3115-121">Na **ustawienia** kliknij przycisk **użytkowników**, następnie kliknij przycisk **ZAPROSIĆ użytkowników więcej** w dolnej części okna.</span><span class="sxs-lookup"><span data-stu-id="b3115-121">On the **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at the bottom of the window.</span></span>
> 
> 

- - -
<span data-ttu-id="b3115-122">**Następnie: [przekazywanie istniejących danych](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="b3115-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
