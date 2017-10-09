
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. <span data-ttu-id="710c3-101">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/) na http://portal.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="710c3-101">Log in toohello [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="710c3-102">Witaj transparencie po lewej stronie, kliknij przycisk **PRZEGLĄDAJ wszystko**.</span><span class="sxs-lookup"><span data-stu-id="710c3-102">In hello left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="710c3-103">Witaj **Przeglądaj** bloku jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="710c3-103">hello **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="710c3-104">Przewiń i kliknij przycisk **serwerów SQL**.</span><span class="sxs-lookup"><span data-stu-id="710c3-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="710c3-105">Witaj **serwerów SQL** bloku jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="710c3-105">hello **SQL servers** blade is displayed.</span></span>
   
    ![Znajdź serwer bazy danych SQL Azure w portalu hello][b21-FindServerInPortal]
4. <span data-ttu-id="710c3-107">Dla wygody, kliknij przycisk hello zminimalizować formantu na powitania wcześniej **Przeglądaj** bloku.</span><span class="sxs-lookup"><span data-stu-id="710c3-107">For convenience, click hello minimize control on hello earlier **Browse** blade.</span></span>
5. <span data-ttu-id="710c3-108">W polu tekstowym hello filtru zacznij wpisywać ciąg hello nazwy serwera.</span><span class="sxs-lookup"><span data-stu-id="710c3-108">In hello filter text box, start typing hello name of your server.</span></span> <span data-ttu-id="710c3-109">Twoje wiersz jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="710c3-109">Your row is displayed.</span></span>
6. <span data-ttu-id="710c3-110">Kliknij wiersz powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="710c3-110">Click hello row for your server.</span></span> <span data-ttu-id="710c3-111">Zostanie wyświetlony blok serwera.</span><span class="sxs-lookup"><span data-stu-id="710c3-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="710c3-112">W bloku serwera, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="710c3-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="710c3-113">Witaj **ustawienia** bloku jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="710c3-113">hello **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="710c3-114">Kliknij przycisk **zapory**.</span><span class="sxs-lookup"><span data-stu-id="710c3-114">Click **Firewall**.</span></span> <span data-ttu-id="710c3-115">Witaj **ustawienia zapory** bloku jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="710c3-115">hello **Firewall Settings** blade is displayed.</span></span>
   
    ![Kliknij przycisk Ustawienia > zapory][b31-SettingsFirewallNavig]
9. <span data-ttu-id="710c3-117">Kliknij przycisk **Dodawanie klienta IP**.</span><span class="sxs-lookup"><span data-stu-id="710c3-117">Click **Add Client IP**.</span></span> <span data-ttu-id="710c3-118">Wpisz nazwę nowej reguły na powitania pierwsze pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="710c3-118">Type in a name for your new rule into hello first text box.</span></span>
10. <span data-ttu-id="710c3-119">Typ w hello niski i wysoki wartości zakresu hello ma adres IP tooenable.</span><span class="sxs-lookup"><span data-stu-id="710c3-119">Type in hello low and high IP address values for hello range you want tooenable.</span></span>
    
    * <span data-ttu-id="710c3-120">Może być przydatny toohave hello niskiej wartości kończyć się **.0** i hello wysokiej z **.255**.</span><span class="sxs-lookup"><span data-stu-id="710c3-120">It can be handy toohave hello low value end with **.0** and hello high with **.255**.</span></span>
    
    ![Dodaj tooallow zakres adresów IP][b41-AddRange]
11. <span data-ttu-id="710c3-122">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="710c3-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
