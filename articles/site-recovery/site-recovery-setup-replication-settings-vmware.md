---
title: "aaaSet ustawienia replikacji dla usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooAzure chmur toodeploy usługi Site Recovery tooorchestrate replikacji, trybu failover i odzyskiwania maszyn wirtualnych funkcji Hyper-V w programie VMM."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a><span data-ttu-id="93b69-103">Zarządzanie zasadami replikacji dla VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="93b69-103">Manage replication policy for VMware tooAzure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="93b69-104">Tworzenie zasad replikacji</span><span class="sxs-lookup"><span data-stu-id="93b69-104">Create a replication policy</span></span>

1. <span data-ttu-id="93b69-105">Wybierz pozycję **Zarządzaj** > **Infrastruktura usługi Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="93b69-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="93b69-106">Wybierz pozycję **Zasady replikacji** w sekcji **Oprogramowanie VMware i maszyny fizyczne**.</span><span class="sxs-lookup"><span data-stu-id="93b69-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="93b69-107">Wybierz pozycję **+Zasady replikacji**.</span><span class="sxs-lookup"><span data-stu-id="93b69-107">Select **+Replication policy**.</span></span>

    ![Tworzenie zasad replikacji](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="93b69-109">Wprowadź nazwę zasad hello.</span><span class="sxs-lookup"><span data-stu-id="93b69-109">Enter hello policy name.</span></span>

5. <span data-ttu-id="93b69-110">W **próg RPO**, określ hello RPO limit.</span><span class="sxs-lookup"><span data-stu-id="93b69-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="93b69-111">Przekroczenie tego limitu przez replikację ciągłą będzie powodować generowanie alertów.</span><span class="sxs-lookup"><span data-stu-id="93b69-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="93b69-112">W **przechowywania punktu odzyskiwania**, określ (w godzinach) hello hello przechowywania przedział czasu dla każdego punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="93b69-112">In **Recovery point retention**, specify (in hours) hello duration of hello retention window for each recovery point.</span></span> <span data-ttu-id="93b69-113">Chronione maszyny można odzyskać tooany punkt w obrębie okna przechowywania.</span><span class="sxs-lookup"><span data-stu-id="93b69-113">Protected machines can be recovered tooany point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="93b69-114">Zapasowej too24 godzin przechowywania jest obsługiwana dla maszyn toopremium replikowanego magazynu.</span><span class="sxs-lookup"><span data-stu-id="93b69-114">Up too24 hours of retention is supported for machines replicated toopremium storage.</span></span> <span data-ttu-id="93b69-115">Zapasowej too72 godzin przechowywania jest obsługiwana dla maszyn toostandard replikowanego magazynu.</span><span class="sxs-lookup"><span data-stu-id="93b69-115">Up too72 hours of retention is supported for machines replicated toostandard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="93b69-116">Zasady replikacji na potrzeby powrotu po awarii są tworzone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="93b69-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="93b69-117">W obszarze **Częstotliwość wykonywania migawek na poziomie aplikacji** określ, jak często (w minutach) będą tworzone punkty odzyskiwania zawierające migawki spójne z aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="93b69-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="93b69-118">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="93b69-118">Click **OK**.</span></span> <span data-ttu-id="93b69-119">Witaj zasady powinny zostać utworzone w too60 30-sekundowym.</span><span class="sxs-lookup"><span data-stu-id="93b69-119">hello policy should be created in 30 too60 seconds.</span></span>

![Generowanie zasad replikacji](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="93b69-121">Kojarzenie serwera konfiguracji z zasadami replikacji</span><span class="sxs-lookup"><span data-stu-id="93b69-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="93b69-122">Wybierz toowhich zasad replikacji hello ma tooassociate hello konfiguracji serwera.</span><span class="sxs-lookup"><span data-stu-id="93b69-122">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="93b69-123">Kliknij pozycję **Skojarz**.</span><span class="sxs-lookup"><span data-stu-id="93b69-123">Click **Associate**.</span></span>
<span data-ttu-id="93b69-124">![Kojarzenie serwera konfiguracji](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="93b69-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="93b69-125">Wybierz serwer konfiguracji hello hello liście serwerów.</span><span class="sxs-lookup"><span data-stu-id="93b69-125">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="93b69-126">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="93b69-126">Click **OK**.</span></span> <span data-ttu-id="93b69-127">Serwer konfiguracji Hello powinna być skojarzona jeden tootwo minut.</span><span class="sxs-lookup"><span data-stu-id="93b69-127">hello configuration server should be associated in one tootwo minutes.</span></span>

![Kojarzenie serwera konfiguracji](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="93b69-129">Edytowanie zasad replikacji</span><span class="sxs-lookup"><span data-stu-id="93b69-129">Edit a replication policy</span></span>
1. <span data-ttu-id="93b69-130">Wybierz zasady replikacji hello, dla której ma zostać tooedit ustawień replikacji.</span><span class="sxs-lookup"><span data-stu-id="93b69-130">Choose hello replication policy for which you want tooedit replication settings.</span></span>
<span data-ttu-id="93b69-131">![Edytowanie zasad replikacji](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="93b69-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="93b69-132">Kliknij pozycję **Edytuj ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="93b69-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="93b69-133">![Edytowanie ustawień zasad replikacji](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="93b69-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="93b69-134">Zmień ustawienia hello oparte na potrzeby.</span><span class="sxs-lookup"><span data-stu-id="93b69-134">Change hello settings based on your need.</span></span>
4. <span data-ttu-id="93b69-135">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="93b69-135">Click **Save**.</span></span> <span data-ttu-id="93b69-136">zasady Hello powinny być zapisywane w dwóch minut toofive, w zależności od liczby maszyn wirtualnych korzystają z tej zasady replikacji.</span><span class="sxs-lookup"><span data-stu-id="93b69-136">hello policy should be saved in two toofive minutes, depending on how many VMs are using that replication policy.</span></span>

![Zapisywanie zasad replikacji](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="93b69-138">Usuwanie skojarzenia serwera konfiguracji z zasad replikacji</span><span class="sxs-lookup"><span data-stu-id="93b69-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="93b69-139">Wybierz toowhich zasad replikacji hello ma tooassociate hello konfiguracji serwera.</span><span class="sxs-lookup"><span data-stu-id="93b69-139">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="93b69-140">Kliknij pozycję **Usuń skojarzenie**.</span><span class="sxs-lookup"><span data-stu-id="93b69-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="93b69-141">Wybierz serwer konfiguracji hello hello liście serwerów.</span><span class="sxs-lookup"><span data-stu-id="93b69-141">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="93b69-142">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="93b69-142">Click **OK**.</span></span> <span data-ttu-id="93b69-143">Serwer konfiguracji Hello powinien można usunąć skojarzenia minut tootwo jeden.</span><span class="sxs-lookup"><span data-stu-id="93b69-143">hello configuration server should be dissociated in one tootwo minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="93b69-144">Jeśli istnieje co najmniej jeden element replikowane za pomocą zasad hello nie może usunąć skojarzenie serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="93b69-144">You cannot dissociate a configuration server if there is at least one replicated item using hello policy.</span></span> <span data-ttu-id="93b69-145">Upewnij się, nie ma żadnych zreplikowanych towarów przy użyciu zasad hello przed skojarzenie powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="93b69-145">Make sure there are no replicated items using hello policy before you dissociate hello configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="93b69-146">Usuwanie zasad replikacji</span><span class="sxs-lookup"><span data-stu-id="93b69-146">Delete a replication policy</span></span>

1. <span data-ttu-id="93b69-147">Wybierz zasady replikacji hello, które mają toodelete.</span><span class="sxs-lookup"><span data-stu-id="93b69-147">Choose hello replication policy that you want toodelete.</span></span>
2. <span data-ttu-id="93b69-148">Kliknij polecenie **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="93b69-148">Click **Delete**.</span></span> <span data-ttu-id="93b69-149">Witaj zasady powinny zostać usunięte w ciągu 30 sekund too60.</span><span class="sxs-lookup"><span data-stu-id="93b69-149">hello policy should be deleted in 30 too60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="93b69-150">Nie można usunąć zasad replikacji, jeśli ma ona co najmniej jeden tooit skojarzone serwerem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="93b69-150">You cannot delete a replication policy if it has at least one configuration server associated tooit.</span></span> <span data-ttu-id="93b69-151">Upewnij się, że nie ma żadnych zreplikowanych elementów za pomocą zasad hello i usunąć wszystkie hello skojarzone serwery konfiguracji przed usunięciem hello zasad.</span><span class="sxs-lookup"><span data-stu-id="93b69-151">Make sure there are no replicated items using hello policy and delete all hello associated configuration servers before you delete hello policy.</span></span>
