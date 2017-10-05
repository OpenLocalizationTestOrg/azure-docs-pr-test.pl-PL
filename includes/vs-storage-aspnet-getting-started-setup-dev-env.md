## <a name="set-up-the-development-environment"></a><span data-ttu-id="cd9da-101">Konfigurowanie środowiska deweloperskiego</span><span class="sxs-lookup"><span data-stu-id="cd9da-101">Set up the development environment</span></span>

<span data-ttu-id="cd9da-102">W tej sekcji przedstawiono konfigurowanie środowiska deweloperskiego, w tym tworzenie aplikacji ASP.NET MVC, dodawanie połączenia usług połączonych dodawania kontrolera i określanie dyrektywy wymaganej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="cd9da-102">This section walks you setting up your development environment, including creating an ASP.NET MVC app, adding a Connected Services connection, adding a controller, and specifying the required namespace directives.</span></span>

### <a name="create-an-aspnet-mvc-app-project"></a><span data-ttu-id="cd9da-103">Utwórz projekt aplikacji platformy ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="cd9da-103">Create an ASP.NET MVC app project</span></span>

1. <span data-ttu-id="cd9da-104">Otwórz program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd9da-104">Open Visual Studio.</span></span>

1. <span data-ttu-id="cd9da-105">Wybierz **Plik -> Nowy -> Projekt** z poziomu menu głównego</span><span class="sxs-lookup"><span data-stu-id="cd9da-105">Select **File->New->Project** from the main menu</span></span>

1. <span data-ttu-id="cd9da-106">Na **nowy projekt** okna dialogowego i określ opcje jako wyróżnione na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="cd9da-106">On the **New Project** dialog, specify the options as highlighted in the following figure:</span></span>

    ![Tworzenie projektu platformy ASP.NET](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-1.png)

1. <span data-ttu-id="cd9da-108">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="cd9da-108">Select **OK**.</span></span>

1. <span data-ttu-id="cd9da-109">Na **nowy projekt ASP.NET** okna dialogowego i określ opcje jako wyróżnione na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="cd9da-109">On the **New ASP.NET Project** dialog, specify the options as highlighted in the following figure:</span></span>

    ![Określ MVC](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-2.png)

1. <span data-ttu-id="cd9da-111">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="cd9da-111">Select **OK**.</span></span>

### <a name="use-connected-services-to-connect-to-an-azure-storage-account"></a><span data-ttu-id="cd9da-112">Połącz się z kontem magazynu platformy Azure za pomocą połączenia usług</span><span class="sxs-lookup"><span data-stu-id="cd9da-112">Use Connected Services to connect to an Azure storage account</span></span>

1. <span data-ttu-id="cd9da-113">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt i wybierz z menu kontekstowego **podłączonej usługi -> Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="cd9da-113">In the **Solution Explorer**, right-click the project, and from the context menu, select **Add->Connected Service**.</span></span>

1. <span data-ttu-id="cd9da-114">Na **dodać podłączonej usługi** okno dialogowe, wybierz opcję **usługi Azure Storage**, a następnie wybierz **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="cd9da-114">On the **Add Connected Service** dialog, select **Azure Storage**, and then select **Configure**.</span></span>

    ![Podłączonej usługi okna dialogowego](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-3.png)

1. <span data-ttu-id="cd9da-116">Na **usługi Azure Storage** okno dialogowe, wybierz konto żądaną magazynu Azure, z którym chcesz pracować, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="cd9da-116">On the **Azure Storage** dialog, select the desired Azure storage account with which you want to work, and select **Add**.</span></span>
