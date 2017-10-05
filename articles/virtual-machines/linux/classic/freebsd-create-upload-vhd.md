---
title: "Utwórz i Przekaż obraz maszyny Wirtualnej FreeBSD | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tworzenie i przekazywanie wirtualnego dysku twardego (VHD) z systemem operacyjnym FreeBSD, aby utworzyć maszynę wirtualną platformy Azure"
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
ms.openlocfilehash: 918f454784a9676297077c2e94c3e49ab2872d2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-upload-a-freebsd-vhd-to-azure"></a><span data-ttu-id="3039d-103">Tworzenie i przekazywanie wirtualnego dysku twardego FreeBSD na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3039d-103">Create and upload a FreeBSD VHD to Azure</span></span>
<span data-ttu-id="3039d-104">W tym artykule opisano tworzenie i przekazywanie wirtualnego dysku twardego (VHD) z systemem operacyjnym FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="3039d-104">This article shows you how to create and upload a virtual hard disk (VHD) that contains the FreeBSD operating system.</span></span> <span data-ttu-id="3039d-105">Po wysłaniu, służy ona jako własnego obrazu można utworzyć maszynę wirtualną (VM) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3039d-105">After you upload it, you can use it as your own image to create a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="3039d-106">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3039d-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3039d-107">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="3039d-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="3039d-108">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3039d-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="3039d-109">Aby dowiedzieć się, jak przekazywanie wirtualnego dysku twardego za pomocą modelu Resource Manager, zobacz [tutaj](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3039d-109">For information about uploading a VHD using the Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3039d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3039d-110">Prerequisites</span></span>
<span data-ttu-id="3039d-111">W tym artykule przyjęto założenie, że masz następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="3039d-111">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="3039d-112">**Subskrypcja platformy Azure**— Jeśli nie masz konta, możesz utworzyć jedną w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="3039d-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="3039d-113">Jeśli masz subskrypcję MSDN, zobacz [Azure miesięczne środki dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="3039d-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="3039d-114">W przeciwnym razie Dowiedz się, jak [utworzyć bezpłatne konto próbne](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3039d-114">Otherwise, learn how to [create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="3039d-115">**Narzędzia programu PowerShell Azure**--modułu Azure PowerShell musi być zainstalowana i skonfigurowana do pracy z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3039d-115">**Azure PowerShell tools**--The Azure PowerShell module must be installed and configured to use your Azure subscription.</span></span> <span data-ttu-id="3039d-116">Aby pobrać module, zobacz [Azure pobiera](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3039d-116">To download the module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="3039d-117">Samouczek, który opisuje sposób instalowania i konfigurowania modułu jest dostępnych tutaj.</span><span class="sxs-lookup"><span data-stu-id="3039d-117">A tutorial that describes how to install and configure the module is available here.</span></span> <span data-ttu-id="3039d-118">Użyj [Azure pobiera](https://azure.microsoft.com/downloads/) polecenia cmdlet w celu przekazania dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="3039d-118">Use the [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet to upload the VHD.</span></span>
* <span data-ttu-id="3039d-119">**FreeBSD zainstalowanego systemu operacyjnego w pliku VHD**musi być zainstalowany system operacyjny — obsługiwane FreeBSD do wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="3039d-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed to a virtual hard disk.</span></span> <span data-ttu-id="3039d-120">Istnieje wiele narzędzi do tworzenia plików VHD.</span><span class="sxs-lookup"><span data-stu-id="3039d-120">Multiple tools exist to create .vhd files.</span></span> <span data-ttu-id="3039d-121">Na przykład umożliwia rozwiązanie wirtualizacji, takich jak funkcja Hyper-V Utwórz plik VHD i zainstalowania systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="3039d-121">For example, you can use a virtualization solution such as Hyper-V to create the .vhd file and install the operating system.</span></span> <span data-ttu-id="3039d-122">Aby uzyskać instrukcje dotyczące instalowania i używania funkcji Hyper-V, zobacz [Instalowanie funkcji Hyper-V i tworzenie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="3039d-122">For instructions about how to install and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="3039d-123">Nowszy format VHDX nie jest obsługiwane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3039d-123">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="3039d-124">Dysk można przekonwertować na format wirtualnego dysku twardego za pomocą Menedżera funkcji Hyper-V lub polecenia cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="3039d-124">You can convert the disk to VHD format by using Hyper-V Manager or the cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="3039d-125">Ponadto istnieje [samouczek w witrynie MSDN dotyczące korzystania z funkcji Hyper-V FreeBSD](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span><span class="sxs-lookup"><span data-stu-id="3039d-125">In addition, there is a [tutorial on MSDN about how to use FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="3039d-126">To zadanie obejmuje następujące kroki 5:</span><span class="sxs-lookup"><span data-stu-id="3039d-126">This task includes the following five steps:</span></span>

## <a name="step-1-prepare-the-image-for-upload"></a><span data-ttu-id="3039d-127">Krok 1: Przygotowanie obrazu do przekazywania</span><span class="sxs-lookup"><span data-stu-id="3039d-127">Step 1: Prepare the image for upload</span></span>
<span data-ttu-id="3039d-128">Na maszynie wirtualnej, w którym zainstalowany jest system operacyjny FreeBSD wykonaj następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="3039d-128">On the virtual machine where you installed the FreeBSD operating system, complete the following procedures:</span></span>

1. <span data-ttu-id="3039d-129">Włącz protokół DHCP.</span><span class="sxs-lookup"><span data-stu-id="3039d-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="3039d-130">Włącz SSH.</span><span class="sxs-lookup"><span data-stu-id="3039d-130">Enable SSH.</span></span>

    <span data-ttu-id="3039d-131">Upewnij się, że serwer SSH jest zainstalowany i skonfigurowany do uruchamiania w czasie rozruchu.</span><span class="sxs-lookup"><span data-stu-id="3039d-131">Ensure that the SSH server is installed and configured to start at boot time.</span></span> <span data-ttu-id="3039d-132">Domyślnie jest włączone po instalacji z dysku FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="3039d-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="3039d-133">Konfigurowanie konsoli szeregowej.</span><span class="sxs-lookup"><span data-stu-id="3039d-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="3039d-134">Zainstaluj plik sudo.</span><span class="sxs-lookup"><span data-stu-id="3039d-134">Install sudo.</span></span>

    <span data-ttu-id="3039d-135">Konta głównego jest wyłączona w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="3039d-135">The root account is disabled in Azure.</span></span> <span data-ttu-id="3039d-136">Oznacza to, że należy korzystać z sudo z nieuprawnionego użytkownika do uruchomienia polecenia z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="3039d-136">This means you need to utilize sudo from an unprivileged user to run commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="3039d-137">Wymagania wstępne dotyczące agenta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3039d-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="3039d-138">Zainstaluj agenta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3039d-138">Install Azure Agent.</span></span>

    <span data-ttu-id="3039d-139">Najnowszą wersję agenta programu Azure zawsze można znaleźć w [github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="3039d-139">The latest release of the Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="3039d-140">Wersja 2.0.10 oficjalnie obsługuje FreeBSD 10 & 10.1 oraz wersji 2.1.4 + (w tym 2.2.x) obsługuje oficjalnie FreeBSD 10.2 i jego nowszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="3039d-140">The version 2.0.10 + officially supports FreeBSD 10 & 10.1, and the version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="3039d-141">2.0 Użyjmy 2.0.16 na przykład:</span><span class="sxs-lookup"><span data-stu-id="3039d-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="3039d-142">2.1 możemy użyć 2.1.4 na przykład:</span><span class="sxs-lookup"><span data-stu-id="3039d-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="3039d-143">Po zainstalowaniu agenta platformy Azure jest dobrym pomysłem jest sprawdzenie, czy działa:</span><span class="sxs-lookup"><span data-stu-id="3039d-143">After you install Azure Agent, it's a good idea to verify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="3039d-144">Anulowanie zastrzeżenia systemu.</span><span class="sxs-lookup"><span data-stu-id="3039d-144">Deprovision the system.</span></span>

    <span data-ttu-id="3039d-145">Anulowanie zastrzeżenia systemu do czyszczenia go i była odpowiednia dla reprovisioning.</span><span class="sxs-lookup"><span data-stu-id="3039d-145">Deprovision the system to clean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="3039d-146">Następujące polecenie spowoduje również usunięcie ostatnie konto użytkownika elastycznie i skojarzone dane:</span><span class="sxs-lookup"><span data-stu-id="3039d-146">The following command also deletes the last provisioned user account and the associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="3039d-147">Teraz można zamknąć maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3039d-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="3039d-148">Krok 2: Utwórz konto magazynu na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3039d-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="3039d-149">Potrzebujesz konta magazynu na platformie Azure, aby przekazać plik VHD, może służyć do tworzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3039d-149">You need a storage account in Azure to upload a .vhd file so it can be used to create a virtual machine.</span></span> <span data-ttu-id="3039d-150">Klasyczny portal Azure umożliwia tworzenie konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3039d-150">You can use the Azure classic portal to create a storage account.</span></span>

1. <span data-ttu-id="3039d-151">Zaloguj się do [klasycznej witryny Azure Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3039d-151">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="3039d-152">Na pasku poleceń Wybierz **nowy**.</span><span class="sxs-lookup"><span data-stu-id="3039d-152">On the command bar, select **New**.</span></span>
3. <span data-ttu-id="3039d-153">Wybierz **usług danych** > **magazynu** > **szybkie tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="3039d-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![Szybkie tworzenie konta magazynu](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="3039d-155">Należy wypełnić pola w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="3039d-155">Fill out the fields as follows:</span></span>

   * <span data-ttu-id="3039d-156">W **adres URL** wpisz nazwę domeny podrzędnej do użycia w adresie URL konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3039d-156">In the **URL** field, type a subdomain name to use in the storage account URL.</span></span> <span data-ttu-id="3039d-157">Wpis może zawierać od 3 do 24 cyfry i małe litery.</span><span class="sxs-lookup"><span data-stu-id="3039d-157">The entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="3039d-158">Ta nazwa jest używana jako nazwa hosta, w ramach adresu URL, która jest wykorzystywana do adresowania magazynu obiektów Blob platformy Azure, magazyn kolejek Azure lub zasobów magazynu tabel Azure dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3039d-158">This name becomes the host name within the URL that is used to address Azure Blob storage, Azure Queue storage, or Azure Table storage resources for the subscription.</span></span>
   * <span data-ttu-id="3039d-159">W **grupa lokalizacji/koligacji** menu rozwijanego wybierz **lokalizacja lub grupa koligacji** dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3039d-159">In the **Location/Affinity Group** drop-down menu, choose the **location or affinity group** for the storage account.</span></span> <span data-ttu-id="3039d-160">Grupa koligacji pozwala umieścić usługi w chmurze i magazynu w tym samym centrum danych.</span><span class="sxs-lookup"><span data-stu-id="3039d-160">An affinity group lets you put your cloud services and storage in the same data center.</span></span>
   * <span data-ttu-id="3039d-161">W **replikacji** Określ, czy używać **geograficznie nadmiarowego** replikacji dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3039d-161">In the **Replication** field, decide whether to use **Geo-Redundant** replication for the storage account.</span></span> <span data-ttu-id="3039d-162">Replikacja geograficzna jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="3039d-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="3039d-163">Ta opcja replikuje dane do lokalizacji dodatkowej, bez ponoszenia kosztów, tak, aby Magazyn awaryjnie przełącza działanie do tej lokalizacji w przypadku poważnej awarii w lokalizacji głównej.</span><span class="sxs-lookup"><span data-stu-id="3039d-163">This option replicates your data to a secondary location, at no cost to you, so that your storage fails over to that location if a major failure occurs at the primary location.</span></span> <span data-ttu-id="3039d-164">Lokalizacja dodatkowa jest przypisywany automatycznie i nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="3039d-164">The secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="3039d-165">Jeśli potrzebujesz większej kontroli nad lokalizacji magazynu oparte na chmurze ze względu na wymagania prawne i zasady organizacji, można wyłączyć replikacji geograficznej.</span><span class="sxs-lookup"><span data-stu-id="3039d-165">If you need more control over the location of your cloud-based storage due to legal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="3039d-166">Należy jednak pamiętać, że jeśli później włączyć replikację geograficzną zostanie naliczona opłaty transfer jednorazowe danych w celu replikowania istniejących danych do lokalizacji dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="3039d-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee to replicate your existing data to the secondary location.</span></span> <span data-ttu-id="3039d-167">Usługi magazynu bez — replikacja geograficzna jest oferowany z rabatem.</span><span class="sxs-lookup"><span data-stu-id="3039d-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="3039d-168">Więcej informacji o zarządzaniu — replikacja geograficzna kont magazynu można znaleźć tutaj: [replikacja usługi Azure Storage](../../../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="3039d-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![Wprowadź szczegóły konta magazynu](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="3039d-170">Wybierz **utworzyć konto magazynu**.</span><span class="sxs-lookup"><span data-stu-id="3039d-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="3039d-171">Konto jest teraz wyświetlany w obszarze **magazynu**.</span><span class="sxs-lookup"><span data-stu-id="3039d-171">The account now appears under **storage**.</span></span>

    ![Pomyślnie utworzono konto magazynu](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="3039d-173">Następnie należy utworzyć kontener dla plików VHD przekazane.</span><span class="sxs-lookup"><span data-stu-id="3039d-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="3039d-174">Wybierz nazwę konta magazynu, a następnie wybierz **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="3039d-174">Select the storage account name, and then select **Containers**.</span></span>

    ![Szczegóły konta magazynu](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="3039d-176">Wybierz **utworzyć kontener**.</span><span class="sxs-lookup"><span data-stu-id="3039d-176">Select **Create a Container**.</span></span>

    ![Szczegóły konta magazynu](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="3039d-178">W **nazwa** wpisz nazwę użytkownika kontenera.</span><span class="sxs-lookup"><span data-stu-id="3039d-178">In the **Name** field, type a name for your container.</span></span> <span data-ttu-id="3039d-179">Następnie w **dostępu** menu rozwijanego, wybierz typ zasad dostępu ma.</span><span class="sxs-lookup"><span data-stu-id="3039d-179">Then, in the **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![Nazwa kontenera](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="3039d-181">Domyślnie kontener jest prywatny i jest dostępny tylko przez właściciela konta.</span><span class="sxs-lookup"><span data-stu-id="3039d-181">By default, the container is private and can only be accessed by the account owner.</span></span> <span data-ttu-id="3039d-182">Aby zezwolić na publiczny dostęp do odczytu do obiektów blob w kontenerze, ale nie do właściwości kontenera i metadanych, należy użyć **publicznego obiektu Blob** opcji.</span><span class="sxs-lookup"><span data-stu-id="3039d-182">To allow public read access to the blobs in the container, but not to the container properties and metadata, use the **Public Blob** option.</span></span> <span data-ttu-id="3039d-183">Aby umożliwić pełnej publiczny dostęp do odczytu do kontenera i obiektów blob, należy użyć **publicznego kontenera** opcji.</span><span class="sxs-lookup"><span data-stu-id="3039d-183">To allow full public read access for the container and blobs, use the **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-the-connection-to-azure"></a><span data-ttu-id="3039d-184">Krok 3: Przygotowanie połączenia z platformą Azure</span><span class="sxs-lookup"><span data-stu-id="3039d-184">Step 3: Prepare the connection to Azure</span></span>
<span data-ttu-id="3039d-185">Zanim można przekazać pliku VHD, należy ustanowić bezpiecznego połączenia między komputerem i Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3039d-185">Before you can upload a .vhd file, you need to establish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="3039d-186">Aby wykonać to zadanie, można użyć metody usługi Azure Active Directory (Azure AD) lub certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="3039d-186">You can use the Azure Active Directory (Azure AD) method or the certificate method to do it.</span></span>

### <a name="use-the-azure-ad-method-to-upload-a-vhd-file"></a><span data-ttu-id="3039d-187">Przekaż plik VHD przy użyciu metody usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3039d-187">Use the Azure AD method to upload a .vhd file</span></span>
1. <span data-ttu-id="3039d-188">Otwórz konsolę programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3039d-188">Open the Azure PowerShell console.</span></span>
2. <span data-ttu-id="3039d-189">Wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="3039d-189">Type the following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="3039d-190">To polecenie powoduje otwarcie okna logowania której możesz zalogować się przy użyciu konta służbowego.</span><span class="sxs-lookup"><span data-stu-id="3039d-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![Okno programu PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="3039d-192">Azure uwierzytelnia i zapisanie informacji o poświadczeniach.</span><span class="sxs-lookup"><span data-stu-id="3039d-192">Azure authenticates and saves the credential information.</span></span> <span data-ttu-id="3039d-193">Następnie zamyka okna.</span><span class="sxs-lookup"><span data-stu-id="3039d-193">Then it closes the window.</span></span>

### <a name="use-the-certificate-method-to-upload-a-vhd-file"></a><span data-ttu-id="3039d-194">Przekaż plik VHD przy użyciu metody certyfikatu</span><span class="sxs-lookup"><span data-stu-id="3039d-194">Use the certificate method to upload a .vhd file</span></span>
1. <span data-ttu-id="3039d-195">Otwórz konsolę programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3039d-195">Open the Azure PowerShell console.</span></span>
2. <span data-ttu-id="3039d-196">Typ: `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="3039d-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="3039d-197">Oknie przeglądarki zostanie otwarty i wyświetli monit o pobranie pliku .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="3039d-197">A browser window opens and prompts you to download the .publishsettings file.</span></span> <span data-ttu-id="3039d-198">Ten plik zawiera informacje i certyfikatu dla Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3039d-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![Strona pobierania przeglądarki](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="3039d-200">Zapisz plik .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="3039d-200">Save the .publishsettings file.</span></span>
5. <span data-ttu-id="3039d-201">Typ: `Import-AzurePublishSettingsFile <PathToFile>`, gdzie `<PathToFile>` jest pełną ścieżką do pliku .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="3039d-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is the full path to the .publishsettings file.</span></span>

   <span data-ttu-id="3039d-202">Aby uzyskać więcej informacji, zobacz [wprowadzenie do poleceń cmdlet systemu Azure](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span><span class="sxs-lookup"><span data-stu-id="3039d-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="3039d-203">Aby uzyskać więcej informacji na temat instalowania i konfigurowania programu PowerShell, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3039d-203">For more information about installing and configuring PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-the-vhd-file"></a><span data-ttu-id="3039d-204">Krok 4: Przekaż plik VHD</span><span class="sxs-lookup"><span data-stu-id="3039d-204">Step 4: Upload the .vhd file</span></span>
<span data-ttu-id="3039d-205">Podczas przekazywania pliku VHD, należy go umieścić w dowolnym w ramach usługi magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="3039d-205">When you upload the .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="3039d-206">Poniżej przedstawiono niektóre warunki, które będą używane podczas przekazywania pliku:</span><span class="sxs-lookup"><span data-stu-id="3039d-206">Following are some terms you will use when you upload the file:</span></span>

* <span data-ttu-id="3039d-207">**BlobStorageURL** jest adres URL dla konta magazynu, który został utworzony w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="3039d-207">**BlobStorageURL** is the URL for the storage account that you created in Step 2.</span></span>
* <span data-ttu-id="3039d-208">**YourImagesFolder** jest kontenera w magazynie obiektów Blob, w którym mają być przechowywane obrazy.</span><span class="sxs-lookup"><span data-stu-id="3039d-208">**YourImagesFolder** is the container within Blob storage where you want to store your images.</span></span>
* <span data-ttu-id="3039d-209">**VHDName** jest etykietę wyświetlaną w klasycznym portalu Azure, aby zidentyfikować wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="3039d-209">**VHDName** is the label that appears in the Azure classic portal to identify the virtual hard disk.</span></span>
* <span data-ttu-id="3039d-210">**PathToVHDFile** jest pełna ścieżka i nazwa pliku VHD.</span><span class="sxs-lookup"><span data-stu-id="3039d-210">**PathToVHDFile** is the full path and name of the .vhd file.</span></span>

<span data-ttu-id="3039d-211">W oknie programu Azure PowerShell używanego w poprzednim kroku wpisz:</span><span class="sxs-lookup"><span data-stu-id="3039d-211">From the Azure PowerShell window you used in the previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-the-uploaded-vhd-file"></a><span data-ttu-id="3039d-212">Krok 5: Tworzenie maszyny Wirtualnej z pliku VHD przekazany</span><span class="sxs-lookup"><span data-stu-id="3039d-212">Step 5: Create a VM with the uploaded .vhd file</span></span>
<span data-ttu-id="3039d-213">Po przekazaniu pliku VHD, można dodać go jako obraz do listy niestandardowych obrazów, które są skojarzone z subskrypcją i Utwórz maszynę wirtualną z tego obrazu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="3039d-213">After you upload the .vhd file, you can add it as an image to the list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="3039d-214">W oknie programu Azure PowerShell używanego w poprzednim kroku wpisz:</span><span class="sxs-lookup"><span data-stu-id="3039d-214">From the Azure PowerShell window you used in the previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of the VHD> -OS <Type of the OS on the VHD>

   > [!NOTE]
   > <span data-ttu-id="3039d-215">Użyj systemu Linux jako typ systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="3039d-215">Use Linux as the OS type.</span></span> <span data-ttu-id="3039d-216">Bieżąca wersja programu Azure PowerShell akceptuje tylko "Linux" lub "Windows" jako parametru.</span><span class="sxs-lookup"><span data-stu-id="3039d-216">The current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="3039d-217">Po wykonaniu poprzednich kroków nowy obraz znajduje się w przypadku **obrazów** karty w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3039d-217">After you complete the previous steps, the new image is listed when you choose the **Images** tab on the Azure classic portal.</span></span>  

    ![Wybierz obraz](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="3039d-219">Utwórz maszynę wirtualną z galerii.</span><span class="sxs-lookup"><span data-stu-id="3039d-219">Create a virtual machine from the gallery.</span></span> <span data-ttu-id="3039d-220">Ten nowy obraz jest teraz dostępna w obszarze **Moje obrazy**.</span><span class="sxs-lookup"><span data-stu-id="3039d-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="3039d-221">Wybierz nowy obraz.</span><span class="sxs-lookup"><span data-stu-id="3039d-221">Select the new image.</span></span> <span data-ttu-id="3039d-222">Następnie należy przejść przez z monitami, aby skonfigurować nazwę hosta, hasła, klucz SSH i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="3039d-222">Next, go through the prompts to set up a host name, password, SSH key, and so on.</span></span>

    ![Obraz niestandardowy](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="3039d-224">Po ukończeniu inicjowania obsługi administracyjnej, zobaczysz maszyny Wirtualnej FreeBSD działające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3039d-224">After you complete the provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![Obraz FreeBSD na platformie azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
