---
title: tooa aaaConnect programu SQL Server Virtual Machine (Resource Manager) | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooconnect tooSQL Server uruchomiony na maszynie wirtualnej na platformie Azure. W tym temacie używa hello klasycznego modelu wdrażania. scenariusze Hello różnią się w zależności od konfiguracji sieci hello i lokalizację hello powitania klienta."
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
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="6b9e5-105">Połącz tooa maszyny wirtualnej programu SQL Server na platformie Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="6b9e5-105">Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b9e5-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6b9e5-106">Resource Manager</span></span>](virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="6b9e5-107">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="6b9e5-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="6b9e5-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6b9e5-108">Overview</span></span>

<span data-ttu-id="6b9e5-109">W tym temacie opisano, jak wystąpienie tooyour tooconnect programu SQL Server uruchomiony na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-109">This topic describes how tooconnect tooyour SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="6b9e5-110">Obejmuje on niektóre [scenariusze ogólne łączności](#connection-scenarios) , a następnie oferuje [szczegółowe kroki związane z konfigurowaniem łączności z serwerem SQL w maszynie Wirtualnej platformy Azure](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="6b9e5-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="6b9e5-111">Jeśli trzeba będzie raczej pełny przewodnik inicjowania obsługi administracyjnej i łączność, zobacz [inicjowania obsługi maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="6b9e5-111">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="6b9e5-112">Scenariusze łączenia</span><span class="sxs-lookup"><span data-stu-id="6b9e5-112">Connection scenarios</span></span>

<span data-ttu-id="6b9e5-113">sposób powitania klienta łączy tooSQL, który serwer z uruchomioną na maszynie wirtualnej różni się w zależności od lokalizacji hello powitania klienta i konfiguracji sieci hello.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-113">hello way a client connects tooSQL Server running on a Virtual Machine differs depending on hello location of hello client and hello networking configuration.</span></span>

<span data-ttu-id="6b9e5-114">Jeśli dostarczasz maszyna wirtualna serwera SQL w hello portalu Azure, masz możliwość określenia typu hello hello **łączność z serwerem SQL**.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-114">If you provision a SQL Server VM in hello Azure portal, you have hello option of specifying hello type of **SQL connectivity**.</span></span>

![Publiczny opcji łączności SQL podczas inicjowania obsługi](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="6b9e5-116">Dostępne opcje dla połączenia:</span><span class="sxs-lookup"><span data-stu-id="6b9e5-116">Your options for connectivity include:</span></span>

| <span data-ttu-id="6b9e5-117">Opcja</span><span class="sxs-lookup"><span data-stu-id="6b9e5-117">Option</span></span> | <span data-ttu-id="6b9e5-118">Opis</span><span class="sxs-lookup"><span data-stu-id="6b9e5-118">Description</span></span> |
|---|---|
| <span data-ttu-id="6b9e5-119">**Publiczna**</span><span class="sxs-lookup"><span data-stu-id="6b9e5-119">**Public**</span></span> | <span data-ttu-id="6b9e5-120">Połącz tooSQL serwera na powitania internet</span><span class="sxs-lookup"><span data-stu-id="6b9e5-120">Connect tooSQL Server over hello internet</span></span> |
| <span data-ttu-id="6b9e5-121">**Prywatne**</span><span class="sxs-lookup"><span data-stu-id="6b9e5-121">**Private**</span></span> | <span data-ttu-id="6b9e5-122">Połącz tooSQL serwera w hello tej samej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6b9e5-122">Connect tooSQL Server in hello same virtual network</span></span> |
| <span data-ttu-id="6b9e5-123">**Lokalne**</span><span class="sxs-lookup"><span data-stu-id="6b9e5-123">**Local**</span></span> | <span data-ttu-id="6b9e5-124">Połącz tooSQL serwera lokalnie na powitania tej samej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6b9e5-124">Connect tooSQL Server locally on hello same virtual machine</span></span> | 

<span data-ttu-id="6b9e5-125">Witaj poniższe sekcje zawierają opis hello **publicznego** i **prywatnej** szczegółowo opcje.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-125">hello following sections explain hello **Public** and **Private** options in more detail.</span></span>

## <a name="connect-toosql-server-over-hello-internet"></a><span data-ttu-id="6b9e5-126">Połącz tooSQL serwera na powitania Internet</span><span class="sxs-lookup"><span data-stu-id="6b9e5-126">Connect tooSQL Server over hello Internet</span></span>

<span data-ttu-id="6b9e5-127">Aparat bazy danych programu SQL Server tooyour tooconnect z hello Internet, wybierz opcję **publicznego** dla hello **łączność z serwerem SQL** typu w portalu hello podczas inicjowania obsługi.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-127">If you want tooconnect tooyour SQL Server database engine from hello Internet, select **Public** for hello **SQL connectivity** type in hello portal during provisioning.</span></span> <span data-ttu-id="6b9e5-128">Hello portal automatycznie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6b9e5-128">hello portal automatically does hello following steps:</span></span>

* <span data-ttu-id="6b9e5-129">Włącza hello protokołu TCP/IP dla programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-129">Enables hello TCP/IP protocol for SQL Server.</span></span>
* <span data-ttu-id="6b9e5-130">Umożliwia skonfigurowanie zapory hello tooopen reguły port TCP programu SQL Server (domyślnie 1433).</span><span class="sxs-lookup"><span data-stu-id="6b9e5-130">Configures a firewall rule tooopen hello SQL Server TCP port (default 1433).</span></span>
* <span data-ttu-id="6b9e5-131">Umożliwia uwierzytelnianie programu SQL Server wymagane dla dostępu publicznego.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-131">Enables SQL Server Authentication, required for public access.</span></span>
* <span data-ttu-id="6b9e5-132">Konfiguruje hello sieciowej grupy zabezpieczeń na powitania ruch TCP tooall maszyn wirtualnych na powitania port programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-132">Configures hello network security group on hello VM tooall TCP traffic on hello SQL Server port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b9e5-133">Hello obrazy maszyny wirtualnej dla programu SQL Server Developer hello i wersji Express nie automatycznie włącza protokół hello TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-133">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="6b9e5-134">Dla deweloperów i ekspresowej wersji, należy użyć programu SQL Server Configuration Manager za[ręcznie włączyć protokół hello TCP/IP](#manualtcp) po utworzeniu hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-134">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="6b9e5-135">Dowolny klient z dostępem do Internetu mogą łączyć się z toohello wystąpienia programu SQL Server, określając hello publicznego adresu IP maszyny wirtualnej hello lub jakakolwiek Etykieta DNS przypisany adres IP toothat.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-135">Any client with internet access can connect toohello SQL Server instance by specifying either hello public IP address of hello virtual machine or any DNS label assigned toothat IP address.</span></span> <span data-ttu-id="6b9e5-136">Jeśli hello port programu SQL Server jest port 1433, nie ma potrzeby toospecify go w parametrach połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-136">If hello SQL Server port is 1433, you do not need toospecify it in hello connection string.</span></span> <span data-ttu-id="6b9e5-137">Witaj następujące parametry połączenia tooa maszyny Wirtualnej SQL łączy się z usługą etykietę DNS z `sqlvmlabel.eastus.cloudapp.azure.com` przy użyciu uwierzytelniania programu SQL (można także użyć hello publiczny adres IP).</span><span class="sxs-lookup"><span data-stu-id="6b9e5-137">hello following connection string connects tooa SQL VM with a DNS label of `sqlvmlabel.eastus.cloudapp.azure.com` using SQL Authentication (you could also use hello public IP address).</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

<span data-ttu-id="6b9e5-138">Mimo że to umożliwia łączność klientów za pośrednictwem Internetu Witaj, nie oznacza to, że każdy użytkownik może połączyć tooyour programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-138">Although this enables connectivity for clients over hello internet, this does not imply that anyone can connect tooyour SQL Server.</span></span> <span data-ttu-id="6b9e5-139">Poza klienci mają toohello prawidłową nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-139">Outside clients have toohello correct username and password.</span></span> <span data-ttu-id="6b9e5-140">Jednak aby dodatkowo zwiększyć bezpieczeństwo, można uniknąć hello dobrze znanego portu 1433.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-140">However, for additional security, you can avoid hello well-known port 1433.</span></span> <span data-ttu-id="6b9e5-141">Na przykład jeśli skonfigurowano toolisten programu SQL Server na porcie 1500 i ustalonych prawidłowego zapory i reguł grup zabezpieczeń sieci, można połączyć przez dodanie nazwy serwera toohello numer portu hello.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-141">For example, if you configured SQL Server toolisten on port 1500 and established proper firewall and network security group rules, you could connect by appending hello port number toohello Server name.</span></span> <span data-ttu-id="6b9e5-142">Witaj poniższy przykład powoduje zmianę hello poprzedniego przez dodanie niestandardowy numer portu, **1500**, toohello nazwa serwera:</span><span class="sxs-lookup"><span data-stu-id="6b9e5-142">hello following example alters hello previous one by adding a custom port number, **1500**, toohello server name:</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> <span data-ttu-id="6b9e5-143">Kwerendy SQL Server na maszynie wirtualnej za pośrednictwem Internetu, wszystkie dane wychodzące hello z hello Azure datacenter jest podmiotu toonormal [ceny na transfer danych wychodzących](https://azure.microsoft.com/pricing/details/data-transfers/).</span><span class="sxs-lookup"><span data-stu-id="6b9e5-143">When you query SQL Server in a VM over hello internet, all outgoing data from hello Azure datacenter is subject toonormal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>

## <a name="connect-toosql-server-within-a-virtual-network"></a><span data-ttu-id="6b9e5-144">Połącz tooSQL serwera w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6b9e5-144">Connect tooSQL Server within a virtual network</span></span>

<span data-ttu-id="6b9e5-145">Po wybraniu **prywatnej** dla hello **łączność z serwerem SQL** typu w portalu hello Azure konfiguruje większość ustawień hello identyczne zbyt**publicznego**.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-145">When you choose **Private** for hello **SQL connectivity** type in hello portal, Azure configures most of hello settings identical too**Public**.</span></span> <span data-ttu-id="6b9e5-146">Hello jeden różnica polega na tym, czy jest nie sieci zabezpieczeń grupy reguł tooallow poza ruchu na powitania port serwera SQL (domyślnie 1433).</span><span class="sxs-lookup"><span data-stu-id="6b9e5-146">hello one difference is that there is no network security group rule tooallow outside traffic on hello SQL Server port (default 1433).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b9e5-147">Hello obrazy maszyny wirtualnej dla programu SQL Server Developer hello i wersji Express nie automatycznie włącza protokół hello TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-147">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="6b9e5-148">Dla deweloperów i ekspresowej wersji, należy użyć programu SQL Server Configuration Manager za[ręcznie włączyć protokół hello TCP/IP](#manualtcp) po utworzeniu hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-148">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="6b9e5-149">Prywatne łączności jest często używana w połączeniu z [sieci wirtualnej](../../../virtual-network/virtual-networks-overview.md), co pozwala kilka scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-149">Private connectivity is often used in conjunction with [Virtual Network](../../../virtual-network/virtual-networks-overview.md), which enables several scenarios.</span></span> <span data-ttu-id="6b9e5-150">Możesz połączyć maszyny wirtualne w tej samej sieci wirtualnej, nawet jeśli te maszyny wirtualne istnieją w różnych grupach zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-150">You can connect VMs in hello same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="6b9e5-151">I [sieci VPN typu lokacja lokacja](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), możesz utworzyć to architektura hybrydowego łączy maszyn wirtualnych z lokalnymi sieciami i maszyn.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-151">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="6b9e5-152">Sieci wirtualne umożliwiają również toojoin można domenę tooa maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-152">Virtual networks also enable     you toojoin your Azure VMs tooa domain.</span></span> <span data-ttu-id="6b9e5-153">Jest to hello tylko sposób toouse uwierzytelniania systemu Windows tooSQL serwera.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-153">This is hello only way toouse Windows Authentication tooSQL Server.</span></span> <span data-ttu-id="6b9e5-154">Witaj inne połączenie scenariusze wymagają uwierzytelniania SQL z nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-154">hello other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="6b9e5-155">Przy założeniu, że skonfigurowano DNS w sieci wirtualnej, można połączyć, określając nazwę komputera maszyny Wirtualnej programu SQL Server hello w parametrach połączenia hello tooyour wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-155">Assuming that you have configured DNS in your virtual network, you can connect tooyour SQL Server instance by specifying hello SQL Server VM computer name in hello connection string.</span></span> <span data-ttu-id="6b9e5-156">Poniższy przykład również Hello założono, że również skonfigurowano uwierzytelnianie systemu Windows i użytkownika hello udzielono wystąpienia programu SQL Server toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-156">hello following example also assumes that Windows Authentication has also been configured and that hello user has been granted access toohello SQL Server instance.</span></span>

```
Server=mysqlvm;Integrated Security=true
```

## <span data-ttu-id="6b9e5-157"><a id="change"></a>Zmień ustawienia połączenia SQL</span><span class="sxs-lookup"><span data-stu-id="6b9e5-157"><a id="change"></a> Change SQL connectivity settings</span></span>

<span data-ttu-id="6b9e5-158">Ustawienia łączności hello można zmienić dla maszyny wirtualnej programu SQL Server w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-158">You can change hello connectivity settings for your SQL Server virtual machine in hello Azure portal.</span></span>

1. <span data-ttu-id="6b9e5-159">Hello portalu Azure, wybierz **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-159">In hello Azure portal, select **Virtual Machines**.</span></span>

2. <span data-ttu-id="6b9e5-160">Wybierz program SQL Server maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-160">Select your SQL Server VM.</span></span>

3. <span data-ttu-id="6b9e5-161">W obszarze **ustawienia**, kliknij przycisk **konfigurację programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-161">Under **Settings**, click **SQL Server configuration**.</span></span>

4. <span data-ttu-id="6b9e5-162">Zmień hello **poziom Połączenie SQL** tooyour wymagane ustawienia.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-162">Change hello **SQL connectivity level** tooyour required setting.</span></span> <span data-ttu-id="6b9e5-163">Można opcjonalnie użyć tego obszaru toochange hello port programu SQL Server lub hello ustawienia uwierzytelniania SQL.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-163">You can optionally use this area toochange hello SQL Server port or hello SQL Authentication settings.</span></span>

   ![Zmień łączność z serwerem SQL](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. <span data-ttu-id="6b9e5-165">Poczekaj kilka minut dla hello toocomplete aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-165">Wait several minutes for hello update toocomplete.</span></span>

   ![Powiadomienie o aktualizacji maszyny Wirtualnej SQL](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <span data-ttu-id="6b9e5-167"><a id="manualtcp"></a>Włącz protokół TCP/IP dla deweloperów i Express w wersji</span><span class="sxs-lookup"><span data-stu-id="6b9e5-167"><a id="manualtcp"></a> Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="6b9e5-168">Zmieniając ustawienia łączności serwera SQL Azure nie powoduje automatycznego włączenia protokołu hello TCP/IP dla programu SQL Server Developer i wersji Express.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-168">When changing SQL Server connectivity settings, Azure does not automatically enable hello TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="6b9e5-169">Witaj poniżej objaśniono sposób toomanually Włącz protokół TCP/IP, dzięki czemu można łączyć zdalnie za pomocą adresu IP.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-169">hello steps below explain how toomanually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="6b9e5-170">Najpierw połącz toohello komputera programu SQL Server przy użyciu pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-170">First, connect toohello SQL Server machine with remote desktop.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="6b9e5-171">Następnie Włącz protokół hello TCP/IP z **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="6b9e5-171">Next, enable hello TCP/IP protocol with **SQL Server Configuration Manager**.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a><span data-ttu-id="6b9e5-172">Nawiązywanie połączenia z programem SSMS</span><span class="sxs-lookup"><span data-stu-id="6b9e5-172">Connect with SSMS</span></span>

<span data-ttu-id="6b9e5-173">Witaj poniższe kroki Pokaż jak toocreate opcjonalne DNS etykietę dla maszyny Wirtualnej platformy Azure i następnie nawiąż połączenie z SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="6b9e5-173">hello following steps show how toocreate an optional DNS Label for your Azure VM and then connect with SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="6b9e5-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6b9e5-174">Next Steps</span></span>

<span data-ttu-id="6b9e5-175">Zobacz instrukcje inicjowania obsługi administracyjnej toosee wraz z tych kroków łączności, [inicjowania obsługi maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="6b9e5-175">toosee provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="6b9e5-176">Dla innych tematach dotyczących toorunning programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b9e5-176">For other topics related toorunning SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
