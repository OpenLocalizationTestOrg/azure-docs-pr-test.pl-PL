---
title: "Zarządzanie kontami magazynu przy użyciu Eksploratora Azure for IntelliJ | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać kontami magazynu Azure za pomocą Eksploratora Azure for IntelliJ."
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
ms.openlocfilehash: a1b56cc2751fc43a1ad6917eca77eec460f26694
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="0cf57-103">Zarządzanie kontami magazynu przy użyciu Eksploratora Azure for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="0cf57-103">Manage storage accounts by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="0cf57-104">Eksploratora Azure, która jest częścią zestawu narzędzi Azure for IntelliJ, oferuje Java deweloperom łatwe w użyciu rozwiązanie do zarządzania kontami magazynu Azure konta od wewnątrz IntelliJ zintegrowane środowisko programistyczne (IDE).</span><span class="sxs-lookup"><span data-stu-id="0cf57-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a><span data-ttu-id="0cf57-105">Utwórz konto magazynu w IntelliJ</span><span class="sxs-lookup"><span data-stu-id="0cf57-105">Create a storage account in IntelliJ</span></span>

<span data-ttu-id="0cf57-106">Aby utworzyć konto magazynu przy użyciu Eksploratora Azure, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0cf57-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="0cf57-107">Zaloguj się do konta platformy Azure przy użyciu [instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse].</span><span class="sxs-lookup"><span data-stu-id="0cf57-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span> 

2. <span data-ttu-id="0cf57-108">W **Eksploratora Azure** wyświetlić, rozwiń węzeł **Azure** węzła, kliknij prawym przyciskiem myszy **kont magazynu**, a następnie kliknij przycisk **Utwórz konto magazynu**.</span><span class="sxs-lookup"><span data-stu-id="0cf57-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Utwórz konto magazynu, polecenie][CS01]

3. <span data-ttu-id="0cf57-110">W **Utwórz konto magazynu** oknie dialogowym określ następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="0cf57-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Tworzenie nowego konta magazynu, okno dialogowe][CS02]

   * <span data-ttu-id="0cf57-112">**Nazwa**: Określa nazwę dla nowego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="0cf57-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="0cf57-113">**Konto rodzaju**: Określa typ konta magazynu (na przykład "Magazynu obiektów Blob").</span><span class="sxs-lookup"><span data-stu-id="0cf57-113">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="0cf57-114">Aby uzyskać więcej informacji, zobacz [kont magazynu Azure o].</span><span class="sxs-lookup"><span data-stu-id="0cf57-114">For more information, see [About Azure storage accounts].</span></span> 

   * <span data-ttu-id="0cf57-115">**Wydajność**: Określa konto magazynu, które oferty do użycia z wybranego wydawcy (na przykład "Premium").</span><span class="sxs-lookup"><span data-stu-id="0cf57-115">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="0cf57-116">Aby uzyskać więcej informacji, zobacz [elementy docelowe skalowalności i wydajności magazynu Azure].</span><span class="sxs-lookup"><span data-stu-id="0cf57-116">For more information, see [Azure storage scalability and performance targets].</span></span> 

   * <span data-ttu-id="0cf57-117">**Replikacja**: Określa replikacji dla konta magazynu (na przykład "Strefowo nadmiarowy").</span><span class="sxs-lookup"><span data-stu-id="0cf57-117">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="0cf57-118">Aby uzyskać więcej informacji, zobacz [replikacji usługi Azure storage].</span><span class="sxs-lookup"><span data-stu-id="0cf57-118">For more information, see [Azure storage replication].</span></span> 

   * <span data-ttu-id="0cf57-119">**Subskrypcja**: Określa subskrypcji Azure, która ma być używany dla nowego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="0cf57-119">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="0cf57-120">**Lokalizacja**: Określa lokalizację, w której zostanie utworzona konta magazynu (na przykład "Zachodnie nam").</span><span class="sxs-lookup"><span data-stu-id="0cf57-120">**Location**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="0cf57-121">**Grupa zasobów**: Określa grupę zasobów dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0cf57-121">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="0cf57-122">Wybierz jedną z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="0cf57-122">Select one of the following options:</span></span>
      * <span data-ttu-id="0cf57-123">**Utwórz nowe**: Określa, czy chcesz utworzyć nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="0cf57-123">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="0cf57-124">**Użyj istniejącego**: Określa, czy będzie wybierz z listy grup zasobów, które są skojarzone z kontem usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="0cf57-124">**Use existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

4. <span data-ttu-id="0cf57-125">Po określeniu wszystkich powyższych opcji kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0cf57-125">When you have specified all of the preceding options, click **OK**.</span></span>

## <a name="create-a-storage-container-in-intellij"></a><span data-ttu-id="0cf57-126">Tworzenie kontenera magazynu w IntelliJ</span><span class="sxs-lookup"><span data-stu-id="0cf57-126">Create a storage container in IntelliJ</span></span>

<span data-ttu-id="0cf57-127">Aby utworzyć kontener magazynu przy użyciu Eksploratora Azure, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0cf57-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="0cf57-128">W widoku Eksploratora Azure, kliknij prawym przyciskiem myszy konto magazynu, w którym chcesz utworzyć kontener, a następnie kliknij przycisk **Tworzenie kontenera obiektów blob**.</span><span class="sxs-lookup"><span data-stu-id="0cf57-128">In the Azure Explorer view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Utwórz polecenie kontenera obiektów blob][CC01]

2. <span data-ttu-id="0cf57-130">W **Tworzenie kontenera obiektów blob** okno dialogowe, określ nazwę użytkownika kontenera, a następnie kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="0cf57-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="0cf57-131">Aby uzyskać więcej informacji o nazwach kontenery magazynu, zobacz [nazewnictwa i odwołuje się do kontenerów, obiektów blob i metadanych].</span><span class="sxs-lookup"><span data-stu-id="0cf57-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Tworzenie kontenera magazynu, okno dialogowe][CC02]

## <a name="delete-a-storage-container-in-intellij"></a><span data-ttu-id="0cf57-133">Usuń kontener magazynu w IntelliJ</span><span class="sxs-lookup"><span data-stu-id="0cf57-133">Delete a storage container in IntelliJ</span></span>

<span data-ttu-id="0cf57-134">Aby usunąć kontenera magazynu przy użyciu Eksploratora Azure, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0cf57-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="0cf57-135">W widoku Eksploratora Azure, kliknij prawym przyciskiem myszy kontener magazynu, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="0cf57-135">In the Azure Explorer view, right-click the storage container, and then click **Delete**.</span></span>

   ![Usuń polecenie kontenera magazynu][DC01]

2. <span data-ttu-id="0cf57-137">W oknie potwierdzenia kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="0cf57-137">In the confirmation window, click **Yes**.</span></span>

   ![Usuń okno potwierdzenia kontenera magazynu][DC02]

## <a name="delete-a-storage-account-in-intellij"></a><span data-ttu-id="0cf57-139">Usuwanie konta magazynu w IntelliJ</span><span class="sxs-lookup"><span data-stu-id="0cf57-139">Delete a storage account in IntelliJ</span></span>

<span data-ttu-id="0cf57-140">Aby usunąć konto magazynu przy użyciu Eksploratora Azure, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0cf57-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="0cf57-141">W **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy konto magazynu, a następnie wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="0cf57-141">In the **Azure Explorer** view, right-click the storage account, and then select **Delete**.</span></span>

   ![Usuwanie z menu konta magazynu][DS01]

2. <span data-ttu-id="0cf57-143">W oknie potwierdzenia kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="0cf57-143">In the confirmation window, click **Yes**.</span></span>

   ![Usuń okno potwierdzenia konta magazynu][DS02]

## <a name="next-steps"></a><span data-ttu-id="0cf57-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0cf57-145">Next steps</span></span>
<span data-ttu-id="0cf57-146">Aby uzyskać więcej informacji o kontach magazynu Azure rozmiarów i cenach, zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="0cf57-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="0cf57-147">[Wprowadzenie do usługi Microsoft Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="0cf57-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="0cf57-148">[kont magazynu Azure o]</span><span class="sxs-lookup"><span data-stu-id="0cf57-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="0cf57-149">Rozmiary konto usługi Azure storage</span><span class="sxs-lookup"><span data-stu-id="0cf57-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="0cf57-150">[Rozmiary dla konta magazynu systemu Windows na platformie Azure]</span><span class="sxs-lookup"><span data-stu-id="0cf57-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="0cf57-151">[Rozmiary dla konta magazynu w systemie Linux na platformie Azure]</span><span class="sxs-lookup"><span data-stu-id="0cf57-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="0cf57-152">Konto usługi Azure storage — cennik</span><span class="sxs-lookup"><span data-stu-id="0cf57-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="0cf57-153">[Cennik konta magazynu systemu Windows]</span><span class="sxs-lookup"><span data-stu-id="0cf57-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="0cf57-154">[Cennik konta magazynu systemu Linux]</span><span class="sxs-lookup"><span data-stu-id="0cf57-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="0cf57-155">Aby uzyskać więcej informacji o narzędzi Azure Java IDEs zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="0cf57-155">For more information about Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="0cf57-156">[Azure zestawu narzędzi dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0cf57-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="0cf57-157">[Nowości w zestawie narzędzi programu Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0cf57-157">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="0cf57-158">[Installing the Azure Toolkit for Eclipse] (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="0cf57-158">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="0cf57-159">[instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0cf57-159">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="0cf57-160">[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0cf57-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="0cf57-161">[Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="0cf57-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="0cf57-162">[Nowości w zestawie narzędzi programu Azure for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="0cf57-162">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="0cf57-163">[Installing the Azure Toolkit for IntelliJ] (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="0cf57-163">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="0cf57-164">[Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="0cf57-164">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="0cf57-165">[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="0cf57-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="0cf57-166">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center] i [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="0cf57-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="0cf57-167">[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="0cf57-167">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="0cf57-168">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="0cf57-168">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="0cf57-169">[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="0cf57-169">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="0cf57-170">[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="0cf57-170">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="0cf57-171">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="0cf57-171">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="0cf57-172">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="0cf57-172">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="0cf57-173">[instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="0cf57-173">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="0cf57-174">[Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="0cf57-174">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="0cf57-175">[Nowości w zestawie narzędzi programu Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="0cf57-175">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="0cf57-176">[Nowości w zestawie narzędzi programu Azure for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="0cf57-176">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="0cf57-177">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="0cf57-177">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="0cf57-178">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="0cf57-178">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="0cf57-179">[Wprowadzenie do usługi Microsoft Azure Storage]: /azure/storage/storage-introduction</span><span class="sxs-lookup"><span data-stu-id="0cf57-179">[Introduction to Microsoft Azure Storage]: /azure/storage/storage-introduction</span></span>
<span data-ttu-id="0cf57-180">[kont magazynu Azure o]: /azure/storage/storage-create-storage-account</span><span class="sxs-lookup"><span data-stu-id="0cf57-180">[About Azure storage accounts]: /azure/storage/storage-create-storage-account</span></span>
<span data-ttu-id="0cf57-181">[replikacji usługi Azure storage]: /azure/storage/storage-redundancy</span><span class="sxs-lookup"><span data-stu-id="0cf57-181">[Azure storage replication]: /azure/storage/storage-redundancy</span></span>
<span data-ttu-id="0cf57-182">[Cele dotyczące wydajności i skalowalności magazynu Azure]: /azure/storage/storage-scalability-targets</span><span class="sxs-lookup"><span data-stu-id="0cf57-182">[Azure storage scalability and Performance Targets]: /azure/storage/storage-scalability-targets</span></span>
<span data-ttu-id="0cf57-183">[nazewnictwa i odwołuje się do kontenerów, obiektów blob i metadanych]: http://go.microsoft.com/fwlink/?LinkId=255555</span><span class="sxs-lookup"><span data-stu-id="0cf57-183">[Naming and referencing containers, blobs, and metadata]: http://go.microsoft.com/fwlink/?LinkId=255555</span></span>

<span data-ttu-id="0cf57-184">[Rozmiary dla konta magazynu systemu Windows na platformie Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="0cf57-184">[Sizes for Windows storage accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="0cf57-185">[Rozmiary dla konta magazynu w systemie Linux na platformie Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="0cf57-185">[Sizes for Linux storage accounts in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="0cf57-186">[Cennik konta magazynu systemu Windows]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="0cf57-186">[Windows storage-account pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="0cf57-187">[Cennik konta magazynu systemu Linux]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="0cf57-187">[Linux storage-account pricing]: /pricing/details/virtual-machines/linux/</span></span>

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
