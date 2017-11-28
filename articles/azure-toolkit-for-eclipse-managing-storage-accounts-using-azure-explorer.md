---
title: "aaaManage kont magazynu przy użyciu hello Eksploratora Azure dla programu Eclipse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage magazyn Azure kont za pomocą hello Eksploratora Azure dla programu Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: b7ec53e77e3c96d87754b9a658d31e6182121b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="3f6aa-103">Zarządzanie kontami magazynu przy użyciu hello Eksploratora Azure dla programu Eclipse</span><span class="sxs-lookup"><span data-stu-id="3f6aa-103">Manage storage accounts by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="3f6aa-104">Hello Eksploratora Azure, która jest częścią zestawu narzędzi platformy Azure dla programu Eclipse hello, zapewnia Java deweloperom łatwe w użyciu rozwiązanie do zarządzania kontami magazynu na koncie Azure z wewnątrz hello Eclipse zintegrowane środowisko programistyczne (IDE).</span><span class="sxs-lookup"><span data-stu-id="3f6aa-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="3f6aa-105">Utwórz konto magazynu w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="3f6aa-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="3f6aa-106">Konto magazynu przy użyciu Eksploratora Azure hello toocreate hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3f6aa-106">toocreate a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="3f6aa-107">Zaloguj się tooyour konto platformy Azure przy użyciu hello [instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse].</span><span class="sxs-lookup"><span data-stu-id="3f6aa-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="3f6aa-108">W hello **Eksploratora Azure** wyświetlić, rozwiń węzeł hello **Azure** węzła, kliknij prawym przyciskiem myszy **kont magazynu**, a następnie kliknij przycisk **Utwórz konto magazynu**.</span><span class="sxs-lookup"><span data-stu-id="3f6aa-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Utwórz konto magazynu, polecenie][CS01]

3. <span data-ttu-id="3f6aa-110">W hello **Utwórz konto magazynu** oknie dialogowym Określ hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="3f6aa-110">In hello **Create Storage Account** dialog box, specify hello following options:</span></span>

   ![Tworzenie nowego konta magazynu, okno dialogowe][CS02]

   * <span data-ttu-id="3f6aa-112">**Nazwa**: Określa nazwę hello hello nowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="3f6aa-112">**Name**: Specifies hello name for hello new storage account.</span></span>

   * <span data-ttu-id="3f6aa-113">**Subskrypcja**: Określa hello mają toouse dla nowego konta magazynu hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3f6aa-113">**Subscription**: Specifies hello Azure subscription that you want toouse for hello new storage account.</span></span>

   * <span data-ttu-id="3f6aa-114">**Grupa zasobów**: Określa hello grupy zasobów dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3f6aa-114">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="3f6aa-115">Wybierz jedną z hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="3f6aa-115">Select one of hello following options:</span></span>
      * <span data-ttu-id="3f6aa-116">**Utwórz nowy**: Określa, że toocreate nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="3f6aa-116">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="3f6aa-117">**Użyj istniejącego**: Określa, czy będzie wybierz z listy grup zasobów, które są skojarzone z kontem usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="3f6aa-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="3f6aa-118">**Region**: Określa lokalizację hello, w której zostanie utworzona konta magazynu (na przykład "Zachodnie nam").</span><span class="sxs-lookup"><span data-stu-id="3f6aa-118">**Region**: Specifies hello location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="3f6aa-119">**Konto rodzaju**: Określa typ hello toocreate konta magazynu (na przykład "magazynu obiektów Blob").</span><span class="sxs-lookup"><span data-stu-id="3f6aa-119">**Account kind**: Specifies hello type of storage account toocreate (for example, "Blob storage").</span></span> <span data-ttu-id="3f6aa-120">Aby uzyskać więcej informacji, zobacz [kont magazynu Azure o].</span><span class="sxs-lookup"><span data-stu-id="3f6aa-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="3f6aa-121">**Wydajność**: Określa konto magazynu, które oferty toouse hello wybranego wydawcy (na przykład "Premium").</span><span class="sxs-lookup"><span data-stu-id="3f6aa-121">**Performance**: Specifies which storage account offering toouse from hello selected publisher (for example, "Premium").</span></span> <span data-ttu-id="3f6aa-122">Aby uzyskać więcej informacji, zobacz [elementy docelowe skalowalności i wydajności magazynu Azure].</span><span class="sxs-lookup"><span data-stu-id="3f6aa-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="3f6aa-123">**Replikacja**: Określa hello replikacji dla konta magazynu hello (na przykład "Strefowo nadmiarowy").</span><span class="sxs-lookup"><span data-stu-id="3f6aa-123">**Replication**: Specifies hello replication for hello storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="3f6aa-124">Aby uzyskać więcej informacji, zobacz [replikacji usługi Azure storage].</span><span class="sxs-lookup"><span data-stu-id="3f6aa-124">For more information, see [Azure storage replication].</span></span>

4. <span data-ttu-id="3f6aa-125">Po określeniu wszystkie hello poprzedzających opcje, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="3f6aa-125">When you have specified all of hello preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="3f6aa-126">Tworzenie kontenera magazynu w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="3f6aa-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="3f6aa-127">toocreate kontener magazynu przy użyciu Eksploratora Azure hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3f6aa-127">toocreate a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="3f6aa-128">W hello **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy konto magazynu hello, gdzie mają toocreate kontener, a następnie kliknij przycisk **Tworzenie kontenera obiektów blob**.</span><span class="sxs-lookup"><span data-stu-id="3f6aa-128">In hello **Azure Explorer** view, right-click hello storage account where you want toocreate a container, and then click **Create blob container**.</span></span>

   ![Utwórz polecenie kontenera obiektów blob][CC01]

2. <span data-ttu-id="3f6aa-130">W hello **Tworzenie kontenera obiektów blob** okno dialogowe, określ nazwę hello z kontenera, a następnie kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f6aa-130">In hello **Create blob container** dialog box, specify hello name for your container, and then click **OK**.</span></span> <span data-ttu-id="3f6aa-131">Aby uzyskać więcej informacji o nazwach kontenery magazynu, zobacz [nazewnictwa i odwołuje się do kontenerów, obiektów blob i metadanych].</span><span class="sxs-lookup"><span data-stu-id="3f6aa-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Tworzenie kontenera obiektów blob, okno dialogowe][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="3f6aa-133">Usuń kontener magazynu w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="3f6aa-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="3f6aa-134">toodelete kontener magazynu przy użyciu Eksploratora Azure hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3f6aa-134">toodelete a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="3f6aa-135">W hello **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy kontener magazynu hello, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="3f6aa-135">In hello **Azure Explorer** view, right-click hello storage container, and then click **Delete**.</span></span>

   ![Usuń polecenie kontenera magazynu][DC01]

2. <span data-ttu-id="3f6aa-137">W oknie potwierdzenia powitania kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f6aa-137">In hello confirmation window, click **OK**.</span></span>

   ![Usuń okno potwierdzenia kontenera magazynu][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="3f6aa-139">Usuwanie konta magazynu w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="3f6aa-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="3f6aa-140">Konto magazynu przy użyciu Eksploratora Azure hello toodelete hello następujące:</span><span class="sxs-lookup"><span data-stu-id="3f6aa-140">toodelete a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="3f6aa-141">W hello **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy konto magazynu hello, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="3f6aa-141">In hello **Azure Explorer** view, right-click hello storage account, and then click **Delete**.</span></span>

   ![Usuń polecenie konta magazynu][DS01]

2. <span data-ttu-id="3f6aa-143">W oknie potwierdzenia powitania kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f6aa-143">In hello confirmation window, click **OK**.</span></span>

   ![Usuń okno potwierdzenia konta magazynu][DS02]

## <a name="next-steps"></a><span data-ttu-id="3f6aa-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3f6aa-145">Next steps</span></span>
<span data-ttu-id="3f6aa-146">Aby uzyskać więcej informacji o kontach magazynu Azure rozmiary i cenach, zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="3f6aa-146">For more information about Azure storage accounts, sizes, and pricing, see hello following resources:</span></span>

* <span data-ttu-id="3f6aa-147">[Wprowadzenie tooMicrosoft usługi Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="3f6aa-147">[Introduction tooMicrosoft Azure Storage]</span></span>
* <span data-ttu-id="3f6aa-148">[kont magazynu Azure o]</span><span class="sxs-lookup"><span data-stu-id="3f6aa-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="3f6aa-149">Rozmiary konto usługi Azure storage</span><span class="sxs-lookup"><span data-stu-id="3f6aa-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="3f6aa-150">[Rozmiary dla konta magazynu systemu Windows na platformie Azure]</span><span class="sxs-lookup"><span data-stu-id="3f6aa-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="3f6aa-151">[Rozmiary dla konta magazynu w systemie Linux na platformie Azure]</span><span class="sxs-lookup"><span data-stu-id="3f6aa-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="3f6aa-152">Konto usługi Azure storage — cennik</span><span class="sxs-lookup"><span data-stu-id="3f6aa-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="3f6aa-153">[Cennik konta magazynu systemu Windows]</span><span class="sxs-lookup"><span data-stu-id="3f6aa-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="3f6aa-154">[Cennik konta magazynu systemu Linux]</span><span class="sxs-lookup"><span data-stu-id="3f6aa-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="3f6aa-155">Aby uzyskać więcej informacji na temat narzędzi Azure dla języka Java IDEs Zobacz hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="3f6aa-155">For more information about Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="3f6aa-156">[Azure zestawu narzędzi dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f6aa-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3f6aa-157">[What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f6aa-157">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3f6aa-158">[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f6aa-158">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3f6aa-159">[instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f6aa-159">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3f6aa-160">[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f6aa-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="3f6aa-161">[Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="3f6aa-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3f6aa-162">[What's new in hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3f6aa-162">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3f6aa-163">[Instalowanie hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3f6aa-163">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3f6aa-164">[Logowanie instrukcje dotyczące hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3f6aa-164">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3f6aa-165">[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3f6aa-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="3f6aa-166">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center] i [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="3f6aa-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalowanie hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Logowanie instrukcje dotyczące hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[What's new in hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/

[Wprowadzenie tooMicrosoft usługi Azure Storage]: /azure/storage/storage-introduction
[kont magazynu Azure o]: /azure/storage/storage-create-storage-account
[replikacji usługi Azure storage]: /azure/storage/storage-redundancy
[Cele dotyczące wydajności i skalowalności magazynu Azure]: /azure/storage/storage-scalability-targets
[nazewnictwa i odwołuje się do kontenerów, obiektów blob i metadanych]: http://go.microsoft.com/fwlink/?LinkId=255555

[Rozmiary dla konta magazynu systemu Windows na platformie Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Rozmiary dla konta magazynu w systemie Linux na platformie Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Cennik konta magazynu systemu Windows]: /pricing/details/virtual-machines/windows/
[Cennik konta magazynu systemu Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
