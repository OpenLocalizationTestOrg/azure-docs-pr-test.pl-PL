### <a name="grant-mobile-engagement-access-to-your-gcm-api-key"></a><span data-ttu-id="3622d-101">Przyznawanie dostępu usługi Mobile Engagement do klucza interfejsu API usługi GCM</span><span class="sxs-lookup"><span data-stu-id="3622d-101">Grant Mobile Engagement access to your GCM API Key</span></span>
<span data-ttu-id="3622d-102">Aby zezwolić usłudze Mobile Engagement na wysyłanie powiadomień wypychanych w swoim imieniu, musisz przyznać jej dostęp do klucza interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3622d-102">To allow Mobile Engagement to send push notifications on your behalf, you need to grant it access to your API Key.</span></span> <span data-ttu-id="3622d-103">W tym celu należy skonfigurować i wprowadzić klucz w portalu usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="3622d-103">This is done by configuring and entering your key into the Mobile Engagement portal.</span></span>

1. <span data-ttu-id="3622d-104">W klasycznym portalu Azure upewnij się, że znajdujesz się w aplikacji używanej w tym projekcie, a następnie kliknij przycisk **Engage** (Włącz) widoczny u dołu:</span><span class="sxs-lookup"><span data-stu-id="3622d-104">From your Azure Classic Portal, ensure you're in the app we're using for this project, and then click the **Engage** button at the bottom:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="3622d-105">Następnie kliknij pozycje **Ustawienia** -> **Native Push** (Natywne powiadomienia wypychane), aby wprowadzić klucz GCM:</span><span class="sxs-lookup"><span data-stu-id="3622d-105">Then click the **Settings** -> **Native Push** section to enter your GCM Key:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="3622d-106">Kliknij ikonę **Edytuj** obok pola **Klucz interfejsu API** w sekcji ustawień usługi **GCM**, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="3622d-106">Click the **Edit** icon in front of **API Key** in the **GCM Settings** section as shown below:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="3622d-107">W oknie podręcznym wklej uzyskany wcześniej klucz serwera usługi GCM, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3622d-107">In the pop-up, paste the GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <span data-ttu-id="3622d-108"><a id="send"></a>Wysyłanie powiadomienia do aplikacji</span><span class="sxs-lookup"><span data-stu-id="3622d-108"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="3622d-109">Teraz utworzymy prostą kampanię z użyciem powiadomień wypychanych, która wyśle powiadomienie wypychane do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3622d-109">We will now create a simple push notification campaign that sends a push notification to our app.</span></span>

1. <span data-ttu-id="3622d-110">Przejdź do karty **REACH** (Zasięg) w portalu usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="3622d-110">Navigate to the **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="3622d-111">Kliknij przycisk **New Announcement** (Nowy anons), aby utworzyć kampanię z użyciem powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="3622d-111">Click **New announcement** to create your push notification campaign.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="3622d-112">Skonfiguruj pierwsze pole kampanii w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="3622d-112">Set up the first field of your campaign through the following steps:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="3622d-113">a.</span><span class="sxs-lookup"><span data-stu-id="3622d-113">a.</span></span> <span data-ttu-id="3622d-114">Nadaj nazwę kampanii.</span><span class="sxs-lookup"><span data-stu-id="3622d-114">Name your campaign.</span></span>
   
    <span data-ttu-id="3622d-115">b.</span><span class="sxs-lookup"><span data-stu-id="3622d-115">b.</span></span> <span data-ttu-id="3622d-116">Wybierz typ dostarczania w obszarze **Delivery type** (Typ dostarczania), wybierając opcje *System notification (Powiadomienie systemowe) -> Simple (Proste)*. Jest to typ prostego powiadomienia wypychanego w systemie Android, które zawiera tytuł i krótki wiersz tekstu.</span><span class="sxs-lookup"><span data-stu-id="3622d-116">Select the **Delivery type** as *System notification -> Simple*: This is the simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="3622d-117">c.</span><span class="sxs-lookup"><span data-stu-id="3622d-117">c.</span></span> <span data-ttu-id="3622d-118">W obszarze **Delivery time** (Godzina dostarczania) wybierz opcję *Any time* (W dowolnym momencie), co umożliwi aplikacji odebranie powiadomienia bez względu na to, czy jest ona uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="3622d-118">Select **Delivery time** as *Any time* to allow the app to receive a notification whether the app is started or not.</span></span>
   
    <span data-ttu-id="3622d-119">d.</span><span class="sxs-lookup"><span data-stu-id="3622d-119">d.</span></span> <span data-ttu-id="3622d-120">W tekście powiadomienia w polu **Title** (Tytuł) wpisz tytuł, który w powiadomieniu wypychanym będzie wyróżniony pogrubioną czcionką.</span><span class="sxs-lookup"><span data-stu-id="3622d-120">In the notification text type the **Title** which will be in bold in the push.</span></span>
   
    <span data-ttu-id="3622d-121">e.</span><span class="sxs-lookup"><span data-stu-id="3622d-121">e.</span></span> <span data-ttu-id="3622d-122">Następnie wpisz komunikat w polu **Message** (Komunikat).</span><span class="sxs-lookup"><span data-stu-id="3622d-122">Then type your **Message**</span></span>
4. <span data-ttu-id="3622d-123">Przewiń w dół i w sekcji **Content** (Zawartość) wybierz opcję **Notification only** (Tylko powiadomienie).</span><span class="sxs-lookup"><span data-stu-id="3622d-123">Scroll down, and in the **Content** section, select **Notification only**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="3622d-124">Na tym kończy się konfigurowanie najbardziej podstawowej kampanii.</span><span class="sxs-lookup"><span data-stu-id="3622d-124">You're done setting the most basic campaign possible.</span></span> <span data-ttu-id="3622d-125">Teraz przewiń ponownie w dół i kliknij przycisk **Create** (Utwórz), aby zapisać kampanię.</span><span class="sxs-lookup"><span data-stu-id="3622d-125">Now scroll down again and click the **Create** button to save your campaign.</span></span>
6. <span data-ttu-id="3622d-126">Ostatni krok: kliknij opcję **Activate** (Aktywuj), aby aktywować kampanię w celu wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="3622d-126">Last step: click **Activate** to activate your campaign to send push notifications.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

