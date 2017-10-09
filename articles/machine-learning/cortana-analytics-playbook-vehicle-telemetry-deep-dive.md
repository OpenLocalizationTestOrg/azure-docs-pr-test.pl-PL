---
title: "Poznaj aaaDeep prognozowania vehicle kondycji i wspierającym zwyczaje - Azure | Dokumentacja firmy Microsoft"
description: "Korzystanie z możliwości hello wgląd w czasie rzeczywistym oraz predykcyjnej toogain Cortana Intelligence na kondycji vehicle i wspierającym zwyczaje."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a><span data-ttu-id="1b902-103">Vehicle telemetrii analizy rozwiązania podręcznikowym: nowości w hello rozwiązania</span><span class="sxs-lookup"><span data-stu-id="1b902-103">Vehicle telemetry analytics solution playbook: deep dive into hello solution</span></span>
<span data-ttu-id="1b902-104">To **menu** toohello części tego podręcznika dotyczącego łączy:</span><span class="sxs-lookup"><span data-stu-id="1b902-104">This **menu** links toohello sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="1b902-105">Ta sekcja rozwija na każdym z etapów hello pokazana na powitania architektury rozwiązania wraz z instrukcjami i wskaźniki do dostosowania.</span><span class="sxs-lookup"><span data-stu-id="1b902-105">This section drills down into each of hello stages depicted in hello Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="1b902-106">Źródła danych</span><span class="sxs-lookup"><span data-stu-id="1b902-106">Data Sources</span></span>
<span data-ttu-id="1b902-107">rozwiązanie Hello używa dwóch różnych źródeł danych:</span><span class="sxs-lookup"><span data-stu-id="1b902-107">hello solution uses two different data sources:</span></span>

* <span data-ttu-id="1b902-108">**Symulowane sygnały vehicle i danych diagnostycznych** i</span><span class="sxs-lookup"><span data-stu-id="1b902-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="1b902-109">**vehicle katalogu**</span><span class="sxs-lookup"><span data-stu-id="1b902-109">**vehicle catalog**</span></span>

<span data-ttu-id="1b902-110">Symulator telematyki vehicle wchodzi w skład tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="1b902-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="1b902-111">Emituje informacje diagnostyczne, a sygnały odpowiadający mu stan toohello hello vehicle i toohello zwiększają wzorca w danym punkcie w czasie.</span><span class="sxs-lookup"><span data-stu-id="1b902-111">It emits diagnostic information and signals corresponding toohello state of hello vehicle and toohello driving pattern at a given point in time.</span></span> <span data-ttu-id="1b902-112">Kliknij przycisk [symulatora telematyki Vehicle](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **Vehicle telematyki symulatora rozwiązania Visual Studio** dostosowań, w zależności od wymagań.</span><span class="sxs-lookup"><span data-stu-id="1b902-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="1b902-113">katalog vehicle Hello zawiera odwołanie do zestawu danych z mapowaniem toomodel VIN.</span><span class="sxs-lookup"><span data-stu-id="1b902-113">hello vehicle catalog contains a reference dataset with a VIN toomodel mapping.</span></span>

![Symulator telematyki vehicle](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="1b902-115">*Rysunek 1 — Vehicle telematyki symulatora*</span><span class="sxs-lookup"><span data-stu-id="1b902-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="1b902-116">Jest to formacie JSON zestawu danych zawierającego powitania po schematu.</span><span class="sxs-lookup"><span data-stu-id="1b902-116">This is a JSON-formatted dataset that contains hello following schema.</span></span>

| <span data-ttu-id="1b902-117">Kolumna</span><span class="sxs-lookup"><span data-stu-id="1b902-117">Column</span></span> | <span data-ttu-id="1b902-118">Opis</span><span class="sxs-lookup"><span data-stu-id="1b902-118">Description</span></span> | <span data-ttu-id="1b902-119">Wartości</span><span class="sxs-lookup"><span data-stu-id="1b902-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1b902-120">VIN</span><span class="sxs-lookup"><span data-stu-id="1b902-120">VIN</span></span> |<span data-ttu-id="1b902-121">Losowo generowany numer identyfikacyjny</span><span class="sxs-lookup"><span data-stu-id="1b902-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="1b902-122">To są uzyskiwane ze wzorca listę 10 000 numery identyfikacyjne losowo generowany pojazdów.</span><span class="sxs-lookup"><span data-stu-id="1b902-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="1b902-123">Poza temperatury</span><span class="sxs-lookup"><span data-stu-id="1b902-123">Outside temperature</span></span> |<span data-ttu-id="1b902-124">Witaj poza temperatury gdzie sterujące hello vehicle</span><span class="sxs-lookup"><span data-stu-id="1b902-124">hello outside temperature where hello vehicle is driving</span></span> |<span data-ttu-id="1b902-125">Losowo generowany numer od 0 do 100</span><span class="sxs-lookup"><span data-stu-id="1b902-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="1b902-126">Aparat temperatury</span><span class="sxs-lookup"><span data-stu-id="1b902-126">Engine temperature</span></span> |<span data-ttu-id="1b902-127">Witaj aparat temperatury pojazdów hello</span><span class="sxs-lookup"><span data-stu-id="1b902-127">hello engine temperature of hello vehicle</span></span> |<span data-ttu-id="1b902-128">Losowo generowany numer od 0-500</span><span class="sxs-lookup"><span data-stu-id="1b902-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="1b902-129">Szybkość</span><span class="sxs-lookup"><span data-stu-id="1b902-129">Speed</span></span> |<span data-ttu-id="1b902-130">szybkość aparat Hello na które hello sterujące vehicle</span><span class="sxs-lookup"><span data-stu-id="1b902-130">hello engine speed at which hello vehicle is driving</span></span> |<span data-ttu-id="1b902-131">Losowo generowany numer od 0 do 100</span><span class="sxs-lookup"><span data-stu-id="1b902-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="1b902-132">Paliwa</span><span class="sxs-lookup"><span data-stu-id="1b902-132">Fuel</span></span> |<span data-ttu-id="1b902-133">poziom paliwa Hello pojazdów hello</span><span class="sxs-lookup"><span data-stu-id="1b902-133">hello fuel level of hello vehicle</span></span> |<span data-ttu-id="1b902-134">Losowo generowany numer od 0 do 100 (procent poziomu paliwa wskazuje)</span><span class="sxs-lookup"><span data-stu-id="1b902-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="1b902-135">EngineOil</span><span class="sxs-lookup"><span data-stu-id="1b902-135">EngineOil</span></span> |<span data-ttu-id="1b902-136">Witaj aparatu wydobycie ropy naftowej pojazdów hello</span><span class="sxs-lookup"><span data-stu-id="1b902-136">hello engine oil level of hello vehicle</span></span> |<span data-ttu-id="1b902-137">Losowo generowany numer od 0 do 100 (procent poziomu wydobycie ropy naftowej aparat oznacza)</span><span class="sxs-lookup"><span data-stu-id="1b902-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="1b902-138">Opona wykorzystania</span><span class="sxs-lookup"><span data-stu-id="1b902-138">Tire pressure</span></span> |<span data-ttu-id="1b902-139">Witaj opona wykorzystania pojazdów hello</span><span class="sxs-lookup"><span data-stu-id="1b902-139">hello tire pressure of hello vehicle</span></span> |<span data-ttu-id="1b902-140">Losowo generowany numer 50 0 (wskazuje procent poziomu wykorzystania opona)</span><span class="sxs-lookup"><span data-stu-id="1b902-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="1b902-141">Licznika</span><span class="sxs-lookup"><span data-stu-id="1b902-141">Odometer</span></span> |<span data-ttu-id="1b902-142">Odczytywanie licznika Hello hello vehicle</span><span class="sxs-lookup"><span data-stu-id="1b902-142">hello odometer reading of hello vehicle</span></span> |<span data-ttu-id="1b902-143">Losowo generowany numer od 0 200000</span><span class="sxs-lookup"><span data-stu-id="1b902-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="1b902-144">Accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="1b902-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="1b902-145">Pozycja szkła akceleratora Hello pojazdów hello</span><span class="sxs-lookup"><span data-stu-id="1b902-145">hello accelerator pedal position of hello vehicle</span></span> |<span data-ttu-id="1b902-146">Losowo generowany numer od 0 do 100 (procent poziomu akceleratora wskazuje)</span><span class="sxs-lookup"><span data-stu-id="1b902-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="1b902-147">Parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="1b902-147">Parking_brake_status</span></span> |<span data-ttu-id="1b902-148">Wskazuje, czy hello vehicle jest stoi lub nie</span><span class="sxs-lookup"><span data-stu-id="1b902-148">Indicates whether hello vehicle is parked or not</span></span> |<span data-ttu-id="1b902-149">Wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="1b902-149">True or False</span></span> |
| <span data-ttu-id="1b902-150">Headlamp_status</span><span class="sxs-lookup"><span data-stu-id="1b902-150">Headlamp_status</span></span> |<span data-ttu-id="1b902-151">Wskazuje, gdzie reflektor hello jest na lub nie</span><span class="sxs-lookup"><span data-stu-id="1b902-151">Indicates where hello headlamp is on or not</span></span> |<span data-ttu-id="1b902-152">Wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="1b902-152">True or False</span></span> |
| <span data-ttu-id="1b902-153">Brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="1b902-153">Brake_pedal_status</span></span> |<span data-ttu-id="1b902-154">Wskazuje, czy pedał hamulca hello zostanie naciśnięty, czy nie</span><span class="sxs-lookup"><span data-stu-id="1b902-154">Indicates whether hello brake pedal is pressed or not</span></span> |<span data-ttu-id="1b902-155">Wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="1b902-155">True or False</span></span> |
| <span data-ttu-id="1b902-156">Transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="1b902-156">Transmission_gear_position</span></span> |<span data-ttu-id="1b902-157">Pozycja koło zębate transmisji Hello pojazdów hello</span><span class="sxs-lookup"><span data-stu-id="1b902-157">hello transmission gear position of hello vehicle</span></span> |<span data-ttu-id="1b902-158">Stan: najpierw drugie, trzecie czwarty, piąte, szóstego, siódme, kolejnego, ósmego</span><span class="sxs-lookup"><span data-stu-id="1b902-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="1b902-159">Ignition_status</span><span class="sxs-lookup"><span data-stu-id="1b902-159">Ignition_status</span></span> |<span data-ttu-id="1b902-160">Wskazuje, czy hello vehicle jest uruchomiona lub zatrzymana</span><span class="sxs-lookup"><span data-stu-id="1b902-160">Indicates whether hello vehicle is running or stopped</span></span> |<span data-ttu-id="1b902-161">Wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="1b902-161">True or False</span></span> |
| <span data-ttu-id="1b902-162">Windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="1b902-162">Windshield_wiper_status</span></span> |<span data-ttu-id="1b902-163">Wskazuje, czy Wycieraczka szyby hello jest wyłączone lub nie</span><span class="sxs-lookup"><span data-stu-id="1b902-163">Indicates whether hello windshield wiper is turned or not</span></span> |<span data-ttu-id="1b902-164">Wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="1b902-164">True or False</span></span> |
| <span data-ttu-id="1b902-165">ABS</span><span class="sxs-lookup"><span data-stu-id="1b902-165">ABS</span></span> |<span data-ttu-id="1b902-166">Wskazuje, czy ABS prowadzi lub nie</span><span class="sxs-lookup"><span data-stu-id="1b902-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="1b902-167">Wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="1b902-167">True or False</span></span> |
| <span data-ttu-id="1b902-168">Znacznik czasu</span><span class="sxs-lookup"><span data-stu-id="1b902-168">Timestamp</span></span> |<span data-ttu-id="1b902-169">Witaj sygnatury czasowej po utworzeniu hello punktu danych.</span><span class="sxs-lookup"><span data-stu-id="1b902-169">hello timestamp when hello data point is created</span></span> |<span data-ttu-id="1b902-170">Date</span><span class="sxs-lookup"><span data-stu-id="1b902-170">Date</span></span> |
| <span data-ttu-id="1b902-171">Miasto</span><span class="sxs-lookup"><span data-stu-id="1b902-171">City</span></span> |<span data-ttu-id="1b902-172">Lokalizacja Hello pojazdów hello</span><span class="sxs-lookup"><span data-stu-id="1b902-172">hello location of hello vehicle</span></span> |<span data-ttu-id="1b902-173">4 miejscowości, w tym rozwiązaniu: Bellevue, Redmond, Sammamish, Seattle</span><span class="sxs-lookup"><span data-stu-id="1b902-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="1b902-174">Hello vehicle modelu odwołanie dataset zawiera mapowania modelu toohello VIN.</span><span class="sxs-lookup"><span data-stu-id="1b902-174">hello vehicle model reference dataset contains VIN toohello model mapping.</span></span> 

| <span data-ttu-id="1b902-175">VIN</span><span class="sxs-lookup"><span data-stu-id="1b902-175">VIN</span></span> | <span data-ttu-id="1b902-176">Model</span><span class="sxs-lookup"><span data-stu-id="1b902-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="1b902-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="1b902-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="1b902-178">Limuzyna</span><span class="sxs-lookup"><span data-stu-id="1b902-178">Sedan</span></span> |
| <span data-ttu-id="1b902-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="1b902-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="1b902-180">Połączenie hybrydowe</span><span class="sxs-lookup"><span data-stu-id="1b902-180">Hybrid</span></span> |
| <span data-ttu-id="1b902-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="1b902-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="1b902-182">Rodziny zamknięte</span><span class="sxs-lookup"><span data-stu-id="1b902-182">Family Saloon</span></span> |
| <span data-ttu-id="1b902-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="1b902-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="1b902-184">Limuzyna</span><span class="sxs-lookup"><span data-stu-id="1b902-184">Sedan</span></span> |
| <span data-ttu-id="1b902-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="1b902-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="1b902-186">Połączenie hybrydowe</span><span class="sxs-lookup"><span data-stu-id="1b902-186">Hybrid</span></span> |
| <span data-ttu-id="1b902-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="1b902-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="1b902-188">Rodziny zamknięte</span><span class="sxs-lookup"><span data-stu-id="1b902-188">Family Saloon</span></span> |
| <span data-ttu-id="1b902-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="1b902-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="1b902-190">Limuzyna</span><span class="sxs-lookup"><span data-stu-id="1b902-190">Sedan</span></span> |
| <span data-ttu-id="1b902-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="1b902-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="1b902-192">Połączenie hybrydowe</span><span class="sxs-lookup"><span data-stu-id="1b902-192">Hybrid</span></span> |
| <span data-ttu-id="1b902-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="1b902-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="1b902-194">Rodziny zamknięte</span><span class="sxs-lookup"><span data-stu-id="1b902-194">Family Saloon</span></span> |
| <span data-ttu-id="1b902-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="1b902-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="1b902-196">Możliwe do przekonwertowania</span><span class="sxs-lookup"><span data-stu-id="1b902-196">Convertible</span></span> |
| <span data-ttu-id="1b902-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="1b902-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="1b902-198">Kombi</span><span class="sxs-lookup"><span data-stu-id="1b902-198">Station Wagon</span></span> |
| <span data-ttu-id="1b902-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="1b902-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="1b902-200">Samochód kompaktowy</span><span class="sxs-lookup"><span data-stu-id="1b902-200">Compact Car</span></span> |
| <span data-ttu-id="1b902-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="1b902-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="1b902-202">Mała SUV</span><span class="sxs-lookup"><span data-stu-id="1b902-202">Small SUV</span></span> |
| <span data-ttu-id="1b902-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="1b902-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="1b902-204">Samochodu sportowych</span><span class="sxs-lookup"><span data-stu-id="1b902-204">Sports Car</span></span> |
| <span data-ttu-id="1b902-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="1b902-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="1b902-206">Średnia SUV</span><span class="sxs-lookup"><span data-stu-id="1b902-206">Medium SUV</span></span> |
| <span data-ttu-id="1b902-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="1b902-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="1b902-208">Kombi</span><span class="sxs-lookup"><span data-stu-id="1b902-208">Station Wagon</span></span> |
| <span data-ttu-id="1b902-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="1b902-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="1b902-210">Duże SUV</span><span class="sxs-lookup"><span data-stu-id="1b902-210">Large SUV</span></span> |
| <span data-ttu-id="1b902-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="1b902-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="1b902-212">Duże SUV</span><span class="sxs-lookup"><span data-stu-id="1b902-212">Large SUV</span></span> |
| <span data-ttu-id="1b902-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="1b902-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="1b902-214">Coupe</span><span class="sxs-lookup"><span data-stu-id="1b902-214">Coupe</span></span> |
| <span data-ttu-id="1b902-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="1b902-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="1b902-216">Limuzyna</span><span class="sxs-lookup"><span data-stu-id="1b902-216">Sedan</span></span> |
| <span data-ttu-id="1b902-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="1b902-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="1b902-218">Połączenie hybrydowe</span><span class="sxs-lookup"><span data-stu-id="1b902-218">Hybrid</span></span> |
| <span data-ttu-id="1b902-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="1b902-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="1b902-220">Rodziny zamknięte</span><span class="sxs-lookup"><span data-stu-id="1b902-220">Family Saloon</span></span> |
| <span data-ttu-id="1b902-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="1b902-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="1b902-222">Limuzyna</span><span class="sxs-lookup"><span data-stu-id="1b902-222">Sedan</span></span> |
| <span data-ttu-id="1b902-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="1b902-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="1b902-224">Połączenie hybrydowe</span><span class="sxs-lookup"><span data-stu-id="1b902-224">Hybrid</span></span> |
| <span data-ttu-id="1b902-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="1b902-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="1b902-226">Rodziny zamknięte</span><span class="sxs-lookup"><span data-stu-id="1b902-226">Family Saloon</span></span> |
| <span data-ttu-id="1b902-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="1b902-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="1b902-228">Limuzyna</span><span class="sxs-lookup"><span data-stu-id="1b902-228">Sedan</span></span> |
| <span data-ttu-id="1b902-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="1b902-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="1b902-230">Połączenie hybrydowe</span><span class="sxs-lookup"><span data-stu-id="1b902-230">Hybrid</span></span> |
| <span data-ttu-id="1b902-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="1b902-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="1b902-232">Rodziny zamknięte</span><span class="sxs-lookup"><span data-stu-id="1b902-232">Family Saloon</span></span> |
| <span data-ttu-id="1b902-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="1b902-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="1b902-234">Możliwe do przekonwertowania</span><span class="sxs-lookup"><span data-stu-id="1b902-234">Convertible</span></span> |
| <span data-ttu-id="1b902-235">…….</span><span class="sxs-lookup"><span data-stu-id="1b902-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="1b902-236">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="1b902-236">References</span></span>
[<span data-ttu-id="1b902-237">Rozwiązanie programu Visual Studio symulatora telematyki vehicle</span><span class="sxs-lookup"><span data-stu-id="1b902-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="1b902-238">Centrum zdarzeń platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1b902-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="1b902-239">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1b902-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="1b902-240">Wprowadzanie</span><span class="sxs-lookup"><span data-stu-id="1b902-240">Ingestion</span></span>
<span data-ttu-id="1b902-241">Kombinacje Azure Event Hubs, Stream Analytics i fabryki danych są wykorzystywane tooingest hello vehicle sygnałów, hello zdarzeń diagnostycznych, w czasie rzeczywistym i partii analytics.</span><span class="sxs-lookup"><span data-stu-id="1b902-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged tooingest hello vehicle signals, hello diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="1b902-242">Wszystkie te składniki są tworzone i skonfigurowany jako część hello wdrażania rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="1b902-242">All these components are created and configured as part of hello solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="1b902-243">Analiza w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="1b902-243">Real-time analysis</span></span>
<span data-ttu-id="1b902-244">Witaj zdarzenia generowane przez hello Vehicle telematyki symulatora są publikowane za pomocą Centrum zdarzeń toohello hello SDK Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="1b902-244">hello events generated by hello Vehicle Telematics Simulator are published toohello Event Hub using hello Event Hub SDK.</span></span> <span data-ttu-id="1b902-245">Zadanie usługi Stream Analytics Hello wysyła strumień te zdarzenia z hello Centrum zdarzeń i danych w czasie rzeczywistym tooanalyze hello vehicle kondycji hello procesów.</span><span class="sxs-lookup"><span data-stu-id="1b902-245">hello Stream Analytics job ingests these events from hello Event Hub and processes hello data in real time tooanalyze hello vehicle health.</span></span> 

![Pulpit nawigacyjny Centrum zdarzeń](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="1b902-247">*Rysunek 4 - pulpit nawigacyjny Centrum zdarzeń*</span><span class="sxs-lookup"><span data-stu-id="1b902-247">*Figure 4 - Event Hub dashboard*</span></span>

![Dane przetwarzania zadania usługi analiza strumienia](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="1b902-249">*Rysunek 5. zadania usługi analiza strumienia przetwarzania danych*</span><span class="sxs-lookup"><span data-stu-id="1b902-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="1b902-250">zadanie Stream Analytics Hello;</span><span class="sxs-lookup"><span data-stu-id="1b902-250">hello Stream Analytics job;</span></span>

* <span data-ttu-id="1b902-251">wysyła strumień danych z hello Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="1b902-251">ingests data from hello Event Hub</span></span> 
* <span data-ttu-id="1b902-252">wykonuje sprzężenie z hello odwołanie toomap hello vehicle VIN toohello odpowiedni model danych</span><span class="sxs-lookup"><span data-stu-id="1b902-252">performs a join with hello reference data toomap hello vehicle VIN toohello corresponding model</span></span> 
* <span data-ttu-id="1b902-253">są utrwalane w magazynie obiektów blob platformy Azure dla analizach wsadowych sformatowanego.</span><span class="sxs-lookup"><span data-stu-id="1b902-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="1b902-254">powitania po zapytań usługi Stream Analytics jest używane toopersist hello dane do magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1b902-254">hello following Stream Analytics query is used toopersist hello data into Azure blob storage.</span></span> 

![Zapytanie dotyczące zadań analizy strumienia dla wprowadzanie danych](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="1b902-256">*Rysunek 6 - analiza strumienia zadania zapytania na wprowadzanie danych*</span><span class="sxs-lookup"><span data-stu-id="1b902-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="1b902-257">Analiza partii</span><span class="sxs-lookup"><span data-stu-id="1b902-257">Batch analysis</span></span>
<span data-ttu-id="1b902-258">Możemy również generowania woluminów sygnały symulowane vehicle i diagnostycznych zestawu danych dla bardziej zaawansowane funkcje analizy partii.</span><span class="sxs-lookup"><span data-stu-id="1b902-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="1b902-259">Jest to wymagane tooensure wolumin danych reprezentatywnych dla przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="1b902-259">This is required tooensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="1b902-260">W tym celu używamy potoku o nazwie "PrepareSampleDataPipeline" w toogenerate przepływu pracy fabryki danych Azure hello wartość jednego roku sygnały symulowane vehicle i zestawu danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="1b902-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in hello Azure Data Factory workflow toogenerate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="1b902-261">Kliknij przycisk [działania niestandardowego fabryki danych](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello niestandardowego działania DotNet rozwiązania Visual Studio dla dostosowania fabryki danych zgodnie z wymaganiami.</span><span class="sxs-lookup"><span data-stu-id="1b902-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![Przygotowanie przykładowych danych do przepływu pracy przetwarzania wsadowego](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="1b902-263">*Rysunek 7 — przygotowanie przykładowych danych do przepływu pracy przetwarzania wsadowego*</span><span class="sxs-lookup"><span data-stu-id="1b902-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="1b902-264">potok Hello składa się z niestandardowych .net ADF działania, Pokaż tutaj:</span><span class="sxs-lookup"><span data-stu-id="1b902-264">hello pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![Działanie PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="1b902-266">*Rysunek 8 - PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="1b902-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="1b902-267">Po potoku hello wykonuje pomyślnie i zestawu danych "RawCarEventsTable" jest oznaczona jako "Gotowe", jednego roku warto symulowane vehicle sygnałów oraz diagnostyki danych są tworzone.</span><span class="sxs-lookup"><span data-stu-id="1b902-267">Once hello pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="1b902-268">Zobacz następujące hello utworzone na Twoim koncie magazynu w kontenerze "connectedcar" hello plików i folderów:</span><span class="sxs-lookup"><span data-stu-id="1b902-268">You see hello following folder and file created in your storage account under hello "connectedcar" container:</span></span>

![Dane wyjściowe PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="1b902-270">*Rysunek 9 - PrepareSampleDataPipeline danych wyjściowych*</span><span class="sxs-lookup"><span data-stu-id="1b902-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="1b902-271">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="1b902-271">References</span></span>
[<span data-ttu-id="1b902-272">Azure SDK Centrum zdarzeń pozyskiwania strumieni</span><span class="sxs-lookup"><span data-stu-id="1b902-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="1b902-273">[Możliwości przenoszenia danych fabryki danych platformy Azure](../data-factory/data-factory-data-movement-activities.md)
[działania DotNet fabryki danych Azure](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="1b902-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="1b902-274">Rozwiązanie programu visual studio działania DotNet fabryki danych Azure przygotowania przykładowe dane</span><span class="sxs-lookup"><span data-stu-id="1b902-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a><span data-ttu-id="1b902-275">Zestaw danych hello partycji</span><span class="sxs-lookup"><span data-stu-id="1b902-275">Partition hello dataset</span></span>
<span data-ttu-id="1b902-276">sygnały raw vehicle częściowo ustrukturyzowanych Hello i zestawu danych diagnostycznych są dzielone w kroku przygotowania danych hello na format rok i miesiąc.</span><span class="sxs-lookup"><span data-stu-id="1b902-276">hello raw semi-structured vehicle signals and diagnostic dataset are partitioned in hello data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="1b902-277">Tym partycjonowanie wspiera efektywniejsze wykonywanie zapytania i skalowalności magazynu długoterminowego przez włączenie błędów w tryb failover z jednego obiektu blob konta toohello obok jako pierwsze konto hello wypełnia.</span><span class="sxs-lookup"><span data-stu-id="1b902-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account toohello next as hello first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="1b902-278">Ten krok w rozwiązaniu hello jest stosowane tylko toobatch przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="1b902-278">This step in hello solution is applicable only toobatch processing.</span></span>

<span data-ttu-id="1b902-279">Wejście i wyjście danych zarządzania danymi:</span><span class="sxs-lookup"><span data-stu-id="1b902-279">Input and output data data management:</span></span>

* <span data-ttu-id="1b902-280">Witaj **dane wyjściowe** (etykietą *PartitionedCarEventsTable*) toobe pozostaje długi okres czasu jako formularz podstawowych / "rawest" hello danych w powitania klienta "Data Lake".</span><span class="sxs-lookup"><span data-stu-id="1b902-280">hello **output data** (labeled *PartitionedCarEventsTable*) is toobe kept for a long period of time as hello foundational/"rawest" form of data in hello customer's "Data Lake".</span></span> 
* <span data-ttu-id="1b902-281">Witaj **dane wejściowe** potoku toothis zwykle będą usunięte, ponieważ dane wyjściowe hello ma toohello pełnej rozdzielczości danych wejściowych — wystarczy znajduje (podzielona na partycje) lepiej dla dalszego wykorzystania.</span><span class="sxs-lookup"><span data-stu-id="1b902-281">hello **input data** toothis pipeline would typically be discarded as hello output data has full fidelity toohello input - it's just stored (partitioned) better for subsequent use.</span></span>

![Przepływ pracy zdarzenia samochodu partycji](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="1b902-283">*Rysunek 10 — przepływ pracy zdarzenia samochodu partycji*</span><span class="sxs-lookup"><span data-stu-id="1b902-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="1b902-284">dane pierwotne Hello jest podzielona na partycje przy użyciu działania Hive HDInsight w "PartitionCarEventsPipeline".</span><span class="sxs-lookup"><span data-stu-id="1b902-284">hello raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="1b902-285">ROK i miesiąc partycjonowanego Hello przykładowych danych wygenerowanych w kroku 1 rok.</span><span class="sxs-lookup"><span data-stu-id="1b902-285">hello sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="1b902-286">partycje Hello są używane toogenerate vehicle sygnały i danych diagnostycznych dla każdego miesiąca roku (całkowita liczba partycji 12).</span><span class="sxs-lookup"><span data-stu-id="1b902-286">hello partitions are used toogenerate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![Działanie PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="1b902-288">*Rysunek 11 — PartitionCarEventsPipeline*</span><span class="sxs-lookup"><span data-stu-id="1b902-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="1b902-289">***Skryptu PartitionConnectedCarEvents Hive***</span><span class="sxs-lookup"><span data-stu-id="1b902-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="1b902-290">Witaj poniższy skrypt Hive, o nazwie "partitioncarevents.hql" służy do partycjonowania i znajduje się w folderze "\demo\src\connectedcar\scripts" hello zip hello pobrane.</span><span class="sxs-lookup"><span data-stu-id="1b902-290">hello following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in hello "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

<span data-ttu-id="1b902-291">Po pomyślnym wykonaniu potoku hello zapoznaj się hello następujące partycje generowane na koncie magazynu w kontenerze "connectedcar" hello.</span><span class="sxs-lookup"><span data-stu-id="1b902-291">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Dane wyjściowe podzielonym na partycje](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="1b902-293">*Rysunek 12 — partycjonowanej danych wyjściowych*</span><span class="sxs-lookup"><span data-stu-id="1b902-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="1b902-294">dane Hello jest zoptymalizowane, jest bardziej łatwe w zarządzaniu i gotowa do dalszego przetwarzania toogain partii bogate informacje na temat technologii.</span><span class="sxs-lookup"><span data-stu-id="1b902-294">hello data is now optimized, is more manageable and ready for further processing toogain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="1b902-295">Analiza danych</span><span class="sxs-lookup"><span data-stu-id="1b902-295">Data Analysis</span></span>
<span data-ttu-id="1b902-296">W tej sekcji, zobaczysz, jak zaawansowane toocombine Azure Stream Analytics, usługi Azure Machine Learning fabryki danych Azure i usłudze Azure HDInsight dla zaawansowanej analizy kondycji vehicle i wspierającym zwyczaje.</span><span class="sxs-lookup"><span data-stu-id="1b902-296">In this section, you see how toocombine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="1b902-297">Istnieją trzy podpunkty tutaj:</span><span class="sxs-lookup"><span data-stu-id="1b902-297">There are three subsections here:</span></span>

1. <span data-ttu-id="1b902-298">**Machine Learning**: ta podsekcja zawiera informacje na temat hello eksperymentu wykrywania anomalii, użytymi w tym pojazdów toopredict rozwiązania wymagające obsługi konserwacji i pojazdów odwołania powodu toosafety problemy wymagające.</span><span class="sxs-lookup"><span data-stu-id="1b902-298">**Machine Learning**: This subsection contains information on hello anomaly detection experiment that we have used in this solution toopredict vehicles requiring servicing maintenance and vehicles requiring recalls due toosafety issues.</span></span>
2. <span data-ttu-id="1b902-299">**W czasie rzeczywistym analizy**: ta podsekcja zawiera informacje dotyczące analiz w czasie rzeczywistym hello przy użyciu hello język zapytań usługi analiza strumienia i operacyjnych uczenia maszynowego hello eksperymentu w czasie rzeczywistym za pomocą aplikacji niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="1b902-299">**Real-time analysis**: This subsection contains information regarding hello real-time analytics using hello Stream Analytics Query Language and operationalizing hello machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="1b902-300">**Partii analizy**: ta podsekcja zawiera informacje dotyczące hello, przekształcanie i przetwarzania danych partii hello przy użyciu usługi Azure HDInsight i usługi Azure Machine Learning operationalized przez fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="1b902-300">**Batch analysis**: This subsection contains information regarding hello transforming and processing of hello batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="1b902-301">Usługa Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1b902-301">Machine Learning</span></span>
<span data-ttu-id="1b902-302">Naszym celem jest pojazdów hello toopredict, które wymagają konserwacji lub wycofania oparte na niektórych statystyki kondycji.</span><span class="sxs-lookup"><span data-stu-id="1b902-302">Our goal here is toopredict hello vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="1b902-303">Wykonujemy powitania po założenia</span><span class="sxs-lookup"><span data-stu-id="1b902-303">We make hello following assumptions</span></span>

* <span data-ttu-id="1b902-304">Jeśli jeden z hello następujące trzy warunki są spełnione, wymagają pojazdów hello **obsługi konserwacji**:</span><span class="sxs-lookup"><span data-stu-id="1b902-304">If one of hello following three conditions are true, hello vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="1b902-305">Brakuje opona wykorzystania</span><span class="sxs-lookup"><span data-stu-id="1b902-305">Tire pressure is low</span></span>
  * <span data-ttu-id="1b902-306">Brakuje wydobycie ropy naftowej aparatu</span><span class="sxs-lookup"><span data-stu-id="1b902-306">Engine oil level is low</span></span>
  * <span data-ttu-id="1b902-307">Aparat temperatury jest wysoka</span><span class="sxs-lookup"><span data-stu-id="1b902-307">Engine temperature is high</span></span>
* <span data-ttu-id="1b902-308">Jeśli jeden z hello następujące warunki są spełnione, może być pojazdów hello **problem bezpieczeństwa** i wymagają **odwołania**:</span><span class="sxs-lookup"><span data-stu-id="1b902-308">If one of hello following conditions are true, hello vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="1b902-309">Aparat temperatury jest wysoka, ale brakuje poza temperatury</span><span class="sxs-lookup"><span data-stu-id="1b902-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="1b902-310">Aparat temperatury jest niska, ale poza temperatury jest wysoka</span><span class="sxs-lookup"><span data-stu-id="1b902-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="1b902-311">Na podstawie hello poprzedniej wymagań, został utworzony dwóch osobnych modeli toodetect anomalii: jeden vehicle obsługi wykrywania i jeden do wykrywania odwołania pojazdów.</span><span class="sxs-lookup"><span data-stu-id="1b902-311">Based on hello previous requirements, we have created two separate models toodetect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="1b902-312">W obu tych modeli hello wbudowanych algorytm analizy składnik główny (PCA) służy do wykrywania anomalii.</span><span class="sxs-lookup"><span data-stu-id="1b902-312">In both these models, hello built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="1b902-313">**Model wykrywania konserwacji**</span><span class="sxs-lookup"><span data-stu-id="1b902-313">**Maintenance detection model**</span></span>

<span data-ttu-id="1b902-314">Jeśli jeden z trzech wskaźniki opona wykorzystania, aparat wydobycie ropy naftowej lub temperatury aparat — spełniał stanu odpowiednich, model wykrywania konserwacji hello raporty anomalii.</span><span class="sxs-lookup"><span data-stu-id="1b902-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, hello maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="1b902-315">W związku z tym tylko potrzebujemy tooconsider te trzy zmienne w budynku hello modelu.</span><span class="sxs-lookup"><span data-stu-id="1b902-315">As a result, we only need tooconsider these three variables in building hello model.</span></span> <span data-ttu-id="1b902-316">W naszym eksperymentu w usłudze Azure Machine Learning, najpierw używamy **Select Columns in Dataset** tooextract modułu tych trzech zmiennych.</span><span class="sxs-lookup"><span data-stu-id="1b902-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module tooextract these three variables.</span></span> <span data-ttu-id="1b902-317">Następnie użyć hello anomalii oparte na PCA wykrywania modułu toobuild hello anomalii wykrywania modelu.</span><span class="sxs-lookup"><span data-stu-id="1b902-317">Next we use hello PCA-based anomaly detection module toobuild hello anomaly detection model.</span></span> 

<span data-ttu-id="1b902-318">Podmiot zabezpieczeń składnika analiza (PCA) to technikę ustalonych w uczeniu maszynowym, które mogą być zastosowane toofeature zaznaczenia, klasyfikacji i anomalii wykrywania.</span><span class="sxs-lookup"><span data-stu-id="1b902-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied toofeature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="1b902-319">PCA Konwertuje zestaw przypadku zawierającego prawdopodobnie skorelowane zmienne, do wartości o nazwie główne składniki.</span><span class="sxs-lookup"><span data-stu-id="1b902-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="1b902-320">Hello klucza informacje o tym, na podstawie PCA modelowania jest tooproject danych na małe wymiarowej miejsca, aby funkcje i anomalie, można łatwiej zidentyfikować.</span><span class="sxs-lookup"><span data-stu-id="1b902-320">hello key idea of PCA-based modeling is tooproject data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="1b902-321">Dla każdego nowego wprowadzania hello zbyt model wykrywania, wykrywanie anomalii hello najpierw oblicza swojej projekcji na powitania eigenvectors, a następnie oblicza hello znormalizowany błąd odbudowy.</span><span class="sxs-lookup"><span data-stu-id="1b902-321">For each new input too hello detection model, hello anomaly detector first computes its projection on hello eigenvectors, and then computes hello normalized reconstruction error.</span></span> <span data-ttu-id="1b902-322">Ten błąd znormalizowane jest hello anomalii wynik.</span><span class="sxs-lookup"><span data-stu-id="1b902-322">This normalized error is hello anomaly score.</span></span> <span data-ttu-id="1b902-323">Hello wyższej hello błąd hello więcej nietypowe wystąpienia hello jest.</span><span class="sxs-lookup"><span data-stu-id="1b902-323">hello higher hello error, hello more anomalous hello instance is.</span></span> 

<span data-ttu-id="1b902-324">Hello obsługi wykrywania problem każdy rekord jest uznawana za ustalony punktu 3-wymiarową przestrzeni opona wykorzystania, aparat wydobycie ropy naftowej i temperatury aparat współrzędnych.</span><span class="sxs-lookup"><span data-stu-id="1b902-324">In hello maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="1b902-325">toocapture tych nieprawidłowości możemy projektu hello oryginalne dane przestrzeni 3-wymiarową hello na 2-wymiarową miejsca, przy użyciu PCA.</span><span class="sxs-lookup"><span data-stu-id="1b902-325">toocapture these anomalies, we can project hello original data in hello 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="1b902-326">W związku z tym możemy ustawić parametr hello liczby składników toouse w PCA toobe 2.</span><span class="sxs-lookup"><span data-stu-id="1b902-326">Thus, we set hello parameter Number of components toouse in PCA toobe 2.</span></span> <span data-ttu-id="1b902-327">Ten parametr odgrywa ważną rolę w stosowaniu wykrywania anomalii oparte na PCA.</span><span class="sxs-lookup"><span data-stu-id="1b902-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="1b902-328">Po zakończeniu operacji przewidywania danych przy użyciu PCA możemy łatwiej ustalić tych nieprawidłowości.</span><span class="sxs-lookup"><span data-stu-id="1b902-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="1b902-329">**Model wykrywania anomalii odwołania** w model wykrywania anomalii odwołania hello używamy hello Select Columns in Dataset i anomalii oparte na PCA modułów wykrywania w podobny sposób.</span><span class="sxs-lookup"><span data-stu-id="1b902-329">**Recall anomaly detection model** In hello recall anomaly detection model, we use hello Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="1b902-330">W szczególności firma Microsoft najpierw wyodrębnić trzy zmienne - temperatury aparatu, poza temperatury i szybkość — przy użyciu hello **Select Columns in Dataset** modułu.</span><span class="sxs-lookup"><span data-stu-id="1b902-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using hello **Select Columns in Dataset** module.</span></span> <span data-ttu-id="1b902-331">Przeprowadzamy szybkości hello zmiennej, ponieważ temperatury aparat hello jest zwykle skorelowane toohello szybkości.</span><span class="sxs-lookup"><span data-stu-id="1b902-331">We also include hello speed variable since hello engine temperature typically is correlated toohello speed.</span></span> <span data-ttu-id="1b902-332">Następnie używamy anomalii oparte na PCA wykrywania modułu tooproject hello danych z 3-wymiarową obszaru hello do 2-wymiarowej.</span><span class="sxs-lookup"><span data-stu-id="1b902-332">Next we use PCA-based anomaly detection module tooproject hello data from hello 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="1b902-333">Hello odwołania kryteriami i hello vehicle wymaga odwołania gdy aparat temperatury i poza temperatury wysokiej negatywnie skorelowane.</span><span class="sxs-lookup"><span data-stu-id="1b902-333">hello recall criteria are satisfied and so hello vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="1b902-334">Za pomocą algorytmu wykrywania anomalii oparte na PCA, firma Microsoft przechwytywać anomalie hello po wykonaniu PCA.</span><span class="sxs-lookup"><span data-stu-id="1b902-334">Using PCA-based anomaly detection algorithm, we can capture hello anomalies after performing PCA.</span></span> 

<span data-ttu-id="1b902-335">Podczas uczenia modelu albo, potrzebujemy danych normalne toouse, które nie wymagają konserwacji lub wycofania jako model wykrywania anomalii oparte na PCA hello tootrain hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="1b902-335">When training either model, we need toouse normal data, which does not require maintenance or recall as hello input data tootrain hello PCA-based anomaly detection model.</span></span> <span data-ttu-id="1b902-336">W hello oceniania eksperymentu używamy toodetect model wykrywania anomalii hello uczony czy hello vehicle wymaga konserwacji lub wycofania.</span><span class="sxs-lookup"><span data-stu-id="1b902-336">In hello scoring experiment, we use hello trained anomaly detection model toodetect whether or not hello vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="1b902-337">Analiza w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="1b902-337">Real-time analysis</span></span>
<span data-ttu-id="1b902-338">następujące zapytanie SQL Stream Analytics Hello jest używany tooget średnią hello wszystkich hello ważny parametry, takie jak prędkość, poziom paliwa temperatury aparatu, odczytu licznika, opona wykorzystania, aparatu wydobycie ropy naftowej i inne.</span><span class="sxs-lookup"><span data-stu-id="1b902-338">hello following Stream Analytics SQL Query is used tooget hello average of all hello important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="1b902-339">Witaj średnie są używane toodetect anomalii, wydawania alertów i określić hello ogólnej kondycji warunki pojazdów obsługiwane w określonym regionie i skorelowania go po toodemographics.</span><span class="sxs-lookup"><span data-stu-id="1b902-339">hello averages are used toodetect anomalies, issue alerts, and determine hello overall health conditions of vehicles operated in specific region and then correlate it toodemographics.</span></span> 

![Stream Analytics zapytania do przetworzenia w czasie rzeczywistym](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="1b902-341">*Rysunek 13 — zapytań usługi Stream Analytics do przetworzenia w czasie rzeczywistym*</span><span class="sxs-lookup"><span data-stu-id="1b902-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="1b902-342">Wszystkie średnie hello są obliczane przez TumblingWindow 3 sekundy.</span><span class="sxs-lookup"><span data-stu-id="1b902-342">All hello averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="1b902-343">Użyto TubmlingWindow w takim przypadku ponieważ wymagamy przedziały czasu nienakładający, jak i ciągłe.</span><span class="sxs-lookup"><span data-stu-id="1b902-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="1b902-344">Kliknij toolearn więcej informacji na temat wszystkie funkcje "Okien" hello, w systemie Azure Stream Analytics [okien (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b902-344">toolearn more about all hello "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="1b902-345">**Prognozowanie w czasie rzeczywistym**</span><span class="sxs-lookup"><span data-stu-id="1b902-345">**Real-time prediction**</span></span>

<span data-ttu-id="1b902-346">Aplikacja jest częścią modelu uczenia maszynowego hello toooperationalize rozwiązania hello w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="1b902-346">An application is included as part of hello solution toooperationalize hello machine learning model in real time.</span></span> <span data-ttu-id="1b902-347">Ta aplikacja o nazwie "RealTimeDashboardApp" zostało utworzone i skonfigurowane jako część wdrożenia rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="1b902-347">This application called “RealTimeDashboardApp” is created and configured as part of hello solution deployment.</span></span> <span data-ttu-id="1b902-348">Aplikacja Hello wykonuje następujące hello:</span><span class="sxs-lookup"><span data-stu-id="1b902-348">hello application performs hello following:</span></span>

1. <span data-ttu-id="1b902-349">Wykrywa tooan Centrum zdarzeń wystąpienia których Stream Analytics jest publikowania hello zdarzeń we wzorcu stale.</span><span class="sxs-lookup"><span data-stu-id="1b902-349">Listens tooan Event Hub instance where Stream Analytics is publishing hello events in a pattern continuously.</span></span> <span data-ttu-id="1b902-350">![Stream Analytics zapytania do publikowania danych hello](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *rysunek 14 — zapytań usługi Stream Analytics publikowania hello tooan danych wyjściowych Centrum zdarzeń wystąpienia*</span><span class="sxs-lookup"><span data-stu-id="1b902-350">![Stream Analytics query for publishing hello data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing hello data tooan output Event Hub instance*</span></span> 
2. <span data-ttu-id="1b902-351">Dla każdego zdarzenia, które otrzymuje tej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="1b902-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="1b902-352">Procesy hello danych przy użyciu punktu końcowego Machine Learning żądań i odpowiedzi oceniania (RR).</span><span class="sxs-lookup"><span data-stu-id="1b902-352">Processes hello data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="1b902-353">punkt końcowy RR Hello jest automatycznie publikowany jako część wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="1b902-353">hello RRS endpoint is automatically published as part of hello deployment.</span></span>
   * <span data-ttu-id="1b902-354">dane wyjściowe RR Hello jest wypychania hello interfejsów API usługi Power BI tooa opublikowanych w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="1b902-354">hello RRS output is published tooa Power BI dataset using hello push APIs.</span></span>

<span data-ttu-id="1b902-355">Ten wzorzec jest również tooscenarios dotyczy mają toointegrate aplikacji biznesowych (LoB), z przepływem analiz w czasie rzeczywistym hello, dla scenariuszy, takich jak alerty, powiadomienia i wiadomości.</span><span class="sxs-lookup"><span data-stu-id="1b902-355">This pattern is also applicable tooscenarios in which you want toointegrate a Line of Business (LoB) application with hello real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="1b902-356">Kliknij przycisk [pobierania RealtimeDashboardApp](http://go.microsoft.com/fwlink/?LinkId=717078) hello toodownload RealtimeDashboardApp rozwiązania Visual Studio dostosowań.</span><span class="sxs-lookup"><span data-stu-id="1b902-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="1b902-357">**Witaj tooexecute w czasie rzeczywistym pulpitu nawigacyjnego aplikacji**</span><span class="sxs-lookup"><span data-stu-id="1b902-357">**tooexecute hello Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="1b902-358">Wyodrębnij i Zapisz lokalnie ![folderu RealtimeDashboardApp](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *rysunek 16 – RealtimeDashboardApp folderu*</span><span class="sxs-lookup"><span data-stu-id="1b902-358">Extract and save locally ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="1b902-359">Uruchom aplikację hello RealtimeDashboardApp.exe</span><span class="sxs-lookup"><span data-stu-id="1b902-359">Execute hello application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="1b902-360">Podaj prawidłowe poświadczenia usługi Power BI, zaloguj się i kliknij przycisk Akceptuj</span><span class="sxs-lookup"><span data-stu-id="1b902-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![W czasie rzeczywistym pulpit nawigacyjny aplikacji logowania tooPower analizy Biznesowej](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Logowania tooPower BI Zakończ w czasie rzeczywistym pulpitu nawigacyjnego aplikacji](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="1b902-363">*Rysunek 17 — RealtimeDashboardApp: Logowania tooPower analizy Biznesowej*</span><span class="sxs-lookup"><span data-stu-id="1b902-363">*Figure 17 – RealtimeDashboardApp: Sign-in tooPower BI*</span></span>

>[!NOTE] 
><span data-ttu-id="1b902-364">Zestaw danych usługi Power BI hello tooflush należy wykonać hello RealtimeDashboardApp z parametrem "flushdata" hello:</span><span class="sxs-lookup"><span data-stu-id="1b902-364">If you want tooflush hello Power BI dataset, execute hello RealtimeDashboardApp with hello "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="1b902-365">Analiza partii</span><span class="sxs-lookup"><span data-stu-id="1b902-365">Batch analysis</span></span>
<span data-ttu-id="1b902-366">Celem Hello jest tooshow jak Motors Contoso używa hello obliczeń platformy Azure możliwości tooharness danych big data toogain szczegółowe, bogate informacje na wzorzec, zachowanie użycia i kondycji pojazdów.</span><span class="sxs-lookup"><span data-stu-id="1b902-366">hello goal here is tooshow how Contoso Motors utilizes hello Azure compute capabilities tooharness big data toogain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="1b902-367">Dzięki temu możliwe:</span><span class="sxs-lookup"><span data-stu-id="1b902-367">This makes it possible to:</span></span>

* <span data-ttu-id="1b902-368">Udoskonalanie powitania klienta i zapewnić ich tańsze zapewniając wgląd na zwyczaje i wydajne zachowania pobudzenie paliwa</span><span class="sxs-lookup"><span data-stu-id="1b902-368">Improve hello customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="1b902-369">Dowiedz się więcej o klientów i ich pobudzenie decyzje biznesowe toogovern patters aktywnego i podaj hello najlepiej w klasie produktów i usług</span><span class="sxs-lookup"><span data-stu-id="1b902-369">Learn proactively about customers and their driving patters toogovern business decisions and provide hello best in class products & services</span></span>

<span data-ttu-id="1b902-370">W tym rozwiązaniu możemy przeznaczonych hello następujące metryki:</span><span class="sxs-lookup"><span data-stu-id="1b902-370">In this solution, we are targeting hello following metrics:</span></span>

1. <span data-ttu-id="1b902-371">**Agresywna zwiększają zachowanie**: identyfikuje trend hello hello modeli, lokalizacje pobudzenie warunki i czas hello roku toogain wgląd w bliskiej schematy.</span><span class="sxs-lookup"><span data-stu-id="1b902-371">**Aggressive driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on aggressive driving patterns.</span></span> <span data-ttu-id="1b902-372">Silniki contoso można używać tych insights kampanii marketingowych, nowe funkcje spersonalizowane i ubezpieczenia opartej na użyciu.</span><span class="sxs-lookup"><span data-stu-id="1b902-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="1b902-373">**Paliwa wydajne działanie pobudzenie**: identyfikuje trend hello hello modeli, lokalizacje pobudzenie warunki i czas hello roku toogain rozeznanie wydajne schematy paliwa.</span><span class="sxs-lookup"><span data-stu-id="1b902-373">**Fuel efficient driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="1b902-374">Silniki contoso można używać tych insights kampanii, zwiększają nowe funkcje i aktywne raportowania toohello sterowniki kosztów obowiązującej oraz środowisko przyjazne zwyczaje jazdy.</span><span class="sxs-lookup"><span data-stu-id="1b902-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting toohello drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="1b902-375">**Odwołaj modele**: identyfikuje modele wymagających odwołań przez operacyjnych hello eksperymentu uczenia maszynowego wykrywania anomalii</span><span class="sxs-lookup"><span data-stu-id="1b902-375">**Recall models**: Identifies models requiring recalls by operationalizing hello anomaly detection machine learning experiment</span></span>

<span data-ttu-id="1b902-376">Oto do hello szczegóły każdego z tych metryk</span><span class="sxs-lookup"><span data-stu-id="1b902-376">Let's look into hello details of each of these metrics,</span></span>

<span data-ttu-id="1b902-377">**Agresywne pobudzenie wzorca**</span><span class="sxs-lookup"><span data-stu-id="1b902-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="1b902-378">Hello sygnały vehicle podzielona na partycje i danych diagnostycznych są przetwarzane w potoku hello o nazwie "AggresiveDrivingPatternPipeline" przy użyciu modeli hello toodetermine Hive, lokalizacji, vehicle, zwiększają warunki oraz innych parametrów, które wykazuje aktywnego wzorzec jazdy.</span><span class="sxs-lookup"><span data-stu-id="1b902-378">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "AggresiveDrivingPatternPipeline" using Hive toodetermine hello models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="1b902-379">![Agresywne pobudzenie przepływu pracy wzorzec](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*rysunek 18 — agresywne pobudzenie przepływu pracy wzorca*</span><span class="sxs-lookup"><span data-stu-id="1b902-379">![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="1b902-380">***Agresywne kierowania zapytań Hive wzorca***</span><span class="sxs-lookup"><span data-stu-id="1b902-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="1b902-381">Hello skryptu Hive o nazwie "aggresivedriving.hql" używany do analizowania aktywnego wzorca warunku jazdy znajduje się w folderze "\demo\src\connectedcar\scripts" hello pobrane zip.</span><span class="sxs-lookup"><span data-stu-id="1b902-381">hello Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


<span data-ttu-id="1b902-382">Używa kombinacji hello vehicle w pozycji koło zębate transmisji, hamulca szkła stanu i szybkość toodetect reckless/agresywne zwiększają działanie hamowania wzorzec dużą prędkością.</span><span class="sxs-lookup"><span data-stu-id="1b902-382">It uses hello combination of vehicle's transmission gear position, brake pedal status, and speed toodetect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="1b902-383">Po pomyślnym wykonaniu potoku hello zapoznaj się hello następujące partycje generowane na koncie magazynu w kontenerze "connectedcar" hello.</span><span class="sxs-lookup"><span data-stu-id="1b902-383">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Dane wyjściowe AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="1b902-385">*Rysunek 19 — AggressiveDrivingPatternPipeline danych wyjściowych*</span><span class="sxs-lookup"><span data-stu-id="1b902-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="1b902-386">**Efektywne wzorzec pobudzenie paliwa**</span><span class="sxs-lookup"><span data-stu-id="1b902-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="1b902-387">Hello sygnały vehicle podzielona na partycje i danych diagnostycznych są przetwarzane w potoku hello o nazwie "FuelEfficientDrivingPatternPipeline".</span><span class="sxs-lookup"><span data-stu-id="1b902-387">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="1b902-388">Gałąź jest używane toodetermine hello modeli, lokalizacji vehicle, pobudzenie warunki i inne właściwości, które wykazują paliwa wydajne pobudzenie wzorca.</span><span class="sxs-lookup"><span data-stu-id="1b902-388">Hive is used toodetermine hello models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![Wzorzec pobudzenie obniżające zużycie paliwa](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="1b902-390">*Rysunek 20 – obniżające zużycie paliwa pobudzenie przepływu pracy wzorca*</span><span class="sxs-lookup"><span data-stu-id="1b902-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="1b902-391">***Paliwa wydajne pobudzenie wzorzec zapytań Hive***</span><span class="sxs-lookup"><span data-stu-id="1b902-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="1b902-392">Hello skryptu Hive o nazwie "fuelefficientdriving.hql" używany do analizowania aktywnego wzorca warunku jazdy znajduje się w folderze "\demo\src\connectedcar\scripts" hello pobrane zip.</span><span class="sxs-lookup"><span data-stu-id="1b902-392">hello Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


<span data-ttu-id="1b902-393">Wykorzystuje kombinację hello vehicle w pozycji koło zębate transmisji, stan szkła hamulca szybkość i paliwa toodetect szkła pozycji akceleratora wydajne działanie pobudzenie oparte na przyspieszenie hamowania, oraz przyspieszyć wzorce.</span><span class="sxs-lookup"><span data-stu-id="1b902-393">It uses hello combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position toodetect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="1b902-394">Po pomyślnym wykonaniu potoku hello zapoznaj się hello następujące partycje generowane na koncie magazynu w kontenerze "connectedcar" hello.</span><span class="sxs-lookup"><span data-stu-id="1b902-394">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Dane wyjściowe FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="1b902-396">*Rysunek 21 — FuelEfficientDrivingPatternPipeline danych wyjściowych*</span><span class="sxs-lookup"><span data-stu-id="1b902-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="1b902-397">**Operacje przewidywania dla odwołania**</span><span class="sxs-lookup"><span data-stu-id="1b902-397">**Recall Predictions**</span></span>

<span data-ttu-id="1b902-398">eksperymentu uczenia maszynowego Hello jest udostępniane i opublikowane jako usługi sieci web jako część wdrożenia rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="1b902-398">hello machine learning experiment is provisioned and published as a web service as part of hello solution deployment.</span></span> <span data-ttu-id="1b902-399">Witaj wsadowego oceniania punkt końcowy jest wykorzystywana w tym przepływie pracy, zarejestrowany jako usługa połączone fabryki danych i operationalized przy użyciu danych fabryki działanie wsadowego oceniania.</span><span class="sxs-lookup"><span data-stu-id="1b902-399">hello batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![Punkt końcowy Machine Learning](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="1b902-401">*Rysunek 22 — punktu końcowego uczenia maszynowego zarejestrowany jako połączonej usługi z fabryki danych*</span><span class="sxs-lookup"><span data-stu-id="1b902-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="1b902-402">Witaj zarejestrowanej połączonej usługi jest używany w hello DetectAnomalyPipeline tooscore hello danych przy użyciu modelu wykrywania anomalii hello.</span><span class="sxs-lookup"><span data-stu-id="1b902-402">hello registered linked service is used in hello DetectAnomalyPipeline tooscore hello data using hello anomaly detection model.</span></span> 

![Learning działanie wsadowego oceniania w fabryce danych komputera](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="1b902-404">*Rysunek 23 — działanie usługi Azure Machine Learning wsadowego oceniania z fabryki danych*</span><span class="sxs-lookup"><span data-stu-id="1b902-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="1b902-405">Istnieje kilka czynności wykonywanych w tym potoku w celu przygotowania danych, dzięki czemu mogą być operationalized z hello wsadowego oceniania usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="1b902-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with hello batch scoring web service.</span></span> 

![DetectAnomalyPipeline do prognozowania pojazdów wymagających odwołań](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="1b902-407">*Rysunek 24 — DetectAnomalyPipeline do prognozowania pojazdów wymagających odwołań*</span><span class="sxs-lookup"><span data-stu-id="1b902-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="1b902-408">***Zapytanie Hive wykrywania anomalii***</span><span class="sxs-lookup"><span data-stu-id="1b902-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="1b902-409">Po zakończeniu oceniania hello działanie HDInsight jest używane tooprocess i hello agregacji danych, które są sklasyfikowane jako anomalii przez model hello wynik prawdopodobieństwa: 0,60 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="1b902-409">Once hello scoring is completed, an HDInsight activity is used tooprocess and aggregate hello data that are categorized as anomalies by hello model with a probability score of 0.60 or higher.</span></span>

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


<span data-ttu-id="1b902-410">Po pomyślnym wykonaniu potoku hello zapoznaj się hello następujące partycje generowane na koncie magazynu w kontenerze "connectedcar" hello.</span><span class="sxs-lookup"><span data-stu-id="1b902-410">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Dane wyjściowe DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="1b902-412">*Rysunek 25 — DetectAnomalyPipeline danych wyjściowych*</span><span class="sxs-lookup"><span data-stu-id="1b902-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="1b902-413">Publikowanie</span><span class="sxs-lookup"><span data-stu-id="1b902-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="1b902-414">Analiza w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="1b902-414">Real-time analysis</span></span>
<span data-ttu-id="1b902-415">Jedną z hello kwerend w zadaniu Stream Analytics hello publikuje dane wyjściowe tooan zdarzenia hello wystąpienia Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="1b902-415">One of hello queries in hello Stream Analytics job publishes hello events tooan output Event Hub instance.</span></span> 

![Zadania usługi analiza strumienia publikuje dane wyjściowe tooan wystąpienia Centrum zdarzeń](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="1b902-417">*Rysunek 26 — zadanie usługi Stream Analytics publikuje dane wyjściowe tooan wystąpienia Centrum zdarzeń*</span><span class="sxs-lookup"><span data-stu-id="1b902-417">*Figure 26 – Stream Analytics job publishes tooan output Event Hub instance*</span></span>

![Stream Analytics query toopublish toohello output wystąpień Centrum zdarzeń](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="1b902-419">*Rysunek 27 — toohello toopublish zapytań usługi Stream Analytics output wystąpień Centrum zdarzeń*</span><span class="sxs-lookup"><span data-stu-id="1b902-419">*Figure 27 – Stream Analytics query toopublish toohello output Event Hub instance*</span></span>

<span data-ttu-id="1b902-420">Ten strumień zdarzeń jest używany przez powitalne RealTimeDashboardApp zawartych w rozwiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="1b902-420">This stream of events is consumed by hello RealTimeDashboardApp included in hello solution.</span></span> <span data-ttu-id="1b902-421">Ta aplikacja korzysta z usługi sieci web Machine Learning żądań i odpowiedzi hello wyników w czasie rzeczywistym i publikuje zestawu danych usługi Power BI tooa dane wynikowe hello zużycia.</span><span class="sxs-lookup"><span data-stu-id="1b902-421">This application leverages hello Machine Learning Request-Response web service for real-time scoring and publishes hello resultant data tooa Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="1b902-422">Analiza partii</span><span class="sxs-lookup"><span data-stu-id="1b902-422">Batch analysis</span></span>
<span data-ttu-id="1b902-423">wyniki Hello hello partii i przetwarzanie w czasie rzeczywistym są tabele bazy danych SQL Azure opublikowanych toohello zużycia.</span><span class="sxs-lookup"><span data-stu-id="1b902-423">hello results of hello batch and real-time processing are published toohello Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="1b902-424">Hello Azure SQL Server, bazy danych i tabele hello są tworzone automatycznie w ramach hello w skrypcie Instalatora.</span><span class="sxs-lookup"><span data-stu-id="1b902-424">hello Azure SQL Server, Database, and hello tables are created automatically as part of hello setup script.</span></span> 

![Przepływ pracy składnicy toodata skopiować wyniki przetwarzania wsadowego](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="1b902-426">*Rysunek 28 — przetwarzania przepływu składnicy toodata kopiowania wyników wsadowego*</span><span class="sxs-lookup"><span data-stu-id="1b902-426">*Figure 28 – Batch processing results copy toodata mart workflow*</span></span>

![Zadania usługi analiza strumienia publikuje składnicy toodata](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="1b902-428">*Rysunek 29 — zadanie usługi Stream Analytics publikuje składnicy toodata*</span><span class="sxs-lookup"><span data-stu-id="1b902-428">*Figure 29 – Stream Analytics job publishes toodata mart*</span></span>

![Ustawienie składnicy danych w zadaniu Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="1b902-430">*Rysunek 30 – składnicy danych ustawienie w zadaniu Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="1b902-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="1b902-431">Używanie</span><span class="sxs-lookup"><span data-stu-id="1b902-431">Consume</span></span>
<span data-ttu-id="1b902-432">Usługi Power BI pozwala to rozwiązanie sformatowanego pulpitu nawigacyjnego i analizy predykcyjnej wizualizacji danych w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="1b902-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="1b902-433">Kliknij tutaj, aby uzyskać szczegółowe instrukcje dotyczące konfigurowania raportów usługi Power BI hello i hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="1b902-433">Click here for detailed instructions on setting up hello Power BI reports and hello dashboard.</span></span> <span data-ttu-id="1b902-434">pulpit nawigacyjny końcowego Hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="1b902-434">hello final dashboard looks like this:</span></span>

![Pulpit nawigacyjny programu Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="1b902-436">*Rysunek 31 - pulpitu nawigacyjnego programu Power BI*</span><span class="sxs-lookup"><span data-stu-id="1b902-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="1b902-437">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="1b902-437">Summary</span></span>
<span data-ttu-id="1b902-438">Ten dokument zawiera szczegółowe przechodzenia z hello rozwiązania analizy Telemetrii pojazdów.</span><span class="sxs-lookup"><span data-stu-id="1b902-438">This document contains a detailed drill-down of hello Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="1b902-439">Ten wzorzec architektury lambda, dla których są wyświetlane w czasie rzeczywistym i partii analizy w usłudze prognoz i akcji.</span><span class="sxs-lookup"><span data-stu-id="1b902-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="1b902-440">Ten wzorzec stosuje tooa szeroką gamę przypadków użycia, które wymagają aktywnej ścieżki (w czasie rzeczywistym) i analiza zimnych ścieżki (partii).</span><span class="sxs-lookup"><span data-stu-id="1b902-440">This pattern applies tooa wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

