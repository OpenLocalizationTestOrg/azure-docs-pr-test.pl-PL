> [!IMPORTANT]
> <span data-ttu-id="8c5cf-101">Aby odbierać powiadomienia wypychane z usługi Mobile Engagement, należy włączyć w aplikacji funkcję `Silent Remote Notifications`.</span><span class="sxs-lookup"><span data-stu-id="8c5cf-101">To receive Push Notifications from Mobile Engagement, you need to enable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="8c5cf-102">Trzeba dodać wartość remote-notification do tablicy UIBackgroundModes w pliku Info.plist.</span><span class="sxs-lookup"><span data-stu-id="8c5cf-102">You need to add the remote-notification value to the UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="8c5cf-103">Otwórz plik `info.plist` w projekcie.</span><span class="sxs-lookup"><span data-stu-id="8c5cf-103">Open `info.plist` file in the project</span></span>
2. <span data-ttu-id="8c5cf-104">Kliknij prawym przyciskiem myszy pierwszy element na liście (`Information Property List`) i dodaj nowy wiersz.</span><span class="sxs-lookup"><span data-stu-id="8c5cf-104">Right click on the top item in the list (`Information Property List`) and add a new row</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="8c5cf-105">W nowym wierszu wprowadź wartość `Required background modes`</span><span class="sxs-lookup"><span data-stu-id="8c5cf-105">In the new row enter `Required background modes`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="8c5cf-106">Kliknij strzałkę w lewo, aby rozwinąć wiersz.</span><span class="sxs-lookup"><span data-stu-id="8c5cf-106">Click on the left arrow to expand the row</span></span>
5. <span data-ttu-id="8c5cf-107">Dodaj następującą wartość do elementu 0: `App downloads content in response to push notifications`</span><span class="sxs-lookup"><span data-stu-id="8c5cf-107">Add the following value to the item 0 `App downloads content in response to push notifications`</span></span>
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="8c5cf-108">Po wprowadzeniu zmiany plik XML info.plist powinien zawierać następujący klucz i wartość:</span><span class="sxs-lookup"><span data-stu-id="8c5cf-108">Once you make the change, the info.plist XML should contain the following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="8c5cf-109">Jeśli używasz programu **Xcode 7 +** i systemu **iOS 9 +**:</span><span class="sxs-lookup"><span data-stu-id="8c5cf-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="8c5cf-110">Włącz funkcję **Push Notifications** (Powiadomienia wypychane), wybierając kolejno opcje Targets (Obiekty docelowe ) > Your Target Name (Nazwa obiektu docelowego) > Capabilities (Funkcje).</span><span class="sxs-lookup"><span data-stu-id="8c5cf-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>

