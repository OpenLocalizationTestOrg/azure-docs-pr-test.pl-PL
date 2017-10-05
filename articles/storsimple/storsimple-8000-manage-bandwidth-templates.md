---
title: "Zarządzaj szablonami przepustowości dla serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "Opisuje sposób zarządzania StorSimple przepustowości szablonów, które umożliwiają kontrolowanie użycia przepustowości."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 50d0a920bef097013feddc828d2c37133b9057b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-storsimple-bandwidth-templates"></a><span data-ttu-id="72126-103">Zarządzaj szablonami przepustowości StorSimple przy użyciu usługi Menedżer StorSimple urządzenia</span><span class="sxs-lookup"><span data-stu-id="72126-103">Use the StorSimple Device Manager service to manage StorSimple bandwidth templates</span></span>

## <a name="overview"></a><span data-ttu-id="72126-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="72126-104">Overview</span></span>

<span data-ttu-id="72126-105">Szablony przepustowości umożliwiają konfigurowanie użycia przepustowości sieci między kilka harmonogramów czasu dnia do warstwy danych z urządzenia StorSimple w chmurze.</span><span class="sxs-lookup"><span data-stu-id="72126-105">Bandwidth templates allow you to configure network bandwidth usage across multiple time-of-day schedules to tier the data from the StorSimple device to the cloud.</span></span>

<span data-ttu-id="72126-106">Harmonogramy ograniczania przepustowości można:</span><span class="sxs-lookup"><span data-stu-id="72126-106">With bandwidth throttling schedules you can:</span></span>

* <span data-ttu-id="72126-107">Określ harmonogramy niestandardowych przepustowości w zależności od użycia sieci obciążenia.</span><span class="sxs-lookup"><span data-stu-id="72126-107">Specify customized bandwidth schedules depending on the workload network usages.</span></span>
* <span data-ttu-id="72126-108">Scentralizowane zarządzanie i ponowne użycie harmonogramy na wielu urządzeniach w sposób łatwy i bezproblemowe.</span><span class="sxs-lookup"><span data-stu-id="72126-108">Centralize management and reuse the schedules across multiple devices in an easy and seamless manner.</span></span>

> [!NOTE]
> <span data-ttu-id="72126-109">Ta funkcja jest dostępna tylko w przypadku urządzenia fizycznego StorSimple (modele 8100 i 8600), a nie urządzenia chmury StorSimple (modele urządzenia 8010 i 8020).</span><span class="sxs-lookup"><span data-stu-id="72126-109">This feature is available only for StorSimple physical devices (models 8100 and 8600) and not for StorSimple Cloud Appliances (models 8010 and 8020).</span></span>


## <a name="the-bandwidth-templates-blade"></a><span data-ttu-id="72126-110">Blok szablony przepustowości</span><span class="sxs-lookup"><span data-stu-id="72126-110">The Bandwidth templates blade</span></span>

<span data-ttu-id="72126-111">**Szablony przepustowości** bloku ma wszystkie szablony przepustowości dla usługi w formacie tabelarycznym i zawiera następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="72126-111">The **Bandwidth templates** blade has all the bandwidth templates for your service in a tabular format, and contains the following information:</span></span>

* <span data-ttu-id="72126-112">**Nazwa** — nazwa przypisana do szablonu przepustowości podczas jej tworzenia.</span><span class="sxs-lookup"><span data-stu-id="72126-112">**Name** – A unique name assigned to the bandwidth template when it was created.</span></span>
* <span data-ttu-id="72126-113">**Harmonogram** — liczba harmonogramów zawarte w szablonie danego przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-113">**Schedule** – The number of schedules contained in a given bandwidth template.</span></span>
* <span data-ttu-id="72126-114">**Używane przez** — liczba woluminów za pomocą szablonów przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-114">**Used by** – The number of volumes using the bandwidth templates.</span></span>

<span data-ttu-id="72126-115">Można również znaleźć dodatkowe informacje ułatwiające konfigurowanie szablonów przepustowości w:</span><span class="sxs-lookup"><span data-stu-id="72126-115">You can also find additional information to help configure bandwidth templates in:</span></span>

* [<span data-ttu-id="72126-116">Pytania i odpowiedzi dotyczące przepustowości szablonów</span><span class="sxs-lookup"><span data-stu-id="72126-116">Questions and answers about bandwidth templates</span></span>](#questions-and-answers-about-bandwidth-templates)
* [<span data-ttu-id="72126-117">Najlepsze rozwiązania dotyczące przepustowości szablonów</span><span class="sxs-lookup"><span data-stu-id="72126-117">Best practices for bandwidth templates</span></span>](#best-practices-for-bandwidth-templates)

## <a name="add-a-bandwidth-template"></a><span data-ttu-id="72126-118">Dodaj szablon przepustowości</span><span class="sxs-lookup"><span data-stu-id="72126-118">Add a bandwidth template</span></span>

<span data-ttu-id="72126-119">Wykonaj poniższe kroki, aby utworzyć nowy szablon przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-119">Perform the following steps to create a new bandwidth template.</span></span>

#### <a name="to-add-a-bandwidth-template"></a><span data-ttu-id="72126-120">Aby dodać szablon przepustowości</span><span class="sxs-lookup"><span data-stu-id="72126-120">To add a bandwidth template</span></span>

1. <span data-ttu-id="72126-121">Przejdź do usługi Menedżer urządzeń StorSimple, kliknij przycisk **szablony przepustowości** , a następnie kliknij przycisk **+ Dodaj przepustowości szablonu**.</span><span class="sxs-lookup"><span data-stu-id="72126-121">Go to your StorSimple Device Manager service, click **Bandwidth templates** and then click **+ Add Bandwidth template**.</span></span>

    ![Kliknij pozycję + Dodaj szablon przepustowości](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp1.png)

2. <span data-ttu-id="72126-123">W **Dodaj szablon przepustowości** blok, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="72126-123">In the **Add bandwidth template** blade, do the following steps:</span></span>
   
    1. <span data-ttu-id="72126-124">Określ unikatową nazwę dla szablonu przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-124">Specify a unique name for your bandwidth template.</span></span>
    2. <span data-ttu-id="72126-125">Zdefiniuj harmonogram przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-125">Define a bandwidth schedule.</span></span> <span data-ttu-id="72126-126">Aby utworzyć harmonogram:</span><span class="sxs-lookup"><span data-stu-id="72126-126">To create a schedule:</span></span>
   
        1. <span data-ttu-id="72126-127">Z listy rozwijanej wybierz **dni** tygodnia harmonogramu jest skonfigurowany dla.</span><span class="sxs-lookup"><span data-stu-id="72126-127">From the drop-down list, choose the **Days** of the week the schedule is configured for.</span></span> <span data-ttu-id="72126-128">Można wybrać kilka dni.</span><span class="sxs-lookup"><span data-stu-id="72126-128">You can select multiple days.</span></span>        
        
        2. <span data-ttu-id="72126-129">Wprowadź **czas rozpoczęcia** w _gg: mm_ format.</span><span class="sxs-lookup"><span data-stu-id="72126-129">Enter a **Start Time** in _hh:mm_ format.</span></span> <span data-ttu-id="72126-130">Jest to, gdy rozpocznie się harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="72126-130">This is when the schedule will begin.</span></span>

        3. <span data-ttu-id="72126-131">Wprowadź **czas zakończenia** w _gg: mm_ format.</span><span class="sxs-lookup"><span data-stu-id="72126-131">Enter an **End Time** in _hh:mm_ format.</span></span> <span data-ttu-id="72126-132">Jest to harmonogram zostanie zatrzymane.</span><span class="sxs-lookup"><span data-stu-id="72126-132">This is when the schedule will stop.</span></span>
      
           > [!NOTE]
           > <span data-ttu-id="72126-133">Nakładające się harmonogramy nie są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="72126-133">Overlapping schedules are not allowed.</span></span> <span data-ttu-id="72126-134">Czas rozpoczęcia i zakończenia spowoduje nakładające się harmonogramu, pojawi się odpowiedni komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="72126-134">If the start and end times will result in an overlapping schedule, you will see an error message to that effect.</span></span>

        4. <span data-ttu-id="72126-135">Określ **szybkość przepustowości**.</span><span class="sxs-lookup"><span data-stu-id="72126-135">Specify the **Bandwidth Rate**.</span></span> <span data-ttu-id="72126-136">Jest to przepustowość w megabitach na sekundę (MB/s) używany przez urządzenia StorSimple w operacji dotyczących chmury (przekazywania i pobierania).</span><span class="sxs-lookup"><span data-stu-id="72126-136">This is the bandwidth in Megabits per second (Mbps) used by your StorSimple device in operations involving the cloud (both uploads and downloads).</span></span> <span data-ttu-id="72126-137">Wprowadź liczbę z zakresu od 1 do 1000 dla tego pola.</span><span class="sxs-lookup"><span data-stu-id="72126-137">Supply a number between 1 and 1,000 for this field.</span></span>

            ![Zdefiniuj harmonogram przepustowości](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp2.png)
         
            <span data-ttu-id="72126-139">Powtórz powyższe kroki, aby zdefiniować wiele harmonogramów szablonu, aż wszystko będzie gotowe.</span><span class="sxs-lookup"><span data-stu-id="72126-139">Repeat the above steps to define multiple schedules for your template until you are done.</span></span>

        5. <span data-ttu-id="72126-140">Kliknij przycisk **Dodaj** aby rozpocząć tworzenie szablonu przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-140">Click **Add** to start creating a bandwidth template.</span></span> <span data-ttu-id="72126-141">Utworzony szablon jest dodawany do listy szablonów przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-141">The created template is added to the list of bandwidth templates.</span></span>
      

## <a name="edit-a-bandwidth-template"></a><span data-ttu-id="72126-142">Edytuj szablon przepustowości</span><span class="sxs-lookup"><span data-stu-id="72126-142">Edit a bandwidth template</span></span>

<span data-ttu-id="72126-143">Wykonaj poniższe kroki, aby edytować szablon przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-143">Perform the following steps to edit a bandwidth template.</span></span>

### <a name="to-edit-a-bandwidth-template"></a><span data-ttu-id="72126-144">Aby edytować szablon przepustowości</span><span class="sxs-lookup"><span data-stu-id="72126-144">To edit a bandwidth template</span></span>

1. <span data-ttu-id="72126-145">Przejdź do Menedżera urządzenia StorSimple usługi, a następnie kliknij przycisk **szablony przepustowości**.</span><span class="sxs-lookup"><span data-stu-id="72126-145">Go to your StorSimple Device Manager service and click **Bandwidth templates**.</span></span>
2. <span data-ttu-id="72126-146">Na liście szablonów przepustowości wybierz szablon, który chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="72126-146">In the list of bandwidth templates, select the template you wish to delete.</span></span> <span data-ttu-id="72126-147">Kliknij prawym przyciskiem myszy i wybierz z menu kontekstowego **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="72126-147">Right-click and from the context menu, select **Delete**.</span></span>
3. <span data-ttu-id="72126-148">Po wyświetleniu monitu o potwierdzenie, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="72126-148">When prompted for confirmation, click **OK**.</span></span> <span data-ttu-id="72126-149">To powinien usunąć szablon przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-149">This should delete the bandwidth template.</span></span> 
4. <span data-ttu-id="72126-150">Lista aktualizacji szablonów przepustowości do uwzględnienia usunięcia.</span><span class="sxs-lookup"><span data-stu-id="72126-150">The list of bandwidth templates updates to reflect the deletion.</span></span>

> [!NOTE]
> <span data-ttu-id="72126-151">Nie można zapisać zmiany, jeśli edytowanych harmonogramu pokrywa się z istniejącego harmonogramu modyfikowanego szablonu przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-151">You cannot save your changes if the edited schedule overlaps with an existing schedule in the bandwidth template that you are modifying.</span></span>

## <a name="delete-a-bandwidth-template"></a><span data-ttu-id="72126-152">Usuń szablon przepustowości</span><span class="sxs-lookup"><span data-stu-id="72126-152">Delete a bandwidth template</span></span>

<span data-ttu-id="72126-153">Wykonaj poniższe kroki, aby usunąć szablon przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-153">Perform the following steps to delete a bandwidth template.</span></span>

#### <a name="to-delete-a-bandwidth-template"></a><span data-ttu-id="72126-154">Aby usunąć szablon przepustowości</span><span class="sxs-lookup"><span data-stu-id="72126-154">To delete a bandwidth template</span></span>

1. <span data-ttu-id="72126-155">Przejdź do Menedżera urządzenia StorSimple usługi, a następnie kliknij przycisk **szablony przepustowości**.</span><span class="sxs-lookup"><span data-stu-id="72126-155">Go to your StorSimple Device Manager service and click **Bandwidth templates**.</span></span>
2. <span data-ttu-id="72126-156">Na liście szablonów przepustowości wybierz szablon, który chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="72126-156">In the list of bandwidth templates, select the template you wish to delete.</span></span> <span data-ttu-id="72126-157">Kliknij prawym przyciskiem myszy i z menu kontekstowego wybierz polecenie Usuń.</span><span class="sxs-lookup"><span data-stu-id="72126-157">Right-click and from the context menu, select Delete.</span></span>
3. <span data-ttu-id="72126-158">Po wyświetleniu monitu o potwierdzenie, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="72126-158">When prompted for confirmation, click **OK**.</span></span> <span data-ttu-id="72126-159">To powinien usunąć szablon przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-159">This should delete the bandwidth template.</span></span>
4. <span data-ttu-id="72126-160">Lista aktualizacji szablonów przepustowości do uwzględnienia usunięcia.</span><span class="sxs-lookup"><span data-stu-id="72126-160">The list of bandwidth templates updates to reflect the deletion.</span></span>

<span data-ttu-id="72126-161">Jeśli szablon jest używany przez wszystkie woluminy, nie będzie można go usunąć.</span><span class="sxs-lookup"><span data-stu-id="72126-161">If the template is in use by any volume(s), you will not be allowed to delete it.</span></span> <span data-ttu-id="72126-162">Pojawi się komunikat o błędzie wskazujący, że szablon jest używany.</span><span class="sxs-lookup"><span data-stu-id="72126-162">You will see an error message indicating that the template is in use.</span></span> <span data-ttu-id="72126-163">Zostanie wyświetlone okno dialogowe komunikat błędu, udzielanie porad należy usunąć wszystkie odwołania do szablonu.</span><span class="sxs-lookup"><span data-stu-id="72126-163">An error message dialog box will appear advising you that all the references to the template should be removed.</span></span>

<span data-ttu-id="72126-164">Możesz usunąć wszystkie odwołania do szablonu po zalogowaniu się do **kontenery woluminów** strony i modyfikowanie kontenery woluminów, które użyć tego szablonu, aby użyć innego szablonu lub użyć ustawienia niestandardowe lub nieograniczone przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-164">You can delete all the references to the template by accessing the **Volume Containers** page and modifying the volume containers that use this template so that they use another template or use a custom or unlimited bandwidth setting.</span></span> <span data-ttu-id="72126-165">Po usunięciu wszystkich odwołań, można usunąć szablonu.</span><span class="sxs-lookup"><span data-stu-id="72126-165">When all the references have been removed, you can delete the template.</span></span>

## <a name="use-a-default-bandwidth-template"></a><span data-ttu-id="72126-166">Użyj domyślnego szablonu przepustowości</span><span class="sxs-lookup"><span data-stu-id="72126-166">Use a default bandwidth template</span></span>

<span data-ttu-id="72126-167">Domyślny szablon przepustowości podano i jest używany przez kontenery woluminów domyślnie w celu wymuszenia kontroli przepustowości podczas uzyskiwania dostępu do chmury.</span><span class="sxs-lookup"><span data-stu-id="72126-167">A default bandwidth template is provided and is used by volume containers by default to enforce bandwidth controls when accessing the cloud.</span></span> <span data-ttu-id="72126-168">Domyślny szablon służy również jako punkt odniesienia gotowy dla użytkowników, którzy tworzyć własne szablony.</span><span class="sxs-lookup"><span data-stu-id="72126-168">The default template also serves as a ready reference for users who create their own templates.</span></span> <span data-ttu-id="72126-169">Szczegóły tego szablonu domyślnego są:</span><span class="sxs-lookup"><span data-stu-id="72126-169">The details of this default template are:</span></span>

* <span data-ttu-id="72126-170">**Nazwa** — w nocy nieograniczone, jak i w weekendy</span><span class="sxs-lookup"><span data-stu-id="72126-170">**Name** – Unlimited nights and weekends</span></span>
* <span data-ttu-id="72126-171">**Harmonogram** — jeden harmonogram od poniedziałku do piątku stosowanym współczynnika przepustowości 1 MB/s miedzy 8 a 17: 00 czasu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="72126-171">**Schedule** – A single schedule from Monday to Friday that applies a bandwidth rate of 1 Mbps between 8 AM and 5 PM device time.</span></span> <span data-ttu-id="72126-172">W pozostałej części tygodnia wynosi przepustowości bez ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="72126-172">The bandwidth is set to Unlimited for the remainder of the week.</span></span>

<span data-ttu-id="72126-173">Można edytować szablon domyślny.</span><span class="sxs-lookup"><span data-stu-id="72126-173">The default template can be edited.</span></span> <span data-ttu-id="72126-174">Użycie tego szablonu (w tym wersje edytowanych) są śledzone.</span><span class="sxs-lookup"><span data-stu-id="72126-174">The usage of this template (including edited versions) is tracked.</span></span>

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a><span data-ttu-id="72126-175">Tworzenie szablonu przepustowości całodzienne, która rozpoczyna się od określonego czasu</span><span class="sxs-lookup"><span data-stu-id="72126-175">Create an all-day bandwidth template that starts at a specified time</span></span>

<span data-ttu-id="72126-176">Wykonaj tę procedurę, aby utworzyć harmonogram, który rozpoczyna się od określonego czasu i uruchamia cały dzień.</span><span class="sxs-lookup"><span data-stu-id="72126-176">Follow this procedure to create a schedule that starts at a specified time and runs all day.</span></span> <span data-ttu-id="72126-177">W tym przykładzie harmonogram rozpoczyna się od 9 AM w nocy i uruchamia do 9 AM następnego dnia rano.</span><span class="sxs-lookup"><span data-stu-id="72126-177">In the example, the schedule starts at 9 AM in the morning and runs until 9 AM the next morning.</span></span> <span data-ttu-id="72126-178">Należy pamiętać, że godziny rozpoczęcia i zakończenia dla danego harmonogramu muszą być jednocześnie zawarte na ten sam harmonogram 24-godzinnym i nie może obejmować wiele dni.</span><span class="sxs-lookup"><span data-stu-id="72126-178">It's important to note that the start and end times for a given schedule must both be contained on the same 24 hour schedule and cannot span multiple days.</span></span> <span data-ttu-id="72126-179">Jeśli trzeba zdefiniować szablony przepustowości, obejmujące wiele dni, należy użyć wielu harmonogramów (jak pokazano w przykładzie).</span><span class="sxs-lookup"><span data-stu-id="72126-179">If you need to set up bandwidth templates that span multiple days, you will need to use multiple schedules (as shown in the example).</span></span>

#### <a name="to-create-an-all-day-bandwidth-template"></a><span data-ttu-id="72126-180">Aby utworzyć szablon przepustowości całodzienne</span><span class="sxs-lookup"><span data-stu-id="72126-180">To create an all-day bandwidth template</span></span>

1. <span data-ttu-id="72126-181">Utwórz harmonogram, który rozpoczyna się od 9 AM w nocy i uruchamia do północy.</span><span class="sxs-lookup"><span data-stu-id="72126-181">Create a schedule that starts at 9 AM in the morning and runs until midnight.</span></span>
2. <span data-ttu-id="72126-182">Dodaj inny harmonogram.</span><span class="sxs-lookup"><span data-stu-id="72126-182">Add another schedule.</span></span> <span data-ttu-id="72126-183">Skonfiguruj drugi harmonogram wykonywania od północy do 9 AM w nocy.</span><span class="sxs-lookup"><span data-stu-id="72126-183">Configure the second schedule to run from midnight until 9 AM in the morning.</span></span>
3. <span data-ttu-id="72126-184">Zapisz szablon przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-184">Save the bandwidth template.</span></span>

<span data-ttu-id="72126-185">Harmonogram złożony będą uruchomione w czasie wybrane i uruchom całodzienne.</span><span class="sxs-lookup"><span data-stu-id="72126-185">The composite schedule will then start at a time of your choosing and run all-day.</span></span>

## <a name="questions-and-answers-about-bandwidth-templates"></a><span data-ttu-id="72126-186">Pytania i odpowiedzi dotyczące przepustowości szablonów</span><span class="sxs-lookup"><span data-stu-id="72126-186">Questions and answers about bandwidth templates</span></span>

<span data-ttu-id="72126-187">**Q**.</span><span class="sxs-lookup"><span data-stu-id="72126-187">**Q**.</span></span> <span data-ttu-id="72126-188">Co się dzieje kontroli przepustowości podczas pracy Between harmonogramy?</span><span class="sxs-lookup"><span data-stu-id="72126-188">What happens to bandwidth controls when you are in between the schedules?</span></span> <span data-ttu-id="72126-189">(Zakończył się zgodnie z harmonogramem i innego nie została jeszcze uruchomiona.)</span><span class="sxs-lookup"><span data-stu-id="72126-189">(A schedule has ended and another one has not started yet.)</span></span>

<span data-ttu-id="72126-190">**A**.</span><span class="sxs-lookup"><span data-stu-id="72126-190">**A**.</span></span> <span data-ttu-id="72126-191">W takich przypadkach zostanie zastosowane bez kontroli przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-191">In such cases, no bandwidth controls will be employed.</span></span> <span data-ttu-id="72126-192">Oznacza to, że urządzenie może używać nieograniczone przepustowości podczas tworzenia warstw danych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="72126-192">This means that the device can use unlimited bandwidth when tiering data to the cloud.</span></span>

<span data-ttu-id="72126-193">**Q**.</span><span class="sxs-lookup"><span data-stu-id="72126-193">**Q**.</span></span> <span data-ttu-id="72126-194">Czy możesz zmodyfikować szablony przepustowość na urządzeniu w trybie offline?</span><span class="sxs-lookup"><span data-stu-id="72126-194">Can you modify bandwidth templates on an offline device?</span></span>

<span data-ttu-id="72126-195">**A**.</span><span class="sxs-lookup"><span data-stu-id="72126-195">**A**.</span></span> <span data-ttu-id="72126-196">Nie można zmodyfikować szablony przepustowość na kontenery woluminów, jeśli odpowiednie urządzenie jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="72126-196">You will not be able to modify bandwidth templates on volumes containers if the corresponding device is offline.</span></span>

<span data-ttu-id="72126-197">**Q**.</span><span class="sxs-lookup"><span data-stu-id="72126-197">**Q**.</span></span> <span data-ttu-id="72126-198">Możesz edytować szablon przepustowości skojarzone z kontenera woluminów, gdy skojarzone woluminy są w trybie offline</span><span class="sxs-lookup"><span data-stu-id="72126-198">Can you edit a bandwidth template associated with a volume container when the associated volumes are offline?</span></span>

<span data-ttu-id="72126-199">**A**.</span><span class="sxs-lookup"><span data-stu-id="72126-199">**A**.</span></span> <span data-ttu-id="72126-200">Można zmodyfikować szablonu przepustowości skojarzone z kontenera woluminów, których woluminy są w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="72126-200">You can modify a bandwidth template associated with a volume container whose volumes are offline.</span></span> <span data-ttu-id="72126-201">Należy pamiętać, że gdy woluminy są w trybie offline, żadne dane nie będą należeć do warstwy z urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="72126-201">Note that when volumes are offline, no data will be tiered from the device to the cloud.</span></span>

<span data-ttu-id="72126-202">**Q**.</span><span class="sxs-lookup"><span data-stu-id="72126-202">**Q**.</span></span> <span data-ttu-id="72126-203">Można usunąć domyślny szablon?</span><span class="sxs-lookup"><span data-stu-id="72126-203">Can you delete a default template?</span></span>

<span data-ttu-id="72126-204">**A**.</span><span class="sxs-lookup"><span data-stu-id="72126-204">**A**.</span></span> <span data-ttu-id="72126-205">Mimo że można usunąć szablonu domyślnego, nie jest dobrym rozwiązaniem, aby to zrobić.</span><span class="sxs-lookup"><span data-stu-id="72126-205">Although you can delete a default template, it is not a good idea to do so.</span></span> <span data-ttu-id="72126-206">Użycie szablonu domyślnego, tym edytowanych wersje są śledzone.</span><span class="sxs-lookup"><span data-stu-id="72126-206">The usage of a default template, including edited versions, is tracked.</span></span> <span data-ttu-id="72126-207">Dane śledzenia są analizowane i w ciągu godziny jest używany do zwiększenia domyślnego szablonu.</span><span class="sxs-lookup"><span data-stu-id="72126-207">The tracking data is analyzed and over the course of time, is used to improve the default template.</span></span>

<span data-ttu-id="72126-208">**Q**.</span><span class="sxs-lookup"><span data-stu-id="72126-208">**Q**.</span></span> <span data-ttu-id="72126-209">Jaki sposób można określić, czy szablony przepustowości muszą zostać zmodyfikowane?</span><span class="sxs-lookup"><span data-stu-id="72126-209">How do you determine that your bandwidth templates need to be modified?</span></span>

<span data-ttu-id="72126-210">**A**.</span><span class="sxs-lookup"><span data-stu-id="72126-210">**A**.</span></span> <span data-ttu-id="72126-211">Jest jednym ze znaków, należy zmodyfikować szablony przepustowości podczas uruchamiania wyświetlać sieci działa wolno lub podlewka wiele razy w ciągu jednego dnia.</span><span class="sxs-lookup"><span data-stu-id="72126-211">One of the signs that you need to modify the bandwidth templates is when you start seeing the network slow down or choke multiple times in a day.</span></span> <span data-ttu-id="72126-212">W takim przypadku monitorowania sieci magazynu i użycia, analizując wykresy wydajności operacji We/Wy i przepustowość sieci.</span><span class="sxs-lookup"><span data-stu-id="72126-212">If this happens, monitor the storage and usage network by looking at the I/O Performance and Network Throughput charts.</span></span>

<span data-ttu-id="72126-213">Z danych przepustowość sieci należy zidentyfikować godzina i kontenery woluminów, w których występuje wąskich gardeł.</span><span class="sxs-lookup"><span data-stu-id="72126-213">From the network throughput data, identify the time of day and the volume containers in which the network bottleneck occurs.</span></span> <span data-ttu-id="72126-214">Jeśli dzieje, gdy jest on warstwowa danych do chmury (uzyskać te informacje z wydajność We/Wy dla wszystkich kontenerów woluminu dla urządzenia do chmury), a następnie należy zmodyfikować szablony przepustowości skojarzone z kontenerów woluminu.</span><span class="sxs-lookup"><span data-stu-id="72126-214">If this happens when data is being tiered to the cloud (get this information from I/O performance for all volume containers for device to cloud), then you will need to modify the bandwidth templates associated with your volume containers.</span></span>

<span data-ttu-id="72126-215">Po modyfikacji szablony są używane, należy monitorować ponownie znaczne opóźnienia sieci.</span><span class="sxs-lookup"><span data-stu-id="72126-215">After the modified templates are in use, you will need to monitor the network again for significant latencies.</span></span> <span data-ttu-id="72126-216">Jeśli te nadal istnieje, następnie konieczne będzie ponowne przeanalizowanie szablonów przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-216">If these still exist, then you will need to revisit your bandwidth templates.</span></span>

<span data-ttu-id="72126-217">**Q**.</span><span class="sxs-lookup"><span data-stu-id="72126-217">**Q**.</span></span> <span data-ttu-id="72126-218">Co się stanie, jeśli ma wiele kontenerów wolumin w urządzeniu planuje tego nakładają się na siebie, ale różne limity mają zastosowanie do każdej?</span><span class="sxs-lookup"><span data-stu-id="72126-218">What happens if multiple volume containers on my device have schedules that overlap but different limits apply to each?</span></span>

<span data-ttu-id="72126-219">**A**.</span><span class="sxs-lookup"><span data-stu-id="72126-219">**A**.</span></span> <span data-ttu-id="72126-220">Załóżmy, że masz urządzenie z 3 kontenery woluminów.</span><span class="sxs-lookup"><span data-stu-id="72126-220">Let's assume that you have a device with 3 volume containers.</span></span> <span data-ttu-id="72126-221">Harmonogramy skojarzone z tych kontenerów całkowicie nakładają się.</span><span class="sxs-lookup"><span data-stu-id="72126-221">The schedules associated with these containers completely overlap.</span></span> <span data-ttu-id="72126-222">Dla każdego z tych kontenerów limity przepustowości, używane są 5, 10 lub 15 MB/s odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="72126-222">For each of these containers, the bandwidth limits used are 5, 10, and 15 Mbps respectively.</span></span> <span data-ttu-id="72126-223">Podczas operacji We/Wy występujących w wszystkie kontenery w tym samym czasie, co najmniej 3 limity przepustowości mogą być stosowane: w tym przypadku 5 MB/s one wychodzących żądań We/Wy udostępnić tę samą kolejkę.</span><span class="sxs-lookup"><span data-stu-id="72126-223">When I/O are occurring on all of these containers at the same time, the minimum of the 3 bandwidth limits may be applied: in this case, 5 Mbps as these outgoing I/O requests share the same queue.</span></span>

## <a name="best-practices-for-bandwidth-templates"></a><span data-ttu-id="72126-224">Najlepsze rozwiązania dotyczące przepustowości szablonów</span><span class="sxs-lookup"><span data-stu-id="72126-224">Best practices for bandwidth templates</span></span>

<span data-ttu-id="72126-225">Należy stosować następujące najlepsze rozwiązania dla urządzenia StorSimple:</span><span class="sxs-lookup"><span data-stu-id="72126-225">Follow these best practices for your StorSimple device:</span></span>

* <span data-ttu-id="72126-226">Konfigurowanie szablonów przepustowość na urządzeniu, aby włączyć zmiennej ograniczania przepustowości sieci przez urządzenie o różnych porach dnia.</span><span class="sxs-lookup"><span data-stu-id="72126-226">Configure bandwidth templates on your device to enable variable throttling of the network throughput by the device at different times of the day.</span></span> <span data-ttu-id="72126-227">Te szablony przepustowości, gdy jest używany z harmonogramy tworzenia kopii zapasowej można efektywnie wykorzystać dodatkowej przepustowości sieci dla operacji poza godzinami szczytu.</span><span class="sxs-lookup"><span data-stu-id="72126-227">These bandwidth templates when used with backup schedules can effectively leverage additional network bandwidth for cloud operations during off-peak hours.</span></span>
* <span data-ttu-id="72126-228">Oblicz rzeczywistej wymaganej dla konkretnego wdrożenia na podstawie rozmiaru wdrożenia i celu czasu wymaganego odzyskiwania (RTO) przepustowości.</span><span class="sxs-lookup"><span data-stu-id="72126-228">Calculate the actual bandwidth required for a particular deployment based on the size of the deployment and the required recovery time objective (RTO).</span></span>

## <a name="next-steps"></a><span data-ttu-id="72126-229">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="72126-229">Next steps</span></span>

<span data-ttu-id="72126-230">Dowiedz się więcej o [przy użyciu usługi Menedżer StorSimple urządzenia do administrowania urządzeniem StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="72126-230">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

