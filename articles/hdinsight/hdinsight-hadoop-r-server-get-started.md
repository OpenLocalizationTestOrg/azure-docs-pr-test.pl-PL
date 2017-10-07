---
title: "aaaGet wprowadzenie R Server w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się jak toocreate Apache Spark w klastrze usługi HDInsight, która obejmuje R Server i przesłać skrypt języka R w klastrze hello."
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="61bd4-103">Wprowadzenie do korzystania z oprogramowania R Server w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="61bd4-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="61bd4-104">HDInsight obejmuje toobe opcji R Server zintegrowana z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61bd4-104">HDInsight includes an R Server option toobe integrated into your HDInsight cluster.</span></span> <span data-ttu-id="61bd4-105">Ta opcja umożliwia skrypty R toouse Spark i MapReduce toorun rozproszone obliczenia.</span><span class="sxs-lookup"><span data-stu-id="61bd4-105">This option allows R scripts toouse Spark and MapReduce toorun distributed computations.</span></span> <span data-ttu-id="61bd4-106">W tym dokumencie możesz dowiedzieć się, jak toocreate R Server w klastrze usługi HDInsight, a następnie uruchom R skrypt, który demonstruje użycie platforma Spark dla rozproszone obliczenia R.</span><span class="sxs-lookup"><span data-stu-id="61bd4-106">In this document, you learn how toocreate an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="61bd4-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="61bd4-107">Prerequisites</span></span>

* <span data-ttu-id="61bd4-108">**Subskrypcja platformy Azure**: przed rozpoczęciem tego samouczka musisz mieć subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="61bd4-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="61bd4-109">Artykuł Przejdź toohello [bezpłatna wersja próbna platformy Microsoft Azure Pobierz](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="61bd4-109">Go toohello article [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="61bd4-110">**Klient Secure Shell (SSH)**: jest używany przez klienta SSH tooremotely Połącz z klastrem usługi HDInsight toohello i Uruchom polecenia bezpośrednio w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="61bd4-110">**A Secure Shell (SSH) client**: An SSH client is used tooremotely connect toohello HDInsight cluster and run commands directly on hello cluster.</span></span> <span data-ttu-id="61bd4-111">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="61bd4-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="61bd4-112">**(Opcjonalnie) kluczy SSH**: można zabezpieczyć hello SSH użyte konto tooconnect toohello klastra przy użyciu hasła lub klucza publicznego.</span><span class="sxs-lookup"><span data-stu-id="61bd4-112">**SSH keys (optional)**: You can secure hello SSH account used tooconnect toohello cluster using either a password or a public key.</span></span> <span data-ttu-id="61bd4-113">Przy użyciu hasła jest łatwiejsze i umożliwia tooget można uruchomić bez konieczności toocreate pary kluczy publiczny/prywatny.</span><span class="sxs-lookup"><span data-stu-id="61bd4-113">Using a password is easier, and allows you tooget started without having toocreate a public/private key pair.</span></span> <span data-ttu-id="61bd4-114">Jednak użycie klucza jest bezpieczniejsze.</span><span class="sxs-lookup"><span data-stu-id="61bd4-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="61bd4-115">Hello kroków w tym dokumencie założono, że używasz hasła.</span><span class="sxs-lookup"><span data-stu-id="61bd4-115">hello steps in this document assume that you are using a password.</span></span>


## <a name="automated-cluster-creation"></a><span data-ttu-id="61bd4-116">Zautomatyzowane tworzenie klastra</span><span class="sxs-lookup"><span data-stu-id="61bd4-116">Automated cluster creation</span></span>

<span data-ttu-id="61bd4-117">Można zautomatyzować tworzenie hello serwerów R HDInsight za pomocą usługi Azure Resource Manager szablony, hello zestawu SDK, a także programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="61bd4-117">You can automate hello creation of HDInsight R Servers using Azure Resource Manager templates, hello SDK, and also PowerShell.</span></span>

* <span data-ttu-id="61bd4-118">Zobacz toocreate R Server przy użyciu szablonu usługi Azure Resource Management [wdrażanie klastra usługi HDInsight R server](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span><span class="sxs-lookup"><span data-stu-id="61bd4-118">toocreate an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="61bd4-119">Zobacz toocreate moduł R Server przy użyciu zestawu .NET SDK hello [tworzenia opartych na systemie Linux klastrów w usłudze HDInsight przy użyciu zestawu .NET SDK hello.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="61bd4-119">toocreate an R Server using hello .NET SDK, see [create Linux-based clusters in HDInsight using hello .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="61bd4-120">toodeploy R Server przy użyciu programu powershell, zobacz artykuł hello na [Tworzenie serwera R w usłudze HDInsight przy użyciu programu PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="61bd4-120">toodeploy R Server using powershell, see hello article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a><span data-ttu-id="61bd4-121">Tworzenie klastra hello przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="61bd4-121">Create hello cluster using hello Azure portal</span></span>

1. <span data-ttu-id="61bd4-122">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="61bd4-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="61bd4-123">Wybierz pozycję **Nowy** -> **Rozwiązania inteligentne + analiza** -> **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="61bd4-123">Select **NEW** -> **Intelligence + Analytics**, -> **HDInsight**.</span></span>

    ![Obraz tworzenia nowego klastra](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. <span data-ttu-id="61bd4-125">W hello **szybkie tworzenie** uruchomienia systemu, wprowadź nazwę klastra hello w hello **nazwy klastra** pola.</span><span class="sxs-lookup"><span data-stu-id="61bd4-125">In hello **Quick create** experience, enter a name for hello cluster in hello **Cluster Name** field.</span></span> <span data-ttu-id="61bd4-126">Jeśli masz wiele subskrypcji Azure, użyj hello **subskrypcji** wpis tooselect hello jedną ma toouse.</span><span class="sxs-lookup"><span data-stu-id="61bd4-126">If you have multiple Azure subscriptions, use hello **Subscription** entry tooselect hello one you want toouse.</span></span>

    ![Wybór nazwy klastra i subskrypcji](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. <span data-ttu-id="61bd4-128">Wybierz **typ klastra** tooopen hello **konfiguracji klastra** bloku.</span><span class="sxs-lookup"><span data-stu-id="61bd4-128">Select **Cluster type** tooopen hello **Cluster configuration** blade.</span></span> <span data-ttu-id="61bd4-129">Na powitania **konfiguracji klastra** bloku hello wybierz następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="61bd4-129">On hello **Cluster Configuration** blade, select hello following options:</span></span>

    * <span data-ttu-id="61bd4-130">**Typ klastra**: R Server</span><span class="sxs-lookup"><span data-stu-id="61bd4-130">**Cluster Type**: R Server</span></span>
    * <span data-ttu-id="61bd4-131">**Wersja**: hello wybierz wersję tooinstall R Server w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="61bd4-131">**Version**: select hello version of R Server tooinstall on hello cluster.</span></span> <span data-ttu-id="61bd4-132">Witaj obecnie dostępna jest wersja ***R Server 9.1 (3,6 HDI)***.</span><span class="sxs-lookup"><span data-stu-id="61bd4-132">hello version currently available is ***R Server 9.1 (HDI 3.6)***.</span></span> <span data-ttu-id="61bd4-133">Dostępne są informacje o wersji dla hello dostępne wersje R Server [tutaj](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span><span class="sxs-lookup"><span data-stu-id="61bd4-133">Release notes for hello available versions of R Server are available [here](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span></span>
    * <span data-ttu-id="61bd4-134">**R Studio community edition dla R Server**: IDE tej przeglądarki jest instalowany domyślnie na powitania węzła krawędzi.</span><span class="sxs-lookup"><span data-stu-id="61bd4-134">**R Studio community edition for R Server**: this browser-based IDE is installed by default on hello edge node.</span></span> <span data-ttu-id="61bd4-135">Jeśli wolisz toonot jest zainstalowany, a następnie usuń zaznaczenie pola wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="61bd4-135">If you would prefer toonot have it installed, then uncheck hello check box.</span></span> <span data-ttu-id="61bd4-136">Jeśli wybierzesz toohave ją zainstalować, adres URL hello dla uzyskiwania dostępu do powitalne logowanie do serwera programu RStudio znajduje się w bloku portalu aplikacji dla klastra, po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="61bd4-136">If you choose toohave it installed, hello URL for accessing hello RStudio Server login is found on a portal application blade for your cluster once it’s been created.</span></span>
    * <span data-ttu-id="61bd4-137">Pozostaw hello inne opcje na powitania wartości domyślne i użyć hello **wybierz** toosave hello klastra typ przycisku.</span><span class="sxs-lookup"><span data-stu-id="61bd4-137">Leave hello other options at hello default values and use hello **Select** button toosave hello cluster type.</span></span>

        ![Zrzut ekranu bloku typu klastra](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. <span data-ttu-id="61bd4-139">Podaj wartości w pozycjach **Nazwa użytkownika logowania klastra** i **Hasło logowania klastra**.</span><span class="sxs-lookup"><span data-stu-id="61bd4-139">Enter a **Cluster login username** and **Cluster login password**.</span></span>

    <span data-ttu-id="61bd4-140">Określ wartość w pozycji **Nazwa użytkownika SSH**.</span><span class="sxs-lookup"><span data-stu-id="61bd4-140">Specify an **SSH Username**.</span></span> <span data-ttu-id="61bd4-141">SSH jest używane tooremotely połączyć toohello klastra przy użyciu **Secure Shell (SSH)** klienta.</span><span class="sxs-lookup"><span data-stu-id="61bd4-141">SSH is used tooremotely connect toohello cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="61bd4-142">Można określić użytkownika SSH hello w tym oknie dialogowym lub po utworzeniu klastra hello (na karcie Konfiguracja hello hello klastra).</span><span class="sxs-lookup"><span data-stu-id="61bd4-142">You can either specify hello SSH user in this dialog or after hello cluster has been created (in hello Configuration tab for hello cluster).</span></span> <span data-ttu-id="61bd4-143">R Server jest skonfigurowany tooexpect **nazwy użytkownika SSH** z "remoteuser".</span><span class="sxs-lookup"><span data-stu-id="61bd4-143">R Server is configured tooexpect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="61bd4-144">**Jeśli używasz innej nazwy użytkownika, należy wykonać dodatkowy krok po utworzeniu klastra hello.**</span><span class="sxs-lookup"><span data-stu-id="61bd4-144">**If you use a different username, you must perform an additional step after hello cluster is created.**</span></span>

    <span data-ttu-id="61bd4-145">Pozostaw pole hello sprawdzane pod kątem **Użyj tego samego hasła jak logowania do klastra** toouse **hasło** wpisywania hello uwierzytelniania, jeśli wolisz użycie klucza publicznego.</span><span class="sxs-lookup"><span data-stu-id="61bd4-145">Leave hello box checked for **Use same password as cluster login** toouse **PASSWORD** as hello authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="61bd4-146">Należy tooaccess pary kluczy publiczny/prywatny R Server w klastrze hello za pomocą zdalnego klienta jako, na przykład RTVS, programu RStudio lub innego pulpitu IDE.</span><span class="sxs-lookup"><span data-stu-id="61bd4-146">You need a public/private key pair tooaccess R Server on hello cluster via a remote client as, for example, RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="61bd4-147">Jeśli zainstalujesz powitania serwera programu RStudio community edition należy toochoose hasło SSH.</span><span class="sxs-lookup"><span data-stu-id="61bd4-147">If you install hello RStudio Server community edition, you need toochoose an SSH password.</span></span>     

    <span data-ttu-id="61bd4-148">toocreate i użyj pary kluczy publiczny/prywatny, usuń zaznaczenie pola wyboru **Użyj tego samego hasła jak logowania do klastra** , a następnie wybierz **klucz PUBLICZNY** i wykonać następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="61bd4-148">toocreate and use a public/private key pair, uncheck **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span> <span data-ttu-id="61bd4-149">W poniższych instrukcjach przyjęto, że jest zainstalowane środowisko Cygwin z programem ssh-keygen lub równoważnym.</span><span class="sxs-lookup"><span data-stu-id="61bd4-149">These instructions assume that you have Cygwin with ssh-keygen or an equivalent installed.</span></span>

    * <span data-ttu-id="61bd4-150">Generowanie pary kluczy publiczny/prywatny z wiersza polecenia hello na laptopie:</span><span class="sxs-lookup"><span data-stu-id="61bd4-150">Generate a public/private key pair from hello command prompt on your laptop:</span></span>

        <span data-ttu-id="61bd4-151">ssh-keygen -t rsa -b 2048</span><span class="sxs-lookup"><span data-stu-id="61bd4-151">ssh-keygen -t rsa -b 2048</span></span>

    * <span data-ttu-id="61bd4-152">Wykonaj hello monitu tooname plik klucza, a następnie wprowadź hasło zwiększyć bezpieczeństwo.</span><span class="sxs-lookup"><span data-stu-id="61bd4-152">Follow hello prompt tooname a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="61bd4-153">Na ekranie powinna przypominać powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="61bd4-153">Your screen should look something like hello following image:</span></span>

        ![Wiersz polecenia SSH w systemie Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * <span data-ttu-id="61bd4-155">To polecenie tworzy plik klucza prywatnego i plik klucza publicznego w obszarze .pub nazwa < prywatny klucz nazwa_pliku > Witaj, na przykład furiosa i furiosa.pub.</span><span class="sxs-lookup"><span data-stu-id="61bd4-155">This command creates a private key file and a public key file under hello name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

        ![Katalog polecenia SSH](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * <span data-ttu-id="61bd4-157">Następnie określ hello pliku klucza publicznego (&#42;. pub) podczas przypisywania HDI klastra poświadczeń i ostatecznie potwierdzić grupy zasobów i region oraz wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="61bd4-157">Then specify hello public key file (&#42;.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**.</span></span>

        ![Blok poświadczeń](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * <span data-ttu-id="61bd4-159">Zmień uprawnienia na powitania keyfile prywatnych na komputerze przenośnym:</span><span class="sxs-lookup"><span data-stu-id="61bd4-159">Change permissions on hello private keyfile on your laptop:</span></span>

        <span data-ttu-id="61bd4-160">chmod 600 <nazwa-pliku-klucza-prywatnego></span><span class="sxs-lookup"><span data-stu-id="61bd4-160">chmod 600 <private-key-filename></span></span>

   * <span data-ttu-id="61bd4-161">Użyj pliku klucza prywatnego hello przy użyciu protokołu SSH do logowania zdalnego:</span><span class="sxs-lookup"><span data-stu-id="61bd4-161">Use hello private key file with SSH for remote login:</span></span>

        <span data-ttu-id="61bd4-162">ssh –i <nazwa-pliku-klucza-prywatnego> remoteuser@<hostname public ip></span><span class="sxs-lookup"><span data-stu-id="61bd4-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span></span>

      <span data-ttu-id="61bd4-163">Lub, jako części definicji hello programu Hadoop Spark obliczeniowe kontekstu R serwera na powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="61bd4-163">Or, as part hello definition of your Hadoop Spark compute context for R Server on hello client.</span></span> <span data-ttu-id="61bd4-164">Zobacz hello **przy użyciu Microsoft R Server jako klienta usługi Hadoop** podsekcji w [utworzyć kontekst obliczeniowe platformy Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span><span class="sxs-lookup"><span data-stu-id="61bd4-164">See hello **Using Microsoft R Server as a Hadoop Client** subsection in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span></span>

6. <span data-ttu-id="61bd4-165">Witaj szybkie tworzenie przejściach toohello **magazynu** bloku tooselect hello konta magazynu toobe ustawienia używane do lokalizacji głównej hello hello systemu, używane przez klaster hello plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="61bd4-165">hello quick create transitions you toohello **Storage** blade tooselect hello storage account settings toobe used for hello primary location of hello HDFS file system used by hello cluster.</span></span> <span data-ttu-id="61bd4-166">Wybierz nowe lub istniejące konto usługi Azure Storage lub istniejące konto usługi Data Lake Storage.</span><span class="sxs-lookup"><span data-stu-id="61bd4-166">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

    - <span data-ttu-id="61bd4-167">W przypadku wybrania konta usługi Azure Storage istniejącego konta magazynu jest zaznaczone, wybierając **wybierz konto magazynu** i wybierając hello odpowiedniego konta.</span><span class="sxs-lookup"><span data-stu-id="61bd4-167">If you select an Azure Storage account, an existing storage account is selected by choosing **Select a storage account** and then selecting hello relevant account.</span></span> <span data-ttu-id="61bd4-168">Utwórz nowe konto, przy użyciu hello **Utwórz nowy** łącze w hello **wybierz konto magazynu** sekcji.</span><span class="sxs-lookup"><span data-stu-id="61bd4-168">Create a new account using hello **Create New** link in hello **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="61bd4-169">W przypadku wybrania **nowy** należy wprowadzić nazwę hello nowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="61bd4-169">If you select **New** you must enter a name for hello new storage account.</span></span> <span data-ttu-id="61bd4-170">Zielonego znacznika wyboru jest wyświetlane, gdy nazwa hello jest akceptowany.</span><span class="sxs-lookup"><span data-stu-id="61bd4-170">A green check appears if hello name is accepted.</span></span>

      <span data-ttu-id="61bd4-171">Witaj **domyślny kontener** domyślne nazwy toohello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="61bd4-171">hello **Default Container** defaults toohello name of hello cluster.</span></span> <span data-ttu-id="61bd4-172">Pozostaw to ustawienie domyślne wartości hello.</span><span class="sxs-lookup"><span data-stu-id="61bd4-172">Leave this default as hello value.</span></span>

      <span data-ttu-id="61bd4-173">Jeśli wybrano opcji nowego konta magazynu monitu tooselect **lokalizacji** jest podany tooselect które toocreate region hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="61bd4-173">If a new storage account option was selected a prompt tooselect **Location** is given tooselect which region toocreate hello storage account.</span></span>  

         ![Blok źródła danych](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="61bd4-175">Wybieranie lokalizacji hello hello domyślne źródło danych również Ustawia lokalizację hello hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61bd4-175">Selecting hello location for hello default data source  also sets hello location of hello HDInsight cluster.</span></span> <span data-ttu-id="61bd4-176">Witaj klaster i domyślne źródło danych musi być w hello tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="61bd4-176">hello cluster and default data source must be in hello same region.</span></span>

    - <span data-ttu-id="61bd4-177">Chcąc toouse istniejącej usługi Data Lake Store, następnie wybierz hello toouse konta magazynu ADLS i Dodaj klaster hello *Dodaj* tożsamości tooyour klastra tooallow dostępu toohello magazynu.</span><span class="sxs-lookup"><span data-stu-id="61bd4-177">If you want toouse an existing Data Lake Store, then select hello ADLS storage account toouse and add hello cluster *ADD* identity tooyour cluster tooallow access toohello store.</span></span> <span data-ttu-id="61bd4-178">Aby uzyskać więcej informacji na temat tego procesu, zobacz [Tworzenie klastra HDInsight z usługą Data Lake Store za pomocą witryny Azure Portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span><span class="sxs-lookup"><span data-stu-id="61bd4-178">For more information on this process, see [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

    <span data-ttu-id="61bd4-179">Użyj hello **wybierz** konfiguracji źródła danych hello toosave przycisku.</span><span class="sxs-lookup"><span data-stu-id="61bd4-179">Use hello **Select** button toosave hello data source configuration.</span></span>


7. <span data-ttu-id="61bd4-180">Witaj **Podsumowanie** bloku następnie wyświetla toovalidate wszystkie ustawienia.</span><span class="sxs-lookup"><span data-stu-id="61bd4-180">hello **Summary** blade then displays toovalidate all your settings.</span></span> <span data-ttu-id="61bd4-181">W tym miejscu możesz zmienić Twojego **rozmiar klastra** toomodify hello liczby serwerów w klastrze, a także określić dowolną **skryptu akcje** ma toorun.</span><span class="sxs-lookup"><span data-stu-id="61bd4-181">Here you can change your **Cluster size** toomodify hello number of servers in your cluster and also specify any **Script actions** you want toorun.</span></span> <span data-ttu-id="61bd4-182">Jeśli nie wiadomo, że należy większego klastra, pozostaw hello liczba węzłów procesu roboczego domyślną hello `4`.</span><span class="sxs-lookup"><span data-stu-id="61bd4-182">Unless you know that you need a larger cluster, leave hello number of worker nodes at hello default of `4`.</span></span> <span data-ttu-id="61bd4-183">Hello szacuje się, że koszt klastra hello jest wyświetlane w bloku hello.</span><span class="sxs-lookup"><span data-stu-id="61bd4-183">hello estimated cost of hello cluster is shown within hello blade.</span></span>

    ![podsumowanie klastra](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="61bd4-185">W razie potrzeby można zmienić rozmiar klastra później za pomocą hello Portal (**klastra** -> **ustawienia** -> **klaster w skali**) tooincrease lub Zmniejsz hello liczba węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="61bd4-185">If needed, you can resize your cluster later through hello Portal (**Cluster** -> **Settings** -> **Scale Cluster**) tooincrease or decrease hello number of worker nodes.</span></span>  <span data-ttu-id="61bd4-186">Ta zmiana rozmiaru mogą być przydatne, biegu dół klastra hello nieużywane lub Dodawanie wymagań hello toomeet wydajności większych zadań.</span><span class="sxs-lookup"><span data-stu-id="61bd4-186">This resizing can be useful for idling down hello cluster when not in use, or for adding capacity toomeet hello needs of larger tasks.</span></span>
   >
   >

   <span data-ttu-id="61bd4-187">Pewne czynniki tookeep pod uwagę podczas określania rozmiaru sieci klastra, hello węzły danych i węzłem krawędzi hello obejmują:</span><span class="sxs-lookup"><span data-stu-id="61bd4-187">Some factors tookeep in mind when sizing your cluster, hello data nodes, and hello edge node include:</span></span>  

   * <span data-ttu-id="61bd4-188">wydajności Hello rozproszonej analiz R Server w Spark jest proporcjonalny toohello liczba węzłów procesu roboczego po hello danych jest duży.</span><span class="sxs-lookup"><span data-stu-id="61bd4-188">hello performance of distributed R Server analyses on Spark is proportional toohello number of worker nodes when hello data is large.</span></span>  

   * <span data-ttu-id="61bd4-189">wydajności Hello R serwera analiz jest liniowa hello rozmiar danych analizowany.</span><span class="sxs-lookup"><span data-stu-id="61bd4-189">hello performance of R Server analyses is linear in hello size of data being analyzed.</span></span> <span data-ttu-id="61bd4-190">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="61bd4-190">For example:</span></span>  

     * <span data-ttu-id="61bd4-191">W przypadku małych toomodest danych wydajności jest najlepiej, gdy przeanalizowany w kontekście lokalnym na powitania węzła krawędzi.</span><span class="sxs-lookup"><span data-stu-id="61bd4-191">For small toomodest data, performance is best when analyzed in a local compute context on hello edge node.</span></span>  <span data-ttu-id="61bd4-192">Aby uzyskać więcej informacji na hello scenariuszy, w jakich lokalne powitania i Spark obliczeniowe kontekstów najlepiej, zobacz Opcje kontekstu obliczeń platformy R Server w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61bd4-192">For more information on hello scenarios under which hello local and Spark compute contexts work best, see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="61bd4-193">Jeśli Zaloguj się w węźle krawędzi toohello i uruchom skrypt R, a następnie wykonywane są wszystkie, oprócz hello ScaleR rx — funkcje <strong>lokalnie</strong> na powitania węzła krawędzi.</span><span class="sxs-lookup"><span data-stu-id="61bd4-193">If you log in toohello edge node and run your R script, then all but hello ScaleR rx-functions are executed <strong>locally</strong> on hello edge node.</span></span> <span data-ttu-id="61bd4-194">Dlatego hello pamięci i liczby rdzeni węzła krawędzi hello należy ustalać w związku z tym.</span><span class="sxs-lookup"><span data-stu-id="61bd4-194">So hello memory and number of cores of hello edge node should be sized accordingly.</span></span> <span data-ttu-id="61bd4-195">Witaj, którego dotyczy to również użycie R Server dla HDI kontekst zdalnego obliczeń z komputera przenośnego.</span><span class="sxs-lookup"><span data-stu-id="61bd4-195">hello same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![Blok warstw cenowych węzła](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     <span data-ttu-id="61bd4-197">Użyj hello **wybierz** węzła hello toosave przycisk cennik konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="61bd4-197">Use hello **Select** button toosave hello node pricing configuration.</span></span>

   <span data-ttu-id="61bd4-198">Dostępny jest również link **Pobierz szablon i parametry**.</span><span class="sxs-lookup"><span data-stu-id="61bd4-198">There is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="61bd4-199">Kliknięcie tego skryptów toodisplay łącza, które mogą być używane tooautomate hello tworzenia klastra z hello wybranej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="61bd4-199">Click on this link toodisplay scripts that can be used tooautomate hello creation of a cluster with hello selected configuration.</span></span> <span data-ttu-id="61bd4-200">Skrypty te są także dostępne w hello Azure portalu wpis dla klastra, po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="61bd4-200">These scripts are also available from hello Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="61bd4-201">Trwa trochę czasu, zanim toobe klastra hello utworzona, zwykle około 20 minut.</span><span class="sxs-lookup"><span data-stu-id="61bd4-201">It takes some time for hello cluster toobe created, usually around 20 minutes.</span></span> <span data-ttu-id="61bd4-202">Użyj kafelka hello na powitania tablicy startowej lub hello **powiadomienia** wpis na powitania rogu toocheck strony hello na powitania procesu tworzenia.</span><span class="sxs-lookup"><span data-stu-id="61bd4-202">Use hello tile on hello Startboard, or hello **Notifications** entry on hello left of hello page toocheck on hello creation process.</span></span>
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a><span data-ttu-id="61bd4-203">Połącz tooRStudio serwera</span><span class="sxs-lookup"><span data-stu-id="61bd4-203">Connect tooRStudio Server</span></span>

<span data-ttu-id="61bd4-204">Jeśli wybrano tooinclude serwera programu RStudio community edition w instalacji, możesz uzyskać dostęp hello programu RStudio logowania za pomocą dwóch różnych metod.</span><span class="sxs-lookup"><span data-stu-id="61bd4-204">If you’ve chosen tooinclude RStudio Server community edition in your installation, then you can access hello RStudio login via two different methods.</span></span>

1. <span data-ttu-id="61bd4-205">Przejdź toohello następującego adresu URL (gdzie **CLUSTERNAME** jest nazwą powitania po utworzeniu klastra hello):</span><span class="sxs-lookup"><span data-stu-id="61bd4-205">Go toohello following URL (where **CLUSTERNAME** is hello name of hello cluster you've created):</span></span>

    <span data-ttu-id="61bd4-206">https://**NAZWA-KLASTRA**.azurehdinsight.net/rstudio/</span><span class="sxs-lookup"><span data-stu-id="61bd4-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="61bd4-207">Otwórz pozycję hello klastra w hello portalu Azure, wybierz hello **pulpity nawigacyjne serwera R** szybkie łącze, a następnie wybierając hello **pulpitu nawigacyjnego Studio R**:</span><span class="sxs-lookup"><span data-stu-id="61bd4-207">Open hello entry for your cluster in hello Azure portal, select hello **R Server Dashboards** quick link and then selecting hello **R Studio Dashboard**:</span></span>

     ![Pulpit nawigacyjny studio hello R dostępu](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Pulpit nawigacyjny studio hello R dostępu](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="61bd4-210">Niezależnie od zastosowanej metody hello hello logujesz się po raz pierwszy należy tooauthenticate dwa razy.</span><span class="sxs-lookup"><span data-stu-id="61bd4-210">Regardless of hello method used, hello first time you log in you need tooauthenticate twice.</span></span>  <span data-ttu-id="61bd4-211">Na powitania pierwszego uwierzytelniania, zapewniają hello *nazwa użytkownika administratora klastra* i *hasło*.</span><span class="sxs-lookup"><span data-stu-id="61bd4-211">At hello first authentication, provide hello *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="61bd4-212">W drugim wierszu hello umożliwiające hello *nazwa użytkownika SSH* i *hasło*.</span><span class="sxs-lookup"><span data-stu-id="61bd4-212">At hello second prompt, provide hello *SSH userid* and *password*.</span></span> <span data-ttu-id="61bd4-213">Dziennik kolejne dodatki wymagać tylko hello *hasło SSH* i *userid*.</span><span class="sxs-lookup"><span data-stu-id="61bd4-213">Subsequent log ins only require hello *SSH password* and *userid*.</span></span>

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a><span data-ttu-id="61bd4-214">Połączenie z węzłem krawędzi serwera R toohello</span><span class="sxs-lookup"><span data-stu-id="61bd4-214">Connect toohello R Server edge node</span></span>

<span data-ttu-id="61bd4-215">Połączenie z węzłem krawędzi serwera tooR hello klastra usługi HDInsight przy użyciu protokołu SSH za pomocą polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="61bd4-215">Connect tooR Server edge node of hello HDInsight cluster using SSH with hello command:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="61bd4-216">Można znaleźć hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` adresu w hello portalu Azure, wybierając klastra następnie **wszystkie ustawienia** -> **aplikacje** -> **użyciu polecenia RServer**.</span><span class="sxs-lookup"><span data-stu-id="61bd4-216">You can find hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in hello Azure portal by selecting your cluster then **All Settings** -> **Apps** -> **RServer**.</span></span> <span data-ttu-id="61bd4-217">Zostaną wyświetlone informacje o punkcie końcowym SSH dla węzła krawędzi hello hello.</span><span class="sxs-lookup"><span data-stu-id="61bd4-217">This displays hello SSH Endpoint information for hello edge node.</span></span>
>
> ![Obraz powitania punkt końcowy SSH dla węzła krawędzi hello](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

<span data-ttu-id="61bd4-219">Jeśli użyto toosecure hasło konta użytkownika SSH, to zostanie wyświetlony monit o tooenter go.</span><span class="sxs-lookup"><span data-stu-id="61bd4-219">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="61bd4-220">Jeśli używasz klucza publicznego, może być toouse hello `-i` toospecify parametru hello odpowiedniego klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="61bd4-220">If you used a public key, you may have toouse hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="61bd4-221">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="61bd4-221">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="61bd4-222">Aby uzyskać więcej informacji, zobacz [połączyć tooHDInsight (Hadoop) przy użyciu protokołu SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="61bd4-222">For more information, see [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="61bd4-223">Po nawiązaniu połączenia przyjeździe monitu o podobnych następujące toohello:</span><span class="sxs-lookup"><span data-stu-id="61bd4-223">Once connected, you arrive at a prompt similar toohello following:</span></span>

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="61bd4-224">Włączanie obsługi równoczesnych użytkowników</span><span class="sxs-lookup"><span data-stu-id="61bd4-224">Enable multiple concurrent users</span></span>

<span data-ttu-id="61bd4-225">Można włączyć wiele równoczesnych użytkowników, dodając więcej użytkowników dla węzła krawędzi hello, na które hello społeczności programu RStudio uruchamia wersję.</span><span class="sxs-lookup"><span data-stu-id="61bd4-225">You can enable multiple concurrent users by adding more users for hello edge node on which hello RStudio community version runs.</span></span>

<span data-ttu-id="61bd4-226">Podczas tworzenia klastra usługi HDInsight musisz podać dwóch użytkowników: użytkownika HTTP i użytkownika SSH:</span><span class="sxs-lookup"><span data-stu-id="61bd4-226">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![Równoczesny użytkownik 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- <span data-ttu-id="61bd4-228">**Nazwa użytkownika logowania klastra**: HTTP użytkownika do uwierzytelniania za pośrednictwem bramy HDInsight hello, która jest używana tooprotect hello HDInsight clusters utworzony.</span><span class="sxs-lookup"><span data-stu-id="61bd4-228">**Cluster login username**: an HTTP user for authentication through hello HDInsight gateway that is used tooprotect hello HDInsight clusters you created.</span></span> <span data-ttu-id="61bd4-229">Ten użytkownik HTTP jest używane tooaccess hello interfejsu użytkownika narzędzia Ambari, interfejsie użytkownika YARN, jak również inne składniki interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="61bd4-229">This HTTP user is used tooaccess hello Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="61bd4-230">**Bezpiecznej powłoki (SSH) username**: SSH użytkownika tooaccess hello klastra za pośrednictwem bezpiecznej powłoki.</span><span class="sxs-lookup"><span data-stu-id="61bd4-230">**Secure Shell (SSH) username**: an SSH user tooaccess hello cluster through secure shell.</span></span> <span data-ttu-id="61bd4-231">Ten użytkownik jest użytkownikiem w hello systemu Linux dla wszystkich węzłów głównych hello węzłów procesu roboczego i węzły krawędzi.</span><span class="sxs-lookup"><span data-stu-id="61bd4-231">This user is a user in hello Linux system for all hello head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="61bd4-232">Aby można było korzystać tooaccess bezpiecznej powłoki dowolny z węzłów hello w zdalnym klastrze.</span><span class="sxs-lookup"><span data-stu-id="61bd4-232">So you can use secure shell tooaccess any of hello nodes in a remote cluster.</span></span>

<span data-ttu-id="61bd4-233">Witaj R Studio Server Community wersja programu używana w hello Microsoft R Server w klastrze usługi HDInsight typu akceptuje tylko Linux nazwę użytkownika i hasło jako mechanizm logowania.</span><span class="sxs-lookup"><span data-stu-id="61bd4-233">hello R Studio Server Community version used in hello Microsoft R Server on HDInsight type cluster accepts only Linux username and password as a login mechanism.</span></span> <span data-ttu-id="61bd4-234">Przekazywanie tokenów nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="61bd4-234">It does not support passing tokens.</span></span> <span data-ttu-id="61bd4-235">Tak, jeśli utworzono nowy klaster, a toouse tooaccess R Studio, należy toolog w dwa razy.</span><span class="sxs-lookup"><span data-stu-id="61bd4-235">So if you have created a new cluster and want toouse R Studio tooaccess it, you need toolog in twice.</span></span>

- <span data-ttu-id="61bd4-236">Najpierw zalogować się przy użyciu poświadczeń użytkownika hello HTTP za pośrednictwem hello bramy usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="61bd4-236">First log in using hello HTTP user credentials through hello HDInsight Gateway:</span></span> 

    ![Równoczesny użytkownik 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- <span data-ttu-id="61bd4-238">Następnie użyj toolog poświadczenia użytkownika SSH hello w tooRStudio:</span><span class="sxs-lookup"><span data-stu-id="61bd4-238">Then use hello SSH user credentials toolog in tooRStudio:</span></span>
  
    ![Równoczesny użytkownik 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

<span data-ttu-id="61bd4-240">Aktualnie podczas aprowizowania klastra usługi HDInsight można utworzyć tylko jedno konto użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="61bd4-240">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="61bd4-241">Dlatego tooenable wielu użytkowników tooaccess Microsoft R Server w usłudze HDInsight clusters, potrzebujemy toocreate dodatkowym użytkownikom w hello systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="61bd4-241">So tooenable multiple users tooaccess Microsoft R Server on HDInsight clusters, we need toocreate additional users in hello Linux system.</span></span>

<span data-ttu-id="61bd4-242">Ponieważ programu RStudio społeczności serwera jest uruchomiona w węźle krawędzi hello klastra, istnieje kilka kroków w tym miejscu:</span><span class="sxs-lookup"><span data-stu-id="61bd4-242">Because RStudio Server Community is running on hello cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="61bd4-243">Użyj toolog użytkownika SSH hello utworzone w węźle krawędzi toohello</span><span class="sxs-lookup"><span data-stu-id="61bd4-243">Use hello created SSH user toolog in toohello edge node</span></span>
2. <span data-ttu-id="61bd4-244">Dodaj użytkowników systemu Linux w węźle krawędzi</span><span class="sxs-lookup"><span data-stu-id="61bd4-244">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="61bd4-245">Wersja ciągu identyfikacyjnego programu RStudio za pomocą hello utworzonych przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="61bd4-245">Use RStudio Community version with hello user created</span></span>

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a><span data-ttu-id="61bd4-246">Krok 1: Stosowanie toolog użytkownika SSH hello utworzone w węźle krawędzi toohello</span><span class="sxs-lookup"><span data-stu-id="61bd4-246">Step 1: Use hello created SSH user toolog in toohello edge node</span></span>

<span data-ttu-id="61bd4-247">Pobranie dowolnego narzędzia SSH (takiego jak Putty) i użycie hello istniejących SSH użytkownika toolog w.</span><span class="sxs-lookup"><span data-stu-id="61bd4-247">Download any SSH tool (such as Putty) and use hello existing SSH user toolog in.</span></span> <span data-ttu-id="61bd4-248">Następnie wykonaj hello instrukcje podane w [połączyć tooHDInsight (Hadoop) przy użyciu protokołu SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello węzła krawędzi.</span><span class="sxs-lookup"><span data-stu-id="61bd4-248">Then follow hello instructions provided in [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello edge node.</span></span> <span data-ttu-id="61bd4-249">jest Hello adres węzła krawędzi serwera R w klastrze usługi HDInsight: *clustername-ed-ssh.azurehdinsight.net*</span><span class="sxs-lookup"><span data-stu-id="61bd4-249">hello edge node address for R Server on HDInsight cluster is: *clustername-ed-ssh.azurehdinsight.net*</span></span>


### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="61bd4-250">Krok 2. Dodawanie użytkowników systemu Linux w węźle krawędzi</span><span class="sxs-lookup"><span data-stu-id="61bd4-250">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="61bd4-251">tooadd węzła krawędzi toohello użytkownika, wykonaj polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="61bd4-251">tooadd a user toohello edge node, execute hello commands:</span></span>

    sudo useradd yournewusername -m
    sudo passwd yourusername

<span data-ttu-id="61bd4-252">Powinny pojawić się hello następujących elementów zwróconych:</span><span class="sxs-lookup"><span data-stu-id="61bd4-252">You should see hello following items returned:</span></span> 

![Równoczesny użytkownik 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

<span data-ttu-id="61bd4-254">Po wyświetleniu monitu o "bieżące hasło protokołu Kerberos:", wystarczy nacisnąć klawisz **Enter** tooignore go.</span><span class="sxs-lookup"><span data-stu-id="61bd4-254">When prompted for “Current Kerberos password:”, just press **Enter** tooignore it.</span></span> <span data-ttu-id="61bd4-255">Witaj `-m` opcji `useradd` polecenie wskazuje, że hello system utworzy folder macierzysty użytkownika hello, co jest wymagane dla wersji społeczności programu RStudio.</span><span class="sxs-lookup"><span data-stu-id="61bd4-255">hello `-m` option in `useradd` command indicates that hello system will create a home folder for hello user, which is required for RStudio Community version.</span></span>


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a><span data-ttu-id="61bd4-256">Krok 3: Użyj programu RStudio społeczności wersji z hello utworzonych przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="61bd4-256">Step 3: Use RStudio Community version with hello user created</span></span>

<span data-ttu-id="61bd4-257">Użyj hello toolog utworzonych przez użytkownika w tooRStudio:</span><span class="sxs-lookup"><span data-stu-id="61bd4-257">Use hello user created toolog in tooRStudio:</span></span>

![Równoczesny użytkownik 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

<span data-ttu-id="61bd4-259">Powiadomienia programu RStudio wskazuje, że używasz hello nowego użytkownika (tutaj, na przykład *sshuser6*) toolog hello klastra:</span><span class="sxs-lookup"><span data-stu-id="61bd4-259">Notice that RStudio indicates that you are using hello new user (here, for example, *sshuser6*) toolog in hello cluster:</span></span> 

![Równoczesny użytkownik 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

<span data-ttu-id="61bd4-261">Możesz także zalogować się przy użyciu poświadczeń oryginalnego hello (domyślnie jest *sshuser*) jednocześnie z innego okna przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="61bd4-261">You can also log in using hello original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="61bd4-262">Zadania można przesyłać za pomocą funkcji programu ScaleR.</span><span class="sxs-lookup"><span data-stu-id="61bd4-262">You can submit a job using scaleR functions.</span></span> <span data-ttu-id="61bd4-263">Oto przykład toorun polecenia używane hello zadania:</span><span class="sxs-lookup"><span data-stu-id="61bd4-263">Here is an example of hello commands used toorun a job:</span></span>

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


<span data-ttu-id="61bd4-264">Zwróć uwagę, czy zadania hello przekazane w różnych nazw użytkowników w interfejsie użytkownika YARN:</span><span class="sxs-lookup"><span data-stu-id="61bd4-264">Notice that hello jobs submitted are under different user names in YARN UI:</span></span>

![Równoczesny użytkownik 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

<span data-ttu-id="61bd4-266">Uwaga również tego hello nowo dodanych użytkowników nie mają uprawnień do katalogu głównego w systemie Linux, ale one mieć hello tego samego dostępu do plików hello tooall hello systemu plików HDFS i WASB magazynu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="61bd4-266">Note also that hello newly added users do not have root privileges in Linux system, but they do have hello same access tooall hello files in hello remote HDFS and WASB storage.</span></span>


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a><span data-ttu-id="61bd4-267">Za pomocą konsoli hello R</span><span class="sxs-lookup"><span data-stu-id="61bd4-267">Use hello R console</span></span>

1. <span data-ttu-id="61bd4-268">Hello sesji SSH używając hello następujące polecenia toostart hello R konsoli:</span><span class="sxs-lookup"><span data-stu-id="61bd4-268">From hello SSH session, use hello following command toostart hello R console:</span></span>  

        R

2. <span data-ttu-id="61bd4-269">Powinny pojawić się dane wyjściowe podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="61bd4-269">You should see output similar toohello following:</span></span>
    
    <span data-ttu-id="61bd4-270">Wersja 3.2.2 (2015-08-14)--"Fire bezpieczeństwa" Copyright (C) 2015 R hello R Foundation dla platformy przetwarzania danych statystycznych: x86_64-komputer linux-gnu (64-bitowe)</span><span class="sxs-lookup"><span data-stu-id="61bd4-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 hello R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span></span>

    <span data-ttu-id="61bd4-271">Bezpłatne oprogramowanie R jest dostarczane BEZ ŻADNEJ GWARANCJI.</span><span class="sxs-lookup"><span data-stu-id="61bd4-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span></span>
    <span data-ttu-id="61bd4-272">Jesteś tooredistribute powitalnej określonych warunkach.</span><span class="sxs-lookup"><span data-stu-id="61bd4-272">You are welcome tooredistribute it under certain conditions.</span></span>
    <span data-ttu-id="61bd4-273">Wpisz „license()” lub „licence()”, aby uzyskać szczegółowe informacje o dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="61bd4-273">Type 'license()' or 'licence()' for distribution details.</span></span>

    <span data-ttu-id="61bd4-274">Oprogramowanie obsługuje język naturalny, ale z angielskimi ustawieniami regionalnymi.</span><span class="sxs-lookup"><span data-stu-id="61bd4-274">Natural language support but running in an English locale</span></span>

    <span data-ttu-id="61bd4-275">R jest projektem zbiorowym, zrzeszającym wielu uczestników.</span><span class="sxs-lookup"><span data-stu-id="61bd4-275">R is a collaborative project with many contributors.</span></span>
    <span data-ttu-id="61bd4-276">Wpisz "contributors()" Aby uzyskać więcej informacji oraz "citation()" w sposób toocite R lub R pakietów w publikacji.</span><span class="sxs-lookup"><span data-stu-id="61bd4-276">Type 'contributors()' for more information and 'citation()' on how toocite R or R packages in publications.</span></span>

    <span data-ttu-id="61bd4-277">Typ "demo()" dla niektórych pokazów, "help()", aby uzyskać pomoc online lub "help.start()" dla toohelp Interfejs przeglądarki HTML.</span><span class="sxs-lookup"><span data-stu-id="61bd4-277">Type 'demo()' for some demos, 'help()' for on-line help, or 'help.start()' for an HTML browser interface toohelp.</span></span>
    <span data-ttu-id="61bd4-278">Wpisz "q()" tooquit R.</span><span class="sxs-lookup"><span data-stu-id="61bd4-278">Type 'q()' tooquit R.</span></span>

    <span data-ttu-id="61bd4-279">Oprogramowanie Microsoft R Server w wersji 8.0: rozszerzona dystrybucja pakietów R firmy Microsoft. Copyright (C) 2016 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="61bd4-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span></span>

    <span data-ttu-id="61bd4-280">Aby uzyskać informacje o wersji, wpisz „readme()”.</span><span class="sxs-lookup"><span data-stu-id="61bd4-280">Type 'readme()' for release notes.</span></span>
    >

3. <span data-ttu-id="61bd4-281">Z hello `>` monitu, można wprowadzić kod R.</span><span class="sxs-lookup"><span data-stu-id="61bd4-281">From hello `>` prompt, you can enter R code.</span></span> <span data-ttu-id="61bd4-282">Serwer R obejmuje pakiety, które pozwalają tooeasily interakcji z Hadoop i uruchom rozproszone obliczenia.</span><span class="sxs-lookup"><span data-stu-id="61bd4-282">R server includes packages that allow you tooeasily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="61bd4-283">Na przykład można użyć następującego polecenia tooview hello głównym hello domyślnego systemu plików dla klastra usługi HDInsight hello hello:</span><span class="sxs-lookup"><span data-stu-id="61bd4-283">For example, use hello following command tooview hello root of hello default file system for hello HDInsight cluster:</span></span>

    <span data-ttu-id="61bd4-284">rxHadoopListFiles("/")</span><span class="sxs-lookup"><span data-stu-id="61bd4-284">rxHadoopListFiles("/")</span></span>

4. <span data-ttu-id="61bd4-285">Umożliwia również hello WASB styl adresowania.</span><span class="sxs-lookup"><span data-stu-id="61bd4-285">You can also use hello WASB style addressing.</span></span>

    <span data-ttu-id="61bd4-286">rxHadoopListFiles("wasb:///")</span><span class="sxs-lookup"><span data-stu-id="61bd4-286">rxHadoopListFiles("wasb:///")</span></span>


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="61bd4-287">Używanie oprogramowania R Server w usłudze HDI ze zdalnego wystąpienia oprogramowania Microsoft R Server lub programu Microsoft R Client</span><span class="sxs-lookup"><span data-stu-id="61bd4-287">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="61bd4-288">Jest możliwe tooset się dostępu toohello HDI Hadoop Spark obliczeń kontekstu ze zdalnego wystąpienia programu Microsoft R Server lub uruchomione na pulpicie lub laptop klienta R firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="61bd4-288">It is possible tooset up access toohello HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop.</span></span> <span data-ttu-id="61bd4-289">Zobacz **przy użyciu Microsoft R Server jako klienta usługi Hadoop** podsekcji w hello [tworzenie kontekst obliczeniowe dla Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="61bd4-289">See **Using Microsoft R Server as a Hadoop Client** subsection in hello [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span></span> <span data-ttu-id="61bd4-290">toodo tak, konieczne jest hello toospecify następujące opcje, definiując kontekstu obliczeń RxSpark hello na laptopie: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches i sshProfileScript.</span><span class="sxs-lookup"><span data-stu-id="61bd4-290">toodo so, you need toospecify hello following options when defining hello RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="61bd4-291">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="61bd4-291">For example:</span></span>


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a><span data-ttu-id="61bd4-292">Używanie kontekstu obliczeniowego</span><span class="sxs-lookup"><span data-stu-id="61bd4-292">Use a compute context</span></span>

<span data-ttu-id="61bd4-293">Kontekst obliczeń umożliwia toocontrol obliczeń jest wykonywana lokalnie na węzeł brzegowy hello lub rozproszone na powitania węzłach w klastrze usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="61bd4-293">A compute context allows you toocontrol whether computation is performed locally on hello edge node or distributed across hello nodes in hello HDInsight cluster.</span></span>

1. <span data-ttu-id="61bd4-294">Z serwera programu RStudio lub konsoli hello R (w sesji SSH) Użyj następującego kodu tooload przykładowe dane do magazynu domyślnego powitania dla usługi HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="61bd4-294">From RStudio Server or hello R console (in an SSH session), use hello following code tooload example data into hello default storage for HDInsight:</span></span>

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. <span data-ttu-id="61bd4-295">Następnie umożliwia tworzenie niektóre informacje o danych i zdefiniowanie dwóch źródeł danych, tak aby firma Microsoft może współpracować z hello danych.</span><span class="sxs-lookup"><span data-stu-id="61bd4-295">Next, let's create some data info and define two data sources so that we can work with hello data.</span></span>

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. <span data-ttu-id="61bd4-296">Teraz uruchom Regresja logistyczna nad danymi hello przy użyciu kontekstu obliczeń lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="61bd4-296">Let's run a logistic regression over hello data using hello local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="61bd4-297">Powinny pojawić się dane wyjściowe, która kończy się toohello podobne wiersze po:</span><span class="sxs-lookup"><span data-stu-id="61bd4-297">You should see output that ends with lines similar toohello following:</span></span>

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. <span data-ttu-id="61bd4-298">Następnie uruchom teraz hello tego samego Regresja logistyczna przy użyciu kontekstu Spark hello.</span><span class="sxs-lookup"><span data-stu-id="61bd4-298">Next, let's run hello same logistic regression using hello Spark context.</span></span> <span data-ttu-id="61bd4-299">kontekst Spark Hello dystrybuuje hello przetwarzania za pośrednictwem wszystkich węzłów procesu roboczego hello hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61bd4-299">hello Spark context distributes hello processing over all hello worker nodes in hello HDInsight cluster.</span></span>

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > <span data-ttu-id="61bd4-300">Umożliwia także MapReduce toodistribute obliczeń na węzłach klastra.</span><span class="sxs-lookup"><span data-stu-id="61bd4-300">You can also use MapReduce toodistribute computation across cluster nodes.</span></span> <span data-ttu-id="61bd4-301">Aby uzyskać więcej informacji na temat kontekstu obliczeniowego, zobacz [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md) (Opcje kontekstu obliczeniowego dla oprogramowania R Server w usłudze HDInsight).</span><span class="sxs-lookup"><span data-stu-id="61bd4-301">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-toomultiple-nodes"></a><span data-ttu-id="61bd4-302">Dystrybuuj węzłów toomultiple kodu języka R</span><span class="sxs-lookup"><span data-stu-id="61bd4-302">Distribute R code toomultiple nodes</span></span>

<span data-ttu-id="61bd4-303">Z serwerem R, można łatwo zająć istniejącego kodu języka R i uruchom go na wielu węzłach w klastrze hello przy użyciu `rxExec`.</span><span class="sxs-lookup"><span data-stu-id="61bd4-303">With R Server, you can easily take existing R code and run it across multiple nodes in hello cluster by using `rxExec`.</span></span> <span data-ttu-id="61bd4-304">Funkcja ta jest przydatna podczas czyszczenia parametrów lub przeprowadzania symulacji.</span><span class="sxs-lookup"><span data-stu-id="61bd4-304">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="61bd4-305">Witaj następujący kod jest przykładem toouse `rxExec`:</span><span class="sxs-lookup"><span data-stu-id="61bd4-305">hello following code is an example of how toouse `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="61bd4-306">Jeśli nadal używasz hello Spark lub kontekstu MapReduce, to polecenie zwraca wartość nodename hello węzłów procesu roboczego hello kodu hello `(Sys.info()["nodename"])` jest uruchamiane na.</span><span class="sxs-lookup"><span data-stu-id="61bd4-306">If you are still using hello Spark or MapReduce context, this  command returns hello nodename value for hello worker nodes that hello code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="61bd4-307">Na przykład w klastrze czterema węzłami, prawdopodobnie tooreceive dane wyjściowe podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="61bd4-307">For example, on a four node cluster, you expect tooreceive output similar toohello following:</span></span>

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="61bd4-308">Dostęp do danych w usługach Hive i Parquet</span><span class="sxs-lookup"><span data-stu-id="61bd4-308">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="61bd4-309">Funkcja dostępna w R Server 9.1 umożliwia toodata bezpośredni dostęp do gałęzi i Parquet do użycia przez funkcje ScaleR w kontekście obliczeń Spark hello.</span><span class="sxs-lookup"><span data-stu-id="61bd4-309">A feature available in R Server 9.1 allows direct access toodata in Hive and Parquet for use by ScaleR functions in hello Spark compute context.</span></span> <span data-ttu-id="61bd4-310">Te funkcje są dostępne nowe ScaleR źródła funkcji danych o nazwie RxHiveData i RxParquetData współpracujących przy użyciu programu Spark SQL tooload dane bezpośrednio do DataFrame Spark, do analizy przez ScaleR.</span><span class="sxs-lookup"><span data-stu-id="61bd4-310">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL tooload data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="61bd4-311">Witaj następującego kodu zawiera niektóre przykładowy kod przy użyciu nowych funkcji hello:</span><span class="sxs-lookup"><span data-stu-id="61bd4-311">hello following code provides some sample code on use of hello new functions:</span></span>

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


<span data-ttu-id="61bd4-312">Aby uzyskać dodatkowe informacje dotyczące użycia tych nowych funkcji, zobacz Pomoc online hello R Server przy użyciu hello `?RxHivedata` i `?RxParquetData` poleceń.</span><span class="sxs-lookup"><span data-stu-id="61bd4-312">For additional info on use of these new functions see hello online help in R Server through use of hello `?RxHivedata` and `?RxParquetData` commands.</span></span>  


## <a name="install-additional-r-packages-on-hello-edge-node"></a><span data-ttu-id="61bd4-313">Zainstaluj dodatkowe pakiety języka R w węźle krawędzi hello</span><span class="sxs-lookup"><span data-stu-id="61bd4-313">Install additional R packages on hello edge node</span></span>

<span data-ttu-id="61bd4-314">Jeśli chcesz, dodatkowe pakiety języka R tooinstall na węzeł brzegowy hello, możesz użyć `install.packages()` bezpośrednio z poziomu hello R konsoli po połączonych toohello krawędzi węzła za pośrednictwem protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="61bd4-314">If you would like tooinstall additional R packages on hello edge node, you can use `install.packages()` directly from within hello R console when connected toohello edge node through SSH.</span></span> <span data-ttu-id="61bd4-315">Jednak pakiety języka R tooinstall na powitania węzłów procesu roboczego hello klastra, należy należy użyć akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="61bd4-315">However, if you need tooinstall R packages on hello worker nodes of hello cluster, you must use a Script Action.</span></span>

<span data-ttu-id="61bd4-316">Akcje skryptu to skrypty Bash, które są używane toomake konfiguracji zmiany toohello HDInsight klastra lub tooinstall dodatkowego oprogramowania, np. dodatkowe pakiety języka R.</span><span class="sxs-lookup"><span data-stu-id="61bd4-316">Script Actions are Bash scripts that are used toomake configuration changes toohello HDInsight cluster or tooinstall additional software, such as additional R packages.</span></span> <span data-ttu-id="61bd4-317">tooinstall dodatkowe pakiety przy użyciu akcji skryptu, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="61bd4-317">tooinstall additional packages using a Script Action, use hello following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61bd4-318">Za pomocą akcji skryptu tooinstall dodatkowe pakiety języka R można używać tylko po utworzeniu klastra hello.</span><span class="sxs-lookup"><span data-stu-id="61bd4-318">Using Script Actions tooinstall additional R packages can only be used after hello cluster has been created.</span></span> <span data-ttu-id="61bd4-319">Nie należy używać tej procedury podczas tworzenia klastra, ponieważ skrypt hello korzysta z tego serwera R całkowicie zainstalowana i skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="61bd4-319">Do not use this procedure during cluster creation, as hello script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="61bd4-320">Z hello [portalu Azure](https://portal.azure.com), wybierz serwer R w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="61bd4-320">From hello [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="61bd4-321">Z hello **ustawienia** bloku, wybierz opcję **akcji skryptu** , a następnie **przesłać nowe** toosubmit nowa akcja skryptu.</span><span class="sxs-lookup"><span data-stu-id="61bd4-321">From hello **Settings** blade, select **Script Actions** and then **Submit New** toosubmit a new Script Action.</span></span>

   ![Obraz bloku akcji skryptu](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. <span data-ttu-id="61bd4-323">Z hello **przesłać akcji skryptu** bloku, podaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="61bd4-323">From hello **Submit script action** blade, provide hello following information:</span></span>

   * <span data-ttu-id="61bd4-324">**Nazwa**: przyjazną nazwę tego skryptu tooidentify</span><span class="sxs-lookup"><span data-stu-id="61bd4-324">**Name**: A friendly name tooidentify this script</span></span>

   * <span data-ttu-id="61bd4-325">**Identyfikator URI skryptu powłoki systemowej**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="61bd4-325">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="61bd4-326">**Główny**: to pole powinno być **niezaznaczone**</span><span class="sxs-lookup"><span data-stu-id="61bd4-326">**Head**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="61bd4-327">**Proces roboczy**: to pole powinno być **zaznaczone**</span><span class="sxs-lookup"><span data-stu-id="61bd4-327">**Worker**: This item should be **checked**</span></span>

   * <span data-ttu-id="61bd4-328">**Węzły krawędzi**: to pole powinno być **niezaznaczone**</span><span class="sxs-lookup"><span data-stu-id="61bd4-328">**Edge nodes**: This item should be **unchecked**.</span></span>

   * <span data-ttu-id="61bd4-329">**Dozorca**: to pole powinno być **niezaznaczone**</span><span class="sxs-lookup"><span data-stu-id="61bd4-329">**Zookeeper**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="61bd4-330">**Parametry**: toobe zainstalowanych pakietów hello R.</span><span class="sxs-lookup"><span data-stu-id="61bd4-330">**Parameters**: hello R packages toobe installed.</span></span> <span data-ttu-id="61bd4-331">Na przykład: `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="61bd4-331">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="61bd4-332">**Utrwal ten skrypt...**: to pole powinno być **zaznaczone**</span><span class="sxs-lookup"><span data-stu-id="61bd4-332">**Persist this script...**: This item should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="61bd4-333">Domyślnie wszystkie pakiety języka R są zainstalowane z migawki spójne z wersją powitania serwera R, która została zainstalowana repozytorium Microsoft MRAN hello.</span><span class="sxs-lookup"><span data-stu-id="61bd4-333">By default, all R packages are installed from a snapshot of hello Microsoft MRAN repository consistent with hello version of R Server that has been installed.</span></span> <span data-ttu-id="61bd4-334">Jeśli chcesz tooinstall nowsze wersje pakietów, oznacza to, że niektóre ryzyka niezgodności.</span><span class="sxs-lookup"><span data-stu-id="61bd4-334">If you want tooinstall newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="61bd4-335">Jednak tego rodzaju instalacji jest możliwe określenie `useCRAN` jako hello pierwszego elementu obiektu pakietów hello listy, na przykład `useCRAN bitops, stringr, arules`.</span><span class="sxs-lookup"><span data-stu-id="61bd4-335">However this kind of install is possible by specifying `useCRAN` as hello first element of hello package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="61bd4-336">Niektóre pakiety R wymagają dodatkowych bibliotek systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="61bd4-336">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="61bd4-337">Dla wygody firma Microsoft wstępnie zainstalować zależności hello wymagane przez hello pierwszych 100 najpopularniejszych R pakietów.</span><span class="sxs-lookup"><span data-stu-id="61bd4-337">For convenience, we have pre-installed hello dependencies needed by hello top 100 most popular R packages.</span></span> <span data-ttu-id="61bd4-338">Jednak jeśli hello R pakiety, które będą instalowane wymagają bibliotek poza te następnie należy pobrać hello skryptu podstawowy używany w tym miejscu i dodać biblioteki systemu hello tooinstall czynności.</span><span class="sxs-lookup"><span data-stu-id="61bd4-338">However, if hello R package(s) you install require libraries beyond these then you must download hello base script used here and add steps tooinstall hello system libraries.</span></span> <span data-ttu-id="61bd4-339">Należy najpierw, a następnie przekazywania hello zmodyfikować skrypt tooa publicznego kontenera w magazynie Azure obiektów blob i korzystanie z pakietów hello tooinstall skryptu hello zmodyfikowane.</span><span class="sxs-lookup"><span data-stu-id="61bd4-339">You must then upload hello modified script tooa public blob container in Azure storage and use hello modified script tooinstall hello packages.</span></span>
   >    <span data-ttu-id="61bd4-340">Aby uzyskać informacje na temat tworzenia akcji skryptu, zobacz [Script Action development](hdinsight-hadoop-script-actions-linux.md) (Tworzenie akcji skryptu).</span><span class="sxs-lookup"><span data-stu-id="61bd4-340">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![Dodawanie akcji skryptu](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="61bd4-342">Wybierz **Utwórz** toorun hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="61bd4-342">Select **Create** toorun hello script.</span></span> <span data-ttu-id="61bd4-343">Po ukończeniu działania skryptu hello pakietów hello R są dostępne na wszystkich węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="61bd4-343">Once hello script completes, hello R packages are available on all worker nodes.</span></span>


## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="61bd4-344">Używanie funkcji opernacjonalizacji oprogramowania Microsoft R Server</span><span class="sxs-lookup"><span data-stu-id="61bd4-344">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="61bd4-345">Po zakończeniu Twojej modelowania danych, aby operacjonalizować hello modelu toomake prognoz.</span><span class="sxs-lookup"><span data-stu-id="61bd4-345">When your data modeling is complete, you can operationalize hello model toomake predictions.</span></span> <span data-ttu-id="61bd4-346">tooconfigure dla operationalization Microsoft R Server wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="61bd4-346">tooconfigure for Microsoft R Server operationalization, perform hello following steps:</span></span>

<span data-ttu-id="61bd4-347">Najpierw ssh do węzła krawędzi hello.</span><span class="sxs-lookup"><span data-stu-id="61bd4-347">First, ssh into hello Edge node.</span></span> <span data-ttu-id="61bd4-348">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="61bd4-348">For example,</span></span> 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="61bd4-349">Po użyciu ssh, zmień katalog dla wersji odpowiednich hello i sudo hello dotnet dll:</span><span class="sxs-lookup"><span data-stu-id="61bd4-349">After using ssh, change directory for hello relevant version and sudo hello dotnet dll:</span></span> 

- <span data-ttu-id="61bd4-350">W przypadku oprogramowania Microsoft R Server 9.1:</span><span class="sxs-lookup"><span data-stu-id="61bd4-350">For Microsoft R Server 9.1:</span></span>

    <span data-ttu-id="61bd4-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="61bd4-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span></span>

- <span data-ttu-id="61bd4-352">W przypadku oprogramowania Microsoft R Server 9.0:</span><span class="sxs-lookup"><span data-stu-id="61bd4-352">For Microsoft R Server 9.0:</span></span>

    <span data-ttu-id="61bd4-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="61bd4-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span></span>

<span data-ttu-id="61bd4-354">operationalization Microsoft R Server tooconfigure z konfiguracją jednego pola hello następujące:</span><span class="sxs-lookup"><span data-stu-id="61bd4-354">tooconfigure Microsoft R Server operationalization with a One-box configuration do hello following:</span></span>

1. <span data-ttu-id="61bd4-355">Wybierz pozycję „Configure R Server for Operationalization” (Konfiguruj oprogramowanie R Server pod kątem operacjonalizacji)</span><span class="sxs-lookup"><span data-stu-id="61bd4-355">Select “Configure R Server for Operationalization”</span></span>
2. <span data-ttu-id="61bd4-356">Wybierz pozycję „A.</span><span class="sxs-lookup"><span data-stu-id="61bd4-356">Select “A.</span></span> <span data-ttu-id="61bd4-357">One-box (web + compute nodes)” (Jedna maszyna — sieć Web i węzły obliczeniowe)</span><span class="sxs-lookup"><span data-stu-id="61bd4-357">One-box (web + compute nodes)”</span></span>
3. <span data-ttu-id="61bd4-358">Wprowadź hasło dla hello **admin** użytkownika</span><span class="sxs-lookup"><span data-stu-id="61bd4-358">Enter a password for hello **admin** user</span></span>

![opernacjonalizacja przy użyciu jednej maszyny](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="61bd4-360">Opcjonalnie możesz wykonać kontrolę diagnostyczną, uruchamiając test diagnostyczny w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="61bd4-360">As an optional step you can perform Diagnostic checks by running a diagnostic test as follows:</span></span>

1. <span data-ttu-id="61bd4-361">Wybierz pozycję „6.</span><span class="sxs-lookup"><span data-stu-id="61bd4-361">Select “6.</span></span> <span data-ttu-id="61bd4-362">Run diagnostic tests” (Uruchom testy diagnostyczne)</span><span class="sxs-lookup"><span data-stu-id="61bd4-362">Run diagnostic tests”</span></span>
2. <span data-ttu-id="61bd4-363">Wybierz pozycję „A.</span><span class="sxs-lookup"><span data-stu-id="61bd4-363">Select “A.</span></span> <span data-ttu-id="61bd4-364">Test configuration” (Testuj konfigurację)</span><span class="sxs-lookup"><span data-stu-id="61bd4-364">Test configuration”</span></span>
3. <span data-ttu-id="61bd4-365">Wpisz ciąg Username = “admin” i hasło określone w poprzednim kroku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="61bd4-365">Enter Username = “admin” and password from previous configuration step</span></span>
4. <span data-ttu-id="61bd4-366">Potwierdź wynik: Overall Health = pass (Ogólna kondycja — dobra)</span><span class="sxs-lookup"><span data-stu-id="61bd4-366">Confirm Overall Health = pass</span></span>
5. <span data-ttu-id="61bd4-367">Administrator narzędzie hello zakończenia</span><span class="sxs-lookup"><span data-stu-id="61bd4-367">Exit hello Admin Utility</span></span>
6. <span data-ttu-id="61bd4-368">Zamknij połączenie SSH</span><span class="sxs-lookup"><span data-stu-id="61bd4-368">Exit SSH</span></span>

![Diagnostyka opernacjonalizacji](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
><span data-ttu-id="61bd4-370">**Duże opóźnienia podczas używania usługi internetowej na platformie Spark**</span><span class="sxs-lookup"><span data-stu-id="61bd4-370">**Long delays when consuming web service on Spark**</span></span>
>
><span data-ttu-id="61bd4-371">Jeśli wystąpią duże opóźnienia podczas próby tooconsume usługi sieci web utworzone za pomocą funkcji mrsdeploy w kontekście obliczeń Spark, może być konieczne tooadd niektórych Brak folderów.</span><span class="sxs-lookup"><span data-stu-id="61bd4-371">If you encounter long delays when trying tooconsume a web service created with mrsdeploy functions in a Spark compute context, you may need tooadd some missing folders.</span></span> <span data-ttu-id="61bd4-372">Witaj aplikacji Spark należy tooa użytkownika o nazwie "*rserve2*" zawsze, gdy jest wywoływana z usługi sieci web przy użyciu funkcji mrsdeploy.</span><span class="sxs-lookup"><span data-stu-id="61bd4-372">hello Spark application belongs tooa user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="61bd4-373">toowork uniknąć tego problemu:</span><span class="sxs-lookup"><span data-stu-id="61bd4-373">toowork around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="61bd4-374">Na tym etapie hello Konfiguracja Operationalization jest pełny.</span><span class="sxs-lookup"><span data-stu-id="61bd4-374">At this stage, hello configuration for Operationalization is complete.</span></span> <span data-ttu-id="61bd4-375">Teraz można używać mrsdeploy"hello" pakiet w Twojej toohello tooconnect RClient Operationalization węzła krawędzi i rozpocząć korzystanie z jej funkcje, takie jak [zdalne wykonywanie kodu](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) i [usług sieci web](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span><span class="sxs-lookup"><span data-stu-id="61bd4-375">Now you can use hello ‘mrsdeploy’ package on your RClient tooconnect toohello Operationalization on edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="61bd4-376">W zależności od tego, czy klastra jest skonfigurowana w sieci wirtualnej lub nie może być konieczne tooset zapasowej portu do przodu tunelowania przez logowania SSH.</span><span class="sxs-lookup"><span data-stu-id="61bd4-376">Depending on whether your cluster is set up on a virtual network or not, you may need tooset up port forward tunneling through SSH login.</span></span> <span data-ttu-id="61bd4-377">Witaj poniższe sekcje zawierają opis sposobu tooset się ten tunel.</span><span class="sxs-lookup"><span data-stu-id="61bd4-377">hello following sections explain how tooset up this tunnel.</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="61bd4-378">Klaster oprogramowania RServer w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="61bd4-378">RServer Cluster on virtual network</span></span>

<span data-ttu-id="61bd4-379">Upewnij się, że można zezwolić na ruch przez port 12800 toohello węzłem krawędzi.</span><span class="sxs-lookup"><span data-stu-id="61bd4-379">Make sure you allow traffic through port 12800 toohello edge node.</span></span> <span data-ttu-id="61bd4-380">Dzięki temu funkcja hello krawędzi węzła tooconnect toohello Operationalization.</span><span class="sxs-lookup"><span data-stu-id="61bd4-380">That way, you can use hello edge node tooconnect toohello Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="61bd4-381">Jeśli hello `remoteLogin()` nie może połączyć się z węzłem krawędzi toohello, ale można węzła krawędzi toohello SSH, a następnie należy tooverify czy hello reguły tooallow ruch na porcie 12800 został ustawiony prawidłowo lub nie.</span><span class="sxs-lookup"><span data-stu-id="61bd4-381">If hello `remoteLogin()` cannot connect toohello edge node, but you can SSH toohello edge node, then you need tooverify whether hello rule tooallow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="61bd4-382">Jeśli będziesz kontynuować tooface hello problem, możesz można obejść, poprzez ustawienie portu do przodu tunelowania za pośrednictwem protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="61bd4-382">If you continue tooface hello issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="61bd4-383">Aby uzyskać instrukcje Zobacz hello następujących sekcji.</span><span class="sxs-lookup"><span data-stu-id="61bd4-383">For instructions, see hello following section.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="61bd4-384">Klaster oprogramowania RServer w sieci niewirtualnej</span><span class="sxs-lookup"><span data-stu-id="61bd4-384">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="61bd4-385">Jeśli klaster nie jest skonfigurowany w sieci wirtualnej lub występują problemy z korzystaniem z sieci wirtualnej, możesz użyć tunelowania przekierowania portów za pomocą protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="61bd4-385">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="61bd4-386">W programie Putty także możesz je skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="61bd4-386">On Putty, you can set it up as well.</span></span>

![połączenie ssh w programie putty](./media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="61bd4-388">Po aktywnej sesji SSH hello z tego komputera, portu 12800 przekazywane są węzłem krawędzi toohello portu 12800 za pośrednictwem sesji SSH.</span><span class="sxs-lookup"><span data-stu-id="61bd4-388">Once your SSH session is active, hello traffic from your machine’s port 12800 is forwarded toohello edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="61bd4-389">Upewnij się, że w metodzie `remoteLogin()` użyto adresu `127.0.0.1:12800`.</span><span class="sxs-lookup"><span data-stu-id="61bd4-389">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="61bd4-390">Loguje operationalization węzłem krawędzi toohello za pomocą przekierowania portów.</span><span class="sxs-lookup"><span data-stu-id="61bd4-390">This logs in toohello edge node’s operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="61bd4-391">Jak tooscale Microsoft R Server Operationalization obliczeniowe węzłów w usłudze HDInsight węzłów procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="61bd4-391">How tooscale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes</span></span>

### <a name="decommission-hello-worker-nodes"></a><span data-ttu-id="61bd4-392">Likwidowanie hello węzłów procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="61bd4-392">Decommission hello worker node(s)</span></span>

<span data-ttu-id="61bd4-393">Oprogramowanie Microsoft R Server nie jest aktualnie zarządzane za pomocą usługi Yarn.</span><span class="sxs-lookup"><span data-stu-id="61bd4-393">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="61bd4-394">Jeśli hello węzłów procesu roboczego nie są wycofany z eksploatacji, hello Yarn Menedżera zasobów nie będzie działać zgodnie z oczekiwaniami, ponieważ nie będą świadomi hello zasobów zostanie pobrana przez powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="61bd4-394">If hello worker nodes are not decommissioned, hello Yarn Resource Manager will not work as expected because it will not be aware of hello resources being taken up by hello server.</span></span> <span data-ttu-id="61bd4-395">W kolejności tooavoid tej sytuacji, firma Microsoft zaleca likwidowania węzłów procesu roboczego hello przed skalowanie węzłów obliczeniowych hello.</span><span class="sxs-lookup"><span data-stu-id="61bd4-395">In order tooavoid this situation, we recommend decommissioning hello worker nodes before you scale out hello compute nodes.</span></span>

<span data-ttu-id="61bd4-396">Kroki toodecommissioning węzłów procesu roboczego:</span><span class="sxs-lookup"><span data-stu-id="61bd4-396">Steps toodecommissioning worker nodes:</span></span>

* <span data-ttu-id="61bd4-397">Zaloguj się w konsoli narzędzia Ambari tooHDI klastra i kliknij na karcie "hostów"</span><span class="sxs-lookup"><span data-stu-id="61bd4-397">Log in tooHDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="61bd4-398">Wybierz węzłów procesu roboczego (toobe zlikwidowana), kliknij pozycję "Akcje" > "Wybrane hosty" > "Hostów" > kliknij "Włącz ON konserwacji tryb".</span><span class="sxs-lookup"><span data-stu-id="61bd4-398">Select worker nodes (toobe decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="61bd4-399">Na przykład w następujących obraz powitania Wybraliśmy toodecommission wn3 i wn4.</span><span class="sxs-lookup"><span data-stu-id="61bd4-399">For example, in hello following image we have selected wn3 and wn4 toodecommission.</span></span>  

   ![likwidowanie węzłów procesu roboczego](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="61bd4-401">Wybierz pozycję **Actions** > **Selected Hosts** > **DataNodes** (Akcje > Wybrane hosty > Węzły danych) i kliknij pozycję **Decommission** (Likwiduj)</span><span class="sxs-lookup"><span data-stu-id="61bd4-401">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**</span></span>
* <span data-ttu-id="61bd4-402">Wybierz pozycję **Actions** > **Selected Hosts** > **NodeManagers** (Akcje > Wybrane hosty > Menedżerowie węzła) i kliknij pozycję **Decommission** (Likwiduj)</span><span class="sxs-lookup"><span data-stu-id="61bd4-402">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**</span></span>
* <span data-ttu-id="61bd4-403">Wybierz pozycję **Actions** > **Selected Hosts** > **DataNodes** (Akcje > Wybrane hosty > Węzły danych) i kliknij pozycję **Stop** (Zatrzymaj)</span><span class="sxs-lookup"><span data-stu-id="61bd4-403">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**</span></span>
* <span data-ttu-id="61bd4-404">Wybierz pozycję **Actions** > **Selected Hosts** > **NodeManagers** (Akcje > Wybrane hosty > Menedżerowie węzła) i kliknij pozycję **Stop** (Zatrzymaj)</span><span class="sxs-lookup"><span data-stu-id="61bd4-404">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**</span></span>
* <span data-ttu-id="61bd4-405">Wybierz pozycję **Actions** > **Selected Hosts** > **Hosts** (Akcje > Wybrane hosty > Hosty) i kliknij pozycję **Stop All Components** (Zatrzymaj wszystkie składniki)</span><span class="sxs-lookup"><span data-stu-id="61bd4-405">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**</span></span>
* <span data-ttu-id="61bd4-406">Usuń zaznaczenie hello węzłów procesu roboczego, a następnie wybierz hello węzłów głównych</span><span class="sxs-lookup"><span data-stu-id="61bd4-406">Unselect hello worker nodes and select hello head nodes</span></span>
* <span data-ttu-id="61bd4-407">Wybierz pozycję **Actions** > **Selected Hosts** > **Hosts** > **Restart All Components** (Akcje > Wybrane hosty > Hosty > Uruchom ponownie wszystkie składniki)</span><span class="sxs-lookup"><span data-stu-id="61bd4-407">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**</span></span>

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="61bd4-408">Konfigurowanie węzłów obliczeniowych na wszystkich zlikwidowanych węzłach procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="61bd4-408">Configure Compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="61bd4-409">Za pomocą protokołu SSH połącz się z każdym zlikwidowanym węzłem procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="61bd4-409">SSH into each decommissioned worker node.</span></span>
2. <span data-ttu-id="61bd4-410">Uruchom narzędzie administracyjne za pomocą polecenia `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span><span class="sxs-lookup"><span data-stu-id="61bd4-410">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span></span>
3. <span data-ttu-id="61bd4-411">Wprowadź "1" tooselect opcję "Konfiguruj dla Operationalization serwera R".</span><span class="sxs-lookup"><span data-stu-id="61bd4-411">Enter "1" tooselect option "Configure R Server for Operationalization".</span></span>
4. <span data-ttu-id="61bd4-412">Wybierz opcję "c" tooselect "C.</span><span class="sxs-lookup"><span data-stu-id="61bd4-412">Enter "c" tooselect option "C.</span></span> <span data-ttu-id="61bd4-413">Compute node” (Węzeł obliczeniowy).</span><span class="sxs-lookup"><span data-stu-id="61bd4-413">Compute node".</span></span> <span data-ttu-id="61bd4-414">Spowoduje to skonfigurowanie węzeł obliczeniowy hello na powitania węzła procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="61bd4-414">This configures hello compute node on hello worker node.</span></span>
5. <span data-ttu-id="61bd4-415">Administrator narzędzie hello zakończenia.</span><span class="sxs-lookup"><span data-stu-id="61bd4-415">Exit hello Admin Utility.</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="61bd4-416">Dodawanie szczegółów węzłów obliczeniowych na węźle sieci Web</span><span class="sxs-lookup"><span data-stu-id="61bd4-416">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="61bd4-417">Po skonfigurowaniu wszystkich węzłów procesu roboczego wycofany z eksploatacji toorun węzła obliczeniowego, wróć na węzeł brzegowy hello i dodać węzłów procesu roboczego wycofany z eksploatacji adresów IP w konfiguracji węzła hello R serwera sieci web:</span><span class="sxs-lookup"><span data-stu-id="61bd4-417">Once all decommissioned worker nodes have been configured toorun compute node, come back on hello edge node and add decommissioned worker nodes' IP addresses in hello Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="61bd4-418">SSH do węzła krawędzi hello.</span><span class="sxs-lookup"><span data-stu-id="61bd4-418">SSH into hello edge node.</span></span>
* <span data-ttu-id="61bd4-419">Uruchom polecenie `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="61bd4-419">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>
* <span data-ttu-id="61bd4-420">Wyszukaj sekcję "URI" hello i Dodaj IP węzła procesu roboczego i Szczegóły portu.</span><span class="sxs-lookup"><span data-stu-id="61bd4-420">Look for hello "URIs" section, and add worker node's IP and port details.</span></span>

    ![wiersz polecenia likwidowania węzłów procesu roboczego](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a><span data-ttu-id="61bd4-422">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="61bd4-422">Troubleshoot</span></span>

<span data-ttu-id="61bd4-423">W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="61bd4-423">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>


## <a name="next-steps"></a><span data-ttu-id="61bd4-424">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="61bd4-424">Next steps</span></span>

<span data-ttu-id="61bd4-425">Teraz należy zrozumieć, jak toocreate nowego klastra usługi HDInsight, który obejmuje hello R Server i hello posługiwać się hello konsoli R w sesji SSH.</span><span class="sxs-lookup"><span data-stu-id="61bd4-425">Now you should understand how toocreate a new HDInsight cluster that includes hello R Server and hello basics of using hello R console from an SSH session.</span></span> <span data-ttu-id="61bd4-426">Witaj poniższych tematach opisano inne sposoby zarządzania i Praca z serwerem R w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="61bd4-426">hello following topics explain other ways of managing and working with R Server on HDInsight:</span></span>

* [<span data-ttu-id="61bd4-427">Dodaj serwer programu RStudio tooHDInsight (Jeśli nie zainstalowano podczas tworzenia klastra)</span><span class="sxs-lookup"><span data-stu-id="61bd4-427">Add RStudio Server tooHDInsight (if not installed during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* <span data-ttu-id="61bd4-428">[Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md) (Opcje kontekstu obliczeniowego dla oprogramowania R Server w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="61bd4-428">[Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md)</span></span>
* <span data-ttu-id="61bd4-429">[Azure Storage options for R Server on HDInsight](hdinsight-hadoop-r-server-storage.md) (Opcje usługi Azure Storage dla oprogramowania R Server w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="61bd4-429">[Azure Storage options for R Server on HDInsight](hdinsight-hadoop-r-server-storage.md)</span></span>
