---
title: "Azure: Szybki start — Tworzenie maszyn wirtualnych z systemem Windows za pomocą portalu | Microsoft Docs"
description: "Azure: Szybki start — Tworzenie maszyn wirtualnych z systemem Windows za pomocą portalu"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 31ac18add9c3fd956e0d37b1e0c1a510265c22e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-windows-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="61437-103">Tworzenie maszyny wirtualnej z systemem Windows za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="61437-103">Create a Windows virtual machine with the Azure portal</span></span>

<span data-ttu-id="61437-104">Maszyny wirtualne platformy Azure można utworzyć za pomocą witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="61437-104">Azure virtual machines can be created through the Azure portal.</span></span> <span data-ttu-id="61437-105">Ta metoda bazuje na opartym na przeglądarce interfejsie użytkownika umożliwiającym tworzenie i konfigurowanie maszyn wirtualnych oraz wszystkich pokrewnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="61437-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="61437-106">Ten przewodnik Szybki start opisuje proces tworzenia maszyny wirtualnej i instalowania serwera sieci Web na tej maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61437-106">This Quickstart steps through creating a virtual machine and installing a webserver on the VM.</span></span>

<span data-ttu-id="61437-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="61437-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="61437-108">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="61437-108">Log in to Azure</span></span>

<span data-ttu-id="61437-109">Zaloguj się w witrynie Azure Portal pod adresem http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="61437-109">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="61437-110">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="61437-110">Create virtual machine</span></span>

1. <span data-ttu-id="61437-111">Kliknij przycisk **Nowy** znajdujący się w lewym górnym rogu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="61437-111">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="61437-112">Wybierz pozycję **Wystąpienia obliczeniowe**, a następnie wybierz pozycję **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="61437-112">Select **Compute**, and then select **Windows Server 2016 Datacenter**.</span></span> 

3. <span data-ttu-id="61437-113">Wprowadź informacje o maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61437-113">Enter the virtual machine information.</span></span> <span data-ttu-id="61437-114">Nazwa użytkownika i hasło wprowadzone w tym miejscu są używane na potrzeby logowania się do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61437-114">The user name and password entered here is used to log in to the virtual machine.</span></span> <span data-ttu-id="61437-115">Po zakończeniu kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="61437-115">When complete, click **OK**.</span></span>

    ![Wprowadzanie podstawowych informacji o maszynie wirtualnej w bloku portalu](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. <span data-ttu-id="61437-117">Wybierz rozmiar maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61437-117">Select a size for the VM.</span></span> <span data-ttu-id="61437-118">Aby wyświetlić więcej rozmiarów, wybierz pozycje **Wyświetl wszystkie** lub zmień filtr **Obsługiwany typ dysku**.</span><span class="sxs-lookup"><span data-stu-id="61437-118">To see more sizes, select **View all** or change the **Supported disk type** filter.</span></span> 

    ![Zrzut ekranu przedstawiający rozmiary maszyn wirtualnych](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. <span data-ttu-id="61437-120">W bloku ustawień pozostaw ustawienia domyślne i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="61437-120">On the settings blade, keep the defaults and click **OK**.</span></span>

6. <span data-ttu-id="61437-121">Na stronie podsumowania kliknij przycisk **OK**, aby rozpocząć wdrażanie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61437-121">On the summary page, click **Ok** to start the virtual machine deployment.</span></span>

7. <span data-ttu-id="61437-122">Maszyna wirtualna zostanie przypięta do pulpitu nawigacyjnego witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="61437-122">The VM will be pinned to the Azure portal dashboard.</span></span> <span data-ttu-id="61437-123">Po zakończeniu wdrożenia zostanie automatycznie otwarty blok podsumowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61437-123">Once the deployment has completed, the VM summary blade automatically opens.</span></span>


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="61437-124">Nawiązywanie połączenia z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="61437-124">Connect to virtual machine</span></span>

<span data-ttu-id="61437-125">Utwórz połączenie pulpitu zdalnego z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="61437-125">Create a remote desktop connection to the virtual machine.</span></span>

1. <span data-ttu-id="61437-126">Kliknij przycisk **Połącz** we właściwościach maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61437-126">Click the **Connect** button on the virtual machine properties.</span></span> <span data-ttu-id="61437-127">Zostanie utworzony i pobrany plik Remote Desktop Protocol (rdp).</span><span class="sxs-lookup"><span data-stu-id="61437-127">A Remote Desktop Protocol file (.rdp file) is created and downloaded.</span></span>

    ![Portal 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="61437-129">Aby połączyć się z maszyną wirtualną, otwórz pobrany plik RDP.</span><span class="sxs-lookup"><span data-stu-id="61437-129">To connect to your VM, open the downloaded RDP file.</span></span> <span data-ttu-id="61437-130">Jeśli zostanie wyświetlony monit, kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="61437-130">If prompted, click **Connect**.</span></span> <span data-ttu-id="61437-131">Na komputerze Mac należy skorzystać z klienta RDP, takiego jak ten [klient pulpitu zdalnego](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) ze sklepu Mac App Store.</span><span class="sxs-lookup"><span data-stu-id="61437-131">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from the Mac App Store.</span></span>

3. <span data-ttu-id="61437-132">Wprowadź nazwę użytkownika i hasło określone podczas tworzenia maszyny wirtualnej, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="61437-132">Enter the user name and password you specified when creating the virtual machine, then click **Ok**.</span></span>

4. <span data-ttu-id="61437-133">Podczas procesu logowania może pojawić się ostrzeżenie o certyfikacie.</span><span class="sxs-lookup"><span data-stu-id="61437-133">You may receive a certificate warning during the sign-in process.</span></span> <span data-ttu-id="61437-134">Kliknij przycisk **Tak** lub **Kontynuuj**, aby kontynuować nawiązywanie połączenia.</span><span class="sxs-lookup"><span data-stu-id="61437-134">Click **Yes** or **Continue** to proceed with the connection.</span></span>


## <a name="install-iis-using-powershell"></a><span data-ttu-id="61437-135">Instalowanie usług IIS przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="61437-135">Install IIS using PowerShell</span></span>

<span data-ttu-id="61437-136">Uruchom sesję programu PowerShell na maszynie wirtualnej i uruchom następujące polecenie, aby zainstalować usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="61437-136">On the virtual machine, start a PowerShell session and run the following command to install IIS.</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="61437-137">Po zakończeniu zamknij sesję RDP i wróć do właściwości maszyny wirtualnej w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="61437-137">When done, exit the RDP session and return the VM properties in the Azure portal.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="61437-138">Otwieranie portu 80 na potrzeby ruchu w sieci Web</span><span class="sxs-lookup"><span data-stu-id="61437-138">Open port 80 for web traffic</span></span> 

<span data-ttu-id="61437-139">Sieciowa grupa zabezpieczeń zabezpiecza ruch przychodzący i wychodzący.</span><span class="sxs-lookup"><span data-stu-id="61437-139">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="61437-140">Po utworzeniu maszyny wirtualnej z poziomu witryny Azure Portal na porcie 3389 jest tworzona reguła ruchu przychodzącego dla połączeń RDP.</span><span class="sxs-lookup"><span data-stu-id="61437-140">When a VM is created from the Azure portal, an inbound rule is created on port 3389 for RDP connections.</span></span> <span data-ttu-id="61437-141">Ponieważ maszyna wirtualna hostuje serwer sieci Web, należy utworzyć regułę sieciowej grupy zabezpieczeń dla portu 80.</span><span class="sxs-lookup"><span data-stu-id="61437-141">Because this VM hosts a webserver, an NSG rule needs to be created for port 80.</span></span>

1. <span data-ttu-id="61437-142">Na maszynie wirtualnej kliknij nazwę **grupy zasobów**.</span><span class="sxs-lookup"><span data-stu-id="61437-142">On the virtual machine, click the name of the **Resource group**.</span></span>
2. <span data-ttu-id="61437-143">Wybierz **sieciową grupę zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="61437-143">Select the **network security group**.</span></span> <span data-ttu-id="61437-144">Sieciową grupę zabezpieczeń można zidentyfikować za pomocą kolumny **Typ**.</span><span class="sxs-lookup"><span data-stu-id="61437-144">The NSG can be identified using the **Type** column.</span></span> 
3. <span data-ttu-id="61437-145">W menu po lewej stronie, w obszarze ustawień, kliknij pozycję **Reguły zabezpieczeń dla ruchu przychodzącego**.</span><span class="sxs-lookup"><span data-stu-id="61437-145">On the left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="61437-146">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="61437-146">Click on **Add**.</span></span>
5. <span data-ttu-id="61437-147">W polu **Nazwa** wpisz wartość **http**.</span><span class="sxs-lookup"><span data-stu-id="61437-147">In **Name**, type **http**.</span></span> <span data-ttu-id="61437-148">Upewnij się, że w polu **Zakres portów** ustawiono wartość 80, a w polu **Akcja** — wartość **Zezwalaj**.</span><span class="sxs-lookup"><span data-stu-id="61437-148">Make sure **Port range** is set to 80 and **Action** is set to **Allow**.</span></span> 
6. <span data-ttu-id="61437-149">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="61437-149">Click **OK**.</span></span>


## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="61437-150">Wyświetlanie strony powitalnej usług IIS</span><span class="sxs-lookup"><span data-stu-id="61437-150">View the IIS welcome page</span></span>

<span data-ttu-id="61437-151">Po zainstalowaniu usług IIS i otwarciu portu 80 dla maszyny wirtualnej można uzyskać dostęp do serwera sieci Web z Internetu.</span><span class="sxs-lookup"><span data-stu-id="61437-151">With IIS installed, and port 80 open to your VM, the webserver can now be accessed from the internet.</span></span> <span data-ttu-id="61437-152">Otwórz przeglądarkę internetową i wpisz publiczny adres IP maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61437-152">Open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="61437-153">Publiczny adres IP można znaleźć w bloku maszyny wirtualnej w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="61437-153">the public IP address can be found on the VM blade in the Azure portal.</span></span>

![Domyślna witryna usług IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="61437-155">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="61437-155">Clean up resources</span></span>

<span data-ttu-id="61437-156">Gdy grupa zasobów, maszyna wirtualna i wszystkie pokrewne zasoby nie będą już potrzebne, można je usunąć.</span><span class="sxs-lookup"><span data-stu-id="61437-156">When no longer needed, delete the resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="61437-157">W tym celu wybierz grupę zasobów z bloku maszyny wirtualnej, a następnie kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="61437-157">To do so, select the resource group from the virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61437-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="61437-158">Next steps</span></span>

<span data-ttu-id="61437-159">W tym przewodniku Szybki start została wdrożona prosta maszyna wirtualna i reguła sieciowej grupy zabezpieczeń oraz zainstalowano serwer sieci Web.</span><span class="sxs-lookup"><span data-stu-id="61437-159">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="61437-160">Aby dowiedzieć się więcej o maszynach wirtualnych platformy Azure, przejdź do samouczka dla maszyn wirtualnych z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="61437-160">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="61437-161">Samouczki dla maszyny wirtualnej platformy Azure z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="61437-161">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
