---
title: aaaCreate i przekazywanie wirtualna FreeBSD obrazu | Dokumentacja firmy Microsoft
description: "Dowiedz się toocreate i przekazywanie wirtualnego dysku twardego (VHD) zawierający hello FreeBSD systemu operacyjnego toocreate maszyny wirtualnej platformy Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a><span data-ttu-id="ca029-103">Tworzenie i przekazywanie tooAzure FreeBSD wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="ca029-103">Create and upload a FreeBSD VHD tooAzure</span></span>
<span data-ttu-id="ca029-104">W tym artykule opisano, jak toocreate i przekazywanie wirtualnego dysku twardego (VHD) zawierający hello FreeBSD systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="ca029-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello FreeBSD operating system.</span></span> <span data-ttu-id="ca029-105">Po wysłaniu, można użyć jej jako toocreate własny obraz maszyny wirtualnej (VM) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ca029-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ca029-106">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ca029-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ca029-107">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="ca029-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ca029-108">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ca029-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ca029-109">Aby dowiedzieć się, jak przekazywanie wirtualnego dysku twardego za pomocą modelu Resource Manager hello, zobacz [tutaj](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ca029-109">For information about uploading a VHD using hello Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca029-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ca029-110">Prerequisites</span></span>
<span data-ttu-id="ca029-111">W tym artykule założono, że hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ca029-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="ca029-112">**Subskrypcja platformy Azure**— Jeśli nie masz konta, możesz utworzyć jedną w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="ca029-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="ca029-113">Jeśli masz subskrypcję MSDN, zobacz [Azure miesięczne środki dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="ca029-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="ca029-114">W przeciwnym razie Dowiedz się, jak za[utworzyć bezpłatne konto próbne](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ca029-114">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="ca029-115">**Narzędzia programu PowerShell Azure**--modułu Azure PowerShell hello musi być zainstalowana i skonfigurowana toouse subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca029-115">**Azure PowerShell tools**--hello Azure PowerShell module must be installed and configured toouse your Azure subscription.</span></span> <span data-ttu-id="ca029-116">Moduł hello toodownload, zobacz [Azure pobiera](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ca029-116">toodownload hello module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="ca029-117">Samouczek, który opisuje sposób tooinstall i skonfigurować moduł hello jest dostępnych tutaj.</span><span class="sxs-lookup"><span data-stu-id="ca029-117">A tutorial that describes how tooinstall and configure hello module is available here.</span></span> <span data-ttu-id="ca029-118">Użyj hello [Azure pobiera](https://azure.microsoft.com/downloads/) polecenia cmdlet tooupload hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="ca029-118">Use hello [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet tooupload hello VHD.</span></span>
* <span data-ttu-id="ca029-119">**FreeBSD zainstalowanego systemu operacyjnego w pliku VHD**--obsługiwany system operacyjny FreeBSD musi być zainstalowany tooa wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="ca029-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="ca029-120">Wiele narzędzi istnieje toocreate pliki VHD.</span><span class="sxs-lookup"><span data-stu-id="ca029-120">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="ca029-121">Można na przykład, takich jak plik VHD hello toocreate funkcji Hyper-V za pomocą rozwiązania wirtualizacji i zainstaluj system operacyjny hello.</span><span class="sxs-lookup"><span data-stu-id="ca029-121">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="ca029-122">Aby uzyskać instrukcje dotyczące sposobu tooinstall i użyj funkcji Hyper-V, zobacz [Instalowanie funkcji Hyper-V i tworzenie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca029-122">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="ca029-123">Witaj nowszy format VHDX nie jest obsługiwane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ca029-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="ca029-124">Można przekonwertować format tooVHD dysku hello przy użyciu Menedżera funkcji Hyper-V lub polecenia cmdlet hello [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca029-124">You can convert hello disk tooVHD format by using Hyper-V Manager or hello cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="ca029-125">Ponadto istnieje [samouczek w witrynie MSDN temat toouse FreeBSD z funkcją Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca029-125">In addition, there is a [tutorial on MSDN about how toouse FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="ca029-126">To zadanie obejmuje następujące kroki pięć hello:</span><span class="sxs-lookup"><span data-stu-id="ca029-126">This task includes hello following five steps:</span></span>

## <a name="step-1-prepare-hello-image-for-upload"></a><span data-ttu-id="ca029-127">Krok 1: Przygotowanie obrazu hello przekazywania</span><span class="sxs-lookup"><span data-stu-id="ca029-127">Step 1: Prepare hello image for upload</span></span>
<span data-ttu-id="ca029-128">Na maszynie wirtualnej hello, w którym zainstalowano system operacyjny FreeBSD hello wykonaj hello następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="ca029-128">On hello virtual machine where you installed hello FreeBSD operating system, complete hello following procedures:</span></span>

1. <span data-ttu-id="ca029-129">Włącz protokół DHCP.</span><span class="sxs-lookup"><span data-stu-id="ca029-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="ca029-130">Włącz SSH.</span><span class="sxs-lookup"><span data-stu-id="ca029-130">Enable SSH.</span></span>

    <span data-ttu-id="ca029-131">Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu.</span><span class="sxs-lookup"><span data-stu-id="ca029-131">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="ca029-132">Domyślnie jest włączone po instalacji z dysku FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="ca029-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="ca029-133">Konfigurowanie konsoli szeregowej.</span><span class="sxs-lookup"><span data-stu-id="ca029-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="ca029-134">Zainstaluj plik sudo.</span><span class="sxs-lookup"><span data-stu-id="ca029-134">Install sudo.</span></span>

    <span data-ttu-id="ca029-135">konta głównego Hello jest wyłączona w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="ca029-135">hello root account is disabled in Azure.</span></span> <span data-ttu-id="ca029-136">Oznacza to, że należy tooutilize sudo z poleceniami toorun nieuprawnionego użytkownika z podniesionymi uprawnieniami.</span><span class="sxs-lookup"><span data-stu-id="ca029-136">This means you need tooutilize sudo from an unprivileged user toorun commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="ca029-137">Wymagania wstępne dotyczące agenta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca029-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="ca029-138">Zainstaluj agenta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca029-138">Install Azure Agent.</span></span>

    <span data-ttu-id="ca029-139">Witaj najnowszej wersji hello Azure agenta zawsze można znaleźć w [github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="ca029-139">hello latest release of hello Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="ca029-140">Witaj wersji 2.0.10 + oficjalnie obsługuje FreeBSD 10 & 10.1 i wersji hello 2.1.4 + (w tym 2.2.x) oficjalnie obsługuje FreeBSD 10.2 i jego nowszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="ca029-140">hello version 2.0.10 + officially supports FreeBSD 10 & 10.1, and hello version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="ca029-141">2.0 Użyjmy 2.0.16 na przykład:</span><span class="sxs-lookup"><span data-stu-id="ca029-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="ca029-142">2.1 możemy użyć 2.1.4 na przykład:</span><span class="sxs-lookup"><span data-stu-id="ca029-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="ca029-143">Po zainstalowaniu agenta platformy Azure jest tooverify dobrym rozwiązaniem, czy działa:</span><span class="sxs-lookup"><span data-stu-id="ca029-143">After you install Azure Agent, it's a good idea tooverify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="ca029-144">Anulowanie zastrzeżenia hello systemu.</span><span class="sxs-lookup"><span data-stu-id="ca029-144">Deprovision hello system.</span></span>

    <span data-ttu-id="ca029-145">Deprovision hello tooclean systemu go i udostępnić go odpowiednie dla reprovisioning.</span><span class="sxs-lookup"><span data-stu-id="ca029-145">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="ca029-146">Witaj następujące polecenie spowoduje również usunięcie hello ostatnie konto użytkownika elastycznie i hello skojarzone dane:</span><span class="sxs-lookup"><span data-stu-id="ca029-146">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="ca029-147">Teraz można zamknąć maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ca029-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="ca029-148">Krok 2: Utwórz konto magazynu na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ca029-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="ca029-149">Należy korzystać z konta magazynu w Azure tooupload pliku VHD, może być używane toocreate maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ca029-149">You need a storage account in Azure tooupload a .vhd file so it can be used toocreate a virtual machine.</span></span> <span data-ttu-id="ca029-150">Możesz użyć hello klasycznego portalu Azure toocreate konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ca029-150">You can use hello Azure classic portal toocreate a storage account.</span></span>

1. <span data-ttu-id="ca029-151">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ca029-151">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ca029-152">Na pasku poleceń hello, wybierz **nowy**.</span><span class="sxs-lookup"><span data-stu-id="ca029-152">On hello command bar, select **New**.</span></span>
3. <span data-ttu-id="ca029-153">Wybierz **usług danych** > **magazynu** > **szybkie tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="ca029-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![Szybkie tworzenie konta magazynu](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="ca029-155">Wypełnij pola hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ca029-155">Fill out hello fields as follows:</span></span>

   * <span data-ttu-id="ca029-156">W hello **adres URL** wpisz adres URL konta magazynu hello toouse nazwę domeny podrzędnej.</span><span class="sxs-lookup"><span data-stu-id="ca029-156">In hello **URL** field, type a subdomain name toouse in hello storage account URL.</span></span> <span data-ttu-id="ca029-157">wpis Hello może zawierać od 3 do 24 cyfry i małe litery.</span><span class="sxs-lookup"><span data-stu-id="ca029-157">hello entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="ca029-158">Ta nazwa staje się nazwa hosta hello w hello adresu URL magazynu obiektów Blob platformy Azure używana tooaddress, magazynu kolejek Azure lub zasobów magazynu tabel Azure hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ca029-158">This name becomes hello host name within hello URL that is used tooaddress Azure Blob storage, Azure Queue storage, or Azure Table storage resources for hello subscription.</span></span>
   * <span data-ttu-id="ca029-159">W hello **grupa lokalizacji/koligacji** menu rozwijanego wybierz hello **lokalizacja lub grupa koligacji** dla konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="ca029-159">In hello **Location/Affinity Group** drop-down menu, choose hello **location or affinity group** for hello storage account.</span></span> <span data-ttu-id="ca029-160">Grupa koligacji pozwala umieścić usługi w chmurze i magazynu w hello tym samym centrum danych.</span><span class="sxs-lookup"><span data-stu-id="ca029-160">An affinity group lets you put your cloud services and storage in hello same data center.</span></span>
   * <span data-ttu-id="ca029-161">W hello **replikacji** określ czy toouse **geograficznie nadmiarowego** replikacji dla konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="ca029-161">In hello **Replication** field, decide whether toouse **Geo-Redundant** replication for hello storage account.</span></span> <span data-ttu-id="ca029-162">Replikacja geograficzna jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="ca029-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="ca029-163">Ta opcja replikuje Twoje dane tooa dodatkowej lokalizacji, nie tooyou kosztów, tak, aby Magazyn awaryjnie toothat lokalizacji, jeżeli poważnej awarii występuje w lokalizacji głównej hello.</span><span class="sxs-lookup"><span data-stu-id="ca029-163">This option replicates your data tooa secondary location, at no cost tooyou, so that your storage fails over toothat location if a major failure occurs at hello primary location.</span></span> <span data-ttu-id="ca029-164">Lokalizacja dodatkowej Hello jest przypisywany automatycznie i nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="ca029-164">hello secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="ca029-165">Jeśli potrzebujesz większej kontroli nad hello lokalizacji magazynu oparte na chmurze wymagania toolegal lub zasady organizacji, można wyłączyć replikacji geograficznej.</span><span class="sxs-lookup"><span data-stu-id="ca029-165">If you need more control over hello location of your cloud-based storage due toolegal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="ca029-166">Należy jednak pamiętać, że jeśli później włączyć replikację geograficzną zostanie naliczona jednorazowego transferu danych opłata tooreplicate Twojego istniejącej lokalizacji dodatkowej toohello danych.</span><span class="sxs-lookup"><span data-stu-id="ca029-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee tooreplicate your existing data toohello secondary location.</span></span> <span data-ttu-id="ca029-167">Usługi magazynu bez — replikacja geograficzna jest oferowany z rabatem.</span><span class="sxs-lookup"><span data-stu-id="ca029-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="ca029-168">Więcej informacji o zarządzaniu — replikacja geograficzna kont magazynu można znaleźć tutaj: [replikacja usługi Azure Storage](../../../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="ca029-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![Wprowadź szczegóły konta magazynu](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="ca029-170">Wybierz **utworzyć konto magazynu**.</span><span class="sxs-lookup"><span data-stu-id="ca029-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="ca029-171">Witaj konto zostanie wyświetlone w obszarze **magazynu**.</span><span class="sxs-lookup"><span data-stu-id="ca029-171">hello account now appears under **storage**.</span></span>

    ![Pomyślnie utworzono konto magazynu](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="ca029-173">Następnie należy utworzyć kontener dla plików VHD przekazane.</span><span class="sxs-lookup"><span data-stu-id="ca029-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="ca029-174">Wybierz nazwę konta magazynu hello, a następnie wybierz **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="ca029-174">Select hello storage account name, and then select **Containers**.</span></span>

    ![Szczegóły konta magazynu](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="ca029-176">Wybierz **utworzyć kontener**.</span><span class="sxs-lookup"><span data-stu-id="ca029-176">Select **Create a Container**.</span></span>

    ![Szczegóły konta magazynu](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="ca029-178">W hello **nazwa** wpisz nazwę użytkownika kontenera.</span><span class="sxs-lookup"><span data-stu-id="ca029-178">In hello **Name** field, type a name for your container.</span></span> <span data-ttu-id="ca029-179">Następnie w hello **dostępu** menu rozwijanego, wybierz typ zasad dostępu ma.</span><span class="sxs-lookup"><span data-stu-id="ca029-179">Then, in hello **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![Nazwa kontenera](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="ca029-181">Domyślnie hello kontener jest prywatny i jest dostępny tylko przez właściciela konta hello.</span><span class="sxs-lookup"><span data-stu-id="ca029-181">By default, hello container is private and can only be accessed by hello account owner.</span></span> <span data-ttu-id="ca029-182">tooallow publiczny dostęp do odczytu toohello BLOB w kontenerach hello, ale nie toohello właściwości kontenera i metadanych, użyj hello **publicznego obiektu Blob** opcji.</span><span class="sxs-lookup"><span data-stu-id="ca029-182">tooallow public read access toohello blobs in hello container, but not toohello container properties and metadata, use hello **Public Blob** option.</span></span> <span data-ttu-id="ca029-183">tooallow publicznego pełny dostęp do odczytu dla hello kontenera i obiektów blob, użyj hello **publicznego kontenera** opcji.</span><span class="sxs-lookup"><span data-stu-id="ca029-183">tooallow full public read access for hello container and blobs, use hello **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a><span data-ttu-id="ca029-184">Krok 3: Przygotowanie hello tooAzure połączenia</span><span class="sxs-lookup"><span data-stu-id="ca029-184">Step 3: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="ca029-185">Zanim można przekazać pliku VHD, należy tooestablish bezpiecznego połączenia między komputerem i Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca029-185">Before you can upload a .vhd file, you need tooestablish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="ca029-186">Możesz użyć hello Azure Active Directory (Azure AD) metoda lub hello toodo metody certyfikatu go.</span><span class="sxs-lookup"><span data-stu-id="ca029-186">You can use hello Azure Active Directory (Azure AD) method or hello certificate method toodo it.</span></span>

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a><span data-ttu-id="ca029-187">Użyj hello Azure AD — metoda tooupload pliku VHD</span><span class="sxs-lookup"><span data-stu-id="ca029-187">Use hello Azure AD method tooupload a .vhd file</span></span>
1. <span data-ttu-id="ca029-188">Hello Otwórz konsolę programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ca029-188">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="ca029-189">Wpisz następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="ca029-189">Type hello following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="ca029-190">To polecenie powoduje otwarcie okna logowania której możesz zalogować się przy użyciu konta służbowego.</span><span class="sxs-lookup"><span data-stu-id="ca029-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![Okno programu PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="ca029-192">Azure uwierzytelnia i zapisanie informacji o poświadczeniach hello.</span><span class="sxs-lookup"><span data-stu-id="ca029-192">Azure authenticates and saves hello credential information.</span></span> <span data-ttu-id="ca029-193">Następnie zamyka okno hello.</span><span class="sxs-lookup"><span data-stu-id="ca029-193">Then it closes hello window.</span></span>

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a><span data-ttu-id="ca029-194">Użyj hello certyfikatu metody tooupload pliku VHD</span><span class="sxs-lookup"><span data-stu-id="ca029-194">Use hello certificate method tooupload a .vhd file</span></span>
1. <span data-ttu-id="ca029-195">Hello Otwórz konsolę programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ca029-195">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="ca029-196">Typ: `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="ca029-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="ca029-197">Oknie przeglądarki zostanie otwarty i wyświetla monit o możesz toodownload hello .publishsettings pliku.</span><span class="sxs-lookup"><span data-stu-id="ca029-197">A browser window opens and prompts you toodownload hello .publishsettings file.</span></span> <span data-ttu-id="ca029-198">Ten plik zawiera informacje i certyfikatu dla Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca029-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![Strona pobierania przeglądarki](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="ca029-200">Zapisz plik .publishsettings hello.</span><span class="sxs-lookup"><span data-stu-id="ca029-200">Save hello .publishsettings file.</span></span>
5. <span data-ttu-id="ca029-201">Typ: `Import-AzurePublishSettingsFile <PathToFile>`, gdzie `<PathToFile>` jest hello pełną ścieżkę toohello .publishsettings pliku.</span><span class="sxs-lookup"><span data-stu-id="ca029-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is hello full path toohello .publishsettings file.</span></span>

   <span data-ttu-id="ca029-202">Aby uzyskać więcej informacji, zobacz [wprowadzenie do poleceń cmdlet systemu Azure](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca029-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="ca029-203">Aby uzyskać więcej informacji na temat instalowania i konfigurowania programu PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ca029-203">For more information about installing and configuring PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-hello-vhd-file"></a><span data-ttu-id="ca029-204">Krok 4: Przekaż plik VHD hello</span><span class="sxs-lookup"><span data-stu-id="ca029-204">Step 4: Upload hello .vhd file</span></span>
<span data-ttu-id="ca029-205">Podczas przekazywania pliku VHD hello, możesz go umieścić w dowolnym w ramach usługi magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="ca029-205">When you upload hello .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="ca029-206">Poniżej przedstawiono niektóre warunki, które będą używane podczas przekazywania pliku hello:</span><span class="sxs-lookup"><span data-stu-id="ca029-206">Following are some terms you will use when you upload hello file:</span></span>

* <span data-ttu-id="ca029-207">**BlobStorageURL** jest adres URL hello hello konta magazynu, który został utworzony w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="ca029-207">**BlobStorageURL** is hello URL for hello storage account that you created in Step 2.</span></span>
* <span data-ttu-id="ca029-208">**YourImagesFolder** jest hello kontenera w magazynie obiektów Blob w miejscu toostore obrazów.</span><span class="sxs-lookup"><span data-stu-id="ca029-208">**YourImagesFolder** is hello container within Blob storage where you want toostore your images.</span></span>
* <span data-ttu-id="ca029-209">**VHDName** jest etykietę hello, pojawiającą hello Azure classic portal tooidentify hello wirtualnym dysku twardym.</span><span class="sxs-lookup"><span data-stu-id="ca029-209">**VHDName** is hello label that appears in hello Azure classic portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="ca029-210">**PathToVHDFile** jest hello Pełna ścieżka i nazwa pliku VHD hello.</span><span class="sxs-lookup"><span data-stu-id="ca029-210">**PathToVHDFile** is hello full path and name of hello .vhd file.</span></span>

<span data-ttu-id="ca029-211">Okno programu Azure PowerShell hello używanego w poprzednim kroku hello wpisz:</span><span class="sxs-lookup"><span data-stu-id="ca029-211">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a><span data-ttu-id="ca029-212">Krok 5: Tworzenie maszyny Wirtualnej z pliku VHD przekazane hello</span><span class="sxs-lookup"><span data-stu-id="ca029-212">Step 5: Create a VM with hello uploaded .vhd file</span></span>
<span data-ttu-id="ca029-213">Po przekazaniu pliku VHD hello, należy dodać go jako listy obrazów toohello niestandardowych obrazów, które są skojarzone z subskrypcją i Utwórz maszynę wirtualną z tego obrazu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="ca029-213">After you upload hello .vhd file, you can add it as an image toohello list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="ca029-214">Okno programu Azure PowerShell hello używanego w poprzednim kroku hello wpisz:</span><span class="sxs-lookup"><span data-stu-id="ca029-214">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > <span data-ttu-id="ca029-215">Użyj systemu Linux jako hello typ systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="ca029-215">Use Linux as hello OS type.</span></span> <span data-ttu-id="ca029-216">Bieżąca wersja programu Azure PowerShell Hello akceptuje tylko "Linux" lub "Windows" jako parametr.</span><span class="sxs-lookup"><span data-stu-id="ca029-216">hello current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="ca029-217">Po wykonaniu poprzednich kroków hello nowy obraz powitania znajduje się po wybraniu hello **obrazów** kartę na powitania klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ca029-217">After you complete hello previous steps, hello new image is listed when you choose hello **Images** tab on hello Azure classic portal.</span></span>  

    ![Wybierz obraz](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="ca029-219">Utwórz maszynę wirtualną z galerii hello.</span><span class="sxs-lookup"><span data-stu-id="ca029-219">Create a virtual machine from hello gallery.</span></span> <span data-ttu-id="ca029-220">Ten nowy obraz jest teraz dostępna w obszarze **Moje obrazy**.</span><span class="sxs-lookup"><span data-stu-id="ca029-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="ca029-221">Wybierz nowy obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="ca029-221">Select hello new image.</span></span> <span data-ttu-id="ca029-222">Następnie należy przejść przez tooset monity hello nazwy hosta, hasła, klucz SSH i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="ca029-222">Next, go through hello prompts tooset up a host name, password, SSH key, and so on.</span></span>

    ![Obraz niestandardowy](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="ca029-224">Po ukończeniu inicjowania obsługi administracyjnej hello, zobaczysz maszyny Wirtualnej FreeBSD działające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ca029-224">After you complete hello provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![Obraz FreeBSD na platformie azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
