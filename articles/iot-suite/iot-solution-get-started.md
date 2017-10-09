---
title: "Przykład MyDriving Azure IoT: Szybki start | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do aplikacji, która jest kompleksowe pokaz tooarchitect system IoT przy użyciu programu Microsoft Azure, w tym usługi Stream Analytics, Machine Learning i usługi Event Hubs."
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
ms.openlocfilehash: 411b9a992deb22b915f8291d8559e2917d976b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="mydriving-iot-system-quick-start"></a><span data-ttu-id="7344c-103">System MyDriving IoT: Szybki start</span><span class="sxs-lookup"><span data-stu-id="7344c-103">MyDriving IoT system: Quick start</span></span>
<span data-ttu-id="7344c-104">MyDriving to system, który demonstruje hello projekt i implementację typowe [Internetu rzeczy](iot-suite-overview.md) rozwiązania (IoT), który zbiera dane telemetryczne z urządzeń, przetwarzania danych w chmurze hello i stosuje uczenia maszynowego tooprovide adaptacyjną odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="7344c-104">MyDriving is a system that demonstrates hello design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in hello cloud, and applies machine learning tooprovide an adaptive response.</span></span> <span data-ttu-id="7344c-105">Pokaz Hello rejestruje dane o Twojej rund samochodu przy użyciu danych z telefonu komórkowego i karty, która zbiera informacje z systemu kontroli samochód.</span><span class="sxs-lookup"><span data-stu-id="7344c-105">hello demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span></span> <span data-ttu-id="7344c-106">Tej opinii tooprovide danych używa własnego stylu pobudzenie porównanie tooother użytkowników.</span><span class="sxs-lookup"><span data-stu-id="7344c-106">It uses this data tooprovide feedback on your driving style in comparison tooother users.</span></span>

<span data-ttu-id="7344c-107">Witaj rzeczywistego celu MyDriving jest tooget uruchomienia podczas tworzenia rozwiązania IoT.</span><span class="sxs-lookup"><span data-stu-id="7344c-107">hello real purpose of MyDriving is tooget you started in creating your own IoT solution.</span></span> <span data-ttu-id="7344c-108">Jednak przed, pomożemy Ci korzystanie z hello MyDriving aplikacja--członkiem naszego zespołu użytkownika testu.</span><span class="sxs-lookup"><span data-stu-id="7344c-108">But before that, let’s get you going with hello MyDriving app itself--as a member of our test user team.</span></span> <span data-ttu-id="7344c-109">Zapewnia to środowisko aplikacji hello i systemie hello za nią klientów, przed delve w architekturze hello.</span><span class="sxs-lookup"><span data-stu-id="7344c-109">This gives you an experience of hello app and hello system behind it as a consumer, before you delve into hello architecture.</span></span> <span data-ttu-id="7344c-110">On również przedstawiono tooHockeyApp, chłodnych sposób zarządzania hello alfa i beta dystrybucje użytkowników tootest aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7344c-110">It also introduces you tooHockeyApp, a cool way of managing hello alpha and beta distributions of your apps tootest users.</span></span>

## <a name="use-hello-mobile-experience"></a><span data-ttu-id="7344c-111">Użyj hello korzystanie z urządzeń przenośnych</span><span class="sxs-lookup"><span data-stu-id="7344c-111">Use hello mobile experience</span></span>
<span data-ttu-id="7344c-112">Możesz użyć aplikacji MyDriving hello, jeśli masz urządzenia z systemem Android, iOS i Windows 10.</span><span class="sxs-lookup"><span data-stu-id="7344c-112">You can use hello MyDriving app if you have an Android, iOS, or Windows 10 device.</span></span>

### <a name="android-and-windows-10-mobile-installation"></a><span data-ttu-id="7344c-113">Android i Windows 10 Mobile instalacji</span><span class="sxs-lookup"><span data-stu-id="7344c-113">Android and Windows 10 Mobile installation</span></span>
<span data-ttu-id="7344c-114">Na urządzeniu:</span><span class="sxs-lookup"><span data-stu-id="7344c-114">On your device:</span></span>

1. <span data-ttu-id="7344c-115">Zezwalaj na projektowanie aplikacji:</span><span class="sxs-lookup"><span data-stu-id="7344c-115">Allow development apps:</span></span>
   
   * <span data-ttu-id="7344c-116">System android: W **ustawienia** > **zabezpieczeń**, Zezwalaj na aplikacje z **nieznane źródła**.</span><span class="sxs-lookup"><span data-stu-id="7344c-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span></span>
   * <span data-ttu-id="7344c-117">Systemie Windows 10: **ustawienia** > **aktualizacje** > **dla deweloperów**ustaw **tryb dewelopera**.</span><span class="sxs-lookup"><span data-stu-id="7344c-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span></span>
2. <span data-ttu-id="7344c-118">Dołącz nasz zespół beta testu przez zarejestrowanie u lub zalogowanie się do, [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="7344c-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span></span> <span data-ttu-id="7344c-119">Platforma HockeyApp umożliwia łatwe toodistribute Wczesne wersje użytkownikom tootest aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7344c-119">HockeyApp makes it easy toodistribute early releases of your app tootest users.</span></span>
   
   <span data-ttu-id="7344c-120">Jeśli używasz systemu Windows 10 za pomocą przeglądarki Edge hello.</span><span class="sxs-lookup"><span data-stu-id="7344c-120">If you’re using Windows 10, use hello Edge browser.</span></span>
   
   <span data-ttu-id="7344c-121">Gdyby uczestnika Build 2016, zaloguj się przy użyciu hello sam e-mail konta Microsoft, zarejestrowanego konferencji hello przy użyciu jednej z hello przycisków firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7344c-121">If you were a Build 2016 attendee, sign in with hello same Microsoft account email that you registered for hello conference, by using one of hello Microsoft buttons.</span></span> <span data-ttu-id="7344c-122">Użytkownik już jest zalogowany z HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="7344c-122">You’re already signed up with HockeyApp.</span></span>
   
   ![Platforma HockeyApp ekranu logowania](./media/iot-solution-get-started/image1.png)
3. <span data-ttu-id="7344c-124">Pobierz i zainstaluj aplikacji hello w tym miejscu:</span><span class="sxs-lookup"><span data-stu-id="7344c-124">Download and install hello app from here:</span></span>
   
   * [<span data-ttu-id="7344c-125">Android</span><span class="sxs-lookup"><span data-stu-id="7344c-125">Android</span></span>](http://rink.io/spMyDrivingAndroid)
   * [<span data-ttu-id="7344c-126">Windows 10</span><span class="sxs-lookup"><span data-stu-id="7344c-126">Windows 10</span></span>](http://rink.io/spMyDrivingUWP)
   
   <span data-ttu-id="7344c-127">Istnieją dwa elementy.</span><span class="sxs-lookup"><span data-stu-id="7344c-127">There are two items.</span></span> <span data-ttu-id="7344c-128">Zainstaluj certyfikat hello w **zaufane osoby**.</span><span class="sxs-lookup"><span data-stu-id="7344c-128">Install hello certificate in **Trusted People**.</span></span> <span data-ttu-id="7344c-129">Następnie zainstaluj aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="7344c-129">Then install hello app.</span></span>

<span data-ttu-id="7344c-130">*Uruchamianie aplikacji hello w systemie Windows 10 Mobile problemy?*</span><span class="sxs-lookup"><span data-stu-id="7344c-130">*Any issues starting hello app on Windows 10 Mobile?*</span></span> <span data-ttu-id="7344c-131">Twój telefon może być aktualizacja lub dwóch za.</span><span class="sxs-lookup"><span data-stu-id="7344c-131">Your phone might be an update or two behind.</span></span> <span data-ttu-id="7344c-132">Upewnij się, otrzymasz najnowsze aktualizacje hello, lub zainstalować:</span><span class="sxs-lookup"><span data-stu-id="7344c-132">Make sure you've got hello latest updates, or install:</span></span>

* [<span data-ttu-id="7344c-133">Microsoft.NET.Native.Framework.1.2.appx</span><span class="sxs-lookup"><span data-stu-id="7344c-133">Microsoft.NET.Native.Framework.1.2.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [<span data-ttu-id="7344c-134">Microsoft.NET.Native.Runtime.1.1.appx</span><span class="sxs-lookup"><span data-stu-id="7344c-134">Microsoft.NET.Native.Runtime.1.1.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [<span data-ttu-id="7344c-135">Microsoft.VCLibs.ARM.14.00.appx</span><span class="sxs-lookup"><span data-stu-id="7344c-135">Microsoft.VCLibs.ARM.14.00.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a><span data-ttu-id="7344c-136">Instalacja systemu iOS</span><span class="sxs-lookup"><span data-stu-id="7344c-136">iOS installation</span></span>
<span data-ttu-id="7344c-137">Jeśli Twoja Build 2016, należy pobrać aplikację hello członkiem naszego zespołu testowego na platformę HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="7344c-137">If you attended Build 2016, download hello app as a member of our test team on HockeyApp:</span></span>

1. <span data-ttu-id="7344c-138">Na urządzeniu z systemem iOS, zaloguj się za[HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="7344c-138">On your iOS device, sign in too[HockeyApp](https://rink.hockeyapp.net).</span></span>
   <span data-ttu-id="7344c-139">Użycie hello jeden hello Microsoft logowania przycisków i zaloguj się przy użyciu tego samego e-mail konta Microsoft, który został zarejestrowany z konferencji hello.</span><span class="sxs-lookup"><span data-stu-id="7344c-139">Use one of hello Microsoft sign-in buttons, and sign in with hello same Microsoft account email that you registered with hello conference.</span></span> <span data-ttu-id="7344c-140">(Nie używaj hello pola wiadomości e-mail i hasło).</span><span class="sxs-lookup"><span data-stu-id="7344c-140">(Don’t use hello email and password fields.)</span></span>
   
   ![Platforma HockeyApp ekranu logowania](./media/iot-solution-get-started/image1.png)
2. <span data-ttu-id="7344c-142">Na pulpicie nawigacyjnym aplikacji HockeyApp hello wybierz MyDriving i pobierz go.</span><span class="sxs-lookup"><span data-stu-id="7344c-142">In hello HockeyApp dashboard, select MyDriving and download it.</span></span>
3. <span data-ttu-id="7344c-143">Autoryzowanie hello wydanie beta z HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="7344c-143">Authorize hello beta release from HockeyApp:</span></span>
   
   <span data-ttu-id="7344c-144">a.</span><span class="sxs-lookup"><span data-stu-id="7344c-144">a.</span></span> <span data-ttu-id="7344c-145">Przejdź za**ustawienia** > **ogólne** > **profilów i zarządzania urządzeniami.**</span><span class="sxs-lookup"><span data-stu-id="7344c-145">Go too**Settings** > **General** > **Profiles and Device Management.**</span></span>
   
   <span data-ttu-id="7344c-146">b.</span><span class="sxs-lookup"><span data-stu-id="7344c-146">b.</span></span> <span data-ttu-id="7344c-147">Zaufania hello **Bit Stadium GmbH** certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="7344c-147">Trust hello **Bit Stadium GmbH** certificate.</span></span>

<span data-ttu-id="7344c-148">Jeśli nim nie zajmiesz Build 2016, możesz skompilować i wdrożyć aplikacji hello samodzielnie:</span><span class="sxs-lookup"><span data-stu-id="7344c-148">If you didn’t attend Build 2016, you can build and deploy hello app yourself:</span></span>

1. <span data-ttu-id="7344c-149">Pobierz kod hello [z usługi GitHub].</span><span class="sxs-lookup"><span data-stu-id="7344c-149">Download hello code [from GitHub].</span></span>
2. <span data-ttu-id="7344c-150">Tworzenie i wdrażanie przez [za pomocą platformy Xamarin].</span><span class="sxs-lookup"><span data-stu-id="7344c-150">Build and deploy by [using Xamarin].</span></span>

<span data-ttu-id="7344c-151">Więcej szczegółów znajduje się w hello [MyDriving podręcznik](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="7344c-151">Find more details in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="get-an-obd-adapter-optional"></a><span data-ttu-id="7344c-152">Pobierz adaptera diagnostycznego (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="7344c-152">Get an OBD adapter (optional)</span></span>
<span data-ttu-id="7344c-153">To jest część hello, który sprawia, że to rzeczywiste systemu Internetu rzeczy!</span><span class="sxs-lookup"><span data-stu-id="7344c-153">This is hello part that makes this a real Internet of Things system!</span></span> <span data-ttu-id="7344c-154">Możesz użyć aplikacji hello bez ani jednego, ale jest więcej fun z czegoś hello, a nie są kosztowne.</span><span class="sxs-lookup"><span data-stu-id="7344c-154">You can use hello app without one, but it’s more fun with hello real thing, and they aren’t expensive.</span></span>

<span data-ttu-id="7344c-155">Lokalnego Diagnostyka to funkcja hello samochód hello garaż tootune używa się samochód i diagnozowanie nieparzysta szumów i świateł ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="7344c-155">On-board diagnostics (OBD) is hello feature of your car that hello garage uses tootune up your car and diagnose odd noises and warning lamps.</span></span> <span data-ttu-id="7344c-156">O ile samochód jest doskonałym antyków, znajdziesz gniazda gdzieś w podręcznego hello, zwykle za niestabilnością adresu w obszarze hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="7344c-156">Unless your car is of great antiquity, you’ll find a socket somewhere in hello cabin, typically behind a flap under hello dashboard.</span></span> <span data-ttu-id="7344c-157">Łącznik prawo hello możesz pobrać metryki wydajności hello aparatu i niektórych dostosować.</span><span class="sxs-lookup"><span data-stu-id="7344c-157">With hello right connector, you can get metrics of hello engine’s performance and make certain adjustments.</span></span> <span data-ttu-id="7344c-158">Łącznik diagnostycznego można zakupić tanio z takich miejsc, zwykle hello.</span><span class="sxs-lookup"><span data-stu-id="7344c-158">An OBD connector can be purchased cheaply from hello usual places.</span></span> <span data-ttu-id="7344c-159">Łączy przy użyciu aplikacji tooan Bluetooth lub Wi-Fi na telefonie.</span><span class="sxs-lookup"><span data-stu-id="7344c-159">It connects by using Bluetooth or Wi-Fi tooan app on your phone.</span></span>

<span data-ttu-id="7344c-160">W takim przypadku zamierzamy tooconnect samochodu toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="7344c-160">In this case, we’re going tooconnect your car toohello cloud.</span></span> <span data-ttu-id="7344c-161">bezpośrednie połączenie hello diagnostycznego Hello jest tooyour telefon, ale aplikacji działa jako przekaźnik.</span><span class="sxs-lookup"><span data-stu-id="7344c-161">hello direct connection from hello OBD is tooyour phone, but our app works as a relay.</span></span> <span data-ttu-id="7344c-162">Dane telemetryczne samochód jest wysyłany proste toohello Centrum MyDriving IoT, w którym jest przetwarzanie toolog Twojego rund drogowej i oceny własnego stylu jazdy.</span><span class="sxs-lookup"><span data-stu-id="7344c-162">Your car's telemetry is sent straight toohello MyDriving IoT hub, where it's processed toolog your road trips and assess your driving style.</span></span>

<span data-ttu-id="7344c-163">tooconnect urządzenia diagnostycznego:</span><span class="sxs-lookup"><span data-stu-id="7344c-163">tooconnect an OBD device:</span></span>

1. <span data-ttu-id="7344c-164">Sprawdź, czy samochód ma gniazda diagnostycznego.</span><span class="sxs-lookup"><span data-stu-id="7344c-164">Check that your car has an OBD socket.</span></span>
2. <span data-ttu-id="7344c-165">Uzyskaj adaptera diagnostycznego:</span><span class="sxs-lookup"><span data-stu-id="7344c-165">Obtain an OBD adapter:</span></span>
   
   * <span data-ttu-id="7344c-166">Jeśli używasz programu Android i Windows phone, potrzebna jest karta II diagnostycznego z obsługą funkcji Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="7344c-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span></span> <span data-ttu-id="7344c-167">My używamy [narzędzie skanowania OBDII Bluetooth 34t5 produktów BAFX].</span><span class="sxs-lookup"><span data-stu-id="7344c-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span></span>
   * <span data-ttu-id="7344c-168">Jeśli używasz telefonu z systemem iOS, należy adaptera diagnostycznego włączone Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="7344c-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span></span> <span data-ttu-id="7344c-169">My używamy [MX OBDLink narzędzia skanowania Wi-Fi: diagnostycznego karty/Diagnostyka skanera].</span><span class="sxs-lookup"><span data-stu-id="7344c-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span></span>
3. <span data-ttu-id="7344c-170">Wykonaj instrukcje hello dostarczanych z Twojej tooconnect adaptera diagnostycznego go tooyour telefonu.</span><span class="sxs-lookup"><span data-stu-id="7344c-170">Follow hello instructions that come with your OBD adapter tooconnect it tooyour phone.</span></span> <span data-ttu-id="7344c-171">Pamiętać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7344c-171">Keep hello following in mind:</span></span>
   
   * <span data-ttu-id="7344c-172">Karta Bluetooth muszą łączyć się z telefonu hello, na powitania **ustawienia** strony.</span><span class="sxs-lookup"><span data-stu-id="7344c-172">A Bluetooth adapter must be paired with hello phone, on hello **Settings** page.</span></span>
   * <span data-ttu-id="7344c-173">Karty sieci Wi-Fi musi mieć adres w hello 192.168.xxx.xxx zakresu.</span><span class="sxs-lookup"><span data-stu-id="7344c-173">A Wi-Fi adapter must have an address in hello range 192.168.xxx.xxx.</span></span>
4. <span data-ttu-id="7344c-174">Jeśli masz kilka samochodów, możesz uzyskać osobnej karty dla każdego (maksymalnie trzy).</span><span class="sxs-lookup"><span data-stu-id="7344c-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span></span>

<span data-ttu-id="7344c-175">Jeśli nie masz adaptera diagnostycznego aplikacji hello nadal będzie wysyłać, lokalizacji i szybkości danych z telefonu hello GPS odbiornika toohello ponownie zakończyć i zapyta, czy ma toosimulate diagnostycznego.</span><span class="sxs-lookup"><span data-stu-id="7344c-175">If you don’t have an OBD adapter, hello app will still send location and speed data from hello phone's GPS receiver toohello back end and will ask if you want toosimulate an OBD.</span></span>

<span data-ttu-id="7344c-176">Znajduje się więcej o używaniu danych z karty diagnostycznego hello aplikacji hello i opcje tworzenia urządzenia diagnostycznego w sekcji 2.1 "Urządzenia IoT," w hello [MyDriving podręcznik](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="7344c-176">You can find out more about how hello app uses data from hello OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="use-hello-app"></a><span data-ttu-id="7344c-177">Użycie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="7344c-177">Use hello app</span></span>
<span data-ttu-id="7344c-178">Uruchamiają aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="7344c-178">Start hello app.</span></span> <span data-ttu-id="7344c-179">Brak początkowej toowalk szybkiego startu sposób jej działania.</span><span class="sxs-lookup"><span data-stu-id="7344c-179">There’s an initial Quickstart toowalk you through how it works.</span></span>

### <a name="track-your-trips"></a><span data-ttu-id="7344c-180">Śledzenie sieci rund</span><span class="sxs-lookup"><span data-stu-id="7344c-180">Track your trips</span></span>
<span data-ttu-id="7344c-181">Wybierz hello przycisk rekordów (big czerwone kółko u dołu ekranu hello hello) toostart podróży, a następnie ponownie wybierz tooend.</span><span class="sxs-lookup"><span data-stu-id="7344c-181">Tap hello record button (big red circle at hello bottom of hello screen) toostart a trip, and tap again tooend.</span></span>

![Ilustracja przycisku rekordu hello podczas podróży śledzenia](./media/iot-solution-get-started/image2.png)

<span data-ttu-id="7344c-183">Każdym uruchomieniu podróży, jeśli istnieje nie jest diagnostycznego urządzeniem, użytkownik zostanie zapytany czy ma toouse hello symulatora.</span><span class="sxs-lookup"><span data-stu-id="7344c-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want toouse hello simulator.</span></span>

<span data-ttu-id="7344c-184">Naciśnij hello Zatrzymaj przycisku, a na końcu hello podróży, uzyskać podsumowanie.</span><span class="sxs-lookup"><span data-stu-id="7344c-184">At hello end of a trip, tap hello stop button, and you get a summary.</span></span>

![Przykład podróży podsumowania](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a><span data-ttu-id="7344c-186">Zapoznaj się z podróży</span><span class="sxs-lookup"><span data-stu-id="7344c-186">Review your trips</span></span>
![Przykład ostatnich podróży](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a><span data-ttu-id="7344c-188">Przejrzyj profilu</span><span class="sxs-lookup"><span data-stu-id="7344c-188">Review your profile</span></span>
![Przykład profilu zwiększają stylu](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a><span data-ttu-id="7344c-190">Wyślij nam swoją opinię testu</span><span class="sxs-lookup"><span data-stu-id="7344c-190">Send us your test feedback</span></span>
<span data-ttu-id="7344c-191">Ponieważ utworzyliśmy Rozpocznij pracę toohelp MyDriving systemów IoT chcemy pewnością toohear od użytkownika o tym, jak działa.</span><span class="sxs-lookup"><span data-stu-id="7344c-191">Because we created MyDriving toohelp jumpstart your own IoT systems, we certainly want toohear from you about how well it works.</span></span> <span data-ttu-id="7344c-192">Daj nam znać, jeśli:</span><span class="sxs-lookup"><span data-stu-id="7344c-192">Let us know if:</span></span>

* <span data-ttu-id="7344c-193">Wystąpiły problemy lub wyzwania.</span><span class="sxs-lookup"><span data-stu-id="7344c-193">You run into difficulties or challenges.</span></span>
* <span data-ttu-id="7344c-194">Brak punktu rozszerzenia, że będą bardziej odpowiedni scenariusz tooyour.</span><span class="sxs-lookup"><span data-stu-id="7344c-194">There is an extension point that would make it more suitable tooyour scenario.</span></span>
* <span data-ttu-id="7344c-195">Efektywniejsze tooaccomplish sposób znaleźć określonych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="7344c-195">You find a more efficient way tooaccomplish certain needs.</span></span>
* <span data-ttu-id="7344c-196">Masz inne sugestie dotyczące poprawiania MyDriving lub niniejszej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="7344c-196">You have any other suggestions for improving MyDriving or this documentation.</span></span>

<span data-ttu-id="7344c-197">W ramach hello MyDriving samej aplikacji, można użyć hello wbudowany mechanizm opinii HockeyApp: w systemach iOS i Android, wystarczy podać telefon potrząsania powoduje lub użyj hello **opinii** polecenia menu.</span><span class="sxs-lookup"><span data-stu-id="7344c-197">Within hello MyDriving app itself, you can use hello built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use hello **Feedback** menu command.</span></span> <span data-ttu-id="7344c-198">Zrzut ekranu, to dołączą automatycznie tak, aby firma Microsoft wie, co jest mowa o.</span><span class="sxs-lookup"><span data-stu-id="7344c-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span></span> <span data-ttu-id="7344c-199">Oraz w przypadku awarii (Crash) wszelkie niefortunne HockeyApp zbiera tootell dzienniki awarii hello nas o nich.</span><span class="sxs-lookup"><span data-stu-id="7344c-199">And if there are any unfortunate crashes, HockeyApp collects hello crash logs tootell us about them.</span></span> <span data-ttu-id="7344c-200">Możesz też udzielić informacje zwrotne przez hello [portalu HockeyApp].</span><span class="sxs-lookup"><span data-stu-id="7344c-200">You can also give feedback through hello [HockeyApp portal].</span></span>

<span data-ttu-id="7344c-201">Można również pliku [problem w usłudze GitHub], lub zostaw komentarz poniżej (en-us edition).</span><span class="sxs-lookup"><span data-stu-id="7344c-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span></span>

<span data-ttu-id="7344c-202">Mamy nadzieję toohearing od Ciebie!</span><span class="sxs-lookup"><span data-stu-id="7344c-202">We look forward toohearing from you!</span></span>

## <a name="next-steps"></a><span data-ttu-id="7344c-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7344c-203">Next steps</span></span>
* <span data-ttu-id="7344c-204">Eksploruj hello [MyDriving podręcznik](http://aka.ms/mydrivingdocs) toounderstand jak wprowadzeniu zaprojektowany i zbudowany hello całego systemu MyDriving.</span><span class="sxs-lookup"><span data-stu-id="7344c-204">Explore hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) toounderstand how we’ve designed and built hello entire MyDriving system.</span></span>
* <span data-ttu-id="7344c-205">[Tworzenie i wdrażanie własnego systemu](iot-solution-build-system.md) za pomocą skryptów naszej usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7344c-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span></span> <span data-ttu-id="7344c-206">Witaj [MyDriving podręcznik](http://aka.ms/mydrivingdocs) prowadzi użytkownika przez obszary, w których należy podjąć hello większości dostosowań.</span><span class="sxs-lookup"><span data-stu-id="7344c-206">hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make hello most customizations.</span></span>

[z usługi GitHub]: https://github.com/Azure-Samples/MyDriving
[za pomocą platformy Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[narzędzie skanowania OBDII Bluetooth 34t5 produktów BAFX]: http://www.amazon.com/gp/product/B005NLQAHS
[MX OBDLink narzędzia skanowania Wi-Fi: diagnostycznego karty/Diagnostyka skanera]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[portalu HockeyApp]: https://rink.hockeyapp.org
[problem w usłudze GitHub]: https://github.com/Azure-Samples/MyDriving/issues
