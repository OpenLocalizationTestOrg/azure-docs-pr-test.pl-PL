

## <a name="generate-hello-certificate-signing-request-file"></a><span data-ttu-id="e1560-101">Generowanie pliku żądania podpisania certyfikatu hello</span><span class="sxs-lookup"><span data-stu-id="e1560-101">Generate hello Certificate Signing Request file</span></span>
<span data-ttu-id="e1560-102">Witaj Apple Push Notification Service (APNS) używa certyfikatów tooauthenticate powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="e1560-102">hello Apple Push Notification Service (APNS) uses certificates tooauthenticate your push notifications.</span></span> <span data-ttu-id="e1560-103">Wykonaj te instrukcje toocreate hello niezbędne wypychania certyfikatu toosend i odbierane powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="e1560-103">Follow these instructions toocreate hello necessary push certificate toosend and receive notifications.</span></span> <span data-ttu-id="e1560-104">Aby uzyskać więcej informacji dotyczących tych pojęć Zobacz oficjalne hello [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="e1560-104">For more information on these concepts see hello official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="e1560-105">Generowanie pliku certyfikatu podpisywania żądania obsługi hello, który jest używany przez Apple toogenerate podpisanego certyfikatu powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="e1560-105">Generate hello Certificate Signing Request (CSR) file, which is used by Apple toogenerate a signed push certificate.</span></span>

1. <span data-ttu-id="e1560-106">Na komputerze Mac Uruchom narzędzie Keychain Access hello.</span><span class="sxs-lookup"><span data-stu-id="e1560-106">On your Mac, run hello Keychain Access tool.</span></span> <span data-ttu-id="e1560-107">Można go otworzyć z hello **narzędzia** folderu lub hello **innych** folderu na konsoli uruchamiania hello.</span><span class="sxs-lookup"><span data-stu-id="e1560-107">It can be opened from hello **Utilities** folder or hello **Other** folder on hello launch pad.</span></span>
2. <span data-ttu-id="e1560-108">Kliknij opcję **Keychain Access**, rozwiń węzeł **Asystent certyfikatu**, a następnie kliknij opcję **Żądaj certyfikatu od urzędu certyfikacji...**.</span><span class="sxs-lookup"><span data-stu-id="e1560-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="e1560-109">Wybierz użytkownika **adres E-mail użytkownika** i **nazwa pospolita** , upewnij się, że **zapisane toodisk** jest zaznaczone, a następnie kliknij przycisk **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="e1560-109">Select your **User Email Address** and **Common Name** , make sure that **Saved toodisk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="e1560-110">Pozostaw hello **adres E-mail urzędu certyfikacji** pola puste, ponieważ nie jest to wymagane.</span><span class="sxs-lookup"><span data-stu-id="e1560-110">Leave hello **CA Email Address** field blank as it is not required.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="e1560-111">Wpisz nazwę pliku certyfikatu podpisywania żądania obsługi hello w **Zapisz jako**, wybierz lokalizację hello w **gdzie**, następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="e1560-111">Type a name for hello Certificate Signing Request (CSR) file in **Save As**, select hello location in **Where**, then click **Save**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="e1560-112">To plik CSR hello jest zapisywany w lokalizacji hello wybrane. lokalizacją domyślną Hello jest hello pulpitu.</span><span class="sxs-lookup"><span data-stu-id="e1560-112">This saves hello CSR file in hello selected location; hello default location is in hello Desktop.</span></span> <span data-ttu-id="e1560-113">Należy pamiętać hello lokalizację wybraną dla tego pliku.</span><span class="sxs-lookup"><span data-stu-id="e1560-113">Remember hello location chosen for this file.</span></span>

<span data-ttu-id="e1560-114">Następnie zostanie zarejestrować aplikację w firmie Apple, Włącz powiadomienia wypychane i przekazać ten toocreate CSR wyeksportowany certyfikat powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="e1560-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR toocreate a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="e1560-115">Rejestrowanie aplikacji dla usługi powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="e1560-115">Register your app for push notifications</span></span>
<span data-ttu-id="e1560-116">toobe toosend stanie wypychania powiadomień tooan aplikacji dla systemu iOS, należy zarejestrować aplikacji z firmy Apple, a także rejestru dla powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="e1560-116">toobe able toosend push notifications tooan iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="e1560-117">Jeśli nie zarejestrowano jeszcze aplikacji, przejdź toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">systemu iOS w portalu inicjowania obsługi</a> hello Centrum deweloperów firmy Apple, logowanie za pomocą Identyfikatora firmy Apple, kliknij **identyfikatory**, następnie kliknij przycisk **identyfikatorów aplikacji** , a na koniec kliknij hello  **+**  zarejestrować tooregister nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e1560-117">If you have not already registered your app, navigate toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at hello Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on hello **+** sign tooregister a new app.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="e1560-118">Zaktualizuj następujące trzy pola dla nowej aplikacji hello, a następnie kliknij przycisk **Kontynuuj**:</span><span class="sxs-lookup"><span data-stu-id="e1560-118">Update hello following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="e1560-119">**Nazwa**: wpisz nazwę opisową aplikacji hello **nazwa** w hello **opis Identyfikatora aplikacji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="e1560-119">**Name**: Type a descriptive name for your app in hello **Name** field in hello **App ID Description** section.</span></span>
   * <span data-ttu-id="e1560-120">**Identyfikator pakietu**: w obszarze hello **jawny identyfikator aplikacji** wprowadź **identyfikator pakietu** w postaci hello `<Organization Identifier>.<Product Name>` jak wspomniano w hello [dystrybucji aplikacji Przewodnik](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span><span class="sxs-lookup"><span data-stu-id="e1560-120">**Bundle Identifier**: Under hello **Explicit App ID** section, enter a **Bundle Identifier** in hello form `<Organization Identifier>.<Product Name>` as mentioned in hello [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="e1560-121">Witaj *identyfikator organizacji* i *nazwa produktu* Użyj musi hello organizacji identyfikator i nazwa produktu, które będą używane podczas tworzenia projektu w programie XCode.</span><span class="sxs-lookup"><span data-stu-id="e1560-121">hello *Organization Identifier* and *Product Name* you use must match hello organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="e1560-122">W zrzucie się ekranu poniżej pozycja hello *NotificationHubs* służy jako identyfikator organizacji i *GetStarted* jest używana jako nazwa produktu hello.</span><span class="sxs-lookup"><span data-stu-id="e1560-122">In hello screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as hello product name.</span></span> <span data-ttu-id="e1560-123">Zagwarantowanie, że odpowiada wartości hello, który będzie używany w projekcie XCode umożliwi możesz toouse hello poprawnego profilu publikowania z XCode.</span><span class="sxs-lookup"><span data-stu-id="e1560-123">Making sure this matches hello values you will use in your XCode project will allow you toouse hello correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="e1560-124">**Powiadomienia wypychane**: hello wyboru **powiadomień wypychanych** opcję hello **usługi aplikacji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="e1560-124">**Push Notifications**: Check hello **Push Notifications** option in hello **App Services** section, .</span></span>
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="e1560-125">To wygenerowanie Identyfikatora aplikacji oraz wyświetlenie informacji hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="e1560-125">This generates your App ID and requests you tooconfirm hello information.</span></span> <span data-ttu-id="e1560-126">Kliknij przycisk **zarejestrować** tooconfirm hello nowy identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e1560-126">Click **Register** tooconfirm hello new App ID.</span></span>
     
      <span data-ttu-id="e1560-127">Po kliknięciu **zarejestrować**, zobaczysz hello **rejestracja ukończona** ekranu, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="e1560-127">Once you click **Register**, you will see hello **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="e1560-128">Kliknij przycisk **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="e1560-128">Click **Done**.</span></span>
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="e1560-129">W hello Centrum deweloperów w obszarze identyfikatory aplikacji zlokalizuj identyfikator aplikacji hello, który właśnie utworzony i kliknij jego wiersz.</span><span class="sxs-lookup"><span data-stu-id="e1560-129">In hello Developer Center, under App IDs, locate hello app ID that you just created, and click on its row.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="e1560-130">Kliknięcie Identyfikatora aplikacji hello są wyświetlane takie szczegóły aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e1560-130">Clicking on hello app ID will display hello app details.</span></span> <span data-ttu-id="e1560-131">Kliknij przycisk hello **Edytuj** u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="e1560-131">Click hello **Edit** button at hello bottom.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="e1560-132">Przewiń toohello dolnej części ekranu hello, a następnie kliknij przycisk hello **Utwórz certyfikat...**  przycisk sekcji hello **certyfikat SSL Push programowanie**.</span><span class="sxs-lookup"><span data-stu-id="e1560-132">Scroll toohello bottom of hello screen, and click hello **Create Certificate...** button under hello section **Development Push SSL Certificate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="e1560-133">Spowoduje to wyświetlenie Asystenta "Dodaj certyfikat iOS" hello.</span><span class="sxs-lookup"><span data-stu-id="e1560-133">This displays hello "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e1560-134">Instrukcje w tym samouczku obejmują użycie certyfikatu deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="e1560-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="e1560-135">Witaj, sam proces jest używane podczas rejestrowania certyfikatu produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e1560-135">hello same process is used when registering a production certificate.</span></span> <span data-ttu-id="e1560-136">Upewnij się, że używasz hello sam typ certyfikatu podczas wysyłania powiadomień.</span><span class="sxs-lookup"><span data-stu-id="e1560-136">Just make sure that you use hello same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="e1560-137">Kliknij przycisk **wybierz plik**, Przeglądaj toohello lokalizacji, w którym zapisano plik CSR hello utworzonego w pierwszym zadaniem hello, a następnie kliknij przycisk **Generuj**.</span><span class="sxs-lookup"><span data-stu-id="e1560-137">Click **Choose File**, browse toohello location where you saved hello CSR file that you created in hello first task, then click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="e1560-138">Po utworzeniu hello certyfikatu przez portal powitania kliknij hello **Pobierz** przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="e1560-138">After hello certificate is created by hello portal, click hello **Download** button, and click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="e1560-139">Pobiera certyfikat hello i zapisuje go tooyour komputera w folderze pobrane.</span><span class="sxs-lookup"><span data-stu-id="e1560-139">This downloads hello certificate and saves it tooyour computer in your Downloads folder.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="e1560-140">Domyślnie program hello pobrany plik certyfikatu deweloperskiego nosi **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="e1560-140">By default, hello downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="e1560-141">Kliknij dwukrotnie hello pobrany certyfikat powiadomień wypychanych **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="e1560-141">Double-click hello downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="e1560-142">Spowoduje to zainstalowanie nowego świadectwa hello w hello łańcucha kluczy, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="e1560-142">This installs hello new certificate in hello Keychain, as shown below:</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="e1560-143">Nazwa Hello certyfikatu może być inna, ale będzie ona poprzedzona ciągiem **Apple Development iOS Push Services:**.</span><span class="sxs-lookup"><span data-stu-id="e1560-143">hello name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="e1560-144">W narzędziu Keychain Access kliknij prawym przyciskiem myszy hello nowy certyfikat powiadomień wypychanych utworzony w hello **certyfikaty** kategorii.</span><span class="sxs-lookup"><span data-stu-id="e1560-144">In Keychain Access, right-click hello new push certificate that you created in hello **Certificates** category.</span></span> <span data-ttu-id="e1560-145">Kliknij przycisk **wyeksportować**, nazwij plik hello, wybierz hello **.p12** format, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="e1560-145">Click **Export**, name hello file, select hello **.p12** format, and then click **Save**.</span></span>
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="e1560-146">Upewnij się, zanotuj hello nazwę pliku i lokalizację hello wyeksportowanego certyfikatu .p12.</span><span class="sxs-lookup"><span data-stu-id="e1560-146">Make a note of hello file name and location of hello exported .p12 certificate.</span></span> <span data-ttu-id="e1560-147">Będzie ona używana tooenable uwierzytelniania przy użyciu usługi APNS.</span><span class="sxs-lookup"><span data-stu-id="e1560-147">It will be used tooenable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e1560-148">W tym samouczku opisano proces tworzenia pliku QuickStart.p12.</span><span class="sxs-lookup"><span data-stu-id="e1560-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="e1560-149">Nazwa i lokalizacja pliku mogą się różnić.</span><span class="sxs-lookup"><span data-stu-id="e1560-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a><span data-ttu-id="e1560-150">Utwórz profil inicjowania obsługi administracyjnej dla aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="e1560-150">Create a provisioning profile for hello app</span></span>
1. <span data-ttu-id="e1560-151">W hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">systemu iOS w portalu inicjowania obsługi</a>, wybierz pozycję **profile inicjowania obsługi**, wybierz pozycję **wszystkie**, a następnie kliknij przycisk hello  **+**  toocreate przycisk Nowy profil.</span><span class="sxs-lookup"><span data-stu-id="e1560-151">Back in hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click hello **+** button toocreate a new profile.</span></span> <span data-ttu-id="e1560-152">Spowoduje to uruchomienie hello **Dodaj profil inicjowania obsługi systemu iOS** Kreatora</span><span class="sxs-lookup"><span data-stu-id="e1560-152">This launches hello **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="e1560-153">Wybierz **tworzenie aplikacji dla systemu iOS** w obszarze **programowanie** jako typ profilu inicjowania obsługi hello, a następnie kliknij przycisk **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="e1560-153">Select **iOS App Development** under **Development** as hello provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="e1560-154">Następnie wybierz nowo utworzony hello identyfikator aplikacji hello **identyfikator aplikacji** listy rozwijanej, a następnie kliknij przycisk **Kontynuuj**</span><span class="sxs-lookup"><span data-stu-id="e1560-154">Next, select hello app ID you just created from hello **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="e1560-155">W hello **wybierz certyfikaty** ekranu, wybierz certyfikat programowania zwykle używany do podpisywania kodu, a następnie kliknij przycisk **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="e1560-155">In hello **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="e1560-156">To nie jest hello wypychania certyfikat, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="e1560-156">This is not hello push certificate you just created.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="e1560-157">Następnie wybierz pozycję hello **urządzeń** toouse testowania, a następnie kliknij przycisk **Kontynuuj**</span><span class="sxs-lookup"><span data-stu-id="e1560-157">Next, select hello **Devices** toouse for testing, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="e1560-158">Na koniec wybierz nazwę dla profilu hello w **nazwa profilu**, kliknij przycisk **Generuj**.</span><span class="sxs-lookup"><span data-stu-id="e1560-158">Finally, pick a name for hello profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="e1560-159">Po utworzeniu nowego profilu inicjowania obsługi administracyjnej hello kliknij toodownload ją i zainstaluj go na komputerze deweloperskim Xcode.</span><span class="sxs-lookup"><span data-stu-id="e1560-159">When hello new provisioning profile is created click toodownload it and install it on your Xcode development machine.</span></span> <span data-ttu-id="e1560-160">Następnie kliknij przycisk **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="e1560-160">Then click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
