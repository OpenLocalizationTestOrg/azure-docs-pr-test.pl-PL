---
title: "Jak zainstalować Linux głównego serwera docelowego dla trybu failover z platformy Azure do środowiska lokalnego | Dokumentacja firmy Microsoft"
description: "Przed ponownej ochrony maszyny wirtualnej systemu Linux, należy Linux głównego serwera docelowego. Dowiedz się, jak zainstalować jedną."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 5341e3e56e0c366079958dd9a885f6ee3e8436cb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="fa1f4-104">Zainstaluj serwer główny cel systemu Linux</span><span class="sxs-lookup"><span data-stu-id="fa1f4-104">Install a Linux master target server</span></span>
<span data-ttu-id="fa1f4-105">Po przejścia w tryb failover maszyn wirtualnych, możesz w trybie wstecz maszyn wirtualnych do lokacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-105">After you fail over your virtual machines, you can fail back the virtual machines to the on-premises site.</span></span> <span data-ttu-id="fa1f4-106">Aby wykonaj powrót po awarii, musisz Włącz ponownie ochronę maszyny wirtualnej z platformy Azure do lokacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-106">To fail back, you need to reprotect the virtual machine from Azure to the on-premises site.</span></span> <span data-ttu-id="fa1f4-107">W przypadku tego procesu należy lokalny główny serwer docelowy do odbierania ruchu.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-107">For this process, you need an on-premises master target server to receive the traffic.</span></span> 

<span data-ttu-id="fa1f4-108">Chronione maszyny wirtualnej w przypadku maszyny wirtualnej systemu Windows, należy główny cel systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="fa1f4-109">W przypadku maszyny wirtualnej systemu Linux należy główny cel systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="fa1f4-110">Przeczytaj poniższe kroki, aby dowiedzieć się, jak utworzyć i zainstalować główny cel systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-110">Read the following steps to learn how to create and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa1f4-111">Począwszy od wersji 9.10.0 główny serwer docelowy, najnowsze głównego serwera docelowego można zainstalować tylko na serwerze Ubuntu 16.04.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-111">Starting with release of the 9.10.0 master target server, the latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="fa1f4-112">Nowe instalacje nie są dozwolone w CentOS6.6 serwerów.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="fa1f4-113">Jednak możesz uaktualnić starego głównego serwerów docelowych przy użyciu 9.10.0 wersji.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-113">However, you can continue to upgrade your old master target servers by using the 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="fa1f4-114">Omówienie</span><span class="sxs-lookup"><span data-stu-id="fa1f4-114">Overview</span></span>
<span data-ttu-id="fa1f4-115">Ten artykuł zawiera instrukcje dotyczące sposobu instalowania główny cel systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-115">This article provides instructions for how to install a Linux master target.</span></span>

<span data-ttu-id="fa1f4-116">Opublikuj komentarze lub pytania na końcu tego artykułu lub na [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="fa1f4-116">Post comments or questions at the end of this article or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa1f4-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fa1f4-117">Prerequisites</span></span>

* <span data-ttu-id="fa1f4-118">Aby wybrać host, na którym chcesz wdrożyć główny cel, ustal, jeśli powrót po awarii będzie istniejących na lokalnej maszynie wirtualnej lub nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-118">To choose the host on which to deploy the master target, determine if the failback is going to be to an existing on-premises virtual machine or to a new virtual machine.</span></span> 
    * <span data-ttu-id="fa1f4-119">Dla istniejącej maszyny wirtualnej host główny cel powinien mieć dostęp do magazynów danych maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-119">For an existing virtual machine, the host of the master target should have access to the data stores of the virtual machine.</span></span>
    * <span data-ttu-id="fa1f4-120">Jeśli nie istnieje na lokalnej maszynie wirtualnej, maszynę wirtualną w przypadku powrotu po awarii jest tworzony na tym samym hoście jako głównego celu.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-120">If the on-premises virtual machine does not exist, the failback virtual machine is created on the same host as the master target.</span></span> <span data-ttu-id="fa1f4-121">Można wybrać dowolnego hosta ESXi, aby zainstalować główny cel.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-121">You can choose any ESXi host to install the master target.</span></span>
* <span data-ttu-id="fa1f4-122">Główny cel powinna być w sieci, który może komunikować się z serwerem przetwarzania i serwer konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-122">The master target should be on a network that can communicate with the process server and the configuration server.</span></span>
* <span data-ttu-id="fa1f4-123">Wersja głównego elementu docelowego musi być późniejsza niż w przypadku wersji serwera przetwarzania i serwer konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-123">The version of the master target must be equal to or earlier than the versions of the process server and the configuration server.</span></span> <span data-ttu-id="fa1f4-124">Na przykład jeśli wersja serwera konfiguracji jest 9.4, wersja głównego celu może być 9.4 lub 9.3, ale nie 9.5.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-124">For example, if the version of the configuration server is 9.4, the version of the master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="fa1f4-125">Główny cel może być tylko maszyny wirtualne VMware, a nie serwera fizycznego.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-125">The master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-the-master-target-according-to-the-sizing-guidelines"></a><span data-ttu-id="fa1f4-126">Tworzenie głównego celu zgodnie z wytycznymi zmiany rozmiaru</span><span class="sxs-lookup"><span data-stu-id="fa1f4-126">Create the master target according to the sizing guidelines</span></span>

<span data-ttu-id="fa1f4-127">Tworzenie głównego celu zgodnie z wytycznymi następujące zmiany rozmiaru:</span><span class="sxs-lookup"><span data-stu-id="fa1f4-127">Create the master target in accordance with the following sizing guidelines:</span></span>
- <span data-ttu-id="fa1f4-128">**Pamięć RAM**: 6 GB lub więcej</span><span class="sxs-lookup"><span data-stu-id="fa1f4-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="fa1f4-129">**Rozmiar dysku systemu operacyjnego**: 100 GB lub więcej (zainstalować CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="fa1f4-129">**OS disk size**: 100 GB or more (to install CentOS6.6)</span></span>
- <span data-ttu-id="fa1f4-130">**Dodatkowy dysk rozmiar dysku przechowywania**: 1 TB</span><span class="sxs-lookup"><span data-stu-id="fa1f4-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="fa1f4-131">**Rdzenie Procesora**: rdzenie 4 lub więcej</span><span class="sxs-lookup"><span data-stu-id="fa1f4-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="fa1f4-132">Obsługiwane są następujące jądra Ubuntu obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-132">The following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="fa1f4-133">Seria jądra</span><span class="sxs-lookup"><span data-stu-id="fa1f4-133">Kernel Series</span></span>  |<span data-ttu-id="fa1f4-134">Obsługuje maksymalnie</span><span class="sxs-lookup"><span data-stu-id="fa1f4-134">Support up to</span></span>  |
|---------|---------|
|<span data-ttu-id="fa1f4-135">4.4</span><span class="sxs-lookup"><span data-stu-id="fa1f4-135">4.4</span></span>      |<span data-ttu-id="fa1f4-136">4.4.0-81-Generic</span><span class="sxs-lookup"><span data-stu-id="fa1f4-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="fa1f4-137">4.8</span><span class="sxs-lookup"><span data-stu-id="fa1f4-137">4.8</span></span>      |<span data-ttu-id="fa1f4-138">4.8.0-56-Generic</span><span class="sxs-lookup"><span data-stu-id="fa1f4-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="fa1f4-139">4.10</span><span class="sxs-lookup"><span data-stu-id="fa1f4-139">4.10</span></span>     |<span data-ttu-id="fa1f4-140">4.10.0-24-Generic</span><span class="sxs-lookup"><span data-stu-id="fa1f4-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-the-master-target-server"></a><span data-ttu-id="fa1f4-141">Wdrażanie główny serwer docelowy</span><span class="sxs-lookup"><span data-stu-id="fa1f4-141">Deploy the master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="fa1f4-142">Zainstaluj Ubuntu 16.04.2 minimalnego</span><span class="sxs-lookup"><span data-stu-id="fa1f4-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="fa1f4-143">Wziąć pod uwagę następujące kroki, aby zainstalować 64-bitowym systemie operacyjnym Ubuntu 16.04.2.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-143">Take the following the steps to install the Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="fa1f4-144">**Krok 1:** przejdź do [pobrać link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) i wybierz najbardziej duplikatów z których pobierania obrazu ISO Ubuntu 16.04.2 minimalnego 64-bitowych.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-144">**Step 1:** Go to the [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose the closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="fa1f4-145">Zachowaj ISO Ubuntu 16.04.2 minimalnego 64-bitowe w stacji dysków DVD i uruchomić system.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in the DVD drive and start the system.</span></span>

<span data-ttu-id="fa1f4-146">**Krok 2:** wybierz **angielski** jako preferowany język, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Wybierz język](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="fa1f4-148">**Krok 3:** wybierz **zainstalować Ubuntu Server**, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![Wybierz opcję instalacji Ubuntu Server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="fa1f4-150">**Krok 4:** wybierz **angielski** jako preferowany język, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Wybierz preferowany język angielski](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="fa1f4-152">**Krok 5:** wybierz odpowiednią opcję z **strefy czasowej** listy Opcje, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-152">**Step 5:** Select the appropriate option from the **Time Zone** options list, and then select **Enter**.</span></span>

![Wybierz odpowiednią strefę czasową](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="fa1f4-154">**Krok 6:** wybierz **nr** (opcja domyślna), a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-154">**Step 6:** Select **No** (the default option), and then select **Enter**.</span></span>


![Konfigurowanie klawiatury](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="fa1f4-156">**Krok 7:** wybierz **języka angielskiego (US)** jako kraju pochodzenia dla klawiatury, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-156">**Step 7:** Select **English (US)** as the country of origin for the keyboard, and then select **Enter**.</span></span>

![Wybierz kraj pochodzenia stany USA](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="fa1f4-158">**Krok 8:** wybierz **języka angielskiego (US)** jako układu klawiatury, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-158">**Step 8:** Select **English (US)** as the keyboard layout, and then select **Enter**.</span></span>

![Wybierz US English jako układu klawiatury](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="fa1f4-160">**Krok 9:** wprowadź nazwę hosta serwera w **Hostname** , a następnie wybierz **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-160">**Step 9:** Enter the hostname for your server in the **Hostname** box, and then select **Continue**.</span></span>

![Wprowadź nazwę hosta serwera](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="fa1f4-162">**Krok 10.** Aby utworzyć konto użytkownika, wprowadź nazwę użytkownika, a następnie wybierz **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-162">**Step 10:** To create a user account, enter the user name, and then select **Continue**.</span></span>

![Tworzenie konta użytkownika](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="fa1f4-164">**Krok 11.** wprowadź hasło dla nowego konta użytkownika, a następnie wybierz **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-164">**Step 11:** Enter the password for the new user account, and then select **Continue**.</span></span>

![Wprowadź hasło](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="fa1f4-166">**Krok 12.** Potwierdź hasło dla nowego użytkownika, a następnie wybierz **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-166">**Step 12:** Confirm the password for the new user, and then select **Continue**.</span></span>

![Potwierdzenie hasła](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="fa1f4-168">**Krok 13:** wybierz **nr** (opcja domyślna), a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-168">**Step 13:** Select **No** (the default option), and then select **Enter**.</span></span>

![Konfigurowanie użytkowników i haseł](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="fa1f4-170">**Krok 14:** strefy czasowej, która jest wyświetlana jest poprawny, wybierz opcję **tak** (opcja domyślna), a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-170">**Step 14:** If the time zone that's displayed is correct, select **Yes** (the default option), and then select **Enter**.</span></span>

<span data-ttu-id="fa1f4-171">Aby ponownie skonfigurować strefę czasową, wybierz **nr**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-171">To reconfigure your time zone, select **No**.</span></span>

![Skonfiguruj zegar](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="fa1f4-173">**Krok 15.** partycjonowania opcje metody, zaznacz **z przewodnikiem - Użyj cały dysk**, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-173">**Step 15:** From the partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![Wybierz opcję partycjonowania — metoda](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="fa1f4-175">**Krok 16:** wybierz odpowiedni dysk z **wybierz dysk do partycji** opcje, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-175">**Step 16:** Select the appropriate disk from the **Select disk to partition** options, and then select **Enter**.</span></span>


![Wybierz dysk](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="fa1f4-177">**Kroku 17:** wybierz **tak** Aby zapisać zmiany na dysku, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-177">**Step 17:** Select **Yes** to write the changes to disk, and then select **Enter**.</span></span>

![Zapisać zmiany na dysku](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="fa1f4-179">**Krok 18:** wybierz opcję domyślną, zaznacz **Kontynuuj**, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-179">**Step 18:** Select the default option, select **Continue**, and then select **Enter**.</span></span>

![Wybierz opcję domyślną](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="fa1f4-181">**Krok 19:** wybierz opcję odpowiednią dla uaktualnienia w systemie zarządzania, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-181">**Step 19:** Select the appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![Wybierz sposób zarządzania uaktualnień](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="fa1f4-183">Azure Site Recovery główny serwer docelowy wymaga bardzo określonej wersji Ubuntu, dlatego należy upewnić się, że jądra, które aktualizacje są wyłączone dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-183">Because the Azure Site Recovery master target server requires a very specific version of the Ubuntu, you need to ensure that the kernel upgrades are disabled for the virtual machine.</span></span> <span data-ttu-id="fa1f4-184">Jeśli są one włączone regularne uaktualnienia spowodować główny serwer docelowy do nieprawidłowego działania.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-184">If they are enabled, then any regular upgrades cause the master target server to malfunction.</span></span> <span data-ttu-id="fa1f4-185">Upewnij się, że wybrano **nie aktualizacje automatyczne** opcji.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-185">Make sure you select the **No automatic updates** option.</span></span>


<span data-ttu-id="fa1f4-186">**Krok 20:** wybierz opcje domyślne.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="fa1f4-187">Jeśli chcesz openSSH dla połączenia SSH, wybierz opcję **OpenSSH serwera** opcji, a następnie wybierz **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-187">If you want openSSH for SSH connect, select the **OpenSSH server** option, and then select **Continue**.</span></span>

![Wybierz oprogramowanie](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="fa1f4-189">**Krok 21:** wybierz **tak**, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![Moduł ładujący rozruchu CHODNIKÓW instalacji](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="fa1f4-191">**Krok 22:** wybierz odpowiednie urządzenie do instalacji moduł ładujący rozruchu (najlepiej **/dev/sda**), a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-191">**Step 22:** Select the appropriate device for the boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![Wybierz urządzenie na potrzeby instalacji moduł ładujący rozruchu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="fa1f4-193">**Krok 23:** wybierz **Kontynuuj**, a następnie wybierz **Enter** do zakończenia instalacji.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-193">**Step 23:** Select **Continue**, and then select **Enter** to finish the installation.</span></span>

![Zakończenie instalacji](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="fa1f4-195">Po zakończeniu instalacji, zaloguj się do maszyny Wirtualnej z nowymi poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-195">After the installation has finished, sign in to the VM with the new user credentials.</span></span> <span data-ttu-id="fa1f4-196">(Zobacz **kroku 10** Aby uzyskać więcej informacji.)</span><span class="sxs-lookup"><span data-stu-id="fa1f4-196">(Refer to **Step 10** for more information.)</span></span>

<span data-ttu-id="fa1f4-197">Wykonaj kroki opisane na poniższym zrzucie ekranu, aby ustawić hasła użytkownika ROOT.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-197">Take the steps that are described in the following screenshot to set the ROOT user password.</span></span> <span data-ttu-id="fa1f4-198">Następnie zaloguj się jako użytkownik ROOT.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-198">Then sign in as ROOT user.</span></span>

![Ustaw główny hasło użytkownika](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-the-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="fa1f4-200">Przygotowuje komputer do konfiguracji jako główny serwer docelowy</span><span class="sxs-lookup"><span data-stu-id="fa1f4-200">Prepare the machine for configuration as a master target server</span></span>
<span data-ttu-id="fa1f4-201">Następnie przygotowuje komputer do konfiguracji jako główny serwer docelowy.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-201">Next, prepare the machine for configuration as a master target server.</span></span>

<span data-ttu-id="fa1f4-202">Aby uzyskać identyfikator dla każdego dysku twardego SCSI maszyny wirtualnej systemu Linux, Włącz **dysku. EnableUUID = TRUE** parametru.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-202">To get the ID for each SCSI hard disk in a Linux virtual machine, enable the **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="fa1f4-203">Aby włączyć ten parametr, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fa1f4-203">To enable this parameter, take the following steps:</span></span>

1. <span data-ttu-id="fa1f4-204">Zamknij maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="fa1f4-205">Kliknij prawym przyciskiem myszy wpis dla maszyny wirtualnej w okienku po lewej stronie, a następnie wybierz **Edytuj ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-205">Right-click the entry for the virtual machine in the left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="fa1f4-206">Wybierz **opcje** kartę.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-206">Select the **Options** tab.</span></span>

4. <span data-ttu-id="fa1f4-207">W okienku po lewej stronie wybierz **zaawansowane** > **ogólne**, a następnie wybierz **parametry konfiguracji** przycisk w prawej dolnej części ekranu.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-207">In the left pane, select **Advanced** > **General**, and then select the **Configuration Parameters** button on the lower-right part of the screen.</span></span>

    ![Karta Opcje](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="fa1f4-209">**Parametry konfiguracji** opcja jest niedostępna, gdy komputer jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-209">The **Configuration Parameters** option is not available when the machine is running.</span></span> <span data-ttu-id="fa1f4-210">Aby uaktywnić na tej karcie, zamknij maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-210">To make this tab active, shut down the virtual machine.</span></span>

5. <span data-ttu-id="fa1f4-211">Zobacz, czy wiersz z **dysku. EnableUUID** już istnieje.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="fa1f4-212">Jeśli wartość istnieje i ma ustawioną wartość **False**, zmień wartość na **True**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-212">If the value exists and is set to **False**, change the value to **True**.</span></span> <span data-ttu-id="fa1f4-213">(Wartości nie jest rozróżniana).</span><span class="sxs-lookup"><span data-stu-id="fa1f4-213">(The values are not case-sensitive.)</span></span>

    - <span data-ttu-id="fa1f4-214">Jeśli wartość istnieje i ma ustawioną wartość **True**, wybierz pozycję **anulować**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-214">If the value exists and is set to **True**, select **Cancel**.</span></span>

    - <span data-ttu-id="fa1f4-215">Jeśli wartość nie istnieje, wybierz **Dodaj wiersz**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-215">If the value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="fa1f4-216">W kolumnie Nazwa Dodaj **dysku. EnableUUID**, a następnie ustaw wartość **TRUE**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-216">In the name column, add **disk.EnableUUID**, and then set the value to **TRUE**.</span></span>

    ![Sprawdzanie Określa, czy na dysku. EnableUUID już istnieje.](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="fa1f4-218">Wyłącz uaktualnienia jądra</span><span class="sxs-lookup"><span data-stu-id="fa1f4-218">Disable kernel upgrades</span></span>

<span data-ttu-id="fa1f4-219">Azure Site Recovery główny serwer docelowy wymaga bardzo określonych wersji systemu Ubuntu, upewnij się, że uaktualnienia jądra są wyłączone dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-219">Azure Site Recovery master target server requires a very specific version of the Ubuntu, ensure that the kernel upgrades are disabled for the virtual machine.</span></span>

<span data-ttu-id="fa1f4-220">Jeśli uaktualnienia jądra są włączone, regularne uaktualnienia spowodować główny serwer docelowy do nieprawidłowego działania.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-220">If kernel upgrades are enabled, then any regular upgrades cause the master target server to malfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="fa1f4-221">Pobieranie i instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="fa1f4-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="fa1f4-222">Upewnij się, że masz połączenie z Internetem na pobieranie i instalowanie dodatkowych pakietów.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-222">Make sure that you have Internet connectivity to download and install additional packages.</span></span> <span data-ttu-id="fa1f4-223">Jeśli nie masz połączenie z Internetem, musisz ręcznie te pakiety RPM Znajdź i zainstaluj je.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-223">If you don't have Internet connectivity, you need to manually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-the-installer-for-setup"></a><span data-ttu-id="fa1f4-224">Pobierz Instalator dla Instalatora</span><span class="sxs-lookup"><span data-stu-id="fa1f4-224">Get the installer for setup</span></span>

<span data-ttu-id="fa1f4-225">Jeśli urządzenie docelowe głównej ma połączenie z Internetem, można użyć następujących kroków pobrać Instalatora.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-225">If your master target has Internet connectivity, you can use the following steps to download the installer.</span></span> <span data-ttu-id="fa1f4-226">W przeciwnym razie należy skopiować Instalator z serwera przetwarzania, a następnie zainstaluj go.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-226">Otherwise, you can copy the installer from the process server and then install it.</span></span>

#### <a name="download-the-master-target-installation-packages"></a><span data-ttu-id="fa1f4-227">Pobierz pakiety instalacyjne główny serwer docelowy</span><span class="sxs-lookup"><span data-stu-id="fa1f4-227">Download the master target installation packages</span></span>

<span data-ttu-id="fa1f4-228">[Pobrać najnowsze oprogramowanie instalacji główny cel Linux](https://aka.ms/latestlinuxmobsvc).</span><span class="sxs-lookup"><span data-stu-id="fa1f4-228">[Download the latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="fa1f4-229">Aby go pobrać przy użyciu systemu Linux, wpisz:</span><span class="sxs-lookup"><span data-stu-id="fa1f4-229">To download it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="fa1f4-230">Upewnij się, można pobrać i Rozpakuj Instalatora w katalogu macierzystym.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-230">Make sure that you download and unzip the installer in your home directory.</span></span> <span data-ttu-id="fa1f4-231">Jeśli plików do **/usr/Local**, instalacja zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-231">If you unzip to **/usr/Local**, then the installation  fails.</span></span>


#### <a name="access-the-installer-from-the-process-server"></a><span data-ttu-id="fa1f4-232">Dostęp do Instalatora z serwera przetwarzania</span><span class="sxs-lookup"><span data-stu-id="fa1f4-232">Access the installer from the process server</span></span>

1. <span data-ttu-id="fa1f4-233">Na serwerze przetwarzania, przejdź do **\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository C:\Program Files (x86)**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-233">On the process server, go to **C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="fa1f4-234">Skopiuj plik Instalatora wymagane z serwera przetwarzania i zapisz go jako **latestlinuxmobsvc.tar.gz** w katalogu macierzystym.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-234">Copy the required installer file from the process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="fa1f4-235">Zastosuj zmiany konfiguracji niestandardowej</span><span class="sxs-lookup"><span data-stu-id="fa1f4-235">Apply custom configuration changes</span></span>

<span data-ttu-id="fa1f4-236">Aby zastosować zmiany konfiguracji niestandardowej, należy użyć następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fa1f4-236">To apply custom configuration changes, use the following steps:</span></span>


1. <span data-ttu-id="fa1f4-237">Uruchom następujące polecenie, aby untar dane binarne.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-237">Run the following command to untar the binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Zrzut ekranu przedstawiający polecenia do uruchomienia](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="fa1f4-239">Uruchom następujące polecenie, aby udzielić zezwolenia.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-239">Run the following command to give permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="fa1f4-240">Uruchom następujące polecenie, aby uruchomić skrypt.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-240">Run the following command to run the script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="fa1f4-241">Uruchom skrypt tylko raz na serwerze.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-241">Run the script only once on the server.</span></span> <span data-ttu-id="fa1f4-242">Zamknij serwer.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-242">Shut down the server.</span></span> <span data-ttu-id="fa1f4-243">Następnie uruchom ponownie serwer po dodaniu dysku, zgodnie z opisem w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-243">Then restart the server after you add a disk, as described in the next section.</span></span>

### <a name="add-a-retention-disk-to-the-linux-master-target-virtual-machine"></a><span data-ttu-id="fa1f4-244">Dodaj dysk przechowywania do głównej docelowej maszyny wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="fa1f4-244">Add a retention disk to the Linux master target virtual machine</span></span>

<span data-ttu-id="fa1f4-245">Wykonaj następujące kroki, aby utworzyć dysk przechowywania:</span><span class="sxs-lookup"><span data-stu-id="fa1f4-245">Use the following steps to create a retention disk:</span></span>

1. <span data-ttu-id="fa1f4-246">Dołącz nowy dysk 1 TB do głównej docelowej maszyny wirtualnej systemu Linux, a następnie uruchomienie maszyny.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-246">Attach a new 1-TB disk to the Linux master target virtual machine, and then start the machine.</span></span>

2. <span data-ttu-id="fa1f4-247">Użyj **wielościeżkowe -ll** polecenie, aby dowiedzieć się wielościeżkowe identyfikator dysku przechowywania.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-247">Use the **multipath -ll** command to learn the multipath ID of the retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![Wielościeżkowe identyfikator dysku przechowywania](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="fa1f4-249">Sformatuj dysk, a następnie utworzyć systemu plików na nowym dysku.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-249">Format the drive, and then create a file system on the new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Tworzenie system plików na dysku](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="fa1f4-251">Po utworzeniu systemu plików, należy zainstalować dysk przechowywania.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-251">After you create the file system, mount the retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Instalowanie dysku przechowywania](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="fa1f4-253">Utwórz **fstab** wejścia, należy zainstalować dysk przechowywania, przy każdym uruchomieniu systemu.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-253">Create the **fstab** entry to mount the retention drive every time the system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="fa1f4-254">Wybierz **Wstaw** aby rozpocząć edytowanie pliku.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-254">Select **Insert** to begin editing the file.</span></span> <span data-ttu-id="fa1f4-255">Utwórz nowy wiersz, a następnie wstaw następujący tekst.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-255">Create a new line, and then insert the following text.</span></span> <span data-ttu-id="fa1f4-256">Edytuj identyfikator wielościeżkowe dysku, na podstawie Identyfikatora wielościeżkowe wyróżnione z poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-256">Edit the disk multipath ID based on the highlighted multipath ID from the previous command.</span></span>

    <span data-ttu-id="fa1f4-257"> **/dev/mapowania/ <Retention disks multipath id> /mnt/rw ext4 przechowywania 0 0**</span><span class="sxs-lookup"><span data-stu-id="fa1f4-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="fa1f4-258">Wybierz **Esc**, a następnie wpisz **: wq** (zapisać i zamknąć) aby zamknąć okno edytora.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-258">Select **Esc**, and then type **:wq** (write and quit) to close the editor window.</span></span>

### <a name="install-the-master-target"></a><span data-ttu-id="fa1f4-259">Zainstaluj główny cel</span><span class="sxs-lookup"><span data-stu-id="fa1f4-259">Install the master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa1f4-260">Wersja główny serwer docelowy musi być późniejsza niż w przypadku wersji serwera przetwarzania i serwer konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-260">The version of the master target server must be equal to or earlier than the versions of the process server and the configuration server.</span></span> <span data-ttu-id="fa1f4-261">Jeśli ten warunek nie jest spełniony, ponownej ochrony zakończy się pomyślnie, ale replikacja nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="fa1f4-262">Przed zainstalowaniem głównego serwera docelowego sprawdź, czy **/etc/hosts** pliku na maszynie wirtualnej zawiera wpisy, które mapują lokalną nazwą hosta do adresów IP, które są skojarzone z wszystkich kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-262">Before you install the master target server, check that the **/etc/hosts** file on the virtual machine contains entries that map the local hostname to the IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="fa1f4-263">Kopiuj hasło z **Recovery\private\connection.passphrase witryny Azure C:\ProgramData\Microsoft** na serwerze konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-263">Copy the passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on the configuration server.</span></span> <span data-ttu-id="fa1f4-264">Następnie zapisz go jako **passphrase.txt** w tym samym katalogu lokalnego, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="fa1f4-264">Then save it as **passphrase.txt** in the same local directory by running the following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="fa1f4-265">Przykład:</span><span class="sxs-lookup"><span data-stu-id="fa1f4-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="fa1f4-266">Należy pamiętać, adres IP serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-266">Note the configuration server's IP address.</span></span> <span data-ttu-id="fa1f4-267">Należy go w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-267">You need it in the next step.</span></span>

3. <span data-ttu-id="fa1f4-268">Uruchom następujące polecenie, aby zainstalować główny serwer docelowy i Zarejestruj serwer z serwerem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-268">Run the following command to install the master target server and register the server with the configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="fa1f4-269">Przykład:</span><span class="sxs-lookup"><span data-stu-id="fa1f4-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="fa1f4-270">Poczekaj na zakończenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-270">Wait until the script finishes.</span></span> <span data-ttu-id="fa1f4-271">Czy główny cel rejestruje pomyślnie, główny cel są dostępne w **infrastruktura usługi Site Recovery** strony portalu.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-271">If the master target registers sucessfully, the master target is listed on the **Site Recovery Infrastructure** page of the portal.</span></span>


#### <a name="install-the-master-target-by-using-interactive-installation"></a><span data-ttu-id="fa1f4-272">Zainstaluj główny cel, używając instalacja interakcyjna</span><span class="sxs-lookup"><span data-stu-id="fa1f4-272">Install the master target by using interactive installation</span></span>

1. <span data-ttu-id="fa1f4-273">Uruchom następujące polecenie, aby zainstalować główny cel.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-273">Run the following command to install the master target.</span></span> <span data-ttu-id="fa1f4-274">W roli agenta, wybierz opcję **docelowego elementu głównego**.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-274">For the agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="fa1f4-275">Wybierz domyślną lokalizację instalacji, a następnie wybierz **Enter** aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-275">Choose the default location for installation, and then select **Enter** to continue.</span></span>

    ![Wybieranie domyślnej lokalizacji instalacji główny serwer docelowy](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="fa1f4-277">Po zakończeniu instalacji należy zarejestrować serwer konfiguracji przy użyciu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-277">After the installation has finished, register the configuration server by using the command line.</span></span>

1. <span data-ttu-id="fa1f4-278">Zanotuj adres IP serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-278">Note the IP address of the configuration server.</span></span> <span data-ttu-id="fa1f4-279">Należy go w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-279">You need it in the next step.</span></span>

2. <span data-ttu-id="fa1f4-280">Uruchom następujące polecenie, aby zainstalować główny serwer docelowy i Zarejestruj serwer z serwerem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-280">Run the following command to install the master target server and register the server with the configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="fa1f4-281">Przykład:</span><span class="sxs-lookup"><span data-stu-id="fa1f4-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="fa1f4-282">Poczekaj na zakończenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-282">Wait until the script finishes.</span></span> <span data-ttu-id="fa1f4-283">Czy główny cel został pomyślnie zarejestrowany, główny docelowy są dostępne w **infrastruktura usługi Site Recovery** strony portalu.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-283">If the master target is registered succesfully, the master target is listed on the **Site Recovery Infrastructure** page of the portal.</span></span>


### <a name="upgrade-the-master-target"></a><span data-ttu-id="fa1f4-284">Uaktualnij główny cel</span><span class="sxs-lookup"><span data-stu-id="fa1f4-284">Upgrade the master target</span></span>

<span data-ttu-id="fa1f4-285">Uruchom Instalatora.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-285">Run the installer.</span></span> <span data-ttu-id="fa1f4-286">Automatycznie wykrywa, że agent jest zainstalowany w głównym celu.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-286">It automatically detects that the agent is installed on the master target.</span></span> <span data-ttu-id="fa1f4-287">Aby przeprowadzić uaktualnienie, wybierz **Y**.  Po zakończeniu instalacji sprawdź wersję programu głównego celu zainstalowane za pomocą następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-287">To upgrade, select **Y**.  After the setup has been completed, check the version of the master target installed by using the following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="fa1f4-288">Można stwierdzić, że **wersji** pola zwraca numer wersji głównego celu.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-288">You can see that the **Version** field gives the version number of the master target.</span></span>

### <a name="install-vmware-tools-on-the-master-target-server"></a><span data-ttu-id="fa1f4-289">Zainstaluj narzędzia VMware na głównym serwerze docelowym</span><span class="sxs-lookup"><span data-stu-id="fa1f4-289">Install VMware tools on the master target server</span></span>

<span data-ttu-id="fa1f4-290">Musisz zainstalować narzędzia VMware w głównym celu tak, aby go odnaleźć w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-290">You need to install VMware tools on the master target so that it can discover the data stores.</span></span> <span data-ttu-id="fa1f4-291">Jeśli narzędzia nie są zainstalowane, ekranu ponownej ochrony nie ma na liście w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-291">If the tools are not installed, the reprotect screen isn't listed in the data stores.</span></span> <span data-ttu-id="fa1f4-292">Po zakończeniu instalacji narzędzi VMware należy ponownie uruchomić.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-292">After installation of the VMware tools, you need to restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa1f4-293">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fa1f4-293">Next steps</span></span>
<span data-ttu-id="fa1f4-294">Po instalacji i rejestracji główny cel zawiera finsihed, można wyświetlić głównego celu, które są wyświetlane na **docelowego elementu głównego** sekcji **infrastruktura usługi Site Recovery**, w obszarze Przegląd serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-294">After the installation and registration of the master target has finsihed, you can see the master target appear on the **Master Target** section in **Site Recovery Infrastructure**, under the configuration server overview.</span></span>

<span data-ttu-id="fa1f4-295">Teraz można przystąpić do [przełączonej](site-recovery-how-to-reprotect.md), a następnie powrót po awarii.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="fa1f4-296">Typowe problemy</span><span class="sxs-lookup"><span data-stu-id="fa1f4-296">Common issues</span></span>

* <span data-ttu-id="fa1f4-297">Upewnij się, że nie należy włączać narzędzia Storage vMotion na wszystkie składniki zarządzania, takie jak głównego celu.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="fa1f4-298">Jeśli po pomyślnej ponownej ochrony jest przenoszony główny cel, nie można odłączyć dysków maszyny wirtualnej (VMDKs).</span><span class="sxs-lookup"><span data-stu-id="fa1f4-298">If the master target moves after a successful reprotect, the virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="fa1f4-299">W takim przypadku powrotu po awarii nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-299">In this case, failback fails.</span></span>

* <span data-ttu-id="fa1f4-300">Główny cel nie powinna mieć żadnych migawek na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-300">The master target should not have any snapshots on the virtual machine.</span></span> <span data-ttu-id="fa1f4-301">W przypadku migawki powrotu po awarii nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="fa1f4-302">Z powodu niektórych niestandardowych konfiguracji karty Sieciowej na komputerach niektórych klientów interfejs sieciowy jest wyłączona podczas uruchamiania, a nie można zainicjować agenta głównego celu.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-302">Due to some custom NIC configurations at some customers, the network interface is disabled during startup, and the master target agent cannot initialize.</span></span> <span data-ttu-id="fa1f4-303">Upewnij się, że następujące właściwości są ustawione poprawnie.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-303">Make sure that the following properties are correctly set.</span></span> <span data-ttu-id="fa1f4-304">Sprawdź tych właściwości w sieci Ethernet karty /etc/sysconfig/network-scripts/ifcfg pliku-eth *.</span><span class="sxs-lookup"><span data-stu-id="fa1f4-304">Check these properties in the Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="fa1f4-305">BOOTPROTO = dhcp</span><span class="sxs-lookup"><span data-stu-id="fa1f4-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="fa1f4-306">ONBOOT = tak</span><span class="sxs-lookup"><span data-stu-id="fa1f4-306">ONBOOT=yes</span></span>
