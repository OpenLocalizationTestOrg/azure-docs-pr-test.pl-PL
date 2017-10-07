---
title: "tooconfigure aaaHow usługi w chmurze (portal) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usług w chmurze tooconfigure na platformie Azure. Dowiedz się, konfiguracji usługi w chmurze hello tooupdate i skonfiguruj wystąpień toorole dostępu zdalnego. Poniższe przykłady użycia hello portalu Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a><span data-ttu-id="5e46d-105">W jaki sposób tooConfigure usług w chmurze</span><span class="sxs-lookup"><span data-stu-id="5e46d-105">How tooConfigure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e46d-106">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5e46d-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="5e46d-107">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5e46d-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="5e46d-108">Usługi w chmurze hello najczęściej używane ustawienia można skonfigurować w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5e46d-108">You can configure hello most commonly used settings for a cloud service in hello Azure portal.</span></span> <span data-ttu-id="5e46d-109">Lub, jeśli chcesz tooupdate plikach konfiguracyjnych bezpośrednio, Pobierz tooupdate pliku konfiguracji usługi, a następnie przekaż hello zaktualizowany plik i aktualizacji hello usługi w chmurze hello zmian konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5e46d-109">Or, if you like tooupdate your configuration files directly, download a service configuration file tooupdate, and then upload hello updated file and update hello cloud service with hello configuration changes.</span></span> <span data-ttu-id="5e46d-110">W obu przypadkach aktualizacji konfiguracji hello są wypychani tooall wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="5e46d-110">Either way, hello configuration updates are pushed out tooall role instances.</span></span>

<span data-ttu-id="5e46d-111">Można również zarządzać wystąpień hello role usługi w chmurze lub pulpitu zdalnego do nich.</span><span class="sxs-lookup"><span data-stu-id="5e46d-111">You can also manage hello instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="5e46d-112">Azure można tylko zapewnienia dostępności usług 99,95% podczas hello aktualizacji konfiguracji Jeśli masz co najmniej dwóch wystąpień roli dla każdej roli.</span><span class="sxs-lookup"><span data-stu-id="5e46d-112">Azure can only ensure 99.95 percent service availability during hello configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="5e46d-113">Umożliwiająca jednego żądania klientów tooprocess maszyny wirtualnej podczas aktualizowania hello innych.</span><span class="sxs-lookup"><span data-stu-id="5e46d-113">That enables one virtual machine tooprocess client requests while hello other is being updated.</span></span> <span data-ttu-id="5e46d-114">Aby uzyskać więcej informacji, zobacz [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="5e46d-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="5e46d-115">Zmiana usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="5e46d-115">Change a cloud service</span></span>
<span data-ttu-id="5e46d-116">Po otwierającym hello [portalu Azure](https://portal.azure.com/), przejdź tooyour usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5e46d-116">After opening hello [Azure portal](https://portal.azure.com/), navigate tooyour cloud service.</span></span> <span data-ttu-id="5e46d-117">W tym miejscu możesz zarządzać wiele aspektów.</span><span class="sxs-lookup"><span data-stu-id="5e46d-117">From here, you manage many aspects of it.</span></span>

![Ustawienia strony](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="5e46d-119">Witaj **ustawienia** lub **wszystkie ustawienia** łącza spowoduje to otwarcie hello **ustawienia** bloku, w którym można zmienić hello **właściwości**, zmień hello **Konfiguracji**, zarządzanie hello **certyfikaty**, Instalator **reguły alertów**i zarządzanie nimi hello **użytkowników** mają dostęp usługi w chmurze toothis.</span><span class="sxs-lookup"><span data-stu-id="5e46d-119">hello **Settings** or **All settings** links will open up hello **Settings** blade where you can change hello **Properties**, change hello **Configuration**, manage hello **Certificates**, setup **Alert rules**, and manage hello **Users** who have access toothis cloud service.</span></span>

![Blok ustawień usługi w chmurze Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="5e46d-121">Zarządzanie wersji systemu operacyjnego gościa</span><span class="sxs-lookup"><span data-stu-id="5e46d-121">Manage Guest OS version</span></span>

<span data-ttu-id="5e46d-122">Domyślnie program Azure okresowo aktualizuje użytkownika gościa obrazu systemu operacyjnego toohello najnowszych obsługiwane w ramach hello rodziny systemów operacyjnych, określoną w konfiguracji usługi (cscfg), takie jak Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="5e46d-122">By default, Azure periodically updates your guest OS toohello latest supported image within hello OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="5e46d-123">Tootarget określonych wersji systemu operacyjnego, należy można ustawić w hello **konfiguracji** bloku.</span><span class="sxs-lookup"><span data-stu-id="5e46d-123">If you need tootarget a specific OS version, you can set it in hello **Configuration** blade.</span></span>

![Ustaw wersję systemu operacyjnego](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="5e46d-125">Wybranie określonych wersji systemu operacyjnego spowoduje wyłączenie automatycznego systemu operacyjnego aktualizacji i umożliwia stosowanie poprawek programu odpowiedzialności.</span><span class="sxs-lookup"><span data-stu-id="5e46d-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="5e46d-126">Należy upewnić się, że wystąpienia roli otrzymują aktualizacje lub może narazić Twoje luk w zabezpieczeniach toosecurity aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5e46d-126">You must ensure that your role instances are receiving updates or you may expose your application toosecurity vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="5e46d-127">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="5e46d-127">Monitoring</span></span>
<span data-ttu-id="5e46d-128">Można dodać usługi w chmurze tooyour alertów.</span><span class="sxs-lookup"><span data-stu-id="5e46d-128">You can add alerts tooyour cloud service.</span></span> <span data-ttu-id="5e46d-129">Kliknij przycisk **ustawienia** > **reguły alertu** > **Dodaj alert**.</span><span class="sxs-lookup"><span data-stu-id="5e46d-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="5e46d-130">W tym miejscu możesz skonfigurować alert.</span><span class="sxs-lookup"><span data-stu-id="5e46d-130">From here, you can setup an alert.</span></span> <span data-ttu-id="5e46d-131">Z hello **Metryka** listy rozwijanej, można ustawić alert hello następujące typy danych.</span><span class="sxs-lookup"><span data-stu-id="5e46d-131">With hello **Metric** drop down box, you can setup an alert for hello following types of data.</span></span>

* <span data-ttu-id="5e46d-132">Odczytu dysku</span><span class="sxs-lookup"><span data-stu-id="5e46d-132">Disk read</span></span>
* <span data-ttu-id="5e46d-133">Zapisu na dysku</span><span class="sxs-lookup"><span data-stu-id="5e46d-133">Disk write</span></span>
* <span data-ttu-id="5e46d-134">Sieci w</span><span class="sxs-lookup"><span data-stu-id="5e46d-134">Network in</span></span>
* <span data-ttu-id="5e46d-135">Sieci limit</span><span class="sxs-lookup"><span data-stu-id="5e46d-135">Network out</span></span>
* <span data-ttu-id="5e46d-136">Procent użycia procesora CPU</span><span class="sxs-lookup"><span data-stu-id="5e46d-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="5e46d-137">Skonfiguruj funkcję monitorowania z metryki kafelka</span><span class="sxs-lookup"><span data-stu-id="5e46d-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="5e46d-138">Zamiast **ustawienia** > **reguły alertów**, możesz kliknąć jeden z hello metryki kafelków w hello **monitorowanie** sekcji hello **chmury Usługa** bloku.</span><span class="sxs-lookup"><span data-stu-id="5e46d-138">Instead of using **Settings** > **Alert Rules**, you can click on one of hello metric tiles in hello **Monitoring** section of hello **Cloud service** blade.</span></span>

![Monitorowanie usługi w chmurze](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="5e46d-140">W tym miejscu można dostosować wykres hello używane z kafelka hello, lub dodać reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="5e46d-140">From here you can customize hello chart used with hello tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="5e46d-141">Ponowne uruchomienie komputera, odtworzenia z obrazu lub pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="5e46d-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="5e46d-142">W tej chwili nie można konfigurować usługi pulpitu zdalnego przy użyciu hello **portalu Azure**.</span><span class="sxs-lookup"><span data-stu-id="5e46d-142">At this time you cannot configure remote desktop using hello **Azure portal**.</span></span> <span data-ttu-id="5e46d-143">Jednak można skonfigurować go za pośrednictwem hello [klasycznego portalu Azure](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), lub za pomocą [programu Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="5e46d-143">However, you can set it up through hello [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="5e46d-144">Najpierw kliknij w wystąpieniu usługi chmury hello.</span><span class="sxs-lookup"><span data-stu-id="5e46d-144">First, click on hello cloud service instance.</span></span>

![Wystąpienie usługi w chmurze](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="5e46d-146">Z hello bloku, który zostanie otwarty, możesz zainicjować połączenie pulpitu zdalnego, zdalnie ponownie hello, lub zdalnie odtworzenia z obrazu (start z obrazem świeże) hello wystąpieniu.</span><span class="sxs-lookup"><span data-stu-id="5e46d-146">From hello blade that opens you can initiate a remote desktop connection, remotely reboot hello instance, or remotely reimage (start with a fresh image) hello instance.</span></span>

![Przyciski wystąpienia usługi chmury](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="5e46d-148">Skonfiguruj ponownie Twoje .cscfg</span><span class="sxs-lookup"><span data-stu-id="5e46d-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="5e46d-149">Może być konieczne tooreconfigure usługi w chmurze za pośrednictwem hello [konfiguracji usługi (cscfg)](cloud-services-model-and-package.md#cscfg) pliku.</span><span class="sxs-lookup"><span data-stu-id="5e46d-149">You may need tooreconfigure your cloud service through hello [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="5e46d-150">Najpierw należy toodownload Twojego .cscfg pliku, zmodyfikuj go, a następnie przekaż go.</span><span class="sxs-lookup"><span data-stu-id="5e46d-150">First you need toodownload your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="5e46d-151">Polecenie hello **ustawienia** ikony lub hello **wszystkie ustawienia** link tooopen się hello **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="5e46d-151">Click on hello **Settings** icon or hello **All settings** link tooopen up hello **Settings** blade.</span></span>

    ![Ustawienia strony](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="5e46d-153">Polecenie hello **konfiguracji** elementu.</span><span class="sxs-lookup"><span data-stu-id="5e46d-153">Click on hello **Configuration** item.</span></span>

    ![Blok konfiguracji](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="5e46d-155">Polecenie hello **Pobierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5e46d-155">Click on hello **Download** button.</span></span>

    ![Do pobrania](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="5e46d-157">Po zaktualizowaniu pliku konfiguracji usługi hello, przekazywanie i stosowania aktualizacji konfiguracji hello:</span><span class="sxs-lookup"><span data-stu-id="5e46d-157">After you update hello service configuration file, upload and apply hello configuration updates:</span></span>

    ![Upload](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="5e46d-159">Wybierz plik .cscfg hello, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="5e46d-159">Select hello .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e46d-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5e46d-160">Next steps</span></span>
* <span data-ttu-id="5e46d-161">Dowiedz się, jak za[wdrażania usługi w chmurze](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5e46d-161">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="5e46d-162">Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5e46d-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="5e46d-163">[Usługi w chmurze zarządzanie](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5e46d-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="5e46d-164">Skonfiguruj [certyfikaty ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5e46d-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
