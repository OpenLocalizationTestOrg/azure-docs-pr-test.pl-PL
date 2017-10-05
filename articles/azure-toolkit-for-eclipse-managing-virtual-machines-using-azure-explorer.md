---
title: "Zarządzania maszynami wirtualnymi przy użyciu Eksploratora Azure dla programu Eclipse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać maszynach wirtualnych platformy Azure za pomocą Eksploratora Azure dla programu Eclipse."
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
ms.openlocfilehash: 9784e8af9c530078afee06f08a23403a44b0762f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="6539b-103">Zarządzania maszynami wirtualnymi przy użyciu Eksploratora Azure dla programu Eclipse</span><span class="sxs-lookup"><span data-stu-id="6539b-103">Manage virtual machines by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="6539b-104">Eksploratora Azure, która jest częścią zestawu narzędzi platformy Azure dla programu Eclipse, oferuje Java deweloperom łatwe w użyciu rozwiązanie do zarządzania maszynami wirtualnymi na koncie Azure z wewnątrz Eclipse zintegrowane środowisko programistyczne (IDE).</span><span class="sxs-lookup"><span data-stu-id="6539b-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="6539b-105">Utwórz maszynę wirtualną w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="6539b-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="6539b-106">Aby utworzyć maszynę wirtualną za pomocą Eksploratora Azure, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6539b-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="6539b-107">Zaloguj się do konta platformy Azure przy użyciu [instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse].</span><span class="sxs-lookup"><span data-stu-id="6539b-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="6539b-108">W **Eksploratora Azure** wyświetlić, rozwiń węzeł **Azure** węzła, kliknij prawym przyciskiem myszy **maszyn wirtualnych**, a następnie kliknij przycisk **Utwórz maszynę Wirtualną**.</span><span class="sxs-lookup"><span data-stu-id="6539b-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   <span data-ttu-id="6539b-109">![Polecenie Utwórz maszynę Wirtualną][CR01]</span><span class="sxs-lookup"><span data-stu-id="6539b-109">![The Create VM command][CR01]</span></span>  
   <span data-ttu-id="6539b-110">**Tworzenia nowej maszyny wirtualnej** zostanie otwarty Kreator.</span><span class="sxs-lookup"><span data-stu-id="6539b-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="6539b-111">W **Wybierz subskrypcję** okna, wybierz subskrypcję, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6539b-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Wybierz okno subskrypcji][CR02]

4. <span data-ttu-id="6539b-113">W **Wybieranie obrazu maszyny wirtualnej** okna, wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="6539b-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="6539b-114">**Lokalizacja**: Określa, gdzie można utworzyć maszyny wirtualnej (na przykład *zachodnie stany USA*).</span><span class="sxs-lookup"><span data-stu-id="6539b-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="6539b-115">**Wydawca**: Określa wydawcy, który utworzył obraz będziesz używać do tworzenia maszyny wirtualnej (na przykład *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="6539b-115">**Publisher**: Specifies the publisher that created the image you'll use to create your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="6539b-116">**Oferują**: określa oferty do użycia z wybranego wydawcy maszyny wirtualnej (na przykład *JDK*).</span><span class="sxs-lookup"><span data-stu-id="6539b-116">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="6539b-117">**Jednostka SKU**: Określa jedn (SKU) do użycia z wybranej oferty (na przykład *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="6539b-117">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="6539b-118">**Wersja #**: Określa, która wersja wybranej jednostki SKU do użycia.</span><span class="sxs-lookup"><span data-stu-id="6539b-118">**Version #**: Specifies which version of the selected SKU to use.</span></span>

    ![Wybierz okno Obraz maszyny wirtualnej][CR03]

5. <span data-ttu-id="6539b-120">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="6539b-120">Click **Next**.</span></span>

6. <span data-ttu-id="6539b-121">W **ustawienia podstawowej maszyny wirtualnej** okna, wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="6539b-121">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="6539b-122">**Nazwa maszyny wirtualnej**: Określa nazwę dla nowej maszyny wirtualnej, który musi rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.</span><span class="sxs-lookup"><span data-stu-id="6539b-122">**Virtual Machine Name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="6539b-123">**Rozmiar**: Określa liczbę rdzeni i ilości pamięci do przydzielenia dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6539b-123">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="6539b-124">**Nazwa użytkownika**: Określa konto administratora, aby utworzyć zarządzania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6539b-124">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="6539b-125">**Hasło** i **Potwierdź**: Określa hasło dla konta administratora.</span><span class="sxs-lookup"><span data-stu-id="6539b-125">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

    ![Okno Ustawienia podstawowej maszyny wirtualnej][CR04]

7. <span data-ttu-id="6539b-127">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="6539b-127">Click **Next**.</span></span>

8. <span data-ttu-id="6539b-128">W **utworzyć nowe konto magazynu** okna, wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="6539b-128">In the **Create New Storage Account** window, enter the following information:</span></span>

   * <span data-ttu-id="6539b-129">**Grupa zasobów**: Określa grupę zasobów dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6539b-129">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="6539b-130">Wybierz jedną z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="6539b-130">Select one of the following options:</span></span>
      * <span data-ttu-id="6539b-131">**Utwórz nowe**: Określa, czy chcesz utworzyć nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="6539b-131">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="6539b-132">**Użyj istniejącego**: Określa, czy chcesz wybrać grupę zasobów, która jest już skojarzona z Twoim kontem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6539b-132">**Use existing**: Specifies that you want to select a resource group that is already associated with your Azure account.</span></span>

      ![Okno dialogowe Tworzenie nowego konta magazynu][CR05]

   * <span data-ttu-id="6539b-134">**Konto magazynu**: Określa konto magazynu do przechowywania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6539b-134">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="6539b-135">Możesz użyć istniejącego konta magazynu lub utworzyć nowe konto.</span><span class="sxs-lookup"><span data-stu-id="6539b-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="6539b-136">**Sieć wirtualna** i **podsieci**: Określa sieci wirtualnej i podsieci, które będą się łączyć maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6539b-136">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="6539b-137">Można użyć istniejącej sieci i podsieci, lub można utworzyć nowej sieci i podsieci.</span><span class="sxs-lookup"><span data-stu-id="6539b-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="6539b-138">W przypadku wybrania **Utwórz nowy**, zostanie wyświetlone następujące okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="6539b-138">If you select **Create new**, the following dialog box is displayed:</span></span>

      ![Okno dialogowe Tworzenie nowej sieci wirtualnej][CR06]

9. <span data-ttu-id="6539b-140">W **skojarzonych zasobów** okna, wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="6539b-140">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="6539b-141">**Publiczny adres IP**: Określa adres IP dołączonej do Internetu dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6539b-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="6539b-142">Użytkownik może utworzyć nowego adresu IP, lub Jeśli maszyna wirtualna nie ma publicznego adresu IP, możesz wybrać **(Brak)**.</span><span class="sxs-lookup"><span data-stu-id="6539b-142">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="6539b-143">**Grupy zabezpieczeń sieci**: Określa opcjonalne zapory sieci dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6539b-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="6539b-144">Możesz wybrać istniejącą zapory lub, jeśli maszyna wirtualna nie będzie używać zapory sieciowej, można wybrać **(Brak)**.</span><span class="sxs-lookup"><span data-stu-id="6539b-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="6539b-145">**Zestaw dostępności**: określa zbiór dostępności opcjonalne, że maszyna wirtualna może należeć do.</span><span class="sxs-lookup"><span data-stu-id="6539b-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="6539b-146">Można wybrać istniejący zestaw dostępności lub Utwórz nowy zestaw dostępności lub, jeśli na komputerze wirtualnym zostanie nie należą do zestawu dostępności, możesz wybrać **(Brak)**.</span><span class="sxs-lookup"><span data-stu-id="6539b-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong to an availability set, you can select **(None)**.</span></span>

   ![Okno skojarzonych zasobów][CR07]

9. <span data-ttu-id="6539b-148">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="6539b-148">Click **Finish**.</span></span>  
  <span data-ttu-id="6539b-149">Nowej maszyny wirtualnej jest wyświetlany w oknie narzędzia Eksplorator Azure.</span><span class="sxs-lookup"><span data-stu-id="6539b-149">Your new virtual machine is displayed in the Azure Explorer tool window.</span></span>

   ![Nowej maszyny wirtualnej][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="6539b-151">Uruchom ponownie maszynę wirtualną w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="6539b-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="6539b-152">Aby ponownie uruchomić maszynę wirtualną za pomocą Eksploratora Azure w programie Eclipse, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6539b-152">To restart a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="6539b-153">W **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy maszynę wirtualną, a następnie wybierz **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="6539b-153">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![Polecenie ponownego uruchomienia maszyny wirtualnej][RE01]

2. <span data-ttu-id="6539b-155">W oknie potwierdzenia kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="6539b-155">In the confirmation window, click **Yes**.</span></span>

   ![Okno potwierdzenia ponownego uruchomienia][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="6539b-157">Zamknij maszynę wirtualną w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="6539b-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="6539b-158">Aby zamknąć uruchomionej maszyny wirtualnej za pomocą Eksploratora Azure w programie Eclipse, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6539b-158">To shut down a running virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="6539b-159">W **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy maszynę wirtualną, a następnie wybierz **zamknięcia**.</span><span class="sxs-lookup"><span data-stu-id="6539b-159">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![Polecenie zamknięcia maszyn wirtualnych][SH01]

2. <span data-ttu-id="6539b-161">W oknie potwierdzenia kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="6539b-161">In the confirmation window, click **Yes**.</span></span>

   ![Okno potwierdzenia zamknięcia maszyn wirtualnych][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="6539b-163">Usuń maszynę wirtualną w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="6539b-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="6539b-164">Aby usunąć maszynę wirtualną za pomocą Eksploratora Azure w programie Eclipse, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6539b-164">To delete a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="6539b-165">W **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy maszynę wirtualną, a następnie wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="6539b-165">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![Polecenie Usuń maszynę wirtualną][DE01]

2. <span data-ttu-id="6539b-167">W oknie potwierdzenia kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="6539b-167">In the confirmation window, click **Yes**.</span></span>

   ![Okno potwierdzenia usunięcia maszyny wirtualnej][DE02]

## <a name="next-steps"></a><span data-ttu-id="6539b-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6539b-169">Next steps</span></span>
<span data-ttu-id="6539b-170">Aby uzyskać więcej informacji na temat rozmiarów maszyn wirtualnych platformy Azure i cenach zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="6539b-170">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="6539b-171">Rozmiary maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6539b-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="6539b-172">[Rozmiary maszyn wirtualnych systemu Windows na platformie Azure]</span><span class="sxs-lookup"><span data-stu-id="6539b-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="6539b-173">[Rozmiary maszyn wirtualnych systemu Linux na platformie Azure]</span><span class="sxs-lookup"><span data-stu-id="6539b-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="6539b-174">Cennik maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6539b-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="6539b-175">[Cennik maszyn wirtualnych systemu Windows]</span><span class="sxs-lookup"><span data-stu-id="6539b-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="6539b-176">[Cennik maszyn wirtualnych systemu Linux]</span><span class="sxs-lookup"><span data-stu-id="6539b-176">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="6539b-177">Aby uzyskać więcej informacji o narzędzi Azure Java IDEs zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="6539b-177">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="6539b-178">[Azure zestawu narzędzi dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6539b-178">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="6539b-179">[Nowości w zestawie narzędzi programu Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6539b-179">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="6539b-180">[Installing the Azure Toolkit for Eclipse] (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="6539b-180">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="6539b-181">[instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6539b-181">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="6539b-182">[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6539b-182">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="6539b-183">[Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="6539b-183">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="6539b-184">[Nowości w zestawie narzędzi programu Azure for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="6539b-184">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="6539b-185">[Installing the Azure Toolkit for IntelliJ] (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="6539b-185">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="6539b-186">[Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="6539b-186">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="6539b-187">[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="6539b-187">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="6539b-188">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center] i [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="6539b-188">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="6539b-189">[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="6539b-189">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="6539b-190">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="6539b-190">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="6539b-191">[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="6539b-191">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="6539b-192">[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="6539b-192">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="6539b-193">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="6539b-193">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="6539b-194">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="6539b-194">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="6539b-195">[instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="6539b-195">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="6539b-196">[Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="6539b-196">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="6539b-197">[Nowości w zestawie narzędzi programu Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="6539b-197">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="6539b-198">[Nowości w zestawie narzędzi programu Azure for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="6539b-198">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="6539b-199">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="6539b-199">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="6539b-200">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="6539b-200">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="6539b-201">[Rozmiary maszyn wirtualnych systemu Windows na platformie Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="6539b-201">[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="6539b-202">[Rozmiary maszyn wirtualnych systemu Linux na platformie Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="6539b-202">[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="6539b-203">[Cennik maszyn wirtualnych systemu Windows]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="6539b-203">[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="6539b-204">[Cennik maszyn wirtualnych systemu Linux]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="6539b-204">[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/</span></span>

<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
