
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, the following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through the new Azure portal
-->


1. <span data-ttu-id="96d95-101">Zaloguj się do [portalu Azure](https://portal.azure.com/) na http://portal.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="96d95-101">Log in to the [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="96d95-102">Na banerze po lewej stronie kliknij **PRZEGLĄDAJ wszystko**.</span><span class="sxs-lookup"><span data-stu-id="96d95-102">In the left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="96d95-103">**Przeglądaj** bloku jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="96d95-103">The **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="96d95-104">Przewiń i kliknij przycisk **serwerów SQL**.</span><span class="sxs-lookup"><span data-stu-id="96d95-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="96d95-105">**Serwerów SQL** bloku jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="96d95-105">The **SQL servers** blade is displayed.</span></span>
   
    ![Znaleźć serwera bazy danych SQL Azure w portalu][b21-FindServerInPortal]
4. <span data-ttu-id="96d95-107">Dla wygody, kliknij kontrolkę Minimalizuj we wcześniejszej **Przeglądaj** bloku.</span><span class="sxs-lookup"><span data-stu-id="96d95-107">For convenience, click the minimize control on the earlier **Browse** blade.</span></span>
5. <span data-ttu-id="96d95-108">W polu filtru zacznij wpisywać nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="96d95-108">In the filter text box, start typing the name of your server.</span></span> <span data-ttu-id="96d95-109">Twoje wiersz jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="96d95-109">Your row is displayed.</span></span>
6. <span data-ttu-id="96d95-110">Kliknij wiersz dla serwera.</span><span class="sxs-lookup"><span data-stu-id="96d95-110">Click the row for your server.</span></span> <span data-ttu-id="96d95-111">Zostanie wyświetlony blok serwera.</span><span class="sxs-lookup"><span data-stu-id="96d95-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="96d95-112">W bloku serwera, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="96d95-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="96d95-113">**Ustawienia** bloku jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="96d95-113">The **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="96d95-114">Kliknij przycisk **zapory**.</span><span class="sxs-lookup"><span data-stu-id="96d95-114">Click **Firewall**.</span></span> <span data-ttu-id="96d95-115">**Ustawienia zapory** bloku jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="96d95-115">The **Firewall Settings** blade is displayed.</span></span>
   
    ![Kliknij przycisk Ustawienia > zapory][b31-SettingsFirewallNavig]
9. <span data-ttu-id="96d95-117">Kliknij przycisk **Dodawanie klienta IP**.</span><span class="sxs-lookup"><span data-stu-id="96d95-117">Click **Add Client IP**.</span></span> <span data-ttu-id="96d95-118">W pierwszym polu tekstowym, wpisz nazwę nowej reguły.</span><span class="sxs-lookup"><span data-stu-id="96d95-118">Type in a name for your new rule into the first text box.</span></span>
10. <span data-ttu-id="96d95-119">Wpisz wartości adresu IP niski i wysoki dla zakresu, który ma zostać włączony.</span><span class="sxs-lookup"><span data-stu-id="96d95-119">Type in the low and high IP address values for the range you want to enable.</span></span>
    
    * <span data-ttu-id="96d95-120">Może być przydatny zakończeń niskiej wartości z **.0** i wysoki z **.255**.</span><span class="sxs-lookup"><span data-stu-id="96d95-120">It can be handy to have the low value end with **.0** and the high with **.255**.</span></span>
    
    ![Dodaj zakres adresów IP, aby umożliwić][b41-AddRange]
11. <span data-ttu-id="96d95-122">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="96d95-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
