<span data-ttu-id="aeacd-101">toounregister kroki powitania serwera przetwarzania różni się w zależności od stanu połączenia z powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="aeacd-101">hello steps toounregister a process server differs depending on its connection status with hello Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="aeacd-102">Wyrejestrowywanie serwera przetwarzania, który jest w stanie Połączono</span><span class="sxs-lookup"><span data-stu-id="aeacd-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="aeacd-103">Zdalne na powitania serwera przetwarzania jako Administrator.</span><span class="sxs-lookup"><span data-stu-id="aeacd-103">Remote into hello process server as an Administrator.</span></span>
2. <span data-ttu-id="aeacd-104">Uruchamianie hello **Panelu sterowania** , a następnie otwórz **programy > Odinstaluj program**</span><span class="sxs-lookup"><span data-stu-id="aeacd-104">Launch hello **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="aeacd-105">Odinstaluj program o nazwie hello **Microsoft Azure lokacji odzyskiwania procesu konfiguracji serwera**</span><span class="sxs-lookup"><span data-stu-id="aeacd-105">Uninstall a program by hello name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="aeacd-106">Po ukończeniu kroku 3 możesz odinstalować **zależności serwera konfiguracji/przetwarzania usługi Microsoft Azure Site Recovery**</span><span class="sxs-lookup"><span data-stu-id="aeacd-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="aeacd-107">Wyrejestrowywanie serwera przetwarzania, który jest w stanie Rozłączono</span><span class="sxs-lookup"><span data-stu-id="aeacd-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="aeacd-108">Użyj hello następujące czynności, należy używać, gdy nie ma żadnego sposób toorevive hello wirtualnej komputera na powitania, który został zainstalowany serwer przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="aeacd-108">Use hello below steps should be used if there is no way toorevive hello virtual machine on which hello Process Server was installed.</span></span>

1. <span data-ttu-id="aeacd-109">Zaloguj się na serwerze konfiguracji tooyour jako Administrator.</span><span class="sxs-lookup"><span data-stu-id="aeacd-109">Log on tooyour configuration server as an Administrator.</span></span>
2. <span data-ttu-id="aeacd-110">Otwórz administracyjny wiersz polecenia i przejdź do katalogu toohello `%ProgramData%\ASR\home\svsystems\bin`.</span><span class="sxs-lookup"><span data-stu-id="aeacd-110">Open an Administrative command prompt and browse toohello directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="aeacd-111">Teraz uruchom polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="aeacd-111">Now run hello command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="aeacd-112">Usunie hello szczegóły serwera przetwarzania hello z hello systemu.</span><span class="sxs-lookup"><span data-stu-id="aeacd-112">This will purge hello details of hello process server from hello system.</span></span>
