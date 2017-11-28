---
title: "Nowości do prognozowania vehicle kondycji i wspierającym zwyczaje - Azure | Dokumentacja firmy Microsoft"
description: "Korzystanie z możliwości Cortana Intelligence, aby uzyskać wgląd w czasie rzeczywistym oraz predykcyjnej na vehicle kondycji i wspierającym zwyczaje."
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
ms.openlocfilehash: 0a4dba58445cf0fd9fd8f51d443576bacd92251b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-the-solution"></a><span data-ttu-id="74c79-103">Podręcznik dotyczący rozwiązań analizy telemetrii pojazdów: szczegółowe informacje na temat rozwiązania</span><span class="sxs-lookup"><span data-stu-id="74c79-103">Vehicle telemetry analytics solution playbook: deep dive into the solution</span></span>
<span data-ttu-id="74c79-104">To **menu** łącza do sekcji tego podręcznika dotyczącego:</span><span class="sxs-lookup"><span data-stu-id="74c79-104">This **menu** links to the sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="74c79-105">Ta sekcja rozwija na każdym z etapów przedstawiono architekturę rozwiązania wraz z instrukcjami i wskaźniki do dostosowania.</span><span class="sxs-lookup"><span data-stu-id="74c79-105">This section drills down into each of the stages depicted in the Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="74c79-106">Źródła danych</span><span class="sxs-lookup"><span data-stu-id="74c79-106">Data Sources</span></span>
<span data-ttu-id="74c79-107">Rozwiązanie używa dwóch różnych źródeł danych:</span><span class="sxs-lookup"><span data-stu-id="74c79-107">The solution uses two different data sources:</span></span>

* <span data-ttu-id="74c79-108">**Symulowane sygnały vehicle i danych diagnostycznych** i</span><span class="sxs-lookup"><span data-stu-id="74c79-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="74c79-109">**vehicle katalogu**</span><span class="sxs-lookup"><span data-stu-id="74c79-109">**vehicle catalog**</span></span>

<span data-ttu-id="74c79-110">Symulator telematyki vehicle wchodzi w skład tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="74c79-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="74c79-111">Emituje informacje diagnostyczne, a sygnały odpowiadającego stanu mechanizm i kierowania wzorca w danym punkcie w czasie.</span><span class="sxs-lookup"><span data-stu-id="74c79-111">It emits diagnostic information and signals corresponding to the state of the vehicle and to the driving pattern at a given point in time.</span></span> <span data-ttu-id="74c79-112">Kliknij przycisk [symulatora telematyki Vehicle](http://go.microsoft.com/fwlink/?LinkId=717075) do pobrania **Vehicle telematyki symulatora rozwiązania Visual Studio** dostosowań, w zależności od wymagań.</span><span class="sxs-lookup"><span data-stu-id="74c79-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) to download the **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="74c79-113">Katalog vehicle zawiera odwołanie do zestawu danych VIN do mapowania modelu.</span><span class="sxs-lookup"><span data-stu-id="74c79-113">The vehicle catalog contains a reference dataset with a VIN to model mapping.</span></span>

![Symulator telematyki vehicle](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="74c79-115">*Rysunek 1 — Vehicle telematyki symulatora*</span><span class="sxs-lookup"><span data-stu-id="74c79-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="74c79-116">Jest to formacie JSON zestawu danych, który zawiera następujące schematu.</span><span class="sxs-lookup"><span data-stu-id="74c79-116">This is a JSON-formatted dataset that contains the following schema.</span></span>

| <span data-ttu-id="74c79-117">Kolumna</span><span class="sxs-lookup"><span data-stu-id="74c79-117">Column</span></span> | <span data-ttu-id="74c79-118">Opis</span><span class="sxs-lookup"><span data-stu-id="74c79-118">Description</span></span> | <span data-ttu-id="74c79-119">Wartości</span><span class="sxs-lookup"><span data-stu-id="74c79-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="74c79-120">VIN</span><span class="sxs-lookup"><span data-stu-id="74c79-120">VIN</span></span> |<span data-ttu-id="74c79-121">Losowo generowany numer identyfikacyjny</span><span class="sxs-lookup"><span data-stu-id="74c79-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="74c79-122">To są uzyskiwane ze wzorca listę 10 000 numery identyfikacyjne losowo generowany pojazdów.</span><span class="sxs-lookup"><span data-stu-id="74c79-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="74c79-123">Poza temperatury</span><span class="sxs-lookup"><span data-stu-id="74c79-123">Outside temperature</span></span> |<span data-ttu-id="74c79-124">Gdzie sterujące mechanizm temperatury na zewnątrz</span><span class="sxs-lookup"><span data-stu-id="74c79-124">The outside temperature where the vehicle is driving</span></span> |<span data-ttu-id="74c79-125">Losowo generowany numer od 0 do 100</span><span class="sxs-lookup"><span data-stu-id="74c79-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="74c79-126">Aparat temperatury</span><span class="sxs-lookup"><span data-stu-id="74c79-126">Engine temperature</span></span> |<span data-ttu-id="74c79-127">Aparat temperatury mechanizm</span><span class="sxs-lookup"><span data-stu-id="74c79-127">The engine temperature of the vehicle</span></span> |<span data-ttu-id="74c79-128">Losowo generowany numer od 0-500</span><span class="sxs-lookup"><span data-stu-id="74c79-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="74c79-129">Szybkość</span><span class="sxs-lookup"><span data-stu-id="74c79-129">Speed</span></span> |<span data-ttu-id="74c79-130">Szybkość aparatu, jaką mechanizm sterujące</span><span class="sxs-lookup"><span data-stu-id="74c79-130">The engine speed at which the vehicle is driving</span></span> |<span data-ttu-id="74c79-131">Losowo generowany numer od 0 do 100</span><span class="sxs-lookup"><span data-stu-id="74c79-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="74c79-132">Paliwa</span><span class="sxs-lookup"><span data-stu-id="74c79-132">Fuel</span></span> |<span data-ttu-id="74c79-133">Poziom paliwa mechanizm</span><span class="sxs-lookup"><span data-stu-id="74c79-133">The fuel level of the vehicle</span></span> |<span data-ttu-id="74c79-134">Losowo generowany numer od 0 do 100 (procent poziomu paliwa wskazuje)</span><span class="sxs-lookup"><span data-stu-id="74c79-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="74c79-135">EngineOil</span><span class="sxs-lookup"><span data-stu-id="74c79-135">EngineOil</span></span> |<span data-ttu-id="74c79-136">Poziom wydobycie ropy naftowej aparat mechanizm</span><span class="sxs-lookup"><span data-stu-id="74c79-136">The engine oil level of the vehicle</span></span> |<span data-ttu-id="74c79-137">Losowo generowany numer od 0 do 100 (procent poziomu wydobycie ropy naftowej aparat oznacza)</span><span class="sxs-lookup"><span data-stu-id="74c79-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="74c79-138">Opona wykorzystania</span><span class="sxs-lookup"><span data-stu-id="74c79-138">Tire pressure</span></span> |<span data-ttu-id="74c79-139">Wykorzystanie opona pojazdów.</span><span class="sxs-lookup"><span data-stu-id="74c79-139">The tire pressure of the vehicle</span></span> |<span data-ttu-id="74c79-140">Losowo generowany numer 50 0 (wskazuje procent poziomu wykorzystania opona)</span><span class="sxs-lookup"><span data-stu-id="74c79-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="74c79-141">Licznika</span><span class="sxs-lookup"><span data-stu-id="74c79-141">Odometer</span></span> |<span data-ttu-id="74c79-142">Odczytywanie licznika mechanizm</span><span class="sxs-lookup"><span data-stu-id="74c79-142">The odometer reading of the vehicle</span></span> |<span data-ttu-id="74c79-143">Losowo generowany numer od 0 200000</span><span class="sxs-lookup"><span data-stu-id="74c79-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="74c79-144">Accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="74c79-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="74c79-145">Pozycja szkła mechanizm klawiszy skrótów</span><span class="sxs-lookup"><span data-stu-id="74c79-145">The accelerator pedal position of the vehicle</span></span> |<span data-ttu-id="74c79-146">Losowo generowany numer od 0 do 100 (procent poziomu akceleratora wskazuje)</span><span class="sxs-lookup"><span data-stu-id="74c79-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="74c79-147">Parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="74c79-147">Parking_brake_status</span></span> |<span data-ttu-id="74c79-148">Wskazuje, czy mechanizm jest stoi lub nie</span><span class="sxs-lookup"><span data-stu-id="74c79-148">Indicates whether the vehicle is parked or not</span></span> |<span data-ttu-id="74c79-149">Wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="74c79-149">True or False</span></span> |
| <span data-ttu-id="74c79-150">Headlamp_status</span><span class="sxs-lookup"><span data-stu-id="74c79-150">Headlamp_status</span></span> |<span data-ttu-id="74c79-151">Wskazuje, gdzie reflektor znajduje się na lub nie</span><span class="sxs-lookup"><span data-stu-id="74c79-151">Indicates where the headlamp is on or not</span></span> |<span data-ttu-id="74c79-152">Wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="74c79-152">True or False</span></span> |
| <span data-ttu-id="74c79-153">Brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="74c79-153">Brake_pedal_status</span></span> |<span data-ttu-id="74c79-154">Wskazuje, czy pedału hamulca zostanie naciśnięty, czy nie</span><span class="sxs-lookup"><span data-stu-id="74c79-154">Indicates whether the brake pedal is pressed or not</span></span> |<span data-ttu-id="74c79-155">Wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="74c79-155">True or False</span></span> |
| <span data-ttu-id="74c79-156">Transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="74c79-156">Transmission_gear_position</span></span> |<span data-ttu-id="74c79-157">Pozycja koło zębate transmisji mechanizm</span><span class="sxs-lookup"><span data-stu-id="74c79-157">The transmission gear position of the vehicle</span></span> |<span data-ttu-id="74c79-158">Stan: najpierw drugie, trzecie czwarty, piąte, szóstego, siódme, kolejnego, ósmego</span><span class="sxs-lookup"><span data-stu-id="74c79-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="74c79-159">Ignition_status</span><span class="sxs-lookup"><span data-stu-id="74c79-159">Ignition_status</span></span> |<span data-ttu-id="74c79-160">Wskazuje, czy mechanizm jest uruchomiona lub zatrzymana</span><span class="sxs-lookup"><span data-stu-id="74c79-160">Indicates whether the vehicle is running or stopped</span></span> |<span data-ttu-id="74c79-161">Wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="74c79-161">True or False</span></span> |
| <span data-ttu-id="74c79-162">Windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="74c79-162">Windshield_wiper_status</span></span> |<span data-ttu-id="74c79-163">Wskazuje, czy Wycieraczka szyby jest wyłączone lub nie</span><span class="sxs-lookup"><span data-stu-id="74c79-163">Indicates whether the windshield wiper is turned or not</span></span> |<span data-ttu-id="74c79-164">Wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="74c79-164">True or False</span></span> |
| <span data-ttu-id="74c79-165">ABS</span><span class="sxs-lookup"><span data-stu-id="74c79-165">ABS</span></span> |<span data-ttu-id="74c79-166">Wskazuje, czy ABS prowadzi lub nie</span><span class="sxs-lookup"><span data-stu-id="74c79-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="74c79-167">Wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="74c79-167">True or False</span></span> |
| <span data-ttu-id="74c79-168">Znacznik czasu</span><span class="sxs-lookup"><span data-stu-id="74c79-168">Timestamp</span></span> |<span data-ttu-id="74c79-169">Sygnatura czasowa po utworzeniu punktu danych.</span><span class="sxs-lookup"><span data-stu-id="74c79-169">The timestamp when the data point is created</span></span> |<span data-ttu-id="74c79-170">Date</span><span class="sxs-lookup"><span data-stu-id="74c79-170">Date</span></span> |
| <span data-ttu-id="74c79-171">Miasto</span><span class="sxs-lookup"><span data-stu-id="74c79-171">City</span></span> |<span data-ttu-id="74c79-172">Lokalizacja mechanizm</span><span class="sxs-lookup"><span data-stu-id="74c79-172">The location of the vehicle</span></span> |<span data-ttu-id="74c79-173">4 miejscowości, w tym rozwiązaniu: Bellevue, Redmond, Sammamish, Seattle</span><span class="sxs-lookup"><span data-stu-id="74c79-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="74c79-174">Zestaw danych odwołania modelu vehicle zawiera VIN do mapowania modelu.</span><span class="sxs-lookup"><span data-stu-id="74c79-174">The vehicle model reference dataset contains VIN to the model mapping.</span></span> 

| <span data-ttu-id="74c79-175">VIN</span><span class="sxs-lookup"><span data-stu-id="74c79-175">VIN</span></span> | <span data-ttu-id="74c79-176">Model</span><span class="sxs-lookup"><span data-stu-id="74c79-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="74c79-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="74c79-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="74c79-178">Limuzyna</span><span class="sxs-lookup"><span data-stu-id="74c79-178">Sedan</span></span> |
| <span data-ttu-id="74c79-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="74c79-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="74c79-180">Połączenie hybrydowe</span><span class="sxs-lookup"><span data-stu-id="74c79-180">Hybrid</span></span> |
| <span data-ttu-id="74c79-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="74c79-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="74c79-182">Rodziny zamknięte</span><span class="sxs-lookup"><span data-stu-id="74c79-182">Family Saloon</span></span> |
| <span data-ttu-id="74c79-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="74c79-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="74c79-184">Limuzyna</span><span class="sxs-lookup"><span data-stu-id="74c79-184">Sedan</span></span> |
| <span data-ttu-id="74c79-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="74c79-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="74c79-186">Połączenie hybrydowe</span><span class="sxs-lookup"><span data-stu-id="74c79-186">Hybrid</span></span> |
| <span data-ttu-id="74c79-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="74c79-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="74c79-188">Rodziny zamknięte</span><span class="sxs-lookup"><span data-stu-id="74c79-188">Family Saloon</span></span> |
| <span data-ttu-id="74c79-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="74c79-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="74c79-190">Limuzyna</span><span class="sxs-lookup"><span data-stu-id="74c79-190">Sedan</span></span> |
| <span data-ttu-id="74c79-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="74c79-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="74c79-192">Połączenie hybrydowe</span><span class="sxs-lookup"><span data-stu-id="74c79-192">Hybrid</span></span> |
| <span data-ttu-id="74c79-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="74c79-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="74c79-194">Rodziny zamknięte</span><span class="sxs-lookup"><span data-stu-id="74c79-194">Family Saloon</span></span> |
| <span data-ttu-id="74c79-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="74c79-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="74c79-196">Możliwe do przekonwertowania</span><span class="sxs-lookup"><span data-stu-id="74c79-196">Convertible</span></span> |
| <span data-ttu-id="74c79-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="74c79-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="74c79-198">Kombi</span><span class="sxs-lookup"><span data-stu-id="74c79-198">Station Wagon</span></span> |
| <span data-ttu-id="74c79-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="74c79-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="74c79-200">Samochód kompaktowy</span><span class="sxs-lookup"><span data-stu-id="74c79-200">Compact Car</span></span> |
| <span data-ttu-id="74c79-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="74c79-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="74c79-202">Mała SUV</span><span class="sxs-lookup"><span data-stu-id="74c79-202">Small SUV</span></span> |
| <span data-ttu-id="74c79-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="74c79-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="74c79-204">Samochodu sportowych</span><span class="sxs-lookup"><span data-stu-id="74c79-204">Sports Car</span></span> |
| <span data-ttu-id="74c79-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="74c79-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="74c79-206">Średnia SUV</span><span class="sxs-lookup"><span data-stu-id="74c79-206">Medium SUV</span></span> |
| <span data-ttu-id="74c79-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="74c79-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="74c79-208">Kombi</span><span class="sxs-lookup"><span data-stu-id="74c79-208">Station Wagon</span></span> |
| <span data-ttu-id="74c79-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="74c79-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="74c79-210">Duże SUV</span><span class="sxs-lookup"><span data-stu-id="74c79-210">Large SUV</span></span> |
| <span data-ttu-id="74c79-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="74c79-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="74c79-212">Duże SUV</span><span class="sxs-lookup"><span data-stu-id="74c79-212">Large SUV</span></span> |
| <span data-ttu-id="74c79-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="74c79-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="74c79-214">Coupe</span><span class="sxs-lookup"><span data-stu-id="74c79-214">Coupe</span></span> |
| <span data-ttu-id="74c79-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="74c79-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="74c79-216">Limuzyna</span><span class="sxs-lookup"><span data-stu-id="74c79-216">Sedan</span></span> |
| <span data-ttu-id="74c79-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="74c79-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="74c79-218">Połączenie hybrydowe</span><span class="sxs-lookup"><span data-stu-id="74c79-218">Hybrid</span></span> |
| <span data-ttu-id="74c79-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="74c79-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="74c79-220">Rodziny zamknięte</span><span class="sxs-lookup"><span data-stu-id="74c79-220">Family Saloon</span></span> |
| <span data-ttu-id="74c79-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="74c79-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="74c79-222">Limuzyna</span><span class="sxs-lookup"><span data-stu-id="74c79-222">Sedan</span></span> |
| <span data-ttu-id="74c79-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="74c79-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="74c79-224">Połączenie hybrydowe</span><span class="sxs-lookup"><span data-stu-id="74c79-224">Hybrid</span></span> |
| <span data-ttu-id="74c79-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="74c79-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="74c79-226">Rodziny zamknięte</span><span class="sxs-lookup"><span data-stu-id="74c79-226">Family Saloon</span></span> |
| <span data-ttu-id="74c79-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="74c79-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="74c79-228">Limuzyna</span><span class="sxs-lookup"><span data-stu-id="74c79-228">Sedan</span></span> |
| <span data-ttu-id="74c79-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="74c79-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="74c79-230">Połączenie hybrydowe</span><span class="sxs-lookup"><span data-stu-id="74c79-230">Hybrid</span></span> |
| <span data-ttu-id="74c79-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="74c79-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="74c79-232">Rodziny zamknięte</span><span class="sxs-lookup"><span data-stu-id="74c79-232">Family Saloon</span></span> |
| <span data-ttu-id="74c79-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="74c79-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="74c79-234">Możliwe do przekonwertowania</span><span class="sxs-lookup"><span data-stu-id="74c79-234">Convertible</span></span> |
| <span data-ttu-id="74c79-235">…….</span><span class="sxs-lookup"><span data-stu-id="74c79-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="74c79-236">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="74c79-236">References</span></span>
[<span data-ttu-id="74c79-237">Rozwiązanie programu Visual Studio symulatora telematyki vehicle</span><span class="sxs-lookup"><span data-stu-id="74c79-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="74c79-238">Centrum zdarzeń platformy Azure</span><span class="sxs-lookup"><span data-stu-id="74c79-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="74c79-239">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="74c79-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="74c79-240">Wprowadzanie</span><span class="sxs-lookup"><span data-stu-id="74c79-240">Ingestion</span></span>
<span data-ttu-id="74c79-241">Kombinacje Azure Event Hubs, Stream Analytics i fabryki danych można wykorzystać do pozyskiwania sygnały vehicle, zdarzeń diagnostycznych i w czasie rzeczywistym i partii analytics.</span><span class="sxs-lookup"><span data-stu-id="74c79-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged to ingest the vehicle signals, the diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="74c79-242">Wszystkie te składniki są tworzone i skonfigurowany jako część wdrożenia rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="74c79-242">All these components are created and configured as part of the solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="74c79-243">Analiza w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="74c79-243">Real-time analysis</span></span>
<span data-ttu-id="74c79-244">Zdarzenia generowane przez symulator telematyki Vehicle są publikowane w Centrum zdarzeń przy użyciu zestawu SDK Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="74c79-244">The events generated by the Vehicle Telematics Simulator are published to the Event Hub using the Event Hub SDK.</span></span> <span data-ttu-id="74c79-245">Zadanie Stream Analytics wysyła strumień te zdarzenia z Centrum zdarzeń i przetwarza dane w czasie rzeczywistym do analizy kondycji pojazdów.</span><span class="sxs-lookup"><span data-stu-id="74c79-245">The Stream Analytics job ingests these events from the Event Hub and processes the data in real time to analyze the vehicle health.</span></span> 

![Pulpit nawigacyjny Centrum zdarzeń](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="74c79-247">*Rysunek 4 - pulpit nawigacyjny Centrum zdarzeń*</span><span class="sxs-lookup"><span data-stu-id="74c79-247">*Figure 4 - Event Hub dashboard*</span></span>

![Dane przetwarzania zadania usługi analiza strumienia](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="74c79-249">*Rysunek 5. zadania usługi analiza strumienia przetwarzania danych*</span><span class="sxs-lookup"><span data-stu-id="74c79-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="74c79-250">Zadanie Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="74c79-250">The Stream Analytics job;</span></span>

* <span data-ttu-id="74c79-251">wysyła strumień danych z Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="74c79-251">ingests data from the Event Hub</span></span> 
* <span data-ttu-id="74c79-252">wykonuje sprzężenie z mapowania vehicle VIN na odpowiedni model danych źródłowych</span><span class="sxs-lookup"><span data-stu-id="74c79-252">performs a join with the reference data to map the vehicle VIN to the corresponding model</span></span> 
* <span data-ttu-id="74c79-253">są utrwalane w magazynie obiektów blob platformy Azure dla analizach wsadowych sformatowanego.</span><span class="sxs-lookup"><span data-stu-id="74c79-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="74c79-254">Następujące zapytanie Stream Analytics jest używany do utrwalenia danych do magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="74c79-254">The following Stream Analytics query is used to persist the data into Azure blob storage.</span></span> 

![Zapytanie dotyczące zadań analizy strumienia dla wprowadzanie danych](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="74c79-256">*Rysunek 6 - analiza strumienia zadania zapytania na wprowadzanie danych*</span><span class="sxs-lookup"><span data-stu-id="74c79-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="74c79-257">Analiza partii</span><span class="sxs-lookup"><span data-stu-id="74c79-257">Batch analysis</span></span>
<span data-ttu-id="74c79-258">Możemy również generowania woluminów sygnały symulowane vehicle i diagnostycznych zestawu danych dla bardziej zaawansowane funkcje analizy partii.</span><span class="sxs-lookup"><span data-stu-id="74c79-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="74c79-259">Jest to wymagane, aby zapewnić objętość danych reprezentatywnych dla przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="74c79-259">This is required to ensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="74c79-260">W tym celu potoku o nazwie "PrepareSampleDataPipeline" w przepływie pracy z fabryką danych Azure jest używany do generowania wartość jednego roku sygnały symulowane vehicle i zestawu danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="74c79-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in the Azure Data Factory workflow to generate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="74c79-261">Kliknij przycisk [działania niestandardowego fabryki danych](http://go.microsoft.com/fwlink/?LinkId=717077) do pobrania działania DotNet niestandardowego fabryki danych rozwiązania Visual Studio dla dostosowania, w zależności od wymagań.</span><span class="sxs-lookup"><span data-stu-id="74c79-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) to download the Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![Przygotowanie przykładowych danych do przepływu pracy przetwarzania wsadowego](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="74c79-263">*Rysunek 7 — przygotowanie przykładowych danych do przepływu pracy przetwarzania wsadowego*</span><span class="sxs-lookup"><span data-stu-id="74c79-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="74c79-264">Potok składa się z niestandardowych .net ADF działania, Pokaż tutaj:</span><span class="sxs-lookup"><span data-stu-id="74c79-264">The pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![Działanie PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="74c79-266">*Rysunek 8 - PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="74c79-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="74c79-267">Po potoku wykonuje pomyślnie i zestawu danych "RawCarEventsTable" jest oznaczona jako "Gotowe", jednego roku warto symulowane vehicle sygnałów oraz diagnostyki danych są tworzone.</span><span class="sxs-lookup"><span data-stu-id="74c79-267">Once the pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="74c79-268">Zostanie wyświetlony następujący folder i plik utworzony na koncie magazynu w kontenerze "connectedcar":</span><span class="sxs-lookup"><span data-stu-id="74c79-268">You see the following folder and file created in your storage account under the "connectedcar" container:</span></span>

![Dane wyjściowe PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="74c79-270">*Rysunek 9 - PrepareSampleDataPipeline danych wyjściowych*</span><span class="sxs-lookup"><span data-stu-id="74c79-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="74c79-271">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="74c79-271">References</span></span>
[<span data-ttu-id="74c79-272">Azure SDK Centrum zdarzeń pozyskiwania strumieni</span><span class="sxs-lookup"><span data-stu-id="74c79-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="74c79-273">[Możliwości przenoszenia danych fabryki danych platformy Azure](../data-factory/data-factory-data-movement-activities.md)
[działania DotNet fabryki danych Azure](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="74c79-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="74c79-274">Rozwiązanie programu visual studio działania DotNet fabryki danych Azure przygotowania przykładowe dane</span><span class="sxs-lookup"><span data-stu-id="74c79-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-the-dataset"></a><span data-ttu-id="74c79-275">Partycja zestawu danych</span><span class="sxs-lookup"><span data-stu-id="74c79-275">Partition the dataset</span></span>
<span data-ttu-id="74c79-276">Sygnały raw vehicle częściową strukturą i zestawu danych diagnostycznych są dzielone w kroku przygotowania danych do formatu rok i miesiąc.</span><span class="sxs-lookup"><span data-stu-id="74c79-276">The raw semi-structured vehicle signals and diagnostic dataset are partitioned in the data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="74c79-277">Zamienia kwerend większą wydajność i skalowalność magazynu długoterminowego jako pierwsze konto się zapełni, włączając błędów w tryb failover z jednego obiektu blob konta do następnego tej partycji.</span><span class="sxs-lookup"><span data-stu-id="74c79-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account to the next as the first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="74c79-278">Ten krok w rozwiązaniu ma zastosowanie tylko do przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="74c79-278">This step in the solution is applicable only to batch processing.</span></span>

<span data-ttu-id="74c79-279">Wejście i wyjście danych zarządzania danymi:</span><span class="sxs-lookup"><span data-stu-id="74c79-279">Input and output data data management:</span></span>

* <span data-ttu-id="74c79-280">**Dane wyjściowe** (etykietą *PartitionedCarEventsTable*) ma być przechowywane przez dłuższy czas jako podstawowych / "rawest" formularza danych odbiorcy "Data Lake".</span><span class="sxs-lookup"><span data-stu-id="74c79-280">The **output data** (labeled *PartitionedCarEventsTable*) is to be kept for a long period of time as the foundational/"rawest" form of data in the customer's "Data Lake".</span></span> 
* <span data-ttu-id="74c79-281">**Dane wejściowe** do tego potoku będzie zazwyczaj odrzucone jako danych wyjściowych ma pełnej rozdzielczości w danych wejściowych — wystarczy znajduje (podzielona na partycje) lepiej dla dalszego wykorzystania.</span><span class="sxs-lookup"><span data-stu-id="74c79-281">The **input data** to this pipeline would typically be discarded as the output data has full fidelity to the input - it's just stored (partitioned) better for subsequent use.</span></span>

![Przepływ pracy zdarzenia samochodu partycji](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="74c79-283">*Rysunek 10 — przepływ pracy zdarzenia samochodu partycji*</span><span class="sxs-lookup"><span data-stu-id="74c79-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="74c79-284">Dane pierwotne jest podzielona na partycje przy użyciu działania Hive HDInsight w "PartitionCarEventsPipeline".</span><span class="sxs-lookup"><span data-stu-id="74c79-284">The raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="74c79-285">Przykładowe dane generowane w kroku 1 rok partycjonowanego rok i miesiąc.</span><span class="sxs-lookup"><span data-stu-id="74c79-285">The sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="74c79-286">Partycje są używane do generowania sygnałów vehicle i danych diagnostycznych dla każdego miesiąca roku (całkowita liczba partycji 12).</span><span class="sxs-lookup"><span data-stu-id="74c79-286">The partitions are used to generate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![Działanie PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="74c79-288">*Rysunek 11 — PartitionCarEventsPipeline*</span><span class="sxs-lookup"><span data-stu-id="74c79-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="74c79-289">***Skryptu PartitionConnectedCarEvents Hive***</span><span class="sxs-lookup"><span data-stu-id="74c79-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="74c79-290">Poniższy skrypt Hive o nazwie "partitioncarevents.hql" służy do partycjonowania i znajduje się w folderze "\demo\src\connectedcar\scripts" pobrany zip.</span><span class="sxs-lookup"><span data-stu-id="74c79-290">The following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in the "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 
    
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

<span data-ttu-id="74c79-291">Po pomyślnym wykonaniu potoku zapoznaj się następujące partycje, które są generowane na koncie magazynu w kontenerze "connectedcar".</span><span class="sxs-lookup"><span data-stu-id="74c79-291">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Dane wyjściowe podzielonym na partycje](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="74c79-293">*Rysunek 12 — partycjonowanej danych wyjściowych*</span><span class="sxs-lookup"><span data-stu-id="74c79-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="74c79-294">Dane są zoptymalizowane pod, jest bardziej łatwe w zarządzaniu i gotowa do dalszego przetwarzania, aby uzyskać wgląd w partii sformatowanego.</span><span class="sxs-lookup"><span data-stu-id="74c79-294">The data is now optimized, is more manageable and ready for further processing to gain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="74c79-295">Analiza danych</span><span class="sxs-lookup"><span data-stu-id="74c79-295">Data Analysis</span></span>
<span data-ttu-id="74c79-296">W tej sekcji zobacz temat jak połączyć usługi Azure Stream Analytics, usługi Azure Machine Learning fabryki danych Azure i usłudze Azure HDInsight dla zaawansowanej, zaawansowane analizy na vehicle kondycji i wspierającym zwyczaje.</span><span class="sxs-lookup"><span data-stu-id="74c79-296">In this section, you see how to combine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="74c79-297">Istnieją trzy podpunkty tutaj:</span><span class="sxs-lookup"><span data-stu-id="74c79-297">There are three subsections here:</span></span>

1. <span data-ttu-id="74c79-298">**Machine Learning**: ta podsekcja zawiera informacje na temat eksperymentu wykrywania anomalii, która użyliśmy w tym rozwiązaniu do prognozowania pojazdów wymagających obsługi konserwacji i pojazdów wymagających odwołania z powodu problemów bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="74c79-298">**Machine Learning**: This subsection contains information on the anomaly detection experiment that we have used in this solution to predict vehicles requiring servicing maintenance and vehicles requiring recalls due to safety issues.</span></span>
2. <span data-ttu-id="74c79-299">**W czasie rzeczywistym analizy**: ta podsekcja zawiera informacje dotyczące analiz w czasie rzeczywistym za pomocą język zapytań usługi analiza strumienia i operacyjnych eksperymentu uczenia maszynowego w czasie rzeczywistym za pomocą aplikacji niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="74c79-299">**Real-time analysis**: This subsection contains information regarding the real-time analytics using the Stream Analytics Query Language and operationalizing the machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="74c79-300">**Partii analizy**: ta podsekcja zawiera informacje dotyczące, przekształcanie i przetwarzania wsadowego danych przy użyciu usługi Azure HDInsight i usługi Azure Machine Learning operationalized przez fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="74c79-300">**Batch analysis**: This subsection contains information regarding the transforming and processing of the batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="74c79-301">Usługa Machine Learning</span><span class="sxs-lookup"><span data-stu-id="74c79-301">Machine Learning</span></span>
<span data-ttu-id="74c79-302">Naszym celem jest do prognozowania pojazdów, które wymagają konserwacji lub wycofania oparte na niektórych statystyki kondycji.</span><span class="sxs-lookup"><span data-stu-id="74c79-302">Our goal here is to predict the vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="74c79-303">Firma Microsoft wprowadzać następujące założenia</span><span class="sxs-lookup"><span data-stu-id="74c79-303">We make the following assumptions</span></span>

* <span data-ttu-id="74c79-304">Jeśli jeden z następujących trzech warunków są spełnione, wymagają pojazdów **obsługi konserwacji**:</span><span class="sxs-lookup"><span data-stu-id="74c79-304">If one of the following three conditions are true, the vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="74c79-305">Brakuje opona wykorzystania</span><span class="sxs-lookup"><span data-stu-id="74c79-305">Tire pressure is low</span></span>
  * <span data-ttu-id="74c79-306">Brakuje wydobycie ropy naftowej aparatu</span><span class="sxs-lookup"><span data-stu-id="74c79-306">Engine oil level is low</span></span>
  * <span data-ttu-id="74c79-307">Aparat temperatury jest wysoka</span><span class="sxs-lookup"><span data-stu-id="74c79-307">Engine temperature is high</span></span>
* <span data-ttu-id="74c79-308">Jeśli jeden z następujących warunków jest spełniony, może być pojazdów **problem bezpieczeństwa** i wymagają **odwołania**:</span><span class="sxs-lookup"><span data-stu-id="74c79-308">If one of the following conditions are true, the vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="74c79-309">Aparat temperatury jest wysoka, ale brakuje poza temperatury</span><span class="sxs-lookup"><span data-stu-id="74c79-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="74c79-310">Aparat temperatury jest niska, ale poza temperatury jest wysoka</span><span class="sxs-lookup"><span data-stu-id="74c79-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="74c79-311">Na podstawie poprzedniego wymagań, został utworzony dwóch osobnych modeli do wykrywania anomalii: jeden vehicle obsługi wykrywania i jeden do wykrywania odwołania pojazdów.</span><span class="sxs-lookup"><span data-stu-id="74c79-311">Based on the previous requirements, we have created two separate models to detect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="74c79-312">W obu tych modeli wbudowanych algorytm analizy składnik główny (PCA) służy do wykrywania anomalii.</span><span class="sxs-lookup"><span data-stu-id="74c79-312">In both these models, the built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="74c79-313">**Model wykrywania konserwacji**</span><span class="sxs-lookup"><span data-stu-id="74c79-313">**Maintenance detection model**</span></span>

<span data-ttu-id="74c79-314">Jeśli jeden z trzech wskaźniki opona wykorzystania, aparat wydobycie ropy naftowej lub temperatury aparat — spełniał stanu odpowiednich, model wykrywania konserwacji raporty anomalii.</span><span class="sxs-lookup"><span data-stu-id="74c79-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, the maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="74c79-315">W związku z tym tylko należy wziąć pod uwagę następujące trzy zmienne podczas konstruowania modelu.</span><span class="sxs-lookup"><span data-stu-id="74c79-315">As a result, we only need to consider these three variables in building the model.</span></span> <span data-ttu-id="74c79-316">W naszym eksperymentu w usłudze Azure Machine Learning, najpierw używamy **Select Columns in Dataset** modułu, aby wyodrębnić te trzy zmienne.</span><span class="sxs-lookup"><span data-stu-id="74c79-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module to extract these three variables.</span></span> <span data-ttu-id="74c79-317">Następnie używamy modułu wykrywania anomalii oparte na PCA do tworzenia modelu wykrywania anomalii.</span><span class="sxs-lookup"><span data-stu-id="74c79-317">Next we use the PCA-based anomaly detection module to build the anomaly detection model.</span></span> 

<span data-ttu-id="74c79-318">Podmiot zabezpieczeń składnika analiza (PCA) to technikę ustalonych w uczeniu maszynowym, który można zastosować funkcji wyboru cech, klasyfikacji i wykrywania anomalii.</span><span class="sxs-lookup"><span data-stu-id="74c79-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied to feature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="74c79-319">PCA Konwertuje zestaw przypadku zawierającego prawdopodobnie skorelowane zmienne, do wartości o nazwie główne składniki.</span><span class="sxs-lookup"><span data-stu-id="74c79-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="74c79-320">Klucza pomysł na podstawie PCA modelowania jest danych projektu na małe wymiarowej miejsca, aby funkcje i anomalie, można łatwiej zidentyfikować.</span><span class="sxs-lookup"><span data-stu-id="74c79-320">The key idea of PCA-based modeling is to project data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="74c79-321">Dla każdego nowego danych wejściowych do modelu wykrywania wykrywanie anomalii najpierw oblicza swojej projekcji na eigenvectors, a następnie oblicza błąd znormalizowane odbudowy.</span><span class="sxs-lookup"><span data-stu-id="74c79-321">For each new input to  the detection model, the anomaly detector first computes its projection on the eigenvectors, and then computes the normalized reconstruction error.</span></span> <span data-ttu-id="74c79-322">Ten błąd znormalizowane jest wynik anomalii.</span><span class="sxs-lookup"><span data-stu-id="74c79-322">This normalized error is the anomaly score.</span></span> <span data-ttu-id="74c79-323">Im wyższa błąd, więcej nietypowych wystąpienie jest.</span><span class="sxs-lookup"><span data-stu-id="74c79-323">The higher the error, the more anomalous the instance is.</span></span> 

<span data-ttu-id="74c79-324">Problem wykrywania konserwacji każdy rekord jest uznawana za ustalony punktu 3-wymiarową przestrzeni opona wykorzystania, aparat wydobycie ropy naftowej i temperatury aparat współrzędnych.</span><span class="sxs-lookup"><span data-stu-id="74c79-324">In the maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="74c79-325">Aby przechwytywać anomalie te, firma Microsoft project oryginalnych danych w przestrzeni trójwymiarowej 3 na 2-wymiarową miejsca, przy użyciu PCA.</span><span class="sxs-lookup"><span data-stu-id="74c79-325">To capture these anomalies, we can project the original data in the 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="74c79-326">W związku z tym firma Microsoft ustaw dla parametru liczby składników do użycia w PCA 2.</span><span class="sxs-lookup"><span data-stu-id="74c79-326">Thus, we set the parameter Number of components to use in PCA to be 2.</span></span> <span data-ttu-id="74c79-327">Ten parametr odgrywa ważną rolę w stosowaniu wykrywania anomalii oparte na PCA.</span><span class="sxs-lookup"><span data-stu-id="74c79-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="74c79-328">Po zakończeniu operacji przewidywania danych przy użyciu PCA możemy łatwiej ustalić tych nieprawidłowości.</span><span class="sxs-lookup"><span data-stu-id="74c79-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="74c79-329">**Model wykrywania anomalii odwołania** w modelu wykrywania anomalii odwołania używamy Select Columns in Dataset i anomalii oparte na PCA modułów wykrywania w podobny sposób.</span><span class="sxs-lookup"><span data-stu-id="74c79-329">**Recall anomaly detection model** In the recall anomaly detection model, we use the Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="74c79-330">W szczególności firma Microsoft najpierw wyodrębnić, trzy - poza temperatury i szybkość temperatury aparat — zmienne przy użyciu **Select Columns in Dataset** modułu.</span><span class="sxs-lookup"><span data-stu-id="74c79-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using the **Select Columns in Dataset** module.</span></span> <span data-ttu-id="74c79-331">Możemy także zmiennej szybkości ponieważ temperatury aparat zwykle są korelowane szybkości.</span><span class="sxs-lookup"><span data-stu-id="74c79-331">We also include the speed variable since the engine temperature typically is correlated to the speed.</span></span> <span data-ttu-id="74c79-332">Następnie używamy modułu wykrywania anomalii oparte na PCA do projektu danych z 3-wymiarową miejsca na miejsce 2-wymiarowej.</span><span class="sxs-lookup"><span data-stu-id="74c79-332">Next we use PCA-based anomaly detection module to project the data from the 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="74c79-333">Są spełnione kryteria odwołania i mechanizm wymaga odwołania gdy aparat temperatury i poza temperatury wysokiej negatywnie skorelowane.</span><span class="sxs-lookup"><span data-stu-id="74c79-333">The recall criteria are satisfied and so the vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="74c79-334">Za pomocą algorytmu wykrywania anomalii oparte na PCA, możemy przechwytywania po wykonaniu PCA nieprawidłowości.</span><span class="sxs-lookup"><span data-stu-id="74c79-334">Using PCA-based anomaly detection algorithm, we can capture the anomalies after performing PCA.</span></span> 

<span data-ttu-id="74c79-335">Podczas uczenia modelu albo, musimy użyj normalnych danych, które nie wymaga jako dane wejściowe do uczenia modelu wykrywania anomalii oparte na PCA konserwacji lub wycofania.</span><span class="sxs-lookup"><span data-stu-id="74c79-335">When training either model, we need to use normal data, which does not require maintenance or recall as the input data to train the PCA-based anomaly detection model.</span></span> <span data-ttu-id="74c79-336">W eksperymencie oceniania używamy wykrywania anomalii uczonego modelu do wykrywania, czy mechanizm wymaga konserwacji lub wycofania.</span><span class="sxs-lookup"><span data-stu-id="74c79-336">In the scoring experiment, we use the trained anomaly detection model to detect whether or not the vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="74c79-337">Analiza w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="74c79-337">Real-time analysis</span></span>
<span data-ttu-id="74c79-338">Następujące zapytanie SQL Stream Analytics jest używany do pobierania średnią wszystkie parametry ważny, takie jak prędkość, poziom paliwa temperatury aparatu, odczytu licznika, opona wykorzystania, aparatu wydobycie ropy naftowej i inne.</span><span class="sxs-lookup"><span data-stu-id="74c79-338">The following Stream Analytics SQL Query is used to get the average of all the important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="74c79-339">Średnie są używane do wykrywania anomalii, alerty, wystawiania i określają warunki ogólnej kondycji pojazdów obsługiwane w określonym regionie i następnie skorelowany demograficznych.</span><span class="sxs-lookup"><span data-stu-id="74c79-339">The averages are used to detect anomalies, issue alerts, and determine the overall health conditions of vehicles operated in specific region and then correlate it to demographics.</span></span> 

![Stream Analytics zapytania do przetworzenia w czasie rzeczywistym](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="74c79-341">*Rysunek 13 — zapytań usługi Stream Analytics do przetworzenia w czasie rzeczywistym*</span><span class="sxs-lookup"><span data-stu-id="74c79-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="74c79-342">Wszystkie wartości średnie są obliczane przez TumblingWindow 3 sekundy.</span><span class="sxs-lookup"><span data-stu-id="74c79-342">All the averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="74c79-343">Użyto TubmlingWindow w takim przypadku ponieważ wymagamy przedziały czasu nienakładający, jak i ciągłe.</span><span class="sxs-lookup"><span data-stu-id="74c79-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="74c79-344">Aby dowiedzieć się więcej na temat wszystkie funkcje "Okien" Azure Stream Analytics, kliknij przycisk [okien (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="74c79-344">To learn more about all the "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="74c79-345">**Prognozowanie w czasie rzeczywistym**</span><span class="sxs-lookup"><span data-stu-id="74c79-345">**Real-time prediction**</span></span>

<span data-ttu-id="74c79-346">Aplikacja jest zawarte w ramach rozwiązania, który umożliwia operacjonalizację modelu uczenia maszynowego w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="74c79-346">An application is included as part of the solution to operationalize the machine learning model in real time.</span></span> <span data-ttu-id="74c79-347">Ta aplikacja o nazwie "RealTimeDashboardApp" jest utworzony i skonfigurowany jako część wdrożenia rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="74c79-347">This application called “RealTimeDashboardApp” is created and configured as part of the solution deployment.</span></span> <span data-ttu-id="74c79-348">Aplikacja wykonuje następujące działania:</span><span class="sxs-lookup"><span data-stu-id="74c79-348">The application performs the following:</span></span>

1. <span data-ttu-id="74c79-349">Nasłuchuje Centrum zdarzeń wystąpienia których Stream Analytics jest publikowanie zdarzenia we wzorcu stale.</span><span class="sxs-lookup"><span data-stu-id="74c79-349">Listens to an Event Hub instance where Stream Analytics is publishing the events in a pattern continuously.</span></span> <span data-ttu-id="74c79-350">![Stream Analytics zapytania do publikowania danych](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *rysunek 14 — zapytań usługi Stream Analytics do publikowania danych wyjściowych Centrum zdarzeń wystąpienia*</span><span class="sxs-lookup"><span data-stu-id="74c79-350">![Stream Analytics query for publishing the data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing the data to an output Event Hub instance*</span></span> 
2. <span data-ttu-id="74c79-351">Dla każdego zdarzenia, które otrzymuje tej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="74c79-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="74c79-352">Przetwarza dane przy użyciu punktu końcowego Machine Learning żądań i odpowiedzi oceniania (RR).</span><span class="sxs-lookup"><span data-stu-id="74c79-352">Processes the data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="74c79-353">Punkt końcowy rekordy zasobów są automatycznie publikowane jako część wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="74c79-353">The RRS endpoint is automatically published as part of the deployment.</span></span>
   * <span data-ttu-id="74c79-354">Dane wyjściowe rekordy zasobów jest opublikowana w zestawie danych usługi Power BI za pomocą wypychania interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="74c79-354">The RRS output is published to a Power BI dataset using the push APIs.</span></span>

<span data-ttu-id="74c79-355">Ten wzorzec jest również dotyczy scenariuszy, w których chcesz zintegrować aplikacji biznesowych (LoB) wraz z przepływem analiz w czasie rzeczywistym dla scenariuszy, takich jak alerty, powiadomienia i wiadomości.</span><span class="sxs-lookup"><span data-stu-id="74c79-355">This pattern is also applicable to scenarios in which you want to integrate a Line of Business (LoB) application with the real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="74c79-356">Kliknij przycisk [pobierania RealtimeDashboardApp](http://go.microsoft.com/fwlink/?LinkId=717078) Aby pobrać rozwiązanie RealtimeDashboardApp Visual Studio dostosowań.</span><span class="sxs-lookup"><span data-stu-id="74c79-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) to download the RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="74c79-357">**Do wykonania aplikacji pulpitu nawigacyjnego w czasie rzeczywistym**</span><span class="sxs-lookup"><span data-stu-id="74c79-357">**To execute the Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="74c79-358">Wyodrębnij i Zapisz lokalnie ![folderu RealtimeDashboardApp](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *rysunek 16 – RealtimeDashboardApp folderu*</span><span class="sxs-lookup"><span data-stu-id="74c79-358">Extract and save locally ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="74c79-359">Uruchom aplikację RealtimeDashboardApp.exe</span><span class="sxs-lookup"><span data-stu-id="74c79-359">Execute the application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="74c79-360">Podaj prawidłowe poświadczenia usługi Power BI, zaloguj się i kliknij przycisk Akceptuj</span><span class="sxs-lookup"><span data-stu-id="74c79-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![W czasie rzeczywistym pulpit nawigacyjny aplikacji logowania do usługi Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Zakończ w czasie rzeczywistym pulpit nawigacyjny aplikacji logowania do usługi Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="74c79-363">*Rysunek 17 — RealtimeDashboardApp: Logowania do usługi Power BI*</span><span class="sxs-lookup"><span data-stu-id="74c79-363">*Figure 17 – RealtimeDashboardApp: Sign-in to Power BI*</span></span>

>[!NOTE] 
><span data-ttu-id="74c79-364">Jeśli chcesz opróżnić zestawu danych usługi Power BI, wykonaj RealtimeDashboardApp z parametrem "flushdata":</span><span class="sxs-lookup"><span data-stu-id="74c79-364">If you want to flush the Power BI dataset, execute the RealtimeDashboardApp with the "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="74c79-365">Analiza partii</span><span class="sxs-lookup"><span data-stu-id="74c79-365">Batch analysis</span></span>
<span data-ttu-id="74c79-366">Celem jest pokazanie, jak silniki Contoso korzysta z możliwości obliczeń platformy Azure o danych big data, aby uzyskać szczegółowe, bogate informacje na wzorzec, zachowanie użycia i kondycji pojazdów.</span><span class="sxs-lookup"><span data-stu-id="74c79-366">The goal here is to show how Contoso Motors utilizes the Azure compute capabilities to harness big data to gain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="74c79-367">Dzięki temu możliwe:</span><span class="sxs-lookup"><span data-stu-id="74c79-367">This makes it possible to:</span></span>

* <span data-ttu-id="74c79-368">Poprawy obsługi klienta i zapewnić ich tańsze zapewniając wgląd na zwyczaje i wydajne zachowania pobudzenie paliwa</span><span class="sxs-lookup"><span data-stu-id="74c79-368">Improve the customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="74c79-369">Zapoznaj się z wyprzedzeniem klientów i ich pobudzenie patters regulują decyzje biznesowe i podaj najciekawszych klasy produktów i usług</span><span class="sxs-lookup"><span data-stu-id="74c79-369">Learn proactively about customers and their driving patters to govern business decisions and provide the best in class products & services</span></span>

<span data-ttu-id="74c79-370">W tym rozwiązaniu możemy przeznaczonych następujące metryki:</span><span class="sxs-lookup"><span data-stu-id="74c79-370">In this solution, we are targeting the following metrics:</span></span>

1. <span data-ttu-id="74c79-371">**Agresywna zwiększają zachowanie**: identyfikuje trend modeli, lokalizacje pobudzenie warunki i czas roku, aby uzyskać wgląd w bliskiej schematy.</span><span class="sxs-lookup"><span data-stu-id="74c79-371">**Aggressive driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of the year to gain insights on aggressive driving patterns.</span></span> <span data-ttu-id="74c79-372">Silniki contoso można używać tych insights kampanii marketingowych, nowe funkcje spersonalizowane i ubezpieczenia opartej na użyciu.</span><span class="sxs-lookup"><span data-stu-id="74c79-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="74c79-373">**Paliwa wydajne działanie pobudzenie**: identyfikuje trend modeli, lokalizacje pobudzenie warunki i czas roku, aby uzyskać szczegółowe informacje na efektywne schematy paliwa.</span><span class="sxs-lookup"><span data-stu-id="74c79-373">**Fuel efficient driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of the year to gain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="74c79-374">Silniki contoso można używać tych insights kampanii, zwiększają nowe funkcje i aktywne podlegające sterowniki kosztów przyjazną zwyczaje pobudzenie wejścia w życie i środowiska.</span><span class="sxs-lookup"><span data-stu-id="74c79-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting to the drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="74c79-375">**Odwołaj modele**: identyfikuje modele wymagających odwołań przez operacyjnych eksperymentu uczenia maszynowego wykrywania anomalii</span><span class="sxs-lookup"><span data-stu-id="74c79-375">**Recall models**: Identifies models requiring recalls by operationalizing the anomaly detection machine learning experiment</span></span>

<span data-ttu-id="74c79-376">Oto do szczegółów każdego z tych metryk</span><span class="sxs-lookup"><span data-stu-id="74c79-376">Let's look into the details of each of these metrics,</span></span>

<span data-ttu-id="74c79-377">**Agresywne pobudzenie wzorca**</span><span class="sxs-lookup"><span data-stu-id="74c79-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="74c79-378">Sygnały vehicle podzielonym na partycje i danych diagnostycznych są przetwarzane w potoku o nazwie "AggresiveDrivingPatternPipeline" przy użyciu Hive w celu określenia modele, lokalizacji vehicle, warunki jazdy i inne parametry który wykazuje zwiększają aktywnego wzorzec.</span><span class="sxs-lookup"><span data-stu-id="74c79-378">The partitioned vehicle signals and diagnostic data are processed in the pipeline named "AggresiveDrivingPatternPipeline" using Hive to determine the models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="74c79-379">![Agresywne pobudzenie przepływu pracy wzorzec](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*rysunek 18 — agresywne pobudzenie przepływu pracy wzorca*</span><span class="sxs-lookup"><span data-stu-id="74c79-379">![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="74c79-380">***Agresywne kierowania zapytań Hive wzorca***</span><span class="sxs-lookup"><span data-stu-id="74c79-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="74c79-381">Skryptu Hive o nazwie "aggresivedriving.hql" używany do analizowania aktywnego wzorca warunku jazdy znajduje się w folderze "\demo\src\connectedcar\scripts" zip pobranego.</span><span class="sxs-lookup"><span data-stu-id="74c79-381">The Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 

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


<span data-ttu-id="74c79-382">Kombinacja transmisji koło zębate pozycji w vehicle, stan szkła hamulca i szybkość używa do wykrywania reckless/agresywne działanie pobudzenie hamowania wzorzec dużą prędkością.</span><span class="sxs-lookup"><span data-stu-id="74c79-382">It uses the combination of vehicle's transmission gear position, brake pedal status, and speed to detect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="74c79-383">Po pomyślnym wykonaniu potoku zapoznaj się następujące partycje, które są generowane na koncie magazynu w kontenerze "connectedcar".</span><span class="sxs-lookup"><span data-stu-id="74c79-383">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Dane wyjściowe AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="74c79-385">*Rysunek 19 — AggressiveDrivingPatternPipeline danych wyjściowych*</span><span class="sxs-lookup"><span data-stu-id="74c79-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="74c79-386">**Efektywne wzorzec pobudzenie paliwa**</span><span class="sxs-lookup"><span data-stu-id="74c79-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="74c79-387">Sygnały vehicle podzielonym na partycje i danych diagnostycznych są przetwarzane w potoku o nazwie "FuelEfficientDrivingPatternPipeline".</span><span class="sxs-lookup"><span data-stu-id="74c79-387">The partitioned vehicle signals and diagnostic data are processed in the pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="74c79-388">Gałąź służy do określenia modele, lokalizacji vehicle, warunki jazdy i inne właściwości, które wykazują paliwa wydajne pobudzenie wzorzec.</span><span class="sxs-lookup"><span data-stu-id="74c79-388">Hive is used to determine the models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![Wzorzec pobudzenie obniżające zużycie paliwa](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="74c79-390">*Rysunek 20 – obniżające zużycie paliwa pobudzenie przepływu pracy wzorca*</span><span class="sxs-lookup"><span data-stu-id="74c79-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="74c79-391">***Paliwa wydajne pobudzenie wzorzec zapytań Hive***</span><span class="sxs-lookup"><span data-stu-id="74c79-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="74c79-392">Skryptu Hive o nazwie "fuelefficientdriving.hql" używany do analizowania aktywnego wzorca warunku jazdy znajduje się w folderze "\demo\src\connectedcar\scripts" zip pobranego.</span><span class="sxs-lookup"><span data-stu-id="74c79-392">The Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 

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


<span data-ttu-id="74c79-393">Używa kombinacji pozycji koło zębate transmisji vehicle w, stan szkła hamulca, szybkości, akceleratora pedał wykryć paliwa wydajne pobudzenie działanie przyspieszenie hamowania i szybkości wzorce.</span><span class="sxs-lookup"><span data-stu-id="74c79-393">It uses the combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position to detect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="74c79-394">Po pomyślnym wykonaniu potoku zapoznaj się następujące partycje, które są generowane na koncie magazynu w kontenerze "connectedcar".</span><span class="sxs-lookup"><span data-stu-id="74c79-394">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Dane wyjściowe FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="74c79-396">*Rysunek 21 — FuelEfficientDrivingPatternPipeline danych wyjściowych*</span><span class="sxs-lookup"><span data-stu-id="74c79-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="74c79-397">**Operacje przewidywania dla odwołania**</span><span class="sxs-lookup"><span data-stu-id="74c79-397">**Recall Predictions**</span></span>

<span data-ttu-id="74c79-398">Eksperymentu uczenia maszynowego jest udostępniane i opublikowane jako usługi sieci web jako część wdrożenia rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="74c79-398">The machine learning experiment is provisioned and published as a web service as part of the solution deployment.</span></span> <span data-ttu-id="74c79-399">Punkt końcowy oceniania partii jest wykorzystywana w tym przepływie pracy, zarejestrowany jako usługa połączone fabryki danych i operationalized przy użyciu danych fabryki działanie wsadowego oceniania.</span><span class="sxs-lookup"><span data-stu-id="74c79-399">The batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![Punkt końcowy Machine Learning](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="74c79-401">*Rysunek 22 — punktu końcowego uczenia maszynowego zarejestrowany jako połączonej usługi z fabryki danych*</span><span class="sxs-lookup"><span data-stu-id="74c79-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="74c79-402">Zarejestrowanej połączonej usługi jest używany w DetectAnomalyPipeline punkty danych za pomocą modelu wykrywania anomalii.</span><span class="sxs-lookup"><span data-stu-id="74c79-402">The registered linked service is used in the DetectAnomalyPipeline to score the data using the anomaly detection model.</span></span> 

![Learning działanie wsadowego oceniania w fabryce danych komputera](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="74c79-404">*Rysunek 23 — działanie usługi Azure Machine Learning wsadowego oceniania z fabryki danych*</span><span class="sxs-lookup"><span data-stu-id="74c79-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="74c79-405">Istnieje kilka czynności wykonywanych w tym potoku w celu przygotowania danych, dzięki czemu mogą być operationalized z wsadowego oceniania usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="74c79-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with the batch scoring web service.</span></span> 

![DetectAnomalyPipeline do prognozowania pojazdów wymagających odwołań](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="74c79-407">*Rysunek 24 — DetectAnomalyPipeline do prognozowania pojazdów wymagających odwołań*</span><span class="sxs-lookup"><span data-stu-id="74c79-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="74c79-408">***Zapytanie Hive wykrywania anomalii***</span><span class="sxs-lookup"><span data-stu-id="74c79-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="74c79-409">Po zakończeniu oceny działanie HDInsight służy do przetwarzania i agregowanie danych, które są skategoryzowane jako anomalii przez model z wynikiem prawdopodobieństwo: 0,60 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="74c79-409">Once the scoring is completed, an HDInsight activity is used to process and aggregate the data that are categorized as anomalies by the model with a probability score of 0.60 or higher.</span></span>

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


<span data-ttu-id="74c79-410">Po pomyślnym wykonaniu potoku zapoznaj się następujące partycje, które są generowane na koncie magazynu w kontenerze "connectedcar".</span><span class="sxs-lookup"><span data-stu-id="74c79-410">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Dane wyjściowe DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="74c79-412">*Rysunek 25 — DetectAnomalyPipeline danych wyjściowych*</span><span class="sxs-lookup"><span data-stu-id="74c79-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="74c79-413">Publikowanie</span><span class="sxs-lookup"><span data-stu-id="74c79-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="74c79-414">Analiza w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="74c79-414">Real-time analysis</span></span>
<span data-ttu-id="74c79-415">Jeden z zapytania w zadaniu Stream Analytics publikuje zdarzenia w danych wyjściowych Centrum zdarzeń wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="74c79-415">One of the queries in the Stream Analytics job publishes the events to an output Event Hub instance.</span></span> 

![Publikuje dane wyjściowe zadania usługi analiza strumienia wystąpienia Centrum zdarzeń](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="74c79-417">*Rysunek 26 — publikuje dane wyjściowe zadania usługi analiza strumienia wystąpienia Centrum zdarzeń*</span><span class="sxs-lookup"><span data-stu-id="74c79-417">*Figure 26 – Stream Analytics job publishes to an output Event Hub instance*</span></span>

![Stream Analytics zapytania do publikowania danych wyjściowych Centrum zdarzeń wystąpienia](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="74c79-419">*Rysunek 27 — zapytań usługi Stream Analytics do publikowania danych wyjściowych Centrum zdarzeń wystąpienia*</span><span class="sxs-lookup"><span data-stu-id="74c79-419">*Figure 27 – Stream Analytics query to publish to the output Event Hub instance*</span></span>

<span data-ttu-id="74c79-420">Ten strumień zdarzeń jest używany przez RealTimeDashboardApp zawarty w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="74c79-420">This stream of events is consumed by the RealTimeDashboardApp included in the solution.</span></span> <span data-ttu-id="74c79-421">Ta aplikacja korzysta z usługą sieci web Machine Learning żądań i odpowiedzi w czasie rzeczywistym oceniania i publikuje dane wynikowe z zestawem danych usługi Power BI zużycia.</span><span class="sxs-lookup"><span data-stu-id="74c79-421">This application leverages the Machine Learning Request-Response web service for real-time scoring and publishes the resultant data to a Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="74c79-422">Analiza partii</span><span class="sxs-lookup"><span data-stu-id="74c79-422">Batch analysis</span></span>
<span data-ttu-id="74c79-423">Wyniki partii i przetwarzanie w czasie rzeczywistym są publikowane w tabelach bazy danych SQL Azure zużycia.</span><span class="sxs-lookup"><span data-stu-id="74c79-423">The results of the batch and real-time processing are published to the Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="74c79-424">Azure SQL Server, bazy danych i tabele są tworzone automatycznie w ramach skrypt instalacyjny.</span><span class="sxs-lookup"><span data-stu-id="74c79-424">The Azure SQL Server, Database, and the tables are created automatically as part of the setup script.</span></span> 

![Kopiuj wyniki do przepływu pracy składnicy danych przetwarzania wsadowego](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="74c79-426">*Rysunek 28 — kopiowania wyniki do przepływu pracy składnicy danych przetwarzania wsadowego*</span><span class="sxs-lookup"><span data-stu-id="74c79-426">*Figure 28 – Batch processing results copy to data mart workflow*</span></span>

![Zadania usługi analiza strumienia publikuje do składnicy danych](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="74c79-428">*Rysunek 29 — analiza strumienia zadania publikuje do składnicy danych*</span><span class="sxs-lookup"><span data-stu-id="74c79-428">*Figure 29 – Stream Analytics job publishes to data mart*</span></span>

![Ustawienie składnicy danych w zadaniu Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="74c79-430">*Rysunek 30 – składnicy danych ustawienie w zadaniu Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="74c79-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="74c79-431">Używanie</span><span class="sxs-lookup"><span data-stu-id="74c79-431">Consume</span></span>
<span data-ttu-id="74c79-432">Usługi Power BI pozwala to rozwiązanie sformatowanego pulpitu nawigacyjnego i analizy predykcyjnej wizualizacji danych w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="74c79-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="74c79-433">Kliknij tutaj, aby uzyskać szczegółowe instrukcje dotyczące konfigurowania raportów usługi Power BI i pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="74c79-433">Click here for detailed instructions on setting up the Power BI reports and the dashboard.</span></span> <span data-ttu-id="74c79-434">Końcowy pulpitu nawigacyjnego wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="74c79-434">The final dashboard looks like this:</span></span>

![Pulpit nawigacyjny programu Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="74c79-436">*Rysunek 31 - pulpitu nawigacyjnego programu Power BI*</span><span class="sxs-lookup"><span data-stu-id="74c79-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="74c79-437">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="74c79-437">Summary</span></span>
<span data-ttu-id="74c79-438">Ten dokument zawiera szczegółowe przechodzenia z rozwiązania analizy Telemetrii pojazdów.</span><span class="sxs-lookup"><span data-stu-id="74c79-438">This document contains a detailed drill-down of the Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="74c79-439">Ten wzorzec architektury lambda, dla których są wyświetlane w czasie rzeczywistym i partii analizy w usłudze prognoz i akcji.</span><span class="sxs-lookup"><span data-stu-id="74c79-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="74c79-440">Ten wzorzec dotyczy szeroką gamę przypadków użycia, które wymagają aktywnej ścieżki (w czasie rzeczywistym) i analiza zimnych ścieżki (partii).</span><span class="sxs-lookup"><span data-stu-id="74c79-440">This pattern applies to a wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

