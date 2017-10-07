---
title: "Rozwiązywanie problemów z: Tworzenie i łączenie obszaru roboczego uczenia maszynowego tooa | Dokumentacja firmy Microsoft"
description: "Rozwiązania typowych problemów z tworzeniem i łączenie obszaru roboczego uczenia maszynowego Azure tooan"
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
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a><span data-ttu-id="e9592-103">Przewodnik rozwiązywania problemów: tworzenie i łączenie tooan obszaru roboczego uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="e9592-103">Troubleshooting guide: Create and connect tooan Machine Learning workspace</span></span>
<span data-ttu-id="e9592-104">Ten przewodnik zawiera temat rozwiązań dla niektórych często spotykanych problemów podczas konfigurowania obszarów roboczych usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e9592-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="e9592-105">Właściciela obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="e9592-105">Workspace owner</span></span>
<span data-ttu-id="e9592-106">tooopen obszaru roboczego w usłudze Machine Learning Studio, musi być zalogowany toohello Account Microsoft użyć obszaru roboczego hello toocreate lub należy tooreceive zaproszenia od hello właściciela toojoin hello roboczym.</span><span class="sxs-lookup"><span data-stu-id="e9592-106">tooopen a workspace in Machine Learning Studio, you must be signed in toohello Microsoft Account you used toocreate hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span> <span data-ttu-id="e9592-107">Z portalu Azure, którymi można zarządzać hello hello obszaru roboczego, w tym hello możliwości tooconfigure dostępu.</span><span class="sxs-lookup"><span data-stu-id="e9592-107">From hello Azure portal you can manage hello workspace, which includes hello ability tooconfigure access.</span></span>

<span data-ttu-id="e9592-108">Aby uzyskać więcej informacji na temat zarządzania obszaru roboczego, zobacz [Zarządzanie obszarem roboczym usługi Azure Machine Learning].</span><span class="sxs-lookup"><span data-stu-id="e9592-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

[Zarządzanie obszarem roboczym usługi Azure Machine Learning]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a><span data-ttu-id="e9592-110">Dozwolonych regionów</span><span class="sxs-lookup"><span data-stu-id="e9592-110">Allowed regions</span></span>
<span data-ttu-id="e9592-111">Usługa Machine Learning jest obecnie dostępna w ograniczonej liczbie regionów.</span><span class="sxs-lookup"><span data-stu-id="e9592-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="e9592-112">Jeśli subskrypcja nie zawiera jeden z tych regionów, może zostać wyświetlony komunikat błędu Witaj, "Masz żadnych subskrypcji w hello dozwolone regiony."</span><span class="sxs-lookup"><span data-stu-id="e9592-112">If your subscription does not include one of these regions, you may see hello error message, “You have no subscriptions in hello allowed regions.”</span></span>

<span data-ttu-id="e9592-113">toorequest, który region można dodać subskrypcji tooyour, Utwórz nowe żądanie pomocy technicznej firmy Microsoft z hello portalu Azure, wybierz **rozliczeń** jako typ problemu hello i wykonaj hello monituje toosubmit Twojego żądania.</span><span class="sxs-lookup"><span data-stu-id="e9592-113">toorequest that a region be added tooyour subscription, create a new Microsoft support request from hello Azure portal, choose **Billing** as hello problem type, and follow hello prompts toosubmit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="e9592-114">Konto magazynu</span><span class="sxs-lookup"><span data-stu-id="e9592-114">Storage account</span></span>
<span data-ttu-id="e9592-115">Witaj usługi Machine Learning musi toostore konta magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="e9592-115">hello Machine Learning service needs a storage account toostore data.</span></span> <span data-ttu-id="e9592-116">Można użyć istniejącego konta magazynu, lub można utworzyć nowe konto magazynu podczas tworzenia obszaru roboczego uczenia maszynowego nowe hello (Jeśli masz toocreate przydziału nowego konta magazynu).</span><span class="sxs-lookup"><span data-stu-id="e9592-116">You can use an existing storage account, or you can create a new storage account when you create hello new Machine Learning workspace (if you have quota toocreate a new storage account).</span></span>

<span data-ttu-id="e9592-117">Po utworzeniu obszaru roboczego uczenia maszynowego nowe hello tooMachine Learning Studio można zaloguj przy użyciu konta Microsoft hello używanych toocreate hello roboczym.</span><span class="sxs-lookup"><span data-stu-id="e9592-117">After hello new Machine Learning workspace is created, you can sign in tooMachine Learning Studio by using hello Microsoft account you used toocreate hello workspace.</span></span> <span data-ttu-id="e9592-118">Jeśli wystąpią komunikat o błędzie hello "Obszaru roboczego nie została odnaleziona" (podobne toohello po zrzut ekranu), użyj hello następujące kroki toodelete pliki cookie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="e9592-118">If you encounter hello error message, “Workspace Not Found” (similar toohello following screenshot), please use hello following steps toodelete your browser cookies.</span></span>

![Nie można odnaleźć obszaru roboczego][screen3]

<span data-ttu-id="e9592-120">**pliki cookie przeglądarki toodelete**</span><span class="sxs-lookup"><span data-stu-id="e9592-120">**toodelete browser cookies**</span></span>

1. <span data-ttu-id="e9592-121">Jeśli używasz programu Internet Explorer, kliknij przycisk hello **narzędzia** w prawym górnym rogu hello i wybrać **Opcje internetowe**.</span><span class="sxs-lookup"><span data-stu-id="e9592-121">If you use Internet Explorer, click hello **Tools** button in hello upper-right corner and select **Internet options**.</span></span>  

![Opcje internetowe][screen4]

2. <span data-ttu-id="e9592-123">W obszarze hello **ogólne** , kliknij pozycję **usunąć...**</span><span class="sxs-lookup"><span data-stu-id="e9592-123">Under hello **General** tab, click **Delete…**</span></span>

![Karta Ogólne][screen5]

3. <span data-ttu-id="e9592-125">W hello **usuwanie historii przeglądania** okna dialogowego upewnij się, **pliki cookie i dane witryn sieci Web** jest zaznaczone, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="e9592-125">In hello **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![Usuń pliki cookie][screen6]

<span data-ttu-id="e9592-127">Po usunięciu plików cookie hello ponowne uruchomienie hello przeglądarki, a następnie przejdź toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) strony.</span><span class="sxs-lookup"><span data-stu-id="e9592-127">After hello cookies are deleted, restart hello browser and then go toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="e9592-128">Gdy zostanie wyświetlony monit o nazwę użytkownika i hasło, wprowadź hello tego samego konta Microsoft użyty toocreate hello roboczym.</span><span class="sxs-lookup"><span data-stu-id="e9592-128">When you are prompted for a user name and password, enter hello same Microsoft account you used toocreate hello workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="e9592-129">Komentarze</span><span class="sxs-lookup"><span data-stu-id="e9592-129">Comments</span></span>

<span data-ttu-id="e9592-130">Naszym celem jest toomake hello środowiska usługi Machine Learning jako bezproblemowe, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="e9592-130">Our goal is toomake hello Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="e9592-131">Opublikuj uwagi i problemy na powitania [forum usługi Azure Machine Learning](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp nam będą one lepsze.</span><span class="sxs-lookup"><span data-stu-id="e9592-131">Please post any comments and issues at hello [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
