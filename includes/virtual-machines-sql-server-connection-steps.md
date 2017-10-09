### <a name="open-tcp-ports-in-hello-windows-firewall-for-hello-default-instance-of-hello-database-engine"></a>Otwartych portów TCP w Zaporze systemu Windows hello dla domyślnego wystąpienia hello hello aparatu bazy danych
1. Maszyna wirtualna toohello Uzyskuj dostęp do usług pulpitu zdalnego. Aby uzyskać szczegółowe instrukcje dotyczące łączenia toohello maszyny Wirtualnej, zobacz [Otwórz maszyny Wirtualnej SQL przy użyciu pulpitu zdalnego](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop).
2. Po zalogowaniu na ekranie startowym hello wpisz **WF.msc**, a następnie naciśnij ENTER.
   
    ![Uruchom hello zapory](./media/virtual-machines-sql-server-connection-steps/12Open-WF.png)
3. W hello **Zapora systemu Windows z zabezpieczeniami zaawansowanymi**, w lewym okienku hello, kliknij prawym przyciskiem myszy **reguły ruchu przychodzącego**, a następnie kliknij przycisk **nową regułę** w okienku akcji hello.
   
    ![Nowa reguła](./media/virtual-machines-sql-server-connection-steps/13New-FW-Rule.png)
4. W hello **Kreatora nowej reguły przychodzącej** okna dialogowego, w obszarze **typ reguły**, wybierz pozycję **portu**, a następnie kliknij przycisk **dalej**.
5. W hello **protokoły i porty** okno dialogowe, użyj domyślnej hello **TCP**. W hello **określone porty lokalne** pola, a następnie wpisz hello numer_portu hello wystąpienie hello aparatu bazy danych (**1433** hello domyślne wystąpienie lub wybrana dla hello port prywatny w kroku punktu końcowego hello).
   
    ![Port TCP 1433](./media/virtual-machines-sql-server-connection-steps/14Port-1433.png)
6. Kliknij przycisk **Dalej**.
7. W hello **akcji** okno dialogowe, wybierz opcję **przyłączenia hello**, a następnie kliknij przycisk **dalej**.
   
    **Uwaga dotycząca zabezpieczeń:** Selecting **przyłączenia hello, jeśli jest bezpieczne** można zapewnić dodatkową ochronę. Wybierz tę opcję, jeśli chcesz tooconfigure dodatkowe opcje zabezpieczeń w środowisku.
   
    ![Zezwalanie na połączenia](./media/virtual-machines-sql-server-connection-steps/15Allow-Connection.png)
8. W hello **profilu** okno dialogowe, wybierz opcję **publicznego**, **prywatnej**, i **domeny**. Następnie kliknij przycisk **Next** (Dalej).
   
    **Uwaga dotycząca zabezpieczeń:** Selecting **publicznego** umożliwia dostęp za pośrednictwem hello internet. Jeśli to możliwe, wybierz bardzie restrykcyjny profil.
   
    ![Profil publiczny](./media/virtual-machines-sql-server-connection-steps/16Public-Private-Domain-Profile.png)
9. W hello **nazwa** okno dialogowe, wpisz nazwę i opis dla tej reguły, a następnie kliknij przycisk **Zakończ**.
   
    ![Nazwa reguły](./media/virtual-machines-sql-server-connection-steps/17Rule-Name.png)

Otwórz dodatkowe porty dla innych składników w zależności od potrzeb. Aby uzyskać więcej informacji, zobacz [Konfigurowanie tooAllow zapory systemu Windows hello dostęp do programu SQL Server](http://msdn.microsoft.com/library/cc646023.aspx).

### <a name="configure-sql-server-toolisten-on-hello-tcp-protocol"></a>Skonfiguruj toolisten programu SQL Server na powitania protokołu TCP

[!INCLUDE [Enable TCP](virtual-machines-sql-server-connection-tcp-protocol.md)]

### <a name="configure-sql-server-for-mixed-mode-authentication"></a>Konfigurowanie programu SQL Server do uwierzytelniania w trybie mieszanym
Witaj aparatu bazy danych programu SQL Server nie można używać uwierzytelniania systemu Windows bez środowiska domeny. tooconnect toohello aparatu bazy danych z innego komputera, skonfigurować serwer SQL dla uwierzytelniania w trybie mieszanym. Uwierzytelnianie w trybie mieszanym umożliwia korzystanie z zarówno uwierzytelniania programu SQL Server, jak i uwierzytelniania systemu Windows.

> [!NOTE]
> Konfigurowanie uwierzytelniania w trybie mieszanym może nie być konieczne, jeśli skonfigurowano usługę Azure Virtual Network ze skonfigurowanym środowiskiem domenowym.
> 
> 

1. Podczas toohello połączonych w przypadku maszyny wirtualnej na powitania strony początkowej, wpisz **programu SQL Server Management Studio** i kliknij ikonę wybranego hello.
   
    Witaj Otwórz Management Studio, należy utworzyć środowisko Management Studio użytkowników powitania po raz pierwszy. Może to potrwać kilka chwil.
2. Przedstawia informacje o Management Studio hello **połączyć tooServer** okno dialogowe. W hello **nazwy serwera** okno, nazwa typu hello hello maszyny wirtualnej tooconnect toohello aparatu bazy danych z hello Eksplorator obiektów (zamiast hello nazwę maszyny wirtualnej można również użyć **(local)** lub jedną kropkę jako hello **nazwy serwera**). Wybierz **uwierzytelniania systemu Windows**i pozostawić  ***nazwa_maszyny_wirtualnej*\your_local_administrator** w hello **nazwy użytkownika** pole. Kliknij przycisk **Połącz**.
   
    ![Połącz tooServer](./media/virtual-machines-sql-server-connection-steps/19Connect-to-Server.png)
3. W Eksploratorze obiektów SQL Server Management Studio, kliknij prawym przyciskiem myszy nazwę hello hello wystąpienia programu SQL Server (hello nazwę maszyny wirtualnej), a następnie kliknij przycisk **właściwości**.
   
    ![Właściwości serwera](./media/virtual-machines-sql-server-connection-steps/20Server-Properties.png)
4. Na powitania **zabezpieczeń** w obszarze **uwierzytelniania serwera**, wybierz pozycję **tryb programu SQL Server i uwierzytelniania systemu Windows**, a następnie kliknij przycisk **OK** .
   
    ![Wybieranie trybu uwierzytelniania](./media/virtual-machines-sql-server-connection-steps/21Mixed-Mode.png)
5. W programie SQL Server Management Studio hello — okno dialogowe, kliknij przycisk **OK** tooacknowledge hello wymaganie toorestart programu SQL Server.
6. W Eksploratorze obiektów kliknij prawym przyciskiem myszy swój serwer, a następnie kliknij pozycję **Uruchom ponownie**. (Jeśli program SQL Server Agent jest uruchomiony, również należy go ponownie uruchomić).
   
    ![Ponowne uruchamianie](./media/virtual-machines-sql-server-connection-steps/22Restart2.png)
7. W programie SQL Server Management Studio hello — okno dialogowe, kliknij przycisk **tak** tooagree, które mają toorestart programu SQL Server.

### <a name="create-sql-server-authentication-logins"></a>Tworzenie identyfikatora logowania do uwierzytelniania w programie SQL Server
tooconnect toohello aparatu bazy danych z innego komputera, należy utworzyć co najmniej jeden identyfikator logowania uwierzytelniania programu SQL Server.

1. W Eksploratorze obiektów SQL Server Management Studio rozwiń folder hello wystąpienia serwera hello, w której ma zostać toocreate hello nowe dane logowania.
2. Powitania kliknij prawym przyciskiem myszy **zabezpieczeń** folderu, wskaż zbyt**nowy**i wybierz **logowania...** .
   
    ![Nowy identyfikator logowania](./media/virtual-machines-sql-server-connection-steps/23New-Login.png)
3. W hello **nowe dane logowania -** okno dialogowe na powitania **ogólne** strony, wprowadź nazwę hello hello nowego użytkownika w hello **nazwa logowania** pole.
4. Wybierz pozycję **Uwierzytelnianie programu SQL Server**.
5. W hello **hasło** wprowadź hasło dla nowego użytkownika hello. Wprowadź hasło ponownie w hello **Potwierdź hasło** pole.
6. Wybierz opcje wymuszania hasła hello wymagane (**wymusić zasady haseł**, **wymusić wygaśnięcie hasła**, i **użytkownik musi zmienić hasło przy następnym logowaniu**). Jeśli używasz tych danych logowania dla siebie, nie trzeba zmienić hasło przy następnym logowaniu hello toorequire.
7. Z hello **domyślna baza danych** wybierz domyślna baza danych hello logowania. **główny** hello domyślne dla tej opcji. Jeśli jeszcze nie utworzono bazy danych użytkownika, to pole pozostanie ustawiona zbyt**wzorca**.
   
    ![Właściwości identyfikatora logowania](./media/virtual-machines-sql-server-connection-steps/24Test-Login.png)
8. To hello logowania pierwszy tworzysz, może być toodesignate tę nazwę logowania administratora programu SQL Server. Jeśli tak, hello **ról serwera** strony, sprawdź **sysadmin**.
   
   > [!NOTE]
   > Członkowie stałej roli serwera sysadmin hello mają pełną kontrolę nad hello aparatu bazy danych. Należy dokładnie ograniczyć członkostwo w tej roli.
   > 
   > 
   
   ![sysadmin](./media/virtual-machines-sql-server-connection-steps/25sysadmin.png)
9. Kliknij przycisk OK.

Aby uzyskać więcej informacji na temat identyfikatorów logowania programu SQL Server, zobacz [Tworzenie identyfikatora logowania](http://msdn.microsoft.com/library/aa337562.aspx).

