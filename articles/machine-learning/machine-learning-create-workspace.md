---
title: "aaaCreate obszaru roboczego usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Jak toocreate obszaru roboczego dla usługi Azure Machine Learning Studio"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="3043d-103">Tworzenie obszaru roboczego usługi Azure Machine Learning i zarządzanie nim</span><span class="sxs-lookup"><span data-stu-id="3043d-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="3043d-104">W tym menu łączy tootopics, które opisują sposób tooset się hello różnych środowiskach nauki danych przez hello Cortana Analytics procesu (CAP).</span><span class="sxs-lookup"><span data-stu-id="3043d-104">This menu links tootopics that describe how tooset up hello various data science environments used by hello Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="3043d-105">toouse Azure Machine Learning Studio, należy toohave obszaru roboczego uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="3043d-105">toouse Azure Machine Learning Studio, you need toohave a Machine Learning workspace.</span></span> <span data-ttu-id="3043d-106">Ten obszar roboczy zawiera narzędzia hello należy toocreate, zarządzania i publikowania eksperymentów.</span><span class="sxs-lookup"><span data-stu-id="3043d-106">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a><span data-ttu-id="3043d-107">toocreate obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="3043d-107">toocreate a workspace</span></span>
1. <span data-ttu-id="3043d-108">Zaloguj się toohello [portalu Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="3043d-108">Sign in toohello [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="3043d-109">toosign w i tworzenie obszaru roboczego, należy toobe administratorem subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3043d-109">toosign in and create a workspace, you need toobe an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="3043d-110">Kliknij przycisk **+ nowy**</span><span class="sxs-lookup"><span data-stu-id="3043d-110">Click **+New**</span></span>

3. <span data-ttu-id="3043d-111">Wybierz **analizy i analiza**, kliknij przycisk **obszaru roboczego uczenia maszyny**, następnie kliknij przycisk **Utwórz**</span><span class="sxs-lookup"><span data-stu-id="3043d-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="3043d-112">Wprowadź informacje obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="3043d-112">Enter your workspace information</span></span>

    - <span data-ttu-id="3043d-113">Witaj *nazwa obszaru roboczego* może być aktywne too260 znaków, nie kończy się spacją.</span><span class="sxs-lookup"><span data-stu-id="3043d-113">hello *workspace name* may be up too260 characters, not ending in a space.</span></span> <span data-ttu-id="3043d-114">Witaj, nazwa nie może zawierać następujących znaków:`< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="3043d-114">hello name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="3043d-115">Witaj *plan usługi sieci web* możesz wybrać (lub Utwórz), wraz z hello skojarzone *warstwy cenowej* wybrać, jest używany w przypadku wdrożenia usługi sieci web z obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="3043d-115">hello *web service plan* you choose (or create), along with hello associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![Tworzenie nowego obszaru roboczego](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="3043d-117">Kliknij przycisk **Utwórz**</span><span class="sxs-lookup"><span data-stu-id="3043d-117">Click **Create**</span></span>

<span data-ttu-id="3043d-118">Po wdrożeniu hello obszaru roboczego można otworzyć go w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="3043d-118">Once hello workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="3043d-119">Przeglądaj tooMachine Learning Studio w [https://studio.azureml.net/](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="3043d-119">Browse tooMachine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="3043d-120">Wybierz obszar roboczy w hello prawej górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="3043d-120">Select your workspace in hello upper-right-hand corner.</span></span>

    ![Wybierz obszar roboczy](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="3043d-122">Kliknij przycisk **eksperymenty**.</span><span class="sxs-lookup"><span data-stu-id="3043d-122">Click **my experiments**.</span></span>

    ![Otwórz eksperymenty](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="3043d-124">Informacje o zarządzaniu obszaru roboczego, zobacz [Zarządzanie obszarem roboczym usługi Azure Machine Learning](machine-learning-manage-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="3043d-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="3043d-125">Jeśli napotkasz problem podczas tworzenia obszaru roboczego, zobacz [przewodnik rozwiązywania problemów: tworzenie i łączenie obszaru roboczego uczenia maszynowego tooa](machine-learning-troubleshooting-creating-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="3043d-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect tooa Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="3043d-126">Udostępnianie obszaru roboczego uczenia maszynowego Azure</span><span class="sxs-lookup"><span data-stu-id="3043d-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="3043d-127">Po utworzeniu obszaru roboczego uczenia maszynowego można zaprosić użytkowników tooyour obszaru roboczego tooshare dostępu tooyour roboczym i wszystkie jego eksperymentów, zestawy danych, notesy itp. Można dodać użytkowników, w jednym z dwóch ról:</span><span class="sxs-lookup"><span data-stu-id="3043d-127">Once a Machine Learning workspace is created, you can invite users tooyour workspace tooshare access tooyour workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="3043d-128">**Użytkownik** -użytkownika obszar roboczy można utworzyć, Otwórz, zmodyfikuj i Usuń eksperymentów, zestawy danych itp., w obszarze roboczym hello.</span><span class="sxs-lookup"><span data-stu-id="3043d-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in hello workspace.</span></span>
* <span data-ttu-id="3043d-129">**Właściciel** — poprosić właściciela i usuwać użytkowników w obszarze roboczym hello toowhat dodanie użytkownika mogą wykonywać.</span><span class="sxs-lookup"><span data-stu-id="3043d-129">**Owner** - An owner can invite and remove users in hello workspace, in addition toowhat a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="3043d-130">konto administratora Hello tworzy hello obszaru roboczego jest automatycznie dodawany toohello obszaru roboczego jako właściciela obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="3043d-130">hello administrator account that creates hello workspace is automatically added toohello workspace as workspace Owner.</span></span> <span data-ttu-id="3043d-131">Jednak innych administratorów lub użytkowników w tej subskrypcji nie są automatycznie udzielony dostęp roboczym toohello — należy tooinvite je jawnie.</span><span class="sxs-lookup"><span data-stu-id="3043d-131">However, other administrators or users in that subscription are not automatically granted access toohello workspace - you need tooinvite them explicitly.</span></span>
> 
> 

### <a name="tooshare-a-workspace"></a><span data-ttu-id="3043d-132">tooshare obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="3043d-132">tooshare a workspace</span></span>

1. <span data-ttu-id="3043d-133">Zaloguj się tooMachine Learning Studio w [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span><span class="sxs-lookup"><span data-stu-id="3043d-133">Sign in tooMachine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="3043d-134">W lewym panelu powitania kliknij **ustawienia**</span><span class="sxs-lookup"><span data-stu-id="3043d-134">In hello left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="3043d-135">Kliknij przycisk hello **użytkowników** kartę</span><span class="sxs-lookup"><span data-stu-id="3043d-135">Click hello **USERS** tab</span></span>

4. <span data-ttu-id="3043d-136">Kliknij przycisk **ZAPROSIĆ użytkowników więcej** u dołu hello hello strony</span><span class="sxs-lookup"><span data-stu-id="3043d-136">Click **INVITE MORE USERS** at hello bottom of hello page</span></span>

    ![Ustawienia Studio](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="3043d-138">Wprowadź co najmniej jeden adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="3043d-138">Enter one or more email addresses.</span></span> <span data-ttu-id="3043d-139">Hello wymaga prawidłowego konta Microsoft lub konta organizacyjnego (z usługą Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3043d-139">hello users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="3043d-140">Wybierz, czy użytkownicy hello tooadd jako właściciela lub użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3043d-140">Select whether you want tooadd hello users as Owner or User.</span></span>

7. <span data-ttu-id="3043d-141">Kliknij przycisk hello **OK** przycisk znacznika wyboru.</span><span class="sxs-lookup"><span data-stu-id="3043d-141">Click hello **OK** checkmark button.</span></span>

<span data-ttu-id="3043d-142">Każdy użytkownik dodawany otrzymają wiadomość e-mail z instrukcjami dotyczącymi sposobu toosign w toohello udostępniony obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="3043d-142">Each user you add will receive an email with instructions on how toosign in toohello shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="3043d-143">Dla toodeploy stanie toobe użytkowników lub zarządzania usługami sieci web, w tym obszarze roboczym, muszą być współautora lub administratora w hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3043d-143">For users toobe able toodeploy or manage web services in this workspace, they must be a contributor or administrator in hello Azure subscription.</span></span> 



