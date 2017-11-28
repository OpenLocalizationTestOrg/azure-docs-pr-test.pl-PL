---
title: "Azure: Szybki start — Tworzenie maszyn wirtualnych za pomocą portalu | Microsoft Docs"
description: "Azure: Szybki start — Tworzenie maszyn wirtualnych za pomocą portalu"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: d009020e86fdfed6a45b5b63b9664c623bcb1843
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-linux-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="a0628-103">Tworzenie maszyny wirtualnej z systemem Linux za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a0628-103">Create a Linux virtual machine with the Azure portal</span></span>

<span data-ttu-id="a0628-104">Maszyny wirtualne platformy Azure można utworzyć za pomocą witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a0628-104">Azure virtual machines can be created through the Azure portal.</span></span> <span data-ttu-id="a0628-105">Ta metoda bazuje na opartym na przeglądarce interfejsie użytkownika umożliwiającym tworzenie i konfigurowanie maszyn wirtualnych oraz wszystkich pokrewnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="a0628-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="a0628-106">Ten przewodnik Szybki start opisuje proces tworzenia maszyny wirtualnej i instalowania serwera sieci Web na tej maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a0628-106">This Quickstart steps through creating a virtual machine and installing a webserver on the VM.</span></span>

<span data-ttu-id="a0628-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="a0628-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-ssh-key-pair"></a><span data-ttu-id="a0628-108">Tworzenie pary kluczy SSH</span><span class="sxs-lookup"><span data-stu-id="a0628-108">Create SSH key pair</span></span>

<span data-ttu-id="a0628-109">Do wykonania kroków tego przewodnika Szybki start konieczne jest posiadanie pary kluczy SSH.</span><span class="sxs-lookup"><span data-stu-id="a0628-109">You need an SSH key pair to complete this quick start.</span></span> <span data-ttu-id="a0628-110">Jeśli masz już parę kluczy SSH, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="a0628-110">If you have an existing SSH key pair, this step can be skipped.</span></span>

<span data-ttu-id="a0628-111">Korzystając z powłoki Bash, uruchom to polecenie i wykonaj instrukcje wyświetlane na ekranie.</span><span class="sxs-lookup"><span data-stu-id="a0628-111">From a Bash shell, run this command and follow the on-screen directions.</span></span> <span data-ttu-id="a0628-112">Dane wyjściowe polecenia zawierają nazwę pliku klucza publicznego.</span><span class="sxs-lookup"><span data-stu-id="a0628-112">The command output includes the file name of the public key file.</span></span> <span data-ttu-id="a0628-113">Skopiuj zawartość pliku klucza publicznego do schowka.</span><span class="sxs-lookup"><span data-stu-id="a0628-113">Copy the contents of the public key file to the clipboard.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-to-azure"></a><span data-ttu-id="a0628-114">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a0628-114">Log in to Azure</span></span> 

<span data-ttu-id="a0628-115">Zaloguj się w witrynie Azure Portal pod adresem http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="a0628-115">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="a0628-116">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a0628-116">Create virtual machine</span></span>

1. <span data-ttu-id="a0628-117">Kliknij przycisk **Nowy** znajdujący się w lewym górnym rogu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a0628-117">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="a0628-118">Wybierz pozycję **Wystąpienia obliczeniowe**, a następnie wybierz pozycję **Ubuntu Server 16.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="a0628-118">Select **Compute**, and then select **Ubuntu Server 16.04 LTS**.</span></span> 

3. <span data-ttu-id="a0628-119">Wprowadź informacje o maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a0628-119">Enter the virtual machine information.</span></span> <span data-ttu-id="a0628-120">W obszarze **Typ uwierzytelniania** wybierz pozycję **Klucz publiczny SSH**.</span><span class="sxs-lookup"><span data-stu-id="a0628-120">For **Authentication type**, select **SSH public key**.</span></span> <span data-ttu-id="a0628-121">Podczas wklejania klucza publicznego SSH pamiętaj, aby usunąć wszystkie wiodące i końcowe białe znaki.</span><span class="sxs-lookup"><span data-stu-id="a0628-121">When pasting in your SSH public key, take care to remove any leading or trailing white space.</span></span> <span data-ttu-id="a0628-122">Po zakończeniu kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0628-122">When complete, click **OK**.</span></span>

    ![Wprowadzanie podstawowych informacji o maszynie wirtualnej w bloku portalu](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. <span data-ttu-id="a0628-124">Wybierz rozmiar maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a0628-124">Select a size for the VM.</span></span> <span data-ttu-id="a0628-125">Aby wyświetlić więcej rozmiarów, wybierz pozycje **Wyświetl wszystkie** lub zmień filtr **Obsługiwany typ dysku**.</span><span class="sxs-lookup"><span data-stu-id="a0628-125">To see more sizes, select **View all** or change the **Supported disk type** filter.</span></span> 

    ![Zrzut ekranu przedstawiający rozmiary maszyn wirtualnych](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. <span data-ttu-id="a0628-127">W bloku ustawień pozostaw ustawienia domyślne i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0628-127">On the settings blade, keep the defaults and click **OK**.</span></span>

6. <span data-ttu-id="a0628-128">Na stronie podsumowania kliknij przycisk **OK**, aby rozpocząć wdrażanie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a0628-128">On the summary page, click **Ok** to start the virtual machine deployment.</span></span>

7. <span data-ttu-id="a0628-129">Maszyna wirtualna zostanie przypięta do pulpitu nawigacyjnego witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a0628-129">The VM will be pinned to the Azure portal dashboard.</span></span> <span data-ttu-id="a0628-130">Po zakończeniu wdrożenia zostanie automatycznie otwarty blok podsumowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a0628-130">Once the deployment has completed, the VM summary blade automatically opens.</span></span>


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="a0628-131">Nawiązywanie połączenia z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="a0628-131">Connect to virtual machine</span></span>

<span data-ttu-id="a0628-132">Utwórz połączenie SSH z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="a0628-132">Create an SSH connection with the virtual machine.</span></span>

1. <span data-ttu-id="a0628-133">Kliknij przycisk **Połącz** w bloku maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a0628-133">Click the **Connect** button on the virtual machine blade.</span></span> <span data-ttu-id="a0628-134">Na przycisku połączenia są wyświetlane parametry połączenia SSH, których można użyć do nawiązania połączenia z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="a0628-134">The connect button displays an SSH connection string that can be used to connect to the virtual machine.</span></span>

    ![Portal 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="a0628-136">Uruchom następujące polecenie, aby utworzyć sesję SSH.</span><span class="sxs-lookup"><span data-stu-id="a0628-136">Run the following command to create an SSH session.</span></span> <span data-ttu-id="a0628-137">Zastąp parametry połączenia wartościami skopiowanymi z witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a0628-137">Replace the connection string with the one you copied from the Azure portal.</span></span>

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a><span data-ttu-id="a0628-138">Instalowanie serwera NGINX</span><span class="sxs-lookup"><span data-stu-id="a0628-138">Install NGINX</span></span>

<span data-ttu-id="a0628-139">Użyj poniższego skryptu powłoki systemowej w celu zaktualizowania źródeł pakietów i zainstalowania najnowszego pakietu NGINX.</span><span class="sxs-lookup"><span data-stu-id="a0628-139">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

<span data-ttu-id="a0628-140">Po zakończeniu zamknij sesję SSH i wróć do właściwości maszyny wirtualnej w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a0628-140">When done, exit the SSH session and return the VM properties in the Azure portal.</span></span>


## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="a0628-141">Otwieranie portu 80 na potrzeby ruchu w sieci Web</span><span class="sxs-lookup"><span data-stu-id="a0628-141">Open port 80 for web traffic</span></span> 

<span data-ttu-id="a0628-142">Sieciowa grupa zabezpieczeń zabezpiecza ruch przychodzący i wychodzący.</span><span class="sxs-lookup"><span data-stu-id="a0628-142">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="a0628-143">Po utworzeniu maszyny wirtualnej z poziomu witryny Azure Portal na porcie 22 jest tworzona reguła ruchu przychodzącego dla połączeń SSH.</span><span class="sxs-lookup"><span data-stu-id="a0628-143">When a VM is created from the Azure portal, an inbound rule is created on port 22 for SSH connections.</span></span> <span data-ttu-id="a0628-144">Ponieważ maszyna wirtualna hostuje serwer sieci Web, należy utworzyć regułę sieciowej grupy zabezpieczeń dla portu 80.</span><span class="sxs-lookup"><span data-stu-id="a0628-144">Because this VM hosts a webserver, an NSG rule needs to be created for port 80.</span></span>

1. <span data-ttu-id="a0628-145">Na maszynie wirtualnej kliknij nazwę **grupy zasobów**.</span><span class="sxs-lookup"><span data-stu-id="a0628-145">On the virtual machine, click the name of the **Resource group**.</span></span>
2. <span data-ttu-id="a0628-146">Wybierz **sieciową grupę zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="a0628-146">Select the **network security group**.</span></span> <span data-ttu-id="a0628-147">Sieciową grupę zabezpieczeń można zidentyfikować za pomocą kolumny **Typ**.</span><span class="sxs-lookup"><span data-stu-id="a0628-147">The NSG can be identified using the **Type** column.</span></span> 
3. <span data-ttu-id="a0628-148">W menu po lewej stronie, w obszarze ustawień, kliknij pozycję **Reguły zabezpieczeń dla ruchu przychodzącego**.</span><span class="sxs-lookup"><span data-stu-id="a0628-148">On the left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="a0628-149">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a0628-149">Click on **Add**.</span></span>
5. <span data-ttu-id="a0628-150">W polu **Nazwa** wpisz wartość **http**.</span><span class="sxs-lookup"><span data-stu-id="a0628-150">In **Name**, type **http**.</span></span> <span data-ttu-id="a0628-151">Upewnij się, że w polu **Zakres portów** ustawiono wartość 80, a w polu **Akcja** — wartość **Zezwalaj**.</span><span class="sxs-lookup"><span data-stu-id="a0628-151">Make sure **Port range** is set to 80 and **Action** is set to **Allow**.</span></span> 
6. <span data-ttu-id="a0628-152">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0628-152">Click **OK**.</span></span>


## <a name="view-the-nginx-welcome-page"></a><span data-ttu-id="a0628-153">Wyświetlanie strony powitalnej serwera NGINX</span><span class="sxs-lookup"><span data-stu-id="a0628-153">View the NGINX welcome page</span></span>

<span data-ttu-id="a0628-154">Po zainstalowaniu serwera NGINX i otwarciu portu 80 dla maszyny wirtualnej można uzyskać dostęp do serwera sieci Web z Internetu.</span><span class="sxs-lookup"><span data-stu-id="a0628-154">With NGINX installed, and port 80 open to your VM, the webserver can now be accessed from the internet.</span></span> <span data-ttu-id="a0628-155">Otwórz przeglądarkę internetową i wpisz publiczny adres IP maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a0628-155">Open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="a0628-156">Publiczny adres IP można znaleźć w bloku maszyny wirtualnej w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a0628-156">The public IP address can be found on the VM blade in the Azure portal.</span></span>

![Domyślna witryna serwera NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="a0628-158">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="a0628-158">Clean up resources</span></span>

<span data-ttu-id="a0628-159">Gdy grupa zasobów, maszyna wirtualna i wszystkie pokrewne zasoby nie będą już potrzebne, można je usunąć.</span><span class="sxs-lookup"><span data-stu-id="a0628-159">When no longer needed, delete the resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="a0628-160">W tym celu wybierz grupę zasobów z bloku maszyny wirtualnej, a następnie kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="a0628-160">To do so, select the resource group from the virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0628-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a0628-161">Next steps</span></span>

<span data-ttu-id="a0628-162">W tym przewodniku Szybki start została wdrożona prosta maszyna wirtualna i reguła sieciowej grupy zabezpieczeń oraz zainstalowano serwer sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a0628-162">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="a0628-163">Aby dowiedzieć się więcej o maszynach wirtualnych platformy Azure, przejdź do samouczka dla maszyn wirtualnych z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="a0628-163">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a0628-164">Samouczki dla maszyny wirtualnej platformy Azure z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="a0628-164">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
