### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a><span data-ttu-id="cebb7-101">Udziel dostępu tooyour tooMobile certyfikatu wypychania zaangażowania</span><span class="sxs-lookup"><span data-stu-id="cebb7-101">Grant access tooyour Push Certificate tooMobile Engagement</span></span>
<span data-ttu-id="cebb7-102">tooallow Mobile Engagement toosend powiadomień wypychanych w Twoim imieniu, należy uzyskać dostępu do certyfikatu tooyour toogrant.</span><span class="sxs-lookup"><span data-stu-id="cebb7-102">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour certificate.</span></span> <span data-ttu-id="cebb7-103">Jest to zrobić, konfigurując i wprowadzić certyfikat w portalu Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="cebb7-103">This is done by configuring and entering your certificate into hello Mobile Engagement portal.</span></span> <span data-ttu-id="cebb7-104">Upewnij się, że dysponujesz certyfikatem p12, zgodnie z objaśnieniem w [dokumentacji firmy Apple](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6).</span><span class="sxs-lookup"><span data-stu-id="cebb7-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="cebb7-105">Przejdź tooyour portalu Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="cebb7-105">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="cebb7-106">Upewnij się, zalogowanie hello poprawne, a następnie kliknij polecenie hello **Engage** u dołu hello:</span><span class="sxs-lookup"><span data-stu-id="cebb7-106">Ensure you're in hello correct and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="cebb7-107">Polecenie hello **ustawienia** strony w portalu usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="cebb7-107">Click on hello **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="cebb7-108">Kliknij hello **natywnych powiadomień wypychanych** sekcji tooupload certyfikat p12:</span><span class="sxs-lookup"><span data-stu-id="cebb7-108">From there click on hello **Native Push** section tooupload your p12 certificate:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="cebb7-109">Wybierz certyfikat p12, prześlij go i wpisz hasło:</span><span class="sxs-lookup"><span data-stu-id="cebb7-109">Select your p12, upload it and type your password:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <span data-ttu-id="cebb7-110"><a id="send"></a>Wyślij aplikacji tooyour powiadomień</span><span class="sxs-lookup"><span data-stu-id="cebb7-110"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="cebb7-111">Teraz utworzymy prostą kampanię powiadomień wypychanych, która będzie wysyłać aplikacji tooour wypychania:</span><span class="sxs-lookup"><span data-stu-id="cebb7-111">We will now create a simple Push Notification campaign that will send a push tooour app:</span></span>

1. <span data-ttu-id="cebb7-112">Przejdź toohello **osiągnąć** kartę w portalu usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="cebb7-112">Navigate toohello **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="cebb7-113">Kliknij przycisk **nowy anons** toocreate kampanii wypychania</span><span class="sxs-lookup"><span data-stu-id="cebb7-113">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="cebb7-114">Konfiguracja hello pierwsze pola kampanii:</span><span class="sxs-lookup"><span data-stu-id="cebb7-114">Setup hello first fields of your campaign:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="cebb7-115">Podaj nazwę kampanii w polu **Name** (Nazwa).</span><span class="sxs-lookup"><span data-stu-id="cebb7-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="cebb7-116">Wybierz hello **czas dostawy** jako **tylko poza aplikacją**: jest to hello Apple push powiadomień typu prostego, który zawiera krótki tekst.</span><span class="sxs-lookup"><span data-stu-id="cebb7-116">Select hello **Delivery time** as **Out of app only**: this is hello simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="cebb7-117">W tekście powiadomienia hello, wpisz pierwszy hello **tytuł** który będzie stanowić pierwszy wiersz hello hello wypychania.</span><span class="sxs-lookup"><span data-stu-id="cebb7-117">In hello notification text, type first hello **Title** which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="cebb7-118">Następnie wpisz Twojej **komunikat** który będzie stanowić drugi wiersz hello</span><span class="sxs-lookup"><span data-stu-id="cebb7-118">Then type your **Message** which will be hello second line</span></span>
4. <span data-ttu-id="cebb7-119">Przewiń w dół i w hello sekcji zawartości wybierz **tylko powiadomienie**</span><span class="sxs-lookup"><span data-stu-id="cebb7-119">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="cebb7-120">Wszystko gotowe ustawienie hello najbardziej podstawowej kampanii.</span><span class="sxs-lookup"><span data-stu-id="cebb7-120">You're done setting hello most basic campaign.</span></span> <span data-ttu-id="cebb7-121">Teraz przewiń w dół i wybierz polecenie **Utwórz** przycisk toosave kampanię powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="cebb7-121">Now scroll down and click on **Create** button toosave your push notification campaign.</span></span> 
6. <span data-ttu-id="cebb7-122">Na koniec — kliknij pozycję **Aktywuj** toosend powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="cebb7-122">Finally - click on **Activate** toosend push notification.</span></span> 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="cebb7-123">Można otrzymywać powiadomienia hello na urządzeniu z systemem iOS w Centrum powiadomień hello podobnie następującej hello:</span><span class="sxs-lookup"><span data-stu-id="cebb7-123">You will be able receive hello notification on your iOS device in hello notification center like hello following:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="cebb7-124">Jeśli masz Apple Watch łączyć się z tego urządzenia z systemem iOS zostanie wyświetlony hello powiadomienie na Twoje Apple Watch:</span><span class="sxs-lookup"><span data-stu-id="cebb7-124">If you have an Apple Watch paired with this iOS device then you will see hello notification on your Apple Watch:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

