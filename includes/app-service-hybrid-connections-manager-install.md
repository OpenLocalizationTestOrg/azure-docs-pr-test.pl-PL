
1. W hello **połączeń hybrydowych** bloku, kliknij połączenie hybrydowe hello właśnie utworzony, a następnie kliknij przycisk **konfiguracji odbiornika**.
   
    ![Kliknij przycisk Ustawienia odbiornika](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. Witaj **właściwości połączenia hybrydowe** zostanie otwarty blok. W obszarze **Menedżera połączeń hybrydowych lokalnymi**, wybierz **pobrać i skonfigurować ręcznie**, zapisać pakiet HybridConnectionManager.msi hello pobrane i skopiuj parametry połączenia bramy hello.
   
    ![Kliknij tutaj tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. Z wiersza polecenia administratora wpisz hello następujące polecenia toostart hello Instalatora:
   
        start HybridConnectionManager.msi
4. Po hello jest uruchamiany Instalator, kliknij przycisk **nie teraz**, a następnie wyszukaj toohello %ProgramFiles%\Microsoft\HybridConnectionManager folder, uruchom HCMConfigWizard.exe i kliknij przycisk **tak** w hello **użytkownika Kontrola konta** okna dialogowego.
5. Wklej parametry połączenia hybrydowe hello, które wcześniej zostały skopiowane, a następnie kliknij przycisk **OK**. 
   
    ![Instalowanie](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. Po zakończeniu instalacji powitania kliknij przycisk **Zamknij**.
   
    ![Kliknij przycisk Zamknij](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    Na powitania **połączeń hybrydowych** bloku, hello **stan** zawiera obecnie kolumnę **połączony**. 
   
    ![Stan połączenia](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

