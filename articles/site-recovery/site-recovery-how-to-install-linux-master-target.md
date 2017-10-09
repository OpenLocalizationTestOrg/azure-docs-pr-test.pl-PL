---
title: "tooinstall aaaHow Linux głównego serwera docelowego dla trybu failover z Azure lokalnych tooon | Dokumentacja firmy Microsoft"
description: "Przed ponownej ochrony maszyny wirtualnej systemu Linux, należy Linux głównego serwera docelowego. Dowiedz się, jak tooinstall jeden."
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
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="77609-104">Zainstaluj serwer główny cel systemu Linux</span><span class="sxs-lookup"><span data-stu-id="77609-104">Install a Linux master target server</span></span>
<span data-ttu-id="77609-105">Po przejścia w tryb failover maszyn wirtualnych, może nie powieść wstecz hello maszyn wirtualnych toohello lokalnej lokacji.</span><span class="sxs-lookup"><span data-stu-id="77609-105">After you fail over your virtual machines, you can fail back hello virtual machines toohello on-premises site.</span></span> <span data-ttu-id="77609-106">toofail ponownie, należy maszyny wirtualnej hello tooreprotect z lokacji lokalnej toohello platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="77609-106">toofail back, you need tooreprotect hello virtual machine from Azure toohello on-premises site.</span></span> <span data-ttu-id="77609-107">W przypadku tego procesu należy ruchu główny cel hello tooreceive serwera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="77609-107">For this process, you need an on-premises master target server tooreceive hello traffic.</span></span> 

<span data-ttu-id="77609-108">Chronione maszyny wirtualnej w przypadku maszyny wirtualnej systemu Windows, należy główny cel systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="77609-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="77609-109">W przypadku maszyny wirtualnej systemu Linux należy główny cel systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="77609-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="77609-110">Odczyt hello następujące kroki toolearn jak toocreate i zainstaluj Linux głównych docelowej.</span><span class="sxs-lookup"><span data-stu-id="77609-110">Read hello following steps toolearn how toocreate and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77609-111">Począwszy od wersji hello 9.10.0 główny serwer docelowy, hello najnowsze głównego serwera docelowego można zainstalować tylko na serwerze Ubuntu 16.04.</span><span class="sxs-lookup"><span data-stu-id="77609-111">Starting with release of hello 9.10.0 master target server, hello latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="77609-112">Nowe instalacje nie są dozwolone w CentOS6.6 serwerów.</span><span class="sxs-lookup"><span data-stu-id="77609-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="77609-113">Jednak możesz kontynuować tooupgrade starego głównego serwerów docelowych przy użyciu wersji hello 9.10.0.</span><span class="sxs-lookup"><span data-stu-id="77609-113">However, you can continue tooupgrade your old master target servers by using hello 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="77609-114">Omówienie</span><span class="sxs-lookup"><span data-stu-id="77609-114">Overview</span></span>
<span data-ttu-id="77609-115">Ten artykuł zawiera instrukcje dotyczące jak tooinstall Linux wzorca docelowego.</span><span class="sxs-lookup"><span data-stu-id="77609-115">This article provides instructions for how tooinstall a Linux master target.</span></span>

<span data-ttu-id="77609-116">Opublikuj komentarze lub pytania na końcu hello tym artykułem lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="77609-116">Post comments or questions at hello end of this article or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77609-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="77609-117">Prerequisites</span></span>

* <span data-ttu-id="77609-118">określić toochoose hello hosta, na które toodeploy hello główny cel, jeśli hello powrotu po awarii będzie toobe tooan istniejącymi lokalnymi maszyny wirtualnej lub tooa nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="77609-118">toochoose hello host on which toodeploy hello master target, determine if hello failback is going toobe tooan existing on-premises virtual machine or tooa new virtual machine.</span></span> 
    * <span data-ttu-id="77609-119">Istniejącej maszyny wirtualnej host hello hello główny cel powinny mieć dostępu do magazyny danych toohello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="77609-119">For an existing virtual machine, hello host of hello master target should have access toohello data stores of hello virtual machine.</span></span>
    * <span data-ttu-id="77609-120">Jeśli nie istnieje hello na lokalnej maszynie wirtualnej, hello powrotu po awarii utworzeniu maszyny wirtualnej na powitania sam hosta jako główny serwer docelowy hello.</span><span class="sxs-lookup"><span data-stu-id="77609-120">If hello on-premises virtual machine does not exist, hello failback virtual machine is created on hello same host as hello master target.</span></span> <span data-ttu-id="77609-121">Można wybrać dowolnego hosta ESXi tooinstall hello głównego celu.</span><span class="sxs-lookup"><span data-stu-id="77609-121">You can choose any ESXi host tooinstall hello master target.</span></span>
* <span data-ttu-id="77609-122">główny cel Hello powinna być w sieci, który może komunikować się z serwera przetwarzania hello i powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="77609-122">hello master target should be on a network that can communicate with hello process server and hello configuration server.</span></span>
* <span data-ttu-id="77609-123">Hello hello główny serwer docelowy musi być równy tooor starszych niż hello wersji serwera przetwarzania hello i hello konfiguracji serwera.</span><span class="sxs-lookup"><span data-stu-id="77609-123">hello version of hello master target must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="77609-124">Na przykład jeśli hello wersja serwera konfiguracji hello jest 9.4, wersja hello hello główny serwer docelowy może być 9.4 lub 9.3, ale nie 9.5.</span><span class="sxs-lookup"><span data-stu-id="77609-124">For example, if hello version of hello configuration server is 9.4, hello version of hello master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="77609-125">główny cel Hello może być tylko maszyny wirtualne VMware, a nie serwera fizycznego.</span><span class="sxs-lookup"><span data-stu-id="77609-125">hello master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a><span data-ttu-id="77609-126">Utwórz hello zgodnie z wytycznymi zmiany rozmiaru toohello głównego celu.</span><span class="sxs-lookup"><span data-stu-id="77609-126">Create hello master target according toohello sizing guidelines</span></span>

<span data-ttu-id="77609-127">Tworzenie głównego celu hello zgodnie z hello następujące wytyczne zmiany rozmiaru:</span><span class="sxs-lookup"><span data-stu-id="77609-127">Create hello master target in accordance with hello following sizing guidelines:</span></span>
- <span data-ttu-id="77609-128">**Pamięć RAM**: 6 GB lub więcej</span><span class="sxs-lookup"><span data-stu-id="77609-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="77609-129">**Rozmiar dysku systemu operacyjnego**: 100 GB lub więcej (tooinstall CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="77609-129">**OS disk size**: 100 GB or more (tooinstall CentOS6.6)</span></span>
- <span data-ttu-id="77609-130">**Dodatkowy dysk rozmiar dysku przechowywania**: 1 TB</span><span class="sxs-lookup"><span data-stu-id="77609-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="77609-131">**Rdzenie Procesora**: rdzenie 4 lub więcej</span><span class="sxs-lookup"><span data-stu-id="77609-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="77609-132">Poniższe Hello obsługiwane Ubuntu jądra są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="77609-132">hello following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="77609-133">Seria jądra</span><span class="sxs-lookup"><span data-stu-id="77609-133">Kernel Series</span></span>  |<span data-ttu-id="77609-134">Obsługuje konto zbyt</span><span class="sxs-lookup"><span data-stu-id="77609-134">Support up too</span></span> |
|---------|---------|
|<span data-ttu-id="77609-135">4.4</span><span class="sxs-lookup"><span data-stu-id="77609-135">4.4</span></span>      |<span data-ttu-id="77609-136">4.4.0-81-Generic</span><span class="sxs-lookup"><span data-stu-id="77609-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="77609-137">4.8</span><span class="sxs-lookup"><span data-stu-id="77609-137">4.8</span></span>      |<span data-ttu-id="77609-138">4.8.0-56-Generic</span><span class="sxs-lookup"><span data-stu-id="77609-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="77609-139">4.10</span><span class="sxs-lookup"><span data-stu-id="77609-139">4.10</span></span>     |<span data-ttu-id="77609-140">4.10.0-24-Generic</span><span class="sxs-lookup"><span data-stu-id="77609-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-hello-master-target-server"></a><span data-ttu-id="77609-141">Wdrażanie hello główny serwer docelowy</span><span class="sxs-lookup"><span data-stu-id="77609-141">Deploy hello master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="77609-142">Zainstaluj Ubuntu 16.04.2 minimalnego</span><span class="sxs-lookup"><span data-stu-id="77609-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="77609-143">Zająć powitania po hello kroki tooinstall hello Ubuntu 16.04.2 64-bitowym systemie operacyjnym.</span><span class="sxs-lookup"><span data-stu-id="77609-143">Take hello following hello steps tooinstall hello Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="77609-144">**Krok 1:** Przejdź toohello [pobrać link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) i wybierz polecenie dublowany najbliższego hello z którego Pobierz obraz ISO Ubuntu 16.04.2 minimalnego 64-bitowych.</span><span class="sxs-lookup"><span data-stu-id="77609-144">**Step 1:** Go toohello [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose hello closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="77609-145">Zachowaj ISO Ubuntu 16.04.2 minimalnego 64-bitowe w stacji dysków DVD hello i uruchomić hello system.</span><span class="sxs-lookup"><span data-stu-id="77609-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in hello DVD drive and start hello system.</span></span>

<span data-ttu-id="77609-146">**Krok 2:** wybierz **angielski** jako preferowany język, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77609-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Wybierz język](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="77609-148">**Krok 3:** wybierz **zainstalować Ubuntu Server**, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77609-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![Wybierz opcję instalacji Ubuntu Server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="77609-150">**Krok 4:** wybierz **angielski** jako preferowany język, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77609-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Wybierz preferowany język angielski](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="77609-152">**Krok 5:** wybierz hello odpowiednią opcję z hello **strefy czasowej** listy Opcje, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77609-152">**Step 5:** Select hello appropriate option from hello **Time Zone** options list, and then select **Enter**.</span></span>

![Wybierz odpowiednią strefę czasową hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="77609-154">**Krok 6:** wybierz **nr** (hello opcja domyślna), a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77609-154">**Step 6:** Select **No** (hello default option), and then select **Enter**.</span></span>


![Konfigurowanie hello klawiatury](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="77609-156">**Krok 7:** wybierz **języka angielskiego (US)** jako hello kraj pochodzenia hello klawiatury, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77609-156">**Step 7:** Select **English (US)** as hello country of origin for hello keyboard, and then select **Enter**.</span></span>

![Wybierz kraj hello pochodzenia stany USA](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="77609-158">**Krok 8:** wybierz **języka angielskiego (US)** jako hello układu klawiatury, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77609-158">**Step 8:** Select **English (US)** as hello keyboard layout, and then select **Enter**.</span></span>

![Wybierz US English jako hello układu klawiatury](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="77609-160">**Krok 9:** wprowadź nazwę hosta powitania serwera w hello **Hostname** , a następnie wybierz **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="77609-160">**Step 9:** Enter hello hostname for your server in hello **Hostname** box, and then select **Continue**.</span></span>

![Wprowadź nazwę hosta powitania serwera](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="77609-162">**Krok 10.** toocreate konta użytkownika, wprowadź nazwę użytkownika hello, a następnie wybierz **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="77609-162">**Step 10:** toocreate a user account, enter hello user name, and then select **Continue**.</span></span>

![Tworzenie konta użytkownika](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="77609-164">**Krok 11.** wprowadź hasło hello hello nowego konta użytkownika, a następnie wybierz **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="77609-164">**Step 11:** Enter hello password for hello new user account, and then select **Continue**.</span></span>

![Wprowadź hasło hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="77609-166">**Krok 12.** Potwierdź hasło hello hello nowego użytkownika, a następnie wybierz **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="77609-166">**Step 12:** Confirm hello password for hello new user, and then select **Continue**.</span></span>

![Potwierdzenie hasła hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="77609-168">**Krok 13:** wybierz **nr** (hello opcja domyślna), a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77609-168">**Step 13:** Select **No** (hello default option), and then select **Enter**.</span></span>

![Konfigurowanie użytkowników i haseł](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="77609-170">**Krok 14:** hello strefy czasowej, która jest wyświetlana jest poprawny, wybierz opcję **tak** (hello opcja domyślna), a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77609-170">**Step 14:** If hello time zone that's displayed is correct, select **Yes** (hello default option), and then select **Enter**.</span></span>

<span data-ttu-id="77609-171">tooreconfigure strefy czasowej, wybierz opcję **nr**.</span><span class="sxs-lookup"><span data-stu-id="77609-171">tooreconfigure your time zone, select **No**.</span></span>

![Skonfiguruj zegar hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="77609-173">**Krok 15.** hello partycjonowania opcje metody, zaznacz **z przewodnikiem - Użyj cały dysk**, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77609-173">**Step 15:** From hello partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![Wybierz hello partycjonowania opcji — Metoda](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="77609-175">**Krok 16:** wybierz hello odpowiedniego dysku z hello **wybierz dysk toopartition** opcje, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77609-175">**Step 16:** Select hello appropriate disk from hello **Select disk toopartition** options, and then select **Enter**.</span></span>


![Wybierz dysk hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="77609-177">**Kroku 17:** wybierz **tak** toowrite hello toodisk zmiany, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77609-177">**Step 17:** Select **Yes** toowrite hello changes toodisk, and then select **Enter**.</span></span>

![Zapis hello toodisk zmiany](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="77609-179">**Krok 18:** wybierz opcję domyślną hello, wybierz pozycję **Kontynuuj**, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77609-179">**Step 18:** Select hello default option, select **Continue**, and then select **Enter**.</span></span>

![Wybierz opcję domyślną hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="77609-181">**Krok 19:** wybierz odpowiednią opcję hello uaktualnień w systemie zarządzania, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77609-181">**Step 19:** Select hello appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![Wybierz sposób uaktualnia toomanage](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="77609-183">Hello Azure Site Recovery główny serwer docelowy wymaga bardzo określonej wersji hello Ubuntu, dlatego należy tooensure tego jądra hello, które aktualizacje są wyłączone dla hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="77609-183">Because hello Azure Site Recovery master target server requires a very specific version of hello Ubuntu, you need tooensure that hello kernel upgrades are disabled for hello virtual machine.</span></span> <span data-ttu-id="77609-184">Jeśli są one włączone regularne uaktualnienia spowodować toomalfunction serwera głównego celu hello.</span><span class="sxs-lookup"><span data-stu-id="77609-184">If they are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span> <span data-ttu-id="77609-185">Upewnij się, że wybrano hello **nie aktualizacje automatyczne** opcji.</span><span class="sxs-lookup"><span data-stu-id="77609-185">Make sure you select hello **No automatic updates** option.</span></span>


<span data-ttu-id="77609-186">**Krok 20:** wybierz opcje domyślne.</span><span class="sxs-lookup"><span data-stu-id="77609-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="77609-187">OpenSSH dla połączenia SSH, zaznacz hello **serwera OpenSSH** opcji, a następnie wybierz **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="77609-187">If you want openSSH for SSH connect, select hello **OpenSSH server** option, and then select **Continue**.</span></span>

![Wybierz oprogramowanie](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="77609-189">**Krok 21:** wybierz **tak**, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77609-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![Instalacji hello CHODNIKÓW — moduł ładujący rozruchu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="77609-191">**Krok 22:** wybierz hello odpowiednie urządzenie na potrzeby instalacji moduł ładujący rozruchu hello (najlepiej **/dev/sda**), a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="77609-191">**Step 22:** Select hello appropriate device for hello boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![Wybierz urządzenie na potrzeby instalacji moduł ładujący rozruchu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="77609-193">**Krok 23:** wybierz **Kontynuuj**, a następnie wybierz **Enter** toofinish hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="77609-193">**Step 23:** Select **Continue**, and then select **Enter** toofinish hello installation.</span></span>

![Zakończenie instalacji hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="77609-195">Po zakończeniu instalacji hello, zaloguj się toohello maszyny Wirtualnej z nowymi poświadczeniami użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="77609-195">After hello installation has finished, sign in toohello VM with hello new user credentials.</span></span> <span data-ttu-id="77609-196">(Zobacz zbyt**kroku 10** Aby uzyskać więcej informacji.)</span><span class="sxs-lookup"><span data-stu-id="77609-196">(Refer too**Step 10** for more information.)</span></span>

<span data-ttu-id="77609-197">Czynności hello opisanymi w powitania po hello tooset zrzut ekranu głównego hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="77609-197">Take hello steps that are described in hello following screenshot tooset hello ROOT user password.</span></span> <span data-ttu-id="77609-198">Następnie zaloguj się jako użytkownik ROOT.</span><span class="sxs-lookup"><span data-stu-id="77609-198">Then sign in as ROOT user.</span></span>

![Hasła użytkownika ROOT hello zestawu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="77609-200">Przygotowanie maszyny hello konfiguracji jako główny serwer docelowy</span><span class="sxs-lookup"><span data-stu-id="77609-200">Prepare hello machine for configuration as a master target server</span></span>
<span data-ttu-id="77609-201">Następnie przygotuj maszyny hello konfiguracji jako główny serwer docelowy.</span><span class="sxs-lookup"><span data-stu-id="77609-201">Next, prepare hello machine for configuration as a master target server.</span></span>

<span data-ttu-id="77609-202">Identyfikator hello tooget dla każdego dysku twardego SCSI na maszynie wirtualnej systemu Linux, Włącz hello **dysku. EnableUUID = TRUE** parametru.</span><span class="sxs-lookup"><span data-stu-id="77609-202">tooget hello ID for each SCSI hard disk in a Linux virtual machine, enable hello **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="77609-203">tooenable, które tego parametru hello wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="77609-203">tooenable this parameter, take hello following steps:</span></span>

1. <span data-ttu-id="77609-204">Zamknij maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="77609-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="77609-205">Kliknij prawym przyciskiem myszy wpis hello hello maszyny wirtualnej w okienku po lewej stronie powitania, a następnie wybierz **Edytuj ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="77609-205">Right-click hello entry for hello virtual machine in hello left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="77609-206">Wybierz hello **opcje** kartę.</span><span class="sxs-lookup"><span data-stu-id="77609-206">Select hello **Options** tab.</span></span>

4. <span data-ttu-id="77609-207">Wybierz w okienku po lewej stronie powitania **zaawansowane** > **ogólne**, a następnie wybierz hello **parametry konfiguracji** przycisk na powitania prawej dolnej części ekranu hello.</span><span class="sxs-lookup"><span data-stu-id="77609-207">In hello left pane, select **Advanced** > **General**, and then select hello **Configuration Parameters** button on hello lower-right part of hello screen.</span></span>

    ![Karta Opcje](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="77609-209">Witaj **parametry konfiguracji** opcja jest niedostępna, gdy maszyna hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="77609-209">hello **Configuration Parameters** option is not available when hello machine is running.</span></span> <span data-ttu-id="77609-210">toomake na tej karcie aktywny, zamknij maszynę wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="77609-210">toomake this tab active, shut down hello virtual machine.</span></span>

5. <span data-ttu-id="77609-211">Zobacz, czy wiersz z **dysku. EnableUUID** już istnieje.</span><span class="sxs-lookup"><span data-stu-id="77609-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="77609-212">Jeśli istnieje wartość hello i ustawiono zbyt**False**, zmień wartość hello zbyt**True**.</span><span class="sxs-lookup"><span data-stu-id="77609-212">If hello value exists and is set too**False**, change hello value too**True**.</span></span> <span data-ttu-id="77609-213">(wartości hello nie jest rozróżniana).</span><span class="sxs-lookup"><span data-stu-id="77609-213">(hello values are not case-sensitive.)</span></span>

    - <span data-ttu-id="77609-214">Jeśli istnieje wartość hello i ustawiono zbyt**True**, wybierz pozycję **anulować**.</span><span class="sxs-lookup"><span data-stu-id="77609-214">If hello value exists and is set too**True**, select **Cancel**.</span></span>

    - <span data-ttu-id="77609-215">Jeśli wartość hello nie istnieje, wybierz **Dodaj wiersz**.</span><span class="sxs-lookup"><span data-stu-id="77609-215">If hello value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="77609-216">Witaj kolumny z nazwami, Dodaj **dysku. EnableUUID**, a następnie ustaw wartość hello zbyt**TRUE**.</span><span class="sxs-lookup"><span data-stu-id="77609-216">In hello name column, add **disk.EnableUUID**, and then set hello value too**TRUE**.</span></span>

    ![Sprawdzanie Określa, czy na dysku. EnableUUID już istnieje.](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="77609-218">Wyłącz uaktualnienia jądra</span><span class="sxs-lookup"><span data-stu-id="77609-218">Disable kernel upgrades</span></span>

<span data-ttu-id="77609-219">Azure Site Recovery główny serwer docelowy wymaga bardzo określonej wersji hello Ubuntu, upewnij się, że hello uaktualnienia jądra są wyłączone dla hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="77609-219">Azure Site Recovery master target server requires a very specific version of hello Ubuntu, ensure that hello kernel upgrades are disabled for hello virtual machine.</span></span>

<span data-ttu-id="77609-220">Jeśli uaktualnienia jądra są włączone, regularne uaktualnienia spowodować toomalfunction serwera głównego celu hello.</span><span class="sxs-lookup"><span data-stu-id="77609-220">If kernel upgrades are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="77609-221">Pobieranie i instalowanie dodatkowych pakietów</span><span class="sxs-lookup"><span data-stu-id="77609-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="77609-222">Upewnij się, że masz toodownload połączenie internetowe i zainstalować dodatkowe pakiety.</span><span class="sxs-lookup"><span data-stu-id="77609-222">Make sure that you have Internet connectivity toodownload and install additional packages.</span></span> <span data-ttu-id="77609-223">Jeśli nie masz połączenie z Internetem, należy toomanually te pakiety RPM Znajdź i zainstaluj je.</span><span class="sxs-lookup"><span data-stu-id="77609-223">If you don't have Internet connectivity, you need toomanually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a><span data-ttu-id="77609-224">Pobierz Instalator hello instalacji</span><span class="sxs-lookup"><span data-stu-id="77609-224">Get hello installer for setup</span></span>

<span data-ttu-id="77609-225">Jeśli urządzenie docelowe głównej ma połączenie z Internetem, możesz użyć hello następujące kroki toodownload hello Instalatora.</span><span class="sxs-lookup"><span data-stu-id="77609-225">If your master target has Internet connectivity, you can use hello following steps toodownload hello installer.</span></span> <span data-ttu-id="77609-226">W przeciwnym razie można skopiować hello Instalatora z serwera przetwarzania hello, a następnie zainstaluj go.</span><span class="sxs-lookup"><span data-stu-id="77609-226">Otherwise, you can copy hello installer from hello process server and then install it.</span></span>

#### <a name="download-hello-master-target-installation-packages"></a><span data-ttu-id="77609-227">Pobierz pakiety instalacyjne hello główny serwer docelowy</span><span class="sxs-lookup"><span data-stu-id="77609-227">Download hello master target installation packages</span></span>

<span data-ttu-id="77609-228">[Pobierz hello najnowsze Linux głównego celu instalacji usługi bits](https://aka.ms/latestlinuxmobsvc).</span><span class="sxs-lookup"><span data-stu-id="77609-228">[Download hello latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="77609-229">toodownload go przy użyciu systemu Linux, wpisz:</span><span class="sxs-lookup"><span data-stu-id="77609-229">toodownload it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="77609-230">Upewnij się, można pobrać i Rozpakuj hello Instalatora w katalogu macierzystym.</span><span class="sxs-lookup"><span data-stu-id="77609-230">Make sure that you download and unzip hello installer in your home directory.</span></span> <span data-ttu-id="77609-231">Jeśli Rozpakuj w zbyt**/usr/Local**, hello instalacja zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="77609-231">If you unzip too**/usr/Local**, then hello installation  fails.</span></span>


#### <a name="access-hello-installer-from-hello-process-server"></a><span data-ttu-id="77609-232">Instalator hello dostęp z serwera przetwarzania hello</span><span class="sxs-lookup"><span data-stu-id="77609-232">Access hello installer from hello process server</span></span>

1. <span data-ttu-id="77609-233">Na powitania serwera przetwarzania, przejdź zbyt**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository C:\Program Files (x86)**.</span><span class="sxs-lookup"><span data-stu-id="77609-233">On hello process server, go too**C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="77609-234">Skopiuj plik Instalatora wymagane hello z serwera przetwarzania hello i zapisz go jako **latestlinuxmobsvc.tar.gz** w katalogu macierzystym.</span><span class="sxs-lookup"><span data-stu-id="77609-234">Copy hello required installer file from hello process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="77609-235">Zastosuj zmiany konfiguracji niestandardowej</span><span class="sxs-lookup"><span data-stu-id="77609-235">Apply custom configuration changes</span></span>

<span data-ttu-id="77609-236">zmiany konfiguracji niestandardowej tooapply, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="77609-236">tooapply custom configuration changes, use hello following steps:</span></span>


1. <span data-ttu-id="77609-237">Uruchom hello następującego pliku binarnego hello toountar polecenia.</span><span class="sxs-lookup"><span data-stu-id="77609-237">Run hello following command toountar hello binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Zrzut ekranu przedstawiający hello polecenia toorun](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="77609-239">Witaj uruchom następujące polecenie toogive uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="77609-239">Run hello following command toogive permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="77609-240">Witaj uruchom następujące polecenie toorun hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="77609-240">Run hello following command toorun hello script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="77609-241">Uruchom skrypt hello tylko raz na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="77609-241">Run hello script only once on hello server.</span></span> <span data-ttu-id="77609-242">Zamknij serwer hello.</span><span class="sxs-lookup"><span data-stu-id="77609-242">Shut down hello server.</span></span> <span data-ttu-id="77609-243">Następnie uruchom ponownie serwer powitania po dodaniu dysku, zgodnie z opisem w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="77609-243">Then restart hello server after you add a disk, as described in hello next section.</span></span>

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a><span data-ttu-id="77609-244">Dodaj maszynę wirtualną systemu Linux główny cel przechowywania dysku toohello</span><span class="sxs-lookup"><span data-stu-id="77609-244">Add a retention disk toohello Linux master target virtual machine</span></span>

<span data-ttu-id="77609-245">Użyj hello następujące kroki toocreate dysku przechowywania:</span><span class="sxs-lookup"><span data-stu-id="77609-245">Use hello following steps toocreate a retention disk:</span></span>

1. <span data-ttu-id="77609-246">Dołącz nowy dysk 1 TB toohello główny cel maszyny wirtualnej systemu Linux, a następnie uruchom hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="77609-246">Attach a new 1-TB disk toohello Linux master target virtual machine, and then start hello machine.</span></span>

2. <span data-ttu-id="77609-247">Użyj hello **wielościeżkowe -ll** toolearn hello wielościeżkowe identyfikator dysku przechowywania hello polecenia.</span><span class="sxs-lookup"><span data-stu-id="77609-247">Use hello **multipath -ll** command toolearn hello multipath ID of hello retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![Identyfikator dysku przechowywania hello wielościeżkowe Hello](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="77609-249">Sformatuj dysk hello, a następnie utworzyć systemu plików na powitania nowego dysku.</span><span class="sxs-lookup"><span data-stu-id="77609-249">Format hello drive, and then create a file system on hello new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Tworzenie system plików na dysku hello](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="77609-251">Po utworzeniu hello systemu plików, należy zainstalować dysk przechowywania hello.</span><span class="sxs-lookup"><span data-stu-id="77609-251">After you create hello file system, mount hello retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Instalowanie hello przechowywania dysku](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="77609-253">Utwórz hello **fstab** wpis toomount hello dysk przechowywania każdym uruchomieniu hello systemu.</span><span class="sxs-lookup"><span data-stu-id="77609-253">Create hello **fstab** entry toomount hello retention drive every time hello system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="77609-254">Wybierz **Wstaw** toobegin edytowania pliku hello.</span><span class="sxs-lookup"><span data-stu-id="77609-254">Select **Insert** toobegin editing hello file.</span></span> <span data-ttu-id="77609-255">Tworzenie nowego wiersza, a następnie Włóż hello następującego tekstu.</span><span class="sxs-lookup"><span data-stu-id="77609-255">Create a new line, and then insert hello following text.</span></span> <span data-ttu-id="77609-256">Edytuj identyfikator dysku hello wielu ścieżek na podstawie Identyfikatora wielościeżkowe hello wyróżnione z hello poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="77609-256">Edit hello disk multipath ID based on hello highlighted multipath ID from hello previous command.</span></span>

    <span data-ttu-id="77609-257"> **/dev/mapowania/ <Retention disks multipath id> /mnt/rw ext4 przechowywania 0 0**</span><span class="sxs-lookup"><span data-stu-id="77609-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="77609-258">Wybierz **Esc**, a następnie wpisz **: wq** (zapisać i zamknąć) tooclose hello w oknie edytora.</span><span class="sxs-lookup"><span data-stu-id="77609-258">Select **Esc**, and then type **:wq** (write and quit) tooclose hello editor window.</span></span>

### <a name="install-hello-master-target"></a><span data-ttu-id="77609-259">Zainstaluj główny cel hello</span><span class="sxs-lookup"><span data-stu-id="77609-259">Install hello master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77609-260">Hello hello główny serwer docelowy musi być równa tooor starszych niż hello wersji serwera przetwarzania hello i hello konfiguracji serwera.</span><span class="sxs-lookup"><span data-stu-id="77609-260">hello version of hello master target server must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="77609-261">Jeśli ten warunek nie jest spełniony, ponownej ochrony zakończy się pomyślnie, ale replikacja nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="77609-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="77609-262">Przed zainstalowaniem hello główny serwer docelowy, sprawdź, że hello **/etc/hosts** pliku na maszynie wirtualnej hello zawiera wpisy, które mapują adresy IP toohello lokalną nazwą hosta hello, które są skojarzone z wszystkich kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="77609-262">Before you install hello master target server, check that hello **/etc/hosts** file on hello virtual machine contains entries that map hello local hostname toohello IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="77609-263">Kopiuj hasło hello z **Recovery\private\connection.passphrase witryny Azure C:\ProgramData\Microsoft** na powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="77609-263">Copy hello passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on hello configuration server.</span></span> <span data-ttu-id="77609-264">Następnie zapisz go jako **passphrase.txt** w hello tego samego katalogu lokalnego, uruchamiając hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="77609-264">Then save it as **passphrase.txt** in hello same local directory by running hello following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="77609-265">Przykład:</span><span class="sxs-lookup"><span data-stu-id="77609-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="77609-266">Należy pamiętać, adres IP serwera konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="77609-266">Note hello configuration server's IP address.</span></span> <span data-ttu-id="77609-267">Należy go hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="77609-267">You need it in hello next step.</span></span>

3. <span data-ttu-id="77609-268">Uruchom hello następujące polecenia tooinstall hello główny serwer docelowy i Zarejestruj serwer hello hello konfiguracji serwera.</span><span class="sxs-lookup"><span data-stu-id="77609-268">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="77609-269">Przykład:</span><span class="sxs-lookup"><span data-stu-id="77609-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="77609-270">Poczekaj na zakończenie hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="77609-270">Wait until hello script finishes.</span></span> <span data-ttu-id="77609-271">Jeśli główny cel hello rejestruje pomyślnie, hello główny serwer docelowy znajduje się na powitania **infrastruktura usługi Site Recovery** hello portalu.</span><span class="sxs-lookup"><span data-stu-id="77609-271">If hello master target registers sucessfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


#### <a name="install-hello-master-target-by-using-interactive-installation"></a><span data-ttu-id="77609-272">Zainstaluj hello główny serwer docelowy przy użyciu instalacji interakcyjnej</span><span class="sxs-lookup"><span data-stu-id="77609-272">Install hello master target by using interactive installation</span></span>

1. <span data-ttu-id="77609-273">Witaj uruchom następujące polecenie tooinstall hello głównego celu.</span><span class="sxs-lookup"><span data-stu-id="77609-273">Run hello following command tooinstall hello master target.</span></span> <span data-ttu-id="77609-274">W roli agenta hello, wybierz opcję **docelowego elementu głównego**.</span><span class="sxs-lookup"><span data-stu-id="77609-274">For hello agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="77609-275">Wybierz hello domyślna lokalizacja instalacji, a następnie wybierz **Enter** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="77609-275">Choose hello default location for installation, and then select **Enter** toocontinue.</span></span>

    ![Wybieranie domyślnej lokalizacji instalacji główny serwer docelowy](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="77609-277">Po zakończeniu instalacji hello, należy zarejestrować serwer konfiguracji hello przy użyciu wiersza polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="77609-277">After hello installation has finished, register hello configuration server by using hello command line.</span></span>

1. <span data-ttu-id="77609-278">Należy pamiętać, adres IP hello hello konfiguracji serwera.</span><span class="sxs-lookup"><span data-stu-id="77609-278">Note hello IP address of hello configuration server.</span></span> <span data-ttu-id="77609-279">Należy go hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="77609-279">You need it in hello next step.</span></span>

2. <span data-ttu-id="77609-280">Uruchom hello następujące polecenia tooinstall hello główny serwer docelowy i Zarejestruj serwer hello hello konfiguracji serwera.</span><span class="sxs-lookup"><span data-stu-id="77609-280">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="77609-281">Przykład:</span><span class="sxs-lookup"><span data-stu-id="77609-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="77609-282">Poczekaj na zakończenie hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="77609-282">Wait until hello script finishes.</span></span> <span data-ttu-id="77609-283">Jeśli hello główny cel został pomyślnie zarejestrowany, hello główny serwer docelowy znajduje się na powitania **infrastruktura usługi Site Recovery** hello portalu.</span><span class="sxs-lookup"><span data-stu-id="77609-283">If hello master target is registered succesfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


### <a name="upgrade-hello-master-target"></a><span data-ttu-id="77609-284">Główny cel hello uaktualnienia</span><span class="sxs-lookup"><span data-stu-id="77609-284">Upgrade hello master target</span></span>

<span data-ttu-id="77609-285">Uruchom Instalatora hello.</span><span class="sxs-lookup"><span data-stu-id="77609-285">Run hello installer.</span></span> <span data-ttu-id="77609-286">Automatycznie wykryje, czy hello agent jest zainstalowany w głównym celu hello.</span><span class="sxs-lookup"><span data-stu-id="77609-286">It automatically detects that hello agent is installed on hello master target.</span></span> <span data-ttu-id="77609-287">tooupgrade, wybierz opcję **Y**.  Po zakończeniu instalacji hello, sprawdź wersję hello z głównego celu hello zainstalowane za pomocą następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="77609-287">tooupgrade, select **Y**.  After hello setup has been completed, check hello version of hello master target installed by using hello following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="77609-288">Widać, że hello **wersji** pola zwraca numer wersji hello hello głównego celu.</span><span class="sxs-lookup"><span data-stu-id="77609-288">You can see that hello **Version** field gives hello version number of hello master target.</span></span>

### <a name="install-vmware-tools-on-hello-master-target-server"></a><span data-ttu-id="77609-289">Zainstaluj narzędzia VMware na powitania główny serwer docelowy</span><span class="sxs-lookup"><span data-stu-id="77609-289">Install VMware tools on hello master target server</span></span>

<span data-ttu-id="77609-290">Należy tooinstall narzędzia VMware w głównym celu hello, aby mogło odnajdować hello magazynów danych.</span><span class="sxs-lookup"><span data-stu-id="77609-290">You need tooinstall VMware tools on hello master target so that it can discover hello data stores.</span></span> <span data-ttu-id="77609-291">Jeśli nie zainstalowano narzędzi hello, hello ponownej ochrony ekranu nie ma na liście w hello magazynów danych.</span><span class="sxs-lookup"><span data-stu-id="77609-291">If hello tools are not installed, hello reprotect screen isn't listed in hello data stores.</span></span> <span data-ttu-id="77609-292">Po zakończeniu instalacji hello narzędzi VMware należy toorestart.</span><span class="sxs-lookup"><span data-stu-id="77609-292">After installation of hello VMware tools, you need toorestart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77609-293">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="77609-293">Next steps</span></span>
<span data-ttu-id="77609-294">Po instalacji hello i rejestracji hello główny serwer docelowy ma finsihed, można wyświetlić głównego celu hello są wyświetlane na powitania **docelowego elementu głównego** sekcji **infrastruktura usługi Site Recovery**, w obszarze hello Omówienie serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="77609-294">After hello installation and registration of hello master target has finsihed, you can see hello master target appear on hello **Master Target** section in **Site Recovery Infrastructure**, under hello configuration server overview.</span></span>

<span data-ttu-id="77609-295">Teraz można przystąpić do [przełączonej](site-recovery-how-to-reprotect.md), a następnie powrót po awarii.</span><span class="sxs-lookup"><span data-stu-id="77609-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="77609-296">Typowe problemy</span><span class="sxs-lookup"><span data-stu-id="77609-296">Common issues</span></span>

* <span data-ttu-id="77609-297">Upewnij się, że nie należy włączać narzędzia Storage vMotion na wszystkie składniki zarządzania, takie jak głównego celu.</span><span class="sxs-lookup"><span data-stu-id="77609-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="77609-298">Jeśli po pomyślnej ponownej ochrony jest przenoszony hello główny cel, nie można odłączyć hello dysków maszyny wirtualnej (VMDKs).</span><span class="sxs-lookup"><span data-stu-id="77609-298">If hello master target moves after a successful reprotect, hello virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="77609-299">W takim przypadku powrotu po awarii nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="77609-299">In this case, failback fails.</span></span>

* <span data-ttu-id="77609-300">główny cel Hello nie powinna mieć żadnych migawek na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="77609-300">hello master target should not have any snapshots on hello virtual machine.</span></span> <span data-ttu-id="77609-301">W przypadku migawki powrotu po awarii nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="77609-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="77609-302">Ze względu na komputerach niektórych klientów konfiguracji kart niestandardowych toosome hello interfejs sieciowy jest wyłączona podczas uruchamiania i hello główny cel agenta nie można zainicjować.</span><span class="sxs-lookup"><span data-stu-id="77609-302">Due toosome custom NIC configurations at some customers, hello network interface is disabled during startup, and hello master target agent cannot initialize.</span></span> <span data-ttu-id="77609-303">Upewnij się, że hello następujące właściwości są poprawnie ustawione.</span><span class="sxs-lookup"><span data-stu-id="77609-303">Make sure that hello following properties are correctly set.</span></span> <span data-ttu-id="77609-304">Sprawdź tych właściwości w hello Ethernet karty /etc/sysconfig/network-scripts/ifcfg pliku-eth *.</span><span class="sxs-lookup"><span data-stu-id="77609-304">Check these properties in hello Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="77609-305">BOOTPROTO = dhcp</span><span class="sxs-lookup"><span data-stu-id="77609-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="77609-306">ONBOOT = tak</span><span class="sxs-lookup"><span data-stu-id="77609-306">ONBOOT=yes</span></span>
