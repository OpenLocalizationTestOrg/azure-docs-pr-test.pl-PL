---
title: "aaaHow toouse hello Azure podrzędna wtyczki o ciągłej integracji Hudson | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toouse hello Azure podrzędna wtyczki o Hudson ciągłej integracji."
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="57e81-103">Jak toouse hello Azure podrzędna wtyczki o Hudson ciągłej integracji</span><span class="sxs-lookup"><span data-stu-id="57e81-103">How toouse hello Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="57e81-104">Hello Azure podrzędna wtyczki dla Hudson umożliwia tooprovision węzłów podrzędnych na platformie Azure uruchamiania rozproszonych kompilacji.</span><span class="sxs-lookup"><span data-stu-id="57e81-104">hello Azure slave plug-in for Hudson enables you tooprovision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-hello-azure-slave-plug-in"></a><span data-ttu-id="57e81-105">Zainstaluj hello Azure podrzędna dodatku plug-in</span><span class="sxs-lookup"><span data-stu-id="57e81-105">Install hello Azure Slave plug-in</span></span>
1. <span data-ttu-id="57e81-106">W hello Hudson pulpitu nawigacyjnego, kliknij przycisk **Zarządzanie Hudson**.</span><span class="sxs-lookup"><span data-stu-id="57e81-106">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="57e81-107">W hello **Zarządzanie Hudson** kliknij pozycję **Zarządzanie wtyczkami**.</span><span class="sxs-lookup"><span data-stu-id="57e81-107">In hello **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="57e81-108">Kliknij przycisk hello **dostępne** kartę.</span><span class="sxs-lookup"><span data-stu-id="57e81-108">Click hello **Available** tab.</span></span>
4. <span data-ttu-id="57e81-109">Kliknij przycisk **wyszukiwania** i typ **Azure** toolimit hello listy toorelevant dodatków plug-in.</span><span class="sxs-lookup"><span data-stu-id="57e81-109">Click **Search** and type **Azure** toolimit hello list toorelevant plug-ins.</span></span>
   
    <span data-ttu-id="57e81-110">Jeśli wybierzesz tooscroll za pośrednictwem listy hello dostępne dodatki plug-in można znaleźć hello Azure podrzędna wtyczki w obszarze hello **klastra zarządzania i dystrybucji kompilacji** części hello **innym** kartę.</span><span class="sxs-lookup"><span data-stu-id="57e81-110">If you opt tooscroll through hello list of available plug-ins, you will find hello Azure slave plug-in under hello **Cluster Management and Distributed Build** section in hello **Others** tab.</span></span>
5. <span data-ttu-id="57e81-111">Zaznacz pole wyboru powitania dla **wtyczki podrzędna Azure**.</span><span class="sxs-lookup"><span data-stu-id="57e81-111">Select hello checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="57e81-112">Kliknij pozycję **Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="57e81-112">Click **Install**.</span></span>
7. <span data-ttu-id="57e81-113">Uruchom ponownie Hudson.</span><span class="sxs-lookup"><span data-stu-id="57e81-113">Restart Hudson.</span></span>

<span data-ttu-id="57e81-114">Po zainstalowaniu tego dodatku plug-in hello hello następne kroki będą hello tooconfigure wtyczki z profilu subskrypcji platformy Azure i toocreate szablon, który będzie używany podczas tworzenia hello wirtualna hello podrzędny węzła.</span><span class="sxs-lookup"><span data-stu-id="57e81-114">Now that hello plug-in is installed, hello next steps would be tooconfigure hello plug-in with your Azure subscription profile and toocreate a template that will be used in creating hello VM for hello slave node.</span></span>

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="57e81-115">Skonfiguruj hello Azure podrzędna wtyczki z profilem subskrypcji</span><span class="sxs-lookup"><span data-stu-id="57e81-115">Configure hello Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="57e81-116">Profil subskrypcji również tooas określonego ustawienia publikowania, jest plik XML, który zawiera bezpiecznych poświadczeń i dodatkowe informacje, należy toowork z platformy Azure w środowisku projektowania.</span><span class="sxs-lookup"><span data-stu-id="57e81-116">A subscription profile, also referred tooas publish settings, is an XML file that contains secure credentials and some additional information you'll need toowork with Azure in your development environment.</span></span> <span data-ttu-id="57e81-117">tooconfigure hello Azure podrzędna wtyczki, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="57e81-117">tooconfigure hello Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="57e81-118">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="57e81-118">Your subscription id</span></span>
* <span data-ttu-id="57e81-119">Certyfikat zarządzania dla subskrypcji</span><span class="sxs-lookup"><span data-stu-id="57e81-119">A management certificate for your subscription</span></span>

<span data-ttu-id="57e81-120">Są one dostępne w Twojej [profilu subskrypcji].</span><span class="sxs-lookup"><span data-stu-id="57e81-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="57e81-121">Poniżej znajduje się przykład profilu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="57e81-121">Below is an example of a subscription profile.</span></span>

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

<span data-ttu-id="57e81-122">Po utworzeniu profilu subskrypcji, wykonaj te kroki tooconfigure hello Azure podrzędna dodatku plug-in.</span><span class="sxs-lookup"><span data-stu-id="57e81-122">Once you have your subscription profile, follow these steps tooconfigure hello Azure slave plug-in.</span></span>

1. <span data-ttu-id="57e81-123">W hello Hudson pulpitu nawigacyjnego, kliknij przycisk **Zarządzanie Hudson**.</span><span class="sxs-lookup"><span data-stu-id="57e81-123">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="57e81-124">Kliknij przycisk **skonfigurować System**.</span><span class="sxs-lookup"><span data-stu-id="57e81-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="57e81-125">Przewiń w dół hello strony toofind hello **chmury** sekcji.</span><span class="sxs-lookup"><span data-stu-id="57e81-125">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="57e81-126">Kliknij przycisk **Dodaj nowe chmury > Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="57e81-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![Dodaj nowy chmury][add new cloud]
   
    <span data-ttu-id="57e81-128">Wyświetli hello pól, których należy tooenter Szczegóły subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="57e81-128">This will show hello fields where you need tooenter your subscription details.</span></span>
   
    ![Konfigurowanie profilu][configure profile]
5. <span data-ttu-id="57e81-130">Skopiuj certyfikat zarządzania i identyfikator subskrypcji hello z Twojej subskrypcji i wklej je w odpowiednich polach hello.</span><span class="sxs-lookup"><span data-stu-id="57e81-130">Copy hello subscription id and management certificate from your subscription profile and paste them in hello appropriate fields.</span></span>
   
    <span data-ttu-id="57e81-131">Podczas kopiowania hello subskrypcji identyfikator i certyfikat zarządzania, **nie** zawierają hello oferty, które należy ująć hello wartości.</span><span class="sxs-lookup"><span data-stu-id="57e81-131">When copying hello subscription id and management certificate, **do not** include hello quotes that enclose hello values.</span></span>
6. <span data-ttu-id="57e81-132">Polecenie **konfiguracji Sprawdź**.</span><span class="sxs-lookup"><span data-stu-id="57e81-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="57e81-133">Gdy hello konfiguracji nie zostanie pomyślnie zweryfikowana, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="57e81-133">When hello configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a><span data-ttu-id="57e81-134">Konfigurowanie szablonu maszyny wirtualnej dla hello Azure podrzędna dodatku plug-in</span><span class="sxs-lookup"><span data-stu-id="57e81-134">Set up a virtual machine template for hello Azure Slave plug-in</span></span>
<span data-ttu-id="57e81-135">Szablon maszyny wirtualnej definiuje parametry hello hello wtyczki użyje toocreate węzeł podrzędny na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="57e81-135">A virtual machine template defines hello parameters hello plug-in will use toocreate a slave node on Azure.</span></span> <span data-ttu-id="57e81-136">W hello następujące kroki, możemy utworzyć szablon dla maszyny Wirtualnej systemu Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="57e81-136">In hello following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="57e81-137">W hello Hudson pulpitu nawigacyjnego, kliknij przycisk **Zarządzanie Hudson**.</span><span class="sxs-lookup"><span data-stu-id="57e81-137">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="57e81-138">Polecenie **skonfigurować System**.</span><span class="sxs-lookup"><span data-stu-id="57e81-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="57e81-139">Przewiń w dół hello strony toofind hello **chmury** sekcji.</span><span class="sxs-lookup"><span data-stu-id="57e81-139">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="57e81-140">W ramach hello **chmury** sekcji, Znajdź **dodać szablon maszyny wirtualnej Azure** i kliknij przycisk hello **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="57e81-140">Within hello **Cloud** section, find **Add Azure Virtual Machine Template** and click hello **Add** button.</span></span>
   
    ![Dodaj szablon maszyny wirtualnej][add vm template]
5. <span data-ttu-id="57e81-142">Określ nazwę usługi w chmurze w hello **nazwa** pola.</span><span class="sxs-lookup"><span data-stu-id="57e81-142">Specify a cloud service name in hello **Name** field.</span></span> <span data-ttu-id="57e81-143">Jeśli nazwa hello odwołuje się tooan istniejące usługi w chmurze, hello maszyny Wirtualnej zostaną zainicjowane w tej usłudze.</span><span class="sxs-lookup"><span data-stu-id="57e81-143">If hello name you specify refers tooan existing cloud service, hello VM will be provisioned in that service.</span></span> <span data-ttu-id="57e81-144">W przeciwnym razie Azure utworzy nowy.</span><span class="sxs-lookup"><span data-stu-id="57e81-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="57e81-145">W hello **opis** wprowadź tekst, który opisuje tworzysz szablon hello.</span><span class="sxs-lookup"><span data-stu-id="57e81-145">In hello **Description** field, enter text that describes hello template you are creating.</span></span> <span data-ttu-id="57e81-146">Te informacje są tylko do celów dokumentacji i nie jest używany w inicjowania obsługi maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="57e81-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="57e81-147">W hello **etykiety** wprowadź **linux**.</span><span class="sxs-lookup"><span data-stu-id="57e81-147">In hello **Labels** field, enter **linux**.</span></span> <span data-ttu-id="57e81-148">Etykieta jest używane tooidentify hello szablon, który tworzysz i szablon hello tooreference następnie używane podczas tworzenia zadania Hudson.</span><span class="sxs-lookup"><span data-stu-id="57e81-148">This label is used tooidentify hello template you are creating and is subsequently used tooreference hello template when creating a Hudson job.</span></span>
8. <span data-ttu-id="57e81-149">Wybierz region, w którym zostanie utworzona hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="57e81-149">Select a region where hello VM will be created.</span></span>
9. <span data-ttu-id="57e81-150">Wybierz odpowiedni rozmiar maszyny Wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="57e81-150">Select hello appropriate VM size.</span></span>
10. <span data-ttu-id="57e81-151">Określ konto magazynu, w którym zostanie utworzona hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="57e81-151">Specify a storage account where hello VM will be created.</span></span> <span data-ttu-id="57e81-152">Upewnij się, że jest on hello usługi w chmurze hello należy używać tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="57e81-152">Make sure that it is in hello same region as hello cloud service you'll be using.</span></span> <span data-ttu-id="57e81-153">Jeśli chcesz, aby nowe toobe magazynu utworzony, to pole może pozostać puste.</span><span class="sxs-lookup"><span data-stu-id="57e81-153">If you want new storage toobe created, you can leave this field blank.</span></span>
11. <span data-ttu-id="57e81-154">Czas przechowywania określa hello liczbę minut, zanim Hudson usuwa bezczynności podrzędna.</span><span class="sxs-lookup"><span data-stu-id="57e81-154">Retention time specifies hello number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="57e81-155">Pozostaw to wartość domyślna hello 60.</span><span class="sxs-lookup"><span data-stu-id="57e81-155">Leave this at hello default value of 60.</span></span>
12. <span data-ttu-id="57e81-156">W **użycia**, wybierz hello odpowiedniego warunku, gdy będzie można użyć ten węzeł podrzędny.</span><span class="sxs-lookup"><span data-stu-id="57e81-156">In **Usage**, select hello appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="57e81-157">Teraz, wybierz **korzystać z tego węzła możliwie**.</span><span class="sxs-lookup"><span data-stu-id="57e81-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="57e81-158">W tym momencie formularza będzie wyglądać nieco podobne toothis:</span><span class="sxs-lookup"><span data-stu-id="57e81-158">At this point, your form would look somewhat similar toothis:</span></span>
    
     ![Konfiguracja szablonu][template config]
13. <span data-ttu-id="57e81-160">W **rodziny obrazu lub identyfikator** ma toospecify obrazów systemu zostanie zainstalowana na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="57e81-160">In **Image Family or Id** you have toospecify what system image will be installed on your VM.</span></span> <span data-ttu-id="57e81-161">Możesz wybrać z listy obrazów rodzin lub określ niestandardowy obraz.</span><span class="sxs-lookup"><span data-stu-id="57e81-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="57e81-162">Tooselect z listy rodzin obrazu, wprowadź hello pierwszego znaku (z uwzględnieniem wielkości liter) Nazwa rodziny hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="57e81-162">If you want tooselect from a list of image families, enter hello first character (case-sensitive) of hello image family name.</span></span> <span data-ttu-id="57e81-163">Na przykład wpisanie **U** pojawi się lista rodzin Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="57e81-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="57e81-164">Po wybraniu z listy hello Wpięć użyje najnowszej wersji tego obrazu systemu z tej rodziny hello podczas inicjowania obsługi administracyjnej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="57e81-164">Once you select from hello list, Jenkins will use hello latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![Listy rodziny systemów operacyjnych][OS family list]
    
     <span data-ttu-id="57e81-166">Jeśli chcesz toouse niestandardowego obrazu, wprowadź nazwę hello niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="57e81-166">If you have a custom image that you want toouse instead, enter hello name of that custom image.</span></span> <span data-ttu-id="57e81-167">Nazwy niestandardowego obrazu nie są wyświetlane na liście, który pozwala uzyskać tooensure, który hello nazwa został wprowadzony prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="57e81-167">Custom image names are not shown in a list so you have tooensure that hello name is entered correctly.</span></span>    
    
     <span data-ttu-id="57e81-168">W tym samouczku, wpisz **U** toobring listy obrazów Ubuntu i wybierz **Ubuntu Server 14.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="57e81-168">For this tutorial, type **U** toobring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="57e81-169">Dla **uruchamiania metody**, wybierz pozycję **SSH**.</span><span class="sxs-lookup"><span data-stu-id="57e81-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="57e81-170">Poniższy skrypt hello kopiowania i wklejania w hello **skryptu Init** pola.</span><span class="sxs-lookup"><span data-stu-id="57e81-170">Copy hello script below and paste in hello **Init script** field.</span></span>
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     <span data-ttu-id="57e81-171">Witaj **skryptu Init** zostanie wykonany po hello zostanie utworzona maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="57e81-171">hello **Init script** will be executed after hello VM is created.</span></span> <span data-ttu-id="57e81-172">W tym przykładzie skrypt hello instaluje Java, usługi git i ant.</span><span class="sxs-lookup"><span data-stu-id="57e81-172">In this example, hello script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="57e81-173">W hello **Username** i **hasło** pól, wprowadź wartości preferowanych hello konta administratora, który zostanie utworzony na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="57e81-173">In hello **Username** and **Password** fields, enter your preferred values for hello administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="57e81-174">Polecenie **Sprawdź szablon** toocheck, jeśli można określić parametry hello są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="57e81-174">Click on **Verify Template** toocheck if hello parameters you specified are valid.</span></span>
18. <span data-ttu-id="57e81-175">Kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="57e81-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="57e81-176">Utwórz zadanie Hudson uruchamianego na węzeł podrzędny na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="57e81-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="57e81-177">W tej sekcji trzeba utworzyć zadania Hudson, które zostanie uruchomione w węźle podrzędna na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="57e81-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="57e81-178">W hello Hudson pulpitu nawigacyjnego, kliknij przycisk **nowe zadanie**.</span><span class="sxs-lookup"><span data-stu-id="57e81-178">In hello Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="57e81-179">Wprowadź nazwę hello zadania, które tworzysz.</span><span class="sxs-lookup"><span data-stu-id="57e81-179">Enter a name for hello job you are creating.</span></span>
3. <span data-ttu-id="57e81-180">Typ zadania hello wybierz **kompilacji zadanie oprogramowania wolne stylu**.</span><span class="sxs-lookup"><span data-stu-id="57e81-180">For hello job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="57e81-181">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="57e81-181">Click **OK**.</span></span>
5. <span data-ttu-id="57e81-182">Na stronie konfiguracji zadania hello wybierz **Ogranicz, w którym można uruchomić tego projektu**.</span><span class="sxs-lookup"><span data-stu-id="57e81-182">In hello job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="57e81-183">Wybierz **węzła i etykiety menu** i wybierz **linux** (możemy określona etykieta w podczas tworzenia szablonu maszyny wirtualnej hello w poprzedniej sekcji hello).</span><span class="sxs-lookup"><span data-stu-id="57e81-183">Select **Node and label menu** and select **linux** (we specified this label when creating hello virtual machine template in hello previous section).</span></span>
7. <span data-ttu-id="57e81-184">W hello **kompilacji** kliknij **kroku kompilacji Dodaj** i wybierz **wykonywania powłoki**.</span><span class="sxs-lookup"><span data-stu-id="57e81-184">In hello **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="57e81-185">Edytuj hello następującego skryptu, zastępując **{nazwa konta usługi github}**, **{nazwę projektu}**, i **{katalogu projektu}** z odpowiednie wartości, a następnie wklej hello Edytowanie skryptu w hello obszaru tekstu, który pojawia się.</span><span class="sxs-lookup"><span data-stu-id="57e81-185">Edit hello following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste hello edited script in hello text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="57e81-186">Kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="57e81-186">Click on **Save**.</span></span>
10. <span data-ttu-id="57e81-187">W hello Hudson pulpitu nawigacyjnego, Znajdź zadanie hello właśnie utworzony i kliknij pozycję hello **zaplanować kompilacji** ikony.</span><span class="sxs-lookup"><span data-stu-id="57e81-187">In hello Hudson dashboard, find hello job you just created and click on hello **Schedule a build** icon.</span></span>

<span data-ttu-id="57e81-188">Hudson będą utworzyć przy użyciu szablonu hello utworzonego w poprzedniej sekcji hello węzeł podrzędny i uruchom skrypt hello określone w hello kroku kompilacji dla tego zadania.</span><span class="sxs-lookup"><span data-stu-id="57e81-188">Hudson will then create a slave node using hello template created in hello previous section and execute hello script you specified in hello build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57e81-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="57e81-189">Next Steps</span></span>
<span data-ttu-id="57e81-190">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="57e81-190">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[profilu subskrypcji]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

