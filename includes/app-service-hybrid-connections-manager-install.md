
1. <span data-ttu-id="cc73e-101">W **połączeń hybrydowych** bloku, kliknij połączenie hybrydowe właśnie utworzony, kliknięcie **konfiguracji odbiornika**.</span><span class="sxs-lookup"><span data-stu-id="cc73e-101">In the **Hybrid connections** blade, click the hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![Kliknij przycisk Ustawienia odbiornika](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="cc73e-103">**Właściwości połączenia hybrydowe** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="cc73e-103">The **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="cc73e-104">W obszarze **Menedżera połączeń hybrydowych lokalnymi**, wybierz **pobrać i skonfigurować ręcznie**, Zapisz pobrany pakiet HybridConnectionManager.msi i skopiuj parametry połączenia bramy.</span><span class="sxs-lookup"><span data-stu-id="cc73e-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save the downloaded HybridConnectionManager.msi package, and copy the gateway connection string.</span></span>
   
    ![Kliknij tutaj, aby zainstalować](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="cc73e-106">Z wiersza polecenia administratora wpisz następujące polecenie, aby uruchomić Instalatora:</span><span class="sxs-lookup"><span data-stu-id="cc73e-106">From an administrator command prompt, type the following command to start the installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="cc73e-107">Po uruchomieniu Instalatora, kliknij przycisk **nie teraz**, następnie przejdź do folderu %ProgramFiles%\Microsoft\HybridConnectionManager, uruchom HCMConfigWizard.exe i kliknij przycisk **tak** w **konta użytkownika Formant** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cc73e-107">After the installer runs, click **Not now**, then browse to the %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in the **User Account Control** dialog.</span></span>
5. <span data-ttu-id="cc73e-108">Wklej parametry połączenia hybrydowe, które wcześniej zostały skopiowane, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc73e-108">Paste the hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![Instalowanie](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="cc73e-110">Po zakończeniu instalacji kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="cc73e-110">When the install completes, click **Close**.</span></span>
   
    ![Kliknij przycisk Zamknij](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="cc73e-112">Na **połączeń hybrydowych** bloku **stan** zawiera obecnie kolumnę **połączony**.</span><span class="sxs-lookup"><span data-stu-id="cc73e-112">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span></span> 
   
    ![Stan połączenia](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

