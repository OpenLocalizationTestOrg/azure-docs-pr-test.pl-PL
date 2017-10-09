---
title: aaaInstall MongoDB na maszynie Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tworzone tooinstall bazy danych MongoDB na maszynie Wirtualnej platformy Azure, system Windows Server 2012 R2 z modelu wdrażania usługi Resource Manager hello."
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
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="bd6f1-103">Instalowanie i Konfigurowanie bazy danych MongoDB na maszynie Wirtualnej systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="bd6f1-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="bd6f1-104">[Bazy danych MongoDB](http://www.mongodb.org) jest popularnych open source, wysokiej wydajności bazę danych NoSQL.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="bd6f1-105">W tym artykule opisano sposób instalowania i konfigurowania bazy danych MongoDB na maszynie wirtualnej systemu Windows Server 2012 R2 (VM) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="bd6f1-106">Możesz również [zainstalować bazy danych MongoDB na Maszynę wirtualną systemu Linux na platformie Azure](../linux/install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="bd6f1-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd6f1-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bd6f1-107">Prerequisites</span></span>
<span data-ttu-id="bd6f1-108">Przed zainstalowaniem i skonfigurowaniem bazy danych MongoDB, którego należy toocreate Maszynę wirtualną, najlepiej jest dodać tooit dysku danych.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-108">Before you install and configure MongoDB, you need toocreate a VM and, ideally, add a data disk tooit.</span></span> <span data-ttu-id="bd6f1-109">Zobacz hello następujące artykuły toocreate maszyny Wirtualnej, a następnie Dodaj dysk z danymi:</span><span class="sxs-lookup"><span data-stu-id="bd6f1-109">See hello following articles toocreate a VM and add a data disk:</span></span>

* <span data-ttu-id="bd6f1-110">Tworzenie maszyny Wirtualnej systemu Windows Server przy użyciu [hello portalu Azure](quick-create-portal.md) lub [programu Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bd6f1-110">Create a Windows Server VM using [hello Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="bd6f1-111">Dołączanie danych dysku tooa maszyny Wirtualnej systemu Windows Server przy użyciu [hello portalu Azure](attach-managed-disk-portal.md) lub [programu Azure PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="bd6f1-111">Attach a data disk tooa Windows Server VM using [hello Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="bd6f1-112">toobegin Instalowanie i Konfigurowanie bazy danych MongoDB, [logowania tooyour maszyny Wirtualnej systemu Windows Server](connect-logon.md) przy użyciu pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-112">toobegin installing and configuring MongoDB, [log on tooyour Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="bd6f1-113">Instalowanie bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="bd6f1-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bd6f1-114">Funkcje zabezpieczeń bazy danych MongoDB, takich jak uwierzytelnianie i powiązanie adresu IP, nie są domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="bd6f1-115">Funkcje zabezpieczeń powinny być włączone przed wdrożeniem w środowisku produkcyjnym tooa bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-115">Security features should be enabled before deploying MongoDB tooa production environment.</span></span> <span data-ttu-id="bd6f1-116">Aby uzyskać więcej informacji, zobacz [MongoDB zabezpieczeń i uwierzytelniania](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="bd6f1-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="bd6f1-117">Po nawiązaniu połączenia tooyour maszyny Wirtualnej przy użyciu pulpitu zdalnego, Otwórz program Internet Explorer z hello **Start** menu na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-117">After you've connected tooyour VM using Remote Desktop, open Internet Explorer from hello **Start** menu on hello VM.</span></span>
2. <span data-ttu-id="bd6f1-118">Wybierz **Użyj zalecanych ustawień zabezpieczeń, prywatności i zgodności** gdy program Internet Explorer najpierw otwiera i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="bd6f1-119">Konfiguracja zwiększonych zabezpieczeń programu Internet Explorer jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="bd6f1-120">Dodaj hello bazy danych MongoDB witryny sieci Web toohello listy dozwolonych witryn:</span><span class="sxs-lookup"><span data-stu-id="bd6f1-120">Add hello MongoDB website toohello list of allowed sites:</span></span>
   
   * <span data-ttu-id="bd6f1-121">Wybierz hello **narzędzia** ikonę w prawym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-121">Select hello **Tools** icon in hello upper-right corner.</span></span>
   * <span data-ttu-id="bd6f1-122">W **Opcje internetowe**, wybierz pozycję hello **zabezpieczeń** , a następnie wybierz hello **Zaufane witryny** ikony.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-122">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="bd6f1-123">Kliknij przycisk hello **witryny** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-123">Click hello **Sites** button.</span></span> <span data-ttu-id="bd6f1-124">Dodaj *https://\*. mongodb.org* toohello listy zaufanych witryn i hello następnie zamknij okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-124">Add *https://\*.mongodb.org* toohello list of trusted sites, and then close hello dialog box.</span></span>
     
     ![Konfigurowanie ustawień zabezpieczeń programu Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="bd6f1-126">Przeglądaj toohello [MongoDB — pliki do pobrania](http://www.mongodb.org/downloads) strony (http://www.mongodb.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="bd6f1-126">Browse toohello [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="bd6f1-127">W razie potrzeby wybierz hello **serwera społeczności** edition i hello a następnie wybierz pozycję najnowsze bieżącej stabilna wersji dla systemu Windows Server 2008 R2 w wersji 64-bitowej lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-127">If needed, select hello **Community Server** edition and then select hello latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="bd6f1-128">toodownload hello Instalatora, kliknij przycisk **pobierania (msi)**.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-128">toodownload hello installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![Pobierz Instalator bazy danych MongoDB](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="bd6f1-130">Uruchom Instalatora hello, po zakończeniu pobierania hello.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-130">Run hello installer after hello download is complete.</span></span>
6. <span data-ttu-id="bd6f1-131">Przeczytaj i zaakceptuj umowę licencyjną hello.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-131">Read and accept hello license agreement.</span></span> <span data-ttu-id="bd6f1-132">Po wyświetleniu monitu wybierz **Complete** zainstalować.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="bd6f1-133">Na ekranie końcowym powitania kliknij **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-133">On hello final screen, click **Install**.</span></span>

## <a name="configure-hello-vm-and-mongodb"></a><span data-ttu-id="bd6f1-134">Skonfiguruj hello maszyny Wirtualnej i bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="bd6f1-134">Configure hello VM and MongoDB</span></span>
1. <span data-ttu-id="bd6f1-135">Witaj zmienne ścieżek nie są aktualizowane przez Instalatora bazy danych MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-135">hello path variables are not updated by hello MongoDB installer.</span></span> <span data-ttu-id="bd6f1-136">Bez hello bazy danych MongoDB `bin` lokalizacji w zmiennej path, należy toospecify hello pełną ścieżkę każdym użyciu wykonywalny bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-136">Without hello MongoDB `bin` location in your path variable, you need toospecify hello full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="bd6f1-137">zmienna ścieżki tooadd hello lokalizacji tooyour:</span><span class="sxs-lookup"><span data-stu-id="bd6f1-137">tooadd hello location tooyour path variable:</span></span>
   
   * <span data-ttu-id="bd6f1-138">Kliknij prawym przyciskiem myszy hello **Start** menu, a następnie wybierz **systemu**.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-138">Right-click hello **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="bd6f1-139">Kliknij przycisk **Zaawansowane ustawienia systemu**, a następnie kliknij przycisk **zmiennych środowiskowych**.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="bd6f1-140">W obszarze **zmienne systemowe**, wybierz pozycję **ścieżki**, a następnie kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![Skonfiguruj zmienne ŚCIEŻEK](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="bd6f1-142">Dodaj hello tooyour ścieżka bazy danych MongoDB `bin` folderu.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-142">Add hello path tooyour MongoDB `bin` folder.</span></span> <span data-ttu-id="bd6f1-143">Bazy danych MongoDB zazwyczaj jest zainstalowany w *C:\Program Files\MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="bd6f1-144">Sprawdź, czy ścieżka instalacji hello na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-144">Verify hello installation path on your VM.</span></span> <span data-ttu-id="bd6f1-145">Witaj poniższy przykład umożliwia dodanie hello domyślnej bazy danych MongoDB instalacji lokalizacji toohello `PATH` zmienną:</span><span class="sxs-lookup"><span data-stu-id="bd6f1-145">hello following example adds hello default MongoDB install location toohello `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="bd6f1-146">Należy się tooadd hello wiodącego średnika (`;`) tooindicate dodajesz tooyour lokalizacji `PATH` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-146">Be sure tooadd hello leading semicolon (`;`) tooindicate that you are adding a location tooyour `PATH` variable.</span></span>

2. <span data-ttu-id="bd6f1-147">Tworzenie bazy danych MongoDB katalogi danych i dziennika na dysku danych.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="bd6f1-148">Z hello **Start** menu, wybierz opcję **wiersza polecenia**.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-148">From hello **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="bd6f1-149">Następujące przykłady Hello tworzenia katalogów hello na dysku F:</span><span class="sxs-lookup"><span data-stu-id="bd6f1-149">hello following examples create hello directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="bd6f1-150">Wystąpienie bazy danych MongoDB zaczynać się hello następujące polecenia, dostosowywania hello ścieżki tooyour danych i dziennika odpowiednio katalogi:</span><span class="sxs-lookup"><span data-stu-id="bd6f1-150">Start a MongoDB instance with hello following command, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="bd6f1-151">Może potrwać kilka minut dla bazy danych MongoDB tooallocate hello plików dziennika i rozpocząć nasłuchiwania dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-151">It may take several minutes for MongoDB tooallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="bd6f1-152">Wszystkie komunikaty dziennika są ukierunkowanej toohello *F:\MongoLogs\mongolog.log* pliku jako `mongod.exe` server uruchamia i przydziela plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-152">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bd6f1-153">Wiersz polecenia Hello pozostaje koncentruje się na to zadanie uruchomionej wystąpienia bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-153">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="bd6f1-154">Pozostaw hello wiersza polecenia okna otwarte toocontinue uruchamiania bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-154">Leave hello command prompt window open toocontinue running MongoDB.</span></span> <span data-ttu-id="bd6f1-155">Ewentualnie można zainstalować bazy danych MongoDB jako usługa, zgodnie z opisem w następnym kroku hello.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-155">Or, install MongoDB as service, as detailed in hello next step.</span></span>

4. <span data-ttu-id="bd6f1-156">W przypadku bardziej niezawodne środowisko bazy danych MongoDB, zainstaluj hello `mongod.exe` jako usługa.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-156">For a more robust MongoDB experience, install hello `mongod.exe` as a service.</span></span> <span data-ttu-id="bd6f1-157">Tworzenie usługi oznacza, że nie ma potrzeby tooleave wiersz polecenia z każdym toouse bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-157">Creating a service means you don't need tooleave a command prompt running each time you want toouse MongoDB.</span></span> <span data-ttu-id="bd6f1-158">Tworzenie usługi hello następujące odpowiednio dostosowywania hello ścieżki tooyour danych i dziennika katalogów:</span><span class="sxs-lookup"><span data-stu-id="bd6f1-158">Create hello service as follows, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="bd6f1-159">Witaj poprzednie polecenie tworzy usługę o nazwie bazy danych MongoDB, opis "BD o Mongo".</span><span class="sxs-lookup"><span data-stu-id="bd6f1-159">hello preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="bd6f1-160">określono też Hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="bd6f1-160">hello following parameters are also specified:</span></span>
   
   * <span data-ttu-id="bd6f1-161">Witaj `--dbpath` opcji określa lokalizację hello hello danych katalogu.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-161">hello `--dbpath` option specifies hello location of hello data directory.</span></span>
   * <span data-ttu-id="bd6f1-162">Witaj `--logpath` opcja musi być używane toospecify pliku dziennika, ponieważ hello uruchomionej usługi nie ma danych wyjściowych toodisplay okna poleceń.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-162">hello `--logpath` option must be used toospecify a log file, because hello running service does not have a command window toodisplay output.</span></span>
   * <span data-ttu-id="bd6f1-163">Witaj `--logappend` opcja określa, czy ponowne uruchomienie usługi hello powoduje, że dane wyjściowe tooappend toohello istniejący plik dziennika.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-163">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>
   
   <span data-ttu-id="bd6f1-164">toostart hello usługi bazy danych MongoDB, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="bd6f1-164">toostart hello MongoDB service, run hello following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="bd6f1-165">Aby uzyskać więcej informacji o tworzeniu hello usługi bazy danych MongoDB, zobacz [skonfigurować usługę systemu Windows dla bazy danych MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span><span class="sxs-lookup"><span data-stu-id="bd6f1-165">For more information about creating hello MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-hello-mongodb-instance"></a><span data-ttu-id="bd6f1-166">Wystąpienie bazy danych MongoDB hello testu</span><span class="sxs-lookup"><span data-stu-id="bd6f1-166">Test hello MongoDB instance</span></span>
<span data-ttu-id="bd6f1-167">Z bazy danych MongoDB, uruchomione jako jedno wystąpienie lub zainstalowany jako usługa można teraz rozpocząć tworzenie i korzystanie z baz danych.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="bd6f1-168">toostart hello powłoki administracyjne bazy danych MongoDB, otworzyć inne okno wiersza polecenia z hello **Start** menu, a następnie wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="bd6f1-168">toostart hello MongoDB administrative shell, open another command prompt window from hello **Start** menu, and enter hello following command:</span></span>

```
mongo  
```

<span data-ttu-id="bd6f1-169">Możesz wyświetlić listę hello baz danych, hello `db` polecenia.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-169">You can list hello databases with hello `db` command.</span></span> <span data-ttu-id="bd6f1-170">Wstaw dowolne dane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="bd6f1-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="bd6f1-171">Wyszukiwanie danych w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="bd6f1-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="bd6f1-172">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="bd6f1-172">hello output is similar toohello following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="bd6f1-173">Zakończ hello `mongo` konsoli w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="bd6f1-173">Exit hello `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="bd6f1-174">Konfigurowanie zapory i reguł sieciowej grupy zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="bd6f1-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="bd6f1-175">Teraz, bazy danych MongoDB jest zainstalowana i uruchomiona, należy otworzyć port w Zaporze systemu Windows, aby mogli zdalnie łączyć z tooMongoDB.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span> <span data-ttu-id="bd6f1-176">toocreate nowy port TCP tooallow reguły dla ruchu przychodzącego 27017, otwórz administracyjny wiersz środowiska PowerShell i wpisz następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="bd6f1-176">toocreate a new inbound rule tooallow TCP port 27017, open an administrative PowerShell prompt and enter hello following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="bd6f1-177">Można również utworzyć reguły hello przy użyciu hello **Zapora systemu Windows z zabezpieczeniami zaawansowanymi** graficzne narzędzie do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-177">You can also create hello rule by using hello **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="bd6f1-178">Utwórz nowy port TCP tooallow reguły dla ruchu przychodzącego 27017.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-178">Create a new inbound rule tooallow TCP port 27017.</span></span>

<span data-ttu-id="bd6f1-179">W razie potrzeby utwórz grupę zabezpieczeń sieci reguły tooallow dostępu tooMongoDB z poza hello istniejącą podsieć sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-179">If needed, create a Network Security Group rule tooallow access tooMongoDB from outside of hello existing Azure virtual network subnet.</span></span> <span data-ttu-id="bd6f1-180">Można utworzyć hello reguł sieciowej grupy zabezpieczeń przy użyciu hello [portalu Azure](nsg-quickstart-portal.md) lub [programu Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bd6f1-180">You can create hello Network Security Group rules by using hello [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="bd6f1-181">Podobnie jak w przypadku reguł zapory systemu Windows hello, Zezwalaj na interfejs sieci wirtualnej toohello port 27017 TCP maszyny wirtualnej bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-181">As with hello Windows Firewall rules, allow TCP port 27017 toohello virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="bd6f1-182">TCP port 27017 hello domyślny port jest używany przez bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-182">TCP port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="bd6f1-183">Tego portu można zmienić za pomocą hello `--port` parametru podczas uruchamiania `mongod.exe` ręcznie lub z poziomu usługi.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-183">You can change this port by using hello `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="bd6f1-184">W przypadku zmiany portu hello, upewnij się, że tooupdate hello zapory systemu Windows i grupy zabezpieczeń sieci reguły w poprzednich krokach hello.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-184">If you change hello port, make sure tooupdate hello Windows Firewall and Network Security Group rules in hello preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bd6f1-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bd6f1-185">Next steps</span></span>
<span data-ttu-id="bd6f1-186">W tym samouczku można przedstawiono sposób tooinstall i skonfigurować bazy danych MongoDB na maszynie Wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="bd6f1-186">In this tutorial, you learned how tooinstall and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="bd6f1-187">Można uzyskać dostęp bazy danych MongoDB na maszynie Wirtualnej systemu Windows, w następujących hello zaawansowanych tematów w hello [dokumentacją usługi MongoDB](https://docs.mongodb.com/manual/).</span><span class="sxs-lookup"><span data-stu-id="bd6f1-187">You can now access MongoDB on your Windows VM, by following hello advanced topics in hello [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

