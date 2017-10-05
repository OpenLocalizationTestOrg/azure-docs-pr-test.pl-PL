---
title: Instalowanie bazy danych MongoDB Windows maszyny Wirtualnej na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak zainstalować bazy danych MongoDB na maszynie Wirtualnej platformy Azure, system Windows Server 2012 R2 utworzone za pomocą modelu wdrażania usługi Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: db1a550b9273925b304fe4280f2a1b0e115f856d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="8687f-103">Instalowanie i Konfigurowanie bazy danych MongoDB na maszynie Wirtualnej systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="8687f-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="8687f-104">[Bazy danych MongoDB](http://www.mongodb.org) jest popularnych open source, wysokiej wydajności bazę danych NoSQL.</span><span class="sxs-lookup"><span data-stu-id="8687f-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="8687f-105">W tym artykule opisano sposób instalowania i konfigurowania bazy danych MongoDB na maszynie wirtualnej systemu Windows Server 2012 R2 (VM) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="8687f-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="8687f-106">Możesz również [zainstalować bazy danych MongoDB na Maszynę wirtualną systemu Linux na platformie Azure](../linux/install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="8687f-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8687f-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8687f-107">Prerequisites</span></span>
<span data-ttu-id="8687f-108">Przed zainstalowaniem i skonfigurowaniem bazy danych MongoDB, należy utworzyć Maszynę wirtualną, a w idealnym przypadku dodania dysku danych do niego.</span><span class="sxs-lookup"><span data-stu-id="8687f-108">Before you install and configure MongoDB, you need to create a VM and, ideally, add a data disk to it.</span></span> <span data-ttu-id="8687f-109">Zobacz następujące artykuły, aby utworzyć Maszynę wirtualną i Dodaj dysk danych:</span><span class="sxs-lookup"><span data-stu-id="8687f-109">See the following articles to create a VM and add a data disk:</span></span>

* <span data-ttu-id="8687f-110">Tworzenie maszyny Wirtualnej systemu Windows Server przy użyciu [portalu Azure](quick-create-portal.md) lub [programu Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8687f-110">Create a Windows Server VM using [the Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="8687f-111">Dołączenie dysku danych do maszyny Wirtualnej systemu Windows Server za pomocą [portalu Azure](attach-managed-disk-portal.md) lub [programu Azure PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8687f-111">Attach a data disk to a Windows Server VM using [the Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="8687f-112">Aby rozpocząć instalowanie i Konfigurowanie bazy danych MongoDB, [Zaloguj się do maszyny Wirtualnej systemu Windows Server](connect-logon.md) przy użyciu pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="8687f-112">To begin installing and configuring MongoDB, [log on to your Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="8687f-113">Instalowanie bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="8687f-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8687f-114">Funkcje zabezpieczeń bazy danych MongoDB, takich jak uwierzytelnianie i powiązanie adresu IP, nie są domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="8687f-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="8687f-115">Funkcje zabezpieczeń powinny być włączone przed wdrożeniem w środowisku produkcyjnym bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8687f-115">Security features should be enabled before deploying MongoDB to a production environment.</span></span> <span data-ttu-id="8687f-116">Aby uzyskać więcej informacji, zobacz [MongoDB zabezpieczeń i uwierzytelniania](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="8687f-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="8687f-117">Po nawiązaniu połączenia z maszyną wirtualną przy użyciu pulpitu zdalnego, Otwórz program Internet Explorer z **Start** menu na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8687f-117">After you've connected to your VM using Remote Desktop, open Internet Explorer from the **Start** menu on the VM.</span></span>
2. <span data-ttu-id="8687f-118">Wybierz **Użyj zalecanych ustawień zabezpieczeń, prywatności i zgodności** gdy program Internet Explorer najpierw otwiera i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8687f-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="8687f-119">Konfiguracja zwiększonych zabezpieczeń programu Internet Explorer jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="8687f-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="8687f-120">Dodaj witrynę bazy danych MongoDB do listy dozwolonych witryn:</span><span class="sxs-lookup"><span data-stu-id="8687f-120">Add the MongoDB website to the list of allowed sites:</span></span>
   
   * <span data-ttu-id="8687f-121">Wybierz **narzędzia** ikonę w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="8687f-121">Select the **Tools** icon in the upper-right corner.</span></span>
   * <span data-ttu-id="8687f-122">W **Opcje internetowe**, wybierz pozycję **zabezpieczeń** , a następnie wybierz **Zaufane witryny** ikony.</span><span class="sxs-lookup"><span data-stu-id="8687f-122">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="8687f-123">Kliknij przycisk **witryny** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8687f-123">Click the **Sites** button.</span></span> <span data-ttu-id="8687f-124">Dodaj *https://\*. mongodb.org* do listy zaufanych witryn, a następnie zamknij okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="8687f-124">Add *https://\*.mongodb.org* to the list of trusted sites, and then close the dialog box.</span></span>
     
     ![Konfigurowanie ustawień zabezpieczeń programu Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="8687f-126">Przejdź do [MongoDB — pliki do pobrania](http://www.mongodb.org/downloads) strony (http://www.mongodb.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="8687f-126">Browse to the [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="8687f-127">W razie potrzeby wybierz **serwera społeczności** edition, a następnie wybierz najnowsze stabilny bieżącej wersji dla systemu Windows Server 2008 R2 w wersji 64-bitowej lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="8687f-127">If needed, select the **Community Server** edition and then select the latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="8687f-128">Aby pobrać Instalatora, kliknij przycisk **pobierania (msi)**.</span><span class="sxs-lookup"><span data-stu-id="8687f-128">To download the installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![Pobierz Instalator bazy danych MongoDB](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="8687f-130">Po zakończeniu pobierania, należy uruchomić Instalatora.</span><span class="sxs-lookup"><span data-stu-id="8687f-130">Run the installer after the download is complete.</span></span>
6. <span data-ttu-id="8687f-131">Przeczytaj i zaakceptuj umowę licencyjną.</span><span class="sxs-lookup"><span data-stu-id="8687f-131">Read and accept the license agreement.</span></span> <span data-ttu-id="8687f-132">Po wyświetleniu monitu wybierz **Complete** zainstalować.</span><span class="sxs-lookup"><span data-stu-id="8687f-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="8687f-133">Na ekranie końcowym, kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="8687f-133">On the final screen, click **Install**.</span></span>

## <a name="configure-the-vm-and-mongodb"></a><span data-ttu-id="8687f-134">Skonfiguruj maszynę Wirtualną i bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="8687f-134">Configure the VM and MongoDB</span></span>
1. <span data-ttu-id="8687f-135">Zmienne ścieżek nie są aktualizowane przez Instalatora bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8687f-135">The path variables are not updated by the MongoDB installer.</span></span> <span data-ttu-id="8687f-136">Bez MongoDB `bin` lokalizacji w zmiennej path, należy określić pełną ścieżkę każdym użyciu wykonywalny bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8687f-136">Without the MongoDB `bin` location in your path variable, you need to specify the full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="8687f-137">Aby dodać lokalizację do zmiennej path:</span><span class="sxs-lookup"><span data-stu-id="8687f-137">To add the location to your path variable:</span></span>
   
   * <span data-ttu-id="8687f-138">Kliknij prawym przyciskiem myszy **Start** menu, a następnie wybierz **systemu**.</span><span class="sxs-lookup"><span data-stu-id="8687f-138">Right-click the **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="8687f-139">Kliknij przycisk **Zaawansowane ustawienia systemu**, a następnie kliknij przycisk **zmiennych środowiskowych**.</span><span class="sxs-lookup"><span data-stu-id="8687f-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="8687f-140">W obszarze **zmienne systemowe**, wybierz pozycję **ścieżki**, a następnie kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="8687f-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![Skonfiguruj zmienne ŚCIEŻEK](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="8687f-142">Dodaj ścieżkę do Twojej bazy danych MongoDB `bin` folderu.</span><span class="sxs-lookup"><span data-stu-id="8687f-142">Add the path to your MongoDB `bin` folder.</span></span> <span data-ttu-id="8687f-143">Bazy danych MongoDB zazwyczaj jest zainstalowany w *C:\Program Files\MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="8687f-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="8687f-144">Sprawdź ścieżkę instalacji na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8687f-144">Verify the installation path on your VM.</span></span> <span data-ttu-id="8687f-145">W poniższym przykładzie dodano domyślnej lokalizacji do instalacji bazy danych MongoDB `PATH` zmienną:</span><span class="sxs-lookup"><span data-stu-id="8687f-145">The following example adds the default MongoDB install location to the `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="8687f-146">Pamiętaj dodać wiodącego średnika (`;`) wskazująca, czy dodajesz lokalizację do Twojej `PATH` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="8687f-146">Be sure to add the leading semicolon (`;`) to indicate that you are adding a location to your `PATH` variable.</span></span>

2. <span data-ttu-id="8687f-147">Tworzenie bazy danych MongoDB katalogi danych i dziennika na dysku danych.</span><span class="sxs-lookup"><span data-stu-id="8687f-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="8687f-148">Z **Start** menu, wybierz opcję **wiersza polecenia**.</span><span class="sxs-lookup"><span data-stu-id="8687f-148">From the **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="8687f-149">Poniższe przykłady tworzenia katalogów na dysku F:</span><span class="sxs-lookup"><span data-stu-id="8687f-149">The following examples create the directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="8687f-150">Uruchom wystąpienie bazy danych MongoDB przy użyciu następującego polecenia dostosowywania ścieżka do danych i dziennika odpowiednio katalogi:</span><span class="sxs-lookup"><span data-stu-id="8687f-150">Start a MongoDB instance with the following command, adjusting the path to your data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="8687f-151">Może upłynąć kilka minut dla bazy danych MongoDB przydzielić plików dziennika i rozpocząć nasłuchiwania dla połączeń.</span><span class="sxs-lookup"><span data-stu-id="8687f-151">It may take several minutes for MongoDB to allocate the journal files and start listening for connections.</span></span> <span data-ttu-id="8687f-152">Wszystkie komunikaty dziennika są kierowane do *F:\MongoLogs\mongolog.log* pliku jako `mongod.exe` server uruchamia i przydziela plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="8687f-152">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8687f-153">Wiersz polecenia pozostaje koncentruje się na to zadanie jest uruchomiona wystąpienia bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8687f-153">The command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="8687f-154">Zamykaj okna wiersza polecenia do kontynuowania pracy bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8687f-154">Leave the command prompt window open to continue running MongoDB.</span></span> <span data-ttu-id="8687f-155">Ewentualnie można zainstalować bazy danych MongoDB jako usługa, zgodnie z opisem w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="8687f-155">Or, install MongoDB as service, as detailed in the next step.</span></span>

4. <span data-ttu-id="8687f-156">W przypadku bardziej niezawodne środowisko bazy danych MongoDB, zainstaluj `mongod.exe` jako usługa.</span><span class="sxs-lookup"><span data-stu-id="8687f-156">For a more robust MongoDB experience, install the `mongod.exe` as a service.</span></span> <span data-ttu-id="8687f-157">Tworzenie usługi oznacza, że nie ma potrzeby pozostaw wiersz polecenia uruchamianiu za każdym razem, którego chcesz użyć bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8687f-157">Creating a service means you don't need to leave a command prompt running each time you want to use MongoDB.</span></span> <span data-ttu-id="8687f-158">Utwórz usługę następujące odpowiednio dostosowywania ścieżka do danych i dziennika katalogów:</span><span class="sxs-lookup"><span data-stu-id="8687f-158">Create the service as follows, adjusting the path to your data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="8687f-159">Poprzednie polecenie tworzy usługę o nazwie bazy danych MongoDB, opis "BD o Mongo".</span><span class="sxs-lookup"><span data-stu-id="8687f-159">The preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="8687f-160">Są także określić następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="8687f-160">The following parameters are also specified:</span></span>
   
   * <span data-ttu-id="8687f-161">`--dbpath` Opcji określa lokalizację katalogu danych.</span><span class="sxs-lookup"><span data-stu-id="8687f-161">The `--dbpath` option specifies the location of the data directory.</span></span>
   * <span data-ttu-id="8687f-162">`--logpath` Opcji należy używać do określenia pliku dziennika, ponieważ uruchomiona usługa nie ma okno polecenia, aby wyświetlić dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="8687f-162">The `--logpath` option must be used to specify a log file, because the running service does not have a command window to display output.</span></span>
   * <span data-ttu-id="8687f-163">`--logappend` Opcja określa, czy ponowne uruchomienie usługi powoduje, że dane wyjściowe do dołączenia do istniejącego pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="8687f-163">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span></span>
   
   <span data-ttu-id="8687f-164">Aby uruchomić usługę bazy danych MongoDB, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="8687f-164">To start the MongoDB service, run the following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="8687f-165">Aby uzyskać więcej informacji na temat tworzenia usługi dla bazy danych MongoDB, zobacz [skonfigurować usługę systemu Windows dla bazy danych MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span><span class="sxs-lookup"><span data-stu-id="8687f-165">For more information about creating the MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-the-mongodb-instance"></a><span data-ttu-id="8687f-166">Testowe wystąpienie bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="8687f-166">Test the MongoDB instance</span></span>
<span data-ttu-id="8687f-167">Z bazy danych MongoDB, uruchomione jako jedno wystąpienie lub zainstalowany jako usługa można teraz rozpocząć tworzenie i korzystanie z baz danych.</span><span class="sxs-lookup"><span data-stu-id="8687f-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="8687f-168">Aby uruchomić powłoki administracyjne bazy danych MongoDB, otworzyć inne okno wiersza polecenia z **Start** menu, a następnie wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="8687f-168">To start the MongoDB administrative shell, open another command prompt window from the **Start** menu, and enter the following command:</span></span>

```
mongo  
```

<span data-ttu-id="8687f-169">Możesz wyświetlić listę z bazami danych z `db` polecenia.</span><span class="sxs-lookup"><span data-stu-id="8687f-169">You can list the databases with the `db` command.</span></span> <span data-ttu-id="8687f-170">Wstaw dowolne dane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="8687f-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="8687f-171">Wyszukiwanie danych w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="8687f-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="8687f-172">Dane wyjściowe są podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="8687f-172">The output is similar to the following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="8687f-173">Zakończ `mongo` konsoli w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="8687f-173">Exit the `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="8687f-174">Konfigurowanie zapory i reguł sieciowej grupy zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="8687f-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="8687f-175">Teraz, bazy danych MongoDB jest zainstalowana i uruchomiona, należy otworzyć port w Zaporze systemu Windows, możesz zdalnie nawiązać połączenie bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8687f-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect to MongoDB.</span></span> <span data-ttu-id="8687f-176">Aby utworzyć nową regułę ruchu przychodzącego zezwalająca na porcie TCP 27017, otwórz administracyjny wiersz środowiska PowerShell i wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="8687f-176">To create a new inbound rule to allow TCP port 27017, open an administrative PowerShell prompt and enter the following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="8687f-177">Można również utworzyć regułę przy użyciu **Zapora systemu Windows z zabezpieczeniami zaawansowanymi** graficzne narzędzie do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="8687f-177">You can also create the rule by using the **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="8687f-178">Utwórz nową regułę ruchu przychodzącego zezwalająca na porcie TCP 27017.</span><span class="sxs-lookup"><span data-stu-id="8687f-178">Create a new inbound rule to allow TCP port 27017.</span></span>

<span data-ttu-id="8687f-179">W razie potrzeby utwórz zasadę sieciową grupę zabezpieczeń, aby zezwolić na dostęp do bazy danych MongoDB z poza istniejącą podsieć sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8687f-179">If needed, create a Network Security Group rule to allow access to MongoDB from outside of the existing Azure virtual network subnet.</span></span> <span data-ttu-id="8687f-180">Można utworzyć reguły grupy zabezpieczeń sieci przy użyciu [portalu Azure](nsg-quickstart-portal.md) lub [programu Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8687f-180">You can create the Network Security Group rules by using the [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="8687f-181">Podobnie jak w przypadku reguł zapory systemu Windows umożliwiają port TCP 27017 do interfejsu sieci wirtualnej maszyny wirtualnej bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8687f-181">As with the Windows Firewall rules, allow TCP port 27017 to the virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="8687f-182">TCP port 27017 jest domyślny port używany przez bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8687f-182">TCP port 27017 is the default port used by MongoDB.</span></span> <span data-ttu-id="8687f-183">Tego portu można zmienić za pomocą `--port` parametru podczas uruchamiania `mongod.exe` ręcznie lub z poziomu usługi.</span><span class="sxs-lookup"><span data-stu-id="8687f-183">You can change this port by using the `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="8687f-184">Jeśli zmienisz numer portu, upewnij się, można zaktualizować reguł zapory systemu Windows i grupy zabezpieczeń sieci w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="8687f-184">If you change the port, make sure to update the Windows Firewall and Network Security Group rules in the preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8687f-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8687f-185">Next steps</span></span>
<span data-ttu-id="8687f-186">W tym samouczku przedstawiono sposób instalowania i konfigurowania bazy danych MongoDB na maszynie Wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="8687f-186">In this tutorial, you learned how to install and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="8687f-187">Na maszynie Wirtualnej systemu Windows, można uzyskać dostęp bazy danych MongoDB, wykonując następujące tematy Zaawansowane w [dokumentacją usługi MongoDB](https://docs.mongodb.com/manual/).</span><span class="sxs-lookup"><span data-stu-id="8687f-187">You can now access MongoDB on your Windows VM, by following the advanced topics in the [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

