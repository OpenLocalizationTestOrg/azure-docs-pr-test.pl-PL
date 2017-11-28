<!--author=SharS last changed: 12/01/15-->

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="54c9f-101">Aby przejść do trybu konserwacji</span><span class="sxs-lookup"><span data-stu-id="54c9f-101">To enter Maintenance mode</span></span>
1. <span data-ttu-id="54c9f-102">W menu konsoli szeregowej wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.</span><span class="sxs-lookup"><span data-stu-id="54c9f-102">In the serial console menu, choose option 1, **Log in with full access**.</span></span>
2. <span data-ttu-id="54c9f-103">Wpisz hasło.</span><span class="sxs-lookup"><span data-stu-id="54c9f-103">Type the password.</span></span> <span data-ttu-id="54c9f-104">Domyślne hasło jest **Password1**.</span><span class="sxs-lookup"><span data-stu-id="54c9f-104">The default password is **Password1**.</span></span>
3. <span data-ttu-id="54c9f-105">W wierszu polecenia wpisz</span><span class="sxs-lookup"><span data-stu-id="54c9f-105">At the command prompt, type</span></span>
   
     `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="54c9f-106">Zobaczysz komunikat ostrzegawczy informujący o trybu konserwacji będzie zakłócać wszystkich żądań We/Wy i sever połączenia do klasycznego portalu Azure i zostanie wyświetlony monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="54c9f-106">You will see a warning message telling you that Maintenance mode will disrupt all I/O requests and sever the connection to the Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="54c9f-107">Typ **Y** do trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="54c9f-107">Type **Y** to enter Maintenance mode.</span></span>
   
    <span data-ttu-id="54c9f-108">Zarówno kontrolery zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="54c9f-108">Both controllers will restart.</span></span> <span data-ttu-id="54c9f-109">Po zakończeniu ponownego uruchomienia innego pojawi się komunikat wskazujący, że urządzenie jest w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="54c9f-109">When the restart is complete, another message will appear indicating that the device is in Maintenance mode.</span></span>

