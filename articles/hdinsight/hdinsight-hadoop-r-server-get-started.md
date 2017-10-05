---
title: "Wprowadzenie do oprogramowania R Server w usłudze HDInsight — platforma Azure | Microsoft Docs"
description: "Dowiedz się, jak utworzyć aparat Apache Spark w klastrze usługi HDInsight zawierającym oprogramowanie R Server, a następnie jak przesłać skrypt języka R do klastra."
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
ms.openlocfilehash: 14e2a14c74e00709e18a80325fbdd3cbcd71da37
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="31195-103">Wprowadzenie do korzystania z oprogramowania R Server w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="31195-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="31195-104">Usługa HDInsight obejmuje opcję oprogramowania R Server, którą można zintegrować z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31195-104">HDInsight includes an R Server option to be integrated into your HDInsight cluster.</span></span> <span data-ttu-id="31195-105">Opcja ta pozwala skryptom języka R używać aparatu Spark i funkcji MapReduce do wykonywania obliczeń rozproszonych.</span><span class="sxs-lookup"><span data-stu-id="31195-105">This option allows R scripts to use Spark and MapReduce to run distributed computations.</span></span> <span data-ttu-id="31195-106">Ten dokument umożliwia poznanie procedury tworzenia oprogramowania R Server w klastrze usługi HDInsight, a następnie uruchamiania skryptu R, który demonstruje sposób użycia aparatu Spark na potrzeby wykonywania rozproszonych obliczeń przez kod R.</span><span class="sxs-lookup"><span data-stu-id="31195-106">In this document, you learn how to create an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="31195-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="31195-107">Prerequisites</span></span>

* <span data-ttu-id="31195-108">**Subskrypcja platformy Azure**: przed rozpoczęciem tego samouczka musisz mieć subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="31195-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="31195-109">Aby uzyskać więcej informacji, przejdź do artykułu [Get Microsoft Azure free trial (Uzyskaj bezpłatną wersję próbną platformy Azure)](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="31195-109">Go to the article [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="31195-110">**Klient protokołu Secure Shell (SSH)**: klient SSH jest używany do zdalnego łączenia z klastrem usługi HDInsight i uruchamiania poleceń bezpośrednio w klastrze.</span><span class="sxs-lookup"><span data-stu-id="31195-110">**A Secure Shell (SSH) client**: An SSH client is used to remotely connect to the HDInsight cluster and run commands directly on the cluster.</span></span> <span data-ttu-id="31195-111">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="31195-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="31195-112">**Klucze SSH (opcjonalnie)**: konto SSH użyte do nawiązania połączenia z klastrem można zabezpieczyć przy użyciu hasła lub klucza publicznego.</span><span class="sxs-lookup"><span data-stu-id="31195-112">**SSH keys (optional)**: You can secure the SSH account used to connect to the cluster using either a password or a public key.</span></span> <span data-ttu-id="31195-113">Użycie hasła jest łatwiejsze i umożliwia rozpoczęcie pracy bez konieczności tworzenia pary kluczy publiczny-prywatny.</span><span class="sxs-lookup"><span data-stu-id="31195-113">Using a password is easier, and allows you to get started without having to create a public/private key pair.</span></span> <span data-ttu-id="31195-114">Jednak użycie klucza jest bezpieczniejsze.</span><span class="sxs-lookup"><span data-stu-id="31195-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="31195-115">W krokach przedstawionych w tym dokumencie przyjęto założenie, że jest używane hasło.</span><span class="sxs-lookup"><span data-stu-id="31195-115">The steps in this document assume that you are using a password.</span></span>


## <a name="automated-cluster-creation"></a><span data-ttu-id="31195-116">Zautomatyzowane tworzenie klastra</span><span class="sxs-lookup"><span data-stu-id="31195-116">Automated cluster creation</span></span>

<span data-ttu-id="31195-117">Aby zautomatyzować tworzenie serwerów HDInsight R Server, możesz użyć szablonów usługi Azure Resource Manager, zestawu SDK oraz programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31195-117">You can automate the creation of HDInsight R Servers using Azure Resource Manager templates, the SDK, and also PowerShell.</span></span>

* <span data-ttu-id="31195-118">Aby utworzyć serwer R Server za pomocą szablonu usługi Azure Resource Management, zobacz [Deploy an R server HDInsight cluster (Wdrażanie klastra usługi HDInsight serwera R Server)](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span><span class="sxs-lookup"><span data-stu-id="31195-118">To create an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="31195-119">Aby utworzyć serwer R Server za pomocą zestawu .NET SDK, zobacz [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) (Tworzenie klastrów opartych na systemie Linux w usłudze HDInsight przy użyciu zestawu .NET SDK).</span><span class="sxs-lookup"><span data-stu-id="31195-119">To create an R Server using the .NET SDK, see [create Linux-based clusters in HDInsight using the .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="31195-120">Aby wdrożyć serwer R Server za pomocą programu PowerShell, zobacz artykuł [Creating an R Server on HDInsight with PowerShell (Tworzenie serwera R Server w usłudze HDInsight przy użyciu programu PowerShell)](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="31195-120">To deploy R Server using powershell, see the article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-the-cluster-using-the-azure-portal"></a><span data-ttu-id="31195-121">Tworzenie klastra przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="31195-121">Create the cluster using the Azure portal</span></span>

1. <span data-ttu-id="31195-122">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31195-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="31195-123">Wybierz pozycję **Nowy** -> **Rozwiązania inteligentne + analiza** -> **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="31195-123">Select **NEW** -> **Intelligence + Analytics**, -> **HDInsight**.</span></span>

    ![Obraz tworzenia nowego klastra](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. <span data-ttu-id="31195-125">W środowisku **Szybkie tworzenie** podaj nazwę klastra w polu **Nazwa klastra**.</span><span class="sxs-lookup"><span data-stu-id="31195-125">In the **Quick create** experience, enter a name for the cluster in the **Cluster Name** field.</span></span> <span data-ttu-id="31195-126">Jeśli masz wiele subskrypcji platformy Azure, użyj pozycji **Subskrypcja**, aby wybrać subskrypcję do użycia.</span><span class="sxs-lookup"><span data-stu-id="31195-126">If you have multiple Azure subscriptions, use the **Subscription** entry to select the one you want to use.</span></span>

    ![Wybór nazwy klastra i subskrypcji](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. <span data-ttu-id="31195-128">Wybierz pozycję **Typ klastra**, aby otworzyć blok **Konfiguracja klastra**.</span><span class="sxs-lookup"><span data-stu-id="31195-128">Select **Cluster type** to open the **Cluster configuration** blade.</span></span> <span data-ttu-id="31195-129">W bloku **Konfiguracja klastra** wybierz następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="31195-129">On the **Cluster Configuration** blade, select the following options:</span></span>

    * <span data-ttu-id="31195-130">**Typ klastra**: R Server</span><span class="sxs-lookup"><span data-stu-id="31195-130">**Cluster Type**: R Server</span></span>
    * <span data-ttu-id="31195-131">**Wersja**: wybierz wersję oprogramowania R Server do zainstalowania w klastrze.</span><span class="sxs-lookup"><span data-stu-id="31195-131">**Version**: select the version of R Server to install on the cluster.</span></span> <span data-ttu-id="31195-132">Aktualnie dostępna jest wersja ***R Server 9.1 (HDI 3.6)***.</span><span class="sxs-lookup"><span data-stu-id="31195-132">The version currently available is ***R Server 9.1 (HDI 3.6)***.</span></span> <span data-ttu-id="31195-133">Informacje o wersji dotyczące dostępnych wersji oprogramowania R Server można znaleźć [tutaj](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span><span class="sxs-lookup"><span data-stu-id="31195-133">Release notes for the available versions of R Server are available [here](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span></span>
    * <span data-ttu-id="31195-134">**Program R Studio Community Edition for R Server**: to środowisko IDE oparte na przeglądarce, które jest instalowane domyślnie w węźle krawędzi.</span><span class="sxs-lookup"><span data-stu-id="31195-134">**R Studio community edition for R Server**: this browser-based IDE is installed by default on the edge node.</span></span> <span data-ttu-id="31195-135">Jeśli nie chcesz go instalować, usuń zaznaczenie pola wyboru.</span><span class="sxs-lookup"><span data-stu-id="31195-135">If you would prefer to not have it installed, then uncheck the check box.</span></span> <span data-ttu-id="31195-136">Jeśli wybierzesz opcję instalacji, adres URL umożliwiający logowanie do programu RStudio Server będzie dostępny w bloku aplikacji portalu dla utworzonego klastra.</span><span class="sxs-lookup"><span data-stu-id="31195-136">If you choose to have it installed, the URL for accessing the RStudio Server login is found on a portal application blade for your cluster once it’s been created.</span></span>
    * <span data-ttu-id="31195-137">Pozostaw wartości domyślne innych opcji i użyj przycisku **Wybierz**, aby zapisać typ klastra.</span><span class="sxs-lookup"><span data-stu-id="31195-137">Leave the other options at the default values and use the **Select** button to save the cluster type.</span></span>

        ![Zrzut ekranu bloku typu klastra](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. <span data-ttu-id="31195-139">Podaj wartości w pozycjach **Nazwa użytkownika logowania klastra** i **Hasło logowania klastra**.</span><span class="sxs-lookup"><span data-stu-id="31195-139">Enter a **Cluster login username** and **Cluster login password**.</span></span>

    <span data-ttu-id="31195-140">Określ wartość w pozycji **Nazwa użytkownika SSH**.</span><span class="sxs-lookup"><span data-stu-id="31195-140">Specify an **SSH Username**.</span></span> <span data-ttu-id="31195-141">Protokół SSH jest używany do zdalnego łączenia z klastrem przy użyciu klienta protokołu **Secure Shell (SSH)**.</span><span class="sxs-lookup"><span data-stu-id="31195-141">SSH is used to remotely connect to the cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="31195-142">Użytkownika SSH można określić w tym oknie dialogowym lub po utworzeniu klastra (na karcie Konfiguracja klastra).</span><span class="sxs-lookup"><span data-stu-id="31195-142">You can either specify the SSH user in this dialog or after the cluster has been created (in the Configuration tab for the cluster).</span></span> <span data-ttu-id="31195-143">Oprogramowanie R Server jest skonfigurowane pod kątem użycia **nazwy użytkownika SSH** „remoteuser”.</span><span class="sxs-lookup"><span data-stu-id="31195-143">R Server is configured to expect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="31195-144">**Jeśli używasz innej nazwy użytkownika, musisz wykonać dodatkowy krok po utworzeniu klastra.**</span><span class="sxs-lookup"><span data-stu-id="31195-144">**If you use a different username, you must perform an additional step after the cluster is created.**</span></span>

    <span data-ttu-id="31195-145">Pozostaw zaznaczone pole **Użyj tego samego hasła podczas logowania do klastra**, aby użyć typu uwierzytelniania **HASŁO**, chyba że wolisz użyć klucza publicznego.</span><span class="sxs-lookup"><span data-stu-id="31195-145">Leave the box checked for **Use same password as cluster login** to use **PASSWORD** as the authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="31195-146">Jeśli planujesz uzyskiwanie dostępu do oprogramowania R Server w klastrze za pomocą zdalnego klienta, na przykład programu RTVS, RStudio lub innego komputerowego środowiska IDE, będzie potrzebna para kluczy publiczny-prywatny.</span><span class="sxs-lookup"><span data-stu-id="31195-146">You need a public/private key pair to access R Server on the cluster via a remote client as, for example, RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="31195-147">W przypadku instalowania programu RStudio Server Community Edition, musisz wybrać hasło SSH.</span><span class="sxs-lookup"><span data-stu-id="31195-147">If you install the RStudio Server community edition, you need to choose an SSH password.</span></span>     

    <span data-ttu-id="31195-148">Aby utworzyć parę kluczy publiczny-prywatny, usuń zaznaczenie pola **Użyj tego samego hasła podczas logowania do klastra**, a następnie wybierz typ uwierzytelniania **KLUCZ PUBLICZNY** i kontynuuj w podany poniżej sposób.</span><span class="sxs-lookup"><span data-stu-id="31195-148">To create and use a public/private key pair, uncheck **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span> <span data-ttu-id="31195-149">W poniższych instrukcjach przyjęto, że jest zainstalowane środowisko Cygwin z programem ssh-keygen lub równoważnym.</span><span class="sxs-lookup"><span data-stu-id="31195-149">These instructions assume that you have Cygwin with ssh-keygen or an equivalent installed.</span></span>

    * <span data-ttu-id="31195-150">Wygeneruj parę kluczy publiczny-prywatny w wierszu polecenia na komputerze przenośnym:</span><span class="sxs-lookup"><span data-stu-id="31195-150">Generate a public/private key pair from the command prompt on your laptop:</span></span>

        <span data-ttu-id="31195-151">ssh-keygen -t rsa -b 2048</span><span class="sxs-lookup"><span data-stu-id="31195-151">ssh-keygen -t rsa -b 2048</span></span>

    * <span data-ttu-id="31195-152">Podaj nazwę pliku klucza po wyświetleniu monitu, a następnie określ hasło, aby podwyższyć poziom zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="31195-152">Follow the prompt to name a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="31195-153">Ekran powinien wyglądać podobnie do następującego:</span><span class="sxs-lookup"><span data-stu-id="31195-153">Your screen should look something like the following image:</span></span>

        ![Wiersz polecenia SSH w systemie Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * <span data-ttu-id="31195-155">Polecenie to pozwala utworzyć plik klucza prywatnego i plik klucza publicznego o nazwie <nazwa-pliku-klucza-prywatnego>.pub, na przykład furiosa i furiosa.pub.</span><span class="sxs-lookup"><span data-stu-id="31195-155">This command creates a private key file and a public key file under the name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

        ![Katalog polecenia SSH](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * <span data-ttu-id="31195-157">Następnie określ plik klucza publicznego (&#42;.pub) podczas przypisywania poświadczeń klastra usługi HDI oraz potwierdź grupę zasobów i region, po czym wybierz pozycję **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="31195-157">Then specify the public key file (&#42;.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**.</span></span>

        ![Blok poświadczeń](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * <span data-ttu-id="31195-159">Zmień uprawnienia do pliku klucza prywatnego na komputerze przenośnym:</span><span class="sxs-lookup"><span data-stu-id="31195-159">Change permissions on the private keyfile on your laptop:</span></span>

        <span data-ttu-id="31195-160">chmod 600 <nazwa-pliku-klucza-prywatnego></span><span class="sxs-lookup"><span data-stu-id="31195-160">chmod 600 <private-key-filename></span></span>

   * <span data-ttu-id="31195-161">Użyj pliku klucza prywatnego do zdalnego logowania za pomocą protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="31195-161">Use the private key file with SSH for remote login:</span></span>

        <span data-ttu-id="31195-162">ssh –i <nazwa-pliku-klucza-prywatnego> remoteuser@<hostname public ip></span><span class="sxs-lookup"><span data-stu-id="31195-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span></span>

      <span data-ttu-id="31195-163">lub jako części definicji kontekstu obliczeniowego aparatu Spark usługi Hadoop dla oprogramowania R Server na kliencie.</span><span class="sxs-lookup"><span data-stu-id="31195-163">Or, as part the definition of your Hadoop Spark compute context for R Server on the client.</span></span> <span data-ttu-id="31195-164">Zobacz podsekcję **Using Microsoft R Server as a Hadoop Client (Używanie oprogramowania Microsoft R Server jako klienta usługi Hadoop)** tematu [Create a Compute Context for Spark (Tworzenie kontekstu obliczeniowego dla aparatu Spark)](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span><span class="sxs-lookup"><span data-stu-id="31195-164">See the **Using Microsoft R Server as a Hadoop Client** subsection in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span></span>

6. <span data-ttu-id="31195-165">Funkcja szybkiego tworzenia przeniesie Cię do bloku **Magazyn**, aby umożliwić wybranie ustawień konta magazynu do użycia dla lokalizacji głównej systemu plików HDFS używanego przez klaster.</span><span class="sxs-lookup"><span data-stu-id="31195-165">The quick create transitions you to the **Storage** blade to select the storage account settings to be used for the primary location of the HDFS file system used by the cluster.</span></span> <span data-ttu-id="31195-166">Wybierz nowe lub istniejące konto usługi Azure Storage lub istniejące konto usługi Data Lake Storage.</span><span class="sxs-lookup"><span data-stu-id="31195-166">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

    - <span data-ttu-id="31195-167">Jeśli wybierzesz konto usługi Microsoft Azure Storage, możesz wskazać istniejące konto magazynu, wybierając pozycję **Wybierz konto magazynu**, a następnie wybierając odpowiednie konto.</span><span class="sxs-lookup"><span data-stu-id="31195-167">If you select an Azure Storage account, an existing storage account is selected by choosing **Select a storage account** and then selecting the relevant account.</span></span> <span data-ttu-id="31195-168">Aby utworzyć nowe konto, użyj linku **Utwórz nowe** w sekcji **Wybierz konto magazynu**.</span><span class="sxs-lookup"><span data-stu-id="31195-168">Create a new account using the **Create New** link in the **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="31195-169">Jeśli wybierzesz pozycję **Nowe**, musisz podać nazwę nowego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="31195-169">If you select **New** you must enter a name for the new storage account.</span></span> <span data-ttu-id="31195-170">Jeśli nazwa zostanie zaakceptowana, pojawi się zielony znacznik.</span><span class="sxs-lookup"><span data-stu-id="31195-170">A green check appears if the name is accepted.</span></span>

      <span data-ttu-id="31195-171">Domyślną wartością pola **Kontener domyślny** jest nazwa klastra.</span><span class="sxs-lookup"><span data-stu-id="31195-171">The **Default Container** defaults to the name of the cluster.</span></span> <span data-ttu-id="31195-172">Nie zmieniaj tej wartości.</span><span class="sxs-lookup"><span data-stu-id="31195-172">Leave this default as the value.</span></span>

      <span data-ttu-id="31195-173">Jeśli wybrano opcję nowego konta magazynu, zostanie wyświetlony monit o określenie wartości **Lokalizacja** umożliwiającej wskazanie regionu, w którym ma zostać utworzone konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="31195-173">If a new storage account option was selected a prompt to select **Location** is given to select which region to create the storage account.</span></span>  

         ![Blok źródła danych](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="31195-175">Wybranie lokalizacji domyślnego źródła danych spowoduje także ustawienie lokalizacji klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31195-175">Selecting the location for the default data source  also sets the location of the HDInsight cluster.</span></span> <span data-ttu-id="31195-176">Klaster i domyślne źródło danych muszą znajdować się w tym samym regionie.</span><span class="sxs-lookup"><span data-stu-id="31195-176">The cluster and default data source must be in the same region.</span></span>

    - <span data-ttu-id="31195-177">Jeśli chcesz użyć istniejącej usługi Data Lake Store, wybierz konto magazynu usługi ADLS, które ma być używane, i dodaj tożsamość usługi *ADD* klastra do klastra, aby umożliwić dostęp do magazynu.</span><span class="sxs-lookup"><span data-stu-id="31195-177">If you want to use an existing Data Lake Store, then select the ADLS storage account to use and add the cluster *ADD* identity to your cluster to allow access to the store.</span></span> <span data-ttu-id="31195-178">Aby uzyskać więcej informacji na temat tego procesu, zobacz [Tworzenie klastra HDInsight z usługą Data Lake Store za pomocą witryny Azure Portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span><span class="sxs-lookup"><span data-stu-id="31195-178">For more information on this process, see [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

    <span data-ttu-id="31195-179">Użyj przycisku **Wybierz**, aby zapisać konfigurację źródła danych.</span><span class="sxs-lookup"><span data-stu-id="31195-179">Use the **Select** button to save the data source configuration.</span></span>


7. <span data-ttu-id="31195-180">Zostanie wyświetlony blok **Podsumowanie**, w którym można zweryfikować wszystkie ustawienia.</span><span class="sxs-lookup"><span data-stu-id="31195-180">The **Summary** blade then displays to validate all your settings.</span></span> <span data-ttu-id="31195-181">W tym miejscu możesz zmienić wartość pozycji **Rozmiar klastra** w celu zmodyfikowania liczby serwerów w klastrze, a także określić wartość pozycji **Akcje skryptu** definiującej skrypty do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="31195-181">Here you can change your **Cluster size** to modify the number of servers in your cluster and also specify any **Script actions** you want to run.</span></span> <span data-ttu-id="31195-182">Pozostaw domyślną liczbę węzłów procesu roboczego — `4`, chyba że wiesz, że potrzebujesz większego klastra.</span><span class="sxs-lookup"><span data-stu-id="31195-182">Unless you know that you need a larger cluster, leave the number of worker nodes at the default of `4`.</span></span> <span data-ttu-id="31195-183">Szacowany koszt klastra zostanie pokazany w bloku.</span><span class="sxs-lookup"><span data-stu-id="31195-183">The estimated cost of the cluster is shown within the blade.</span></span>

    ![podsumowanie klastra](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="31195-185">W razie potrzeby możesz później zmienić rozmiar klastra w witrynie Portal (**Klaster** -> **Ustawienia** -> **Skaluj klaster**), aby zwiększyć lub zmniejszyć liczbę węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="31195-185">If needed, you can resize your cluster later through the Portal (**Cluster** -> **Settings** -> **Scale Cluster**) to increase or decrease the number of worker nodes.</span></span>  <span data-ttu-id="31195-186">Zmiana rozmiaru może być przydatna do zmniejszenia klastra, gdy nie jest on używany, lub zwiększenia mocy obliczeniowej w celu spełnienia wymagań bardziej zaawansowanych zadań.</span><span class="sxs-lookup"><span data-stu-id="31195-186">This resizing can be useful for idling down the cluster when not in use, or for adding capacity to meet the needs of larger tasks.</span></span>
   >
   >

   <span data-ttu-id="31195-187">Podczas zmiany rozmiaru klastra, węzłów danych i węzła krawędzi należy uwzględnić pewne czynniki:</span><span class="sxs-lookup"><span data-stu-id="31195-187">Some factors to keep in mind when sizing your cluster, the data nodes, and the edge node include:</span></span>  

   * <span data-ttu-id="31195-188">Wydajność rozproszonych analiz wykonywanych za pomocą aparatu Spark w oprogramowaniu R Server jest proporcjonalna do liczby węzłów procesu roboczego, jeśli danych jest dużo.</span><span class="sxs-lookup"><span data-stu-id="31195-188">The performance of distributed R Server analyses on Spark is proportional to the number of worker nodes when the data is large.</span></span>  

   * <span data-ttu-id="31195-189">Wydajność analiz oprogramowania R Server jest liniowa w stosunku do rozmiaru analizowanych danych.</span><span class="sxs-lookup"><span data-stu-id="31195-189">The performance of R Server analyses is linear in the size of data being analyzed.</span></span> <span data-ttu-id="31195-190">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="31195-190">For example:</span></span>  

     * <span data-ttu-id="31195-191">Dla małych i średnich ilości danych wydajność jest najwyższa w przypadku analizowania w lokalnym kontekście obliczeniowym w węźle krawędzi.</span><span class="sxs-lookup"><span data-stu-id="31195-191">For small to modest data, performance is best when analyzed in a local compute context on the edge node.</span></span>  <span data-ttu-id="31195-192">Aby uzyskać więcej informacji na temat scenariuszy, w których lokalne konteksty obliczeniowe i konteksty obliczeniowe aparatu Spark działają najlepiej, zobacz Compute context options for R Server on HDInsight (Opcje kontekstu obliczeniowego dla oprogramowania R Server w usłudze HDInsight).</span><span class="sxs-lookup"><span data-stu-id="31195-192">For more information on the scenarios under which the local and Spark compute contexts work best, see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="31195-193">Jeśli zalogujesz się do węzła krawędzi i uruchomisz skrypt języka R, wszystkie funkcje poza funkcjami rx programu ScaleR zostaną uruchomione <strong>lokalnie</strong> w węźle krawędzi.</span><span class="sxs-lookup"><span data-stu-id="31195-193">If you log in to the edge node and run your R script, then all but the ScaleR rx-functions are executed <strong>locally</strong> on the edge node.</span></span> <span data-ttu-id="31195-194">Z tego względu musisz odpowiednio dostosować wielkość pamięci i liczbę rdzeni węzła krawędzi.</span><span class="sxs-lookup"><span data-stu-id="31195-194">So the memory and number of cores of the edge node should be sized accordingly.</span></span> <span data-ttu-id="31195-195">To samo dotyczy sytuacji, w której oprogramowanie R Server w usłudze HDI jest używane z komputera przenośnego jako zdalny kontekst obliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="31195-195">The same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![Blok warstw cenowych węzła](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     <span data-ttu-id="31195-197">Użyj przycisku **Wybierz**, aby zapisać konfigurację cen węzła.</span><span class="sxs-lookup"><span data-stu-id="31195-197">Use the **Select** button to save the node pricing configuration.</span></span>

   <span data-ttu-id="31195-198">Dostępny jest również link **Pobierz szablon i parametry**.</span><span class="sxs-lookup"><span data-stu-id="31195-198">There is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="31195-199">Kliknięcie tego linku spowoduje wyświetlenie skryptów, których można użyć do zautomatyzowania tworzenia klastra z wybraną konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="31195-199">Click on this link to display scripts that can be used to automate the creation of a cluster with the selected configuration.</span></span> <span data-ttu-id="31195-200">Te skrypty są także dostępne z pozycji Azure Portal dla klastra po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="31195-200">These scripts are also available from the Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="31195-201">Tworzenie klastra zajmuje trochę czasu, zwykle około 20 minut.</span><span class="sxs-lookup"><span data-stu-id="31195-201">It takes some time for the cluster to be created, usually around 20 minutes.</span></span> <span data-ttu-id="31195-202">Użyj kafelka na tablicy startowej lub pozycji **Powiadomienia** w lewej części strony, aby sprawdzić postęp procesu tworzenia.</span><span class="sxs-lookup"><span data-stu-id="31195-202">Use the tile on the Startboard, or the **Notifications** entry on the left of the page to check on the creation process.</span></span>
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-to-rstudio-server"></a><span data-ttu-id="31195-203">Łączenie z programem RStudio Server</span><span class="sxs-lookup"><span data-stu-id="31195-203">Connect to RStudio Server</span></span>

<span data-ttu-id="31195-204">Jeśli wybrano opcję instalacji programu RStudio Server Community Edition, można się do niego zalogować na dwa sposoby.</span><span class="sxs-lookup"><span data-stu-id="31195-204">If you’ve chosen to include RStudio Server community edition in your installation, then you can access the RStudio login via two different methods.</span></span>

1. <span data-ttu-id="31195-205">Przejdź do następującego adresu URL (gdzie **NAZWA-KLASTRA** to nazwa utworzonego klastra):</span><span class="sxs-lookup"><span data-stu-id="31195-205">Go to the following URL (where **CLUSTERNAME** is the name of the cluster you've created):</span></span>

    <span data-ttu-id="31195-206">https://**NAZWA-KLASTRA**.azurehdinsight.net/rstudio/</span><span class="sxs-lookup"><span data-stu-id="31195-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="31195-207">Otwórz pozycję klastra w witrynie Azure Portal, wybierz szybki link **Pulpity nawigacyjne oprogramowania R Server**, a następnie wybierz **pulpit nawigacyjny programu R Studio**:</span><span class="sxs-lookup"><span data-stu-id="31195-207">Open the entry for your cluster in the Azure portal, select the **R Server Dashboards** quick link and then selecting the **R Studio Dashboard**:</span></span>

     ![Dostęp do pulpitu nawigacyjnego programu R Studio](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Dostęp do pulpitu nawigacyjnego programu R Studio](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="31195-210">Niezależnie od wybranej metody, pierwsze logowanie wymaga dwukrotnego uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="31195-210">Regardless of the method used, the first time you log in you need to authenticate twice.</span></span>  <span data-ttu-id="31195-211">Podczas pierwszego uwierzytelniania podaj *identyfikator użytkownika administratora klastra* i *hasło*.</span><span class="sxs-lookup"><span data-stu-id="31195-211">At the first authentication, provide the *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="31195-212">Przy drugim monicie podaj *identyfikator użytkownika SSH* i *hasło*.</span><span class="sxs-lookup"><span data-stu-id="31195-212">At the second prompt, provide the *SSH userid* and *password*.</span></span> <span data-ttu-id="31195-213">Podczas kolejnych logowań będą wymagane tylko *hasło SSH* oraz *identyfikator użytkownika*.</span><span class="sxs-lookup"><span data-stu-id="31195-213">Subsequent log ins only require the *SSH password* and *userid*.</span></span>

<a name="connect-to-edge-node"></a>
## <a name="connect-to-the-r-server-edge-node"></a><span data-ttu-id="31195-214">Łączenie z węzłem krawędzi oprogramowania R Server</span><span class="sxs-lookup"><span data-stu-id="31195-214">Connect to the R Server edge node</span></span>

<span data-ttu-id="31195-215">Następujące polecenie umożliwia połączenie się z węzłem krawędzi oprogramowania R Server klastra usługi HDInsight za pomocą protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="31195-215">Connect to R Server edge node of the HDInsight cluster using SSH with the command:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="31195-216">Adres `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` jest także dostępny w witrynie Azure Portal po wybraniu klastra, a następnie pozycji **Wszystkie ustawienia** -> **Aplikacje** -> **RServer**.</span><span class="sxs-lookup"><span data-stu-id="31195-216">You can find the `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in the Azure portal by selecting your cluster then **All Settings** -> **Apps** -> **RServer**.</span></span> <span data-ttu-id="31195-217">Spowoduje to wyświetlenie informacji o punkcie końcowym SSH dla węzła krawędzi.</span><span class="sxs-lookup"><span data-stu-id="31195-217">This displays the SSH Endpoint information for the edge node.</span></span>
>
> ![Obraz punktu końcowego SSH dla węzła krawędzi](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

<span data-ttu-id="31195-219">Jeśli do zabezpieczenia konta użytkownika SSH użyto hasła, zostanie wyświetlony monit o jego wprowadzenie.</span><span class="sxs-lookup"><span data-stu-id="31195-219">If you used a password to secure your SSH user account, you are prompted to enter it.</span></span> <span data-ttu-id="31195-220">Jeśli używasz klucza publicznego, może być konieczne użycie parametru `-i` w celu określenia zgodnego klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="31195-220">If you used a public key, you may have to use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="31195-221">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="31195-221">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="31195-222">Aby uzyskać więcej informacji, zobacz [Łączenie się z usługą HDInsight (Hadoop) przy użyciu protokołu SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="31195-222">For more information, see [Connect to HDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="31195-223">Po nawiązaniu połączenia zostanie wyświetlony monit podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="31195-223">Once connected, you arrive at a prompt similar to the following:</span></span>

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="31195-224">Włączanie obsługi równoczesnych użytkowników</span><span class="sxs-lookup"><span data-stu-id="31195-224">Enable multiple concurrent users</span></span>

<span data-ttu-id="31195-225">Można umożliwić jednoczesną pracę wielu użytkowników, dodając użytkowników do węzła krawędzi, na którym jest uruchomiony program RStudio Community.</span><span class="sxs-lookup"><span data-stu-id="31195-225">You can enable multiple concurrent users by adding more users for the edge node on which the RStudio community version runs.</span></span>

<span data-ttu-id="31195-226">Podczas tworzenia klastra usługi HDInsight musisz podać dwóch użytkowników: użytkownika HTTP i użytkownika SSH:</span><span class="sxs-lookup"><span data-stu-id="31195-226">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![Równoczesny użytkownik 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- <span data-ttu-id="31195-228">**Nazwa użytkownika logowania klastra**: użytkownik HTTP uwierzytelniany za pośrednictwem bramy HDInsight, która umożliwia ochronę utworzonych klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31195-228">**Cluster login username**: an HTTP user for authentication through the HDInsight gateway that is used to protect the HDInsight clusters you created.</span></span> <span data-ttu-id="31195-229">Przy pomocy użytkownika HTTP można uzyskiwać dostęp do interfejsu użytkownika Ambari lub YARN oraz innych składników interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="31195-229">This HTTP user is used to access the Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="31195-230">**Nazwa użytkownika protokołu SSH (Secure Shell)**: użytkownik SSH zapewniający dostęp do klastra za pośrednictwem protokołu Secure Shell.</span><span class="sxs-lookup"><span data-stu-id="31195-230">**Secure Shell (SSH) username**: an SSH user to access the cluster through secure shell.</span></span> <span data-ttu-id="31195-231">Jest to użytkownik systemu Linux, który ma dostęp do wszystkich węzłów głównych, węzłów procesu roboczego oraz węzłów krawędzi.</span><span class="sxs-lookup"><span data-stu-id="31195-231">This user is a user in the Linux system for all the head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="31195-232">Pozwala to na korzystanie z dowolnego węzła klastra zdalnego za pomocą protokołu Secure Shell.</span><span class="sxs-lookup"><span data-stu-id="31195-232">So you can use secure shell to access any of the nodes in a remote cluster.</span></span>

<span data-ttu-id="31195-233">W mechanizmie logowania wersji programu R Studio Server Community używanej na serwerze Microsoft R Server w klastrze typu HDInsight są akceptowane tylko nazwa użytkownika i hasło systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="31195-233">The R Studio Server Community version used in the Microsoft R Server on HDInsight type cluster accepts only Linux username and password as a login mechanism.</span></span> <span data-ttu-id="31195-234">Przekazywanie tokenów nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="31195-234">It does not support passing tokens.</span></span> <span data-ttu-id="31195-235">Jeśli chcesz użyć programu R Studio do uzyskania dostępu do nowo utworzonego klastra, musisz zalogować się dwukrotnie.</span><span class="sxs-lookup"><span data-stu-id="31195-235">So if you have created a new cluster and want to use R Studio to access it, you need to log in twice.</span></span>

- <span data-ttu-id="31195-236">Najpierw zaloguj się przy użyciu poświadczeń użytkownika HTTP za pośrednictwem bramy usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="31195-236">First log in using the HTTP user credentials through the HDInsight Gateway:</span></span> 

    ![Równoczesny użytkownik 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- <span data-ttu-id="31195-238">Następnie zaloguj się do programu RStudio przy użyciu poświadczeń użytkownika SSH:</span><span class="sxs-lookup"><span data-stu-id="31195-238">Then use the SSH user credentials to log in to RStudio:</span></span>
  
    ![Równoczesny użytkownik 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

<span data-ttu-id="31195-240">Aktualnie podczas aprowizowania klastra usługi HDInsight można utworzyć tylko jedno konto użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="31195-240">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="31195-241">Dlatego aby umożliwić wielu użytkownikom dostęp do serwera Microsoft R Server w klastrach usługi HDInsight, należy utworzyć dodatkowych użytkowników w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="31195-241">So to enable multiple users to access Microsoft R Server on HDInsight clusters, we need to create additional users in the Linux system.</span></span>

<span data-ttu-id="31195-242">Ponieważ program RStudio Server Community działa w węźle krawędzi klastra, wymagane jest wykonanie kilku czynności:</span><span class="sxs-lookup"><span data-stu-id="31195-242">Because RStudio Server Community is running on the cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="31195-243">Zaloguj się do węzła krawędzi przy użyciu poświadczeń utworzonego użytkownika SSH</span><span class="sxs-lookup"><span data-stu-id="31195-243">Use the created SSH user to log in to the edge node</span></span>
2. <span data-ttu-id="31195-244">Dodaj użytkowników systemu Linux w węźle krawędzi</span><span class="sxs-lookup"><span data-stu-id="31195-244">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="31195-245">Przy pomocy utworzonego użytkownika możesz korzystać z programu RStudio Community</span><span class="sxs-lookup"><span data-stu-id="31195-245">Use RStudio Community version with the user created</span></span>

### <a name="step-1-use-the-created-ssh-user-to-log-in-to-the-edge-node"></a><span data-ttu-id="31195-246">Krok 1. Logowanie do węzła krawędzi przy użyciu poświadczeń utworzonego użytkownika SSH</span><span class="sxs-lookup"><span data-stu-id="31195-246">Step 1: Use the created SSH user to log in to the edge node</span></span>

<span data-ttu-id="31195-247">Pobierz dowolne narzędzie SSH (takie jak Putty) i zaloguj się za pomocą istniejącego konta użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="31195-247">Download any SSH tool (such as Putty) and use the existing SSH user to log in.</span></span> <span data-ttu-id="31195-248">Aby uzyskać dostęp do węzła krawędzi, postępuj zgodnie z instrukcjami podanymi w temacie [Łączenie się z usługą HDInsight (Hadoop) przy użyciu protokołu SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="31195-248">Then follow the instructions provided in [Connect to HDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md) to access the edge node.</span></span> <span data-ttu-id="31195-249">Adres węzła krawędzi serwera R Server w klastrze usługi HDInsight to: *nazwa_klastra-ed-ssh.azurehdinsight.net*</span><span class="sxs-lookup"><span data-stu-id="31195-249">The edge node address for R Server on HDInsight cluster is: *clustername-ed-ssh.azurehdinsight.net*</span></span>


### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="31195-250">Krok 2. Dodawanie użytkowników systemu Linux w węźle krawędzi</span><span class="sxs-lookup"><span data-stu-id="31195-250">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="31195-251">Aby dodać użytkownika do węzła krawędzi, uruchom te polecenia:</span><span class="sxs-lookup"><span data-stu-id="31195-251">To add a user to the edge node, execute the commands:</span></span>

    sudo useradd yournewusername -m
    sudo passwd yourusername

<span data-ttu-id="31195-252">Powinny zostać zwrócone następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="31195-252">You should see the following items returned:</span></span> 

![Równoczesny użytkownik 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

<span data-ttu-id="31195-254">Gdy pojawi się monit o podanie bieżącego hasła protokołu Kerberos, po prostu go zignoruj, naciskając klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="31195-254">When prompted for “Current Kerberos password:”, just press **Enter** to ignore it.</span></span> <span data-ttu-id="31195-255">Podanie opcji `-m` w poleceniu `useradd` powoduje, że system utworzy folder macierzysty użytkownika, wymagany przez program RStudio Community.</span><span class="sxs-lookup"><span data-stu-id="31195-255">The `-m` option in `useradd` command indicates that the system will create a home folder for the user, which is required for RStudio Community version.</span></span>


### <a name="step-3-use-rstudio-community-version-with-the-user-created"></a><span data-ttu-id="31195-256">Krok 3. Korzystanie z programu RStudio Community przy pomocy utworzonego użytkownika</span><span class="sxs-lookup"><span data-stu-id="31195-256">Step 3: Use RStudio Community version with the user created</span></span>

<span data-ttu-id="31195-257">Zaloguj się do programu RStudio przy użyciu utworzonego konta użytkownika:</span><span class="sxs-lookup"><span data-stu-id="31195-257">Use the user created to log in to RStudio:</span></span>

![Równoczesny użytkownik 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

<span data-ttu-id="31195-259">Zwróć uwagę na to, że program RStudio wyświetla informację, że do logowania się w klastrze jest używane nowe konto użytkownika (w tym przypadku *sshuser6*):</span><span class="sxs-lookup"><span data-stu-id="31195-259">Notice that RStudio indicates that you are using the new user (here, for example, *sshuser6*) to log in the cluster:</span></span> 

![Równoczesny użytkownik 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

<span data-ttu-id="31195-261">Jednocześnie w innym oknie przeglądarki możesz także zalogować się przy użyciu oryginalnych poświadczeń (domyślnie: *sshuser*).</span><span class="sxs-lookup"><span data-stu-id="31195-261">You can also log in using the original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="31195-262">Zadania można przesyłać za pomocą funkcji programu ScaleR.</span><span class="sxs-lookup"><span data-stu-id="31195-262">You can submit a job using scaleR functions.</span></span> <span data-ttu-id="31195-263">Oto przykładowe polecenia służące do uruchamiania zadania:</span><span class="sxs-lookup"><span data-stu-id="31195-263">Here is an example of the commands used to run a job:</span></span>

    # Set the HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data to the tmp folder.
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

    # Set directory in bigDataDirRoot to load the data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create the directory.
    rxHadoopMakeDir(inputDir)

    # Copy the data from source to input.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define the HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for the airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all the column names.
    varNames <- names(airlineColInfo)

    # Define the text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define the text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify the formula to use.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define the Spark compute context.
    mySparkCluster <- RxSpark()

    # Set the compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


<span data-ttu-id="31195-264">Zwróć uwagę, że przesłane zadania mają inne nazwy użytkowników w interfejsie użytkownika YARN:</span><span class="sxs-lookup"><span data-stu-id="31195-264">Notice that the jobs submitted are under different user names in YARN UI:</span></span>

![Równoczesny użytkownik 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

<span data-ttu-id="31195-266">Pamiętaj, że nowo dodani użytkownicy nie mają uprawnień użytkownika root w systemie Linux, ale mają takie same prawa dostępu do wszystkich plików w magazynie zdalnym HDFS i WASB.</span><span class="sxs-lookup"><span data-stu-id="31195-266">Note also that the newly added users do not have root privileges in Linux system, but they do have the same access to all the files in the remote HDFS and WASB storage.</span></span>


<a name="use-r-console"></a>
## <a name="use-the-r-console"></a><span data-ttu-id="31195-267">Użycie konsoli R</span><span class="sxs-lookup"><span data-stu-id="31195-267">Use the R console</span></span>

1. <span data-ttu-id="31195-268">W sesji SSH wpisz następujące polecenie, aby uruchomić konsolę R:</span><span class="sxs-lookup"><span data-stu-id="31195-268">From the SSH session, use the following command to start the R console:</span></span>  

        R

2. <span data-ttu-id="31195-269">Powinny zostać wyświetlone dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="31195-269">You should see output similar to the following:</span></span>
    
    <span data-ttu-id="31195-270">R version 3.2.2 (2015-08-14) — "Fire Safety"  Copyright (C) 2015 The R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span><span class="sxs-lookup"><span data-stu-id="31195-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 The R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span></span>

    <span data-ttu-id="31195-271">Bezpłatne oprogramowanie R jest dostarczane BEZ ŻADNEJ GWARANCJI.</span><span class="sxs-lookup"><span data-stu-id="31195-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span></span>
    <span data-ttu-id="31195-272">Zachęcamy do jego rozpowszechniania pod pewnymi warunkami.</span><span class="sxs-lookup"><span data-stu-id="31195-272">You are welcome to redistribute it under certain conditions.</span></span>
    <span data-ttu-id="31195-273">Wpisz „license()” lub „licence()”, aby uzyskać szczegółowe informacje o dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="31195-273">Type 'license()' or 'licence()' for distribution details.</span></span>

    <span data-ttu-id="31195-274">Oprogramowanie obsługuje język naturalny, ale z angielskimi ustawieniami regionalnymi.</span><span class="sxs-lookup"><span data-stu-id="31195-274">Natural language support but running in an English locale</span></span>

    <span data-ttu-id="31195-275">R jest projektem zbiorowym, zrzeszającym wielu uczestników.</span><span class="sxs-lookup"><span data-stu-id="31195-275">R is a collaborative project with many contributors.</span></span>
    <span data-ttu-id="31195-276">Aby uzyskać więcej informacji, wpisz „contributors()”. Aby wyświetlić wskazówki dotyczące wskazywania elementów lub pakietów platformy R, wpisz „citation()”.</span><span class="sxs-lookup"><span data-stu-id="31195-276">Type 'contributors()' for more information and 'citation()' on how to cite R or R packages in publications.</span></span>

    <span data-ttu-id="31195-277">Za pomocą polecenia „demo()” można wyświetlić prezentacje. Polecenie „help()” umożliwia uzyskanie pomocy online. Aby wyświetlić pomoc w przeglądarce z interfejsem HTML, wpisz „help.start()”.</span><span class="sxs-lookup"><span data-stu-id="31195-277">Type 'demo()' for some demos, 'help()' for on-line help, or 'help.start()' for an HTML browser interface to help.</span></span>
    <span data-ttu-id="31195-278">Aby zamknąć środowisko R, wpisz „q()”.</span><span class="sxs-lookup"><span data-stu-id="31195-278">Type 'q()' to quit R.</span></span>

    <span data-ttu-id="31195-279">Oprogramowanie Microsoft R Server w wersji 8.0: rozszerzona dystrybucja pakietów R firmy Microsoft. Copyright (C) 2016 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="31195-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span></span>

    <span data-ttu-id="31195-280">Aby uzyskać informacje o wersji, wpisz „readme()”.</span><span class="sxs-lookup"><span data-stu-id="31195-280">Type 'readme()' for release notes.</span></span>
    >

3. <span data-ttu-id="31195-281">W monicie `>` możesz podać kod R.</span><span class="sxs-lookup"><span data-stu-id="31195-281">From the `>` prompt, you can enter R code.</span></span> <span data-ttu-id="31195-282">Oprogramowanie R Server zawiera pakiety, które umożliwiają łatwą współpracę z usługą Hadoop i uruchamianie rozproszonych obliczeń.</span><span class="sxs-lookup"><span data-stu-id="31195-282">R server includes packages that allow you to easily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="31195-283">Na przykład następujące polecenie umożliwia wyświetlenie katalogu głównego domyślnego systemu plików klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="31195-283">For example, use the following command to view the root of the default file system for the HDInsight cluster:</span></span>

    <span data-ttu-id="31195-284">rxHadoopListFiles("/")</span><span class="sxs-lookup"><span data-stu-id="31195-284">rxHadoopListFiles("/")</span></span>

4. <span data-ttu-id="31195-285">Dostępne jest także adresowanie w stylu WASB.</span><span class="sxs-lookup"><span data-stu-id="31195-285">You can also use the WASB style addressing.</span></span>

    <span data-ttu-id="31195-286">rxHadoopListFiles("wasb:///")</span><span class="sxs-lookup"><span data-stu-id="31195-286">rxHadoopListFiles("wasb:///")</span></span>


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="31195-287">Używanie oprogramowania R Server w usłudze HDI ze zdalnego wystąpienia oprogramowania Microsoft R Server lub programu Microsoft R Client</span><span class="sxs-lookup"><span data-stu-id="31195-287">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="31195-288">Możliwe jest skonfigurowanie dostępu do kontekstu obliczeniowego aparatu Spark usługi Hadoop w usłudze HDI ze zdalnego wystąpienia programu Microsoft R Server lub programu Microsoft R Client uruchomionego na komputerze stacjonarnym lub przenośnym.</span><span class="sxs-lookup"><span data-stu-id="31195-288">It is possible to set up access to the HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop.</span></span> <span data-ttu-id="31195-289">Zobacz podsekcję **Using Microsoft R Server as a Hadoop Client (Używanie oprogramowania Microsoft R Server jako klienta usługi Hadoop)** tematu [Create a Compute Context for Spark (Tworzenie kontekstu obliczeniowego dla aparatu Spark)](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="31195-289">See **Using Microsoft R Server as a Hadoop Client** subsection in the [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span></span> <span data-ttu-id="31195-290">W tym celu należy określić następujące opcje podczas definiowania kontekstu obliczeniowego programu RxSpark na komputerze przenośnym: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches i sshProfileScript.</span><span class="sxs-lookup"><span data-stu-id="31195-290">To do so, you need to specify the following options when defining the RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="31195-291">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="31195-291">For example:</span></span>


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


## <a name="use-a-compute-context"></a><span data-ttu-id="31195-292">Używanie kontekstu obliczeniowego</span><span class="sxs-lookup"><span data-stu-id="31195-292">Use a compute context</span></span>

<span data-ttu-id="31195-293">Kontekst obliczeniowy pozwala określić, czy obliczenia są wykonywane lokalnie w węźle krawędzi czy są rozproszone w węzłach klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31195-293">A compute context allows you to control whether computation is performed locally on the edge node or distributed across the nodes in the HDInsight cluster.</span></span>

1. <span data-ttu-id="31195-294">W programie RStudio Server lub konsoli R (w ramach sesji SSH) załaduj przykładowe dane do domyślnego magazynu usługi HDInsight za pomocą następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="31195-294">From RStudio Server or the R console (in an SSH session), use the following code to load example data into the default storage for HDInsight:</span></span>

        # Set the HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data to the tmp folder
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

        # Set directory in bigDataDirRoot to load the data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make the directory
        rxHadoopMakeDir(inputDir)

        # Copy the data from source to input
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. <span data-ttu-id="31195-295">Następnie utwórzmy trochę informacji o danych i zdefiniujmy dwa źródła danych, aby umożliwić pracę z danymi.</span><span class="sxs-lookup"><span data-stu-id="31195-295">Next, let's create some data info and define two data sources so that we can work with the data.</span></span>

        # Define the HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for the airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all the column names
        varNames <- names(airlineColInfo)

        # Define the text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define the text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula to use
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. <span data-ttu-id="31195-296">Przeprowadźmy regresję logistyczną na danych za pomocą lokalnego kontekstu obliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="31195-296">Let's run a logistic regression over the data using the local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="31195-297">Powinny zostać wyświetlone dane wyjściowe kończące się wierszami podobnymi do następujących:</span><span class="sxs-lookup"><span data-stu-id="31195-297">You should see output that ends with lines similar to the following:</span></span>

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

4. <span data-ttu-id="31195-298">Następnie przeprowadźmy tę samą regresję logistyczną za pomocą kontekstu aparatu Spark.</span><span class="sxs-lookup"><span data-stu-id="31195-298">Next, let's run the same logistic regression using the Spark context.</span></span> <span data-ttu-id="31195-299">Dzięki kontekstowi aparatu Spark przetwarzanie jest dystrybuowane do wszystkich węzłów procesu roboczego w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31195-299">The Spark context distributes the processing over all the worker nodes in the HDInsight cluster.</span></span>

        # Define the Spark compute context
        mySparkCluster <- RxSpark()

        # Set the compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > <span data-ttu-id="31195-300">Możesz także użyć funkcji MapReduce do rozproszenia obliczeń na węzłach klastra.</span><span class="sxs-lookup"><span data-stu-id="31195-300">You can also use MapReduce to distribute computation across cluster nodes.</span></span> <span data-ttu-id="31195-301">Aby uzyskać więcej informacji na temat kontekstu obliczeniowego, zobacz [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md) (Opcje kontekstu obliczeniowego dla oprogramowania R Server w usłudze HDInsight).</span><span class="sxs-lookup"><span data-stu-id="31195-301">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-to-multiple-nodes"></a><span data-ttu-id="31195-302">Dystrybucja kodu R do wielu węzłów</span><span class="sxs-lookup"><span data-stu-id="31195-302">Distribute R code to multiple nodes</span></span>

<span data-ttu-id="31195-303">Przy użyciu oprogramowania R Server możesz w łatwy sposób uruchomić istniejący kod R w wielu węzłach klastra za pomocą programu `rxExec`.</span><span class="sxs-lookup"><span data-stu-id="31195-303">With R Server, you can easily take existing R code and run it across multiple nodes in the cluster by using `rxExec`.</span></span> <span data-ttu-id="31195-304">Funkcja ta jest przydatna podczas czyszczenia parametrów lub przeprowadzania symulacji.</span><span class="sxs-lookup"><span data-stu-id="31195-304">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="31195-305">Poniższy kod przedstawia przykładowe użycie programu `rxExec`:</span><span class="sxs-lookup"><span data-stu-id="31195-305">The following code is an example of how to use `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="31195-306">Jeśli nadal używasz kontekstu Spark lub MapReduce, uruchomienie tego polecenia spowoduje zwrócenie wartości nodename dla węzłów procesu roboczego, w których uruchomiono kod `(Sys.info()["nodename"])`.</span><span class="sxs-lookup"><span data-stu-id="31195-306">If you are still using the Spark or MapReduce context, this  command returns the nodename value for the worker nodes that the code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="31195-307">Na przykład w przypadku klastra składającego się z czterech węzłów dane wyjściowe mogą być podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="31195-307">For example, on a four node cluster, you expect to receive output similar to the following:</span></span>

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


## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="31195-308">Dostęp do danych w usługach Hive i Parquet</span><span class="sxs-lookup"><span data-stu-id="31195-308">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="31195-309">Funkcja dostępna w oprogramowaniu R Server 9.1 umożliwia bezpośredni dostęp do danych w usługach Hive i Parquet w celu użycia ich w funkcjach programu ScaleR w kontekście obliczeniowym aparatu Spark.</span><span class="sxs-lookup"><span data-stu-id="31195-309">A feature available in R Server 9.1 allows direct access to data in Hive and Parquet for use by ScaleR functions in the Spark compute context.</span></span> <span data-ttu-id="31195-310">Te możliwości są dostępne za pomocą nowych funkcji źródła danych programu ScaleR o nazwie RxHiveData i RxParquetData, które używają kodu Spark SQL do ładowania danych bezpośrednio do elementów DataFrame aparatu Spark na potrzeby analizy przez program ScaleR.</span><span class="sxs-lookup"><span data-stu-id="31195-310">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL to load data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="31195-311">Poniżej przedstawiono przykładowy kod korzystający z nowych funkcji:</span><span class="sxs-lookup"><span data-stu-id="31195-311">The following code provides some sample code on use of the new functions:</span></span>

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

    #Check on Spark data objects, cleanup, and close the Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


<span data-ttu-id="31195-312">Dodatkowe informacje na temat używania tych nowych funkcji zawiera pomoc online oprogramowania R Server dostępna przy użyciu poleceń `?RxHivedata` i `?RxParquetData`.</span><span class="sxs-lookup"><span data-stu-id="31195-312">For additional info on use of these new functions see the online help in R Server through use of the `?RxHivedata` and `?RxParquetData` commands.</span></span>  


## <a name="install-additional-r-packages-on-the-edge-node"></a><span data-ttu-id="31195-313">Instalowanie dodatkowych pakietów R w węźle krawędzi</span><span class="sxs-lookup"><span data-stu-id="31195-313">Install additional R packages on the edge node</span></span>

<span data-ttu-id="31195-314">Jeśli chcesz zainstalować dodatkowe pakiety R na węźle krawędzi, możesz użyć polecenia `install.packages()` bezpośrednio z konsoli R, gdy masz połączenie SSH z węzłem krawędzi.</span><span class="sxs-lookup"><span data-stu-id="31195-314">If you would like to install additional R packages on the edge node, you can use `install.packages()` directly from within the R console when connected to the edge node through SSH.</span></span> <span data-ttu-id="31195-315">Jednak jeśli potrzebujesz zainstalować pakiety R na węzłach procesu roboczego klastra, musisz użyć akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="31195-315">However, if you need to install R packages on the worker nodes of the cluster, you must use a Script Action.</span></span>

<span data-ttu-id="31195-316">Akcje skryptu to skrypty powłoki Bash używane do wprowadzania zmian w konfiguracji klastra usługi HDInsight lub instalowania dodatkowego oprogramowania, np. pakietów R.</span><span class="sxs-lookup"><span data-stu-id="31195-316">Script Actions are Bash scripts that are used to make configuration changes to the HDInsight cluster or to install additional software, such as additional R packages.</span></span> <span data-ttu-id="31195-317">Aby zainstalować dodatkowe pakiety przy użyciu akcji skryptu, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="31195-317">To install additional packages using a Script Action, use the following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31195-318">Dodatkowe pakiety R można zainstalować przy użyciu akcji skryptu dopiero po utworzeniu klastra.</span><span class="sxs-lookup"><span data-stu-id="31195-318">Using Script Actions to install additional R packages can only be used after the cluster has been created.</span></span> <span data-ttu-id="31195-319">Nie wykonuj tej procedury podczas tworzenia klastra, ponieważ skrypt wymaga w pełni zainstalowanego i skonfigurowanego oprogramowania R Server.</span><span class="sxs-lookup"><span data-stu-id="31195-319">Do not use this procedure during cluster creation, as the script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="31195-320">W witrynie [Azure Portal](https://portal.azure.com) wybierz oprogramowanie R Server lub klaster usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31195-320">From the [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="31195-321">W bloku **Ustawienia** wybierz pozycję **Akcje skryptu**, a następnie pozycję **Prześlij nową**, aby przesłać nową akcję skryptu.</span><span class="sxs-lookup"><span data-stu-id="31195-321">From the **Settings** blade, select **Script Actions** and then **Submit New** to submit a new Script Action.</span></span>

   ![Obraz bloku akcji skryptu](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. <span data-ttu-id="31195-323">W bloku **Prześlij akcję skryptu** podaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="31195-323">From the **Submit script action** blade, provide the following information:</span></span>

   * <span data-ttu-id="31195-324">**Nazwa**: przyjazna nazwa identyfikująca skrypt</span><span class="sxs-lookup"><span data-stu-id="31195-324">**Name**: A friendly name to identify this script</span></span>

   * <span data-ttu-id="31195-325">**Identyfikator URI skryptu powłoki systemowej**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="31195-325">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="31195-326">**Główny**: to pole powinno być **niezaznaczone**</span><span class="sxs-lookup"><span data-stu-id="31195-326">**Head**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="31195-327">**Proces roboczy**: to pole powinno być **zaznaczone**</span><span class="sxs-lookup"><span data-stu-id="31195-327">**Worker**: This item should be **checked**</span></span>

   * <span data-ttu-id="31195-328">**Węzły krawędzi**: to pole powinno być **niezaznaczone**</span><span class="sxs-lookup"><span data-stu-id="31195-328">**Edge nodes**: This item should be **unchecked**.</span></span>

   * <span data-ttu-id="31195-329">**Dozorca**: to pole powinno być **niezaznaczone**</span><span class="sxs-lookup"><span data-stu-id="31195-329">**Zookeeper**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="31195-330">**Parametry**: pakiety R do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="31195-330">**Parameters**: The R packages to be installed.</span></span> <span data-ttu-id="31195-331">Na przykład: `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="31195-331">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="31195-332">**Utrwal ten skrypt...**: to pole powinno być **zaznaczone**</span><span class="sxs-lookup"><span data-stu-id="31195-332">**Persist this script...**: This item should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="31195-333">Domyślnie wszystkie pakiety R są instalowane z migawki repozytorium Microsoft MRAN odpowiedniej do zainstalowanej wersji oprogramowania R Server.</span><span class="sxs-lookup"><span data-stu-id="31195-333">By default, all R packages are installed from a snapshot of the Microsoft MRAN repository consistent with the version of R Server that has been installed.</span></span> <span data-ttu-id="31195-334">Jeśli chcesz zainstalować nowsze wersje pakietów, musisz uwzględnić pewne ryzyko niezgodności.</span><span class="sxs-lookup"><span data-stu-id="31195-334">If you want to install newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="31195-335">Jednak możesz to zrobić za pomocą parametru `useCRAN` użytego jako pierwszy element listy pakietów, na przykład `useCRAN bitops, stringr, arules`.</span><span class="sxs-lookup"><span data-stu-id="31195-335">However this kind of install is possible by specifying `useCRAN` as the first element of the package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="31195-336">Niektóre pakiety R wymagają dodatkowych bibliotek systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="31195-336">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="31195-337">Dla Twojej wygody zainstalowaliśmy wstępnie wymagania dla 100 najpopularniejszych pakietów R.</span><span class="sxs-lookup"><span data-stu-id="31195-337">For convenience, we have pre-installed the dependencies needed by the top 100 most popular R packages.</span></span> <span data-ttu-id="31195-338">Jednak jeśli instalowane pakiety R wymagają jeszcze innych bibliotek, musisz pobrać skrypt podstawowy użyty tutaj i dodać kroki instalowania bibliotek systemowych.</span><span class="sxs-lookup"><span data-stu-id="31195-338">However, if the R package(s) you install require libraries beyond these then you must download the base script used here and add steps to install the system libraries.</span></span> <span data-ttu-id="31195-339">Następnie musisz przekazać zmodyfikowany skrypt do publicznego kontenera obiektów blob w usłudze Azure Storage i użyć zmodyfikowanego skryptu do zainstalowania pakietów.</span><span class="sxs-lookup"><span data-stu-id="31195-339">You must then upload the modified script to a public blob container in Azure storage and use the modified script to install the packages.</span></span>
   >    <span data-ttu-id="31195-340">Aby uzyskać informacje na temat tworzenia akcji skryptu, zobacz [Script Action development](hdinsight-hadoop-script-actions-linux.md) (Tworzenie akcji skryptu).</span><span class="sxs-lookup"><span data-stu-id="31195-340">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![Dodawanie akcji skryptu](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="31195-342">Wybierz polecenie **Utwórz**, aby uruchomić skrypt.</span><span class="sxs-lookup"><span data-stu-id="31195-342">Select **Create** to run the script.</span></span> <span data-ttu-id="31195-343">Po zakończeniu działania skryptu pakiety R będą dostępne we wszystkich węzłach procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="31195-343">Once the script completes, the R packages are available on all worker nodes.</span></span>


## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="31195-344">Używanie funkcji opernacjonalizacji oprogramowania Microsoft R Server</span><span class="sxs-lookup"><span data-stu-id="31195-344">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="31195-345">Po zakończeniu modelowania danych możesz zopernacjonalizować model, aby wykonywać prognozowanie.</span><span class="sxs-lookup"><span data-stu-id="31195-345">When your data modeling is complete, you can operationalize the model to make predictions.</span></span> <span data-ttu-id="31195-346">Aby skonfigurować funkcję operacjonalizacji oprogramowania Microsoft R Server, wykonaj poniższe kroki:</span><span class="sxs-lookup"><span data-stu-id="31195-346">To configure for Microsoft R Server operationalization, perform the following steps:</span></span>

<span data-ttu-id="31195-347">Nawiąż połączenie SSH z węzłem krawędzi.</span><span class="sxs-lookup"><span data-stu-id="31195-347">First, ssh into the Edge node.</span></span> <span data-ttu-id="31195-348">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="31195-348">For example,</span></span> 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="31195-349">Po nawiązaniu połączenia SSH zmień katalog dla odpowiedniej wersji i użyj polecenia sudo dla biblioteki dotnet dll:</span><span class="sxs-lookup"><span data-stu-id="31195-349">After using ssh, change directory for the relevant version and sudo the dotnet dll:</span></span> 

- <span data-ttu-id="31195-350">W przypadku oprogramowania Microsoft R Server 9.1:</span><span class="sxs-lookup"><span data-stu-id="31195-350">For Microsoft R Server 9.1:</span></span>

    <span data-ttu-id="31195-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="31195-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span></span>

- <span data-ttu-id="31195-352">W przypadku oprogramowania Microsoft R Server 9.0:</span><span class="sxs-lookup"><span data-stu-id="31195-352">For Microsoft R Server 9.0:</span></span>

    <span data-ttu-id="31195-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="31195-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span></span>

<span data-ttu-id="31195-354">Aby skonfigurować operacjonalizację oprogramowania Microsoft R Server pod kątem jednej maszyny, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="31195-354">To configure Microsoft R Server operationalization with a One-box configuration do the following:</span></span>

1. <span data-ttu-id="31195-355">Wybierz pozycję „Configure R Server for Operationalization” (Konfiguruj oprogramowanie R Server pod kątem operacjonalizacji)</span><span class="sxs-lookup"><span data-stu-id="31195-355">Select “Configure R Server for Operationalization”</span></span>
2. <span data-ttu-id="31195-356">Wybierz pozycję „A.</span><span class="sxs-lookup"><span data-stu-id="31195-356">Select “A.</span></span> <span data-ttu-id="31195-357">One-box (web + compute nodes)” (Jedna maszyna — sieć Web i węzły obliczeniowe)</span><span class="sxs-lookup"><span data-stu-id="31195-357">One-box (web + compute nodes)”</span></span>
3. <span data-ttu-id="31195-358">Podaj hasło dla **administratora**</span><span class="sxs-lookup"><span data-stu-id="31195-358">Enter a password for the **admin** user</span></span>

![opernacjonalizacja przy użyciu jednej maszyny](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="31195-360">Opcjonalnie możesz wykonać kontrolę diagnostyczną, uruchamiając test diagnostyczny w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="31195-360">As an optional step you can perform Diagnostic checks by running a diagnostic test as follows:</span></span>

1. <span data-ttu-id="31195-361">Wybierz pozycję „6.</span><span class="sxs-lookup"><span data-stu-id="31195-361">Select “6.</span></span> <span data-ttu-id="31195-362">Run diagnostic tests” (Uruchom testy diagnostyczne)</span><span class="sxs-lookup"><span data-stu-id="31195-362">Run diagnostic tests”</span></span>
2. <span data-ttu-id="31195-363">Wybierz pozycję „A.</span><span class="sxs-lookup"><span data-stu-id="31195-363">Select “A.</span></span> <span data-ttu-id="31195-364">Test configuration” (Testuj konfigurację)</span><span class="sxs-lookup"><span data-stu-id="31195-364">Test configuration”</span></span>
3. <span data-ttu-id="31195-365">Wpisz ciąg Username = “admin” i hasło określone w poprzednim kroku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="31195-365">Enter Username = “admin” and password from previous configuration step</span></span>
4. <span data-ttu-id="31195-366">Potwierdź wynik: Overall Health = pass (Ogólna kondycja — dobra)</span><span class="sxs-lookup"><span data-stu-id="31195-366">Confirm Overall Health = pass</span></span>
5. <span data-ttu-id="31195-367">Zamknij narzędzie administracyjne</span><span class="sxs-lookup"><span data-stu-id="31195-367">Exit the Admin Utility</span></span>
6. <span data-ttu-id="31195-368">Zamknij połączenie SSH</span><span class="sxs-lookup"><span data-stu-id="31195-368">Exit SSH</span></span>

![Diagnostyka opernacjonalizacji](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
><span data-ttu-id="31195-370">**Duże opóźnienia podczas używania usługi internetowej na platformie Spark**</span><span class="sxs-lookup"><span data-stu-id="31195-370">**Long delays when consuming web service on Spark**</span></span>
>
><span data-ttu-id="31195-371">Jeśli wystąpią duże opóźnienia podczas próby korzystania z usługi internetowej utworzonej za pomocą funkcji mrsdeploy w ramach kontekstu obliczeniowego platformy Spark, może być konieczne dodanie niektórych brakujących folderów.</span><span class="sxs-lookup"><span data-stu-id="31195-371">If you encounter long delays when trying to consume a web service created with mrsdeploy functions in a Spark compute context, you may need to add some missing folders.</span></span> <span data-ttu-id="31195-372">Aplikacja Spark należy do użytkownika o nazwie „*rserve2*” zawsze wtedy, gdy jest wywoływana z usługi internetowej przy użyciu funkcji mrsdeploy.</span><span class="sxs-lookup"><span data-stu-id="31195-372">The Spark application belongs to a user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="31195-373">Aby obejść ten problem:</span><span class="sxs-lookup"><span data-stu-id="31195-373">To work around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="31195-374">Na tym etapie konfiguracja opernacjonalizacji jest ukończona.</span><span class="sxs-lookup"><span data-stu-id="31195-374">At this stage, the configuration for Operationalization is complete.</span></span> <span data-ttu-id="31195-375">Teraz możesz użyć pakietu „mrsdeploy” w programie RClient, aby nawiązać połączenie z operacjonalizacją w węźle krawędzi i rozpocząć korzystanie z jej funkcji, takich jak [zdalne wykonywanie](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) i [usługi internetowe](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span><span class="sxs-lookup"><span data-stu-id="31195-375">Now you can use the ‘mrsdeploy’ package on your RClient to connect to the Operationalization on edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="31195-376">W zależności od tego, czy klaster został skonfigurowany w sieci wirtualnej, może być konieczne skonfigurowanie tunelowania przekierowania portów za pomocą logowania SSH.</span><span class="sxs-lookup"><span data-stu-id="31195-376">Depending on whether your cluster is set up on a virtual network or not, you may need to set up port forward tunneling through SSH login.</span></span> <span data-ttu-id="31195-377">W poniższych sekcjach wyjaśniono, jak skonfigurować taki tunel.</span><span class="sxs-lookup"><span data-stu-id="31195-377">The following sections explain how to set up this tunnel.</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="31195-378">Klaster oprogramowania RServer w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="31195-378">RServer Cluster on virtual network</span></span>

<span data-ttu-id="31195-379">Sprawdź, czy ruch przez port 12800 węzła krawędzi jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="31195-379">Make sure you allow traffic through port 12800 to the edge node.</span></span> <span data-ttu-id="31195-380">Pozwala to użyć węzła krawędzi do nawiązania połączenia z funkcją operacjonalizacji.</span><span class="sxs-lookup"><span data-stu-id="31195-380">That way, you can use the edge node to connect to the Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="31195-381">Jeśli metoda `remoteLogin()` nie może połączyć się z węzłem krawędzi, lecz nawiązanie połączenia SSH z węzłem krawędzi jest możliwe, sprawdź, czy reguła zezwalająca na ruch przez port 12800 jest skonfigurowana poprawnie.</span><span class="sxs-lookup"><span data-stu-id="31195-381">If the `remoteLogin()` cannot connect to the edge node, but you can SSH to the edge node, then you need to verify whether the rule to allow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="31195-382">Jeśli problem nie ustąpi, możesz go obejść, konfigurując tunelowanie przekierowania portów przez połączenie SSH.</span><span class="sxs-lookup"><span data-stu-id="31195-382">If you continue to face the issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="31195-383">Odpowiednie instrukcje znajdują się w następującej sekcji.</span><span class="sxs-lookup"><span data-stu-id="31195-383">For instructions, see the following section.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="31195-384">Klaster oprogramowania RServer w sieci niewirtualnej</span><span class="sxs-lookup"><span data-stu-id="31195-384">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="31195-385">Jeśli klaster nie jest skonfigurowany w sieci wirtualnej lub występują problemy z korzystaniem z sieci wirtualnej, możesz użyć tunelowania przekierowania portów za pomocą protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="31195-385">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="31195-386">W programie Putty także możesz je skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="31195-386">On Putty, you can set it up as well.</span></span>

![połączenie ssh w programie putty](./media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="31195-388">Gdy sesja SSH jest aktywna, ruch z portu 12800 maszyny jest przekazywany do portu 12800 węzła krawędzi za pomocą sesji SSH.</span><span class="sxs-lookup"><span data-stu-id="31195-388">Once your SSH session is active, the traffic from your machine’s port 12800 is forwarded to the edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="31195-389">Upewnij się, że w metodzie `remoteLogin()` użyto adresu `127.0.0.1:12800`.</span><span class="sxs-lookup"><span data-stu-id="31195-389">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="31195-390">Umożliwi to logowanie do funkcji operacjonalizacji węzła krawędzi przez przekierowanie portów.</span><span class="sxs-lookup"><span data-stu-id="31195-390">This logs in to the edge node’s operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-to-scale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="31195-391">Jak skalować węzły obliczeniowe operacjonalizacji oprogramowania Microsoft R Server na węzłach procesu roboczego usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="31195-391">How to scale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes</span></span>

### <a name="decommission-the-worker-nodes"></a><span data-ttu-id="31195-392">Likwidowanie węzłów procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="31195-392">Decommission the worker node(s)</span></span>

<span data-ttu-id="31195-393">Oprogramowanie Microsoft R Server nie jest aktualnie zarządzane za pomocą usługi Yarn.</span><span class="sxs-lookup"><span data-stu-id="31195-393">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="31195-394">Jeśli węzły procesu roboczego nie zostaną zlikwidowane, menedżer zasobów usługi Yarn nie będzie działać w oczekiwany sposób, ponieważ nie będzie znał zasobów zajętych przez serwer.</span><span class="sxs-lookup"><span data-stu-id="31195-394">If the worker nodes are not decommissioned, the Yarn Resource Manager will not work as expected because it will not be aware of the resources being taken up by the server.</span></span> <span data-ttu-id="31195-395">Aby tego uniknąć, zalecamy zlikwidowanie węzłów procesu roboczego przed przystąpieniem do skalowania węzłów obliczeniowych na zewnątrz.</span><span class="sxs-lookup"><span data-stu-id="31195-395">In order to avoid this situation, we recommend decommissioning the worker nodes before you scale out the compute nodes.</span></span>

<span data-ttu-id="31195-396">Kroki likwidowania węzłów procesu roboczego:</span><span class="sxs-lookup"><span data-stu-id="31195-396">Steps to decommissioning worker nodes:</span></span>

* <span data-ttu-id="31195-397">Zaloguj się do konsoli Ambari klastra usługi HDI i kliknij kartę „hosts” (Hosty)</span><span class="sxs-lookup"><span data-stu-id="31195-397">Log in to HDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="31195-398">Wybierz węzły procesu roboczego do zlikwidowania. Kliknij pozycje „Actions” > „Selected Hosts” > „Hosts” > „Turn ON Maintenance Mode” (Akcje > Wybrane hosty > Hosty > Włącz tryb konserwacji).</span><span class="sxs-lookup"><span data-stu-id="31195-398">Select worker nodes (to be decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="31195-399">Na przykład na poniższej ilustracji węzły wn3 i wn4 są przeznaczone do likwidacji.</span><span class="sxs-lookup"><span data-stu-id="31195-399">For example, in the following image we have selected wn3 and wn4 to decommission.</span></span>  

   ![likwidowanie węzłów procesu roboczego](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="31195-401">Wybierz pozycję **Actions** > **Selected Hosts** > **DataNodes** (Akcje > Wybrane hosty > Węzły danych) i kliknij pozycję **Decommission** (Likwiduj)</span><span class="sxs-lookup"><span data-stu-id="31195-401">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**</span></span>
* <span data-ttu-id="31195-402">Wybierz pozycję **Actions** > **Selected Hosts** > **NodeManagers** (Akcje > Wybrane hosty > Menedżerowie węzła) i kliknij pozycję **Decommission** (Likwiduj)</span><span class="sxs-lookup"><span data-stu-id="31195-402">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**</span></span>
* <span data-ttu-id="31195-403">Wybierz pozycję **Actions** > **Selected Hosts** > **DataNodes** (Akcje > Wybrane hosty > Węzły danych) i kliknij pozycję **Stop** (Zatrzymaj)</span><span class="sxs-lookup"><span data-stu-id="31195-403">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**</span></span>
* <span data-ttu-id="31195-404">Wybierz pozycję **Actions** > **Selected Hosts** > **NodeManagers** (Akcje > Wybrane hosty > Menedżerowie węzła) i kliknij pozycję **Stop** (Zatrzymaj)</span><span class="sxs-lookup"><span data-stu-id="31195-404">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**</span></span>
* <span data-ttu-id="31195-405">Wybierz pozycję **Actions** > **Selected Hosts** > **Hosts** (Akcje > Wybrane hosty > Hosty) i kliknij pozycję **Stop All Components** (Zatrzymaj wszystkie składniki)</span><span class="sxs-lookup"><span data-stu-id="31195-405">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**</span></span>
* <span data-ttu-id="31195-406">Usuń zaznaczenie węzłów procesu roboczego i wybierz węzły główne</span><span class="sxs-lookup"><span data-stu-id="31195-406">Unselect the worker nodes and select the head nodes</span></span>
* <span data-ttu-id="31195-407">Wybierz pozycję **Actions** > **Selected Hosts** > **Hosts** > **Restart All Components** (Akcje > Wybrane hosty > Hosty > Uruchom ponownie wszystkie składniki)</span><span class="sxs-lookup"><span data-stu-id="31195-407">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**</span></span>

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="31195-408">Konfigurowanie węzłów obliczeniowych na wszystkich zlikwidowanych węzłach procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="31195-408">Configure Compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="31195-409">Za pomocą protokołu SSH połącz się z każdym zlikwidowanym węzłem procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="31195-409">SSH into each decommissioned worker node.</span></span>
2. <span data-ttu-id="31195-410">Uruchom narzędzie administracyjne za pomocą polecenia `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span><span class="sxs-lookup"><span data-stu-id="31195-410">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span></span>
3. <span data-ttu-id="31195-411">Wpisz „1”, aby wybrać opcję „Configure R Server for Operationalization” (Konfiguruj oprogramowanie R Server pod kątem operacjonalizacji).</span><span class="sxs-lookup"><span data-stu-id="31195-411">Enter "1" to select option "Configure R Server for Operationalization".</span></span>
4. <span data-ttu-id="31195-412">Wpisz „c”, aby wybrać opcję „C.</span><span class="sxs-lookup"><span data-stu-id="31195-412">Enter "c" to select option "C.</span></span> <span data-ttu-id="31195-413">Compute node” (Węzeł obliczeniowy).</span><span class="sxs-lookup"><span data-stu-id="31195-413">Compute node".</span></span> <span data-ttu-id="31195-414">Umożliwi to skonfigurowanie węzła obliczeniowego w węźle procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="31195-414">This configures the compute node on the worker node.</span></span>
5. <span data-ttu-id="31195-415">Zamknij narzędzie administracyjne.</span><span class="sxs-lookup"><span data-stu-id="31195-415">Exit the Admin Utility.</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="31195-416">Dodawanie szczegółów węzłów obliczeniowych na węźle sieci Web</span><span class="sxs-lookup"><span data-stu-id="31195-416">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="31195-417">Po skonfigurowaniu wszystkich zlikwidowanych węzłów procesu roboczego pod kątem uruchamiania węzła obliczeniowego wróć do węzła krawędzi i dodaj adresy IP zlikwidowanych węzłów procesu roboczego do konfiguracji węzła internetowego oprogramowania Microsoft R Server:</span><span class="sxs-lookup"><span data-stu-id="31195-417">Once all decommissioned worker nodes have been configured to run compute node, come back on the edge node and add decommissioned worker nodes' IP addresses in the Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="31195-418">Połącz się z węzłem krawędzi za pomocą protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="31195-418">SSH into the edge node.</span></span>
* <span data-ttu-id="31195-419">Uruchom polecenie `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="31195-419">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>
* <span data-ttu-id="31195-420">W sekcji „URIs” (Identyfikatory URI) dodaj adres IP i port węzła procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="31195-420">Look for the "URIs" section, and add worker node's IP and port details.</span></span>

    ![wiersz polecenia likwidowania węzłów procesu roboczego](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a><span data-ttu-id="31195-422">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="31195-422">Troubleshoot</span></span>

<span data-ttu-id="31195-423">W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="31195-423">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>


## <a name="next-steps"></a><span data-ttu-id="31195-424">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="31195-424">Next steps</span></span>

<span data-ttu-id="31195-425">Wiesz już, jak utworzyć nowy klaster usługi HDInsight zawierający serwer R Server, oraz znasz podstawy używania konsoli R w sesji SSH.</span><span class="sxs-lookup"><span data-stu-id="31195-425">Now you should understand how to create a new HDInsight cluster that includes the R Server and the basics of using the R console from an SSH session.</span></span> <span data-ttu-id="31195-426">W poniższych tematach opisano inne sposoby korzystania z serwera R Server w usłudze HDInsight oraz zarządzania nim:</span><span class="sxs-lookup"><span data-stu-id="31195-426">The following topics explain other ways of managing and working with R Server on HDInsight:</span></span>

* <span data-ttu-id="31195-427">[Add RStudio Server to HDInsight (if not installed during cluster creation)](hdinsight-hadoop-r-server-install-r-studio.md) (Dodawanie programu RStudio Server do usługi HDInsight — jeśli nie zainstalowano podczas tworzenia klastra)</span><span class="sxs-lookup"><span data-stu-id="31195-427">[Add RStudio Server to HDInsight (if not installed during cluster creation)](hdinsight-hadoop-r-server-install-r-studio.md)</span></span>
* <span data-ttu-id="31195-428">[Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md) (Opcje kontekstu obliczeniowego dla oprogramowania R Server w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="31195-428">[Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md)</span></span>
* <span data-ttu-id="31195-429">[Azure Storage options for R Server on HDInsight](hdinsight-hadoop-r-server-storage.md) (Opcje usługi Azure Storage dla oprogramowania R Server w usłudze HDInsight)</span><span class="sxs-lookup"><span data-stu-id="31195-429">[Azure Storage options for R Server on HDInsight](hdinsight-hadoop-r-server-storage.md)</span></span>
