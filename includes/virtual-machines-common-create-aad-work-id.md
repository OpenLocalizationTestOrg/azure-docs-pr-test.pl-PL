
<br>

> [!NOTE]
> Jeśli nazwa użytkownika i hasło zostały podane przez administratora, jest dobrym pomysłem już pracy lub szkołą identyfikator (nazywanych także *Identyfikatora organizacyjnego*). Jeśli tak, możesz od razu rozpocząć toouse tooaccess Twojego konta Azure zasobów platformy Azure, które wymagają. Jeśli okaże się, że nie można używać tych zasobów, aby uzyskać pomoc może być konieczne tooreturn toothis artykułu. Aby uzyskać więcej informacji, zobacz [kont, które można zarejestrować się w](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) i [jak Azure subskrypcji jest powiązane tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).
> 
> 

kroki Hello są proste. Należy toolocate użytego do na tożsamości w hello klasycznego portalu Azure, odnajdowanie domenę usługi Azure Active Directory domyślne i dodać nowe tooit użytkownika jako administratora wspólnej platformy Azure.

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a>Zlokalizuj domyślny katalog w hello klasycznego portalu Azure
Uruchom po zalogowaniu się toohello [klasycznego portalu Azure](https://manage.windowsazure.com) z tożsamości konta Microsoft. Po zarejestrowaniu przewiń w dół panelu hello niebieski na powitania po lewej stronie i kliknij przycisk **usługi ACTIVE DIRECTORY**.

![Usługa Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

Zacznijmy od znajdowanie informacji o tożsamości na platformie Azure. Powinien zostać wyświetlony ekran podobny do powitania po w okienku głównym hello, ze wskazaniem, że masz jeden domyślny katalog.

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

Załóżmy Dowiedz się więcej informacji na temat go. Kliknij wiersz katalog domyślny hello, udostępnia należy do hello domyślnego katalogu właściwości.  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

tooview hello domyślna nazwa domeny, kliknij przycisk **DOMEN**.

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

W tym miejscu powinno być możliwe toosee podczas tworzenia hello konto platformy Azure, Azure Active Directory utworzony osobiste domyślnej domeny, która jest wartość skrótu (Liczba wygenerowanych z ciągu tekstowego) identyfikatora osobistego używany jako poddomeny onmicrosoft.com. To toowhich domeny hello teraz spowoduje dodanie nowego użytkownika.

## <a name="creating-a-new-user-in-hello-default-domain"></a>Tworzenie nowego użytkownika w domenie domyślnej hello
Kliknij przycisk **użytkowników** i poszukaj jednego konta osobistego. Powinny pojawić się w hello **źródło** kolumny, która jest **konta Microsoft**. Chcemy toocreate użytkownika w domyślnej. onmicrosoft.com domeny usługi Azure Active Directory.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

Zamierzamy toofollow [tych instrukcji](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) w następnych kilku krokach hello, ale należy użyć określonej przykładu.

U dołu hello hello strony, kliknij przycisk **+ Dodaj użytkownika**. Na stronie powitania wyświetlany, wpisz nową nazwę użytkownika hello i wybierz hello **typ użytkownika** **nowy użytkownik w organizacji**. W tym przykładzie jest nową nazwę użytkownika hello `ahmet`. Wybierz hello domyślnej domeny, który należy odnaleźć wcześniej jako domena hello ahmet tego adresu e-mail. Kliknij strzałkę dalej powitania po zakończeniu.

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

Dodaj więcej szczegółów dla Ahmet, ale upewnij się, że hello tooselect odpowiednie **roli** wartość. Jest łatwy toouse **administratora globalnego** toomake sure elementów pracy, ale jeśli używasz starszej roli, który jest dobrze. W tym przykładzie użyto hello **użytkownika** roli. (Dowiedz się więcej, zobacz [uprawnienia administratora przez rolę](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Nie należy włączać uwierzytelniania wieloskładnikowego, chyba że chcesz toouse uwierzytelnianie wieloskładnikowe dla każdego dziennika w operacji. Kliknij strzałkę dalej powitania po zakończeniu.

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

Kliknij przycisk hello **utworzyć** przycisk toogenerate i wyświetlić hasło tymczasowe dla Ahmet.

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

Skopiuj adres e-mail użytkownika hello, lub użyj **Wyślij E-mail na hasło**. Konieczne będzie toolog informacji hello na wkrótce.

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

Teraz powinien zostać wyświetlony nowy użytkownik hello **Ahmet hello Developer**, pochodzące z wyszukiwania z usługi Azure Active Directory. Po utworzeniu hello nowej pracy lub szkoły tożsamości z usługi Azure Active Directory. Jednak ta tożsamość jeszcze nie ma uprawnienia toouse Azure zasobów.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

Jeśli używasz **Wyślij E-mail na hasło**, hello następującego typu wiadomości e-mail są wysyłane.

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a>Dodawanie uprawnień administratora współpracującego Azure dla subskrypcji
Teraz należy tooadd hello nowego użytkownika jako współadministrator subskrypcji, hello nowy użytkownik może zalogować toohello portalu zarządzania. toodo, w panelu lewym dolnym powitania kliknij **ustawienia**.

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

Witaj głównego ustawienia i kliknij **ADMINISTRATORZY** na powitania górnej i powinien zostać wyświetlony tylko Microsoft konta tożsamości. U dołu hello hello strony, kliknij przycisk **+ Dodaj** toospecify współadministratorem. W tym miejscu wprowadź adres e-mail hello hello nowego użytkownika, którego została utworzona, w tym domeny domyślnej. Jak pokazano w następnym zrzut ekranu: hello, zielony znacznik wyboru pojawia się dalej użytkownika toohello hello domyślny katalog. Należy pamiętać, tooselect wszystkie subskrypcje hello chcieliby tooadminister stanie toobe użytkownika.

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

Gdy wszystko będzie gotowe, powinna zostać wyświetlona dwóch użytkowników, w tym nowe tożsamości współadministratorem. Wyloguj się z hello portalu.

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a>Logowanie i zmiana hello nowe hasło użytkownika
Zaloguj się jako hello nowego użytkownika, który został utworzony.

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

Natychmiast będzie toocreate zostanie wyświetlony monit o nowe hasło.

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

Użytkownik powinien, aby otrzymać sukces, która wygląda hello.

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a>Następne kroki
Teraz możesz skorzystać z nowych toouse tożsamości usługi Azure Active Directory [Szablony grupy zasobów platformy Azure](../articles/xplat-cli-azure-resource-manager.md).

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
