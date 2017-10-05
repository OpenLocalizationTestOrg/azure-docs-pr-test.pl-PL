---
title: "Połączenie z maszyną wirtualną programu SQL Server (Resource Manager) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak nawiązać połączenia z programem SQL Server uruchomiony na maszynie wirtualnej na platformie Azure. W tym temacie używa klasycznego modelu wdrażania. Scenariusze są różne w zależności od konfiguracji sieci i lokalizację klienta."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 67ba43f9456bbeffbf602067586143c4c68af672
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-a-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="72f8f-105">Łączenie z maszyną wirtualną programu SQL Server na platformie Azure (usługa Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="72f8f-105">Connect to a SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="72f8f-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="72f8f-106">Resource Manager</span></span>](virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="72f8f-107">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="72f8f-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="72f8f-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="72f8f-108">Overview</span></span>

<span data-ttu-id="72f8f-109">W tym temacie opisano sposób podłączania do wystąpienia programu SQL Server uruchomiony na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="72f8f-109">This topic describes how to connect to your SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="72f8f-110">Obejmuje on niektóre [scenariusze ogólne łączności](#connection-scenarios) , a następnie oferuje [szczegółowe kroki związane z konfigurowaniem łączności z serwerem SQL w maszynie Wirtualnej platformy Azure](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="72f8f-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="72f8f-111">Jeśli trzeba będzie raczej pełny przewodnik inicjowania obsługi administracyjnej i łączność, zobacz [inicjowania obsługi maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="72f8f-111">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="72f8f-112">Scenariusze łączenia</span><span class="sxs-lookup"><span data-stu-id="72f8f-112">Connection scenarios</span></span>

<span data-ttu-id="72f8f-113">Sposób którą klient nawiąże połączenie z programem SQL Server uruchomiony na maszynie wirtualnej różni się w zależności od lokalizacji klienta i konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="72f8f-113">The way a client connects to SQL Server running on a Virtual Machine differs depending on the location of the client and the networking configuration.</span></span>

<span data-ttu-id="72f8f-114">Jeśli dostarczasz maszyny Wirtualnej programu SQL Server w portalu Azure, masz możliwość określenia typu **łączność z serwerem SQL**.</span><span class="sxs-lookup"><span data-stu-id="72f8f-114">If you provision a SQL Server VM in the Azure portal, you have the option of specifying the type of **SQL connectivity**.</span></span>

![Publiczny opcji łączności SQL podczas inicjowania obsługi](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="72f8f-116">Dostępne opcje dla połączenia:</span><span class="sxs-lookup"><span data-stu-id="72f8f-116">Your options for connectivity include:</span></span>

| <span data-ttu-id="72f8f-117">Opcja</span><span class="sxs-lookup"><span data-stu-id="72f8f-117">Option</span></span> | <span data-ttu-id="72f8f-118">Opis</span><span class="sxs-lookup"><span data-stu-id="72f8f-118">Description</span></span> |
|---|---|
| <span data-ttu-id="72f8f-119">**Publiczna**</span><span class="sxs-lookup"><span data-stu-id="72f8f-119">**Public**</span></span> | <span data-ttu-id="72f8f-120">Połączenia z serwerem SQL w Internecie</span><span class="sxs-lookup"><span data-stu-id="72f8f-120">Connect to SQL Server over the internet</span></span> |
| <span data-ttu-id="72f8f-121">**Prywatne**</span><span class="sxs-lookup"><span data-stu-id="72f8f-121">**Private**</span></span> | <span data-ttu-id="72f8f-122">Połączenia z serwerem SQL w tej samej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="72f8f-122">Connect to SQL Server in the same virtual network</span></span> |
| <span data-ttu-id="72f8f-123">**Lokalne**</span><span class="sxs-lookup"><span data-stu-id="72f8f-123">**Local**</span></span> | <span data-ttu-id="72f8f-124">Połączenia z serwerem SQL lokalnie na tej samej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="72f8f-124">Connect to SQL Server locally on the same virtual machine</span></span> | 

<span data-ttu-id="72f8f-125">W poniższych sekcjach opisano **publicznego** i **prywatnej** szczegółowo opcje.</span><span class="sxs-lookup"><span data-stu-id="72f8f-125">The following sections explain the **Public** and **Private** options in more detail.</span></span>

## <a name="connect-to-sql-server-over-the-internet"></a><span data-ttu-id="72f8f-126">Połączenia z serwerem SQL w Internecie</span><span class="sxs-lookup"><span data-stu-id="72f8f-126">Connect to SQL Server over the Internet</span></span>

<span data-ttu-id="72f8f-127">Jeśli chcesz nawiązać połączenia z aparatem bazy danych programu SQL Server z Internetu, wybierz opcję **publicznego** dla **łączność z serwerem SQL** typu w portalu podczas inicjowania obsługi.</span><span class="sxs-lookup"><span data-stu-id="72f8f-127">If you want to connect to your SQL Server database engine from the Internet, select **Public** for the **SQL connectivity** type in the portal during provisioning.</span></span> <span data-ttu-id="72f8f-128">Portal automatycznie wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="72f8f-128">The portal automatically does the following steps:</span></span>

* <span data-ttu-id="72f8f-129">Włącza protokół TCP/IP dla programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="72f8f-129">Enables the TCP/IP protocol for SQL Server.</span></span>
* <span data-ttu-id="72f8f-130">Konfiguruje regułę zapory, aby otworzyć port TCP programu SQL Server (domyślnie 1433).</span><span class="sxs-lookup"><span data-stu-id="72f8f-130">Configures a firewall rule to open the SQL Server TCP port (default 1433).</span></span>
* <span data-ttu-id="72f8f-131">Umożliwia uwierzytelnianie programu SQL Server wymagane dla dostępu publicznego.</span><span class="sxs-lookup"><span data-stu-id="72f8f-131">Enables SQL Server Authentication, required for public access.</span></span>
* <span data-ttu-id="72f8f-132">Umożliwia skonfigurowanie grupy zabezpieczeń sieci na maszynie Wirtualnej, aby cały ruch TCP na porcie programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="72f8f-132">Configures the network security group on the VM to all TCP traffic on the SQL Server port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72f8f-133">Obrazy maszyny wirtualnej dla programu SQL Server Developer i wersji Express nie należy włączać automatycznie protokołu TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="72f8f-133">The virtual machine images for the SQL Server Developer and Express editions do not automatically enable the TCP/IP protocol.</span></span> <span data-ttu-id="72f8f-134">Dla deweloperów i ekspresowej wersji, należy użyć programu SQL Server Configuration Manager do [ręcznie Włącz protokół TCP/IP](#manualtcp) po utworzeniu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="72f8f-134">For Developer and Express editions, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#manualtcp) after creating the VM.</span></span>

<span data-ttu-id="72f8f-135">Dowolnego klienta z dostępem do Internetu może nawiązać wystąpienie programu SQL Server za pośrednictwem publicznego adresu IP maszyny wirtualnej albo jakakolwiek Etykieta DNS przypisane do tego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="72f8f-135">Any client with internet access can connect to the SQL Server instance by specifying either the public IP address of the virtual machine or any DNS label assigned to that IP address.</span></span> <span data-ttu-id="72f8f-136">Port serwera SQL jest port 1433, nie trzeba określić je w parametrach połączenia.</span><span class="sxs-lookup"><span data-stu-id="72f8f-136">If the SQL Server port is 1433, you do not need to specify it in the connection string.</span></span> <span data-ttu-id="72f8f-137">Następujący ciąg połączenia łączy się z maszyną wirtualną programu SQL z etykietą DNS `sqlvmlabel.eastus.cloudapp.azure.com` przy użyciu uwierzytelniania programu SQL (można także użyć publiczny adres IP).</span><span class="sxs-lookup"><span data-stu-id="72f8f-137">The following connection string connects to a SQL VM with a DNS label of `sqlvmlabel.eastus.cloudapp.azure.com` using SQL Authentication (you could also use the public IP address).</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

<span data-ttu-id="72f8f-138">Mimo że to umożliwia łączność klientów za pośrednictwem Internetu, nie oznacza każdy można połączyć z serwerem SQL.</span><span class="sxs-lookup"><span data-stu-id="72f8f-138">Although this enables connectivity for clients over the internet, this does not imply that anyone can connect to your SQL Server.</span></span> <span data-ttu-id="72f8f-139">Poza klienci muszą prawidłową nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="72f8f-139">Outside clients have to the correct username and password.</span></span> <span data-ttu-id="72f8f-140">Jednak aby dodatkowo zwiększyć bezpieczeństwo, można uniknąć dobrze znanego portu 1433.</span><span class="sxs-lookup"><span data-stu-id="72f8f-140">However, for additional security, you can avoid the well-known port 1433.</span></span> <span data-ttu-id="72f8f-141">Na przykład jeśli skonfigurowano program SQL Server do nasłuchiwania na port 1500 i ustalonych prawidłowego zapory i reguł grup zabezpieczeń sieci może połączyć przez dołączenie numer portu do nazwy serwera.</span><span class="sxs-lookup"><span data-stu-id="72f8f-141">For example, if you configured SQL Server to listen on port 1500 and established proper firewall and network security group rules, you could connect by appending the port number to the Server name.</span></span> <span data-ttu-id="72f8f-142">Poniższy przykład powoduje zmianę poprzedniego przez dodanie niestandardowy numer portu, **1500**, aby nazwa serwera:</span><span class="sxs-lookup"><span data-stu-id="72f8f-142">The following example alters the previous one by adding a custom port number, **1500**, to the server name:</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> <span data-ttu-id="72f8f-143">Określona w zapytaniu SQL Server na maszynie wirtualnej za pośrednictwem Internetu, wszystkich danych wychodzących z centrum danych Azure podlega normalny [ceny na transfer danych wychodzących](https://azure.microsoft.com/pricing/details/data-transfers/).</span><span class="sxs-lookup"><span data-stu-id="72f8f-143">When you query SQL Server in a VM over the internet, all outgoing data from the Azure datacenter is subject to normal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>

## <a name="connect-to-sql-server-within-a-virtual-network"></a><span data-ttu-id="72f8f-144">Połączenia z serwerem SQL w ramach sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="72f8f-144">Connect to SQL Server within a virtual network</span></span>

<span data-ttu-id="72f8f-145">Po wybraniu **prywatnej** dla **łączność z serwerem SQL** typu w portalu Azure konfiguruje większości takie same jak ustawienia **publicznego**.</span><span class="sxs-lookup"><span data-stu-id="72f8f-145">When you choose **Private** for the **SQL connectivity** type in the portal, Azure configures most of the settings identical to **Public**.</span></span> <span data-ttu-id="72f8f-146">Jeden różnica polega na tym, czy znajduje się żadna reguła grupy zabezpieczeń sieci zezwalająca na ruch poza na port serwera SQL (domyślnie 1433).</span><span class="sxs-lookup"><span data-stu-id="72f8f-146">The one difference is that there is no network security group rule to allow outside traffic on the SQL Server port (default 1433).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72f8f-147">Obrazy maszyny wirtualnej dla programu SQL Server Developer i wersji Express nie należy włączać automatycznie protokołu TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="72f8f-147">The virtual machine images for the SQL Server Developer and Express editions do not automatically enable the TCP/IP protocol.</span></span> <span data-ttu-id="72f8f-148">Dla deweloperów i ekspresowej wersji, należy użyć programu SQL Server Configuration Manager do [ręcznie Włącz protokół TCP/IP](#manualtcp) po utworzeniu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="72f8f-148">For Developer and Express editions, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#manualtcp) after creating the VM.</span></span>

<span data-ttu-id="72f8f-149">Prywatne łączności jest często używana w połączeniu z [sieci wirtualnej](../../../virtual-network/virtual-networks-overview.md), co pozwala kilka scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="72f8f-149">Private connectivity is often used in conjunction with [Virtual Network](../../../virtual-network/virtual-networks-overview.md), which enables several scenarios.</span></span> <span data-ttu-id="72f8f-150">Możesz połączyć maszyn wirtualnych w tej samej sieci wirtualnej, nawet jeżeli tych maszyn wirtualnych znajdują się w różnych grupach zasobów.</span><span class="sxs-lookup"><span data-stu-id="72f8f-150">You can connect VMs in the same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="72f8f-151">I [sieci VPN typu lokacja lokacja](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), możesz utworzyć to architektura hybrydowego łączy maszyn wirtualnych z lokalnymi sieciami i maszyn.</span><span class="sxs-lookup"><span data-stu-id="72f8f-151">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="72f8f-152">Sieci wirtualne umożliwiają także dołączyć do domeny maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="72f8f-152">Virtual networks also enable     you to join your Azure VMs to a domain.</span></span> <span data-ttu-id="72f8f-153">To jest jedynym sposobem, aby używać uwierzytelniania systemu Windows z programem SQL Server.</span><span class="sxs-lookup"><span data-stu-id="72f8f-153">This is the only way to use Windows Authentication to SQL Server.</span></span> <span data-ttu-id="72f8f-154">Inne scenariusze połączenia wymagają uwierzytelniania SQL z nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="72f8f-154">The other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="72f8f-155">Przy założeniu, że skonfigurowano DNS w sieci wirtualnej, należy połączyć z do wystąpienia programu SQL Server, określając nazwę komputera maszyny Wirtualnej programu SQL Server w parametrach połączenia.</span><span class="sxs-lookup"><span data-stu-id="72f8f-155">Assuming that you have configured DNS in your virtual network, you can connect to your SQL Server instance by specifying the SQL Server VM computer name in the connection string.</span></span> <span data-ttu-id="72f8f-156">W poniższym przykładzie założono również, czy też skonfigurowano uwierzytelnianie systemu Windows i czy użytkownik ma zostać przyznany dostęp do wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="72f8f-156">The following example also assumes that Windows Authentication has also been configured and that the user has been granted access to the SQL Server instance.</span></span>

```
Server=mysqlvm;Integrated Security=true
```

## <span data-ttu-id="72f8f-157"><a id="change"></a>Zmień ustawienia połączenia SQL</span><span class="sxs-lookup"><span data-stu-id="72f8f-157"><a id="change"></a> Change SQL connectivity settings</span></span>

<span data-ttu-id="72f8f-158">Możesz zmienić ustawienia połączenia dla maszyny wirtualnej programu SQL Server w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="72f8f-158">You can change the connectivity settings for your SQL Server virtual machine in the Azure portal.</span></span>

1. <span data-ttu-id="72f8f-159">W portalu Azure wybierz **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="72f8f-159">In the Azure portal, select **Virtual Machines**.</span></span>

2. <span data-ttu-id="72f8f-160">Wybierz program SQL Server maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="72f8f-160">Select your SQL Server VM.</span></span>

3. <span data-ttu-id="72f8f-161">W obszarze **ustawienia**, kliknij przycisk **konfigurację programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="72f8f-161">Under **Settings**, click **SQL Server configuration**.</span></span>

4. <span data-ttu-id="72f8f-162">Zmień **poziom Połączenie SQL** wymagane ustawienia.</span><span class="sxs-lookup"><span data-stu-id="72f8f-162">Change the **SQL connectivity level** to your required setting.</span></span> <span data-ttu-id="72f8f-163">Ten obszar służy Opcjonalnie można zmienić port programu SQL Server i jego ustawienia uwierzytelniania SQL.</span><span class="sxs-lookup"><span data-stu-id="72f8f-163">You can optionally use this area to change the SQL Server port or the SQL Authentication settings.</span></span>

   ![Zmień łączność z serwerem SQL](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. <span data-ttu-id="72f8f-165">Poczekaj kilka minut na ukończenie aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="72f8f-165">Wait several minutes for the update to complete.</span></span>

   ![Powiadomienie o aktualizacji maszyny Wirtualnej SQL](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <span data-ttu-id="72f8f-167"><a id="manualtcp"></a>Włącz protokół TCP/IP dla deweloperów i Express w wersji</span><span class="sxs-lookup"><span data-stu-id="72f8f-167"><a id="manualtcp"></a> Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="72f8f-168">Zmieniając ustawienia łączności serwera SQL Azure nie powoduje automatycznego włączenia protokołu TCP/IP dla programu SQL Server Developer i wersji Express.</span><span class="sxs-lookup"><span data-stu-id="72f8f-168">When changing SQL Server connectivity settings, Azure does not automatically enable the TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="72f8f-169">W poniższych krokach omówiono, jak ręcznie włączyć protokół TCP/IP w celu zdalnego nawiązania połączenia przy użyciu adresu IP.</span><span class="sxs-lookup"><span data-stu-id="72f8f-169">The steps below explain how to manually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="72f8f-170">Najpierw nawiąż połączenie z maszyną programu SQL Server przy użyciu pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="72f8f-170">First, connect to the SQL Server machine with remote desktop.</span></span>

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="72f8f-171">Następnie Włącz protokół TCP/IP z **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="72f8f-171">Next, enable the TCP/IP protocol with **SQL Server Configuration Manager**.</span></span>

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a><span data-ttu-id="72f8f-172">Nawiązywanie połączenia z programem SSMS</span><span class="sxs-lookup"><span data-stu-id="72f8f-172">Connect with SSMS</span></span>

<span data-ttu-id="72f8f-173">Poniższe kroki pokazują, jak utworzyć opcjonalną etykietę DNS dla sieci maszyny Wirtualnej platformy Azure, a następnie nawiąż połączenie z SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="72f8f-173">The following steps show how to create an optional DNS Label for your Azure VM and then connect with SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [Connect to SQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="72f8f-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="72f8f-174">Next Steps</span></span>

<span data-ttu-id="72f8f-175">Aby wyświetlić inicjowania obsługi administracyjnej instrukcje wraz z tych kroków łączności, zobacz [inicjowania obsługi maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="72f8f-175">To see provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="72f8f-176">Do innych tematów związanych z programem SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="72f8f-176">For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>