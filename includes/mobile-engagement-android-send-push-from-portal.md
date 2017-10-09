### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="df700-101">Udziel Mobile Engagement tooyour dostępu do klucza interfejsu API usługi GCM</span><span class="sxs-lookup"><span data-stu-id="df700-101">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="df700-102">tooallow Mobile Engagement toosend powiadomień wypychanych w Twoim imieniu, należy mieć do niej dostęp tooyour klucz interfejsu API toogrant.</span><span class="sxs-lookup"><span data-stu-id="df700-102">tooallow Mobile Engagement toosend push notifications on your behalf, you need toogrant it access tooyour API Key.</span></span> <span data-ttu-id="df700-103">Jest to zrobić, konfigurując i wprowadzić klucz w portalu Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="df700-103">This is done by configuring and entering your key into hello Mobile Engagement portal.</span></span>

1. <span data-ttu-id="df700-104">W klasycznym portalu Azure, upewnij się, pracy w aplikacji hello możemy jest używany dla tego projektu, a następnie kliknij przycisk hello **Engage** u dołu hello:</span><span class="sxs-lookup"><span data-stu-id="df700-104">From your Azure Classic Portal, ensure you're in hello app we're using for this project, and then click hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="df700-105">Następnie kliknij przycisk hello **ustawienia** -> **natywnych powiadomień wypychanych** sekcji tooenter klucz GCM:</span><span class="sxs-lookup"><span data-stu-id="df700-105">Then click hello **Settings** -> **Native Push** section tooenter your GCM Key:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="df700-106">Kliknij przycisk hello **Edytuj** ikona przed **klucz interfejsu API** w hello **ustawienia GCM** sekcji, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="df700-106">Click hello **Edit** icon in front of **API Key** in hello **GCM Settings** section as shown below:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="df700-107">W oknie podręcznym hello wklej uzyskany wcześniej klucz serwera GCM Server hello, a następnie kliknij przycisk **Ok**.</span><span class="sxs-lookup"><span data-stu-id="df700-107">In hello pop-up, paste hello GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <span data-ttu-id="df700-108"><a id="send"></a>Wyślij aplikacji tooyour powiadomień</span><span class="sxs-lookup"><span data-stu-id="df700-108"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="df700-109">Teraz utworzymy kampanii powiadomień wypychanych proste wysyłanej aplikacji tooour powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="df700-109">We will now create a simple push notification campaign that sends a push notification tooour app.</span></span>

1. <span data-ttu-id="df700-110">Przejdź toohello **OSIĄGNĄĆ** kartę w portalu usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="df700-110">Navigate toohello **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="df700-111">Kliknij przycisk **nowy anons** toocreate kampanię powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="df700-111">Click **New announcement** toocreate your push notification campaign.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="df700-112">Skonfiguruj hello pierwsze pole kampanii hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="df700-112">Set up hello first field of your campaign through hello following steps:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="df700-113">a.</span><span class="sxs-lookup"><span data-stu-id="df700-113">a.</span></span> <span data-ttu-id="df700-114">Nadaj nazwę kampanii.</span><span class="sxs-lookup"><span data-stu-id="df700-114">Name your campaign.</span></span>
   
    <span data-ttu-id="df700-115">b.</span><span class="sxs-lookup"><span data-stu-id="df700-115">b.</span></span> <span data-ttu-id="df700-116">Wybierz hello **typ dostawy** jako *powiadomienie systemowe -> Simple*: to hello prostego systemu Android wypychania powiadomień typ, który zawiera tytuł i krótki wiersz tekstu.</span><span class="sxs-lookup"><span data-stu-id="df700-116">Select hello **Delivery type** as *System notification -> Simple*: This is hello simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="df700-117">c.</span><span class="sxs-lookup"><span data-stu-id="df700-117">c.</span></span> <span data-ttu-id="df700-118">Wybierz **czas dostawy** jako *Powi№zanych* tooallow hello tooreceive aplikacji powiadomienie, czy aplikacja hello jest uruchomiona lub nie.</span><span class="sxs-lookup"><span data-stu-id="df700-118">Select **Delivery time** as *Any time* tooallow hello app tooreceive a notification whether hello app is started or not.</span></span>
   
    <span data-ttu-id="df700-119">d.</span><span class="sxs-lookup"><span data-stu-id="df700-119">d.</span></span> <span data-ttu-id="df700-120">W hello powiadomień tekst typu hello **tytuł** której będą znajdować się w pogrubioną hello wypychania.</span><span class="sxs-lookup"><span data-stu-id="df700-120">In hello notification text type hello **Title** which will be in bold in hello push.</span></span>
   
    <span data-ttu-id="df700-121">e.</span><span class="sxs-lookup"><span data-stu-id="df700-121">e.</span></span> <span data-ttu-id="df700-122">Następnie wpisz komunikat w polu **Message** (Komunikat).</span><span class="sxs-lookup"><span data-stu-id="df700-122">Then type your **Message**</span></span>
4. <span data-ttu-id="df700-123">Przewiń w dół i w hello **zawartości** zaznacz **tylko powiadomienie**.</span><span class="sxs-lookup"><span data-stu-id="df700-123">Scroll down, and in hello **Content** section, select **Notification only**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="df700-124">Ustawienie hello najprostsze kampanii możliwe jest gotowe.</span><span class="sxs-lookup"><span data-stu-id="df700-124">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="df700-125">Teraz przewiń ponownie w dół i kliknij przycisk hello **Utwórz** przycisk toosave kampanii.</span><span class="sxs-lookup"><span data-stu-id="df700-125">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
6. <span data-ttu-id="df700-126">Ostatni krok: kliknij **Aktywuj** tooactivate toosend kampanię powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="df700-126">Last step: click **Activate** tooactivate your campaign toosend push notifications.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

