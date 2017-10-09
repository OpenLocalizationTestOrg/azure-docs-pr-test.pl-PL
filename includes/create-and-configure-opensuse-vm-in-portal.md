1. Zaloguj się toohello [klasycznego portalu Azure](http://manage.windowsazure.com).  
2. Na pasku poleceń hello u dołu okna hello powitania kliknij **nowy**.
3. W obszarze **obliczeniowe**, kliknij przycisk **maszyny wirtualnej**, a następnie kliknij przycisk **z galerii**.
   
    ![Tworzenie nowej maszyny wirtualnej][Image1]
4. W obszarze hello **SUSE** grupy, wybierz OpenSUSE obraz maszyny wirtualnej, a następnie kliknij hello toocontinue strzałki.
5. Na powitania pierwszy **konfiguracji maszyny wirtualnej** strony:
   
   * Wpisz **nazwę maszyny wirtualnej**, takie jak "testlinuxvm". Nazwa Hello musi zawierać od 3 do 15 znaków, może zawierać tylko litery, cyfry i łączniki, musi zaczynać się literą i kończyć literą lub cyfrą.
   * Sprawdź hello **warstwy** i wybierz **rozmiar**. Warstwa Hello Określa rozmiary hello, które są dostępne. można dołączyć Hello rozmiar wpływa na powitania koszt używania go, a także opcje konfiguracji, takich jak jak wiele dysków z danymi. Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
   * Wpisz **nową nazwę użytkownika**, lub zaakceptuj wartość domyślną hello **azureuser**. Ta nazwa jest dodawana toohello Sudoers listy plików.
   * Zdecyduj, którego typ **uwierzytelniania** toouse. Hasło ogólne wskazówki, zobacz [silne hasła](http://msdn.microsoft.com/library/ms161962.aspx).
6. Na powitania dalej **konfiguracji maszyny wirtualnej** strony:
   
   * Użyj domyślnej hello **Utwórz nową usługę w chmurze**.
   * W hello **nazwy DNS** wpisz unikatową toouse nazwy DNS jako część adresu hello, takie jak "testlinuxvm".
   * W hello **Region/koligacji grupy/wirtualnej sieci** wybierz region, w którym będzie hostowana ten obraz wirtualnej.
   * W obszarze **punkty końcowe**, zachować punkt końcowy SSH hello. Można dodać inne teraz, lub Dodaj, Zmień lub usuń je, po utworzeniu maszyny wirtualnej hello.
     
     > [!NOTE]
     > Jeśli chcesz, aby toouse maszyny wirtualnej sieci wirtualnej, możesz **musi** hello sieci wirtualnej można określić podczas tworzenia maszyny wirtualnej hello. Nie można dodać sieci wirtualnej tooa maszyny wirtualnej, po utworzeniu maszyny wirtualnej hello. Aby uzyskać więcej informacji, zobacz [omówienie sieci wirtualnych](../articles/virtual-network/virtual-networks-overview.md).
     > 
     > 
7. Na powitania ostatniego **konfiguracji maszyny wirtualnej** , zachować ustawienia domyślne hello a następnie kliknij przycisk hello toofinish znacznik wyboru.

Witaj portal Wyświetla hello nowej maszyny wirtualnej w obszarze **maszyn wirtualnych**. Gdy stan hello został zgłoszony jako **(Inicjowanie obsługi administracyjnej)**, maszyny wirtualnej hello jest konfigurowana. Gdy stan hello został zgłoszony jako **systemem**, można przenieść na toohello następnego kroku.

## <a name="connect-toohello-virtual-machine"></a>Połącz toohello maszyny wirtualnej
Użyjesz SSH lub PuTTY tooconnect toohello maszyny wirtualnej, w zależności od systemu operacyjnego hello na komputerze hello, którą będzie łączyć z:

* Z komputera z systemem Linux używanie protokołu SSH. Witaj wiersza polecenia wpisz:
  
    `$ ssh newuser@testlinuxvm.cloudapp.net -o ServerAliveInterval=180`
  
    Wpisz hasło użytkownika hello.
* Z komputera z systemem Windows przy użyciu programu PuTTY. Jeśli użytkownik nie jest zainstalowany, pobierz go z hello [strony pobierania programu PuTTY][PuTTYDownload].
  
    Zapisz **putty.exe** tooa katalogu na komputerze. Otwórz wiersz polecenia, przejdź do folderu toothat i uruchom **putty.exe**.
  
    Wpisz nazwę hosta hello, takie jak "testlinuxvm.cloudapp.net", a następnie wpisz "22" dla hello **portu**.
  
    ![Ekran programu puTTY][Image6]  

## <a name="update-hello-virtual-machine-optional"></a>Aktualizacja hello maszyny wirtualnej (opcjonalnie)
1. Po jesteś połączony toohello maszyny wirtualnej, można opcjonalnie zainstalować poprawki i aktualizacje systemu. Aktualizacja hello toorun, typ:
   
    `$ sudo zypper update`
2. Wybierz **oprogramowania**, następnie **aktualizacji w trybie Online** toolist dostępne aktualizacje. Wybierz **Akceptuj** toostart hello instalacji i zastosować wszystkie nowe dostępnych poprawek (z wyjątkiem hello tych opcjonalnych).
3. Po zakończeniu instalacji wybierz **Zakończ**.  System działa teraz toodate.

[PuTTYDownload]: http://www.puttyssh.org/download.html

[Image1]: ./media/create-and-configure-opensuse-vm-in-portal/CreateVM.png

[Image6]: ./media/create-and-configure-opensuse-vm-in-portal/putty.png
