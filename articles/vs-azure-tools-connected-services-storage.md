---
title: "aaaAdd usługi Azure Storage za pomocą usług połączonych w programie Visual Studio | Dokumentacja firmy Microsoft"
description: "Dodaj aplikację tooyour usługi Azure Storage za pomocą programu Visual Studio Dodaj połączone usługi hello — okno dialogowe"
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
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="ff6d0-103">Dodawanie magazynu platformy Azure przy użyciu programu Visual Studio usługami</span><span class="sxs-lookup"><span data-stu-id="ff6d0-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="ff6d0-104">Za pomocą programu Visual Studio, można połączyć żadnego powitania po tooAzure magazynu przy użyciu hello **dodać usług połączonych** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="ff6d0-104">With Visual Studio, you can connect any of hello following tooAzure Storage by using hello **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="ff6d0-105">Usługi w chmurze C#</span><span class="sxs-lookup"><span data-stu-id="ff6d0-105">C# cloud service</span></span>
- <span data-ttu-id="ff6d0-106">Usługi mobilnej zaplecza .NET</span><span class="sxs-lookup"><span data-stu-id="ff6d0-106">.NET backend mobile service</span></span>
- <span data-ttu-id="ff6d0-107">Witryny sieci Web ASP.NET lub usługi</span><span class="sxs-lookup"><span data-stu-id="ff6d0-107">ASP.NET website or service</span></span>
- <span data-ttu-id="ff6d0-108">Usługi platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ff6d0-108">ASP.NET Core service</span></span>
- <span data-ttu-id="ff6d0-109">Usługa zadań WebJob Azure</span><span class="sxs-lookup"><span data-stu-id="ff6d0-109">Azure WebJob service</span></span> 

<span data-ttu-id="ff6d0-110">Witaj podłączonej usługi funkcja dodaje wszystkie odwołania hello potrzebne i projektu tooyour kodu połączenia i odpowiednio modyfikuje plików konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ff6d0-110">hello connected service functionality adds all hello needed references and connection code tooyour project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="ff6d0-111">Po zakończeniu hello **dodać usług połączonych** automatycznie wyświetlone okno dialogowe dokumentacji wyszczególnieniem toostart wymagane kroki hello Praca z magazynu obiektów blob, kolejek i tabel.</span><span class="sxs-lookup"><span data-stu-id="ff6d0-111">After completion, hello **Add Connected Services** dialog automatically displays documentation detailing hello steps required toostart working with blob storage, queues, and tables.</span></span>

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a><span data-ttu-id="ff6d0-112">Połącz tooAzure magazynu przy użyciu usług połączonych hello okna dialogowego</span><span class="sxs-lookup"><span data-stu-id="ff6d0-112">Connect tooAzure Storage using hello Connected Services dialog</span></span>
1. <span data-ttu-id="ff6d0-113">Otwórz projekt w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ff6d0-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="ff6d0-114">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **usług połączonych** węzeł i z menu kontekstowego hello, a następnie wybierz **dodać podłączonej usługi**.</span><span class="sxs-lookup"><span data-stu-id="ff6d0-114">In **Solution Explorer**, right-click hello **Connected Services** node, and, from hello context menu, and select **Add Connected Service**.</span></span>
   
    ![Dodaj Azure połączona usługa](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="ff6d0-116">W hello **usług połączonych** wybierz pozycję **magazynu w chmurze z usługą Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="ff6d0-116">In hello **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Dodawanie magazynu Azure](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="ff6d0-118">W hello **usługi Azure Storage** okno dialogowe, wybierz istniejące konto magazynu i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ff6d0-118">In hello **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="ff6d0-119">Jeśli potrzebujesz toocreate konta magazynu, przejdź toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="ff6d0-119">If you need toocreate a storage account, go toohello next step.</span></span> <span data-ttu-id="ff6d0-120">W przeciwnym razie Pomiń toostep 6.</span><span class="sxs-lookup"><span data-stu-id="ff6d0-120">Otherwise, skip toostep 6.</span></span>
    
    ![Dodaj istniejące tooproject konta magazynu](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="ff6d0-122">toocreate konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="ff6d0-122">toocreate a storage account:</span></span> 
   
   1. <span data-ttu-id="ff6d0-123">Wybierz **Utwórz nowe konto magazynu** u dołu okna dialogowego hello hello.</span><span class="sxs-lookup"><span data-stu-id="ff6d0-123">Select **Create a New Storage Account** at hello bottom of hello dialog.</span></span>

   1. <span data-ttu-id="ff6d0-124">Wypełnianie hello **Utwórz konto magazynu** okna dialogowego, a następnie wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ff6d0-124">Fill out hello **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![Nowe konto magazynu Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="ff6d0-126">Gdy hello **usługi Azure Storage** zostanie wyświetlone okno dialogowe, hello nowe konto magazynu jest wyświetlana na liście hello.</span><span class="sxs-lookup"><span data-stu-id="ff6d0-126">When hello **Azure Storage** dialog is displayed, hello new storage account appears in hello list.</span></span> <span data-ttu-id="ff6d0-127">Wybierz nowe konto magazynu hello hello listy, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ff6d0-127">Select hello new storage account in hello list, and select **Add**.</span></span>

1. <span data-ttu-id="ff6d0-128">Witaj magazynu podłączonej usługi pojawia się w obszarze hello **odwołania do usług** węzła projektu.</span><span class="sxs-lookup"><span data-stu-id="ff6d0-128">hello storage connected service appears under hello **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="ff6d0-129">Jak zmienić jest projektu</span><span class="sxs-lookup"><span data-stu-id="ff6d0-129">How your project is modified</span></span>
<span data-ttu-id="ff6d0-130">Po zakończeniu okna dialogowego hello Visual Studio dodaje odwołania i modyfikuje niektórych plików konfiguracyjnych.</span><span class="sxs-lookup"><span data-stu-id="ff6d0-130">When you finish hello dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="ff6d0-131">zmiany Hello są zależne od typu projektu hello:</span><span class="sxs-lookup"><span data-stu-id="ff6d0-131">hello specific changes depend on hello project type:</span></span> 

- <span data-ttu-id="ff6d0-132">Projekt ASP.NET - [co się stało — projekty programu ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span><span class="sxs-lookup"><span data-stu-id="ff6d0-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="ff6d0-133">Projekt platformy ASP.NET Core - [co się stało — projekty programu ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span><span class="sxs-lookup"><span data-stu-id="ff6d0-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="ff6d0-134">Projekt usługi w chmurze (role sieci web i proces roboczy) - [co się stało — projekty usługi w chmurze](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span><span class="sxs-lookup"><span data-stu-id="ff6d0-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="ff6d0-135">Projekt zadania WebJob — [co się stało — projekty zadania WebJob](visual-studio/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="ff6d0-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff6d0-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ff6d0-136">Next steps</span></span>
- [<span data-ttu-id="ff6d0-137">MSDN Forum: Usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ff6d0-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="ff6d0-138">Blog zespołu usługi Magazyn Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ff6d0-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="ff6d0-139">Dokumentację magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ff6d0-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
