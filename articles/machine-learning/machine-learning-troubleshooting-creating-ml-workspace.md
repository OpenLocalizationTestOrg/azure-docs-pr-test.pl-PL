---
title: "Rozwiązywanie problemów: Utworzyć i nawiązywanie z obszaru roboczego usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Rozwiązania typowych problemów z tworzeniem i nawiązywania połączenia z obszaru roboczego uczenia maszynowego Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 398ac3d9c9d32a1ab10413ce0d7ce8d448890409
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-create-and-connect-to-an-machine-learning-workspace"></a><span data-ttu-id="4d9df-103">Podręcznik rozwiązywania problemów: tworzenie obszaru roboczego usługi Machine Learning i nawiązywanie połączenia z nim</span><span class="sxs-lookup"><span data-stu-id="4d9df-103">Troubleshooting guide: Create and connect to an Machine Learning workspace</span></span>
<span data-ttu-id="4d9df-104">Ten przewodnik zawiera temat rozwiązań dla niektórych często spotykanych problemów podczas konfigurowania obszarów roboczych usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4d9df-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="4d9df-105">Właściciela obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="4d9df-105">Workspace owner</span></span>
<span data-ttu-id="4d9df-106">Aby otworzyć obszar roboczy usługi Machine Learning Studio, użytkownik musi zalogować się Account Microsoft użyty do utworzenia obszaru roboczego lub konieczność odbierania zaproszenia od właściciela do obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="4d9df-106">To open a workspace in Machine Learning Studio, you must be signed in to the Microsoft Account you used to create the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span> <span data-ttu-id="4d9df-107">W portalu Azure można zarządzać obszaru roboczego, który obejmuje możliwość konfigurowania dostępu.</span><span class="sxs-lookup"><span data-stu-id="4d9df-107">From the Azure portal you can manage the workspace, which includes the ability to configure access.</span></span>

<span data-ttu-id="4d9df-108">Aby uzyskać więcej informacji na temat zarządzania obszaru roboczego, zobacz [Zarządzanie obszarem roboczym usługi Azure Machine Learning].</span><span class="sxs-lookup"><span data-stu-id="4d9df-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

<span data-ttu-id="4d9df-109">[Zarządzanie obszarem roboczym usługi Azure Machine Learning]: machine-learning-manage-workspace.md</span><span class="sxs-lookup"><span data-stu-id="4d9df-109">[Manage an Azure Machine Learning workspace]: machine-learning-manage-workspace.md</span></span>

## <a name="allowed-regions"></a><span data-ttu-id="4d9df-110">Dozwolonych regionów</span><span class="sxs-lookup"><span data-stu-id="4d9df-110">Allowed regions</span></span>
<span data-ttu-id="4d9df-111">Usługa Machine Learning jest obecnie dostępna w ograniczonej liczbie regionów.</span><span class="sxs-lookup"><span data-stu-id="4d9df-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="4d9df-112">Jeśli subskrypcja nie zawiera jeden z tych regionów, zobaczysz komunikat o błędzie, "Masz żadnych subskrypcji w dozwolonych regionów."</span><span class="sxs-lookup"><span data-stu-id="4d9df-112">If your subscription does not include one of these regions, you may see the error message, “You have no subscriptions in the allowed regions.”</span></span>

<span data-ttu-id="4d9df-113">Żądanie dodania obszaru do subskrypcji, Utwórz nowe żądanie pomocy technicznej firmy Microsoft z portalu Azure, wybierz **rozliczeń** jako typ problemu i postępuj zgodnie z monitami, aby przesłać żądanie.</span><span class="sxs-lookup"><span data-stu-id="4d9df-113">To request that a region be added to your subscription, create a new Microsoft support request from the Azure portal, choose **Billing** as the problem type, and follow the prompts to submit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="4d9df-114">Konto magazynu</span><span class="sxs-lookup"><span data-stu-id="4d9df-114">Storage account</span></span>
<span data-ttu-id="4d9df-115">Usługa Machine Learning wymaga konta magazynu do przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="4d9df-115">The Machine Learning service needs a storage account to store data.</span></span> <span data-ttu-id="4d9df-116">Można użyć istniejącego konta magazynu, lub można utworzyć nowe konto magazynu, podczas tworzenia nowego obszaru roboczego uczenia maszynowego (jeśli istnieje limit przydziału, aby utworzyć nowe konto magazynu).</span><span class="sxs-lookup"><span data-stu-id="4d9df-116">You can use an existing storage account, or you can create a new storage account when you create the new Machine Learning workspace (if you have quota to create a new storage account).</span></span>

<span data-ttu-id="4d9df-117">Po utworzeniu nowego obszaru roboczego uczenia maszynowego można logowania się do usługi Machine Learning Studio za pomocą konta Microsoft, który został użyty do utworzenia obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="4d9df-117">After the new Machine Learning workspace is created, you can sign in to Machine Learning Studio by using the Microsoft account you used to create the workspace.</span></span> <span data-ttu-id="4d9df-118">Jeśli wystąpią komunikat o błędzie, "Obszaru roboczego nie została odnaleziona" (podobnie jak w poniższym zrzucie ekranu), aby usunąć pliki cookie przeglądarki użyj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="4d9df-118">If you encounter the error message, “Workspace Not Found” (similar to the following screenshot), please use the following steps to delete your browser cookies.</span></span>

![Nie można odnaleźć obszaru roboczego][screen3]

<span data-ttu-id="4d9df-120">**Aby usunąć pliki cookie przeglądarki**</span><span class="sxs-lookup"><span data-stu-id="4d9df-120">**To delete browser cookies**</span></span>

1. <span data-ttu-id="4d9df-121">Jeśli używasz programu Internet Explorer, kliknij przycisk **narzędzia** przycisk w prawym górnym rogu i wybierz **Opcje internetowe**.</span><span class="sxs-lookup"><span data-stu-id="4d9df-121">If you use Internet Explorer, click the **Tools** button in the upper-right corner and select **Internet options**.</span></span>  

![Opcje internetowe][screen4]

2. <span data-ttu-id="4d9df-123">W obszarze **ogólne** , kliknij pozycję **usunąć...**</span><span class="sxs-lookup"><span data-stu-id="4d9df-123">Under the **General** tab, click **Delete…**</span></span>

![Karta Ogólne][screen5]

3. <span data-ttu-id="4d9df-125">W **usuwanie historii przeglądania** okna dialogowego upewnij się, **pliki cookie i dane witryn sieci Web** jest zaznaczone, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="4d9df-125">In the **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![Usuń pliki cookie][screen6]

<span data-ttu-id="4d9df-127">Po usunięciu plików cookie, uruchom ponownie przeglądarkę, a następnie przejdź do [Microsoft Azure Machine Learning](https://studio.azureml.net) strony.</span><span class="sxs-lookup"><span data-stu-id="4d9df-127">After the cookies are deleted, restart the browser and then go to the [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="4d9df-128">Po wyświetleniu monitu o nazwę użytkownika i hasło, wprowadź konto Microsoft, którego użyto do utworzenia obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="4d9df-128">When you are prompted for a user name and password, enter the same Microsoft account you used to create the workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="4d9df-129">Komentarze</span><span class="sxs-lookup"><span data-stu-id="4d9df-129">Comments</span></span>

<span data-ttu-id="4d9df-130">Naszym celem jest zapewnienie środowiska usługi Machine Learning jako bezproblemowe, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="4d9df-130">Our goal is to make the Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="4d9df-131">Opublikuj uwagi i problemy z [forum usługi Azure Machine Learning](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) w celu ułatwienia obsługi można lepiej.</span><span class="sxs-lookup"><span data-stu-id="4d9df-131">Please post any comments and issues at the [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) to help us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
