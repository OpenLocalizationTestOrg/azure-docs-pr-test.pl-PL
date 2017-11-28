---
title: "tooiOS powiadomienia wypychane aaaSending przy użyciu usługi Azure Notification Hubs | Dokumentacja firmy Microsoft"
description: "Z tego samouczka dowiesz się, jak toosend usługi Azure Notification Hubs toouse wypychanych aplikacji dla systemu iOS tooan powiadomienia."
services: notification-hubs
documentationcenter: ios
keywords: powiadomienie wypychane, powiadomienia wypychane, powiadomienia wypychane w systemie ios
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a><span data-ttu-id="542c3-104">Wysyłanie tooiOS powiadomień wypychanych przy użyciu usługi Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="542c3-104">Sending push notifications tooiOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="542c3-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="542c3-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="542c3-106">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="542c3-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="542c3-107">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="542c3-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="542c3-108">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="542c3-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="542c3-109">Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse wypychanych aplikacji dla systemu iOS tooan powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="542c3-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span> <span data-ttu-id="542c3-110">Utworzysz aplikację iOS puste, która odbiera powiadomienia wypychane przy użyciu hello [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span><span class="sxs-lookup"><span data-stu-id="542c3-110">You'll create a blank iOS app that receives push notifications by using hello [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="542c3-111">Po zakończeniu będziesz w stanie toouse Twojego toobroadcast Centrum powiadomień wypychanych powiadomienia tooall hello urządzeń z tą aplikacją.</span><span class="sxs-lookup"><span data-stu-id="542c3-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="542c3-112">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="542c3-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="542c3-113">Kod ukończyć powitalnych dla tego samouczka można znaleźć [w serwisie GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="542c3-113">hello completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="542c3-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="542c3-114">Prerequisites</span></span>
<span data-ttu-id="542c3-115">Ten samouczek wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="542c3-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="542c3-116">[usług Mobile Services systemu iOS SDK w wersji 1.2.4]</span><span class="sxs-lookup"><span data-stu-id="542c3-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="542c3-117">Najnowsza wersja środowiska [Xcode]</span><span class="sxs-lookup"><span data-stu-id="542c3-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="542c3-118">Urządzenie zgodne z systemem iOS 8 (lub nowszą wersją)</span><span class="sxs-lookup"><span data-stu-id="542c3-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="542c3-119">Członkostwo w [programie dla deweloperów firmy Apple](https://developer.apple.com/programs/)</span><span class="sxs-lookup"><span data-stu-id="542c3-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="542c3-120">Ze względu na wymagania dotyczące konfiguracji powiadomień wypychanych należy wdrożyć i przetestować powiadomienia wypychane na urządzenie fizyczne z systemem iOS (iPhone i iPad) zamiast hello symulatora systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="542c3-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of hello iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="542c3-121">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Notification Hubs dotyczących aplikacji dla systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="542c3-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="542c3-122">Konfigurowanie centrum powiadomień dla powiadomień wypychanych systemu iOS</span><span class="sxs-lookup"><span data-stu-id="542c3-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="542c3-123">Ta sekcja przeprowadzi Cię przez proces tworzenia nowego centrum powiadomień i konfigurowania uwierzytelniania w usłudze APNS przy użyciu hello **.p12** utworzony certyfikat wypychania.</span><span class="sxs-lookup"><span data-stu-id="542c3-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="542c3-124">Jeśli chcesz toouse Centrum powiadomień, które zostały już utworzone, możesz pominąć toostep 5.</span><span class="sxs-lookup"><span data-stu-id="542c3-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="542c3-125">Kliknij przycisk hello <b>usługi powiadomień</b> przycisku na powitania <b>ustawienia</b> bloku, następnie wybierz <b>Apple (APNS)</b>.</span><span class="sxs-lookup"><span data-stu-id="542c3-125">Click hello <b>Notification Services</b> button in hello <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="542c3-126">Polecenie <b>Przekaż certyfikat</b> i wybierz hello <b>.p12</b> wcześniej wyeksportowany plik.</span><span class="sxs-lookup"><span data-stu-id="542c3-126">Click on <b>Upload Certificate</b> and select hello <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="542c3-127">Upewnij się, że należy także określić hello poprawne hasło.</span><span class="sxs-lookup"><span data-stu-id="542c3-127">Make sure you also specify hello correct password.</span></span></p>

<p><span data-ttu-id="542c3-128">Upewnij się, że tooselect <b>piaskownicy</b> trybu, ponieważ jest to do tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="542c3-128">Make sure tooselect <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="542c3-129">Używaj tylko hello <b>produkcji</b> Chcąc toosend toousers powiadomień wypychanych, którzy kupili twoją aplikację w sklepie hello.</span><span class="sxs-lookup"><span data-stu-id="542c3-129">Only use hello <b>Production</b> if you want toosend push notifications toousers who purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="542c3-130">&emsp;&emsp;&emsp;&emsp;![Konfigurowanie usługi APNS w portalu Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="542c3-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![Konfigurowanie certyfikacji APNs w witrynie Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="542c3-132">Centrum powiadomień jest teraz skonfigurowany toowork przy użyciu usługi APNS i mieć tooregister ciągów połączenia hello aplikacji oraz wysyłać powiadomienia wypychane.</span><span class="sxs-lookup"><span data-stu-id="542c3-132">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-toonotification-hubs"></a><span data-ttu-id="542c3-133">Połącz z tooNotification aplikacji systemu iOS koncentratory</span><span class="sxs-lookup"><span data-stu-id="542c3-133">Connect your iOS app tooNotification Hubs</span></span>
1. <span data-ttu-id="542c3-134">W środowisku Xcode Utwórz nowy projekt dla systemu iOS, a następnie wybierz hello **pojedynczą aplikacją widoku** szablonu.</span><span class="sxs-lookup"><span data-stu-id="542c3-134">In Xcode, create a new iOS project and select hello **Single View Application** template.</span></span>
   
    ![Xcode — aplikacja z jednym widokiem][8]
    
2. <span data-ttu-id="542c3-136">Podczas ustawiania opcji hello nowego projektu, upewnij się, toouse hello sam **nazwa produktu** i **identyfikator organizacji** które zostały użyte podczas wcześniejszego ustawiania Identyfikatora pakietu hello na powitania deweloperów firmy Apple Portal.</span><span class="sxs-lookup"><span data-stu-id="542c3-136">When setting hello options for your new project, make sure toouse hello same **Product Name** and **Organization Identifier** that you used when you previously set hello bundle ID on hello Apple Developer portal.</span></span>
   
    ![Xcode — opcje projektu][11]
    
3. <span data-ttu-id="542c3-138">W obszarze **elementy docelowe**, kliknij nazwę projektu, kliknij przycisk hello **ustawieniach kompilacji** karcie i rozwiń **tożsamość podpisywania kodu**, a następnie w obszarze **debugowania**, ustaw swoją tożsamość podpisywania kodu.</span><span class="sxs-lookup"><span data-stu-id="542c3-138">Under **Targets**, click your project name, click hello **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="542c3-139">Przełącz **poziomy** z **podstawowe** za**wszystkie**i ustaw **profilu inicjowania obsługi administracyjnej** toohello profil utworzony wcześniej inicjowania obsługi administracyjnej .</span><span class="sxs-lookup"><span data-stu-id="542c3-139">Toggle **Levels** from **Basic** too**All**, and set **Provisioning Profile** toohello provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="542c3-140">Jeśli nie widzisz hello nowych inicjowania obsługi profilu utworzonego w programie Xcode, spróbuj odświeżyć hello profile dla Twojej tożsamości podpisywania.</span><span class="sxs-lookup"><span data-stu-id="542c3-140">If you don't see hello new provisioning profile that you created in Xcode, try refreshing hello profiles for your signing identity.</span></span> <span data-ttu-id="542c3-141">Kliknij przycisk **Xcode** hello paska menu, kliknij przycisk **preferencje**, kliknij hello **konta** , kliknij pozycję hello **Wyświetl szczegóły** , kliknij użytkownika tożsamość podpisywania, a następnie kliknij przycisk Odśwież hello hello prawym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="542c3-141">Click **Xcode** on hello menu bar, click **Preferences**, click hello **Account** tab, click hello **View Details** button, click your signing identity, and then click hello refresh button in hello bottom-right corner.</span></span>
   
    ![Xcode — profil aprowizowania][9]
4. <span data-ttu-id="542c3-143">Pobierz hello [usług Mobile Services systemu iOS SDK w wersji 1.2.4] i rozpakuj plik hello.</span><span class="sxs-lookup"><span data-stu-id="542c3-143">Download hello [Mobile Services iOS SDK version 1.2.4] and unzip hello file.</span></span> <span data-ttu-id="542c3-144">W programie Xcode, kliknij prawym przyciskiem myszy projekt i kliknij przycisk hello **Dodaj pliki do** hello tooadd opcji **WindowsAzureMessaging.framework** projektu Xcode tooyour folderu.</span><span class="sxs-lookup"><span data-stu-id="542c3-144">In Xcode, right-click your project and click hello **Add Files to** option tooadd hello **WindowsAzureMessaging.framework** folder tooyour Xcode project.</span></span> <span data-ttu-id="542c3-145">Wybierz pozycję **Copy items if needed** (Skopiuj elementy w razie potrzeby), a następnie kliknij pozycję **Add** (Dodaj).</span><span class="sxs-lookup"><span data-stu-id="542c3-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="542c3-146">centra powiadomień Hello zestawu SDK nie obsługuje obecnie kodu bitowego w programie Xcode 7.</span><span class="sxs-lookup"><span data-stu-id="542c3-146">hello notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="542c3-147">Należy ustawić **włączyć Bitcode** za**nr** w hello **opcji kompilacji** dla projektu.</span><span class="sxs-lookup"><span data-stu-id="542c3-147">You must set **Enable Bitcode** too**No** in hello **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Rozpakowywanie zestawu SDK platformy Azure][10]
5. <span data-ttu-id="542c3-149">Dodawanie nowego nagłówka pliku tooyour projektu o nazwie `HubInfo.h`.</span><span class="sxs-lookup"><span data-stu-id="542c3-149">Add a new header file tooyour project named `HubInfo.h`.</span></span> <span data-ttu-id="542c3-150">Ten plik będzie zawierać hello stałe dla Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="542c3-150">This file will hold hello constants for your notification hub.</span></span>  <span data-ttu-id="542c3-151">Dodaj następujące definicje hello i Zastąp hello symbole zastępcze literału ciągu z Twojej *nazwy centrum* i hello *DefaultListenSharedAccessSignature* zanotowany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="542c3-151">Add hello following definitions and replace hello string literal placeholders with your *hub name* and hello *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="542c3-152">Otwórz z `AppDelegate.h` pliku Dodaj następujące dyrektywy importu hello:</span><span class="sxs-lookup"><span data-stu-id="542c3-152">Open your `AppDelegate.h` file add hello following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="542c3-153">W Twojej `AppDelegate.m file`, Dodaj hello następującego kodu w hello `didFinishLaunchingWithOptions` zależnie od wersji systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="542c3-153">In your `AppDelegate.m file`, add hello following code in hello `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="542c3-154">Ten kod rejestruje dojście do urządzenia w usłudze APNs:</span><span class="sxs-lookup"><span data-stu-id="542c3-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="542c3-155">Dla systemu iOS 8:</span><span class="sxs-lookup"><span data-stu-id="542c3-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="542c3-156">Dla too8 wcześniejsze wersje systemu iOS:</span><span class="sxs-lookup"><span data-stu-id="542c3-156">For iOS versions prior too8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="542c3-157">W hello tego samego pliku, Dodaj następujące metody hello.</span><span class="sxs-lookup"><span data-stu-id="542c3-157">In hello same file, add hello following methods.</span></span> <span data-ttu-id="542c3-158">Ten kod łączy toohello Centrum powiadomień przy użyciu hello informacji o połączeniu określonych w pliku HubInfo.h.</span><span class="sxs-lookup"><span data-stu-id="542c3-158">This code connects toohello notification hub using hello connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="542c3-159">Następnie przekazuje Centrum powiadomień token toohello urządzenia hello tak, aby hello Centrum powiadomień może wysyłać powiadomienia:</span><span class="sxs-lookup"><span data-stu-id="542c3-159">It then gives hello device token toohello notification hub so that hello notification hub can send notifications:</span></span>
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. <span data-ttu-id="542c3-160">W hello tego samego pliku, Dodaj następujące metody toodisplay hello **UIAlert** w przypadku otrzymania powiadomienia hello, gdy aplikacja hello jest aktywna:</span><span class="sxs-lookup"><span data-stu-id="542c3-160">In hello same file, add hello following method toodisplay a **UIAlert** if hello notification is received while hello app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="542c3-161">Tworzenie i uruchamianie aplikacji hello na tooverify Twojego urządzenia, czy nie występują żadne błędy.</span><span class="sxs-lookup"><span data-stu-id="542c3-161">Build and run hello app on your device tooverify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="542c3-162">Wysyłanie testowych powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="542c3-162">Send test push notifications</span></span>
<span data-ttu-id="542c3-163">Możesz przetestować odbieranie powiadomień w aplikacji przez wysyłanie powiadomień wypychanych w hello [Azure Portal] za pośrednictwem hello **Rozwiązywanie problemów** sekcji w bloku Centrum hello (Użyj hello *Wysyłanietestowe* opcja).</span><span class="sxs-lookup"><span data-stu-id="542c3-163">You can test receiving notifications in your app by sending push notifications in hello [Azure Portal] via hello **Troubleshooting** section in hello hub blade (use hello *Test Send* option).</span></span>

![Portal Azure — wysyłanie testowe][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a><span data-ttu-id="542c3-165">(Opcjonalnie) Wysyłanie powiadomień wypychanych z aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="542c3-165">(Optional) Send push notifications from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="542c3-166">Przykładem wysyłania powiadomień z powitania klienta aplikacji jest dostępna dla tylko do celów szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="542c3-166">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="542c3-167">Ponieważ wymaga to hello `DefaultFullSharedAccessSignature` toobe na powitania klienta aplikacji, opisuje czy użytkownik może uzyskać powiadomienia toosend nieautoryzowany dostęp tooyour klientów ryzyko toohello Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="542c3-167">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="542c3-168">Jeśli chcesz toosend powiadomień wypychanych z poziomu aplikacji, ta sekcja zawiera przykładowy sposób toodo to przy użyciu hello interfejsu REST.</span><span class="sxs-lookup"><span data-stu-id="542c3-168">If you want toosend push notifications from within an app, this section provides an example of how toodo this using hello REST interface.</span></span>

1. <span data-ttu-id="542c3-169">Otwórz w programie Xcode, `Main.storyboard` i dodaj następujące składniki interfejsu użytkownika z hello obiekt bibliotece tooallow hello użytkownika toosend powiadomień wypychanych w aplikacji hello hello:</span><span class="sxs-lookup"><span data-stu-id="542c3-169">In Xcode, open `Main.storyboard` and add hello following UI components from hello object library tooallow hello user toosend push notifications in hello app:</span></span>
   
   * <span data-ttu-id="542c3-170">Etykieta bez tekstu etykiety.</span><span class="sxs-lookup"><span data-stu-id="542c3-170">A label with no label text.</span></span> <span data-ttu-id="542c3-171">Będzie ona używana tooreport błędów wysyłania powiadomień.</span><span class="sxs-lookup"><span data-stu-id="542c3-171">It will be used tooreport errors in sending notifications.</span></span> <span data-ttu-id="542c3-172">Witaj **wierszy** właściwość powinna być ustawiona zbyt**0** tak, aby automatycznie zmieni rozmiar, prawo ograniczonego toohello i prawego marginesu oraz góry hello hello widoku.</span><span class="sxs-lookup"><span data-stu-id="542c3-172">hello **Lines** property should be set too**0** so that it will automatically size constrained toohello right and left margins and hello top of hello view.</span></span>
   * <span data-ttu-id="542c3-173">Pole tekstowe **symbolu zastępczego** tekst jest ustawiany za**wprowadź komunikat powiadomienia**.</span><span class="sxs-lookup"><span data-stu-id="542c3-173">A text field with **Placeholder** text set too**Enter Notification Message**.</span></span> <span data-ttu-id="542c3-174">Ogranicz pole hello poniżej hello etykiety, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="542c3-174">Constrain hello field just below hello label as shown below.</span></span> <span data-ttu-id="542c3-175">Ustaw hello kontroler widoku jako delegat gniazda hello.</span><span class="sxs-lookup"><span data-stu-id="542c3-175">Set hello View Controller as hello outlet delegate.</span></span>
   * <span data-ttu-id="542c3-176">Przycisk zatytułowany **Wyślij powiadomienie E-mail** ograniczony bezpośrednio poniżej pola tekstowego hello i w poziomie Centrum hello.</span><span class="sxs-lookup"><span data-stu-id="542c3-176">A button titled **Send Notification** constrained just below hello text field and in hello horizontal center.</span></span>
     
     <span data-ttu-id="542c3-177">Widok Hello powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="542c3-177">hello view should look as follows:</span></span>
     
     ![Projektant programu Xcode][32]
2. <span data-ttu-id="542c3-179">[Dodaj gniazda](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) dla hello etykiety i pola tekstowego połączonych z widokiem i zaktualizuj Twojej `interface` toosupport definicji `UITextFieldDelegate` i `NSXMLParserDelegate`.</span><span class="sxs-lookup"><span data-stu-id="542c3-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for hello label and text field connected your view, and update your `interface` definition toosupport `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="542c3-180">Dodaj hello trzy deklaracje właściwości przedstawione poniżej toohelp obsługę wywoływania hello interfejsu API REST i analizowanie odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="542c3-180">Add hello three property declarations shown below toohelp support calling hello REST API and parsing hello response.</span></span>
   
    <span data-ttu-id="542c3-181">Plik ViewController.h powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="542c3-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="542c3-182">Otwórz `HubInfo.h` i Dodaj hello następujące ograniczenia, które będą używane do wysyłania powiadomień tooyour koncentratora.</span><span class="sxs-lookup"><span data-stu-id="542c3-182">Open `HubInfo.h` and add hello following constants which will be used for sending notifications tooyour hub.</span></span> <span data-ttu-id="542c3-183">Zamień na powitania symbol zastępczy literału ciągu rzeczywistymi *DefaultFullSharedAccessSignature* parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="542c3-183">Replace hello placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="542c3-184">Dodaj następujące hello `#import` tooyour instrukcje `ViewController.h` pliku.</span><span class="sxs-lookup"><span data-stu-id="542c3-184">Add hello following `#import` statements tooyour `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="542c3-185">W `ViewController.m` dodać powitania po implementacji interfejsu toohello kodu.</span><span class="sxs-lookup"><span data-stu-id="542c3-185">In `ViewController.m` add hello following code toohello interface implementation.</span></span> <span data-ttu-id="542c3-186">Ten kod będzie analizować parametry połączenia *DefaultFullSharedAccessSignature*.</span><span class="sxs-lookup"><span data-stu-id="542c3-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="542c3-187">Jak wspomniano w hello [dokumentacji interfejsu API REST](http://msdn.microsoft.com/library/azure/dn495627.aspx), te przeanalizowane informacje będą używane toogenerate token sygnatury dostępu współdzielonego dla hello **autoryzacji** nagłówek żądania.</span><span class="sxs-lookup"><span data-stu-id="542c3-187">As mentioned in hello [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used toogenerate a SaS token for hello **Authorization** request header.</span></span>
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. <span data-ttu-id="542c3-188">W `ViewController.m`, hello aktualizacji `viewDidLoad` metody tooparse hello ciągu połączenia podczas ładowania widoku hello.</span><span class="sxs-lookup"><span data-stu-id="542c3-188">In `ViewController.m`, update hello `viewDidLoad` method tooparse hello connection string when hello view loads.</span></span> <span data-ttu-id="542c3-189">Dodaj również metody narzędziowe hello, pokazano poniżej, toohello implementacji interfejsu.</span><span class="sxs-lookup"><span data-stu-id="542c3-189">Also add hello utility methods, shown below, toohello interface implementation.</span></span>  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. <span data-ttu-id="542c3-190">W `ViewController.m`, Dodaj hello następującego kodu toohello interfejsu implementacji toogenerate hello tokenu sygnatury dostępu współdzielonego autoryzacji zapewnianej w hello **autoryzacji** nagłówka, jak wspomniano w hello [interfejsu API REST Odwołanie](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="542c3-190">In `ViewController.m`, add hello following code toohello interface implementation toogenerate hello SaS authorization token that will be provided in hello **Authorization** header, as mentioned in hello [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. <span data-ttu-id="542c3-191">CTRL i przeciągnij od hello **Wyślij powiadomienie E-mail** przycisk zbyt`ViewController.m` tooadd akcji o nazwie **SendNotificationMessage** dla hello **Touch Down** zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="542c3-191">Ctrl+drag from hello **Send Notification** button too`ViewController.m` tooadd an action named **SendNotificationMessage** for hello **Touch Down** event.</span></span> <span data-ttu-id="542c3-192">Zaktualizuj metodę przy hello następujące powiadomienia hello toosend kodu za pomocą hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="542c3-192">Update method with hello following code toosend hello notification using hello REST API.</span></span>
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. <span data-ttu-id="542c3-193">W `ViewController.m`, Dodaj powitania od zamknięcia hello klawiatury dla pola tekstowego hello toosupport metody delegata.</span><span class="sxs-lookup"><span data-stu-id="542c3-193">In `ViewController.m`, add hello following delegate method toosupport closing hello keyboard for hello text field.</span></span> <span data-ttu-id="542c3-194">CTRL i przeciągnij od hello tekst pola toohello ikony kontrolera widoku w hello interfejsu tooset projektanta hello wyświetlić kontroler jako delegat gniazda hello.</span><span class="sxs-lookup"><span data-stu-id="542c3-194">Ctrl+drag from hello text field toohello View Controller icon in hello interface designer tooset hello view controller as hello outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="542c3-195">W `ViewController.m`, Dodaj następujące hello delegować metody toosupport podczas analizowania odpowiedzi hello za pomocą `NSXMLParser`.</span><span class="sxs-lookup"><span data-stu-id="542c3-195">In `ViewController.m`, add hello following delegate methods toosupport parsing hello response by using `NSXMLParser`.</span></span>
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="542c3-196">Skompiluj projekt hello i sprawdź, czy nie ma żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="542c3-196">Build hello project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="542c3-197">Jeśli wystąpi błąd kompilacji w Xcode7 dotyczące obsługi kodu bitowego, należy zmienić hello **ustawieniach kompilacji** > **włączyć Bitcode (ENABLE_BITCODE)** za**nr** w środowisku Xcode.</span><span class="sxs-lookup"><span data-stu-id="542c3-197">If you encounter a build error in Xcode7 about bitcode support, you should change hello **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** too**NO** in Xcode.</span></span> <span data-ttu-id="542c3-198">Witaj zestaw SDK usługi Notification Hubs nie obsługuje obecnie kodu bitowego.</span><span class="sxs-lookup"><span data-stu-id="542c3-198">hello Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="542c3-199">Wszystkie hello możliwe ładunki powiadomień można znaleźć w hello Apple [lokalnych i wypychanych Podręcznik programowania powiadomień].</span><span class="sxs-lookup"><span data-stu-id="542c3-199">You can find all hello possible notification payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="542c3-200">Sprawdzanie, czy aplikacja może odbierać powiadomienia wypychane</span><span class="sxs-lookup"><span data-stu-id="542c3-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="542c3-201">tootest powiadomienia wypychane w systemie iOS, należy wdrożyć urządzenie fizyczne z systemem iOS tooa aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="542c3-201">tootest push notifications on iOS, you must deploy hello app tooa physical iOS device.</span></span> <span data-ttu-id="542c3-202">Nie można wysłać powiadomień wypychanych firmy Apple przy użyciu hello symulatora systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="542c3-202">You cannot send Apple push notifications by using hello iOS Simulator.</span></span>

1. <span data-ttu-id="542c3-203">Uruchamianie aplikacji hello i sprawdź, czy rejestracja zakończy się powodzeniem, a następnie naciśnij **OK**.</span><span class="sxs-lookup"><span data-stu-id="542c3-203">Run hello app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![Test rejestracji powiadomień wypychanych aplikacji dla systemu iOS][33]
2. <span data-ttu-id="542c3-205">Testowe powiadomienie wypychane możesz wysłać z hello [Azure Portal], zgodnie z powyższym opisem.</span><span class="sxs-lookup"><span data-stu-id="542c3-205">You can send a test push notification from hello [Azure Portal], as described above.</span></span> <span data-ttu-id="542c3-206">Jeśli dodano kod umożliwiający wysyłanie powiadomień wypychanych w aplikacji hello, dotknij w tooenter pole tekstowe hello komunikatu powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="542c3-206">If you added code for sending push notifications in hello app, touch inside hello text field tooenter a notification message.</span></span> <span data-ttu-id="542c3-207">Następnie naciśnij klawisz hello **wysyłania** przycisk hello klawiatury lub hello **Wyślij powiadomienie E-mail** przycisku na powitania widoku toosend hello powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="542c3-207">Then press hello **Send** button on hello keyboard or hello **Send Notification** button in hello view toosend hello notification message.</span></span>
   
    ![Test wysyłania powiadomienia wypychanego z aplikacji dla systemu iOS][34]
3. <span data-ttu-id="542c3-209">Witaj powiadomienie wypychane zostanie wysłane tooall urządzeń, które są zarejestrowane tooreceive hello powiadomień z hello określonego Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="542c3-209">hello push notification is sent tooall devices that are registered tooreceive hello notifications from hello particular Notification Hub.</span></span>
   
    ![Test odbierania powiadomienia wypychanego z aplikacji dla systemu iOS][35]

## <a name="next-steps"></a><span data-ttu-id="542c3-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="542c3-211">Next steps</span></span>
<span data-ttu-id="542c3-212">W tym prostym przykładzie wysłano tooall powiadomień wypychanych urządzeń z systemem iOS w zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="542c3-212">In this simple example, you broadcasted push notifications tooall your registered iOS devices.</span></span> <span data-ttu-id="542c3-213">Sugerujemy jako kolejny krok zapoznanie się czy kontynuować toohello [Azure Notification Hubs Powiadom użytkowników dla systemu iOS z zaplecza programu .NET] samouczek, który przeprowadzi Cię przez proces tworzenia wypychania toosend zaplecza powiadomienia przy użyciu tagów.</span><span class="sxs-lookup"><span data-stu-id="542c3-213">We suggest as a next step in your learning that you proceed toohello [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend toosend push notifications using tags.</span></span> 

<span data-ttu-id="542c3-214">Jeśli chcesz toosegment użytkowników na grupy zainteresowań, możesz również przejść toohello [toosend użyciu usługi Notification Hubs fundamentalne wiadomości] samouczka.</span><span class="sxs-lookup"><span data-stu-id="542c3-214">If you want toosegment your users by interest groups, you can additionally move on toohello [Use Notification Hubs toosend breaking news] tutorial.</span></span> 

<span data-ttu-id="542c3-215">Ogólne informacje o usłudze Notification Hubs zawiera temat [Wskazówki dotyczące usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="542c3-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[usług Mobile Services systemu iOS SDK w wersji 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[Wskazówki dotyczące usługi Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure Notification Hubs Powiadom użytkowników dla systemu iOS z zaplecza programu .NET]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md (Powiadamianie użytkowników urządzeń z systemem iOS przy użyciu usługi Azure Notification Hubs z zapleczem programu .NET)
[toosend użyciu usługi Notification Hubs fundamentalne wiadomości]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[lokalnych i wypychanych Podręcznik programowania powiadomień]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Azure Portal]: https://portal.azure.com
