---
title: "Przykład MyDriving Azure IoT: Szybki start | Dokumentacja firmy Microsoft"
description: "Zacznij korzystać z aplikacji, która jest kompleksowe pokaz zaprojektować IoT system przy użyciu programu Microsoft Azure, w tym usługi Stream Analytics, Machine Learning i usługi Event Hubs."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: 031b492df1f186087e7b91102cbb44f552999293
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="mydriving-iot-system-quick-start"></a><span data-ttu-id="2b2d9-103">System MyDriving IoT: Szybki start</span><span class="sxs-lookup"><span data-stu-id="2b2d9-103">MyDriving IoT system: Quick start</span></span>
<span data-ttu-id="2b2d9-104">MyDriving to system, który demonstruje projekt i implementację typowe [Internetu rzeczy](iot-suite-overview.md) rozwiązania (IoT), który zbiera dane telemetryczne z urządzeń, przetwarzania danych w chmurze i stosuje machine learning w celu zapewnienia adaptacyjnego odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-104">MyDriving is a system that demonstrates the design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in the cloud, and applies machine learning to provide an adaptive response.</span></span> <span data-ttu-id="2b2d9-105">Pokazu rejestruje dane o Twojej rund samochodu na podstawie danych z telefonu komórkowego i karty, która zbiera informacje z systemu kontroli samochód.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-105">The demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span></span> <span data-ttu-id="2b2d9-106">Używa tych danych do przekazywania opinii własnego stylu jazdy w odróżnieniu od innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-106">It uses this data to provide feedback on your driving style in comparison to other users.</span></span>

<span data-ttu-id="2b2d9-107">Rzeczywistego celu MyDriving jest ułatwiających rozpoczęcie pracy podczas tworzenia rozwiązania IoT.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-107">The real purpose of MyDriving is to get you started in creating your own IoT solution.</span></span> <span data-ttu-id="2b2d9-108">Jednak przed, pomożemy Ci korzystanie z MyDriving aplikacja--członkiem naszego zespołu użytkownika testu.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-108">But before that, let’s get you going with the MyDriving app itself--as a member of our test user team.</span></span> <span data-ttu-id="2b2d9-109">Zapewnia to środowisko aplikacji i systemu za nią klientów, przed delve do architektury.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-109">This gives you an experience of the app and the system behind it as a consumer, before you delve into the architecture.</span></span> <span data-ttu-id="2b2d9-110">On również przedstawiono HockeyApp, chłodnych sposób zarządzania alfa i beta dystrybucji aplikacji użytkowników testowych.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-110">It also introduces you to HockeyApp, a cool way of managing the alpha and beta distributions of your apps to test users.</span></span>

## <a name="use-the-mobile-experience"></a><span data-ttu-id="2b2d9-111">Użyj korzystanie z urządzeń przenośnych</span><span class="sxs-lookup"><span data-stu-id="2b2d9-111">Use the mobile experience</span></span>
<span data-ttu-id="2b2d9-112">Jeśli masz urządzenia z systemem Android, iOS i Windows 10, mogą korzystać z aplikacji MyDriving.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-112">You can use the MyDriving app if you have an Android, iOS, or Windows 10 device.</span></span>

### <a name="android-and-windows-10-mobile-installation"></a><span data-ttu-id="2b2d9-113">Android i Windows 10 Mobile instalacji</span><span class="sxs-lookup"><span data-stu-id="2b2d9-113">Android and Windows 10 Mobile installation</span></span>
<span data-ttu-id="2b2d9-114">Na urządzeniu:</span><span class="sxs-lookup"><span data-stu-id="2b2d9-114">On your device:</span></span>

1. <span data-ttu-id="2b2d9-115">Zezwalaj na projektowanie aplikacji:</span><span class="sxs-lookup"><span data-stu-id="2b2d9-115">Allow development apps:</span></span>
   
   * <span data-ttu-id="2b2d9-116">System android: W **ustawienia** > **zabezpieczeń**, Zezwalaj na aplikacje z **nieznane źródła**.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span></span>
   * <span data-ttu-id="2b2d9-117">Systemie Windows 10: **ustawienia** > **aktualizacje** > **dla deweloperów**ustaw **tryb dewelopera**.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span></span>
2. <span data-ttu-id="2b2d9-118">Dołącz nasz zespół beta testu przez zarejestrowanie u lub zalogowanie się do, [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="2b2d9-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span></span> <span data-ttu-id="2b2d9-119">Platforma HockeyApp ułatwia dystrybucję Wczesne wersje aplikacji użytkowników testowych.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-119">HockeyApp makes it easy to distribute early releases of your app to test users.</span></span>
   
   <span data-ttu-id="2b2d9-120">Jeśli używasz systemu Windows 10, użyj przeglądarki Edge.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-120">If you’re using Windows 10, use the Edge browser.</span></span>
   
   <span data-ttu-id="2b2d9-121">Gdyby uczestnika Build 2016, zaloguj się przy użyciu tego samego e-mail konta Microsoft zarejestrowana konferencji za pomocą jednego z przycisków firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-121">If you were a Build 2016 attendee, sign in with the same Microsoft account email that you registered for the conference, by using one of the Microsoft buttons.</span></span> <span data-ttu-id="2b2d9-122">Użytkownik już jest zalogowany z HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-122">You’re already signed up with HockeyApp.</span></span>
   
   ![Platforma HockeyApp ekranu logowania](./media/iot-solution-get-started/image1.png)
3. <span data-ttu-id="2b2d9-124">Pobierz i zainstaluj aplikację w tym miejscu:</span><span class="sxs-lookup"><span data-stu-id="2b2d9-124">Download and install the app from here:</span></span>
   
   * [<span data-ttu-id="2b2d9-125">Android</span><span class="sxs-lookup"><span data-stu-id="2b2d9-125">Android</span></span>](http://rink.io/spMyDrivingAndroid)
   * [<span data-ttu-id="2b2d9-126">Windows 10</span><span class="sxs-lookup"><span data-stu-id="2b2d9-126">Windows 10</span></span>](http://rink.io/spMyDrivingUWP)
   
   <span data-ttu-id="2b2d9-127">Istnieją dwa elementy.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-127">There are two items.</span></span> <span data-ttu-id="2b2d9-128">Zainstaluj certyfikat w **zaufane osoby**.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-128">Install the certificate in **Trusted People**.</span></span> <span data-ttu-id="2b2d9-129">Następnie zainstaluj aplikację.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-129">Then install the app.</span></span>

<span data-ttu-id="2b2d9-130">*Uruchamianie aplikacji w systemie Windows 10 Mobile problemy?*</span><span class="sxs-lookup"><span data-stu-id="2b2d9-130">*Any issues starting the app on Windows 10 Mobile?*</span></span> <span data-ttu-id="2b2d9-131">Twój telefon może być aktualizacja lub dwóch za.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-131">Your phone might be an update or two behind.</span></span> <span data-ttu-id="2b2d9-132">Upewnij się, że masz najnowsze aktualizacje, lub zainstalować:</span><span class="sxs-lookup"><span data-stu-id="2b2d9-132">Make sure you've got the latest updates, or install:</span></span>

* [<span data-ttu-id="2b2d9-133">Microsoft.NET.Native.Framework.1.2.appx</span><span class="sxs-lookup"><span data-stu-id="2b2d9-133">Microsoft.NET.Native.Framework.1.2.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [<span data-ttu-id="2b2d9-134">Microsoft.NET.Native.Runtime.1.1.appx</span><span class="sxs-lookup"><span data-stu-id="2b2d9-134">Microsoft.NET.Native.Runtime.1.1.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [<span data-ttu-id="2b2d9-135">Microsoft.VCLibs.ARM.14.00.appx</span><span class="sxs-lookup"><span data-stu-id="2b2d9-135">Microsoft.VCLibs.ARM.14.00.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a><span data-ttu-id="2b2d9-136">Instalacja systemu iOS</span><span class="sxs-lookup"><span data-stu-id="2b2d9-136">iOS installation</span></span>
<span data-ttu-id="2b2d9-137">Jeśli Twoja Build 2016, Pobierz aplikację członkiem naszego zespołu testowego na platformę HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="2b2d9-137">If you attended Build 2016, download the app as a member of our test team on HockeyApp:</span></span>

1. <span data-ttu-id="2b2d9-138">Na urządzeniu z systemem iOS, zaloguj się do [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="2b2d9-138">On your iOS device, sign in to [HockeyApp](https://rink.hockeyapp.net).</span></span>
   <span data-ttu-id="2b2d9-139">Użyj jednej z Microsoft logowania przycisków i zaloguj się przy użyciu tego samego e-mail konta Microsoft, który został zarejestrowany z konferencji.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-139">Use one of the Microsoft sign-in buttons, and sign in with the same Microsoft account email that you registered with the conference.</span></span> <span data-ttu-id="2b2d9-140">(Nie używaj pola wiadomości e-mail i hasło).</span><span class="sxs-lookup"><span data-stu-id="2b2d9-140">(Don’t use the email and password fields.)</span></span>
   
   ![Platforma HockeyApp ekranu logowania](./media/iot-solution-get-started/image1.png)
2. <span data-ttu-id="2b2d9-142">Na pulpicie nawigacyjnym aplikacji HockeyApp MyDriving wybierz i pobierz go.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-142">In the HockeyApp dashboard, select MyDriving and download it.</span></span>
3. <span data-ttu-id="2b2d9-143">Autoryzowanie wydanie beta z HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="2b2d9-143">Authorize the beta release from HockeyApp:</span></span>
   
   <span data-ttu-id="2b2d9-144">a.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-144">a.</span></span> <span data-ttu-id="2b2d9-145">Przejdź do **ustawienia** > **ogólne** > **profilów i zarządzania urządzeniami.**</span><span class="sxs-lookup"><span data-stu-id="2b2d9-145">Go to **Settings** > **General** > **Profiles and Device Management.**</span></span>
   
   <span data-ttu-id="2b2d9-146">b.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-146">b.</span></span> <span data-ttu-id="2b2d9-147">Zaufania **Bit Stadium GmbH** certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-147">Trust the **Bit Stadium GmbH** certificate.</span></span>

<span data-ttu-id="2b2d9-148">Jeśli nim nie zajmiesz Build 2016, możesz skompilować i wdrożyć aplikację samodzielnie:</span><span class="sxs-lookup"><span data-stu-id="2b2d9-148">If you didn’t attend Build 2016, you can build and deploy the app yourself:</span></span>

1. <span data-ttu-id="2b2d9-149">Pobierz kod [z usługi GitHub].</span><span class="sxs-lookup"><span data-stu-id="2b2d9-149">Download the code [from GitHub].</span></span>
2. <span data-ttu-id="2b2d9-150">Tworzenie i wdrażanie przez [za pomocą platformy Xamarin].</span><span class="sxs-lookup"><span data-stu-id="2b2d9-150">Build and deploy by [using Xamarin].</span></span>

<span data-ttu-id="2b2d9-151">Znajdź więcej szczegółów w [MyDriving podręcznik](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="2b2d9-151">Find more details in the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="get-an-obd-adapter-optional"></a><span data-ttu-id="2b2d9-152">Pobierz adaptera diagnostycznego (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="2b2d9-152">Get an OBD adapter (optional)</span></span>
<span data-ttu-id="2b2d9-153">Jest to element, który sprawia, że to rzeczywiste systemu Internetu rzeczy!</span><span class="sxs-lookup"><span data-stu-id="2b2d9-153">This is the part that makes this a real Internet of Things system!</span></span> <span data-ttu-id="2b2d9-154">Możesz użyć aplikacji bez ani jednego, ale jest więcej fun z czegoś, a nie są kosztowne.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-154">You can use the app without one, but it’s more fun with the real thing, and they aren’t expensive.</span></span>

<span data-ttu-id="2b2d9-155">Lokalnego Diagnostyka jest funkcją samochód używającej garaż dostrajanie samochód i diagnozowanie nieparzysta szumów i świateł ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-155">On-board diagnostics (OBD) is the feature of your car that the garage uses to tune up your car and diagnose odd noises and warning lamps.</span></span> <span data-ttu-id="2b2d9-156">O ile samochód jest doskonałym antyków, znajdziesz gniazda gdzieś w podręcznego, zwykle za niestabilnością adresu w ramach pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-156">Unless your car is of great antiquity, you’ll find a socket somewhere in the cabin, typically behind a flap under the dashboard.</span></span> <span data-ttu-id="2b2d9-157">Prawy łącznik możesz pobrać metryki wydajności przez aparat i niektórych dostosować.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-157">With the right connector, you can get metrics of the engine’s performance and make certain adjustments.</span></span> <span data-ttu-id="2b2d9-158">Łącznik diagnostycznego można zakupić tanio z zwykle miejsca.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-158">An OBD connector can be purchased cheaply from the usual places.</span></span> <span data-ttu-id="2b2d9-159">Łączy za pomocą urządzenia Bluetooth lub Wi-Fi do aplikacji w telefonie.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-159">It connects by using Bluetooth or Wi-Fi to an app on your phone.</span></span>

<span data-ttu-id="2b2d9-160">W takim przypadku zamierzamy samochód nawiązać połączenia z chmurą.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-160">In this case, we’re going to connect your car to the cloud.</span></span> <span data-ttu-id="2b2d9-161">Bezpośrednie połączenie z diagnostycznego jest na Twój telefon, ale aplikacji działa jako przekaźnik.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-161">The direct connection from the OBD is to your phone, but our app works as a relay.</span></span> <span data-ttu-id="2b2d9-162">Telemetrii samochód są wysyłane bezpośrednio do Centrum MyDriving IoT, gdzie są przetwarzane do logowania użytkownika rund drogowej i oceny własnego stylu jazdy.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-162">Your car's telemetry is sent straight to the MyDriving IoT hub, where it's processed to log your road trips and assess your driving style.</span></span>

<span data-ttu-id="2b2d9-163">Aby podłączyć urządzenia diagnostycznego:</span><span class="sxs-lookup"><span data-stu-id="2b2d9-163">To connect an OBD device:</span></span>

1. <span data-ttu-id="2b2d9-164">Sprawdź, czy samochód ma gniazda diagnostycznego.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-164">Check that your car has an OBD socket.</span></span>
2. <span data-ttu-id="2b2d9-165">Uzyskaj adaptera diagnostycznego:</span><span class="sxs-lookup"><span data-stu-id="2b2d9-165">Obtain an OBD adapter:</span></span>
   
   * <span data-ttu-id="2b2d9-166">Jeśli używasz programu Android i Windows phone, potrzebna jest karta II diagnostycznego z obsługą funkcji Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span></span> <span data-ttu-id="2b2d9-167">My używamy [narzędzie skanowania OBDII Bluetooth 34t5 produktów BAFX].</span><span class="sxs-lookup"><span data-stu-id="2b2d9-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span></span>
   * <span data-ttu-id="2b2d9-168">Jeśli używasz telefonu z systemem iOS, należy adaptera diagnostycznego włączone Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span></span> <span data-ttu-id="2b2d9-169">My używamy [MX OBDLink narzędzia skanowania Wi-Fi: diagnostycznego karty/Diagnostyka skanera].</span><span class="sxs-lookup"><span data-stu-id="2b2d9-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span></span>
3. <span data-ttu-id="2b2d9-170">Postępuj zgodnie z instrukcjami dostarczonymi z kartą diagnostycznego w celu połączenia jej na Twój telefon.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-170">Follow the instructions that come with your OBD adapter to connect it to your phone.</span></span> <span data-ttu-id="2b2d9-171">Należy pamiętać, że:</span><span class="sxs-lookup"><span data-stu-id="2b2d9-171">Keep the following in mind:</span></span>
   
   * <span data-ttu-id="2b2d9-172">Karta Bluetooth muszą łączyć się z telefonu, na **ustawienia** strony.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-172">A Bluetooth adapter must be paired with the phone, on the **Settings** page.</span></span>
   * <span data-ttu-id="2b2d9-173">Karty sieci Wi-Fi musi mieć adres w 192.168.xxx.xxx zakresu.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-173">A Wi-Fi adapter must have an address in the range 192.168.xxx.xxx.</span></span>
4. <span data-ttu-id="2b2d9-174">Jeśli masz kilka samochodów, możesz uzyskać osobnej karty dla każdego (maksymalnie trzy).</span><span class="sxs-lookup"><span data-stu-id="2b2d9-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span></span>

<span data-ttu-id="2b2d9-175">Jeśli nie masz adaptera diagnostycznego aplikacja nadal będzie wysyłać dane lokalizacji i szybkość z odbiornika GPS telefonu do wewnętrznej i zapyta, czy chcesz symulować diagnostycznego.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-175">If you don’t have an OBD adapter, the app will still send location and speed data from the phone's GPS receiver to the back end and will ask if you want to simulate an OBD.</span></span>

<span data-ttu-id="2b2d9-176">Można dowiedzieć się więcej o jak aplikacja korzysta z danych z karty diagnostycznego i opcje tworzenia urządzenia diagnostycznego w sekcji 2.1 "Urządzenia IoT,", w [MyDriving podręcznik](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="2b2d9-176">You can find out more about how the app uses data from the OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="use-the-app"></a><span data-ttu-id="2b2d9-177">Za pomocą aplikacji</span><span class="sxs-lookup"><span data-stu-id="2b2d9-177">Use the app</span></span>
<span data-ttu-id="2b2d9-178">Uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-178">Start the app.</span></span> <span data-ttu-id="2b2d9-179">Brak początkowej szybkiego startu, aby zademonstrować sposób jej działania.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-179">There’s an initial Quickstart to walk you through how it works.</span></span>

### <a name="track-your-trips"></a><span data-ttu-id="2b2d9-180">Śledzenie sieci rund</span><span class="sxs-lookup"><span data-stu-id="2b2d9-180">Track your trips</span></span>
<span data-ttu-id="2b2d9-181">Naciśnij przycisk rekordu (big czerwone kółko w dolnej części ekranu) można uruchomić podróży i ponownie naciśnij, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-181">Tap the record button (big red circle at the bottom of the screen) to start a trip, and tap again to end.</span></span>

![Ilustracja przycisku rekordu podczas podróży śledzenia](./media/iot-solution-get-started/image2.png)

<span data-ttu-id="2b2d9-183">Podczas każdego uruchomienia podróży, jeśli istnieje nie jest diagnostycznego urządzeniem, użytkownik zostanie zapytany Jeśli chcesz użyć symulatora.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want to use the simulator.</span></span>

<span data-ttu-id="2b2d9-184">Na koniec podróży naciśnij przycisk Zatrzymaj, a uzyskać podsumowanie.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-184">At the end of a trip, tap the stop button, and you get a summary.</span></span>

![Przykład podróży podsumowania](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a><span data-ttu-id="2b2d9-186">Zapoznaj się z podróży</span><span class="sxs-lookup"><span data-stu-id="2b2d9-186">Review your trips</span></span>
![Przykład ostatnich podróży](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a><span data-ttu-id="2b2d9-188">Przejrzyj profilu</span><span class="sxs-lookup"><span data-stu-id="2b2d9-188">Review your profile</span></span>
![Przykład profilu zwiększają stylu](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a><span data-ttu-id="2b2d9-190">Wyślij nam swoją opinię testu</span><span class="sxs-lookup"><span data-stu-id="2b2d9-190">Send us your test feedback</span></span>
<span data-ttu-id="2b2d9-191">Ponieważ systemy IoT utworzyliśmy MyDriving ułatwiające Rozpocznij pracę chcemy pewnością poznać Twoją opinię o tym, jak działa.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-191">Because we created MyDriving to help jumpstart your own IoT systems, we certainly want to hear from you about how well it works.</span></span> <span data-ttu-id="2b2d9-192">Daj nam znać, jeśli:</span><span class="sxs-lookup"><span data-stu-id="2b2d9-192">Let us know if:</span></span>

* <span data-ttu-id="2b2d9-193">Wystąpiły problemy lub wyzwania.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-193">You run into difficulties or challenges.</span></span>
* <span data-ttu-id="2b2d9-194">Brak punktu rozszerzenia, że będą bardziej odpowiednie do realizowanego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-194">There is an extension point that would make it more suitable to your scenario.</span></span>
* <span data-ttu-id="2b2d9-195">Możesz znaleźć bardziej wydajny sposób wykonywania określonych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-195">You find a more efficient way to accomplish certain needs.</span></span>
* <span data-ttu-id="2b2d9-196">Masz inne sugestie dotyczące poprawiania MyDriving lub niniejszej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-196">You have any other suggestions for improving MyDriving or this documentation.</span></span>

<span data-ttu-id="2b2d9-197">W ramach MyDriving aplikacji, można użyć wbudowany mechanizm opinii HockeyApp: w systemach iOS i Android, wystarczy podać telefon potrząsania powoduje lub użyj **opinii** polecenia menu.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-197">Within the MyDriving app itself, you can use the built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use the **Feedback** menu command.</span></span> <span data-ttu-id="2b2d9-198">Zrzut ekranu, to dołączą automatycznie tak, aby firma Microsoft wie, co jest mowa o.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span></span> <span data-ttu-id="2b2d9-199">A w przypadku awarii (Crash) wszelkie niefortunne HockeyApp zbiera dzienniki awarii, aby poinstruować nas o nich.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-199">And if there are any unfortunate crashes, HockeyApp collects the crash logs to tell us about them.</span></span> <span data-ttu-id="2b2d9-200">Możesz też udzielić informacje zwrotne przez [portalu HockeyApp].</span><span class="sxs-lookup"><span data-stu-id="2b2d9-200">You can also give feedback through the [HockeyApp portal].</span></span>

<span data-ttu-id="2b2d9-201">Można również pliku [problem w usłudze GitHub], lub zostaw komentarz poniżej (en-us edition).</span><span class="sxs-lookup"><span data-stu-id="2b2d9-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span></span>

<span data-ttu-id="2b2d9-202">Czekamy na przesłuchanie od Ciebie!</span><span class="sxs-lookup"><span data-stu-id="2b2d9-202">We look forward to hearing from you!</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b2d9-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2b2d9-203">Next steps</span></span>
* <span data-ttu-id="2b2d9-204">Eksploruj [MyDriving podręcznik](http://aka.ms/mydrivingdocs) zrozumieć, jak wprowadzeniu zaprojektowany i zbudowany całego systemu MyDriving.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-204">Explore the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) to understand how we’ve designed and built the entire MyDriving system.</span></span>
* <span data-ttu-id="2b2d9-205">[Tworzenie i wdrażanie własnego systemu](iot-solution-build-system.md) za pomocą skryptów naszej usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span></span> <span data-ttu-id="2b2d9-206">[MyDriving podręcznik](http://aka.ms/mydrivingdocs) prowadzi użytkownika przez obszary, w których należy podjąć najbardziej dostosowania.</span><span class="sxs-lookup"><span data-stu-id="2b2d9-206">The [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make the most customizations.</span></span>

<span data-ttu-id="2b2d9-207">[z usługi GitHub]: https://github.com/Azure-Samples/MyDriving</span><span class="sxs-lookup"><span data-stu-id="2b2d9-207">[from GitHub]: https://github.com/Azure-Samples/MyDriving</span></span>
<span data-ttu-id="2b2d9-208">[za pomocą platformy Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/</span><span class="sxs-lookup"><span data-stu-id="2b2d9-208">[using Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/</span></span>
<span data-ttu-id="2b2d9-209">[narzędzie skanowania OBDII Bluetooth 34t5 produktów BAFX]: http://www.amazon.com/gp/product/B005NLQAHS</span><span class="sxs-lookup"><span data-stu-id="2b2d9-209">[BAFX Products 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS</span></span>
<span data-ttu-id="2b2d9-210">[MX OBDLink narzędzia skanowania Wi-Fi: diagnostycznego karty/Diagnostyka skanera]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP</span><span class="sxs-lookup"><span data-stu-id="2b2d9-210">[ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP</span></span>
<span data-ttu-id="2b2d9-211">[portalu HockeyApp]: https://rink.hockeyapp.org</span><span class="sxs-lookup"><span data-stu-id="2b2d9-211">[HockeyApp portal]: https://rink.hockeyapp.org</span></span>
<span data-ttu-id="2b2d9-212">[problem w usłudze GitHub]: https://github.com/Azure-Samples/MyDriving/issues</span><span class="sxs-lookup"><span data-stu-id="2b2d9-212">[issue on GitHub]: https://github.com/Azure-Samples/MyDriving/issues</span></span>
