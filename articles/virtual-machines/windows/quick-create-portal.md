---
title: Szybki Start - aaaAzure Tworzenie portalu maszyny Wirtualnej z systemem Windows | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 5646ad51244db6d214c0121d1f7cc45c59f9a78b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="8c255-103">Utwórz maszynę wirtualną systemu Windows z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8c255-103">Create a Windows virtual machine with hello Azure portal</span></span>

<span data-ttu-id="8c255-104">Maszyny wirtualne platformy Azure mogą być tworzone za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8c255-104">Azure virtual machines can be created through hello Azure portal.</span></span> <span data-ttu-id="8c255-105">Ta metoda bazuje na opartym na przeglądarce interfejsie użytkownika umożliwiającym tworzenie i konfigurowanie maszyn wirtualnych oraz wszystkich pokrewnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="8c255-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="8c255-106">Ta procedura Szybki Start do utworzenia maszyny wirtualnej oraz jest instalowany serwer sieci Web na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8c255-106">This Quickstart steps through creating a virtual machine and installing a webserver on hello VM.</span></span>

<span data-ttu-id="8c255-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="8c255-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="8c255-108">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="8c255-108">Log in tooAzure</span></span>

<span data-ttu-id="8c255-109">Zaloguj się za toohello portalu Azure w http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="8c255-109">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="8c255-110">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="8c255-110">Create virtual machine</span></span>

1. <span data-ttu-id="8c255-111">Kliknij przycisk hello **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8c255-111">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="8c255-112">Wybierz pozycję **Wystąpienia obliczeniowe**, a następnie wybierz pozycję **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="8c255-112">Select **Compute**, and then select **Windows Server 2016 Datacenter**.</span></span> 

3. <span data-ttu-id="8c255-113">Wprowadź informacje o maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="8c255-113">Enter hello virtual machine information.</span></span> <span data-ttu-id="8c255-114">Hello nazwy użytkownika i hasła wprowadzonego w tym miejscu jest używane toolog toohello maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8c255-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="8c255-115">Po zakończeniu kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8c255-115">When complete, click **OK**.</span></span>

    ![Podaj podstawowe informacje dotyczące maszyny Wirtualnej w bloku portalu hello](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. <span data-ttu-id="8c255-117">Wybierz rozmiar hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8c255-117">Select a size for hello VM.</span></span> <span data-ttu-id="8c255-118">Wybierz więcej rozmiary toosee **Wyświetl wszystkie** lub zmień hello **obsługiwany typ dysku** filtru.</span><span class="sxs-lookup"><span data-stu-id="8c255-118">toosee more sizes, select **View all** or change hello **Supported disk type** filter.</span></span> 

    ![Zrzut ekranu przedstawiający rozmiary maszyn wirtualnych](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. <span data-ttu-id="8c255-120">W bloku ustawień hello zachować hello wartości domyślne, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8c255-120">On hello settings blade, keep hello defaults and click **OK**.</span></span>

6. <span data-ttu-id="8c255-121">Na stronie Podsumowanie powitania kliknij **Ok** wdrożenia maszyny wirtualnej hello toostart.</span><span class="sxs-lookup"><span data-stu-id="8c255-121">On hello summary page, click **Ok** toostart hello virtual machine deployment.</span></span>

7. <span data-ttu-id="8c255-122">Witaj maszyny Wirtualnej będzie przypiętych toohello pulpitu nawigacyjnego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8c255-122">hello VM will be pinned toohello Azure portal dashboard.</span></span> <span data-ttu-id="8c255-123">Po zakończeniu wdrażania hello bloku podsumowania hello maszyny Wirtualnej automatycznie otwiera.</span><span class="sxs-lookup"><span data-stu-id="8c255-123">Once hello deployment has completed, hello VM summary blade automatically opens.</span></span>


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="8c255-124">Podłącz maszynę toovirtual</span><span class="sxs-lookup"><span data-stu-id="8c255-124">Connect toovirtual machine</span></span>

<span data-ttu-id="8c255-125">Utwórz maszynę wirtualną toohello połączeń usług pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="8c255-125">Create a remote desktop connection toohello virtual machine.</span></span>

1. <span data-ttu-id="8c255-126">Kliknij przycisk hello **Connect** przycisk na powitania właściwości maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8c255-126">Click hello **Connect** button on hello virtual machine properties.</span></span> <span data-ttu-id="8c255-127">Zostanie utworzony i pobrany plik Remote Desktop Protocol (rdp).</span><span class="sxs-lookup"><span data-stu-id="8c255-127">A Remote Desktop Protocol file (.rdp file) is created and downloaded.</span></span>

    ![Portal 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="8c255-129">tooyour tooconnect maszynę Wirtualną, otwórz hello pobrany plik RDP.</span><span class="sxs-lookup"><span data-stu-id="8c255-129">tooconnect tooyour VM, open hello downloaded RDP file.</span></span> <span data-ttu-id="8c255-130">Jeśli zostanie wyświetlony monit, kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="8c255-130">If prompted, click **Connect**.</span></span> <span data-ttu-id="8c255-131">Na komputerze Mac, należy klienta RDP, takich jak ta [klienta usług pulpitu zdalnego](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) z hello Mac App Store.</span><span class="sxs-lookup"><span data-stu-id="8c255-131">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from hello Mac App Store.</span></span>

3. <span data-ttu-id="8c255-132">Wprowadź hello nazwę użytkownika i hasło określone podczas tworzenia maszyny wirtualnej hello, a następnie kliknij przycisk **Ok**.</span><span class="sxs-lookup"><span data-stu-id="8c255-132">Enter hello user name and password you specified when creating hello virtual machine, then click **Ok**.</span></span>

4. <span data-ttu-id="8c255-133">Może pojawić się ostrzeżenie o certyfikacie podczas hello procesu logowania.</span><span class="sxs-lookup"><span data-stu-id="8c255-133">You may receive a certificate warning during hello sign-in process.</span></span> <span data-ttu-id="8c255-134">Kliknij przycisk **tak** lub **Kontynuuj** tooproceed z połączeniem hello.</span><span class="sxs-lookup"><span data-stu-id="8c255-134">Click **Yes** or **Continue** tooproceed with hello connection.</span></span>


## <a name="install-iis-using-powershell"></a><span data-ttu-id="8c255-135">Instalowanie usług IIS przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c255-135">Install IIS using PowerShell</span></span>

<span data-ttu-id="8c255-136">Na maszynie wirtualnej hello Uruchom sesję programu PowerShell i uruchom hello następujące polecenia tooinstall usług IIS.</span><span class="sxs-lookup"><span data-stu-id="8c255-136">On hello virtual machine, start a PowerShell session and run hello following command tooinstall IIS.</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="8c255-137">Po zakończeniu zamknąć sesji protokołu RDP hello i zwróć hello właściwości maszyny Wirtualnej na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8c255-137">When done, exit hello RDP session and return hello VM properties in hello Azure portal.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="8c255-138">Otwieranie portu 80 na potrzeby ruchu w sieci Web</span><span class="sxs-lookup"><span data-stu-id="8c255-138">Open port 80 for web traffic</span></span> 

<span data-ttu-id="8c255-139">Sieciowa grupa zabezpieczeń zabezpiecza ruch przychodzący i wychodzący.</span><span class="sxs-lookup"><span data-stu-id="8c255-139">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="8c255-140">Po utworzeniu maszyny Wirtualnej z portalu Azure hello tworzona jest reguła dla ruchu przychodzącego z portu 3389 połączenia RDP.</span><span class="sxs-lookup"><span data-stu-id="8c255-140">When a VM is created from hello Azure portal, an inbound rule is created on port 3389 for RDP connections.</span></span> <span data-ttu-id="8c255-141">Ponieważ ta maszyna wirtualna znajduje się serwer sieci Web, reguły NSG musi toobe utworzony dla portu 80.</span><span class="sxs-lookup"><span data-stu-id="8c255-141">Because this VM hosts a webserver, an NSG rule needs toobe created for port 80.</span></span>

1. <span data-ttu-id="8c255-142">Na maszynie wirtualnej hello, kliknij nazwę hello hello **grupy zasobów**.</span><span class="sxs-lookup"><span data-stu-id="8c255-142">On hello virtual machine, click hello name of hello **Resource group**.</span></span>
2. <span data-ttu-id="8c255-143">Wybierz hello **sieciowej grupy zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="8c255-143">Select hello **network security group**.</span></span> <span data-ttu-id="8c255-144">Witaj grupy NSG mogą zostać zidentyfikowane przy użyciu hello **typu** kolumny.</span><span class="sxs-lookup"><span data-stu-id="8c255-144">hello NSG can be identified using hello **Type** column.</span></span> 
3. <span data-ttu-id="8c255-145">W menu po lewej stronie powitania, w obszarze Ustawienia, kliknij polecenie **reguły zabezpieczeń dla ruchu przychodzącego**.</span><span class="sxs-lookup"><span data-stu-id="8c255-145">On hello left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="8c255-146">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="8c255-146">Click on **Add**.</span></span>
5. <span data-ttu-id="8c255-147">W polu **Nazwa** wpisz wartość **http**.</span><span class="sxs-lookup"><span data-stu-id="8c255-147">In **Name**, type **http**.</span></span> <span data-ttu-id="8c255-148">Upewnij się, że **zakres portów** ustawiono too80 i **akcji** ustawiono zbyt**Zezwalaj**.</span><span class="sxs-lookup"><span data-stu-id="8c255-148">Make sure **Port range** is set too80 and **Action** is set too**Allow**.</span></span> 
6. <span data-ttu-id="8c255-149">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8c255-149">Click **OK**.</span></span>


## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="8c255-150">Widok hello strona powitalna usług IIS</span><span class="sxs-lookup"><span data-stu-id="8c255-150">View hello IIS welcome page</span></span>

<span data-ttu-id="8c255-151">Z programem IIS zainstalowanych i port 80 Otwórz tooyour maszyny Wirtualnej, hello serwer sieci Web jest teraz dostępna z hello internet.</span><span class="sxs-lookup"><span data-stu-id="8c255-151">With IIS installed, and port 80 open tooyour VM, hello webserver can now be accessed from hello internet.</span></span> <span data-ttu-id="8c255-152">Otwórz przeglądarkę sieci web, a następnie wprowadź hello publicznego adresu IP hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8c255-152">Open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="8c255-153">Witaj publiczny adres IP można znaleźć w bloku maszyny Wirtualnej hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8c255-153">hello public IP address can be found on hello VM blade in hello Azure portal.</span></span>

![Domyślna witryna usług IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="8c255-155">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="8c255-155">Clean up resources</span></span>

<span data-ttu-id="8c255-156">Gdy nie są już potrzebne, Usuń grupy zasobów hello, maszyny wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="8c255-156">When no longer needed, delete hello resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="8c255-157">toodo tak, zaznacz grupę zasobów hello hello bloku maszyny wirtualnej i kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="8c255-157">toodo so, select hello resource group from hello virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c255-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8c255-158">Next steps</span></span>

<span data-ttu-id="8c255-159">W tym przewodniku Szybki start została wdrożona prosta maszyna wirtualna i reguła sieciowej grupy zabezpieczeń oraz zainstalowano serwer sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8c255-159">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="8c255-160">toolearn więcej informacji o maszynach wirtualnych platformy Azure, nadal samouczek toohello dla maszyn wirtualnych systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="8c255-160">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8c255-161">Samouczki dla maszyny wirtualnej platformy Azure z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="8c255-161">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
