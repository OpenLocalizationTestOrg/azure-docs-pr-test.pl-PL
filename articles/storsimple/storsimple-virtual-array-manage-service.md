---
title: "Wdrażanie usługi Menedżer urządzenia StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tworzyć i usuwać usługi Menedżer StorSimple urządzenia w portalu Azure i opisano sposób zarządzania klucz rejestracji usługi."
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
ms.openlocfilehash: 1881a0625b107ae1a90e5b772f5296a4d728973d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-the-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="5c121-103">Wdrażanie usługi Menedżer StorSimple urządzenia dla tablicy wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="5c121-103">Deploy the StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="5c121-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="5c121-104">Overview</span></span>

<span data-ttu-id="5c121-105">Usługa Menedżera urządzeń StorSimple działa na platformie Microsoft Azure i łączy się z wieloma urządzeniami StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5c121-105">The StorSimple Device Manager service runs in Microsoft Azure and connects to multiple StorSimple devices.</span></span> <span data-ttu-id="5c121-106">Po utworzeniu usługi musisz służy do zarządzania urządzeniami z portalu Microsoft Azure działającego w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="5c121-106">After you create the service, you can use it to manage the devices from the Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="5c121-107">Dzięki temu można monitorować wszystkie urządzenia, które są połączone z usługą Menedżera urządzeń StorSimple z jednym centralnym miejscu, w tym samym minimalizując nakładu prac administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="5c121-107">This allows you to monitor all the devices that are connected to the StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="5c121-108">Typowe zadania związane z usługą Menedżera urządzeń StorSimple są:</span><span class="sxs-lookup"><span data-stu-id="5c121-108">The common tasks related to a StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="5c121-109">Tworzenie usługi</span><span class="sxs-lookup"><span data-stu-id="5c121-109">Create a service</span></span>
* <span data-ttu-id="5c121-110">Usuwanie usługi</span><span class="sxs-lookup"><span data-stu-id="5c121-110">Delete a service</span></span>
* <span data-ttu-id="5c121-111">Pobieranie klucza rejestracji usługi</span><span class="sxs-lookup"><span data-stu-id="5c121-111">Get the service registration key</span></span>
* <span data-ttu-id="5c121-112">Wygeneruj ponownie klucz rejestracji usługi</span><span class="sxs-lookup"><span data-stu-id="5c121-112">Regenerate the service registration key</span></span>

<span data-ttu-id="5c121-113">W tym samouczku opisano sposób wykonywania wszystkich poprzednich zadań.</span><span class="sxs-lookup"><span data-stu-id="5c121-113">This tutorial describes how to perform each of the preceding tasks.</span></span> <span data-ttu-id="5c121-114">Informacje zawarte w tym artykule ma zastosowanie tylko do tablic wirtualne StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5c121-114">The information contained in this article is applicable only to StorSimple Virtual Arrays.</span></span> <span data-ttu-id="5c121-115">Aby uzyskać więcej informacji dotyczących serii StorSimple 8000, przejdź do [wdrożyć usługę Menedżer StorSimple](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="5c121-115">For more information on StorSimple 8000 series, go to [deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="5c121-116">Tworzenie usługi</span><span class="sxs-lookup"><span data-stu-id="5c121-116">Create a service</span></span>

<span data-ttu-id="5c121-117">Aby utworzyć usługę, musi być:</span><span class="sxs-lookup"><span data-stu-id="5c121-117">To create a service, you need to have:</span></span>

* <span data-ttu-id="5c121-118">Subskrypcja z umową Enterprise</span><span class="sxs-lookup"><span data-stu-id="5c121-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="5c121-119">Aktywne konto magazynu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5c121-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="5c121-120">Informacji dotyczących rozliczeń, która służy do zarządzania dostępem</span><span class="sxs-lookup"><span data-stu-id="5c121-120">The billing information that is used for access management</span></span>

<span data-ttu-id="5c121-121">Można także wygenerować konta magazynu podczas tworzenia usługi.</span><span class="sxs-lookup"><span data-stu-id="5c121-121">You can also choose to generate a storage account when you create the service.</span></span>

<span data-ttu-id="5c121-122">Jednej usługi można zarządzać wieloma urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="5c121-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="5c121-123">Jednak urządzenia nie może obejmować wiele usług.</span><span class="sxs-lookup"><span data-stu-id="5c121-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="5c121-124">Duże przedsiębiorstwa mogą być wiele wystąpień usługi do pracy z różnych subskrypcji, organizacji lub nawet miejsc wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="5c121-124">A large enterprise can have multiple service instances to work with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="5c121-125">Należy oddzielnego wystąpienia usługi Menedżer urządzenia StorSimple do zarządzania urządzeń z serii StorSimple 8000 i tablice wirtualne StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5c121-125">You need separate instances of StorSimple Device Manager service to manage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="5c121-126">Wykonaj poniższe kroki, aby utworzyć usługę.</span><span class="sxs-lookup"><span data-stu-id="5c121-126">Perform the following steps to create a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="5c121-127">Usuwanie usługi</span><span class="sxs-lookup"><span data-stu-id="5c121-127">Delete a service</span></span>

<span data-ttu-id="5c121-128">Przed usunięciem usługi, upewnij się, że żadnych podłączonych urządzeń używają go.</span><span class="sxs-lookup"><span data-stu-id="5c121-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="5c121-129">Jeśli usługa jest w użyciu, Dezaktywuj połączonych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5c121-129">If the service is in use, deactivate the connected devices.</span></span> <span data-ttu-id="5c121-130">Operacja Dezaktywuj sever połączenia między urządzeniem i usługi, ale zachować dane urządzenie w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5c121-130">The deactivate operation will sever the connection between the device and the service, but preserve the device data in the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c121-131">Po usunięciu usługi nie można cofnąć operacji.</span><span class="sxs-lookup"><span data-stu-id="5c121-131">After a service is deleted, the operation cannot be reversed.</span></span> <span data-ttu-id="5c121-132">Dowolne urządzenie, które zostało przy użyciu usługi będzie trzeba resetowanie, zanim będzie można go używać z inną usługą do ustawień fabrycznych.</span><span class="sxs-lookup"><span data-stu-id="5c121-132">Any device that was using the service will need to be factory reset before it can be used with another service.</span></span> <span data-ttu-id="5c121-133">W tym scenariuszu dane lokalne na urządzeniu, a także konfiguracji, zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="5c121-133">In this scenario, the local data on the device, as well as the configuration, will be lost.</span></span>
 

<span data-ttu-id="5c121-134">Wykonaj poniższe kroki, aby usunąć usługę.</span><span class="sxs-lookup"><span data-stu-id="5c121-134">Perform the following steps to delete a service.</span></span>

#### <a name="to-delete-a-service"></a><span data-ttu-id="5c121-135">Aby usunąć usługę</span><span class="sxs-lookup"><span data-stu-id="5c121-135">To delete a service</span></span>

1. <span data-ttu-id="5c121-136">Przejdź do **wszystkie zasoby**.</span><span class="sxs-lookup"><span data-stu-id="5c121-136">Go to **All resources**.</span></span> <span data-ttu-id="5c121-137">Wyszukiwanie usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5c121-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="5c121-138">Wybierz usługi, który chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="5c121-138">Select the service that you wish to delete.</span></span>
   
    ![Wybierz usługę do usunięcia](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="5c121-140">Przejdź do pulpitu nawigacyjnego usługi, aby upewnić się, Brak urządzeń, połączone z tą usługą.</span><span class="sxs-lookup"><span data-stu-id="5c121-140">Go to your service dashboard to ensure there are no devices connected to the service.</span></span> <span data-ttu-id="5c121-141">Jeśli nie ma żadnych urządzeń zarejestrowanych w usłudze tej usługi, pojawi się także komunikat transparentu, w celu.</span><span class="sxs-lookup"><span data-stu-id="5c121-141">If there are no devices registered with this service, you will also see a banner message to the effect.</span></span> <span data-ttu-id="5c121-142">Kliknij polecenie **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="5c121-142">Click **Delete**.</span></span>
   
    ![Usuwanie usługi](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="5c121-144">Po wyświetleniu monitu o potwierdzenie, kliknij przycisk **tak** powiadomienia o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="5c121-144">When prompted for confirmation, click **Yes** in the confirmation notification.</span></span> 
   
    ![Potwierdź usunięcie usługi](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="5c121-146">Może upłynąć kilka minut, aż usługi do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="5c121-146">It may take a few minutes for the service to be deleted.</span></span> <span data-ttu-id="5c121-147">Po pomyślnym usunięciu usługi, otrzymasz powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="5c121-147">After the service is successfully deleted, you will be notified.</span></span>
   
    ![Usunięcie usługi powiodło się](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="5c121-149">Na liście usług będą odświeżane.</span><span class="sxs-lookup"><span data-stu-id="5c121-149">The list of services will be refreshed.</span></span>

 ![Zaktualizowaną listę usług](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-the-service-registration-key"></a><span data-ttu-id="5c121-151">Pobieranie klucza rejestracji usługi</span><span class="sxs-lookup"><span data-stu-id="5c121-151">Get the service registration key</span></span>
<span data-ttu-id="5c121-152">Po pomyślnym utworzeniu usługi musisz zarejestrować urządzenie StorSimple w usłudze.</span><span class="sxs-lookup"><span data-stu-id="5c121-152">After you have successfully created a service, you will need to register your StorSimple device with the service.</span></span> <span data-ttu-id="5c121-153">Aby zarejestrować pierwszego urządzenia StorSimple, konieczne będzie klucz rejestracji usługi.</span><span class="sxs-lookup"><span data-stu-id="5c121-153">To register your first StorSimple device, you will need the service registration key.</span></span> <span data-ttu-id="5c121-154">Aby zarejestrować dodatkowych urządzeń z istniejącej usługi StorSimple, konieczne będzie zarówno klucz rejestracji i klucza szyfrowania danych usługi (który jest generowany na pierwszym urządzeniem podczas rejestracji).</span><span class="sxs-lookup"><span data-stu-id="5c121-154">To register additional devices with an existing StorSimple service, you will need both the registration key and the service data encryption key (which is generated on the first device during registration).</span></span> <span data-ttu-id="5c121-155">Aby uzyskać więcej informacji na temat klucza szyfrowania danych usługi, zobacz [zabezpieczenia usługi StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="5c121-155">For more information about the service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="5c121-156">Możesz pobrać klucz rejestracji po zalogowaniu się do **klucze** bloku dla usługi.</span><span class="sxs-lookup"><span data-stu-id="5c121-156">You can get the registration key by accessing the **Keys** blade for your service.</span></span>

<span data-ttu-id="5c121-157">Wykonaj poniższe kroki, aby pobrać klucz rejestracji usługi.</span><span class="sxs-lookup"><span data-stu-id="5c121-157">Perform the following steps to get the service registration key.</span></span>

#### <a name="to-get-the-service-registration-key"></a><span data-ttu-id="5c121-158">Aby pobrać klucz rejestracji usługi</span><span class="sxs-lookup"><span data-stu-id="5c121-158">To get the service registration key</span></span>
1. <span data-ttu-id="5c121-159">W **Menedżera urządzeń StorSimple** bloku, przejdź do **zarządzania &gt;**  **klucze**.</span><span class="sxs-lookup"><span data-stu-id="5c121-159">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![Blok Klucze](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="5c121-161">W **klucze** zostanie wyświetlony blok, klucz rejestracji usługi.</span><span class="sxs-lookup"><span data-stu-id="5c121-161">In the **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="5c121-162">Skopiuj klucz rejestracji za pomocą ikony kopiowania.</span><span class="sxs-lookup"><span data-stu-id="5c121-162">Copy the registration key using the copy icon.</span></span> 

<span data-ttu-id="5c121-163">Klucz rejestracji usługi należy przechowywać w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="5c121-163">Keep the service registration key in a safe location.</span></span> <span data-ttu-id="5c121-164">Należy tego klucza, a także klucz szyfrowania danych usługi, aby zarejestrować dodatkowych urządzeń z tą usługą.</span><span class="sxs-lookup"><span data-stu-id="5c121-164">You will need this key, as well as the service data encryption key, to register additional devices with this service.</span></span> <span data-ttu-id="5c121-165">Po uzyskaniu klucza rejestracji usługi, należy skonfigurować urządzenie za pomocą programu Windows PowerShell dla StorSimple interfejsu.</span><span class="sxs-lookup"><span data-stu-id="5c121-165">After obtaining the service registration key, you will need to configure your device through the Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-the-service-registration-key"></a><span data-ttu-id="5c121-166">Wygeneruj ponownie klucz rejestracji usługi</span><span class="sxs-lookup"><span data-stu-id="5c121-166">Regenerate the service registration key</span></span>
<span data-ttu-id="5c121-167">Należy ponownie wygenerować klucz rejestracji usługi, jeśli jest wymagane do wykonania obrotu klucza lub zmiana listy administratorów usługi.</span><span class="sxs-lookup"><span data-stu-id="5c121-167">You will need to regenerate a service registration key if you are required to perform key rotation or if the list of service administrators has changed.</span></span> <span data-ttu-id="5c121-168">Podczas ponownego generowania klucza, nowy klucz służy tylko do celów rejestracji kolejnych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5c121-168">When you regenerate the key, the new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="5c121-169">Przez ten proces nie dotyczy to urządzeń, które zostały już zarejestrowane.</span><span class="sxs-lookup"><span data-stu-id="5c121-169">The devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="5c121-170">Wykonaj poniższe kroki, aby wygenerować ponownie klucz rejestracji usługi.</span><span class="sxs-lookup"><span data-stu-id="5c121-170">Perform the following steps to regenerate a service registration key.</span></span>

#### <a name="to-regenerate-the-service-registration-key"></a><span data-ttu-id="5c121-171">Można ponownie wygenerować klucz rejestracji usługi</span><span class="sxs-lookup"><span data-stu-id="5c121-171">To regenerate the service registration key</span></span>
1. <span data-ttu-id="5c121-172">W **Menedżera urządzeń StorSimple** bloku, przejdź do **zarządzania &gt;**  **klucze**.</span><span class="sxs-lookup"><span data-stu-id="5c121-172">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![Blok Klucze](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="5c121-174">W **klucze** bloku, kliknij przycisk **ponownie wygenerować**.</span><span class="sxs-lookup"><span data-stu-id="5c121-174">In the **Keys** blade, click **Regenerate**.</span></span>
   
   ![Kliknij przycisk regenerate](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="5c121-176">W **klucz rejestracji usługi Regenerate** bloku, przeglądanie nagrań akcji wymagany, gdy klucze są generowane.</span><span class="sxs-lookup"><span data-stu-id="5c121-176">In the **Regenerate service registration key** blade, review the action required when the keys are regenerated.</span></span> <span data-ttu-id="5c121-177">Wszystkie kolejne urządzenia, które są zarejestrowane z tą usługą użyje nowy klucz rejestracji.</span><span class="sxs-lookup"><span data-stu-id="5c121-177">All the subsequent devices that are registered with this service will use the new registration key.</span></span> <span data-ttu-id="5c121-178">Kliknij przycisk **ponownie wygenerować** o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="5c121-178">Click **Regenerate** to confirm.</span></span> <span data-ttu-id="5c121-179">Po zakończeniu rejestracji, otrzymasz powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="5c121-179">You will be notified after the registration is complete.</span></span>
   
   ![Potwierdź klucz regenerate](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="5c121-181">Pojawi się nowy klucz rejestracji usługi.</span><span class="sxs-lookup"><span data-stu-id="5c121-181">A new service registration key will appear.</span></span>
   
    ![Potwierdź klucz regenerate](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="5c121-183">Skopiuj ten klucz i zapisać go do rejestracji żadnych nowych urządzeń z tą usługą.</span><span class="sxs-lookup"><span data-stu-id="5c121-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c121-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5c121-184">Next steps</span></span>
* <span data-ttu-id="5c121-185">Dowiedz się, jak [wprowadzenie](storsimple-virtual-array-deploy1-portal-prep.md) tablicą wirtualne StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5c121-185">Learn how to [get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="5c121-186">Dowiedz się, jak [administrowania urządzenia StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="5c121-186">Learn how to [administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

