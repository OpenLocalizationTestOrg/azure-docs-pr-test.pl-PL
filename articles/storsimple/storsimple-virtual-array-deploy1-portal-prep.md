---
title: Portal przedprodukcyjnym dla tablicy wirtualnego StorSimple | Dokumentacja firmy Microsoft
description: "Pierwszy samouczek, aby wdrożyć wirtualny tablicy StorSimple obejmuje przygotowanie portalu Azure"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3d0801053721f98ce7a2b0fcbe3c65da8dbdd8d3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-the-azure-portal"></a><span data-ttu-id="77c3f-103">Wdrażanie tablicy wirtualne StorSimple — przygotowanie portalu Azure</span><span class="sxs-lookup"><span data-stu-id="77c3f-103">Deploy StorSimple Virtual Array - Prepare the Azure portal</span></span>

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a><span data-ttu-id="77c3f-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="77c3f-104">Overview</span></span>

<span data-ttu-id="77c3f-105">Jest to pierwszy artykuł z serii samouczki wdrażania wymaganych do całkowicie wdrożenia wirtualnego tablica jako serwera plików lub serwera iSCSI przy użyciu modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="77c3f-105">This is the first article in the series of deployment tutorials required to completely deploy your virtual array as a file server or an iSCSI server using the Resource Manager model.</span></span> <span data-ttu-id="77c3f-106">W tym artykule opisano przygotowania wymagane do tworzenia i konfigurowania usługi Menedżer StorSimple urządzenia przed udostępniania wirtualnego tablicy.</span><span class="sxs-lookup"><span data-stu-id="77c3f-106">This article describes the preparation required to create and configure your StorSimple Device Manager service prior to provisioning a virtual array.</span></span> <span data-ttu-id="77c3f-107">Ten artykuł zawiera również linki się lista kontrolna dotycząca konfiguracji wdrożenia i konfiguracji wymagań wstępnych.</span><span class="sxs-lookup"><span data-stu-id="77c3f-107">This article also links out to a deployment configuration checklist and configuration prerequisites.</span></span>

<span data-ttu-id="77c3f-108">Do ukończenia procesu instalacji i konfiguracji niezbędne są uprawnienia administratora.</span><span class="sxs-lookup"><span data-stu-id="77c3f-108">You need administrator privileges to complete the setup and configuration process.</span></span> <span data-ttu-id="77c3f-109">Firma Microsoft zaleca przejrzenie listy kontrolnej konfiguracji wdrożenia przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="77c3f-109">We recommend that you review the deployment configuration checklist before you begin.</span></span> <span data-ttu-id="77c3f-110">Przygotowanie portalu ma mniej niż 10 minut.</span><span class="sxs-lookup"><span data-stu-id="77c3f-110">The portal preparation takes less than 10 minutes.</span></span>

<span data-ttu-id="77c3f-111">Informacje zawarte w tym artykule dotyczą wdrażania tablic wirtualnego StorSimple w portalu Azure i Microsoft Azure dla instytucji rządowych chmury.</span><span class="sxs-lookup"><span data-stu-id="77c3f-111">The information published in this article applies to the deployment of StorSimple Virtual Arrays in the Azure portal and Microsoft Azure Government Cloud.</span></span>

### <a name="get-started"></a><span data-ttu-id="77c3f-112">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="77c3f-112">Get started</span></span>
<span data-ttu-id="77c3f-113">Przepływ pracy wdrażania składa się z przygotowanie portalu, udostępniania wirtualnego tablicy w środowisku zwirtualizowanym i zakończeniu instalacji.</span><span class="sxs-lookup"><span data-stu-id="77c3f-113">The deployment workflow consists of preparing the portal, provisioning a virtual array in your virtualized environment, and completing the setup.</span></span> <span data-ttu-id="77c3f-114">Aby rozpocząć pracę z wdrożeniem tablicy wirtualnego StorSimple jako serwer plików lub serwera iSCSI, należy odwoływać się do następujących zasobów tabelaryczne.</span><span class="sxs-lookup"><span data-stu-id="77c3f-114">To get started with the StorSimple Virtual Array deployment as a file server or an iSCSI server, you need to refer to the following tabulated resources.</span></span>

#### <a name="deployment-articles"></a><span data-ttu-id="77c3f-115">Wdrażania</span><span class="sxs-lookup"><span data-stu-id="77c3f-115">Deployment articles</span></span>

<span data-ttu-id="77c3f-116">Aby wdrożyć tablica wirtualnego StorSimple, można znaleźć w następujących artykułach w określonej kolejności.</span><span class="sxs-lookup"><span data-stu-id="77c3f-116">To deploy your StorSimple Virtual Array, refer to the following articles in the prescribed sequence.</span></span>

| **#** | <span data-ttu-id="77c3f-117">**W tym kroku**</span><span class="sxs-lookup"><span data-stu-id="77c3f-117">**In this step**</span></span> | <span data-ttu-id="77c3f-118">**Aby to zrobić...**</span><span class="sxs-lookup"><span data-stu-id="77c3f-118">**You do this …**</span></span> | <span data-ttu-id="77c3f-119">**I korzystać z tych dokumentów.**</span><span class="sxs-lookup"><span data-stu-id="77c3f-119">**And use these documents.**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="77c3f-120">1.</span><span class="sxs-lookup"><span data-stu-id="77c3f-120">1.</span></span> |<span data-ttu-id="77c3f-121">**Konfigurowanie portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="77c3f-121">**Set up the Azure portal**</span></span> |<span data-ttu-id="77c3f-122">Tworzenie i konfigurowanie usługi Menedżer StorSimple urządzenia przed inicjowania obsługi administracyjnej dla tablicy wirtualne StorSimple.</span><span class="sxs-lookup"><span data-stu-id="77c3f-122">Create and configure your StorSimple Device Manager service prior to provisioning a StorSimple Virtual Array.</span></span> |[<span data-ttu-id="77c3f-123">Przygotowanie portalu</span><span class="sxs-lookup"><span data-stu-id="77c3f-123">Prepare the portal</span></span>](storsimple-virtual-array-deploy1-portal-prep.md) |
| <span data-ttu-id="77c3f-124">2.</span><span class="sxs-lookup"><span data-stu-id="77c3f-124">2.</span></span> |<span data-ttu-id="77c3f-125">**Udostępnianie wirtualnych tablicy**</span><span class="sxs-lookup"><span data-stu-id="77c3f-125">**Provision the Virtual Array**</span></span> |<span data-ttu-id="77c3f-126">Dla funkcji Hyper-V udostępniania i Połącz z tablicą wirtualnego StorSimple na komputerze hosta z funkcją Hyper-V w systemie Windows Server 2012 R2, Windows Server 2012 lub Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="77c3f-126">For Hyper-V, provision and connect to a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <br></br> <br></br> <span data-ttu-id="77c3f-127">Dla VMware udostępniania i Połącz z tablicą wirtualnego StorSimple, na komputerze hosta z systemem VMware ESXi 5.5 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="77c3f-127">For VMware, provision and connect to a StorSimple Virtual Array on a host system running VMware ESXi 5.5 and above.</span></span><br></br> |[<span data-ttu-id="77c3f-128">Udostępnianie wirtualnych tablicy w funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="77c3f-128">Provision a virtual array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [<span data-ttu-id="77c3f-129">Udostępnianie wirtualnych tablicy w środowisku programu VMware</span><span class="sxs-lookup"><span data-stu-id="77c3f-129">Provision a virtual array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md) |
| <span data-ttu-id="77c3f-130">3.</span><span class="sxs-lookup"><span data-stu-id="77c3f-130">3.</span></span> |<span data-ttu-id="77c3f-131">**Konfigurowanie wirtualnego tablicy**</span><span class="sxs-lookup"><span data-stu-id="77c3f-131">**Set up the Virtual Array**</span></span> |<span data-ttu-id="77c3f-132">Dla serwera plików wykonywania początkowej konfiguracji, zarejestruj StorSimple serwera plików, a następnie przeprowadzić konfigurację urządzenia.</span><span class="sxs-lookup"><span data-stu-id="77c3f-132">For your file server, perform initial setup, register your StorSimple file server, and complete the device setup.</span></span> <span data-ttu-id="77c3f-133">Można następnie udostępnić udziałów SMB.</span><span class="sxs-lookup"><span data-stu-id="77c3f-133">You can then provision SMB shares.</span></span> <br></br> <br></br> <span data-ttu-id="77c3f-134">Dla serwera iSCSI wykonywania początkowej konfiguracji, Zarejestruj serwer iSCSI StorSimple i ukończyć instalację na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="77c3f-134">For your iSCSI server, perform initial setup, register your StorSimple iSCSI server, and complete the device setup.</span></span> <span data-ttu-id="77c3f-135">Następnie można alokować woluminy iSCSI.</span><span class="sxs-lookup"><span data-stu-id="77c3f-135">You can then provision iSCSI volumes.</span></span> |[<span data-ttu-id="77c3f-136">Konfigurowanie wirtualnego tablicy jako serwer plików</span><span class="sxs-lookup"><span data-stu-id="77c3f-136">Set up virtual array as file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[<span data-ttu-id="77c3f-137">Konfigurowanie wirtualnego tablicy jako serwer iSCSI</span><span class="sxs-lookup"><span data-stu-id="77c3f-137">Set up virtual array as iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md) |

<span data-ttu-id="77c3f-138">Teraz można rozpocząć konfigurowanie portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="77c3f-138">You can now begin to set up the Azure portal.</span></span>

## <a name="configuration-checklist"></a><span data-ttu-id="77c3f-139">Lista kontrolna dotycząca konfiguracji</span><span class="sxs-lookup"><span data-stu-id="77c3f-139">Configuration checklist</span></span>

<span data-ttu-id="77c3f-140">Lista kontrolna dotycząca konfiguracji opisano informacje, które należy zebrać przed rozpoczęciem konfigurowania oprogramowania na tablica wirtualnego StorSimple.</span><span class="sxs-lookup"><span data-stu-id="77c3f-140">The configuration checklist describes the information that you need to collect before you configure the software on your StorSimple Virtual Array.</span></span> <span data-ttu-id="77c3f-141">Te informacje wcześniejsze przygotowanie pomaga usprawnić proces wdrażania urządzenia StorSimple w środowisku.</span><span class="sxs-lookup"><span data-stu-id="77c3f-141">Preparing this information ahead of time helps streamline the process of deploying the StorSimple device in your environment.</span></span> <span data-ttu-id="77c3f-142">Zależności od tego, czy tablica wirtualne StorSimple jest wdrożona jako serwera plików lub serwera iSCSI, potrzebujesz jednego z następujących list kontrolnych.</span><span class="sxs-lookup"><span data-stu-id="77c3f-142">Depending upon whether your StorSimple Virtual Array is deployed as a file server or an iSCSI server, you need one of the following checklists.</span></span>

* <span data-ttu-id="77c3f-143">Pobierz [Lista kontrolna konfiguracji serwera plików tablicy wirtualnego StorSimple](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).</span><span class="sxs-lookup"><span data-stu-id="77c3f-143">Download the [StorSimple Virtual Array File Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).</span></span>
* <span data-ttu-id="77c3f-144">Pobierz [iSCSI tablicy wirtualnego StorSimple Lista kontrolna dotycząca konfiguracji serwera](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).</span><span class="sxs-lookup"><span data-stu-id="77c3f-144">Download the [StorSimple Virtual Array iSCSI Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77c3f-145">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="77c3f-145">Prerequisites</span></span>

<span data-ttu-id="77c3f-146">W tym miejscu możesz znaleźć wymagania wstępne dotyczące konfiguracji dla usługi Menedżer urządzeń StorSimple, tablica wirtualnego StorSimple i sieci centrum danych.</span><span class="sxs-lookup"><span data-stu-id="77c3f-146">Here you find the configuration prerequisites for your StorSimple Device Manager service, your StorSimple Virtual Array, and the datacenter network.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="77c3f-147">Usługa Menedżer urządzeń StorSimple</span><span class="sxs-lookup"><span data-stu-id="77c3f-147">For the StorSimple Device Manager service</span></span>

<span data-ttu-id="77c3f-148">Przed rozpoczęciem upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="77c3f-148">Before you begin, make sure that:</span></span>

* <span data-ttu-id="77c3f-149">Masz konto Microsoft z poświadczeniami dostępu.</span><span class="sxs-lookup"><span data-stu-id="77c3f-149">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="77c3f-150">Masz konto magazynu platformy Microsoft Azure z poświadczeniami dostępu.</span><span class="sxs-lookup"><span data-stu-id="77c3f-150">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="77c3f-151">Subskrypcja platformy Microsoft Azure powinno być włączone dla usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="77c3f-151">Your Microsoft Azure subscription should be enabled for StorSimple Device Manager service.</span></span>

### <a name="for-the-storsimple-virtual-array"></a><span data-ttu-id="77c3f-152">Dla tablicy wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="77c3f-152">For the StorSimple Virtual Array</span></span>

<span data-ttu-id="77c3f-153">Przed wdrożeniem wirtualnego tablicy, upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="77c3f-153">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="77c3f-154">Masz dostęp do systemu hosta funkcji Hyper-V w systemie Windows Server 2008 R2 lub nowszym lub VMware (ESXi 5.5 lub nowszego), które mogą być używane do udostępniania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="77c3f-154">You have access to a host system running Hyper-V on Windows Server 2008 R2 or later or VMware (ESXi 5.5 or later) that can be used to a provision a device.</span></span>
* <span data-ttu-id="77c3f-155">System hosta jest w stanie dedykować następujących zasobów, aby udostępnić wirtualny tablica:</span><span class="sxs-lookup"><span data-stu-id="77c3f-155">The host system is able to dedicate the following resources to provision your virtual array:</span></span>
  
  * <span data-ttu-id="77c3f-156">Co najmniej 4 rdzenie.</span><span class="sxs-lookup"><span data-stu-id="77c3f-156">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="77c3f-157">Co najmniej 8 GB pamięci RAM.</span><span class="sxs-lookup"><span data-stu-id="77c3f-157">At least 8 GB of RAM.</span></span> <span data-ttu-id="77c3f-158">Jeśli planujesz skonfigurować wirtualny tablicy jako serwer plików, 8 GB obsługuje 2 milionów plików.</span><span class="sxs-lookup"><span data-stu-id="77c3f-158">If you plan to configure the virtual array as file server, 8 GB supports 2 million files.</span></span> <span data-ttu-id="77c3f-159">Należy 16 GB pamięci RAM 2-4 miliony plików obsługi.</span><span class="sxs-lookup"><span data-stu-id="77c3f-159">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="77c3f-160">Jeden interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="77c3f-160">One network interface.</span></span>
  * <span data-ttu-id="77c3f-161">Dysk wirtualny 500 GB danych systemu.</span><span class="sxs-lookup"><span data-stu-id="77c3f-161">A 500 GB virtual disk for system data.</span></span>

### <a name="for-the-datacenter-network"></a><span data-ttu-id="77c3f-162">Dla sieci centrum danych</span><span class="sxs-lookup"><span data-stu-id="77c3f-162">For the datacenter network</span></span>

<span data-ttu-id="77c3f-163">Przed rozpoczęciem upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="77c3f-163">Before you begin, make sure that:</span></span>

* <span data-ttu-id="77c3f-164">Sieć w centrum danych jest skonfigurowany zgodnie z wymaganiami sieci dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="77c3f-164">The network in your datacenter is configured as per the networking requirements for your StorSimple device.</span></span> <span data-ttu-id="77c3f-165">Aby uzyskać więcej informacji, zobacz [wymagania systemowe tablicy wirtualnego StorSimple](storsimple-ova-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="77c3f-165">For more information, see the [StorSimple Virtual Array System Requirements](storsimple-ova-system-requirements.md).</span></span>
* <span data-ttu-id="77c3f-166">Tablica wirtualnego StorSimple ma dedykowany 5 MB/s przepustowości połączenia z Internetem (lub więcej) dostępne przez cały czas.</span><span class="sxs-lookup"><span data-stu-id="77c3f-166">Your StorSimple Virtual Array has a dedicated 5 Mbps Internet bandwidth (or more) available at all times.</span></span> <span data-ttu-id="77c3f-167">Przepustowość nie powinien być współużytkowany z innych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77c3f-167">This bandwidth should not be shared with any other applications.</span></span>

## <a name="step-by-step-preparation"></a><span data-ttu-id="77c3f-168">Krok przygotowania</span><span class="sxs-lookup"><span data-stu-id="77c3f-168">Step-by-step preparation</span></span>

<span data-ttu-id="77c3f-169">Poniższe instrukcje krok po kroku umożliwia przygotowanie portalem usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="77c3f-169">Use the following step-by-step instructions to prepare your portal for the StorSimple Device Manager service.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="77c3f-170">Krok 1. Tworzenie nowej usługi</span><span class="sxs-lookup"><span data-stu-id="77c3f-170">Step 1: Create a new service</span></span>

<span data-ttu-id="77c3f-171">Jedno wystąpienie usługi Menedżer StorSimple urządzeń można zarządzać wiele tablic wirtualne StorSimple.</span><span class="sxs-lookup"><span data-stu-id="77c3f-171">A single instance of the StorSimple Device Manager service can manage multiple StorSimple Virtual Arrays.</span></span> <span data-ttu-id="77c3f-172">Wykonaj poniższe kroki, aby utworzyć wystąpienie usługi Menedżer urządzeń StorSimple.</span><span class="sxs-lookup"><span data-stu-id="77c3f-172">Perform the following steps to create an instance of the StorSimple Device Manager service.</span></span> <span data-ttu-id="77c3f-173">Jeśli masz istniejącą usługę Menedżer StorSimple urządzenia do zarządzania z macierzami wirtualnego, Pomiń ten krok i przejdź do [krok 2: pobieranie klucza rejestracji usługi](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="77c3f-173">If you have an existing StorSimple Device Manager service to manage your virtual arrays, skip this step and go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> <span data-ttu-id="77c3f-174">Jeśli nie włączono automatycznego tworzenia konta magazynu przy użyciu usługi, po pomyślnym utworzeniu usługi musisz utworzyć co najmniej jedno konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="77c3f-174">If you did not enable the automatic creation of a storage account with your service, you will need to create at least one storage account after you have successfully created a service.</span></span>
> 
> * <span data-ttu-id="77c3f-175">Jeśli nie utworzono automatycznie konta magazynu, przejdź do kroku [Konfigurowanie nowego konta magazynu dla usługi](#optional-step-configure-a-new-storage-account-for-the-service) w celu uzyskania szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="77c3f-175">If you did not create a storage account automatically, go to [Configure a new storage account for the service](#optional-step-configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="77c3f-176">Jeśli włączono automatyczne tworzenie konta magazynu, przejdź do części [Krok 2. Pobieranie klucza rejestracji usługi](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="77c3f-176">If you enabled the automatic creation of a storage account, go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span>
> 
> 

## <a name="step-2-get-the-service-registration-key"></a><span data-ttu-id="77c3f-177">Krok 2. Pobieranie klucza rejestracji usługi</span><span class="sxs-lookup"><span data-stu-id="77c3f-177">Step 2: Get the service registration key</span></span>

<span data-ttu-id="77c3f-178">Po skonfigurowaniu i uruchomieniu usługi Menedżer urządzeń StorSimple musisz pobrać klucz rejestracji usługi.</span><span class="sxs-lookup"><span data-stu-id="77c3f-178">After the StorSimple Device Manager service is up and running, you will need to get the service registration key.</span></span> <span data-ttu-id="77c3f-179">Ten klucz służy do rejestrowania urządzenia StorSimple i łączenia go z usługą.</span><span class="sxs-lookup"><span data-stu-id="77c3f-179">This key is used to register and connect your StorSimple device with the service.</span></span>

<span data-ttu-id="77c3f-180">Wykonaj poniższe kroki w [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="77c3f-180">Perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> <span data-ttu-id="77c3f-181">Klucz rejestracji usługi służy do rejestrowania wszystkich urządzeń Menedżer urządzeń StorSimple, które należy zarejestrować przy użyciu usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="77c3f-181">The service registration key is used to register all the StorSimple Device Manager devices that need to register with your StorSimple Device Manager service.</span></span>
> 
> 

## <a name="step-3-download-the-virtual-array-image"></a><span data-ttu-id="77c3f-182">Krok 3: Pobierz obraz wirtualnego tablicy</span><span class="sxs-lookup"><span data-stu-id="77c3f-182">Step 3: Download the virtual array image</span></span>

<span data-ttu-id="77c3f-183">Po klucz rejestracji usługi, będzie konieczne pobranie obrazu odpowiednie tablicy wirtualnego do udostępniania wirtualnego tablicy w systemie hosta.</span><span class="sxs-lookup"><span data-stu-id="77c3f-183">After you have the service registration key, you will need to download the appropriate virtual array image to provision a virtual array on your host system.</span></span> <span data-ttu-id="77c3f-184">Obrazy wirtualnego tablicy są zależne od systemu operacyjnego, można pobrać ze strony szybkiego startu w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="77c3f-184">The virtual array images are operating system specific and can be downloaded from the Quick Start page in the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77c3f-185">Oprogramowanie działające na tablicy wirtualnego StorSimple można używać tylko w usłudze Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="77c3f-185">The software running on the StorSimple Virtual Array may only be used with the StorSimple Device Manager service.</span></span>
> 
> 

<span data-ttu-id="77c3f-186">Wykonaj poniższe kroki w [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="77c3f-186">Perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="to-get-the-virtual-array-image"></a><span data-ttu-id="77c3f-187">Do pobrania obrazu wirtualnego tablicy</span><span class="sxs-lookup"><span data-stu-id="77c3f-187">To get the virtual array image</span></span>

1. <span data-ttu-id="77c3f-188">Zaloguj się do [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="77c3f-188">Sign into the [Azure portal](https://portal.azure.com/).</span></span> 
2. <span data-ttu-id="77c3f-189">W portalu Azure kliknij **Przeglądaj > menedżerów urządzenia StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="77c3f-189">In the Azure portal, click **Browse > StorSimple Device Managers**.</span></span>
3. <span data-ttu-id="77c3f-190">Wybierz istniejącą usługę Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="77c3f-190">Select an existing StorSimple Device Manager service.</span></span> <span data-ttu-id="77c3f-191">W **Menedżera urządzeń StorSimple** bloku, kliknij przycisk **Szybki Start**.</span><span class="sxs-lookup"><span data-stu-id="77c3f-191">In the **StorSimple Device Manager** blade, click **Quick Start**.</span></span> 
4. <span data-ttu-id="77c3f-192">Kliknij link odpowiadający obrazu, który ma zostać pobrana z Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="77c3f-192">Click the link corresponding to the image that you want to download from the Microsoft Download Center.</span></span> <span data-ttu-id="77c3f-193">Pliki są około 4.8 GB.</span><span class="sxs-lookup"><span data-stu-id="77c3f-193">The image files are approximately 4.8 GB.</span></span>
   
   * <span data-ttu-id="77c3f-194">VHDX dla funkcji Hyper-V w systemie Windows Server 2012 lub nowszym</span><span class="sxs-lookup"><span data-stu-id="77c3f-194">VHDX for Hyper-V on Windows Server 2012 and later</span></span>
   * <span data-ttu-id="77c3f-195">Wirtualnego dysku twardego funkcji Hyper-v w systemie Windows Server 2008 R2 lub nowszym</span><span class="sxs-lookup"><span data-stu-id="77c3f-195">VHD for Hyper-V on Windows Server 2008 R2 and later</span></span>
   * <span data-ttu-id="77c3f-196">VMDK VMWare ESXi 5.5 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="77c3f-196">VMDK for VMWare ESXi 5.5 and later</span></span>
5. <span data-ttu-id="77c3f-197">Pobierz i rozpakuj plik lokalny dysk, co Zanotuj którym znajduje się plik rozpakowane.</span><span class="sxs-lookup"><span data-stu-id="77c3f-197">Download and unzip the file to a local drive, making a note of where the unzipped file is located.</span></span>

## <a name="optional-step-configure-a-new-storage-account-for-the-service"></a><span data-ttu-id="77c3f-198">Krok opcjonalny: Konfigurowanie nowego konta magazynu dla usługi</span><span class="sxs-lookup"><span data-stu-id="77c3f-198">Optional step: Configure a new storage account for the service</span></span>

<span data-ttu-id="77c3f-199">Ten krok jest opcjonalny i należy wykonać tylko wtedy, gdy nie włączono automatycznego tworzenia konta magazynu z usługą.</span><span class="sxs-lookup"><span data-stu-id="77c3f-199">This step is optional and should be performed only if you did not enable the automatic creation of a storage account with your service.</span></span>

<span data-ttu-id="77c3f-200">Jeśli musisz utworzyć konto magazynu platformy Azure w innym regionie, zobacz [jak utworzyć konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="77c3f-200">If you need to create an Azure storage account in a different region, see [How to create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for step-by-step instructions.</span></span>

<span data-ttu-id="77c3f-201">Wykonaj poniższe kroki w [portalu Azure](https://ms.portal.azure.com/) na stronie usługi Menedżer StorSimple urządzenia można dodać istniejącego konta magazynu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="77c3f-201">Perform the following steps in the [Azure portal](https://ms.portal.azure.com/) on the StorSimple Device Manager service page to add an existing Microsoft Azure storage account.</span></span>

#### <a name="to-add-a-storage-account-credential-that-has-the-same-azure-subscription-as-the-device-manager-service"></a><span data-ttu-id="77c3f-202">Aby dodać poświadczeniami konta magazynu, które mają tej samej subskrypcji platformy Azure jako usługa Menedżera urządzeń</span><span class="sxs-lookup"><span data-stu-id="77c3f-202">To add a storage account credential that has the same Azure subscription as the Device Manager service</span></span>

1. <span data-ttu-id="77c3f-203">Przejdź do usługi Menedżera urządzeń, wybierz opcję i kliknij ją dwukrotnie.</span><span class="sxs-lookup"><span data-stu-id="77c3f-203">Navigate to your Device Manager service, select and double-click it.</span></span> <span data-ttu-id="77c3f-204">Spowoduje to otwarcie **omówienie** bloku.</span><span class="sxs-lookup"><span data-stu-id="77c3f-204">This opens the **Overview** blade.</span></span>
2. <span data-ttu-id="77c3f-205">Wybierz **poświadczeń konta magazynu** w **konfiguracji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="77c3f-205">Select **Storage account credentials** within the **Configuration** section.</span></span>
3. <span data-ttu-id="77c3f-206">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="77c3f-206">Click **Add**.</span></span>
4. <span data-ttu-id="77c3f-207">W **dodawania konta magazynu** blok, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="77c3f-207">In the **Add a storage account** blade, do the following:</span></span>
   
    1. <span data-ttu-id="77c3f-208">Aby uzyskać **subskrypcji**, wybierz pozycję **bieżącego**.</span><span class="sxs-lookup"><span data-stu-id="77c3f-208">For **Subscription**, select **Current**.</span></span>
   
    2. <span data-ttu-id="77c3f-209">Podaj nazwę konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="77c3f-209">Provide the name of your Azure storage account.</span></span>
   
    3. <span data-ttu-id="77c3f-210">Wybierz **włączyć** można utworzyć bezpiecznego kanału komunikacji sieciowej między urządzeniem StorSimple i chmury.</span><span class="sxs-lookup"><span data-stu-id="77c3f-210">Select **Enable** to create a secure channel for network communication between your StorSimple device and the cloud.</span></span> <span data-ttu-id="77c3f-211">Wybierz **wyłączyć** tylko wtedy, gdy pracujesz w chmurze prywatnej.</span><span class="sxs-lookup"><span data-stu-id="77c3f-211">Select **Disable** only if you are operating within a private cloud.</span></span>
   
    4. <span data-ttu-id="77c3f-212">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="77c3f-212">Click **Add**.</span></span> <span data-ttu-id="77c3f-213">Użytkownik jest powiadamiany po pomyślnym utworzeniu konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="77c3f-213">You are notified after the storage account is successfully created.</span></span><br></br>
   
     ![Dodawanie istniejących poświadczeń dla konta magazynu](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a><span data-ttu-id="77c3f-215">Następny krok</span><span class="sxs-lookup"><span data-stu-id="77c3f-215">Next step</span></span>

<span data-ttu-id="77c3f-216">Następnym krokiem jest do udostępnienia maszyny wirtualnej dla macierzy wirtualne StorSimple.</span><span class="sxs-lookup"><span data-stu-id="77c3f-216">The next step is to provision a virtual machine for your StorSimple Virtual Array.</span></span> <span data-ttu-id="77c3f-217">W zależności od systemu operacyjnego hosta Zobacz szczegółowe instrukcje w:</span><span class="sxs-lookup"><span data-stu-id="77c3f-217">Depending on your host operating system, see the detailed instructions in:</span></span>

* [<span data-ttu-id="77c3f-218">Zapewnij tablicą wirtualnego StorSimple w funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="77c3f-218">Provision a StorSimple Virtual Array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [<span data-ttu-id="77c3f-219">Zapewnij tablicą wirtualnego StorSimple w środowisku programu VMware</span><span class="sxs-lookup"><span data-stu-id="77c3f-219">Provision a StorSimple Virtual Array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md)

