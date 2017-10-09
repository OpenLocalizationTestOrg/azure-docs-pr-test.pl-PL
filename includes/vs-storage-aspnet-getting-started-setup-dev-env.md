## <a name="set-up-hello-development-environment"></a><span data-ttu-id="a0f68-101">Konfigurowanie środowiska deweloperskiego hello</span><span class="sxs-lookup"><span data-stu-id="a0f68-101">Set up hello development environment</span></span>

<span data-ttu-id="a0f68-102">W tej sekcji przedstawiono konfigurowanie środowiska deweloperskiego, w tym tworzenie aplikacji ASP.NET MVC, dodawanie połączenia usług połączonych dodawania kontrolera, i określanie hello wymagane dyrektywy przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="a0f68-102">This section walks you setting up your development environment, including creating an ASP.NET MVC app, adding a Connected Services connection, adding a controller, and specifying hello required namespace directives.</span></span>

### <a name="create-an-aspnet-mvc-app-project"></a><span data-ttu-id="a0f68-103">Utwórz projekt aplikacji platformy ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="a0f68-103">Create an ASP.NET MVC app project</span></span>

1. <span data-ttu-id="a0f68-104">Otwórz program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0f68-104">Open Visual Studio.</span></span>

1. <span data-ttu-id="a0f68-105">Wybierz **Plik -> Nowy -> Projekt** z menu głównego hello</span><span class="sxs-lookup"><span data-stu-id="a0f68-105">Select **File->New->Project** from hello main menu</span></span>

1. <span data-ttu-id="a0f68-106">Na powitania **nowy projekt** okna dialogowego i określ opcje hello jako hello wyróżniane na następującej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="a0f68-106">On hello **New Project** dialog, specify hello options as highlighted in hello following figure:</span></span>

    ![Tworzenie projektu platformy ASP.NET](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-1.png)

1. <span data-ttu-id="a0f68-108">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0f68-108">Select **OK**.</span></span>

1. <span data-ttu-id="a0f68-109">Na powitania **nowy projekt ASP.NET** okna dialogowego i określ opcje hello jako hello wyróżniane na następującej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="a0f68-109">On hello **New ASP.NET Project** dialog, specify hello options as highlighted in hello following figure:</span></span>

    ![Określ MVC](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-2.png)

1. <span data-ttu-id="a0f68-111">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0f68-111">Select **OK**.</span></span>

### <a name="use-connected-services-tooconnect-tooan-azure-storage-account"></a><span data-ttu-id="a0f68-112">Użyj konta magazynu Azure tooan tooconnect usługami</span><span class="sxs-lookup"><span data-stu-id="a0f68-112">Use Connected Services tooconnect tooan Azure storage account</span></span>

1. <span data-ttu-id="a0f68-113">W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz z menu kontekstowego hello **podłączonej usługi -> Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a0f68-113">In hello **Solution Explorer**, right-click hello project, and from hello context menu, select **Add->Connected Service**.</span></span>

1. <span data-ttu-id="a0f68-114">Na powitania **dodać podłączonej usługi** okno dialogowe, wybierz opcję **usługi Azure Storage**, a następnie wybierz **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="a0f68-114">On hello **Add Connected Service** dialog, select **Azure Storage**, and then select **Configure**.</span></span>

    ![Podłączonej usługi okna dialogowego](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-3.png)

1. <span data-ttu-id="a0f68-116">Na powitania **usługi Azure Storage** okno dialogowe, wybierz opcję hello kontem żądaną magazynu platformy Azure, z którą ma toowork i zaznacz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a0f68-116">On hello **Azure Storage** dialog, select hello desired Azure storage account with which you want toowork, and select **Add**.</span></span>
