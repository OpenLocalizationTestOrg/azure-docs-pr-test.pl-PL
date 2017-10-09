
<br>

> [!NOTE]
> <span data-ttu-id="343bd-101">Jeśli nazwa użytkownika i hasło zostały podane przez administratora, jest dobrym pomysłem już pracy lub szkołą identyfikator (nazywanych także *Identyfikatora organizacyjnego*).</span><span class="sxs-lookup"><span data-stu-id="343bd-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="343bd-102">Jeśli tak, możesz od razu rozpocząć toouse tooaccess Twojego konta Azure zasobów platformy Azure, które wymagają.</span><span class="sxs-lookup"><span data-stu-id="343bd-102">If so, you can immediately begin toouse your Azure account tooaccess Azure resources that require one.</span></span> <span data-ttu-id="343bd-103">Jeśli okaże się, że nie można używać tych zasobów, aby uzyskać pomoc może być konieczne tooreturn toothis artykułu.</span><span class="sxs-lookup"><span data-stu-id="343bd-103">If you find that you cannot use those resources, you may need tooreturn toothis article for help.</span></span> <span data-ttu-id="343bd-104">Aby uzyskać więcej informacji, zobacz [kont, które można zarejestrować się w](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) i [jak Azure subskrypcji jest powiązane tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span><span class="sxs-lookup"><span data-stu-id="343bd-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="343bd-105">kroki Hello są proste.</span><span class="sxs-lookup"><span data-stu-id="343bd-105">hello steps are simple.</span></span> <span data-ttu-id="343bd-106">Należy toolocate użytego do na tożsamości w hello klasycznego portalu Azure, odnajdowanie domenę usługi Azure Active Directory domyślne i dodać nowe tooit użytkownika jako administratora wspólnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="343bd-106">You need toolocate your signed on identity in hello Azure classic portal, discover your default Azure Active Directory domain, and add a new user tooit as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a><span data-ttu-id="343bd-107">Zlokalizuj domyślny katalog w hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="343bd-107">Locate your default directory in hello Azure classic portal</span></span>
<span data-ttu-id="343bd-108">Uruchom po zalogowaniu się toohello [klasycznego portalu Azure](https://manage.windowsazure.com) z tożsamości konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="343bd-108">Start by logging in toohello [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="343bd-109">Po zarejestrowaniu przewiń w dół panelu hello niebieski na powitania po lewej stronie i kliknij przycisk **usługi ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="343bd-109">After you are logged in, scroll down hello blue panel on hello left side and click **ACTIVE DIRECTORY**.</span></span>

![Usługa Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="343bd-111">Zacznijmy od znajdowanie informacji o tożsamości na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="343bd-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="343bd-112">Powinien zostać wyświetlony ekran podobny do powitania po w okienku głównym hello, ze wskazaniem, że masz jeden domyślny katalog.</span><span class="sxs-lookup"><span data-stu-id="343bd-112">You should see something like hello following in hello main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="343bd-113">Załóżmy Dowiedz się więcej informacji na temat go.</span><span class="sxs-lookup"><span data-stu-id="343bd-113">Let's find out some more information about it.</span></span> <span data-ttu-id="343bd-114">Kliknij wiersz katalog domyślny hello, udostępnia należy do hello domyślnego katalogu właściwości.</span><span class="sxs-lookup"><span data-stu-id="343bd-114">Click hello default directory row, which brings you into hello default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="343bd-115">tooview hello domyślna nazwa domeny, kliknij przycisk **DOMEN**.</span><span class="sxs-lookup"><span data-stu-id="343bd-115">tooview hello default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="343bd-116">W tym miejscu powinno być możliwe toosee podczas tworzenia hello konto platformy Azure, Azure Active Directory utworzony osobiste domyślnej domeny, która jest wartość skrótu (Liczba wygenerowanych z ciągu tekstowego) identyfikatora osobistego używany jako poddomeny onmicrosoft.com. To toowhich domeny hello teraz spowoduje dodanie nowego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="343bd-116">Here you should be able toosee that when hello Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com. That's hello domain toowhich you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-hello-default-domain"></a><span data-ttu-id="343bd-117">Tworzenie nowego użytkownika w domenie domyślnej hello</span><span class="sxs-lookup"><span data-stu-id="343bd-117">Creating a new user in hello default domain</span></span>
<span data-ttu-id="343bd-118">Kliknij przycisk **użytkowników** i poszukaj jednego konta osobistego.</span><span class="sxs-lookup"><span data-stu-id="343bd-118">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="343bd-119">Powinny pojawić się w hello **źródło** kolumny, która jest **konta Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="343bd-119">You should see in hello **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="343bd-120">Chcemy toocreate użytkownika w domyślnej. onmicrosoft.com domeny usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="343bd-120">We want toocreate a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="343bd-121">Zamierzamy toofollow [tych instrukcji](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) w następnych kilku krokach hello, ale należy użyć określonej przykładu.</span><span class="sxs-lookup"><span data-stu-id="343bd-121">We're going toofollow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in hello next few steps, but use a specific example.</span></span>

<span data-ttu-id="343bd-122">U dołu hello hello strony, kliknij przycisk **+ Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="343bd-122">At hello bottom of hello page, click **+ADD USER**.</span></span> <span data-ttu-id="343bd-123">Na stronie powitania wyświetlany, wpisz nową nazwę użytkownika hello i wybierz hello **typ użytkownika** **nowy użytkownik w organizacji**.</span><span class="sxs-lookup"><span data-stu-id="343bd-123">In hello page that appears, type hello new user name, and make hello **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="343bd-124">W tym przykładzie jest nową nazwę użytkownika hello `ahmet`.</span><span class="sxs-lookup"><span data-stu-id="343bd-124">In this example, hello new user name is `ahmet`.</span></span> <span data-ttu-id="343bd-125">Wybierz hello domyślnej domeny, który należy odnaleźć wcześniej jako domena hello ahmet tego adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="343bd-125">Select hello default domain that you discovered previously as hello domain for ahmet's email address.</span></span> <span data-ttu-id="343bd-126">Kliknij strzałkę dalej powitania po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="343bd-126">Click hello next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="343bd-127">Dodaj więcej szczegółów dla Ahmet, ale upewnij się, że hello tooselect odpowiednie **roli** wartość.</span><span class="sxs-lookup"><span data-stu-id="343bd-127">Add more details for Ahmet, but make sure tooselect hello appropriate **ROLE** value.</span></span> <span data-ttu-id="343bd-128">Jest łatwy toouse **administratora globalnego** toomake sure elementów pracy, ale jeśli używasz starszej roli, który jest dobrze.</span><span class="sxs-lookup"><span data-stu-id="343bd-128">It's easy toouse **Global Admin** toomake sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="343bd-129">W tym przykładzie użyto hello **użytkownika** roli.</span><span class="sxs-lookup"><span data-stu-id="343bd-129">This example uses hello **User** role.</span></span> <span data-ttu-id="343bd-130">(Dowiedz się więcej, zobacz [uprawnienia administratora przez rolę](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Nie należy włączać uwierzytelniania wieloskładnikowego, chyba że chcesz toouse uwierzytelnianie wieloskładnikowe dla każdego dziennika w operacji.</span><span class="sxs-lookup"><span data-stu-id="343bd-130">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want toouse multifactor authentication for each log in operation.</span></span> <span data-ttu-id="343bd-131">Kliknij strzałkę dalej powitania po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="343bd-131">Click hello next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="343bd-132">Kliknij przycisk hello **utworzyć** przycisk toogenerate i wyświetlić hasło tymczasowe dla Ahmet.</span><span class="sxs-lookup"><span data-stu-id="343bd-132">Click hello **create** button toogenerate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="343bd-133">Skopiuj adres e-mail użytkownika hello, lub użyj **Wyślij E-mail na hasło**.</span><span class="sxs-lookup"><span data-stu-id="343bd-133">Copy hello user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="343bd-134">Konieczne będzie toolog informacji hello na wkrótce.</span><span class="sxs-lookup"><span data-stu-id="343bd-134">You'll need hello information toolog on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="343bd-135">Teraz powinien zostać wyświetlony nowy użytkownik hello **Ahmet hello Developer**, pochodzące z wyszukiwania z usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="343bd-135">Now you should see hello new user, **Ahmet hello Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="343bd-136">Po utworzeniu hello nowej pracy lub szkoły tożsamości z usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="343bd-136">You've created hello new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="343bd-137">Jednak ta tożsamość jeszcze nie ma uprawnienia toouse Azure zasobów.</span><span class="sxs-lookup"><span data-stu-id="343bd-137">However, this identity does not yet have permissions toouse Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="343bd-138">Jeśli używasz **Wyślij E-mail na hasło**, hello następującego typu wiadomości e-mail są wysyłane.</span><span class="sxs-lookup"><span data-stu-id="343bd-138">If you use **SEND PASSWORD IN EMAIL**, hello following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="343bd-139">Dodawanie uprawnień administratora współpracującego Azure dla subskrypcji</span><span class="sxs-lookup"><span data-stu-id="343bd-139">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="343bd-140">Teraz należy tooadd hello nowego użytkownika jako współadministrator subskrypcji, hello nowy użytkownik może zalogować toohello portalu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="343bd-140">Now you need tooadd hello new user as a co-administrator of your subscription so hello new user can sign in toohello Management Portal.</span></span> <span data-ttu-id="343bd-141">toodo, w panelu lewym dolnym powitania kliknij **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="343bd-141">toodo this, in hello lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="343bd-142">Witaj głównego ustawienia i kliknij **ADMINISTRATORZY** na powitania górnej i powinien zostać wyświetlony tylko Microsoft konta tożsamości.</span><span class="sxs-lookup"><span data-stu-id="343bd-142">In hello main settings area, click **ADMINISTRATORS** at hello top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="343bd-143">U dołu hello hello strony, kliknij przycisk **+ Dodaj** toospecify współadministratorem.</span><span class="sxs-lookup"><span data-stu-id="343bd-143">At hello bottom of hello page, click **+ADD** toospecify a co-administrator.</span></span> <span data-ttu-id="343bd-144">W tym miejscu wprowadź adres e-mail hello hello nowego użytkownika, którego została utworzona, w tym domeny domyślnej.</span><span class="sxs-lookup"><span data-stu-id="343bd-144">Here, enter hello email address of hello new user you had created, including your default domain.</span></span> <span data-ttu-id="343bd-145">Jak pokazano w następnym zrzut ekranu: hello, zielony znacznik wyboru pojawia się dalej użytkownika toohello hello domyślny katalog.</span><span class="sxs-lookup"><span data-stu-id="343bd-145">As shown in hello next screenshot, a green check mark appears next toohello user for hello default directory.</span></span> <span data-ttu-id="343bd-146">Należy pamiętać, tooselect wszystkie subskrypcje hello chcieliby tooadminister stanie toobe użytkownika.</span><span class="sxs-lookup"><span data-stu-id="343bd-146">Remember tooselect all of hello subscriptions that you would like this user toobe able tooadminister.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="343bd-147">Gdy wszystko będzie gotowe, powinna zostać wyświetlona dwóch użytkowników, w tym nowe tożsamości współadministratorem.</span><span class="sxs-lookup"><span data-stu-id="343bd-147">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="343bd-148">Wyloguj się z hello portalu.</span><span class="sxs-lookup"><span data-stu-id="343bd-148">Log out of hello portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a><span data-ttu-id="343bd-149">Logowanie i zmiana hello nowe hasło użytkownika</span><span class="sxs-lookup"><span data-stu-id="343bd-149">Logging in and changing hello new user's password</span></span>
<span data-ttu-id="343bd-150">Zaloguj się jako hello nowego użytkownika, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="343bd-150">Log in as hello new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="343bd-151">Natychmiast będzie toocreate zostanie wyświetlony monit o nowe hasło.</span><span class="sxs-lookup"><span data-stu-id="343bd-151">You will immediately be prompted toocreate a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="343bd-152">Użytkownik powinien, aby otrzymać sukces, która wygląda hello.</span><span class="sxs-lookup"><span data-stu-id="343bd-152">You should be rewarded with success that looks like hello following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="343bd-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="343bd-153">Next steps</span></span>
<span data-ttu-id="343bd-154">Teraz możesz skorzystać z nowych toouse tożsamości usługi Azure Active Directory [Szablony grupy zasobów platformy Azure](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="343bd-154">You can now use your new Azure Active Directory identity toouse [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how tooset them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@aztrainpassxxxxxoutlook.onmicrosoft.com
    Password: *********
    /info:    Added subscription Azure Pass
    info:    Setting subscription Azure Pass as default
    +
    info:    login command OK
    ralph@local:~$ azure config mode arm
    info:    New mode is arm
    ralph@local:~$ azure group list
    info:    Executing command group list
    + Listing resource groups
    info:    No matched resource groups were found
    info:    group list command OK
    ralph@local:~$ azure group create newgroup westus
    info:    Executing command group create
    + Getting resource group newgroup
    + Creating resource group newgroup
    info:    Created resource group newgroup
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/newgroup
    data:    Name:                newgroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags:
    data:
    info:    group create command OK
