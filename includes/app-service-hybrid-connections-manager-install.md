
1. <span data-ttu-id="f8498-101">W hello **połączeń hybrydowych** bloku, kliknij połączenie hybrydowe hello właśnie utworzony, a następnie kliknij przycisk **konfiguracji odbiornika**.</span><span class="sxs-lookup"><span data-stu-id="f8498-101">In hello **Hybrid connections** blade, click hello hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![Kliknij przycisk Ustawienia odbiornika](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="f8498-103">Witaj **właściwości połączenia hybrydowe** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="f8498-103">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="f8498-104">W obszarze **Menedżera połączeń hybrydowych lokalnymi**, wybierz **pobrać i skonfigurować ręcznie**, zapisać pakiet HybridConnectionManager.msi hello pobrane i skopiuj parametry połączenia bramy hello.</span><span class="sxs-lookup"><span data-stu-id="f8498-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save hello downloaded HybridConnectionManager.msi package, and copy hello gateway connection string.</span></span>
   
    ![Kliknij tutaj tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="f8498-106">Z wiersza polecenia administratora wpisz hello następujące polecenia toostart hello Instalatora:</span><span class="sxs-lookup"><span data-stu-id="f8498-106">From an administrator command prompt, type hello following command toostart hello installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="f8498-107">Po hello jest uruchamiany Instalator, kliknij przycisk **nie teraz**, a następnie wyszukaj toohello %ProgramFiles%\Microsoft\HybridConnectionManager folder, uruchom HCMConfigWizard.exe i kliknij przycisk **tak** w hello **użytkownika Kontrola konta** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f8498-107">After hello installer runs, click **Not now**, then browse toohello %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in hello **User Account Control** dialog.</span></span>
5. <span data-ttu-id="f8498-108">Wklej parametry połączenia hybrydowe hello, które wcześniej zostały skopiowane, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f8498-108">Paste hello hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![Instalowanie](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="f8498-110">Po zakończeniu instalacji powitania kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="f8498-110">When hello install completes, click **Close**.</span></span>
   
    ![Kliknij przycisk Zamknij](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="f8498-112">Na powitania **połączeń hybrydowych** bloku, hello **stan** zawiera obecnie kolumnę **połączony**.</span><span class="sxs-lookup"><span data-stu-id="f8498-112">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Stan połączenia](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

