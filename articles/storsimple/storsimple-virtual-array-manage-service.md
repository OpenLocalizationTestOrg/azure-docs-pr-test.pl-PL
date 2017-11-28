---
title: "aaaDeploy usługi Menedżer urządzenia StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak toocreate i delete hello usługi Menedżer urządzenia StorSimple w hello portalu Azure, a w tym artykule opisano, jak toomanage hello klucz rejestracji usługi."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="e2a2f-103">Wdrażanie usługi Menedżer StorSimple urządzenia hello tablicy wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="e2a2f-103">Deploy hello StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="e2a2f-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e2a2f-104">Overview</span></span>

<span data-ttu-id="e2a2f-105">Hello usługi Menedżer StorSimple urządzenie działa w systemie Microsoft Azure i łączy toomultiple urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-105">hello StorSimple Device Manager service runs in Microsoft Azure and connects toomultiple StorSimple devices.</span></span> <span data-ttu-id="e2a2f-106">Po utworzeniu usługi hello, można użyć toomanage hello urządzenia z hello Microsoft Azure portalu działającego w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-106">After you create hello service, you can use it toomanage hello devices from hello Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="e2a2f-107">Dzięki temu toomonitor usługi wszystkie urządzenia hello, które są połączone toohello Menedżera urządzeń StorSimple z jednym centralnym miejscu, w tym samym minimalizując nakładu prac administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-107">This allows you toomonitor all hello devices that are connected toohello StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="e2a2f-108">Witaj typowe zadania pokrewne tooa usługi Menedżer StorSimple urządzenia są:</span><span class="sxs-lookup"><span data-stu-id="e2a2f-108">hello common tasks related tooa StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="e2a2f-109">Tworzenie usługi</span><span class="sxs-lookup"><span data-stu-id="e2a2f-109">Create a service</span></span>
* <span data-ttu-id="e2a2f-110">Usuwanie usługi</span><span class="sxs-lookup"><span data-stu-id="e2a2f-110">Delete a service</span></span>
* <span data-ttu-id="e2a2f-111">Pobierz klucz rejestracji usługi hello</span><span class="sxs-lookup"><span data-stu-id="e2a2f-111">Get hello service registration key</span></span>
* <span data-ttu-id="e2a2f-112">Wygeneruj ponownie klucz rejestracji usługi hello</span><span class="sxs-lookup"><span data-stu-id="e2a2f-112">Regenerate hello service registration key</span></span>

<span data-ttu-id="e2a2f-113">W tym samouczku opisano, jak tooperform z hello poprzednich zadań.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-113">This tutorial describes how tooperform each of hello preceding tasks.</span></span> <span data-ttu-id="e2a2f-114">Hello informacje zawarte w tym artykule jest stosowane tylko tablice wirtualnego tooStorSimple.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-114">hello information contained in this article is applicable only tooStorSimple Virtual Arrays.</span></span> <span data-ttu-id="e2a2f-115">Aby uzyskać więcej informacji na serii StorSimple 8000 Przejdź zbyt[wdrożyć usługę Menedżer StorSimple](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="e2a2f-115">For more information on StorSimple 8000 series, go too[deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="e2a2f-116">Tworzenie usługi</span><span class="sxs-lookup"><span data-stu-id="e2a2f-116">Create a service</span></span>

<span data-ttu-id="e2a2f-117">toocreate usługi należy toohave:</span><span class="sxs-lookup"><span data-stu-id="e2a2f-117">toocreate a service, you need toohave:</span></span>

* <span data-ttu-id="e2a2f-118">Subskrypcja z umową Enterprise</span><span class="sxs-lookup"><span data-stu-id="e2a2f-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="e2a2f-119">Aktywne konto magazynu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e2a2f-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="e2a2f-120">Witaj informacji dotyczących rozliczeń, która służy do zarządzania dostępem</span><span class="sxs-lookup"><span data-stu-id="e2a2f-120">hello billing information that is used for access management</span></span>

<span data-ttu-id="e2a2f-121">Możesz również toogenerate konta magazynu podczas tworzenia usługi hello.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-121">You can also choose toogenerate a storage account when you create hello service.</span></span>

<span data-ttu-id="e2a2f-122">Jednej usługi można zarządzać wieloma urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="e2a2f-123">Jednak urządzenia nie może obejmować wiele usług.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="e2a2f-124">Duże przedsiębiorstwa mogą być wielu toowork wystąpienia usługi z różnych subskrypcji, organizacji lub nawet miejsc wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-124">A large enterprise can have multiple service instances toowork with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="e2a2f-125">Należy oddzielnego wystąpienia Menedżera urządzeń StorSimple usługi toomanage StorSimple 8000 serii urządzeń i tablice wirtualne StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-125">You need separate instances of StorSimple Device Manager service toomanage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="e2a2f-126">Wykonaj następujące kroki toocreate usługi hello.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-126">Perform hello following steps toocreate a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="e2a2f-127">Usuwanie usługi</span><span class="sxs-lookup"><span data-stu-id="e2a2f-127">Delete a service</span></span>

<span data-ttu-id="e2a2f-128">Przed usunięciem usługi, upewnij się, że żadnych podłączonych urządzeń używają go.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="e2a2f-129">Jeśli usługa hello jest używany, Dezaktywuj hello podłączone urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-129">If hello service is in use, deactivate hello connected devices.</span></span> <span data-ttu-id="e2a2f-130">Witaj dezaktywować operacji sever hello połączenie między hello urządzeń i usług hello, ale zachować dane urządzenie hello w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-130">hello deactivate operation will sever hello connection between hello device and hello service, but preserve hello device data in hello cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2a2f-131">Po usunięciu usługi hello operacji nie można cofnąć.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-131">After a service is deleted, hello operation cannot be reversed.</span></span> <span data-ttu-id="e2a2f-132">Dowolne urządzenie, które zostało przy użyciu usługi hello należy toobe resetowanie, zanim będzie można go używać z inną usługą do ustawień fabrycznych.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-132">Any device that was using hello service will need toobe factory reset before it can be used with another service.</span></span> <span data-ttu-id="e2a2f-133">W tym scenariuszu dane lokalne powitania na powitania urządzenia, a także konfiguracji hello zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-133">In this scenario, hello local data on hello device, as well as hello configuration, will be lost.</span></span>
 

<span data-ttu-id="e2a2f-134">Wykonaj następujące kroki toodelete usługi hello.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-134">Perform hello following steps toodelete a service.</span></span>

#### <a name="toodelete-a-service"></a><span data-ttu-id="e2a2f-135">toodelete usługi</span><span class="sxs-lookup"><span data-stu-id="e2a2f-135">toodelete a service</span></span>

1. <span data-ttu-id="e2a2f-136">Przejdź za**wszystkie zasoby**.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-136">Go too**All resources**.</span></span> <span data-ttu-id="e2a2f-137">Wyszukiwanie usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="e2a2f-138">Wybierz usługę hello, że chcesz toodelete.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-138">Select hello service that you wish toodelete.</span></span>
   
    ![Wybierz toodelete usługi](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="e2a2f-140">Przejdź tooensure pulpitu nawigacyjnego usługi tooyour istnieją nie urządzeń połączonych toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-140">Go tooyour service dashboard tooensure there are no devices connected toohello service.</span></span> <span data-ttu-id="e2a2f-141">Jeśli nie ma żadnych urządzeń zarejestrowanych w usłudze tej usługi, pojawi się także efekt toohello komunikat transparentu.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-141">If there are no devices registered with this service, you will also see a banner message toohello effect.</span></span> <span data-ttu-id="e2a2f-142">Kliknij polecenie **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-142">Click **Delete**.</span></span>
   
    ![Usuwanie usługi](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="e2a2f-144">Po wyświetleniu monitu o potwierdzenie, kliknij przycisk **tak** hello powiadomienia o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-144">When prompted for confirmation, click **Yes** in hello confirmation notification.</span></span> 
   
    ![Potwierdź usunięcie usługi](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="e2a2f-146">Może upłynąć kilka minut, aż toobe usługi hello usunięte.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-146">It may take a few minutes for hello service toobe deleted.</span></span> <span data-ttu-id="e2a2f-147">Po hello usługa jest pomyślnie usunięte, otrzymasz powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-147">After hello service is successfully deleted, you will be notified.</span></span>
   
    ![Usunięcie usługi powiodło się](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="e2a2f-149">Lista Hello usług zostanie odświeżona.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-149">hello list of services will be refreshed.</span></span>

 ![Zaktualizowaną listę usług](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a><span data-ttu-id="e2a2f-151">Pobierz klucz rejestracji usługi hello</span><span class="sxs-lookup"><span data-stu-id="e2a2f-151">Get hello service registration key</span></span>
<span data-ttu-id="e2a2f-152">Po pomyślnym utworzeniu usługi należy tooregister urządzenie StorSimple przy użyciu usługi hello.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-152">After you have successfully created a service, you will need tooregister your StorSimple device with hello service.</span></span> <span data-ttu-id="e2a2f-153">tooregister pierwszego urządzenia StorSimple, będzie konieczne hello klucz rejestracji usługi.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-153">tooregister your first StorSimple device, you will need hello service registration key.</span></span> <span data-ttu-id="e2a2f-154">tooregister dodatkowych urządzeń z istniejącej usługi StorSimple, konieczne będzie zarówno klucz rejestracji hello, jak i klucz szyfrowania danych usługi hello, (który jest generowany na powitania pierwszego urządzenia podczas rejestracji).</span><span class="sxs-lookup"><span data-stu-id="e2a2f-154">tooregister additional devices with an existing StorSimple service, you will need both hello registration key and hello service data encryption key (which is generated on hello first device during registration).</span></span> <span data-ttu-id="e2a2f-155">Aby uzyskać więcej informacji na temat klucza szyfrowania danych usługi hello, zobacz [zabezpieczenia usługi StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="e2a2f-155">For more information about hello service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="e2a2f-156">Klucz rejestracji hello można uzyskać, uzyskując dostęp do hello **klucze** bloku dla usługi.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-156">You can get hello registration key by accessing hello **Keys** blade for your service.</span></span>

<span data-ttu-id="e2a2f-157">Wykonaj powitania po klucz rejestracji usługi hello tooget czynności.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-157">Perform hello following steps tooget hello service registration key.</span></span>

#### <a name="tooget-hello-service-registration-key"></a><span data-ttu-id="e2a2f-158">klucz rejestracji usługi hello tooget</span><span class="sxs-lookup"><span data-stu-id="e2a2f-158">tooget hello service registration key</span></span>
1. <span data-ttu-id="e2a2f-159">W hello **Menedżera urządzeń StorSimple** bloku Przejdź zbyt**zarządzania &gt;**  **klucze**.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-159">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![Blok Klucze](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="e2a2f-161">W hello **klucze** zostanie wyświetlony blok, klucz rejestracji usługi.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-161">In hello **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="e2a2f-162">Skopiuj klucz rejestracji hello za pomocą ikony kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-162">Copy hello registration key using hello copy icon.</span></span> 

<span data-ttu-id="e2a2f-163">Klucz rejestracji usługi hello należy przechowywać w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-163">Keep hello service registration key in a safe location.</span></span> <span data-ttu-id="e2a2f-164">Należy tego klucza, a także klucz szyfrowania danych usługi hello tooregister dodatkowych urządzeń z tą usługą.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-164">You will need this key, as well as hello service data encryption key, tooregister additional devices with this service.</span></span> <span data-ttu-id="e2a2f-165">Po uzyskaniu klucza rejestracji usługi hello, konieczne będzie tooconfigure urządzenia za pośrednictwem hello środowiska Windows PowerShell dla StorSimple interfejsu.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-165">After obtaining hello service registration key, you will need tooconfigure your device through hello Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-hello-service-registration-key"></a><span data-ttu-id="e2a2f-166">Wygeneruj ponownie klucz rejestracji usługi hello</span><span class="sxs-lookup"><span data-stu-id="e2a2f-166">Regenerate hello service registration key</span></span>
<span data-ttu-id="e2a2f-167">Należy tooregenerate klucz rejestracji usługi, jeśli są wymagane tooperform obrotu klucza lub jeśli zmieniono hello listy administratorów usługi.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-167">You will need tooregenerate a service registration key if you are required tooperform key rotation or if hello list of service administrators has changed.</span></span> <span data-ttu-id="e2a2f-168">Podczas ponownego generowania klucza hello, nowy klucz hello jest używany tylko do celów rejestracji kolejnych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-168">When you regenerate hello key, hello new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="e2a2f-169">przez ten proces nie dotyczy to urządzeń Hello, które zostały już zarejestrowane.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-169">hello devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="e2a2f-170">Wykonaj hello następujące kroki tooregenerate klucz rejestracji usługi.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-170">Perform hello following steps tooregenerate a service registration key.</span></span>

#### <a name="tooregenerate-hello-service-registration-key"></a><span data-ttu-id="e2a2f-171">klucz rejestracji usługi hello tooregenerate</span><span class="sxs-lookup"><span data-stu-id="e2a2f-171">tooregenerate hello service registration key</span></span>
1. <span data-ttu-id="e2a2f-172">W hello **Menedżera urządzeń StorSimple** bloku Przejdź zbyt**zarządzania &gt;**  **klucze**.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-172">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![Blok Klucze](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="e2a2f-174">W hello **klucze** bloku, kliknij przycisk **ponownie wygenerować**.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-174">In hello **Keys** blade, click **Regenerate**.</span></span>
   
   ![Kliknij przycisk regenerate](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="e2a2f-176">W hello **klucz rejestracji usługi Regenerate** bloku, przejrzyj hello Akcja wymagana, gdy hello klucze są generowane.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-176">In hello **Regenerate service registration key** blade, review hello action required when hello keys are regenerated.</span></span> <span data-ttu-id="e2a2f-177">Wszystkie urządzenia kolejnych hello, które są zarejestrowane z tą usługą użyje hello nowy klucz rejestracji.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-177">All hello subsequent devices that are registered with this service will use hello new registration key.</span></span> <span data-ttu-id="e2a2f-178">Kliknij przycisk **ponownie wygenerować** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-178">Click **Regenerate** tooconfirm.</span></span> <span data-ttu-id="e2a2f-179">Po zakończeniu rejestracji hello, otrzymasz powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-179">You will be notified after hello registration is complete.</span></span>
   
   ![Potwierdź klucz regenerate](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="e2a2f-181">Pojawi się nowy klucz rejestracji usługi.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-181">A new service registration key will appear.</span></span>
   
    ![Potwierdź klucz regenerate](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="e2a2f-183">Skopiuj ten klucz i zapisać go do rejestracji żadnych nowych urządzeń z tą usługą.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2a2f-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e2a2f-184">Next steps</span></span>
* <span data-ttu-id="e2a2f-185">Dowiedz się, jak za[wprowadzenie](storsimple-virtual-array-deploy1-portal-prep.md) tablicą wirtualne StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e2a2f-185">Learn how too[get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="e2a2f-186">Dowiedz się, jak za[administrowania urządzenia StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="e2a2f-186">Learn how too[administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

