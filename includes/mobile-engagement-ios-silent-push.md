> [!IMPORTANT]
> <span data-ttu-id="c5ba8-101">tooreceive powiadomienia wypychane z usługi Mobile Engagement należy tooenable `Silent Remote Notifications` w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c5ba8-101">tooreceive Push Notifications from Mobile Engagement, you need tooenable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="c5ba8-102">Należy tablicy UIBackgroundModes toohello tooadd hello wartość remote-notification w pliku Info.plist.</span><span class="sxs-lookup"><span data-stu-id="c5ba8-102">You need tooadd hello remote-notification value toohello UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="c5ba8-103">Otwórz `info.plist` plik w projekcie hello</span><span class="sxs-lookup"><span data-stu-id="c5ba8-103">Open `info.plist` file in hello project</span></span>
2. <span data-ttu-id="c5ba8-104">Kliknij prawym przyciskiem myszy pierwszy element listy hello hello (`Information Property List`) i Dodaj nowy wiersz</span><span class="sxs-lookup"><span data-stu-id="c5ba8-104">Right click on hello top item in hello list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="c5ba8-105">W hello wprowadź nowy wiersz`Required background modes`</span><span class="sxs-lookup"><span data-stu-id="c5ba8-105">In hello new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="c5ba8-106">Polecenie hello strzałki w lewo tooexpand hello wiersza</span><span class="sxs-lookup"><span data-stu-id="c5ba8-106">Click on hello left arrow tooexpand hello row</span></span>
5. <span data-ttu-id="c5ba8-107">Dodaj hello elementem toohello wartość 0`App downloads content in response toopush notifications`</span><span class="sxs-lookup"><span data-stu-id="c5ba8-107">Add hello following value toohello item 0 `App downloads content in response toopush notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="c5ba8-108">Po wprowadzeniu zmiany hello info.plist hello XML powinien zawierać powitania po klucz i wartość:</span><span class="sxs-lookup"><span data-stu-id="c5ba8-108">Once you make hello change, hello info.plist XML should contain hello following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="c5ba8-109">Jeśli używasz programu **Xcode 7 +** i systemu **iOS 9 +**:</span><span class="sxs-lookup"><span data-stu-id="c5ba8-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="c5ba8-110">Włącz funkcję **Push Notifications** (Powiadomienia wypychane), wybierając kolejno opcje Targets (Obiekty docelowe ) > Your Target Name (Nazwa obiektu docelowego) > Capabilities (Funkcje).</span><span class="sxs-lookup"><span data-stu-id="c5ba8-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

