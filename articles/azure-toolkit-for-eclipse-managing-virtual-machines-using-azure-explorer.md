---
title: "aaaManage maszyn wirtualnych przy użyciu hello Eksploratora Azure dla programu Eclipse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage maszynach wirtualnych platformy Azure przy użyciu hello Explorer Azure dla programu Eclipse."
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
ms.openlocfilehash: aa83ec7546a0a8514842723b51ce8a5af81f98f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="94699-103">Zarządzania maszynami wirtualnymi przy użyciu hello Eksploratora Azure dla programu Eclipse</span><span class="sxs-lookup"><span data-stu-id="94699-103">Manage virtual machines by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="94699-104">Hello Eksploratora Azure, która jest częścią zestawu narzędzi platformy Azure dla programu Eclipse hello, zapewnia Java deweloperom łatwe w użyciu rozwiązanie do zarządzania maszynami wirtualnymi na koncie Azure z wewnątrz hello Eclipse zintegrowane środowisko programistyczne (IDE).</span><span class="sxs-lookup"><span data-stu-id="94699-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="94699-105">Utwórz maszynę wirtualną w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="94699-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="94699-106">toocreate maszynę wirtualną za pomocą Eksploratora Azure hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="94699-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="94699-107">Zaloguj się tooyour konto platformy Azure przy użyciu hello [instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse].</span><span class="sxs-lookup"><span data-stu-id="94699-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="94699-108">W hello **Eksploratora Azure** wyświetlić, rozwiń węzeł hello **Azure** węzła, kliknij prawym przyciskiem myszy **maszyn wirtualnych**, a następnie kliknij przycisk **Utwórz maszynę Wirtualną**.</span><span class="sxs-lookup"><span data-stu-id="94699-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   <span data-ttu-id="94699-109">![Witaj polecenia Utwórz maszynę Wirtualną][CR01]</span><span class="sxs-lookup"><span data-stu-id="94699-109">![hello Create VM command][CR01]</span></span>  
   <span data-ttu-id="94699-110">Witaj **tworzenia nowej maszyny wirtualnej** zostanie otwarty Kreator.</span><span class="sxs-lookup"><span data-stu-id="94699-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="94699-111">W hello **Wybierz subskrypcję** okna, wybierz subskrypcję, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="94699-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Witaj wybierz okno subskrypcji][CR02]

4. <span data-ttu-id="94699-113">W hello **Wybieranie obrazu maszyny wirtualnej** okna, wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="94699-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="94699-114">**Lokalizacja**: Określa, gdzie można utworzyć maszyny wirtualnej (na przykład *zachodnie stany USA*).</span><span class="sxs-lookup"><span data-stu-id="94699-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="94699-115">**Wydawca**: Określa hello wydawcy, który utworzył obraz powitania użyjesz toocreate maszyny wirtualnej (na przykład *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="94699-115">**Publisher**: Specifies hello publisher that created hello image you'll use toocreate your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="94699-116">**Oferują**: Określa maszyny wirtualnej hello oferty toouse hello wybranego wydawcy (na przykład *JDK*).</span><span class="sxs-lookup"><span data-stu-id="94699-116">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="94699-117">**Jednostka SKU**: Określa hello składowania jednostka SKU toouse z wybranej oferty hello (na przykład *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="94699-117">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="94699-118">**Wersja #**: Określa, która wersja hello wybrane toouse jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="94699-118">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

    ![Witaj Wybierz przedział obraz maszyny wirtualnej][CR03]

5. <span data-ttu-id="94699-120">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="94699-120">Click **Next**.</span></span>

6. <span data-ttu-id="94699-121">W hello **ustawienia podstawowej maszyny wirtualnej** okna, wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="94699-121">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="94699-122">**Nazwa maszyny wirtualnej**: Określa nazwę powitania dla nowej maszyny wirtualnej, który musi rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.</span><span class="sxs-lookup"><span data-stu-id="94699-122">**Virtual Machine Name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="94699-123">**Rozmiar**: Określa liczbę hello rdzeni i tooallocate pamięci dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="94699-123">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="94699-124">**Nazwa użytkownika**: Określa toocreate konto administratora hello zarządzania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="94699-124">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="94699-125">**Hasło** i **Potwierdź**: Określa hello hasło dla konta administratora.</span><span class="sxs-lookup"><span data-stu-id="94699-125">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

    ![Witaj okno Ustawienia podstawowej maszyny wirtualnej][CR04]

7. <span data-ttu-id="94699-127">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="94699-127">Click **Next**.</span></span>

8. <span data-ttu-id="94699-128">W hello **utworzyć nowe konto magazynu** okna, wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="94699-128">In hello **Create New Storage Account** window, enter hello following information:</span></span>

   * <span data-ttu-id="94699-129">**Grupa zasobów**: Określa hello grupy zasobów dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="94699-129">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="94699-130">Wybierz jedną z hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="94699-130">Select one of hello following options:</span></span>
      * <span data-ttu-id="94699-131">**Utwórz nowe**: Określa, że toocreate nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="94699-131">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="94699-132">**Użyj istniejącego**: Określa, że tooselect grupę zasobów, która jest już skojarzona z Twoim kontem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="94699-132">**Use existing**: Specifies that you want tooselect a resource group that is already associated with your Azure account.</span></span>

      ![okno dialogowe Tworzenie nowego konta magazynu Hello][CR05]

   * <span data-ttu-id="94699-134">**Konto magazynu**: Określa toouse konta magazynu hello do przechowywania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="94699-134">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="94699-135">Możesz użyć istniejącego konta magazynu lub utworzyć nowe konto.</span><span class="sxs-lookup"><span data-stu-id="94699-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="94699-136">**Sieć wirtualna** i **podsieci**: Określa hello sieci wirtualnej i podsieci, które będą się łączyć maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="94699-136">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="94699-137">Można użyć istniejącej sieci i podsieci, lub można utworzyć nowej sieci i podsieci.</span><span class="sxs-lookup"><span data-stu-id="94699-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="94699-138">W przypadku wybrania **Utwórz nowy**, hello następujące okno dialogowe jest wyświetlane:</span><span class="sxs-lookup"><span data-stu-id="94699-138">If you select **Create new**, hello following dialog box is displayed:</span></span>

      ![Utwórz nową sieć wirtualną Hello — okno dialogowe][CR06]

9. <span data-ttu-id="94699-140">W hello **skojarzonych zasobów** okna, wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="94699-140">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="94699-141">**Publiczny adres IP**: Określa adres IP dołączonej do Internetu dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="94699-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="94699-142">Można wybrać toocreate nowego adresu IP, lub Jeśli maszyna wirtualna nie ma publicznego adresu IP, możesz wybrać **(Brak)**.</span><span class="sxs-lookup"><span data-stu-id="94699-142">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="94699-143">**Grupy zabezpieczeń sieci**: Określa opcjonalne zapory sieci dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="94699-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="94699-144">Możesz wybrać istniejącą zapory lub, jeśli maszyna wirtualna nie będzie używać zapory sieciowej, można wybrać **(Brak)**.</span><span class="sxs-lookup"><span data-stu-id="94699-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="94699-145">**Zestaw dostępności**: określa zbiór dostępności opcjonalne, że maszyna wirtualna może należeć do.</span><span class="sxs-lookup"><span data-stu-id="94699-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="94699-146">Możesz wybrać istniejący zestaw dostępności lub utworzyć nowy zbiór dostępności, lub Jeśli maszyna wirtualna nie będą należeć tooan zestawu dostępności, możesz wybrać **(Brak)**.</span><span class="sxs-lookup"><span data-stu-id="94699-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong tooan availability set, you can select **(None)**.</span></span>

   ![Okno skojarzone zasoby Hello][CR07]

9. <span data-ttu-id="94699-148">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="94699-148">Click **Finish**.</span></span>  
  <span data-ttu-id="94699-149">Nowej maszyny wirtualnej jest wyświetlany w oknie narzędzia Eksploratora Azure hello.</span><span class="sxs-lookup"><span data-stu-id="94699-149">Your new virtual machine is displayed in hello Azure Explorer tool window.</span></span>

   ![Nowej maszyny wirtualnej][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="94699-151">Uruchom ponownie maszynę wirtualną w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="94699-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="94699-152">toorestart maszynę wirtualną za pomocą hello Eksploratora Azure w programie Eclipse hello następujące:</span><span class="sxs-lookup"><span data-stu-id="94699-152">toorestart a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="94699-153">W hello **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy hello maszyny wirtualnej, a następnie wybierz **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="94699-153">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![Witaj polecenia ponownego uruchomienia maszyny wirtualnej][RE01]

2. <span data-ttu-id="94699-155">W oknie potwierdzenia powitania kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="94699-155">In hello confirmation window, click **Yes**.</span></span>

   ![okno potwierdzenia Hello ponownego uruchomienia][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="94699-157">Zamknij maszynę wirtualną w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="94699-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="94699-158">tooshut dół uruchomionej maszyny wirtualnej za pomocą hello Eksploratora Azure w programie Eclipse hello następujące:</span><span class="sxs-lookup"><span data-stu-id="94699-158">tooshut down a running virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="94699-159">W hello **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy hello maszyny wirtualnej, a następnie wybierz **zamknięcia**.</span><span class="sxs-lookup"><span data-stu-id="94699-159">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![polecenie zamknięcia Hello maszyn wirtualnych][SH01]

2. <span data-ttu-id="94699-161">W oknie potwierdzenia powitania kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="94699-161">In hello confirmation window, click **Yes**.</span></span>

   ![okno potwierdzenia Hello zamykania maszyn wirtualnych][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="94699-163">Usuń maszynę wirtualną w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="94699-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="94699-164">toodelete maszynę wirtualną za pomocą hello Eksploratora Azure w programie Eclipse hello następujące:</span><span class="sxs-lookup"><span data-stu-id="94699-164">toodelete a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="94699-165">W hello **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy hello maszyny wirtualnej, a następnie wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="94699-165">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![polecenie Usuń Hello maszyn wirtualnych][DE01]

2. <span data-ttu-id="94699-167">W oknie potwierdzenia powitania kliknij **tak**.</span><span class="sxs-lookup"><span data-stu-id="94699-167">In hello confirmation window, click **Yes**.</span></span>

   ![okno potwierdzenia Hello usuwanie maszyny wirtualnej][DE02]

## <a name="next-steps"></a><span data-ttu-id="94699-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="94699-169">Next steps</span></span>
<span data-ttu-id="94699-170">Aby uzyskać więcej informacji na temat rozmiarów maszyn wirtualnych platformy Azure i cenach Zobacz hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="94699-170">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="94699-171">Rozmiary maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="94699-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="94699-172">[Rozmiary maszyn wirtualnych systemu Windows na platformie Azure]</span><span class="sxs-lookup"><span data-stu-id="94699-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="94699-173">[Rozmiary maszyn wirtualnych systemu Linux na platformie Azure]</span><span class="sxs-lookup"><span data-stu-id="94699-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="94699-174">Cennik maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="94699-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="94699-175">[Cennik maszyn wirtualnych systemu Windows]</span><span class="sxs-lookup"><span data-stu-id="94699-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="94699-176">[Cennik maszyn wirtualnych systemu Linux]</span><span class="sxs-lookup"><span data-stu-id="94699-176">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="94699-177">Aby uzyskać więcej informacji o hello narzędzi Azure Java IDEs zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="94699-177">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="94699-178">[Azure zestawu narzędzi dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="94699-178">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="94699-179">[What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="94699-179">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="94699-180">[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="94699-180">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="94699-181">[instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="94699-181">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="94699-182">[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]</span><span class="sxs-lookup"><span data-stu-id="94699-182">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="94699-183">[Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="94699-183">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="94699-184">[What's new in hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="94699-184">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="94699-185">[Instalowanie hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="94699-185">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="94699-186">[Logowanie instrukcje dotyczące hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="94699-186">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="94699-187">[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="94699-187">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="94699-188">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center] i [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="94699-188">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

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

[Rozmiary maszyn wirtualnych systemu Windows na platformie Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Rozmiary maszyn wirtualnych systemu Linux na platformie Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Cennik maszyn wirtualnych systemu Windows]: /pricing/details/virtual-machines/windows/
[Cennik maszyn wirtualnych systemu Linux]: /pricing/details/virtual-machines/linux/

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
