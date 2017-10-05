---
title: "Wysyłanie powiadomień wypychanych do urządzeń z systemem iOS przy użyciu usługi Azure Notification Hubs | Microsoft Docs"
description: "Korzystając z tego samouczka, dowiesz się, jak wysyłać powiadomienia wypychane do aplikacji dla systemu iOS przy użyciu usługi Azure Notification Hubs."
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
ms.openlocfilehash: ab0777f859e80afcd61e371056b44d018c7b7ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-ios-with-azure-notification-hubs"></a><span data-ttu-id="82b56-104">Wysyłanie powiadomień wypychanych do urządzeń z systemem iOS przy użyciu usługi Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="82b56-104">Sending push notifications to iOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="82b56-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="82b56-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="82b56-106">Do wykonania kroków tego samouczka potrzebne jest aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="82b56-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="82b56-107">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="82b56-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="82b56-108">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="82b56-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="82b56-109">Korzystając z tego samouczka, dowiesz się, jak wysyłać powiadomienia wypychane do aplikacji dla systemu iOS przy użyciu usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="82b56-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span></span> <span data-ttu-id="82b56-110">Utworzysz pustą aplikację dla systemu iOS służącą do odbierania powiadomień wypychanych przy użyciu usługi [Apple Push Notification Service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span><span class="sxs-lookup"><span data-stu-id="82b56-110">You'll create a blank iOS app that receives push notifications by using the [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="82b56-111">Po zakończeniu będzie można za pomocą centrum powiadomień wysyłać powiadomienia wypychane do wszystkich urządzeń z tą aplikacją.</span><span class="sxs-lookup"><span data-stu-id="82b56-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="82b56-112">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="82b56-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="82b56-113">Kompletny kod dla tego samouczka można znaleźć [w witrynie GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="82b56-113">The completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="82b56-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="82b56-114">Prerequisites</span></span>
<span data-ttu-id="82b56-115">Dla tego samouczka wymagane są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="82b56-115">This tutorial requires the following:</span></span>

* <span data-ttu-id="82b56-116">[zestaw SDK usługi Mobile Services systemu iOS w wersji 1.2.4]</span><span class="sxs-lookup"><span data-stu-id="82b56-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="82b56-117">Najnowsza wersja środowiska [Xcode]</span><span class="sxs-lookup"><span data-stu-id="82b56-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="82b56-118">Urządzenie zgodne z systemem iOS 8 (lub nowszą wersją)</span><span class="sxs-lookup"><span data-stu-id="82b56-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="82b56-119">Członkostwo w [programie dla deweloperów firmy Apple](https://developer.apple.com/programs/)</span><span class="sxs-lookup"><span data-stu-id="82b56-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="82b56-120">Ze względu na wymagania dotyczące konfiguracji powiadomień wypychanych należy wdrożyć i przetestować powiadomienia wypychane na fizycznym urządzeniu z systemem iOS (telefonie iPhone lub tablecie iPad), a nie w symulatorze systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="82b56-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of the iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="82b56-121">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Notification Hubs dotyczących aplikacji dla systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="82b56-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="82b56-122">Konfigurowanie centrum powiadomień dla powiadomień wypychanych systemu iOS</span><span class="sxs-lookup"><span data-stu-id="82b56-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="82b56-123">W tej sekcji opisano kroki tworzenia nowego centrum powiadomień i konfigurowania uwierzytelniania w usłudze APNs przy użyciu utworzonego przez Ciebie certyfikatu powiadomień wypychanych **.p12**.</span><span class="sxs-lookup"><span data-stu-id="82b56-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span></span> <span data-ttu-id="82b56-124">Jeśli chcesz użyć już utworzonego centrum powiadomień, możesz przejść do kroku 5.</span><span class="sxs-lookup"><span data-stu-id="82b56-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="82b56-125">Kliknij przycisk <b>Usługi powiadomień</b> w bloku <b>Ustawienia</b>, a następnie wybierz pozycję <b>Apple (APNs)</b>.</span><span class="sxs-lookup"><span data-stu-id="82b56-125">Click the <b>Notification Services</b> button in the <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="82b56-126">Kliknij pozycję <b>Przekaż certyfikat</b> i wybierz wcześniej wyeksportowany plik <b>.p12</b>.</span><span class="sxs-lookup"><span data-stu-id="82b56-126">Click on <b>Upload Certificate</b> and select the <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="82b56-127">Upewnij się, że określono prawidłowe hasło.</span><span class="sxs-lookup"><span data-stu-id="82b56-127">Make sure you also specify the correct password.</span></span></p>

<p><span data-ttu-id="82b56-128">Upewnij się, że wybrano tryb <b>Piaskownica</b> na potrzeby tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="82b56-128">Make sure to select <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="82b56-129">Tryb <b>Produkcja</b> należy wybrać wyłącznie wówczas, gdy chcesz wysyłać powiadomienia wypychane do użytkowników, którzy kupili Twoją aplikację w sklepie.</span><span class="sxs-lookup"><span data-stu-id="82b56-129">Only use the <b>Production</b> if you want to send push notifications to users who purchased your app from the store.</span></span></p>
</li>
</ol>
<span data-ttu-id="82b56-130">&emsp;&emsp;&emsp;&emsp;![Konfigurowanie usługi APNS w portalu Azure](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="82b56-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![Konfigurowanie certyfikacji APNs w witrynie Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="82b56-132">Twoje centrum powiadomień jest teraz skonfigurowane do pracy z usługą APNs i uzyskano parametry połączenia służące do rejestrowania aplikacji w celu wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="82b56-132">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-to-notification-hubs"></a><span data-ttu-id="82b56-133">Łączenie aplikacji dla systemu iOS z usługą Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="82b56-133">Connect your iOS app to Notification Hubs</span></span>
1. <span data-ttu-id="82b56-134">W środowisku Xcode utwórz nowy projekt dla systemu iOS i wybierz szablon **Single View Application** (Aplikacja z jednym widokiem).</span><span class="sxs-lookup"><span data-stu-id="82b56-134">In Xcode, create a new iOS project and select the **Single View Application** template.</span></span>
   
    ![Xcode — aplikacja z jednym widokiem][8]
    
2. <span data-ttu-id="82b56-136">Podczas określania opcji dla nowego projektu upewnij się, że użyto tych samych wartości **Product Name** (Nazwa produktu) i **Organization Identifier** (Identyfikator organizacji), które zostały użyte podczas wcześniejszego ustawiania identyfikatora pakietu w portalu dla deweloperów firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="82b56-136">When setting the options for your new project, make sure to use the same **Product Name** and **Organization Identifier** that you used when you previously set the bundle ID on the Apple Developer portal.</span></span>
   
    ![Xcode — opcje projektu][11]
    
3. <span data-ttu-id="82b56-138">W obszarze **Targets** (Elementy docelowe) kliknij nazwę projektu, kliknij kartę **Build Settings** (Ustawienia kompilacji) i rozwiń węzeł **Code Signing Identity** (Tożsamość podpisywania kodu), a następnie w obszarze **Debug** (Debugowanie) ustaw tożsamość podpisywania kodu.</span><span class="sxs-lookup"><span data-stu-id="82b56-138">Under **Targets**, click your project name, click the **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="82b56-139">Zmień ustawienie opcji **Levels** (Poziomy) z **Basic** (Podstawowe) na **All** (Wszystkie) i jako **Provisioning Profile** (Profil aprowizowania) ustaw wcześniej utworzony profil aprowizowania.</span><span class="sxs-lookup"><span data-stu-id="82b56-139">Toggle **Levels** from **Basic** to **All**, and set **Provisioning Profile** to the provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="82b56-140">Jeśli nowy profil aprowizowania utworzony w programie Xcode nie jest widoczny, odśwież profile dla Twojej tożsamości podpisywania.</span><span class="sxs-lookup"><span data-stu-id="82b56-140">If you don't see the new provisioning profile that you created in Xcode, try refreshing the profiles for your signing identity.</span></span> <span data-ttu-id="82b56-141">Kliknij pozycję **Xcode** na pasku menu, kliknij pozycję **Preferences** (Preferencje), kliknij kartę **Account** (Konto), kliknij przycisk **View Details** (Pokaż szczegóły), kliknij tożsamość podpisywania, a następnie kliknij przycisk odświeżania w prawym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="82b56-141">Click **Xcode** on the menu bar, click **Preferences**, click the **Account** tab, click the **View Details** button, click your signing identity, and then click the refresh button in the bottom-right corner.</span></span>
   
    ![Xcode — profil aprowizowania][9]
4. <span data-ttu-id="82b56-143">Pobierz [zestaw SDK usługi Mobile Services systemu iOS w wersji 1.2.4] i rozpakuj plik.</span><span class="sxs-lookup"><span data-stu-id="82b56-143">Download the [Mobile Services iOS SDK version 1.2.4] and unzip the file.</span></span> <span data-ttu-id="82b56-144">W programie Xcode kliknij prawym przyciskiem myszy projekt i kliknij opcję **Add Files to** (Dodaj pliki do), aby dodać folder **WindowsAzureMessaging.framework** do projektu Xcode.</span><span class="sxs-lookup"><span data-stu-id="82b56-144">In Xcode, right-click your project and click the **Add Files to** option to add the **WindowsAzureMessaging.framework** folder to your Xcode project.</span></span> <span data-ttu-id="82b56-145">Wybierz pozycję **Copy items if needed** (Skopiuj elementy w razie potrzeby), a następnie kliknij pozycję **Add** (Dodaj).</span><span class="sxs-lookup"><span data-stu-id="82b56-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="82b56-146">Zestaw SDK usługi Notification Hubs nie obsługuje obecnie kodu bitowego w programie Xcode 7.</span><span class="sxs-lookup"><span data-stu-id="82b56-146">The notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="82b56-147">Dla ustawienia **Enable Bitcode** (Włącz kod bitowy) należy wybrać opcję **No** (Nie) w obszarze **Build Options** (Opcje kompilacji) projektu.</span><span class="sxs-lookup"><span data-stu-id="82b56-147">You must set **Enable Bitcode** to **No** in the **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Rozpakowywanie zestawu SDK platformy Azure][10]
5. <span data-ttu-id="82b56-149">Dodaj nowy plik nagłówka do projektu o nazwie `HubInfo.h`.</span><span class="sxs-lookup"><span data-stu-id="82b56-149">Add a new header file to your project named `HubInfo.h`.</span></span> <span data-ttu-id="82b56-150">Ten plik będzie zawierać stałe dla centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="82b56-150">This file will hold the constants for your notification hub.</span></span>  <span data-ttu-id="82b56-151">Dodaj następujące definicje i zastąp symbole zastępcze literału ciągu przy użyciu *nazwy centrum* i wartości *DefaultListenSharedAccessSignature* zanotowanej wcześniej.</span><span class="sxs-lookup"><span data-stu-id="82b56-151">Add the following definitions and replace the string literal placeholders with your *hub name* and the *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter the name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="82b56-152">Otwórz plik `AppDelegate.h` i dodaj następujące dyrektywy importu:</span><span class="sxs-lookup"><span data-stu-id="82b56-152">Open your `AppDelegate.h` file add the following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="82b56-153">W pliku `AppDelegate.m file` dodaj następujący kod w metodzie `didFinishLaunchingWithOptions` zależnie od wersji systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="82b56-153">In your `AppDelegate.m file`, add the following code in the `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="82b56-154">Ten kod rejestruje dojście do urządzenia w usłudze APNs:</span><span class="sxs-lookup"><span data-stu-id="82b56-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="82b56-155">Dla systemu iOS 8:</span><span class="sxs-lookup"><span data-stu-id="82b56-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="82b56-156">Dla wersji systemu iOS starszych niż 8:</span><span class="sxs-lookup"><span data-stu-id="82b56-156">For iOS versions prior to 8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="82b56-157">W tym samym pliku dodaj następujące metody.</span><span class="sxs-lookup"><span data-stu-id="82b56-157">In the same file, add the following methods.</span></span> <span data-ttu-id="82b56-158">Ten kod łączy się z centrum powiadomień przy użyciu informacji o połączeniu określonych w pliku HubInfo.h.</span><span class="sxs-lookup"><span data-stu-id="82b56-158">This code connects to the notification hub using the connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="82b56-159">Następnie przekazuje token urządzenia do centrum powiadomień, aby umożliwić wysyłanie powiadomień:</span><span class="sxs-lookup"><span data-stu-id="82b56-159">It then gives the device token to the notification hub so that the notification hub can send notifications:</span></span>
   
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
9. <span data-ttu-id="82b56-160">W tym samym pliku dodaj następującą metodę służącą do wyświetlania elementu **UIAlert** w przypadku otrzymania powiadomienia, gdy aplikacja jest aktywna:</span><span class="sxs-lookup"><span data-stu-id="82b56-160">In the same file, add the following method to display a **UIAlert** if the notification is received while the app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="82b56-161">Skompiluj i uruchom aplikację na urządzeniu, aby upewnić się, że nie występują żadne błędy.</span><span class="sxs-lookup"><span data-stu-id="82b56-161">Build and run the app on your device to verify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="82b56-162">Wysyłanie testowych powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="82b56-162">Send test push notifications</span></span>
<span data-ttu-id="82b56-163">Odbieranie powiadomień w aplikacji możesz przetestować, wysyłając powiadomienia wypychane w witrynie [Azure Portal] za pośrednictwem sekcji **Rozwiązywanie problemów** w bloku centrum (użyj opcji *Wysyłanie testowe*).</span><span class="sxs-lookup"><span data-stu-id="82b56-163">You can test receiving notifications in your app by sending push notifications in the [Azure Portal] via the **Troubleshooting** section in the hub blade (use the *Test Send* option).</span></span>

![Portal Azure — wysyłanie testowe][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-the-app"></a><span data-ttu-id="82b56-165">(Opcjonalnie) Wysyłanie powiadomień wypychanych z poziomu aplikacji</span><span class="sxs-lookup"><span data-stu-id="82b56-165">(Optional) Send push notifications from the app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="82b56-166">Ten przykład wysyłania powiadomień z aplikacji klienckiej został podany tylko dla celów szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="82b56-166">This example of sending notifications from the client app is provided for learning purposes only.</span></span> <span data-ttu-id="82b56-167">Ponieważ wymaga to obecności `DefaultFullSharedAccessSignature` w aplikacji klienckiej, naraża centrum powiadomień na ryzyko, że użytkownik może uzyskać dostęp do wysyłania nieautoryzowanych powiadomień do Twoich klientów.</span><span class="sxs-lookup"><span data-stu-id="82b56-167">Since this will require the `DefaultFullSharedAccessSignature` to be present on the client app, it exposes your notification hub to the risk that a user may gain access to send unauthorized notifications to your clients.</span></span>
> 
> 

<span data-ttu-id="82b56-168">Jeśli chcesz wysyłać powiadomienia wypychane z poziomu aplikacji, ta sekcja zawiera przykład, jak to zrobić przy użyciu interfejsu REST.</span><span class="sxs-lookup"><span data-stu-id="82b56-168">If you want to send push notifications from within an app, this section provides an example of how to do this using the REST interface.</span></span>

1. <span data-ttu-id="82b56-169">W programie Xcode otwórz plik `Main.storyboard` i dodaj następujące składniki interfejsu użytkownika z biblioteki obiektów, aby umożliwić użytkownikom wysyłanie powiadomień wypychanych w aplikacji:</span><span class="sxs-lookup"><span data-stu-id="82b56-169">In Xcode, open `Main.storyboard` and add the following UI components from the object library to allow the user to send push notifications in the app:</span></span>
   
   * <span data-ttu-id="82b56-170">Etykieta bez tekstu etykiety.</span><span class="sxs-lookup"><span data-stu-id="82b56-170">A label with no label text.</span></span> <span data-ttu-id="82b56-171">Będzie służyć do raportowania błędów wysyłania powiadomień.</span><span class="sxs-lookup"><span data-stu-id="82b56-171">It will be used to report errors in sending notifications.</span></span> <span data-ttu-id="82b56-172">Dla właściwości **Lines** (Wiersze) należy ustawić wartość **0**, aby rozmiar elementu był automatycznie ograniczony do lewego i prawego marginesu oraz góry widoku.</span><span class="sxs-lookup"><span data-stu-id="82b56-172">The **Lines** property should be set to **0** so that it will automatically size constrained to the right and left margins and the top of the view.</span></span>
   * <span data-ttu-id="82b56-173">Pole tekstowe **Placeholder** (Symbol zastępczy) z ustawionym tekstem **Enter Notification Message** (Wprowadź komunikat powiadomienia).</span><span class="sxs-lookup"><span data-stu-id="82b56-173">A text field with **Placeholder** text set to **Enter Notification Message**.</span></span> <span data-ttu-id="82b56-174">Ogranicz pole bezpośrednio pod etykietą w sposób przedstawiony poniżej.</span><span class="sxs-lookup"><span data-stu-id="82b56-174">Constrain the field just below the label as shown below.</span></span> <span data-ttu-id="82b56-175">Ustaw kontroler widoku jako delegat gniazda.</span><span class="sxs-lookup"><span data-stu-id="82b56-175">Set the View Controller as the outlet delegate.</span></span>
   * <span data-ttu-id="82b56-176">Przycisk zatytułowany **Send Notification** (Wyślij powiadomienie) ograniczony bezpośrednio poniżej pola tekstowego i wyśrodkowany w poziomie.</span><span class="sxs-lookup"><span data-stu-id="82b56-176">A button titled **Send Notification** constrained just below the text field and in the horizontal center.</span></span>
     
     <span data-ttu-id="82b56-177">Widok powinien wyglądać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="82b56-177">The view should look as follows:</span></span>
     
     ![Projektant programu Xcode][32]
2. <span data-ttu-id="82b56-179">[Dodaj gniazda](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) dla etykiety i pola tekstowego połączonych z widokiem i zaktualizuj definicję `interface` w celu obsługi elementów `UITextFieldDelegate` i `NSXMLParserDelegate`.</span><span class="sxs-lookup"><span data-stu-id="82b56-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for the label and text field connected your view, and update your `interface` definition to support `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="82b56-180">Dodaj trzy deklaracje właściwości przedstawione poniżej, aby ułatwić obsługę wywołań interfejsu API REST i analizowanie odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="82b56-180">Add the three property declarations shown below to help support calling the REST API and parsing the response.</span></span>
   
    <span data-ttu-id="82b56-181">Plik ViewController.h powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="82b56-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected to your UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="82b56-182">Otwórz plik `HubInfo.h` i dodaj następujące ograniczenia, które będą używane podczas wysyłania powiadomień do centrum.</span><span class="sxs-lookup"><span data-stu-id="82b56-182">Open `HubInfo.h` and add the following constants which will be used for sending notifications to your hub.</span></span> <span data-ttu-id="82b56-183">Zastąp symbol zastępczy literału ciągu rzeczywistymi parametrami połączenia *DefaultFullSharedAccessSignature*.</span><span class="sxs-lookup"><span data-stu-id="82b56-183">Replace the placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="82b56-184">Dodaj następujące instrukcje `#import` do pliku `ViewController.h`:</span><span class="sxs-lookup"><span data-stu-id="82b56-184">Add the following `#import` statements to your `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="82b56-185">W pliku `ViewController.m` dodaj następujący kod do implementacji interfejsu.</span><span class="sxs-lookup"><span data-stu-id="82b56-185">In `ViewController.m` add the following code to the interface implementation.</span></span> <span data-ttu-id="82b56-186">Ten kod będzie analizować parametry połączenia *DefaultFullSharedAccessSignature*.</span><span class="sxs-lookup"><span data-stu-id="82b56-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="82b56-187">Jak wspomniano w [dokumentacji interfejsu API REST](http://msdn.microsoft.com/library/azure/dn495627.aspx), te przeanalizowane informacje będą używane do generowania tokenu sygnatury dostępu współdzielonego dla nagłówka żądania **Authorization**.</span><span class="sxs-lookup"><span data-stu-id="82b56-187">As mentioned in the [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used to generate a SaS token for the **Authorization** request header.</span></span>
   
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
6. <span data-ttu-id="82b56-188">W pliku `ViewController.m` zaktualizuj metodę `viewDidLoad`, aby parametry połączenia były analizowane po załadowaniu widoku.</span><span class="sxs-lookup"><span data-stu-id="82b56-188">In `ViewController.m`, update the `viewDidLoad` method to parse the connection string when the view loads.</span></span> <span data-ttu-id="82b56-189">Dodaj również metody narzędziowe przedstawione poniżej do implementacji interfejsu.</span><span class="sxs-lookup"><span data-stu-id="82b56-189">Also add the utility methods, shown below, to the interface implementation.</span></span>  

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





1. <span data-ttu-id="82b56-190">W pliku `ViewController.m` dodaj następujący kod do implementacji interfejsu w celu wygenerowania tokenu sygnatury dostępu współdzielonego, który zostanie podany w nagłówku **Authorization**, jak opisano w [dokumentacji interfejsu API REST](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="82b56-190">In `ViewController.m`, add the following code to the interface implementation to generate the SaS authorization token that will be provided in the **Authorization** header, as mentioned in the [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
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
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
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
2. <span data-ttu-id="82b56-191">Naciśnij klawisz Ctrl i przeciągnij od przycisku **Send Notification** (Wyślij powiadomienie) do pliku `ViewController.m`, aby dodać akcję **SendNotificationMessage** dla zdarzenia **Touch Down** (Dotknięcie).</span><span class="sxs-lookup"><span data-stu-id="82b56-191">Ctrl+drag from the **Send Notification** button to `ViewController.m` to add an action named **SendNotificationMessage** for the **Touch Down** event.</span></span> <span data-ttu-id="82b56-192">Zaktualizuj metodę przy użyciu następującego kodu w celu wysyłania powiadomień przy użyciu interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="82b56-192">Update method with the following code to send the notification using the REST API.</span></span>
   
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
   
            // Apple Notification format of the notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct the message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate the token to be used in the authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create the request to add the APNs notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send the REST request
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
3. <span data-ttu-id="82b56-193">W pliku `ViewController.m` dodaj następującą metodę delegata w celu obsługi zamykania klawiatury dla pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="82b56-193">In `ViewController.m`, add the following delegate method to support closing the keyboard for the text field.</span></span> <span data-ttu-id="82b56-194">Naciśnij klawisz Ctrl i przeciągnij od pola tekstowego do ikony kontrolera widoku w projektancie interfejsu, aby ustawić kontroler widoku jako delegat gniazda.</span><span class="sxs-lookup"><span data-stu-id="82b56-194">Ctrl+drag from the text field to the View Controller icon in the interface designer to set the view controller as the outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="82b56-195">W pliku `ViewController.m` dodaj następujące metody delegata w celu obsługi analizowania odpowiedzi przy użyciu analizatora `NSXMLParser`.</span><span class="sxs-lookup"><span data-stu-id="82b56-195">In `ViewController.m`, add the following delegate methods to support parsing the response by using `NSXMLParser`.</span></span>
   
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
           // Set the status label text on the UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="82b56-196">Skompiluj projekt i upewnij się, że nie ma żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="82b56-196">Build the project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="82b56-197">W przypadku wystąpienia błędu kompilacji w programie Xcode 7 dotyczącego obsługi kodu bitowego, należy zmienić ustawienie **Build Settings** (Ustawienia kompilacji)  >  **Enable Bitcode (ENABLE_BITCODE)** (Włącz kod bitowy [ENABLE_BITCODE]) na **NO** (NIE) w programie Xcode.</span><span class="sxs-lookup"><span data-stu-id="82b56-197">If you encounter a build error in Xcode7 about bitcode support, you should change the **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** to **NO** in Xcode.</span></span> <span data-ttu-id="82b56-198">Zestaw SDK usługi Notification Hubs nie obsługuje obecnie kodu bitowego.</span><span class="sxs-lookup"><span data-stu-id="82b56-198">The Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="82b56-199">Wszystkie możliwe ładunki powiadomień można znaleźć w publikacji [Podręcznik programowania powiadomień lokalnych i wypychanych] firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="82b56-199">You can find all the possible notification payloads in the Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="82b56-200">Sprawdzanie, czy aplikacja może odbierać powiadomienia wypychane</span><span class="sxs-lookup"><span data-stu-id="82b56-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="82b56-201">Aby przetestować powiadomienia wypychane w systemie iOS, należy wdrożyć aplikację na fizycznym urządzeniu z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="82b56-201">To test push notifications on iOS, you must deploy the app to a physical iOS device.</span></span> <span data-ttu-id="82b56-202">Nie można wysłać powiadomień wypychanych firmy Apple przy użyciu symulatora systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="82b56-202">You cannot send Apple push notifications by using the iOS Simulator.</span></span>

1. <span data-ttu-id="82b56-203">Uruchom aplikację i upewnij się, że rejestracja zakończyła się powodzeniem, a następnie naciśnij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="82b56-203">Run the app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![Test rejestracji powiadomień wypychanych aplikacji dla systemu iOS][33]
2. <span data-ttu-id="82b56-205">Testowe powiadomienie wypychane możesz wysłać z poziomu witryny [Azure Portal] zgodnie z powyższym opisem.</span><span class="sxs-lookup"><span data-stu-id="82b56-205">You can send a test push notification from the [Azure Portal], as described above.</span></span> <span data-ttu-id="82b56-206">Jeśli dodano kod umożliwiający wysyłanie powiadomień wypychanych z aplikacji, dotknij w polu tekstowym, aby wprowadzić komunikat powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="82b56-206">If you added code for sending push notifications in the app, touch inside the text field to enter a notification message.</span></span> <span data-ttu-id="82b56-207">Następnie naciśnij przycisk **Send** (Wyślij) na klawiaturze lub przycisk **Send Notification** (Wyślij powiadomienie) w widoku, aby wysłać komunikat powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="82b56-207">Then press the **Send** button on the keyboard or the **Send Notification** button in the view to send the notification message.</span></span>
   
    ![Test wysyłania powiadomienia wypychanego z aplikacji dla systemu iOS][34]
3. <span data-ttu-id="82b56-209">Powiadomienie wypychane zostanie wysłane do wszystkich urządzeń zarejestrowanych do odbierania powiadomień od określonego centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="82b56-209">The push notification is sent to all devices that are registered to receive the notifications from the particular Notification Hub.</span></span>
   
    ![Test odbierania powiadomienia wypychanego z aplikacji dla systemu iOS][35]

## <a name="next-steps"></a><span data-ttu-id="82b56-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="82b56-211">Next steps</span></span>
<span data-ttu-id="82b56-212">W tym prostym przykładzie wysłano powiadomienia wypychane do wszystkich zarejestrowanych urządzeń z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="82b56-212">In this simple example, you broadcasted push notifications to all your registered iOS devices.</span></span> <span data-ttu-id="82b56-213">Jako kolejny krok sugerujemy zapoznanie się z samouczkiem [Azure Notification Hubs Notify Users for iOS with .NET backend] (Powiadamianie użytkowników urządzeń z systemem iOS przy użyciu usługi Azure Notification Hubs z zapleczem programu .NET), który zawiera instrukcje dotyczące tworzenia zaplecza służącego do wysyłania powiadomień wypychanych przy użyciu tagów.</span><span class="sxs-lookup"><span data-stu-id="82b56-213">We suggest as a next step in your learning that you proceed to the [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend to send push notifications using tags.</span></span> 

<span data-ttu-id="82b56-214">Jeśli chcesz podzielić użytkowników na grupy zainteresowań, możesz dodatkowo zapoznać się z samouczkiem [Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="82b56-214">If you want to segment your users by interest groups, you can additionally move on to the [Use Notification Hubs to send breaking news] tutorial.</span></span> 

<span data-ttu-id="82b56-215">Ogólne informacje o usłudze Notification Hubs zawiera temat [Wskazówki dotyczące usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="82b56-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

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
<span data-ttu-id="82b56-216">[zestaw SDK usługi Mobile Services systemu iOS w wersji 1.2.4]: http://aka.ms/kymw2g</span><span class="sxs-lookup"><span data-stu-id="82b56-216">[Mobile Services iOS SDK version 1.2.4]: http://aka.ms/kymw2g</span></span>
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="82b56-217">[Wskazówki dotyczące usługi Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="82b56-217">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="82b56-218">[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532</span><span class="sxs-lookup"><span data-stu-id="82b56-218">[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532</span></span>
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
<span data-ttu-id="82b56-219">[Azure Notification Hubs Notify Users for iOS with .NET backend]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md (Powiadamianie użytkowników urządzeń z systemem iOS przy użyciu usługi Azure Notification Hubs z zapleczem programu .NET)</span><span class="sxs-lookup"><span data-stu-id="82b56-219">[Azure Notification Hubs Notify Users for iOS with .NET backend]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md</span></span>
<span data-ttu-id="82b56-220">[Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs]: notification-hubs-ios-xplat-segmented-apns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="82b56-220">[Use Notification Hubs to send breaking news]: notification-hubs-ios-xplat-segmented-apns-push-notification.md</span></span>

<span data-ttu-id="82b56-221">[Podręcznik programowania powiadomień lokalnych i wypychanych]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1</span><span class="sxs-lookup"><span data-stu-id="82b56-221">[Local and Push Notification Programming Guide]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1</span></span>
<span data-ttu-id="82b56-222">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="82b56-222">[Azure Portal]: https://portal.azure.com</span></span>
