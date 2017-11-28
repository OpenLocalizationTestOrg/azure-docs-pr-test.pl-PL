---
title: "aaaSQL grup dostępności serwera — maszyny wirtualne Azure — samouczek | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak toocreate programu SQL Server zawsze w grupie dostępności na maszynach wirtualnych platformy Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="47e07-103">Konfigurowanie zawsze włączonej grupy dostępności w maszynie Wirtualnej platformy Azure ręcznie</span><span class="sxs-lookup"><span data-stu-id="47e07-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="47e07-104">Ten samouczek pokazuje, jak toocreate programu SQL Server zawsze w grupie dostępności na maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="47e07-104">This tutorial shows how toocreate a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="47e07-105">Samouczek pełną Hello tworzy grupy dostępności z repliki bazy danych na dwóch serwerach SQL.</span><span class="sxs-lookup"><span data-stu-id="47e07-105">hello complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="47e07-106">**Szacowanie czasu**: trwa około 30 minut toocomplete po hello wymagania wstępne są spełnione.</span><span class="sxs-lookup"><span data-stu-id="47e07-106">**Time estimate**: Takes about 30 minutes toocomplete once hello prerequisites are met.</span></span>

<span data-ttu-id="47e07-107">Witaj diagramie kompilacji w samouczku hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-107">hello diagram illustrates what you build in hello tutorial.</span></span>

![Grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="47e07-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="47e07-109">Prerequisites</span></span>

<span data-ttu-id="47e07-110">Hello samouczka przyjęto założenie, że masz podstawową wiedzę na temat programu SQL Server zawsze włączonych grup dostępności.</span><span class="sxs-lookup"><span data-stu-id="47e07-110">hello tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="47e07-111">Aby uzyskać więcej informacji, zobacz [Omówienie programu zawsze włączonych grup dostępności (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span><span class="sxs-lookup"><span data-stu-id="47e07-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="47e07-112">Witaj poniższej tabeli wymieniono wymagania wstępne hello muszą toocomplete przed rozpoczęciem tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="47e07-112">hello following table lists hello prerequisites that you need toocomplete before starting this tutorial:</span></span>

|  |<span data-ttu-id="47e07-113">Wymaganie</span><span class="sxs-lookup"><span data-stu-id="47e07-113">Requirement</span></span> |<span data-ttu-id="47e07-114">Opis</span><span class="sxs-lookup"><span data-stu-id="47e07-114">Description</span></span> |
|----- |----- |----- |
|![kwadratowe](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="47e07-116">Dwa serwery SQL</span><span class="sxs-lookup"><span data-stu-id="47e07-116">Two SQL Servers</span></span> | <span data-ttu-id="47e07-117">— W zestawie dostępności Azure</span><span class="sxs-lookup"><span data-stu-id="47e07-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="47e07-118">— W jednej domenie</span><span class="sxs-lookup"><span data-stu-id="47e07-118">- In a single domain</span></span> <br/> <span data-ttu-id="47e07-119">-Z zainstalowaną funkcją klastra trybu Failover</span><span class="sxs-lookup"><span data-stu-id="47e07-119">- With Failover Clustering feature installed</span></span> |
|![kwadratowe](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="47e07-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="47e07-121">Windows Server</span></span> | <span data-ttu-id="47e07-122">Udział plików dla monitora klastra</span><span class="sxs-lookup"><span data-stu-id="47e07-122">File share for cluster witness</span></span> |  
|![kwadratowe](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="47e07-124">Konto usługi programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="47e07-124">SQL Server service account</span></span> | <span data-ttu-id="47e07-125">Konto domeny</span><span class="sxs-lookup"><span data-stu-id="47e07-125">Domain account</span></span> |
|![kwadratowe](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="47e07-127">Konto usługi programu SQL Server Agent</span><span class="sxs-lookup"><span data-stu-id="47e07-127">SQL Server Agent service account</span></span> | <span data-ttu-id="47e07-128">Konto domeny</span><span class="sxs-lookup"><span data-stu-id="47e07-128">Domain account</span></span> |  
|![kwadratowe](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="47e07-130">Otwórz porty zapory</span><span class="sxs-lookup"><span data-stu-id="47e07-130">Firewall ports open</span></span> | <span data-ttu-id="47e07-131">— Program SQL Server: **1433** dla domyślnego wystąpienia</span><span class="sxs-lookup"><span data-stu-id="47e07-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="47e07-132">-Dublowania bazy danych punktu końcowego: **5022** lub dowolny dostępny port</span><span class="sxs-lookup"><span data-stu-id="47e07-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="47e07-133">-Sondę modułu równoważenia obciążenia azure: **59999** lub dowolny dostępny port</span><span class="sxs-lookup"><span data-stu-id="47e07-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![kwadratowe](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="47e07-135">Dodawanie obsługi klastrów pracy awaryjnej</span><span class="sxs-lookup"><span data-stu-id="47e07-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="47e07-136">Oba serwery SQL wymagają tej funkcji</span><span class="sxs-lookup"><span data-stu-id="47e07-136">Both SQL Servers require this feature</span></span> |
|![kwadratowe](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="47e07-138">Konto domeny instalacji</span><span class="sxs-lookup"><span data-stu-id="47e07-138">Installation domain account</span></span> | <span data-ttu-id="47e07-139">-Lokalnego administratora na każdym serwerze SQL</span><span class="sxs-lookup"><span data-stu-id="47e07-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="47e07-140">-Członek roli serwera sysadmin programu SQL Server dla każdego wystąpienia programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="47e07-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="47e07-141">Przed rozpoczęciem powitalne samouczka należy zbyt[ukończyć wymagania wstępne dotyczące tworzenia zawsze włączonych grup dostępności w maszynach wirtualnych platformy Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="47e07-141">Before you begin hello tutorial, you need too[Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="47e07-142">Jeśli te wymagania wstępne są już wypełnione, można przejść za[tworzenia klastrów](#CreateCluster).</span><span class="sxs-lookup"><span data-stu-id="47e07-142">If these prerequisites are completed already, you can jump too[Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="47e07-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Tworzenie klastra hello</span><span class="sxs-lookup"><span data-stu-id="47e07-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create hello cluster</span></span>

<span data-ttu-id="47e07-144">Po hello wymagania wstępne są zakończone, hello pierwszym krokiem jest toocreate klastra trybu Failover serwera systemu Windows, która zawiera dwa serwery SQL i serwer monitora.</span><span class="sxs-lookup"><span data-stu-id="47e07-144">After hello prerequisites are completed, hello first step is toocreate a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="47e07-145">RDP toohello pierwszego programu SQL Server przy użyciu konta domeny, które jest kontem administratora na serwerach SQL i powitania serwera monitora.</span><span class="sxs-lookup"><span data-stu-id="47e07-145">RDP toohello first SQL Server using a domain account that is an administrator on both SQL Servers and hello witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="47e07-146">Po wykonaniu hello [dokumentu z wymaganiami wstępnymi](virtual-machines-windows-portal-sql-availability-group-prereq.md), zostało utworzone konto o nazwie **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="47e07-146">If you followed hello [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="47e07-147">Użyj tego konta.</span><span class="sxs-lookup"><span data-stu-id="47e07-147">Use this account.</span></span>

2. <span data-ttu-id="47e07-148">W hello **Menedżera serwera** pulpitu nawigacyjnego, wybierz opcję **narzędzia**, a następnie kliknij przycisk **Menedżera klastra trybu Failover**.</span><span class="sxs-lookup"><span data-stu-id="47e07-148">In hello **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="47e07-149">W okienku po lewej stronie powitania kliknij prawym przyciskiem myszy **Menedżera klastra trybu Failover**, a następnie kliknij przycisk **utworzyć klaster**.</span><span class="sxs-lookup"><span data-stu-id="47e07-149">In hello left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="47e07-150">![Tworzenie klastra](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="47e07-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="47e07-151">W hello Kreatora tworzenia klastra, tworzenie klastra z jednym węzłem przez krokowe hello stron z ustawieniami hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="47e07-151">In hello Create Cluster Wizard, create a one-node cluster by stepping through hello pages with hello settings in hello following table:</span></span>

   | <span data-ttu-id="47e07-152">Strona</span><span class="sxs-lookup"><span data-stu-id="47e07-152">Page</span></span> | <span data-ttu-id="47e07-153">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="47e07-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="47e07-154">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="47e07-154">Before You Begin</span></span> |<span data-ttu-id="47e07-155">Użyj wartości domyślnych</span><span class="sxs-lookup"><span data-stu-id="47e07-155">Use defaults</span></span> |
   | <span data-ttu-id="47e07-156">Wybierz serwery</span><span class="sxs-lookup"><span data-stu-id="47e07-156">Select Servers</span></span> |<span data-ttu-id="47e07-157">Witaj typu Nazwa pierwszego serwera SQL w **wprowadź nazwę serwera** i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="47e07-157">Type hello first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="47e07-158">Ostrzeżenie dotyczące sprawdzania poprawności</span><span class="sxs-lookup"><span data-stu-id="47e07-158">Validation Warning</span></span> |<span data-ttu-id="47e07-159">Wybierz **testów nr nie jest wymagana obsługa firmy Microsoft dla tego klastra, a w związku z tym nie ma toorun hello weryfikacji. Po kliknięciu przycisku dalej kontynuować tworzenie klastra hello**.</span><span class="sxs-lookup"><span data-stu-id="47e07-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want toorun hello validation tests. When I click Next, continue Creating hello cluster**.</span></span> |
   | <span data-ttu-id="47e07-160">Punkt dostępu do hello administrowanie klastra</span><span class="sxs-lookup"><span data-stu-id="47e07-160">Access Point for Administering hello Cluster</span></span> |<span data-ttu-id="47e07-161">Wpisz nazwę klastra, na przykład **SQLAGCluster1** w **nazwy klastra**.</span><span class="sxs-lookup"><span data-stu-id="47e07-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="47e07-162">Potwierdzenie</span><span class="sxs-lookup"><span data-stu-id="47e07-162">Confirmation</span></span> |<span data-ttu-id="47e07-163">Użyj wartości domyślnych, chyba że w przypadku korzystania z funkcji miejsca do magazynowania.</span><span class="sxs-lookup"><span data-stu-id="47e07-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="47e07-164">Patrz Uwaga hello poniżej tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="47e07-164">See hello note following this table.</span></span> |

### <a name="set-hello-cluster-ip-address"></a><span data-ttu-id="47e07-165">Ustaw adres IP klastra hello</span><span class="sxs-lookup"><span data-stu-id="47e07-165">Set hello cluster IP address</span></span>

1. <span data-ttu-id="47e07-166">W **Menedżera klastra trybu Failover**, przewiń w dół za**zasoby podstawowe klastra** i rozwiń hello szczegółów klastra.</span><span class="sxs-lookup"><span data-stu-id="47e07-166">In **Failover Cluster Manager**, scroll down too**Cluster Core Resources** and expand hello cluster details.</span></span> <span data-ttu-id="47e07-167">Powinny być widoczne oba hello **nazwa** i hello **adres IP** zasobów w hello **** stanu.</span><span class="sxs-lookup"><span data-stu-id="47e07-167">You should see both hello **Name** and hello **IP Address** resources in hello **Failed** state.</span></span> <span data-ttu-id="47e07-168">Hello zasobu adresu IP nie może być przełączony w tryb online ponieważ klastra hello przypisano hello sam adres IP jako samej maszyny hello, dlatego jest zduplikowany adres.</span><span class="sxs-lookup"><span data-stu-id="47e07-168">hello IP address resource cannot be brought online because hello cluster is assigned hello same IP address as hello machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="47e07-169">Kliknij prawym przyciskiem myszy hello nie powiodło się **adres IP** zasobów, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="47e07-169">Right-click hello failed **IP Address** resource, and then click **Properties**.</span></span>

   ![Właściwości klastra](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="47e07-171">Wybierz **statyczny adres IP** i określ adres podsieci hello programu SQL Server w przypadku w polu tekstowym adres hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-171">Select **Static IP Address** and specify an available address from subnet where hello SQL Server is in hello Address text box.</span></span> <span data-ttu-id="47e07-172">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="47e07-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="47e07-173">W hello **zasoby podstawowe klastra** sekcji, kliknij prawym przyciskiem myszy nazwę klastra i kliknij przycisk **przejdź do trybu Online**.</span><span class="sxs-lookup"><span data-stu-id="47e07-173">In hello **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="47e07-174">Następnie zaczekaj, aż oba zasoby są w trybie online.</span><span class="sxs-lookup"><span data-stu-id="47e07-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="47e07-175">Gdy zasób Nazwa hello klastra do trybu online, aktualizuje powitania serwera kontrolera domeny przy użyciu nowego konta komputera usługi AD.</span><span class="sxs-lookup"><span data-stu-id="47e07-175">When hello cluster name resource comes online, it updates hello DC server with a new AD computer account.</span></span> <span data-ttu-id="47e07-176">Użyj tego AD hello toorun konta grupy dostępności w klastrze usługi później.</span><span class="sxs-lookup"><span data-stu-id="47e07-176">Use this AD account toorun hello Availability Group clustered service later.</span></span>

### <span data-ttu-id="47e07-177"><a name="addNode"></a>Dodaj hello innych toocluster programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="47e07-177"><a name="addNode"></a>Add hello other SQL Server toocluster</span></span>

<span data-ttu-id="47e07-178">Dodaj hello innych klastra toohello programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="47e07-178">Add hello other SQL Server toohello cluster.</span></span>

1. <span data-ttu-id="47e07-179">W drzewie przeglądarki hello, kliknij prawym przyciskiem myszy hello klastra, a następnie kliknij przycisk **Dodaj węzeł**.</span><span class="sxs-lookup"><span data-stu-id="47e07-179">In hello browser tree, right-click hello cluster and click **Add Node**.</span></span>

    ![Dodaj toohello węzła klastra](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="47e07-181">W hello **Kreatora dodawania węzłów**, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-181">In hello **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="47e07-182">W hello **Wybieranie serwerów** Dodaj hello drugiego serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="47e07-182">In hello **Select Servers** page, add hello second SQL Server.</span></span> <span data-ttu-id="47e07-183">Wpisz nazwę serwera hello w **wprowadź nazwę serwera** , a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="47e07-183">Type hello server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="47e07-184">Gdy wszystko będzie gotowe, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="47e07-185">W hello **ostrzeżenie dotyczące sprawdzania poprawności** kliknij przycisk **nr** (w środowisku produkcyjnym należy przeprowadzić testy weryfikacyjne hello).</span><span class="sxs-lookup"><span data-stu-id="47e07-185">In hello **Validation Warning** page, click **No** (in a production scenario you should perform hello validation tests).</span></span> <span data-ttu-id="47e07-186">Następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="47e07-187">W hello **potwierdzenie** strony, jeśli używasz funkcji miejsca do magazynowania, hello Usuń zaznaczenie pola wyboru z etykietą **Dodaj wszystkie odpowiednie magazyny toohello klastra.**</span><span class="sxs-lookup"><span data-stu-id="47e07-187">In hello **Confirmation** page if you are using Storage Spaces, clear hello checkbox labeled **Add all eligible storage toohello cluster.**</span></span>

   ![Dodaj potwierdzenie węzła](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="47e07-189">Jeśli używasz funkcji miejsca do magazynowania i nie Usuń zaznaczenie pola wyboru **Dodaj wszystkie odpowiednie magazyny toohello klaster**, Windows odłącza dyski wirtualne hello podczas hello klastrowanie procesu.</span><span class="sxs-lookup"><span data-stu-id="47e07-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage toohello cluster**, Windows detaches hello virtual disks during hello clustering process.</span></span> <span data-ttu-id="47e07-190">W związku z tym są wyświetlane w Menedżerze dysków lub w Eksploratorze dopiero hello miejsca do magazynowania są usuwane z hello klastra i ponownie nałożona przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47e07-190">As a result, they do not appear in Disk Manager or Explorer until hello storage spaces are removed from hello cluster and reattached using PowerShell.</span></span> <span data-ttu-id="47e07-191">Funkcja miejsca do magazynowania grupuje wiele dysków w pule toostorage.</span><span class="sxs-lookup"><span data-stu-id="47e07-191">Storage Spaces groups multiple disks in toostorage pools.</span></span> <span data-ttu-id="47e07-192">Aby uzyskać więcej informacji, zobacz [miejsca do magazynowania](https://technet.microsoft.com/library/hh831739).</span><span class="sxs-lookup"><span data-stu-id="47e07-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="47e07-193">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-193">Click **Next**.</span></span>

1. <span data-ttu-id="47e07-194">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="47e07-194">Click **Finish**.</span></span>

   <span data-ttu-id="47e07-195">Menedżer klastra trybu failover pokazuje, czy klaster ma nowy węzeł i wyświetla go w hello **węzłów** kontenera.</span><span class="sxs-lookup"><span data-stu-id="47e07-195">Failover Cluster Manager shows that your cluster has a new node and lists it in hello **Nodes** container.</span></span>

10. <span data-ttu-id="47e07-196">Wyloguj się z hello sesji usług pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="47e07-196">Log out of hello remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="47e07-197">Dodaj udział plików kworum klastra</span><span class="sxs-lookup"><span data-stu-id="47e07-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="47e07-198">W tym przykładzie klastra systemu Windows hello używa toocreate udziału pliku kworum klastra.</span><span class="sxs-lookup"><span data-stu-id="47e07-198">In this example hello Windows cluster uses a file share toocreate a cluster quorum.</span></span> <span data-ttu-id="47e07-199">W tym samouczku używana kworum Większość węzłów i plików udziału.</span><span class="sxs-lookup"><span data-stu-id="47e07-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="47e07-200">Aby uzyskać więcej informacji, zobacz [opis konfiguracji kworum w klastrze pracy awaryjnej](http://technet.microsoft.com/library/cc731739.aspx).</span><span class="sxs-lookup"><span data-stu-id="47e07-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="47e07-201">Serwer członkowski monitora udziału plików toohello Uzyskuj dostęp do sesji pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="47e07-201">Connect toohello file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="47e07-202">Na **Menedżera serwera**, kliknij przycisk **narzędzia**.</span><span class="sxs-lookup"><span data-stu-id="47e07-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="47e07-203">Otwórz **Zarządzanie komputerem**.</span><span class="sxs-lookup"><span data-stu-id="47e07-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="47e07-204">Kliknij przycisk **foldery udostępnione**.</span><span class="sxs-lookup"><span data-stu-id="47e07-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="47e07-205">Kliknij prawym przyciskiem myszy **udziałów**i kliknij przycisk **nowy udział...** .</span><span class="sxs-lookup"><span data-stu-id="47e07-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Nowy udział](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="47e07-207">Użyj **udostępnionych Kreator tworzenia folderu** toocreate udziału.</span><span class="sxs-lookup"><span data-stu-id="47e07-207">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="47e07-208">Na **ścieżka folderu**, kliknij przycisk **Przeglądaj** oraz znajdowanie lub utworzyć ścieżkę do folderu udostępnionego hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-208">On **Folder Path**, click **Browse** and locate or create a path for hello shared folder.</span></span> <span data-ttu-id="47e07-209">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-209">Click **Next**.</span></span>

1. <span data-ttu-id="47e07-210">W **nazwę, opis i ustawienia** Sprawdź hello nazwy udziału i ścieżki.</span><span class="sxs-lookup"><span data-stu-id="47e07-210">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="47e07-211">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-211">Click **Next**.</span></span>

1. <span data-ttu-id="47e07-212">Na **uprawnienia folderu udostępnionego** ustawić **Dostosuj uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="47e07-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="47e07-213">Kliknij przycisk **niestandardowy...** .</span><span class="sxs-lookup"><span data-stu-id="47e07-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="47e07-214">Na **dostosowywanie uprawnień**, kliknij przycisk **Dodaj...** .</span><span class="sxs-lookup"><span data-stu-id="47e07-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="47e07-215">Upewnij się, hello konto używane toocreate hello klastra ma pełną kontrolę.</span><span class="sxs-lookup"><span data-stu-id="47e07-215">Make sure that hello account used toocreate hello cluster has full control.</span></span>

   ![Nowy udział](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="47e07-217">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="47e07-217">Click **OK**.</span></span>

1. <span data-ttu-id="47e07-218">W **uprawnienia folderu udostępnionego**, kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="47e07-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="47e07-219">Kliknij przycisk **Zakończ** ponownie.</span><span class="sxs-lookup"><span data-stu-id="47e07-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="47e07-220">Wyloguj się z powitania serwera</span><span class="sxs-lookup"><span data-stu-id="47e07-220">Log out of hello server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="47e07-221">Konfigurowanie kworum klastra</span><span class="sxs-lookup"><span data-stu-id="47e07-221">Configure cluster quorum</span></span>

<span data-ttu-id="47e07-222">Następnie należy ustawić hello kworum klastra.</span><span class="sxs-lookup"><span data-stu-id="47e07-222">Next, set hello cluster quorum.</span></span>

1. <span data-ttu-id="47e07-223">Połącz toohello na pierwszym węźle klastra przy użyciu pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="47e07-223">Connect toohello first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="47e07-224">W **Menedżera klastra trybu Failover**, kliknij prawym przyciskiem myszy klaster hello, wskaż zbyt**więcej akcji**i kliknij przycisk **Konfiguruj ustawienia kworum klastra...** .</span><span class="sxs-lookup"><span data-stu-id="47e07-224">In **Failover Cluster Manager**, right-click hello cluster, point too**More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![Nowy udział](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="47e07-226">W **Kreatora konfiguracji kworum klastra**, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="47e07-227">W **Wybieranie opcji konfiguracji kworum**, wybierz **Wybieranie monitora kworum hello**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-227">In **Select Quorum Configuration Option**, choose **Select hello quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="47e07-228">Na **Wybieranie monitora kworum**, kliknij przycisk **Konfigurowanie monitora udziału plików**.</span><span class="sxs-lookup"><span data-stu-id="47e07-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="47e07-229">Windows Server 2016 obsługuje monitora chmury.</span><span class="sxs-lookup"><span data-stu-id="47e07-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="47e07-230">Jeśli wybierzesz tego typu monitora nie ma potrzeby pliku monitor udostępniania.</span><span class="sxs-lookup"><span data-stu-id="47e07-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="47e07-231">Aby uzyskać więcej informacji, zobacz [wdrażania chmury monitora dla klastra trybu Failover](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="47e07-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="47e07-232">Ten samouczek używa monitora udziału plików, który jest obsługiwany przez wcześniejsze systemy operacyjne.</span><span class="sxs-lookup"><span data-stu-id="47e07-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="47e07-233">Na **Konfigurowanie monitora udostępniania plików**, wpisz ścieżkę hello udziału hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="47e07-233">On **Configure File Share Witness**, type hello path for hello share you created.</span></span> <span data-ttu-id="47e07-234">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-234">Click **Next**.</span></span>

1. <span data-ttu-id="47e07-235">Sprawdź ustawienia hello na **potwierdzenie**.</span><span class="sxs-lookup"><span data-stu-id="47e07-235">Verify hello settings on **Confirmation**.</span></span> <span data-ttu-id="47e07-236">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-236">Click **Next**.</span></span>

1. <span data-ttu-id="47e07-237">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="47e07-237">Click **Finish**.</span></span>

<span data-ttu-id="47e07-238">Zasoby podstawowe klastra Hello są skonfigurowane z monitora udziału plików.</span><span class="sxs-lookup"><span data-stu-id="47e07-238">hello cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="47e07-239">Włącz grupy dostępności</span><span class="sxs-lookup"><span data-stu-id="47e07-239">Enable Availability Groups</span></span>

<span data-ttu-id="47e07-240">Następnie włącz opcję hello **zawsze włączonych grup dostępności** funkcji.</span><span class="sxs-lookup"><span data-stu-id="47e07-240">Next, enable hello **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="47e07-241">Wykonaj te kroki na obu serwerach SQL.</span><span class="sxs-lookup"><span data-stu-id="47e07-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="47e07-242">Z hello **Start** ekranu, uruchom **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="47e07-242">From hello **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="47e07-243">W drzewie przeglądarki powitania kliknij **usług SQL Server**, kliknij prawym przyciskiem myszy hello **programu SQL Server (MSSQLSERVER)** usługi, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="47e07-243">In hello browser tree, click **SQL Server Services**, then right-click hello **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="47e07-244">Kliknij przycisk hello **wysokiej dostępności funkcji AlwaysOn** , a następnie wybierz **Włącz zawsze włączone grupy dostępności**w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="47e07-244">Click hello **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![Włącz zawsze włączone grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="47e07-246">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="47e07-246">Click **Apply**.</span></span> <span data-ttu-id="47e07-247">Kliknij przycisk **OK** w wyskakującym oknie dialogowym hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-247">Click **OK** in hello pop-up dialog.</span></span>

5. <span data-ttu-id="47e07-248">Uruchom ponownie usługę SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-248">Restart hello SQL Server service.</span></span>

<span data-ttu-id="47e07-249">Powtórz te czynności na powitania innego serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="47e07-249">Repeat these steps on hello other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a><span data-ttu-id="47e07-250">Utwórz bazę danych na powitania pierwszego serwera SQL</span><span class="sxs-lookup"><span data-stu-id="47e07-250">Create a database on hello first SQL Server</span></span>

1. <span data-ttu-id="47e07-251">Uruchamiania hello RDP pliku toohello pierwszego programu SQL Server z domeny konta będący członkiem roli sysadmin stałej roli serwera.</span><span class="sxs-lookup"><span data-stu-id="47e07-251">Launch hello RDP file toohello first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="47e07-252">Otwórz program SQL Server Management Studio i połącz toohello pierwszego serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="47e07-252">Open SQL Server Management Studio and connect toohello first SQL Server.</span></span>
7. <span data-ttu-id="47e07-253">W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy **baz danych** i kliknij przycisk **nową bazę danych**.</span><span class="sxs-lookup"><span data-stu-id="47e07-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="47e07-254">W **Nazwa bazy danych**, typ **MyDB1**, następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="47e07-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="47e07-255"><a name="backupshare"></a>Tworzenie kopii zapasowej udziału</span><span class="sxs-lookup"><span data-stu-id="47e07-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="47e07-256">Na hello pierwszego serwera SQL w **Menedżera serwera**, kliknij przycisk **narzędzia**.</span><span class="sxs-lookup"><span data-stu-id="47e07-256">On hello first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="47e07-257">Otwórz **Zarządzanie komputerem**.</span><span class="sxs-lookup"><span data-stu-id="47e07-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="47e07-258">Kliknij przycisk **foldery udostępnione**.</span><span class="sxs-lookup"><span data-stu-id="47e07-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="47e07-259">Kliknij prawym przyciskiem myszy **udziałów**i kliknij przycisk **nowy udział...** .</span><span class="sxs-lookup"><span data-stu-id="47e07-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Nowy udział](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="47e07-261">Użyj **udostępnionych Kreator tworzenia folderu** toocreate udziału.</span><span class="sxs-lookup"><span data-stu-id="47e07-261">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="47e07-262">Na **ścieżka folderu**, kliknij przycisk **Przeglądaj** oraz znajdowanie lub utworzyć ścieżki dla kopii zapasowej folderu udostępnionego hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="47e07-262">On **Folder Path**, click **Browse** and locate or create a path for hello database backup shared folder.</span></span> <span data-ttu-id="47e07-263">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-263">Click **Next**.</span></span>

1. <span data-ttu-id="47e07-264">W **nazwę, opis i ustawienia** Sprawdź hello nazwy udziału i ścieżki.</span><span class="sxs-lookup"><span data-stu-id="47e07-264">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="47e07-265">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-265">Click **Next**.</span></span>

1. <span data-ttu-id="47e07-266">Na **uprawnienia folderu udostępnionego** ustawić **Dostosuj uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="47e07-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="47e07-267">Kliknij przycisk **niestandardowy...** .</span><span class="sxs-lookup"><span data-stu-id="47e07-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="47e07-268">Na **dostosowywanie uprawnień**, kliknij przycisk **Dodaj...** .</span><span class="sxs-lookup"><span data-stu-id="47e07-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="47e07-269">Upewnij się, że hello konta usługi programu SQL Server i Agent serwera SQL dla obu serwerów mają pełną kontrolę.</span><span class="sxs-lookup"><span data-stu-id="47e07-269">Make sure that hello SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![Nowy udział](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="47e07-271">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="47e07-271">Click **OK**.</span></span>

1. <span data-ttu-id="47e07-272">W **uprawnienia folderu udostępnionego**, kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="47e07-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="47e07-273">Kliknij przycisk **Zakończ** ponownie.</span><span class="sxs-lookup"><span data-stu-id="47e07-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-hello-database"></a><span data-ttu-id="47e07-274">Utworzenia pełnej kopii zapasowej hello bazy danych</span><span class="sxs-lookup"><span data-stu-id="47e07-274">Take a full backup of hello database</span></span>

<span data-ttu-id="47e07-275">Należy tooback się hello nowej bazy danych tooinitialize hello łańcuch dziennika.</span><span class="sxs-lookup"><span data-stu-id="47e07-275">You need tooback up hello new database tooinitialize hello log chain.</span></span> <span data-ttu-id="47e07-276">Jeśli nie wykonuje kopię zapasową hello nową bazę danych, nie można uwzględnić w grupie dostępności.</span><span class="sxs-lookup"><span data-stu-id="47e07-276">If you do not take a backup of hello new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="47e07-277">W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy hello bazy danych, wskaż zbyt**zadań...** , kliknij przycisk **kopię zapasową**.</span><span class="sxs-lookup"><span data-stu-id="47e07-277">In **Object Explorer**, right-click hello database, point too**Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="47e07-278">Kliknij przycisk **OK** tootake pełnej kopii zapasowej toohello domyślnej lokalizacji kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="47e07-278">Click **OK** tootake a full backup toohello default backup location.</span></span>

## <a name="create-hello-availability-group"></a><span data-ttu-id="47e07-279">Utwórz hello grupy dostępności</span><span class="sxs-lookup"><span data-stu-id="47e07-279">Create hello Availability Group</span></span>
<span data-ttu-id="47e07-280">Wszystko jest teraz gotowy tooconfigure, które grupy dostępności przy użyciu hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="47e07-280">You are now ready tooconfigure an Availability Group using hello following steps:</span></span>

* <span data-ttu-id="47e07-281">Utwórz bazę danych na powitania pierwszego serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="47e07-281">Create a database on hello first SQL Server.</span></span>
* <span data-ttu-id="47e07-282">Przełączyć pełnej kopii zapasowej i kopii zapasowej dziennika transakcji bazy danych hello</span><span class="sxs-lookup"><span data-stu-id="47e07-282">Take both a full backup and a transaction log backup of hello database</span></span>
* <span data-ttu-id="47e07-283">Pełna hello przywracania i drugie programu SQL Server z hello toohello kopii zapasowych dziennika **NORECOVERY** opcji</span><span class="sxs-lookup"><span data-stu-id="47e07-283">Restore hello full and log backups toohello second SQL Server with hello **NORECOVERY** option</span></span>
* <span data-ttu-id="47e07-284">Utwórz hello grupy dostępności (**AG1**) z zatwierdzanie synchroniczne, automatycznej pracy awaryjnej i do odczytu replikach pomocniczych</span><span class="sxs-lookup"><span data-stu-id="47e07-284">Create hello Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-hello-availability-group"></a><span data-ttu-id="47e07-285">Utwórz hello grupy dostępności:</span><span class="sxs-lookup"><span data-stu-id="47e07-285">Create hello Availability Group:</span></span>

1. <span data-ttu-id="47e07-286">W sesji pulpitu zdalnego toohello pierwszego serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="47e07-286">On remote desktop session toohello first SQL Server.</span></span> <span data-ttu-id="47e07-287">W **Eksplorator obiektów** w programie SSMS, kliknij prawym przyciskiem myszy **wysokiej dostępności funkcji AlwaysOn** i kliknij przycisk **Kreatora nowej grupy dostępności**.</span><span class="sxs-lookup"><span data-stu-id="47e07-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![Uruchom Kreatora nowej grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="47e07-289">W hello **wprowadzenie** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-289">In hello **Introduction** page, click **Next**.</span></span> <span data-ttu-id="47e07-290">W hello **Określ nazwę grupy dostępności** strony, na przykład wpisz nazwę grupy dostępności hello **AG1**w **Nazwa grupy dostępności**.</span><span class="sxs-lookup"><span data-stu-id="47e07-290">In hello **Specify Availability Group Name** page, type a name for hello Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="47e07-291">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-291">Click **Next**.</span></span>

    ![Kreator nowego AG, określ nazwę grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="47e07-293">W hello **wybierz baz danych** , wybierz bazę danych i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-293">In hello **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="47e07-294">Hello bazy danych spełnia wymagania wstępne powitania dla grupy dostępności, ponieważ co najmniej jedną pełną kopię zapasową wykonano na powitania zamierzone repliki podstawowej.</span><span class="sxs-lookup"><span data-stu-id="47e07-294">hello database meets hello prerequisites for an Availability Group because you have taken at least one full backup on hello intended primary replica.</span></span>

   ![Kreatora nowej grupy dostępności, wybierz baz danych](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="47e07-296">W hello **Określanie replik** kliknij przycisk **dodać repliki**.</span><span class="sxs-lookup"><span data-stu-id="47e07-296">In hello **Specify Replicas** page, click **Add Replica**.</span></span>

   ![Kreator nowego AG, określ repliki](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="47e07-298">Witaj **połączyć tooServer** wyskakującej okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="47e07-298">hello **Connect tooServer** dialog pops up.</span></span> <span data-ttu-id="47e07-299">Nazwa typu hello hello drugiego serwera w **nazwy serwera**.</span><span class="sxs-lookup"><span data-stu-id="47e07-299">Type hello name of hello second server in **Server name**.</span></span> <span data-ttu-id="47e07-300">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="47e07-300">Click **Connect**.</span></span>

   <span data-ttu-id="47e07-301">Po powrocie do hello **Określanie replik** strony, powinien zostać wyświetlony hello drugi serwer na liście **replik dostępności**.</span><span class="sxs-lookup"><span data-stu-id="47e07-301">Back in hello **Specify Replicas** page, you should now see hello second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="47e07-302">Konfigurowanie replik hello w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="47e07-302">Configure hello replicas as follows.</span></span>

   ![Kreator nowego AG, określ repliki (pełną)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="47e07-304">Kliknij przycisk **punkty końcowe** bazy danych hello toosee punktu końcowego dublowania dla tej grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="47e07-304">Click **Endpoints** toosee hello database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="47e07-305">Użyj hello sam portu można używać po ustawieniu hello [reguły zapory dla punktów końcowych dublowania bazy danych](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="47e07-305">Use hello same port that you used when you set hello [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![Kreatora nowej grupy dostępności, wybierz początkową synchronizację danych](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="47e07-307">W hello **Wybierz początkową synchronizację danych** wybierz **pełne** i określ udostępnionej lokalizacji sieciowej.</span><span class="sxs-lookup"><span data-stu-id="47e07-307">In hello **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="47e07-308">Dla lokalizacji hello Użyj hello [udziale kopii zapasowej utworzonego](#backupshare).</span><span class="sxs-lookup"><span data-stu-id="47e07-308">For hello location, use hello [backup share that you created](#backupshare).</span></span> <span data-ttu-id="47e07-309">W przykładzie hello został **\\\\\<pierwszy serwer SQL\>\Backup\**.</span><span class="sxs-lookup"><span data-stu-id="47e07-309">In hello example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="47e07-310">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="47e07-311">Pełna synchronizacja ma pełną kopię zapasową bazy danych hello na powitania pierwszego wystąpienia programu SQL Server i przywracania go toohello drugie wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="47e07-311">Full synchronization takes a full backup of hello database on hello first instance of SQL Server and restores it toohello second instance.</span></span> <span data-ttu-id="47e07-312">Pełna synchronizacja w przypadku dużych baz danych nie jest zalecane, ponieważ może zająć dużo czasu.</span><span class="sxs-lookup"><span data-stu-id="47e07-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="47e07-313">Teraz można zmniejszyć ręcznie wykonywanie kopii zapasowej bazy danych hello i przywracania jej z `NO RECOVERY`.</span><span class="sxs-lookup"><span data-stu-id="47e07-313">You can reduce this time by manually taking a backup of hello database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="47e07-314">Jeśli baza danych hello już została przywrócona z `NO RECOVERY` na powitania drugie programu SQL Server przed rozpoczęciem konfigurowania hello grupy dostępności, wybierz **tylko Dołącz**.</span><span class="sxs-lookup"><span data-stu-id="47e07-314">If hello database is already restored with `NO RECOVERY` on hello second SQL Server before configuring hello Availability Group, choose **Join only**.</span></span> <span data-ttu-id="47e07-315">Kopia zapasowa hello tootake po skonfigurowaniu hello grupy dostępności, wybierz opcję **Pomiń początkową synchronizację danych**.</span><span class="sxs-lookup"><span data-stu-id="47e07-315">If you want tootake hello backup after configuring hello Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![Kreatora nowej grupy dostępności, wybierz początkową synchronizację danych](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="47e07-317">W hello **weryfikacji** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="47e07-317">In hello **Validation** page, click **Next**.</span></span> <span data-ttu-id="47e07-318">Ta strona powinna wyglądać podobnie toohello po obrazu:</span><span class="sxs-lookup"><span data-stu-id="47e07-318">This page should look similar toohello following image:</span></span>

    ![Kreator nowego AG, sprawdzanie poprawności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="47e07-320">Brak ostrzeżenia dla konfiguracji odbiornika hello ponieważ odbiornika grupy dostępności nie zostały skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="47e07-320">There is a warning for hello listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="47e07-321">Można zignorować to ostrzeżenie, ponieważ na maszynach wirtualnych Azure tworzenia odbiornika powitania po utworzeniu usługi równoważenia obciążenia Azure hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-321">You can ignore this warning because on Azure virtual machines you create hello listener after creating hello Azure load balancer.</span></span>

10. <span data-ttu-id="47e07-322">W hello **Podsumowanie** kliknij przycisk **Zakończ**, a następnie zaczekaj, aż Kreator hello konfiguruje hello nowej grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="47e07-322">In hello **Summary** page, click **Finish**, then wait while hello wizard configures hello new Availability Group.</span></span> <span data-ttu-id="47e07-323">W hello **postępu** strony, możesz kliknąć **szczegółowe** tooview hello szczegółowe postępu.</span><span class="sxs-lookup"><span data-stu-id="47e07-323">In hello **Progress** page, you can click **More details** tooview hello detailed progress.</span></span> <span data-ttu-id="47e07-324">Po zakończeniu pracy Kreatora hello sprawdzić hello **wyniki** tooverify strony, która hello grupy dostępności została pomyślnie utworzona.</span><span class="sxs-lookup"><span data-stu-id="47e07-324">Once hello wizard is finished, inspect hello **Results** page tooverify that hello Availability Group is successfully created.</span></span>

     ![Wyniki w Kreatorze nowej grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="47e07-326">Kliknij przycisk **Zamknij** tooexit hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="47e07-326">Click **Close** tooexit hello wizard.</span></span>

### <a name="check-hello-availability-group"></a><span data-ttu-id="47e07-327">Sprawdź hello grupy dostępności</span><span class="sxs-lookup"><span data-stu-id="47e07-327">Check hello Availability Group</span></span>

1. <span data-ttu-id="47e07-328">W **Eksplorator obiektów**, rozwiń węzeł **wysokiej dostępności funkcji AlwaysOn**, następnie rozwiń węzeł **grup dostępności**.</span><span class="sxs-lookup"><span data-stu-id="47e07-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="47e07-329">Powinien zostać wyświetlony hello nowej grupy dostępności w tym kontenerze.</span><span class="sxs-lookup"><span data-stu-id="47e07-329">You should now see hello new Availability Group in this container.</span></span> <span data-ttu-id="47e07-330">Kliknij prawym przyciskiem myszy hello grupy dostępności, a następnie kliknij przycisk **Pokaż pulpit nawigacyjny**.</span><span class="sxs-lookup"><span data-stu-id="47e07-330">Right-click hello Availability Group and click **Show Dashboard**.</span></span>

   ![Pokaż AG pulpitu nawigacyjnego](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="47e07-332">Twoje **pulpitu nawigacyjnego AlwaysOn** powinien wyglądać podobnie toothis.</span><span class="sxs-lookup"><span data-stu-id="47e07-332">Your **AlwaysOn Dashboard** should look similar toothis.</span></span>

   ![Pulpit nawigacyjny grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="47e07-334">Widać hello replik, tryb pracy awaryjnej hello każdej repliki i hello stanu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="47e07-334">You can see hello replicas, hello failover mode of each replica and hello synchronization state.</span></span>

2. <span data-ttu-id="47e07-335">W **Menedżera klastra trybu Failover**, kliknij przycisk klastra.</span><span class="sxs-lookup"><span data-stu-id="47e07-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="47e07-336">Wybierz **ról**.</span><span class="sxs-lookup"><span data-stu-id="47e07-336">Select **Roles**.</span></span> <span data-ttu-id="47e07-337">Nazwa grupy dostępności Hello, używanego to rola na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="47e07-337">hello Availability Group name you used is a role on hello cluster.</span></span> <span data-ttu-id="47e07-338">Tej grupy dostępności nie ma adresu IP dla połączeń klienckich, ponieważ nie może skonfigurować odbiornik.</span><span class="sxs-lookup"><span data-stu-id="47e07-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="47e07-339">Skonfiguruj odbiornik powitania po utworzeniu usługi równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="47e07-339">You will configure hello listener after you create an Azure load balancer.</span></span>

   ![W Menedżerze klastra trybu Failover grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="47e07-341">Nie próbuj toofail za pośrednictwem hello grupy dostępności z hello Menedżera klastra trybu Failover.</span><span class="sxs-lookup"><span data-stu-id="47e07-341">Do not try toofail over hello Availability Group from hello Failover Cluster Manager.</span></span> <span data-ttu-id="47e07-342">Należy wykonać wszystkie operacje trybu failover z poziomu **pulpitu nawigacyjnego AlwaysOn** w programie SSMS.</span><span class="sxs-lookup"><span data-stu-id="47e07-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="47e07-343">Aby uzyskać więcej informacji, zobacz [ograniczenia dotyczące Using hello Menedżera klastra trybu Failover z grupami dostępności](https://msdn.microsoft.com/library/ff929171.aspx).</span><span class="sxs-lookup"><span data-stu-id="47e07-343">For more information, see [Restrictions on Using hello Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="47e07-344">W tym momencie masz grupę dostępności z replik na dwa wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="47e07-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="47e07-345">Witaj grupy dostępności można przenosić między wystąpieniami.</span><span class="sxs-lookup"><span data-stu-id="47e07-345">You can move hello Availability Group between instances.</span></span> <span data-ttu-id="47e07-346">Nie można połączyć toohello grupy dostępności jeszcze, ponieważ nie masz odbiornik.</span><span class="sxs-lookup"><span data-stu-id="47e07-346">You cannot connect toohello Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="47e07-347">W maszynach wirtualnych platformy Azure odbiornika hello wymaga usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="47e07-347">In Azure virtual machines, hello listener requires a load balancer.</span></span> <span data-ttu-id="47e07-348">Witaj następnym krokiem jest toocreate modułu równoważenia obciążenia hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="47e07-348">hello next step is toocreate hello load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="47e07-349">Tworzenie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="47e07-349">Create an Azure load balancer</span></span>

<span data-ttu-id="47e07-350">Na maszynach wirtualnych Azure grupy dostępności programu SQL Server wymaga usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="47e07-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="47e07-351">Moduł równoważenia obciążenia Hello przechowuje hello adresu IP dla odbiornika grupy dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-351">hello load balancer holds hello IP address for hello Availability Group listener.</span></span> <span data-ttu-id="47e07-352">Ta sekcja zawiera podsumowanie, jak usługa równoważenia w portalu Azure hello obciążenia toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-352">This section summarizes how toocreate hello load balancer in hello Azure portal.</span></span>

1. <span data-ttu-id="47e07-353">W hello portalu Azure, przejdź do pozycji toohello grupy zasobów, których są serwery SQL i kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="47e07-353">In hello Azure portal, go toohello resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="47e07-354">Wyszukaj **modułu równoważenia obciążenia**.</span><span class="sxs-lookup"><span data-stu-id="47e07-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="47e07-355">Wybierz moduł równoważenia obciążenia hello opublikowane przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="47e07-355">Choose hello load balancer published by Microsoft.</span></span>

   ![W Menedżerze klastra trybu Failover grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="47e07-357">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="47e07-357">Click **Create**.</span></span>
3. <span data-ttu-id="47e07-358">Skonfiguruj następujące parametry dla usługi równoważenia obciążenia hello hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-358">Configure hello following parameters for hello load balancer.</span></span>

   | <span data-ttu-id="47e07-359">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="47e07-359">Setting</span></span> | <span data-ttu-id="47e07-360">Pole</span><span class="sxs-lookup"><span data-stu-id="47e07-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="47e07-361">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="47e07-361">**Name**</span></span> |<span data-ttu-id="47e07-362">Użyj nazwy tekst hello modułu równoważenia obciążenia, na przykład **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="47e07-362">Use a text name for hello load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="47e07-363">**Typ**</span><span class="sxs-lookup"><span data-stu-id="47e07-363">**Type**</span></span> |<span data-ttu-id="47e07-364">wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="47e07-364">Internal</span></span> |
   | <span data-ttu-id="47e07-365">**Sieć wirtualna**</span><span class="sxs-lookup"><span data-stu-id="47e07-365">**Virtual network**</span></span> |<span data-ttu-id="47e07-366">Użyj nazwy hello hello sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="47e07-366">Use hello name of hello Azure virtual network.</span></span> |
   | <span data-ttu-id="47e07-367">**Podsieć**</span><span class="sxs-lookup"><span data-stu-id="47e07-367">**Subnet**</span></span> |<span data-ttu-id="47e07-368">Użyj nazwy hello hello podsieci, która hello maszyny wirtualnej jest w.</span><span class="sxs-lookup"><span data-stu-id="47e07-368">Use hello name of hello subnet that hello virtual machine is in.</span></span>  |
   | <span data-ttu-id="47e07-369">**Przypisywanie adresów IP**</span><span class="sxs-lookup"><span data-stu-id="47e07-369">**IP address assignment**</span></span> |<span data-ttu-id="47e07-370">Statyczny</span><span class="sxs-lookup"><span data-stu-id="47e07-370">Static</span></span> |
   | <span data-ttu-id="47e07-371">**Adres IP**</span><span class="sxs-lookup"><span data-stu-id="47e07-371">**IP address**</span></span> |<span data-ttu-id="47e07-372">Użyj dostępny adres podsieci.</span><span class="sxs-lookup"><span data-stu-id="47e07-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="47e07-373">**Subskrypcja**</span><span class="sxs-lookup"><span data-stu-id="47e07-373">**Subscription**</span></span> |<span data-ttu-id="47e07-374">Użyj hello sam subskrypcji jako hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="47e07-374">Use hello same subscription as hello virtual machine.</span></span> |
   | <span data-ttu-id="47e07-375">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="47e07-375">**Location**</span></span> |<span data-ttu-id="47e07-376">Użyj hello sam lokalizacji co hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="47e07-376">Use hello same location as hello virtual machine.</span></span> |

   <span data-ttu-id="47e07-377">Witaj bloku portalu Azure powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="47e07-377">hello Azure portal blade should look like this:</span></span>

   ![Tworzenie usługi równoważenia obciążenia](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="47e07-379">Kliknij przycisk **Utwórz**, usługi równoważenia obciążenia hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="47e07-379">Click **Create**, toocreate hello load balancer.</span></span>

<span data-ttu-id="47e07-380">Moduł równoważenia obciążenia hello tooconfigure, należy toocreate puli wewnętrznej bazy danych, sondowania i reguły równoważenia obciążenia hello zestawu.</span><span class="sxs-lookup"><span data-stu-id="47e07-380">tooconfigure hello load balancer, you need toocreate a backend pool, a probe, and set hello load balancing rules.</span></span> <span data-ttu-id="47e07-381">Czy w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="47e07-381">Do these in hello Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="47e07-382">Dodawanie puli wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="47e07-382">Add backend pool</span></span>

1. <span data-ttu-id="47e07-383">W hello portalu Azure Przejdź tooyour grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="47e07-383">In hello Azure portal, go tooyour availability group.</span></span> <span data-ttu-id="47e07-384">Może być konieczne równoważenia obciążenia hello nowo utworzony toosee toorefresh hello widoku.</span><span class="sxs-lookup"><span data-stu-id="47e07-384">You might need toorefresh hello view toosee hello newly created load balancer.</span></span>

   ![Znajdź moduł równoważenia obciążenia w grupie zasobów](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="47e07-386">Kliknij hello modułu równoważenia obciążenia, kliknij przycisk **pul zaplecza**i kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="47e07-386">Click hello load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="47e07-387">Ustaw puli zaplecza hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="47e07-387">Set hello backend pool as follows:</span></span>

   | <span data-ttu-id="47e07-388">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="47e07-388">Setting</span></span> | <span data-ttu-id="47e07-389">Opis</span><span class="sxs-lookup"><span data-stu-id="47e07-389">Description</span></span> | <span data-ttu-id="47e07-390">Przykład</span><span class="sxs-lookup"><span data-stu-id="47e07-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="47e07-391">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="47e07-391">**Name**</span></span> | <span data-ttu-id="47e07-392">Wpisz nazwę tekstu</span><span class="sxs-lookup"><span data-stu-id="47e07-392">Type a text name</span></span> | <span data-ttu-id="47e07-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="47e07-393">SQLLBBE</span></span>
   | <span data-ttu-id="47e07-394">**Skojarzony z**</span><span class="sxs-lookup"><span data-stu-id="47e07-394">**Associated to**</span></span> | <span data-ttu-id="47e07-395">Wybierz z listy</span><span class="sxs-lookup"><span data-stu-id="47e07-395">Pick from list</span></span> | <span data-ttu-id="47e07-396">Zestaw dostępności</span><span class="sxs-lookup"><span data-stu-id="47e07-396">Availability set</span></span>
   | <span data-ttu-id="47e07-397">**Zestaw dostępności**</span><span class="sxs-lookup"><span data-stu-id="47e07-397">**Availability set**</span></span> | <span data-ttu-id="47e07-398">Użyj nazwy zestawu dostępności hello, który maszyn wirtualnych programu SQL Server znajdują się w</span><span class="sxs-lookup"><span data-stu-id="47e07-398">Use a name of hello availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="47e07-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="47e07-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="47e07-400">**Maszyny wirtualne**</span><span class="sxs-lookup"><span data-stu-id="47e07-400">**Virtual machines**</span></span> |<span data-ttu-id="47e07-401">Witaj dwie nazwy maszyny Wirtualnej Azure SQL Server</span><span class="sxs-lookup"><span data-stu-id="47e07-401">hello two Azure SQL Server VM names</span></span> | <span data-ttu-id="47e07-402">SQLServer-0, sqlserver 1</span><span class="sxs-lookup"><span data-stu-id="47e07-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="47e07-403">Wpisz nazwę hello hello puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="47e07-403">Type hello name for hello back end pool.</span></span>

1. <span data-ttu-id="47e07-404">Kliknij przycisk **+ Dodaj maszynę wirtualną**.</span><span class="sxs-lookup"><span data-stu-id="47e07-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="47e07-405">Dla zestawu dostępności hello wybierz ten hello serwerami programu SQL Server znajdują się w zestawie dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-405">For hello availability set, choose hello availability set that hello SQL Servers are in.</span></span>

1. <span data-ttu-id="47e07-406">W przypadku maszyn wirtualnych zawierają oba hello serwerów SQL.</span><span class="sxs-lookup"><span data-stu-id="47e07-406">For virtual machines, include both of hello SQL Servers.</span></span> <span data-ttu-id="47e07-407">Nie dołączaj serwera monitora udziału plików hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-407">Do not include hello file share witness server.</span></span>

1. <span data-ttu-id="47e07-408">Kliknij przycisk **OK** puli zaplecza hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="47e07-408">Click **OK** toocreate hello backend pool.</span></span>

### <a name="set-hello-probe"></a><span data-ttu-id="47e07-409">Sonda zbioru hello</span><span class="sxs-lookup"><span data-stu-id="47e07-409">Set hello probe</span></span>

1. <span data-ttu-id="47e07-410">Kliknij hello modułu równoważenia obciążenia, kliknij przycisk **sondy kondycji**i kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="47e07-410">Click hello load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="47e07-411">Ustaw sondy kondycji hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="47e07-411">Set hello health probe as follows:</span></span>

   | <span data-ttu-id="47e07-412">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="47e07-412">Setting</span></span> | <span data-ttu-id="47e07-413">Opis</span><span class="sxs-lookup"><span data-stu-id="47e07-413">Description</span></span> | <span data-ttu-id="47e07-414">Przykład</span><span class="sxs-lookup"><span data-stu-id="47e07-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="47e07-415">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="47e07-415">**Name**</span></span> | <span data-ttu-id="47e07-416">Tekst</span><span class="sxs-lookup"><span data-stu-id="47e07-416">Text</span></span> | <span data-ttu-id="47e07-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="47e07-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="47e07-418">**Protokół**</span><span class="sxs-lookup"><span data-stu-id="47e07-418">**Protocol**</span></span> | <span data-ttu-id="47e07-419">Wybierz protokół TCP</span><span class="sxs-lookup"><span data-stu-id="47e07-419">Choose TCP</span></span> | <span data-ttu-id="47e07-420">TCP</span><span class="sxs-lookup"><span data-stu-id="47e07-420">TCP</span></span> |
   | <span data-ttu-id="47e07-421">**Port**</span><span class="sxs-lookup"><span data-stu-id="47e07-421">**Port**</span></span> | <span data-ttu-id="47e07-422">Wszelkie nieużywany port.</span><span class="sxs-lookup"><span data-stu-id="47e07-422">Any unused port</span></span> | <span data-ttu-id="47e07-423">59999</span><span class="sxs-lookup"><span data-stu-id="47e07-423">59999</span></span> |
   | <span data-ttu-id="47e07-424">**Interwał**</span><span class="sxs-lookup"><span data-stu-id="47e07-424">**Interval**</span></span>  | <span data-ttu-id="47e07-425">Witaj ilość czasu między sondowania prób w sekundach</span><span class="sxs-lookup"><span data-stu-id="47e07-425">hello amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="47e07-426">5</span><span class="sxs-lookup"><span data-stu-id="47e07-426">5</span></span> |
   | <span data-ttu-id="47e07-427">**Próg złej kondycji**</span><span class="sxs-lookup"><span data-stu-id="47e07-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="47e07-428">Witaj liczbę kolejnych niepowodzeń sondy musi nastąpić toobe maszyny wirtualnej, określana jako Zła</span><span class="sxs-lookup"><span data-stu-id="47e07-428">hello number of consecutive probe failures that must occur for a virtual machine toobe considered unhealthy</span></span>  | <span data-ttu-id="47e07-429">2</span><span class="sxs-lookup"><span data-stu-id="47e07-429">2</span></span> |

1. <span data-ttu-id="47e07-430">Kliknij przycisk **OK** sondy kondycji hello tooset.</span><span class="sxs-lookup"><span data-stu-id="47e07-430">Click **OK** tooset hello health probe.</span></span>

### <a name="set-hello-load-balancing-rules"></a><span data-ttu-id="47e07-431">Ustaw reguły równoważenia obciążenia hello</span><span class="sxs-lookup"><span data-stu-id="47e07-431">Set hello load balancing rules</span></span>

1. <span data-ttu-id="47e07-432">Kliknij hello modułu równoważenia obciążenia, kliknij przycisk **reguły równoważenia obciążenia**i kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="47e07-432">Click hello load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="47e07-433">Ustaw reguły były w następujący sposób równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-433">Set hello load balancing rules as follows.</span></span>
   | <span data-ttu-id="47e07-434">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="47e07-434">Setting</span></span> | <span data-ttu-id="47e07-435">Opis</span><span class="sxs-lookup"><span data-stu-id="47e07-435">Description</span></span> | <span data-ttu-id="47e07-436">Przykład</span><span class="sxs-lookup"><span data-stu-id="47e07-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="47e07-437">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="47e07-437">**Name**</span></span> | <span data-ttu-id="47e07-438">Tekst</span><span class="sxs-lookup"><span data-stu-id="47e07-438">Text</span></span> | <span data-ttu-id="47e07-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="47e07-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="47e07-440">**Adres IP frontonu**</span><span class="sxs-lookup"><span data-stu-id="47e07-440">**Frontend IP address**</span></span> | <span data-ttu-id="47e07-441">Wybierz adres</span><span class="sxs-lookup"><span data-stu-id="47e07-441">Choose an address</span></span> |<span data-ttu-id="47e07-442">Użyj adresu hello, który został utworzony podczas tworzenia modułu równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-442">Use hello address that you created when you created hello load balancer.</span></span> |
   | <span data-ttu-id="47e07-443">**Protokół**</span><span class="sxs-lookup"><span data-stu-id="47e07-443">**Protocol**</span></span> | <span data-ttu-id="47e07-444">Wybierz protokół TCP</span><span class="sxs-lookup"><span data-stu-id="47e07-444">Choose TCP</span></span> |<span data-ttu-id="47e07-445">TCP</span><span class="sxs-lookup"><span data-stu-id="47e07-445">TCP</span></span> |
   | <span data-ttu-id="47e07-446">**Port**</span><span class="sxs-lookup"><span data-stu-id="47e07-446">**Port**</span></span> | <span data-ttu-id="47e07-447">Korzystając z portu hello hello wystąpienia programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="47e07-447">Use hello port for hello SQL Server instance</span></span> | <span data-ttu-id="47e07-448">1433</span><span class="sxs-lookup"><span data-stu-id="47e07-448">1433</span></span> |
   | <span data-ttu-id="47e07-449">**Port zaplecza**</span><span class="sxs-lookup"><span data-stu-id="47e07-449">**Backend Port**</span></span> | <span data-ttu-id="47e07-450">To pole nie jest używany, gdy pływający adres IP jest wartość dla serwera bezpośredniego zwrotu</span><span class="sxs-lookup"><span data-stu-id="47e07-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="47e07-451">1433</span><span class="sxs-lookup"><span data-stu-id="47e07-451">1433</span></span> |
   | <span data-ttu-id="47e07-452">**Sondy**</span><span class="sxs-lookup"><span data-stu-id="47e07-452">**Probe**</span></span> |<span data-ttu-id="47e07-453">Nazwa Hello hello sondy</span><span class="sxs-lookup"><span data-stu-id="47e07-453">hello name you specified for hello probe</span></span> | <span data-ttu-id="47e07-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="47e07-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="47e07-455">**Trwałość sesji**</span><span class="sxs-lookup"><span data-stu-id="47e07-455">**Session Persistence**</span></span> | <span data-ttu-id="47e07-456">Listy rozwijanej</span><span class="sxs-lookup"><span data-stu-id="47e07-456">Drop down list</span></span> | <span data-ttu-id="47e07-457">**Brak**</span><span class="sxs-lookup"><span data-stu-id="47e07-457">**None**</span></span> |
   | <span data-ttu-id="47e07-458">**Limit czasu bezczynności**</span><span class="sxs-lookup"><span data-stu-id="47e07-458">**Idle Timeout**</span></span> | <span data-ttu-id="47e07-459">Otwórz połączenie TCP tookeep minut</span><span class="sxs-lookup"><span data-stu-id="47e07-459">Minutes tookeep a TCP connection open</span></span> | <span data-ttu-id="47e07-460">4</span><span class="sxs-lookup"><span data-stu-id="47e07-460">4</span></span> |
   | <span data-ttu-id="47e07-461">**Zmienny adres IP (bezpośredni zwrot serwera)**</span><span class="sxs-lookup"><span data-stu-id="47e07-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="47e07-462">Enabled (Włączony)</span><span class="sxs-lookup"><span data-stu-id="47e07-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="47e07-463">Bezpośredni zwrot serwera jest ustawiana podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="47e07-463">Direct server return is set during creation.</span></span> <span data-ttu-id="47e07-464">Nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="47e07-464">It cannot be changed.</span></span>

1. <span data-ttu-id="47e07-465">Kliknij przycisk **OK** reguły równoważenia obciążenia hello tooset.</span><span class="sxs-lookup"><span data-stu-id="47e07-465">Click **OK** tooset hello load balancing rules.</span></span>

## <span data-ttu-id="47e07-466"><a name="configure-listener"></a>Skonfiguruj odbiornik hello</span><span class="sxs-lookup"><span data-stu-id="47e07-466"><a name="configure-listener"></a> Configure hello listener</span></span>

<span data-ttu-id="47e07-467">dalej toodo operacją Hello jest tooconfigure odbiornika grupy dostępności w klastrze trybu failover hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-467">hello next thing toodo is tooconfigure an Availability Group listener on hello failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="47e07-468">Ten samouczek pokazuje, jak adres toocreate jednego odbiornika — jeden ILB protokołu IP.</span><span class="sxs-lookup"><span data-stu-id="47e07-468">This tutorial shows how toocreate a single listener - with one ILB IP address.</span></span> <span data-ttu-id="47e07-469">toocreate co najmniej jednego odbiornika za pomocą jednego lub więcej adresów IP, zobacz [odbiornika Create Availability Group, a moduł równoważenia obciążenia | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="47e07-469">toocreate one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="47e07-470">Port odbiornika zestawu</span><span class="sxs-lookup"><span data-stu-id="47e07-470">Set listener port</span></span>

<span data-ttu-id="47e07-471">W programu SQL Server Management Studio Ustaw hello port odbiornika.</span><span class="sxs-lookup"><span data-stu-id="47e07-471">In SQL Server Management Studio, set hello listener port.</span></span>

1. <span data-ttu-id="47e07-472">Uruchom program SQL Server Management Studio i połącz toohello repliki podstawowej.</span><span class="sxs-lookup"><span data-stu-id="47e07-472">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="47e07-473">Przejdź za**wysokiej dostępności funkcji AlwaysOn** | **grup dostępności** | **odbiorniki grupy dostępności**.</span><span class="sxs-lookup"><span data-stu-id="47e07-473">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="47e07-474">Powinna zostać wyświetlona nazwa odbiornika hello utworzonego w Menedżerze klastra trybu Failover.</span><span class="sxs-lookup"><span data-stu-id="47e07-474">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="47e07-475">Kliknij prawym przyciskiem myszy nazwę odbiornika hello, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="47e07-475">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="47e07-476">W hello **portu** Określ numer portu odbiornika grupy dostępności hello hello przy użyciu hello $EndpointPort użyto wcześniej (1433 była hello domyślna), następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="47e07-476">In hello **Port** box, specify hello port number for hello Availability Group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

<span data-ttu-id="47e07-477">Masz teraz grupy dostępności programu SQL Server na maszynach wirtualnych Azure działających w trybie Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="47e07-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-toolistener"></a><span data-ttu-id="47e07-478">Test połączenia toolistener</span><span class="sxs-lookup"><span data-stu-id="47e07-478">Test connection toolistener</span></span>

<span data-ttu-id="47e07-479">tootest hello połączenia:</span><span class="sxs-lookup"><span data-stu-id="47e07-479">tootest hello connection:</span></span>

1. <span data-ttu-id="47e07-480">RDP tooa programu SQL Server, który znajduje się w hello sam wirtualnych sieci, ale nie nie własnych hello repliki.</span><span class="sxs-lookup"><span data-stu-id="47e07-480">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="47e07-481">Można użyć innego serwera SQL w klastrze hello hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-481">You can use hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="47e07-482">Użyj **sqlcmd** narzędzie tootest hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="47e07-482">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="47e07-483">Na przykład ustanawia hello następującego skryptu **sqlcmd** repliki podstawowej toohello połączenia za pośrednictwem hello odbiornika z uwierzytelnianiem systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="47e07-483">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="47e07-484">Jeśli odbiornik hello używa portu innego niż hello domyślnego portu (1433), określ hello port w parametrach połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-484">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="47e07-485">Na przykład hello następującego polecenia sqlcmd łączy odbiornika tooa portu 1435:</span><span class="sxs-lookup"><span data-stu-id="47e07-485">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="47e07-486">Witaj SQLCMD połączenia automatycznie łączy toowhichever wystąpienie programu SQL Server repliki podstawowej hello hostów.</span><span class="sxs-lookup"><span data-stu-id="47e07-486">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="47e07-487">Upewnij się, że port hello określony jest otwarty na zaporze hello obu serwerów SQL.</span><span class="sxs-lookup"><span data-stu-id="47e07-487">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="47e07-488">Oba serwery wymagają regułę ruchu przychodzącego dla portu TCP, którego używasz hello.</span><span class="sxs-lookup"><span data-stu-id="47e07-488">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="47e07-489">Aby uzyskać więcej informacji, zobacz [Dodawanie lub edytowanie reguły zapory](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="47e07-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a><span data-ttu-id="47e07-490">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="47e07-490">Next steps</span></span>

- <span data-ttu-id="47e07-491">[Dodaj IP adres tooa Usługa równoważenia obciążenia w grupie dostępności drugi](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span><span class="sxs-lookup"><span data-stu-id="47e07-491">[Add an IP address tooa load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
