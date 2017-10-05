---
title: "Dodawanie magazynu Azure za pomocą usług połączonych w programie Visual Studio | Dokumentacja firmy Microsoft"
description: "Dodawanie magazynu Azure do aplikacji przy użyciu okna dialogowego programu Visual Studio Dodaj połączone usługi"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 35638083cd75e1b751d00a9c8163a3bc7480f0cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="35ff6-103">Dodawanie magazynu platformy Azure przy użyciu programu Visual Studio usługami</span><span class="sxs-lookup"><span data-stu-id="35ff6-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="35ff6-104">Przy użyciu programu Visual Studio możesz można nawiązać żadnego z następujących usługi Azure Storage za pomocą **dodać usług połączonych** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="35ff6-104">With Visual Studio, you can connect any of the following to Azure Storage by using the **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="35ff6-105">Usługi w chmurze C#</span><span class="sxs-lookup"><span data-stu-id="35ff6-105">C# cloud service</span></span>
- <span data-ttu-id="35ff6-106">Usługi mobilnej zaplecza .NET</span><span class="sxs-lookup"><span data-stu-id="35ff6-106">.NET backend mobile service</span></span>
- <span data-ttu-id="35ff6-107">Witryny sieci Web ASP.NET lub usługi</span><span class="sxs-lookup"><span data-stu-id="35ff6-107">ASP.NET website or service</span></span>
- <span data-ttu-id="35ff6-108">Usługi platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="35ff6-108">ASP.NET Core service</span></span>
- <span data-ttu-id="35ff6-109">Usługa zadań WebJob Azure</span><span class="sxs-lookup"><span data-stu-id="35ff6-109">Azure WebJob service</span></span> 

<span data-ttu-id="35ff6-110">Funkcja podłączonej usługi dodaje wszystkie niezbędne odwołania i kod połączenia do projektu i odpowiednio modyfikuje plików konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="35ff6-110">The connected service functionality adds all the needed references and connection code to your project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="35ff6-111">Po zakończeniu **dodać usług połączonych** okno dialogowe automatycznie wyświetla dokumentacji wyszczególnieniem kroków wymaganych do rozpoczęcia pracy z magazynem obiektów blob, kolejek i tabel.</span><span class="sxs-lookup"><span data-stu-id="35ff6-111">After completion, the **Add Connected Services** dialog automatically displays documentation detailing the steps required to start working with blob storage, queues, and tables.</span></span>

## <a name="connect-to-azure-storage-using-the-connected-services-dialog"></a><span data-ttu-id="35ff6-112">Łączenie się z magazynem Azure za pomocą okna dialogowego połączenia usługi</span><span class="sxs-lookup"><span data-stu-id="35ff6-112">Connect to Azure Storage using the Connected Services dialog</span></span>
1. <span data-ttu-id="35ff6-113">Otwórz projekt w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="35ff6-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="35ff6-114">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **usług połączonych** węzeł i z menu kontekstowego, a następnie wybierz **dodać podłączonej usługi**.</span><span class="sxs-lookup"><span data-stu-id="35ff6-114">In **Solution Explorer**, right-click the **Connected Services** node, and, from the context menu, and select **Add Connected Service**.</span></span>
   
    ![Dodaj Azure połączona usługa](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="35ff6-116">W **usług połączonych** wybierz pozycję **magazynu w chmurze z usługą Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="35ff6-116">In the **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Dodawanie magazynu Azure](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="35ff6-118">W **usługi Azure Storage** okno dialogowe, wybierz istniejące konto magazynu i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="35ff6-118">In the **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="35ff6-119">Jeśli musisz utworzyć konto magazynu, przejdź do następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="35ff6-119">If you need to create a storage account, go to the next step.</span></span> <span data-ttu-id="35ff6-120">W przeciwnym razie przejdź do kroku 6.</span><span class="sxs-lookup"><span data-stu-id="35ff6-120">Otherwise, skip to step 6.</span></span>
    
    ![Dodaj istniejące konto magazynu do projektu](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="35ff6-122">Aby utworzyć konto magazynu:</span><span class="sxs-lookup"><span data-stu-id="35ff6-122">To create a storage account:</span></span> 
   
   1. <span data-ttu-id="35ff6-123">Wybierz **Utwórz nowe konto magazynu** w dolnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="35ff6-123">Select **Create a New Storage Account** at the bottom of the dialog.</span></span>

   1. <span data-ttu-id="35ff6-124">Wypełnianie **Utwórz konto magazynu** okna dialogowego, a następnie wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="35ff6-124">Fill out the **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![Nowe konto magazynu Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="35ff6-126">Gdy **usługi Azure Storage** zostanie wyświetlone okno dialogowe, nowe konto magazynu zostanie wyświetlony na liście.</span><span class="sxs-lookup"><span data-stu-id="35ff6-126">When the **Azure Storage** dialog is displayed, the new storage account appears in the list.</span></span> <span data-ttu-id="35ff6-127">Wybierz nowe konto magazynu na liście, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="35ff6-127">Select the new storage account in the list, and select **Add**.</span></span>

1. <span data-ttu-id="35ff6-128">Magazyn podłączonej usługi pojawia się w obszarze **odwołania do usług** węzła projektu.</span><span class="sxs-lookup"><span data-stu-id="35ff6-128">The storage connected service appears under the **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="35ff6-129">Jak zmienić jest projektu</span><span class="sxs-lookup"><span data-stu-id="35ff6-129">How your project is modified</span></span>
<span data-ttu-id="35ff6-130">Po zakończeniu okna dialogowego programu Visual Studio dodaje odwołania i modyfikuje niektórych plików konfiguracyjnych.</span><span class="sxs-lookup"><span data-stu-id="35ff6-130">When you finish the dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="35ff6-131">Określone zmiany są zależne od typu projektu:</span><span class="sxs-lookup"><span data-stu-id="35ff6-131">The specific changes depend on the project type:</span></span> 

- <span data-ttu-id="35ff6-132">Projekt ASP.NET - [co się stało — projekty programu ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span><span class="sxs-lookup"><span data-stu-id="35ff6-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="35ff6-133">Projekt platformy ASP.NET Core - [co się stało — projekty programu ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span><span class="sxs-lookup"><span data-stu-id="35ff6-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="35ff6-134">Projekt usługi w chmurze (role sieci web i proces roboczy) - [co się stało — projekty usługi w chmurze](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span><span class="sxs-lookup"><span data-stu-id="35ff6-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="35ff6-135">Projekt zadania WebJob — [co się stało — projekty zadania WebJob](visual-studio/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="35ff6-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="35ff6-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="35ff6-136">Next steps</span></span>
- [<span data-ttu-id="35ff6-137">MSDN Forum: Usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="35ff6-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="35ff6-138">Blog zespołu usługi Magazyn Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="35ff6-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="35ff6-139">Dokumentację magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="35ff6-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
