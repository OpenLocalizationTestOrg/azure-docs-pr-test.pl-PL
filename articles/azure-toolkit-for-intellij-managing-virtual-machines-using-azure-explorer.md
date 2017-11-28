---
title: "aaaManage maszyn wirtualnych przy użyciu hello Azure Explorer for IntelliJ | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage maszynach wirtualnych platformy Azure przy użyciu hello Azure Explorer for IntelliJ."
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
ms.openlocfilehash: a73dd4f73b311dd3413f6712e3b76c36ee464de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="90715-103">Zarządzania maszynami wirtualnymi przy użyciu hello Azure Explorer for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="90715-103">Manage virtual machines by using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="90715-104">Hello Azure Eksploratora, będący częścią hello Azure Toolkit for IntelliJ zapewnia Java deweloperom łatwe w użyciu rozwiązanie do zarządzania maszynami wirtualnymi na koncie Azure z wewnątrz hello IntelliJ zintegrowane środowisko programistyczne (IDE).</span><span class="sxs-lookup"><span data-stu-id="90715-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="90715-105">Utwórz maszynę wirtualną w IntelliJ</span><span class="sxs-lookup"><span data-stu-id="90715-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="90715-106">toocreate maszynę wirtualną za pomocą Eksploratora Azure hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="90715-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span> 

1. <span data-ttu-id="90715-107">Zaloguj tooyour konto platformy Azure przy użyciu kroków hello w hello [logowania instrukcje dotyczące hello Azure Toolkit for IntelliJ] artykułu.</span><span class="sxs-lookup"><span data-stu-id="90715-107">Sign in tooyour Azure account by using hello steps in hello [Sign-in instructions for hello Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="90715-108">W hello **Eksploratora Azure** wyświetlić, rozwiń węzeł hello **Azure** węzła, kliknij prawym przyciskiem myszy **maszyn wirtualnych**, a następnie kliknij przycisk **Utwórz maszynę Wirtualną**.</span><span class="sxs-lookup"><span data-stu-id="90715-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="90715-109">![Witaj polecenia Utwórz maszynę Wirtualną][CR01]</span><span class="sxs-lookup"><span data-stu-id="90715-109">![hello Create VM command][CR01]</span></span>  
    <span data-ttu-id="90715-110">Witaj **tworzenia nowej maszyny wirtualnej** zostanie otwarty Kreator.</span><span class="sxs-lookup"><span data-stu-id="90715-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="90715-111">W hello **Wybierz subskrypcję** okna, wybierz subskrypcję, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="90715-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![Witaj wybierz okno subskrypcji][CR02]

4. <span data-ttu-id="90715-113">W hello **Wybieranie obrazu maszyny wirtualnej** okna, wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="90715-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="90715-114">**Lokalizacja**: Określa, gdzie można utworzyć maszyny wirtualnej (na przykład *zachodnie stany USA*).</span><span class="sxs-lookup"><span data-stu-id="90715-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="90715-115">**Zalecane obrazu**: Określa, czy wybierzesz obraz z skróconą listę często używane obrazy.</span><span class="sxs-lookup"><span data-stu-id="90715-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="90715-116">**Obraz niestandardowy**: Określa, że będzie Wybieranie niestandardowego obrazu, zapewniając hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="90715-116">**Custom image**: Specifies that you will choose a custom image by providing hello following information:</span></span>

      * <span data-ttu-id="90715-117">**Wydawca**: Określa hello wydawcy, który utworzył obraz hello, która będzie używana dla maszyny wirtualnej (na przykład *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="90715-117">**Publisher**: Specifies hello publisher that created hello image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="90715-118">**Oferują**: Określa maszyny wirtualnej hello oferty toouse hello wybranego wydawcy (na przykład *JDK*).</span><span class="sxs-lookup"><span data-stu-id="90715-118">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="90715-119">**Jednostka SKU**: Określa hello składowania jednostka SKU toouse z wybranej oferty hello (na przykład *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="90715-119">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="90715-120">**Wersja #**: Określa, która wersja hello wybrane toouse jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="90715-120">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

   ![Witaj Wybierz przedział obraz maszyny wirtualnej][CR03]

5. <span data-ttu-id="90715-122">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="90715-122">Click **Next**.</span></span> 

6. <span data-ttu-id="90715-123">W hello **ustawienia podstawowej maszyny wirtualnej** okna, wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="90715-123">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="90715-124">**Nazwa maszyny wirtualnej**: Określa nazwę powitania dla nowej maszyny wirtualnej, który musi rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.</span><span class="sxs-lookup"><span data-stu-id="90715-124">**Virtual machine name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="90715-125">**Rozmiar**: Określa liczbę hello rdzeni i tooallocate pamięci dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="90715-125">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="90715-126">**Nazwa użytkownika**: Określa toocreate konto administratora hello zarządzania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="90715-126">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="90715-127">**Hasło** i **Potwierdź**: Określa hello hasło dla konta administratora.</span><span class="sxs-lookup"><span data-stu-id="90715-127">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

   ![Witaj okno Ustawienia podstawowej maszyny wirtualnej][CR04]

7. <span data-ttu-id="90715-129">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="90715-129">Click **Next**.</span></span> 

8. <span data-ttu-id="90715-130">W hello **skojarzonych zasobów** okna, wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="90715-130">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="90715-131">**Grupa zasobów**: Określa hello grupy zasobów dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="90715-131">**Resource group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="90715-132">Wybierz jedną z hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="90715-132">Select one of hello following options:</span></span>
      * <span data-ttu-id="90715-133">**Utwórz nowe**: Określa, że toocreate nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="90715-133">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="90715-134">**Użyj istniejącego**: Określa, że tooselect z listy grup zasobów, które są skojarzone z Twoim kontem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="90715-134">**Use existing**: Specifies that you want tooselect from a list of resource groups that are associated with your Azure account.</span></span>

       ![Okno skojarzone zasoby Hello][CR07]

   * <span data-ttu-id="90715-136">**Konto magazynu**: Określa toouse konta magazynu hello do przechowywania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="90715-136">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="90715-137">Można wybrać istniejące konto magazynu lub utworzyć nowe konto.</span><span class="sxs-lookup"><span data-stu-id="90715-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="90715-138">Jeśli wybierzesz **Utwórz nowy**, zostanie wyświetlone następujące okno dialogowe hello:</span><span class="sxs-lookup"><span data-stu-id="90715-138">If you choose **Create New**, hello following dialog box appears:</span></span>

      ![okno dialogowe Tworzenie konta magazynu Hello][CR05]

   * <span data-ttu-id="90715-140">**Sieć wirtualna** i **podsieci**: Określa hello sieci wirtualnej i podsieci, które będą się łączyć maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="90715-140">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="90715-141">Można użyć istniejącej sieci i podsieci, lub można utworzyć nowej sieci i podsieci.</span><span class="sxs-lookup"><span data-stu-id="90715-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="90715-142">W przypadku wybrania **Utwórz nowy**, zostanie wyświetlone następujące okno dialogowe hello:</span><span class="sxs-lookup"><span data-stu-id="90715-142">If you select **Create new**, hello following dialog box appears:</span></span>

      ![okno dialogowe Tworzenie sieci wirtualnej Hello][CR06]

   * <span data-ttu-id="90715-144">**Publiczny adres IP**: Określa adres IP dołączonej do Internetu dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="90715-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="90715-145">Można wybrać toocreate nowego adresu IP, lub Jeśli maszyna wirtualna nie ma publicznego adresu IP, możesz wybrać **(Brak)**.</span><span class="sxs-lookup"><span data-stu-id="90715-145">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="90715-146">**Grupy zabezpieczeń sieci**: Określa opcjonalne zapory sieci dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="90715-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="90715-147">Możesz wybrać istniejącą zapory lub, jeśli maszyna wirtualna nie będzie używać zapory sieciowej, można wybrać **(Brak)**.</span><span class="sxs-lookup"><span data-stu-id="90715-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="90715-148">**Zestaw dostępności**: określa zbiór dostępności opcjonalne, że maszyna wirtualna może należeć do.</span><span class="sxs-lookup"><span data-stu-id="90715-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="90715-149">Można wybrać istniejący zestaw dostępności, Utwórz nowy zestaw dostępności lub, jeśli na komputerze wirtualnym, nie będą należeć tooan zestawu dostępności, wybierz **(Brak)**.</span><span class="sxs-lookup"><span data-stu-id="90715-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong tooan availability set, select **(None)**.</span></span>

9. <span data-ttu-id="90715-150">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="90715-150">Click **Finish**.</span></span>  
    <span data-ttu-id="90715-151">Nowej maszyny wirtualnej jest wyświetlany w oknie narzędzia Eksploratora Azure hello.</span><span class="sxs-lookup"><span data-stu-id="90715-151">Your new virtual machine appears in hello Azure Explorer tool window.</span></span> 

   ![Nową maszynę wirtualną w widoku Eksploratora Azure hello][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="90715-153">Uruchom ponownie maszynę wirtualną w IntelliJ</span><span class="sxs-lookup"><span data-stu-id="90715-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="90715-154">toorestart maszynę wirtualną za pomocą Eksploratora Azure hello w IntelliJ, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="90715-154">toorestart a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="90715-155">W hello **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy hello maszyny wirtualnej, a następnie wybierz **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="90715-155">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![Witaj polecenia ponownego uruchomienia maszyny wirtualnej][RE01]

2. <span data-ttu-id="90715-157">W oknie potwierdzenia powitania kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="90715-157">In hello confirmation window, click **Yes**.</span></span> 

   ![Witaj ponownie uruchom okno potwierdzenia maszyny wirtualnej][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="90715-159">Zamknij maszynę wirtualną w IntelliJ</span><span class="sxs-lookup"><span data-stu-id="90715-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="90715-160">tooshut dół uruchomionej maszyny wirtualnej za pomocą Eksploratora Azure hello w IntelliJ, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="90715-160">tooshut down a running virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="90715-161">W hello **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy hello maszyny wirtualnej, a następnie wybierz **zamknięcia**.</span><span class="sxs-lookup"><span data-stu-id="90715-161">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![polecenie zamknięcia Hello maszyn wirtualnych][SH01]

2. <span data-ttu-id="90715-163">W oknie potwierdzenia powitania kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="90715-163">In hello confirmation window, click **Yes**.</span></span> 

   ![Witaj, zamknij okno potwierdzenia maszyny wirtualnej][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="90715-165">Usuń maszynę wirtualną w IntelliJ</span><span class="sxs-lookup"><span data-stu-id="90715-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="90715-166">toodelete maszynę wirtualną za pomocą Eksploratora Azure hello w IntelliJ, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="90715-166">toodelete a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="90715-167">W hello **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy hello maszyny wirtualnej, a następnie wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="90715-167">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![polecenie Usuń Hello maszyn wirtualnych][DE01]

2. <span data-ttu-id="90715-169">W oknie potwierdzenia powitania kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="90715-169">In hello confirmation window, click **Yes**.</span></span> 

   ![Witaj usunąć okno potwierdzenia maszyny wirtualnej][DE02]

## <a name="next-steps"></a><span data-ttu-id="90715-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="90715-171">Next steps</span></span>
<span data-ttu-id="90715-172">Aby uzyskać więcej informacji na temat rozmiarów maszyn wirtualnych platformy Azure i cenach Zobacz hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="90715-172">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="90715-173">Rozmiary maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="90715-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="90715-174">[Rozmiary maszyn wirtualnych systemu Windows na platformie Azure]</span><span class="sxs-lookup"><span data-stu-id="90715-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="90715-175">[Rozmiary maszyn wirtualnych systemu Linux na platformie Azure]</span><span class="sxs-lookup"><span data-stu-id="90715-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="90715-176">Cennik maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="90715-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="90715-177">[Cennik maszyn wirtualnych systemu Windows]</span><span class="sxs-lookup"><span data-stu-id="90715-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="90715-178">[Cennik maszyn wirtualnych systemu Linux]</span><span class="sxs-lookup"><span data-stu-id="90715-178">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="90715-179">Aby uzyskać więcej informacji o hello narzędzi Azure Java IDEs zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="90715-179">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="90715-180">[Azure zestawu narzędzi dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="90715-180">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="90715-181">[What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="90715-181">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="90715-182">[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="90715-182">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="90715-183">[Instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="90715-183">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="90715-184">[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]</span><span class="sxs-lookup"><span data-stu-id="90715-184">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="90715-185">[Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="90715-185">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="90715-186">[What's new in hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="90715-186">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="90715-187">[Instalowanie hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="90715-187">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="90715-188">[logowania instrukcje dotyczące hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="90715-188">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="90715-189">[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="90715-189">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="90715-190">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center] i [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="90715-190">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalowanie hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[logowania instrukcje dotyczące hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[What's new in hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/

[Rozmiary maszyn wirtualnych systemu Windows na platformie Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Rozmiary maszyn wirtualnych systemu Linux na platformie Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Cennik maszyn wirtualnych systemu Windows]: /pricing/details/virtual-machines/windows/
[Cennik maszyn wirtualnych systemu Linux]: /pricing/details/virtual-machines/linux/


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
