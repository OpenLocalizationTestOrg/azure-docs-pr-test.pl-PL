---
title: "aaaAdd uwierzytelniania w systemie iOS w usłudze Azure Mobile Apps"
description: "Dowiedz się, jak toouse Azure Mobile Apps tooauthenticate użytkowników aplikacji systemu iOS za pomocą różnych dostawców tożsamości, obejmującej AAD, Google, Facebook, Twitter i firmy Microsoft."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: ef3d3cbe-e7ca-45f9-987f-80c44209dc06
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: glenga
ms.openlocfilehash: df129e1c7517582db0e4705e0a6e98345ac8a48c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-ios-app"></a><span data-ttu-id="08981-103">Dodawanie aplikacji dla systemu iOS tooyour uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="08981-103">Add authentication tooyour iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="08981-104">W tym samouczku, możesz dodać uwierzytelniania toohello [iOS szybki start] projektu przy użyciu dostawcy tożsamości obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="08981-104">In this tutorial, you add authentication toohello [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="08981-105">W tym samouczku jest oparta na powitania [iOS szybki start] — samouczek, należy najpierw wykonać.</span><span class="sxs-lookup"><span data-stu-id="08981-105">This tutorial is based on hello [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="08981-106"><a name="register"></a>Zarejestrować aplikację do uwierzytelniania i skonfigurować hello usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="08981-106"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="08981-107"><a name="redirecturl"></a>Dodaj adresy URL przekierowania zewnętrznych dozwolone Twojej aplikacji toohello</span><span class="sxs-lookup"><span data-stu-id="08981-107"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="08981-108">Bezpieczne uwierzytelnianie wymaga Zdefiniuj nowy schemat adresu URL dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08981-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="08981-109">Po zakończeniu procesu uwierzytelniania hello dzięki temu hello uwierzytelniania systemu tooredirect wstecz tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08981-109">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span>  <span data-ttu-id="08981-110">W tym samouczku używamy schemat adresu URL _appname_ w ciągu.</span><span class="sxs-lookup"><span data-stu-id="08981-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="08981-111">Można jednak użyć dowolnego wybranego schematu URL.</span><span class="sxs-lookup"><span data-stu-id="08981-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="08981-112">Powinna być unikatowa tooyour aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="08981-112">It should be unique tooyour mobile application.</span></span>  <span data-ttu-id="08981-113">Przekierowanie hello tooenable na th po stronie serwera:</span><span class="sxs-lookup"><span data-stu-id="08981-113">tooenable hello redirection on th server side:</span></span>

1. <span data-ttu-id="08981-114">W hello [portalu Azure], wybierz usługę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08981-114">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="08981-115">Kliknij przycisk hello **uwierzytelniania / autoryzacji** opcji menu.</span><span class="sxs-lookup"><span data-stu-id="08981-115">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="08981-116">Kliknij przycisk **usługi Azure Active Directory** w obszarze hello **dostawców uwierzytelniania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="08981-116">Click **Azure Active Directory** under hello **Authentication Providers** section.</span></span>

4. <span data-ttu-id="08981-117">Zestaw hello **tryb zarządzania** za**zaawansowane**.</span><span class="sxs-lookup"><span data-stu-id="08981-117">Set hello **Management mode** too**Advanced**.</span></span>

5. <span data-ttu-id="08981-118">W hello **dozwolone zewnętrznych adresów URL przekierowań**, wprowadź `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="08981-118">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="08981-119">Witaj _appname_ ten ciąg jest hello schemat adresu URL aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="08981-119">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="08981-120">Musi on być zgodny normalne Specyfikacja adresu URL dla protokołu (Użyj litery i tylko cyfry i rozpoczyna się od litery).</span><span class="sxs-lookup"><span data-stu-id="08981-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="08981-121">Należy zanotuj ciąg hello, który możesz wybrać, ponieważ będzie potrzebny tooadjust kodu aplikacji mobilnej przy użyciu hello schemat adresu URL w kilku miejscach.</span><span class="sxs-lookup"><span data-stu-id="08981-121">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

6. <span data-ttu-id="08981-122">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="08981-122">Click **OK**.</span></span>

7. <span data-ttu-id="08981-123">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="08981-123">Click **Save**.</span></span>

## <span data-ttu-id="08981-124"><a name="permissions"></a>Ogranicz uprawnienia tooauthenticated użytkowników</span><span class="sxs-lookup"><span data-stu-id="08981-124"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="08981-125">W programie Xcode, naciśnij klawisz **Uruchom** toostart hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08981-125">In Xcode, press **Run** toostart hello app.</span></span> <span data-ttu-id="08981-126">Zgłoszony wyjątek, ponieważ aplikacja hello prób tooaccess wewnętrznej bazy danych jako nieuwierzytelniony użytkownik, ale hello *TodoItem* tabeli teraz wymaga uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="08981-126">An exception is raised because hello app attempts tooaccess the backend as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="08981-127"><a name="add-authentication"></a>Dodaj tooapp uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="08981-127"><a name="add-authentication"></a>Add authentication tooapp</span></span>
<span data-ttu-id="08981-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="08981-128">**Objective-C**:</span></span>

1. <span data-ttu-id="08981-129">Na komputerze Mac Otwórz *QSTodoListViewController.m* w środowisku Xcode i dodaj następujące metody hello:</span><span class="sxs-lookup"><span data-stu-id="08981-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add hello following method:</span></span>

    ```Objective-C
    - (void)loginAndGetData
    {
        QSAppDelegate *appDelegate = (QSAppDelegate *)[UIApplication sharedApplication].delegate;
        appDelegate.qsTodoService = self.todoService;

        [self.todoService.client loginWithProvider:@"google" urlScheme:@"appname" controller:self animated:YES completion:^(MSUser * _Nullable user, NSError * _Nullable error) {
            if (error) {
                NSLog(@"Login failed with error: %@, %@", error, [error userInfo]);
            }
            else {
                self.todoService.client.currentUser = user;
                NSLog(@"User logged in: %@", user.userId);

                [self refresh];
            }
        }];
    }
    ```

    <span data-ttu-id="08981-130">Zmień *google* za*microsoftaccount*, *twitter*, *facebook*, lub *windowsazureactivedirectory* Jeśli nie używasz Google jako dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="08981-130">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="08981-131">Jeśli korzystasz z usługi Facebook, należy najpierw [dozwolonych domen Facebook] [ 1] w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08981-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="08981-132">Zastąp hello **urlScheme** z unikatową nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08981-132">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="08981-133">Hello urlScheme powinny być hello sam jako hello protokół schemat adresu URL, który określono w hello **dozwolone zewnętrznych adresów URL przekierowań** w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="08981-133">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="08981-134">Hello urlScheme jest używany przez hello uwierzytelniania wywołania zwrotnego tooswitch wstecz tooyour aplikacji, po zakończeniu żądania uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="08981-134">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="08981-135">Zastąp `[self refresh]` w `viewDidLoad` w *QSTodoListViewController.m* z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="08981-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with hello following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="08981-136">Otwórz hello `QSAppDelegate.h` plik i dodać hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="08981-136">Open hello `QSAppDelegate.h` file and add hello following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="08981-137">Otwórz hello `QSAppDelegate.m` plik i dodać hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="08981-137">Open hello `QSAppDelegate.m` file and add hello following code:</span></span>

    ```Objective-C
    - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
    {
        if ([[url.scheme lowercaseString] isEqualToString:@"appname"]) {
            // Resume login flow
            return [self.qsTodoService.client resumeWithURL:url];
        }
        else {
            return NO;
        }
    }
    ```

   <span data-ttu-id="08981-138">Dodaj ten kod bezpośrednio przed przeczytaniem wiersza hello `#pragma mark - Core Data stack`.</span><span class="sxs-lookup"><span data-stu-id="08981-138">Add this code directly before hello line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="08981-139">Zastąp _appname_ o hello urlScheme wartość, który został użyty w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="08981-139">Replace the _appname_ wih hello urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="08981-140">Otwórz hello `AppName-Info.plist` pliku (zastępując AppName o nazwie hello aplikacji), a następnie dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="08981-140">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

    ```XML
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    <span data-ttu-id="08981-141">Ten kod powinien być umieszczony wewnątrz hello `<dict>` elementu.</span><span class="sxs-lookup"><span data-stu-id="08981-141">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="08981-142">Zastąp hello _appname_ ciągu (w tablicy dla **CFBundleURLSchemes**) o nazwie aplikacji hello wybranymi w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="08981-142">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="08981-143">Możesz również wprowadzić te zmiany w hello plist Edytor — Witaj, kliknij polecenie `AppName-Info.plist` plik w edytorze plist hello tooopen XCode.</span><span class="sxs-lookup"><span data-stu-id="08981-143">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="08981-144">Zastąp hello `com.microsoft.azure.zumo` ciągu dla **CFBundleURLName** z Twojej firmy Apple identyfikator pakietu.</span><span class="sxs-lookup"><span data-stu-id="08981-144">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="08981-145">Naciśnij klawisz *Uruchom* toostart hello aplikacji, a następnie zaloguj.</span><span class="sxs-lookup"><span data-stu-id="08981-145">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="08981-146">Gdy użytkownik jest zalogowany, należy listy Todo hello stanie tooview i aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="08981-146">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="08981-147">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="08981-147">**Swift**:</span></span>

1. <span data-ttu-id="08981-148">Na komputerze Mac Otwórz *ToDoTableViewController.swift* w środowisku Xcode i dodaj następujące metody hello:</span><span class="sxs-lookup"><span data-stu-id="08981-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add hello following method:</span></span>

    ```swift
    func loginAndGetData() {

        guard let client = self.table?.client, client.currentUser == nil else {
            return
        }

        let appDelegate = UIApplication.shared.delegate as! AppDelegate
        appDelegate.todoTableViewController = self

        let loginBlock: MSClientLoginBlock = {(user, error) -> Void in
            if (error != nil) {
                print("Error: \(error?.localizedDescription)")
            }
            else {
                client.currentUser = user
                print("User logged in: \(user?.userId)")
            }
        }

        client.login(withProvider:"google", urlScheme: "appname", controller: self, animated: true, completion: loginBlock)

    }
    ```

    <span data-ttu-id="08981-149">Zmień *google* za*microsoftaccount*, *twitter*, *facebook*, lub *windowsazureactivedirectory* Jeśli nie używasz Google jako dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="08981-149">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="08981-150">Jeśli korzystasz z usługi Facebook, należy najpierw [dozwolonych domen Facebook] [ 1] w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08981-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="08981-151">Zastąp hello **urlScheme** z unikatową nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08981-151">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="08981-152">Hello urlScheme powinny być hello sam jako hello protokół schemat adresu URL, który określono w hello **dozwolone zewnętrznych adresów URL przekierowań** w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="08981-152">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="08981-153">Hello urlScheme jest używany przez hello uwierzytelniania wywołania zwrotnego tooswitch wstecz tooyour aplikacji, po zakończeniu żądania uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="08981-153">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="08981-154">Usuń wiersze hello `self.refreshControl?.beginRefreshing()` i `self.onRefresh(self.refreshControl)` na końcu `viewDidLoad()` w *ToDoTableViewController.swift*.</span><span class="sxs-lookup"><span data-stu-id="08981-154">Remove hello lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="08981-155">Dodaj wywołanie za`loginAndGetData()` zamiast nich:</span><span class="sxs-lookup"><span data-stu-id="08981-155">Add a call too`loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="08981-156">Otwórz hello `AppDelegate.swift` plik i dodać powitania po wierszu toohello `AppDelegate` klasy:</span><span class="sxs-lookup"><span data-stu-id="08981-156">Open hello `AppDelegate.swift` file and add hello following line toohello `AppDelegate` class:</span></span>

    ```swift
    var todoTableViewController: ToDoTableViewController?

    func application(_ application: UIApplication, openURL url: NSURL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
        if url.scheme?.lowercased() == "appname" {
            return (todoTableViewController!.table?.client.resume(with: url as URL))!
        }
        else {
            return false
        }
    }
    ```

    <span data-ttu-id="08981-157">Zastąp hello _appname_ o hello urlScheme wartość, który został użyty w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="08981-157">Replace hello _appname_ wih hello urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="08981-158">Otwórz hello `AppName-Info.plist` pliku (zastępując AppName o nazwie hello aplikacji), a następnie dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="08981-158">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    <span data-ttu-id="08981-159">Ten kod powinien być umieszczony wewnątrz hello `<dict>` elementu.</span><span class="sxs-lookup"><span data-stu-id="08981-159">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="08981-160">Zastąp hello _appname_ ciągu (w tablicy dla **CFBundleURLSchemes**) o nazwie aplikacji hello wybranymi w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="08981-160">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="08981-161">Możesz również wprowadzić te zmiany w hello plist Edytor — Witaj, kliknij polecenie `AppName-Info.plist` plik w edytorze plist hello tooopen XCode.</span><span class="sxs-lookup"><span data-stu-id="08981-161">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="08981-162">Zastąp hello `com.microsoft.azure.zumo` ciągu dla **CFBundleURLName** z Twojej firmy Apple identyfikator pakietu.</span><span class="sxs-lookup"><span data-stu-id="08981-162">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="08981-163">Naciśnij klawisz *Uruchom* toostart hello aplikacji, a następnie zaloguj.</span><span class="sxs-lookup"><span data-stu-id="08981-163">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="08981-164">Gdy użytkownik jest zalogowany, należy listy Todo hello stanie tooview i aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="08981-164">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="08981-165">Usługi aplikacji — uwierzytelnianie przy użyciu jabłek komunikacji między aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="08981-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="08981-166">Aby uzyskać więcej informacji na ten temat można znaleźć toohello [dokumentacji firmy Apple][2]</span><span class="sxs-lookup"><span data-stu-id="08981-166">For more details on this subject, refer toohello [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[portalu Azure]: https://portal.azure.com

[iOS szybki start]: app-service-mobile-ios-get-started.md

