
1. <span data-ttu-id="dc387-101">Przejdź toohello [Google Cloud Console](https://console.developers.google.com/project), zaloguj się przy użyciu poświadczeń konta Google.</span><span class="sxs-lookup"><span data-stu-id="dc387-101">Navigate toohello [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span></span> 
2. <span data-ttu-id="dc387-102">Kliknij opcję **Create Project** (Utwórz projekt), wpisz nazwę projektu, a następnie kliknij przycisk **Create** (Utwórz).</span><span class="sxs-lookup"><span data-stu-id="dc387-102">Click **Create Project**, type a project name, then click **Create**.</span></span> <span data-ttu-id="dc387-103">Jeśli jest to wymagane, wykonać hello weryfikację SMS i kliknij przycisk **Utwórz** ponownie.</span><span class="sxs-lookup"><span data-stu-id="dc387-103">If requested, carry out hello SMS Verification, and click **Create** again.</span></span>
   
    ![Tworzenie nowego projektu](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     <span data-ttu-id="dc387-105">Wpisz nową nazwę w polu **Project name** (Nazwa projektu) i kliknij pozycję **Create project** (Utwórz projekt).</span><span class="sxs-lookup"><span data-stu-id="dc387-105">Type in your new **Project name** and click **Create project**.</span></span>
3. <span data-ttu-id="dc387-106">Kliknij przycisk hello **narzędzia i inne** przycisk, a następnie kliknij przycisk **informacji o projekcie**.</span><span class="sxs-lookup"><span data-stu-id="dc387-106">Click hello **Utilities and More** button and then click **Project Information**.</span></span> <span data-ttu-id="dc387-107">Zanotuj hello **numer projektu**.</span><span class="sxs-lookup"><span data-stu-id="dc387-107">Make a note of hello **Project Number**.</span></span> <span data-ttu-id="dc387-108">Konieczne będzie tooset tej wartości jako hello `SenderId` zmiennej w powitania klienta aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dc387-108">You will need tooset this value as hello `SenderId` variable in hello client app.</span></span>
   
    ![Narzędzia i nie tylko](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. <span data-ttu-id="dc387-110">W hello projektu pulpitu nawigacyjnego, w obszarze **mobilnych interfejsów API**, kliknij przycisk **Google Cloud Messaging**, następnie na następnej stronie powitania kliknij **Włącz interfejs API** i zaakceptuj postanowienia hello usługi.</span><span class="sxs-lookup"><span data-stu-id="dc387-110">In hello project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on hello next page click **Enable API** and accept hello terms of service.</span></span> 
   
    ![Włączanie usługi GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Włączanie usługi GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. <span data-ttu-id="dc387-113">Na pulpicie nawigacyjnym projektu hello, kliknij przycisk **poświadczenia** > **poświadczenie tworzenia** > **klucz interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="dc387-113">In hello project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span></span> 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. <span data-ttu-id="dc387-114">W obszarze **Create a new key** (Utwórz nowy klucz) kliknij opcję **Server key** (Klucz serwera), wpisz nazwę klucza, a następnie kliknij przycisk **Create** (Utwórz).</span><span class="sxs-lookup"><span data-stu-id="dc387-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span></span>
7. <span data-ttu-id="dc387-115">Zanotuj hello **klucz interfejsu API** wartość.</span><span class="sxs-lookup"><span data-stu-id="dc387-115">Make a note of hello **API KEY** value.</span></span>
   
    <span data-ttu-id="dc387-116">Spowoduje to tooenable wartość klucza interfejsu API Azure tooauthenticate za pomocą usługi GCM i wysyłania powiadomień wypychanych w imieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dc387-116">You will use this API key value tooenable Azure tooauthenticate with GCM and send push notifications on behalf of your app.</span></span>

