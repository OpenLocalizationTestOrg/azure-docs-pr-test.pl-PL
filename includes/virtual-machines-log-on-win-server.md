1. Kliknięcie opcji **Połącz** powoduje utworzenie i pobranie pliku Remote Desktop Protocol (rdp). Kliknij przycisk **Otwórz** toouse tego pliku.
2. Zostanie wyświetlone ostrzeżenie, że hello plik RDP pochodzi od nieznanego wydawcy. Jest to normalne. W oknie pulpitu zdalnego powitania kliknij **Connect** toocontinue.
   
    ![Zrzut ekranu przedstawiający ostrzeżenie o nieznanym wydawcy.](./media/virtual-machines-log-on-win-server/rdp-warn.png)
3. W hello **zabezpieczenia systemu Windows** okna, wpisz hello poświadczeń dla konta na powitania maszyny wirtualnej, a następnie kliknij przycisk **OK**.
   
     **Konto lokalne** — zazwyczaj jest to konto lokalne powitania nazwę użytkownika i hasło określone podczas tworzenia hello maszyny wirtualnej. W takim przypadku hello domeny jest nazwa hello hello maszyny wirtualnej i jest wprowadzana jako *vmname*&#92; *Nazwa użytkownika*.  
   
    **Maszyna wirtualna przyłączona do domeny** — Jeśli hello maszyny Wirtualnej należy tooa domeny, wprowadź nazwę użytkownika hello w formacie hello *domeny*&#92; *Nazwa użytkownika*. Witaj, konto musi również tooeither w hello Administratorzy grupy lub przyznano toohello uprawnienia dostępu zdalnego do maszyny Wirtualnej.
   
    **Kontroler domeny** — Jeśli hello maszyny Wirtualnej jest kontroler domeny, wpisz hello nazwę użytkownika i hasło konta administratora domeny dla tej domeny.
4. Kliknij przycisk **tak** tooverify hello tożsamości hello maszyny wirtualnej i zakończyć logowanie.
   
   ![Zrzut ekranu przedstawiający komunikat dotyczący, potwierdzenia tożsamości hello hello maszyny Wirtualnej.](./media/virtual-machines-log-on-win-server/cert-warning.png)

