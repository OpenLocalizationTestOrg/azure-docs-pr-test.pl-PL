---
title: "Tworzenie obszaru roboczego usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Tworzenie obszaru roboczego dla usługi Azure Machine Learning Studio"
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
ms.openlocfilehash: 182a34822e71d63f4d7229548ae3f59d9f195337
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="6caa1-103">Tworzenie obszaru roboczego usługi Azure Machine Learning i zarządzanie nim</span><span class="sxs-lookup"><span data-stu-id="6caa1-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="6caa1-104">To menu łącza do tematów opisujących sposób konfigurowania różnych środowiskach nauki danych używany przez proces Analytics Cortana (CAP).</span><span class="sxs-lookup"><span data-stu-id="6caa1-104">This menu links to topics that describe how to set up the various data science environments used by the Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="6caa1-105">Aby korzystać z usługi Azure Machine Learning Studio, musisz mieć obszaru roboczego uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="6caa1-105">To use Azure Machine Learning Studio, you need to have a Machine Learning workspace.</span></span> <span data-ttu-id="6caa1-106">Ten obszar roboczy zawiera narzędzia potrzebne do tworzenia, zarządzania i opublikować eksperymentów.</span><span class="sxs-lookup"><span data-stu-id="6caa1-106">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="to-create-a-workspace"></a><span data-ttu-id="6caa1-107">Aby utworzyć obszar roboczy</span><span class="sxs-lookup"><span data-stu-id="6caa1-107">To create a workspace</span></span>
1. <span data-ttu-id="6caa1-108">Zaloguj się do [portalu Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="6caa1-108">Sign in to the [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="6caa1-109">Zalogować się i utworzyć obszaru roboczego, musisz być administratorem subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6caa1-109">To sign in and create a workspace, you need to be an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="6caa1-110">Kliknij przycisk **+ nowy**</span><span class="sxs-lookup"><span data-stu-id="6caa1-110">Click **+New**</span></span>

3. <span data-ttu-id="6caa1-111">Wybierz **analizy i analiza**, kliknij przycisk **obszaru roboczego uczenia maszyny**, następnie kliknij przycisk **Utwórz**</span><span class="sxs-lookup"><span data-stu-id="6caa1-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="6caa1-112">Wprowadź informacje obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="6caa1-112">Enter your workspace information</span></span>

    - <span data-ttu-id="6caa1-113">*Nazwa obszaru roboczego* może mieć maksymalnie 260 znaków, nie kończy się spacją.</span><span class="sxs-lookup"><span data-stu-id="6caa1-113">The *workspace name* may be up to 260 characters, not ending in a space.</span></span> <span data-ttu-id="6caa1-114">Nazwa nie może zawierać następujących znaków:`< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="6caa1-114">The name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="6caa1-115">*Plan usługi sieci web* możesz wybrać (lub Utwórz), oraz skojarzone *warstwy cenowej* wybrać, jest używany w przypadku wdrożenia usługi sieci web z obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="6caa1-115">The *web service plan* you choose (or create), along with the associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![Tworzenie nowego obszaru roboczego](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="6caa1-117">Kliknij przycisk **Utwórz**</span><span class="sxs-lookup"><span data-stu-id="6caa1-117">Click **Create**</span></span>

<span data-ttu-id="6caa1-118">Po wdrożeniu obszaru roboczego, możesz otworzyć go w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="6caa1-118">Once the workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="6caa1-119">Przejdź do usługi Machine Learning Studio w [https://studio.azureml.net/](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="6caa1-119">Browse to Machine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="6caa1-120">Wybierz obszar roboczy w prawej górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="6caa1-120">Select your workspace in the upper-right-hand corner.</span></span>

    ![Wybierz obszar roboczy](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="6caa1-122">Kliknij przycisk **eksperymenty**.</span><span class="sxs-lookup"><span data-stu-id="6caa1-122">Click **my experiments**.</span></span>

    ![Otwórz eksperymenty](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="6caa1-124">Informacje o zarządzaniu obszaru roboczego, zobacz [Zarządzanie obszarem roboczym usługi Azure Machine Learning](machine-learning-manage-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="6caa1-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="6caa1-125">Jeśli napotkasz problem podczas tworzenia obszaru roboczego, zobacz [przewodnik rozwiązywania problemów: utworzyć i nawiązywanie z obszaru roboczego uczenia maszynowego](machine-learning-troubleshooting-creating-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="6caa1-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect to a Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="6caa1-126">Udostępnianie obszaru roboczego uczenia maszynowego Azure</span><span class="sxs-lookup"><span data-stu-id="6caa1-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="6caa1-127">Po utworzeniu obszaru roboczego uczenia maszynowego, można zaprosić użytkowników do swojego obszaru roboczego można udzielać dostępu do swojego obszaru roboczego i wszystkie jego eksperymentów, zestawy danych, notesy itp. Można dodać użytkowników, w jednym z dwóch ról:</span><span class="sxs-lookup"><span data-stu-id="6caa1-127">Once a Machine Learning workspace is created, you can invite users to your workspace to share access to your workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="6caa1-128">**Użytkownik** -użytkownika obszar roboczy można utworzyć, Otwórz, zmodyfikuj i Usuń eksperymentów, zestawy danych itp., w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="6caa1-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in the workspace.</span></span>
* <span data-ttu-id="6caa1-129">**Właściciel** — poprosić właściciela i usuwać użytkowników w obszarze roboczym, oprócz jakie użytkownika mogą wykonywać.</span><span class="sxs-lookup"><span data-stu-id="6caa1-129">**Owner** - An owner can invite and remove users in the workspace, in addition to what a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="6caa1-130">Konto administratora, które tworzy obszaru roboczego jest automatycznie dodawany do obszaru roboczego jako właściciela obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="6caa1-130">The administrator account that creates the workspace is automatically added to the workspace as workspace Owner.</span></span> <span data-ttu-id="6caa1-131">Jednak innych administratorów lub użytkowników w tej subskrypcji nie automatycznie otrzymują dostęp do obszaru roboczego — należy je jawnie zaprosić.</span><span class="sxs-lookup"><span data-stu-id="6caa1-131">However, other administrators or users in that subscription are not automatically granted access to the workspace - you need to invite them explicitly.</span></span>
> 
> 

### <a name="to-share-a-workspace"></a><span data-ttu-id="6caa1-132">Aby udostępnić obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="6caa1-132">To share a workspace</span></span>

1. <span data-ttu-id="6caa1-133">Zaloguj się do usługi Machine Learning Studio w [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span><span class="sxs-lookup"><span data-stu-id="6caa1-133">Sign in to Machine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="6caa1-134">W lewym panelu kliknij **ustawienia**</span><span class="sxs-lookup"><span data-stu-id="6caa1-134">In the left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="6caa1-135">Kliknij przycisk **użytkowników** kartę</span><span class="sxs-lookup"><span data-stu-id="6caa1-135">Click the **USERS** tab</span></span>

4. <span data-ttu-id="6caa1-136">Kliknij przycisk **ZAPROSIĆ użytkowników więcej** w dolnej części strony</span><span class="sxs-lookup"><span data-stu-id="6caa1-136">Click **INVITE MORE USERS** at the bottom of the page</span></span>

    ![Ustawienia Studio](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="6caa1-138">Wprowadź co najmniej jeden adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="6caa1-138">Enter one or more email addresses.</span></span> <span data-ttu-id="6caa1-139">Użytkownicy muszą prawidłowego konta Microsoft lub konta organizacyjnego (z usługą Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="6caa1-139">The users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="6caa1-140">Określ, czy chcesz dodać użytkowników jako właściciela lub użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6caa1-140">Select whether you want to add the users as Owner or User.</span></span>

7. <span data-ttu-id="6caa1-141">Kliknij przycisk **OK** przycisk znacznika wyboru.</span><span class="sxs-lookup"><span data-stu-id="6caa1-141">Click the **OK** checkmark button.</span></span>

<span data-ttu-id="6caa1-142">Każdy użytkownik dodawany otrzymają wiadomość e-mail z instrukcjami dotyczącymi sposobu Zaloguj się do udostępnionego obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="6caa1-142">Each user you add will receive an email with instructions on how to sign in to the shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="6caa1-143">Aby umożliwić użytkownikom możliwość wdrażania i zarządzania usługami sieci web, w tym obszarze roboczym musi być współautora lub administrator w subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6caa1-143">For users to be able to deploy or manage web services in this workspace, they must be a contributor or administrator in the Azure subscription.</span></span> 



