---
title: "aaaSet się Apache Tomcat na maszynie wirtualnej systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset się Apache Tomcat7 przy użyciu maszyn wirtualnych Azure z systemem Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="79448-103">Konfigurowanie Tomcat7 na maszynie wirtualnej systemu Linux przy użyciu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="79448-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="79448-104">Apache Tomcat (lub po prostu Tomcat, również nazywanych Jakarta Tomcat) to serwer sieci web typu open source i kontener serwlet opracowane przez hello Foundation oprogramowania Apache (ASF).</span><span class="sxs-lookup"><span data-stu-id="79448-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by hello Apache Software Foundation (ASF).</span></span> <span data-ttu-id="79448-105">Tomcat implementuje hello Serwlet Java i hello specyfikacje Sun Microsystems JavaServer Pages (JSP).</span><span class="sxs-lookup"><span data-stu-id="79448-105">Tomcat implements hello Java Servlet and hello JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="79448-106">Tomcat udostępnia czysty środowisko serwera sieci web Java HTTP w których toorun kodu języka Java.</span><span class="sxs-lookup"><span data-stu-id="79448-106">Tomcat provides a pure Java HTTP web server environment in which toorun Java code.</span></span> <span data-ttu-id="79448-107">W hello najprostsza konfiguracja Tomcat działa w procesie jeden system operacyjny.</span><span class="sxs-lookup"><span data-stu-id="79448-107">In hello simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="79448-108">Ten proces jest uruchomiony maszyny wirtualnej Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="79448-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="79448-109">Każde żądanie HTTP z tooTomcat przeglądarki jest przetwarzany jako oddzielnym wątku w procesie Tomcat hello.</span><span class="sxs-lookup"><span data-stu-id="79448-109">Every HTTP request from a browser tooTomcat is processed as a separate thread in hello Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="79448-110">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="79448-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="79448-111">W tym artykule opisano, jak toouse hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="79448-111">This article covers how toouse hello classic deployment model.</span></span> <span data-ttu-id="79448-112">Zaleca się, że większości nowych wdrożeń Użyj modelu Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="79448-112">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="79448-113">Zobacz toouse toodeploy szablon Menedżera zasobów maszyny Wirtualnej systemu Ubuntu JDK otwarte i Tomcat, [w tym artykule](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span><span class="sxs-lookup"><span data-stu-id="79448-113">toouse a Resource Manager template toodeploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="79448-114">W tym artykule zainstalujesz Tomcat7 w obrazie systemu Linux i wdrożyć go na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="79448-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="79448-115">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="79448-115">You will learn:</span></span>  

* <span data-ttu-id="79448-116">Jak toocreate maszynę wirtualną na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="79448-116">How toocreate a virtual machine in Azure.</span></span>
* <span data-ttu-id="79448-117">Jak tooprepare hello maszyny wirtualnej dla Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="79448-117">How tooprepare hello virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="79448-118">Jak tooinstall Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="79448-118">How tooinstall Tomcat7.</span></span>

<span data-ttu-id="79448-119">Zakłada się, że masz już subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="79448-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="79448-120">Jeśli nie, można założyć bezpłatnej wersji próbnej na [hello Azure witryny sieci Web](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="79448-120">If not, you can sign up for a free trial at [hello Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="79448-121">Jeśli masz subskrypcję MSDN, zobacz [specjalne cennik Microsoft Azure: MSDN, MPN i korzyści BizSpark](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span><span class="sxs-lookup"><span data-stu-id="79448-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="79448-122">toolearn więcej informacji na temat usługi Azure, zobacz [co to jest Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span><span class="sxs-lookup"><span data-stu-id="79448-122">toolearn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="79448-123">W tym artykule przyjęto założenie, że masz podstawową wiedzę na temat pracy z Tomcat i Linux.</span><span class="sxs-lookup"><span data-stu-id="79448-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="79448-124">Faza 1: Tworzenie obrazu</span><span class="sxs-lookup"><span data-stu-id="79448-124">Phase 1: Create an image</span></span>
<span data-ttu-id="79448-125">W tej fazie spowoduje utworzenie maszyny wirtualnej za pomocą obrazu systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="79448-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="79448-126">Krok 1: Generowanie klucza uwierzytelniania SSH</span><span class="sxs-lookup"><span data-stu-id="79448-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="79448-127">SSH jest narzędziem ważne dla administratorów systemu.</span><span class="sxs-lookup"><span data-stu-id="79448-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="79448-128">Konfigurowanie zabezpieczeń dostępu na podstawie hasła ustalić ludzkich nie jest jednak zalecane.</span><span class="sxs-lookup"><span data-stu-id="79448-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="79448-129">Złośliwi użytkownicy można podzielić na podstawie nazwy użytkownika i hasło słabe systemu.</span><span class="sxs-lookup"><span data-stu-id="79448-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="79448-130">Dobra wiadomość Hello jest, czy istnieje sposób tooleave dostępu zdalnego Otwórz i nie martw się o hasłach.</span><span class="sxs-lookup"><span data-stu-id="79448-130">hello good news is that there is a way tooleave remote access open and not worry about passwords.</span></span> <span data-ttu-id="79448-131">Ta metoda składa się z uwierzytelniania za pomocą kryptografii asymetrycznej.</span><span class="sxs-lookup"><span data-stu-id="79448-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="79448-132">Witaj klucza prywatnego użytkownika jest hello, który przyznaje hello uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="79448-132">hello user’s private key is hello one that grants hello authentication.</span></span> <span data-ttu-id="79448-133">Można nawet blokować hello konta toonot Zezwalaj na uwierzytelnianie hasła.</span><span class="sxs-lookup"><span data-stu-id="79448-133">You can even lock hello user’s account toonot allow password authentication.</span></span>

<span data-ttu-id="79448-134">Zaletą tej metody jest niepotrzebne toosign różnych haseł w toodifferent serwerów.</span><span class="sxs-lookup"><span data-stu-id="79448-134">Another advantage of this method is that you do not need different passwords toosign in toodifferent servers.</span></span> <span data-ttu-id="79448-135">Można uwierzytelniać za pomocą klucza prywatnego osobistego hello na wszystkich serwerach, co zapobiega konieczności tooremember kilka haseł.</span><span class="sxs-lookup"><span data-stu-id="79448-135">You can authenticate by using hello personal private key on all servers, which prevents you from having tooremember several passwords.</span></span>



<span data-ttu-id="79448-136">Wykonaj te kroki toogenerate hello SSH uwierzytelniania klucza.</span><span class="sxs-lookup"><span data-stu-id="79448-136">Follow these steps toogenerate hello SSH authentication key.</span></span>

1. <span data-ttu-id="79448-137">Pobierz i zainstaluj PuTTYgen z następującej lokalizacji hello: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="79448-137">Download and install PuTTYgen from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="79448-138">Uruchom Puttygen.exe.</span><span class="sxs-lookup"><span data-stu-id="79448-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="79448-139">Kliknij przycisk **Generuj** toogenerate hello kluczy.</span><span class="sxs-lookup"><span data-stu-id="79448-139">Click **Generate** toogenerate hello keys.</span></span> <span data-ttu-id="79448-140">W procesie hello może zwiększyć losowości przez przenoszenie hello myszy nad hello pusty obszar w oknie hello.</span><span class="sxs-lookup"><span data-stu-id="79448-140">In hello process, you can increase randomness by moving hello mouse over hello blank area in hello window.</span></span>  
   <span data-ttu-id="79448-141">![PuTTY zrzut ekranu generatora klucza, pokazujący hello nowego klucza przycisk Generuj][1]</span><span class="sxs-lookup"><span data-stu-id="79448-141">![PuTTY Key Generator screenshot that shows hello generate new key button][1]</span></span>
4. <span data-ttu-id="79448-142">Po hello Generuj proces, Puttygen.exe wyświetli nowy klucz publiczny.</span><span class="sxs-lookup"><span data-stu-id="79448-142">After hello generate process, Puttygen.exe will show your new public key.</span></span>  
   ![PuTTY zrzut ekranu generatora klucza, pokazujący hello nowego klucza publicznego i hello prywatnego klucza przyciskiem Zapisz][2]
5. <span data-ttu-id="79448-144">Zaznacz i skopiuj klucz publiczny hello i zapisz go w pliku o nazwie publicKey.pem.</span><span class="sxs-lookup"><span data-stu-id="79448-144">Select and copy hello public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="79448-145">Nie klikaj pozycji **Zapisz klucz publiczny**, ponieważ jest inny niż klucz publiczny hello chcemy hello zapisanego formatu pliku klucza publicznego.</span><span class="sxs-lookup"><span data-stu-id="79448-145">Don’t click **Save public key**, because hello saved public key’s file format is different from hello public key we want.</span></span>
6. <span data-ttu-id="79448-146">Kliknij przycisk **Zapisz klucz prywatny**i zapisz go w pliku o nazwie privateKey.ppk.</span><span class="sxs-lookup"><span data-stu-id="79448-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a><span data-ttu-id="79448-147">Krok 2: Tworzenie obraz powitania w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="79448-147">Step 2: Create hello image in hello Azure portal</span></span>
1. <span data-ttu-id="79448-148">W hello [portal](https://portal.azure.com/), kliknij przycisk **nowy** w hello zadań paska toocreate obrazu.</span><span class="sxs-lookup"><span data-stu-id="79448-148">In hello [portal](https://portal.azure.com/), click **New** in hello task bar toocreate an image.</span></span> <span data-ttu-id="79448-149">Następnie wybierz obraz systemu Linux hello jest na podstawie Twoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="79448-149">Then choose hello Linux image that is based on your needs.</span></span> <span data-ttu-id="79448-150">Witaj poniższym przykładzie użyto hello Ubuntu 14.04 obrazu.</span><span class="sxs-lookup"><span data-stu-id="79448-150">hello following example uses hello Ubuntu 14.04 image.</span></span>
<span data-ttu-id="79448-151">![Zrzut ekranu przedstawiający portal hello, który zawiera przycisk Nowy hello][3]</span><span class="sxs-lookup"><span data-stu-id="79448-151">![Screenshot of hello portal that shows hello New button][3]</span></span>

2. <span data-ttu-id="79448-152">Aby uzyskać **nazwy hosta**, określ nazwę hello hello adres URL, czy użytkownik i klientów internetowych użyje tooaccess tej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="79448-152">For **Host Name**, specify hello name for hello URL that you and Internet clients will use tooaccess this virtual machine.</span></span> <span data-ttu-id="79448-153">Zdefiniuj hello ostatnia część hello nazwy DNS, na przykład tomcatdemo.</span><span class="sxs-lookup"><span data-stu-id="79448-153">Define hello last part of hello DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="79448-154">Azure będzie generować hello adresu URL jako tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="79448-154">Azure will then generate hello URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="79448-155">Dla **klucz uwierzytelniania SSH**, skopiuj wartość klucza hello z hello publicKey.pem pliku, który zawiera klucz publiczny hello generowane przez PuTTYgen.</span><span class="sxs-lookup"><span data-stu-id="79448-155">For **SSH Authentication Key**, copy hello key value from hello publicKey.pem file, which contains hello public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="79448-156">![Wprowadź klucz uwierzytelniania SSH w portalu hello][4]</span><span class="sxs-lookup"><span data-stu-id="79448-156">![SSH Authentication Key box in hello portal][4]</span></span>

4. <span data-ttu-id="79448-157">Skonfiguruj inne ustawienia, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="79448-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="79448-158">Faza 2: Przygotowanie maszyny wirtualnej do Tomcat7</span><span class="sxs-lookup"><span data-stu-id="79448-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="79448-159">W tym kroku zostanie konfigurowania punktu końcowego dla ruchu Tomcat, a następnie połącz tooyour nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="79448-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect tooyour new virtual machine.</span></span>

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a><span data-ttu-id="79448-160">Krok 1: Otwórz dostęp w sieci web tooallow portu hello HTTP</span><span class="sxs-lookup"><span data-stu-id="79448-160">Step 1: Open hello HTTP port tooallow web access</span></span>
<span data-ttu-id="79448-161">Punkty końcowe platformy Azure składają się z protokołem TCP lub UDP, oraz port publiczny i prywatny.</span><span class="sxs-lookup"><span data-stu-id="79448-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="79448-162">port prywatny Hello jest port hello, że maszyna wirtualna hello tooon nasłuchuje usługa hello.</span><span class="sxs-lookup"><span data-stu-id="79448-162">hello private port is hello port that hello service is listening tooon hello virtual machine.</span></span> <span data-ttu-id="79448-163">port publiczny Hello jest port hello hello usługi w chmurze Azure nasłuchuje tooexternally dla ruchu przychodzącego, internetowego.</span><span class="sxs-lookup"><span data-stu-id="79448-163">hello public port is hello port that hello Azure cloud service listens tooexternally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="79448-164">TCP port 8080 jest hello domyślny numer portu używany toolisten Tomcat.</span><span class="sxs-lookup"><span data-stu-id="79448-164">TCP port 8080 is hello default port number that Tomcat uses toolisten.</span></span> <span data-ttu-id="79448-165">Ten port jest otwarty z punktu końcowego platformy Azure, możesz i innych Klienci internetowi mogą uzyskiwać dostęp stron Tomcat.</span><span class="sxs-lookup"><span data-stu-id="79448-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="79448-166">W portalu powitania kliknij **Przeglądaj** > **maszyn wirtualnych**, a następnie kliknij przycisk hello maszyny wirtualnej, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="79448-166">In hello portal, click **Browse** > **Virtual machines**, and then click hello virtual machine that you created.</span></span>  
   <span data-ttu-id="79448-167">![Zrzut ekranu przedstawiający hello katalogu maszyny wirtualne][5]</span><span class="sxs-lookup"><span data-stu-id="79448-167">![Screenshot of hello Virtual machines directory][5]</span></span>
2. <span data-ttu-id="79448-168">tooadd punktu końcowego maszyny wirtualnej tooyour, kliknij przycisk hello **punkty końcowe** pole.</span><span class="sxs-lookup"><span data-stu-id="79448-168">tooadd an endpoint tooyour virtual machine, click hello **Endpoints** box.</span></span>
   <span data-ttu-id="79448-169">![Zrzut ekranu pokazujący pole punkty końcowe hello][6]</span><span class="sxs-lookup"><span data-stu-id="79448-169">![Screenshot that shows hello Endpoints box][6]</span></span>
3. <span data-ttu-id="79448-170">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="79448-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="79448-171">Dla punktu końcowego hello, wprowadź nazwę dla punktu końcowego hello w **punktu końcowego**, a następnie wprowadź 80 w **Port publiczny**.</span><span class="sxs-lookup"><span data-stu-id="79448-171">For hello endpoint, enter a name for hello endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="79448-172">Jeśli zostanie ustawiona too80, nie potrzebujesz numeru portu hello tooinclude hello adres URL, który jest używany tooaccess Tomcat.</span><span class="sxs-lookup"><span data-stu-id="79448-172">If you set it too80, you don’t need tooinclude hello port number in hello URL that is used tooaccess Tomcat.</span></span> <span data-ttu-id="79448-173">Na przykład http://tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="79448-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="79448-174">Jeśli zostanie ustawiona wartość tooanother, na przykład 81, należy tooadd hello portu numer toohello adres URL tooaccess Tomcat.</span><span class="sxs-lookup"><span data-stu-id="79448-174">If you set it tooanother value, such as 81, you need tooadd hello port number toohello URL tooaccess Tomcat.</span></span> <span data-ttu-id="79448-175">Na przykład http://tomcatdemo.cloudapp.net:81 /.</span><span class="sxs-lookup"><span data-stu-id="79448-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="79448-176">Wprowadź 8080 w **Port prywatny**.</span><span class="sxs-lookup"><span data-stu-id="79448-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="79448-177">Domyślnie Tomcat nasłuchuje na porcie TCP 8080.</span><span class="sxs-lookup"><span data-stu-id="79448-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="79448-178">Zmieniono hello domyślne nasłuchiwania portu Tomcat, należy zaktualizować **Port prywatny** toobe hello tak samo jak hello port nasłuchiwania Tomcat.</span><span class="sxs-lookup"><span data-stu-id="79448-178">If you changed hello default listen port of Tomcat, you should update **Private Port** toobe hello same as hello Tomcat listen port.</span></span>  
      <span data-ttu-id="79448-179">![Zrzut ekranu z interfejsu użytkownika, który zawiera polecenie Dodaj, Port publiczny i Port prywatny][7]</span><span class="sxs-lookup"><span data-stu-id="79448-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="79448-180">Kliknij przycisk **OK** maszyny wirtualnej tooyour tooadd hello punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="79448-180">Click **OK** tooadd hello endpoint tooyour virtual machine.</span></span>

### <a name="step-2-connect-toohello-image-you-created"></a><span data-ttu-id="79448-181">Krok 2: Łączenie toohello obrazu, który został utworzony</span><span class="sxs-lookup"><span data-stu-id="79448-181">Step 2: Connect toohello image you created</span></span>
<span data-ttu-id="79448-182">Można wybrać żadnej maszyny wirtualnej tooyour tooconnect SSH narzędzia.</span><span class="sxs-lookup"><span data-stu-id="79448-182">You can choose any SSH tool tooconnect tooyour virtual machine.</span></span> <span data-ttu-id="79448-183">W tym przykładzie używamy programu PuTTY.</span><span class="sxs-lookup"><span data-stu-id="79448-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="79448-184">Pobierz nazwę DNS hello maszyny wirtualnej z hello portalu.</span><span class="sxs-lookup"><span data-stu-id="79448-184">Get hello DNS name of your virtual machine from hello portal.</span></span>
    1. <span data-ttu-id="79448-185">Kliknij przycisk **Przeglądaj** > **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="79448-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="79448-186">Wybierz nazwę hello maszyny wirtualnej, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="79448-186">Select hello name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="79448-187">W hello **właściwości** kafelka, Szukaj w hello **nazwy domeny** nazwy DNS hello tooget pole.</span><span class="sxs-lookup"><span data-stu-id="79448-187">In hello **Properties** tile, look in hello **Domain Name** box tooget hello DNS name.</span></span>  

2. <span data-ttu-id="79448-188">Pobierz hello numer portu dla połączenia SSH z hello **SSH** pole.</span><span class="sxs-lookup"><span data-stu-id="79448-188">Get hello port number for SSH connections from hello **SSH** box.</span></span>  
<span data-ttu-id="79448-189">![Zrzut ekranu pokazujący numer portu połączenia SSH hello][8]</span><span class="sxs-lookup"><span data-stu-id="79448-189">![Screenshot that shows hello SSH connection port number][8]</span></span>

3. <span data-ttu-id="79448-190">Pobierz [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="79448-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="79448-191">Po pobraniu, kliknij plik wykonywalny hello Putty.exe.</span><span class="sxs-lookup"><span data-stu-id="79448-191">After downloading, click hello executable file Putty.exe.</span></span> <span data-ttu-id="79448-192">W konfiguracji programu PuTTY Konfiguruj opcje Podstawowe hello hello nazwy hosta i portu numer uzyskany z hello właściwości maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="79448-192">In PuTTY configuration, configure hello basic options with hello host name and port number that is obtained from hello properties of your virtual machine.</span></span>   
![Zrzut ekranu pokazujący hello PuTTY konfiguracji hosta, portu i opcje][9]

5. <span data-ttu-id="79448-194">W okienku po lewej stronie powitania kliknij **połączenia** > **SSH** > **uwierzytelniania**, a następnie kliknij przycisk **Przeglądaj** toospecify Lokalizacja Hello hello privateKey.ppk pliku.</span><span class="sxs-lookup"><span data-stu-id="79448-194">In hello left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** toospecify hello location of hello privateKey.ppk file.</span></span> <span data-ttu-id="79448-195">Plik privateKey.ppk Hello zawiera hello klucza prywatnego, który jest generowany przez PuTTYgen we wcześniejszej części hello "faza 1: Tworzenie obrazu" w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="79448-195">hello privateKey.ppk file contains hello private key that is generated by PuTTYgen earlier in hello "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="79448-196">![Zrzut ekranu pokazujący hierarchii katalogów połączenia hello i przycisk przeglądania][10]</span><span class="sxs-lookup"><span data-stu-id="79448-196">![Screenshot that shows hello Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="79448-197">Kliknij przycisk **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="79448-197">Click **Open**.</span></span> <span data-ttu-id="79448-198">Użytkownik może otrzymywać alerty przez okno komunikatu.</span><span class="sxs-lookup"><span data-stu-id="79448-198">You might be alerted by a message box.</span></span> <span data-ttu-id="79448-199">Jeśli skonfigurowano hello nazwę DNS i numer portu poprawnie, kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="79448-199">If you have configured hello DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="79448-200">![Zrzut ekranu pokazujący hello powiadomień][11]</span><span class="sxs-lookup"><span data-stu-id="79448-200">![Screenshot that shows hello notification][11]</span></span>

7. <span data-ttu-id="79448-201">Możesz się zostanie wyświetlony monit o tooenter nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="79448-201">You are prompted tooenter your username.</span></span>  
![Zrzut ekranu pokazujący, gdzie tooenter nazwy użytkownika][12]

8. <span data-ttu-id="79448-203">Wprowadź nazwę użytkownika hello używane maszyny wirtualnej hello toocreate w hello "faza 1: Tworzenie obrazu" wcześniej w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="79448-203">Enter hello username that you used toocreate hello virtual machine in hello "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="79448-204">Zostanie wyświetlony ekran podobny do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="79448-204">You will see something like hello following:</span></span>  
![Zrzut ekranu pokazujący hello uwierzytelniania potwierdzenia][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="79448-206">Faza 3: Instalacja oprogramowania</span><span class="sxs-lookup"><span data-stu-id="79448-206">Phase 3: Install software</span></span>
<span data-ttu-id="79448-207">Na tym etapie należy zainstalować środowisko uruchomieniowe języka Java hello, Tomcat7 i inne składniki Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="79448-207">In this phase, you install hello Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="79448-208">Środowisko uruchomieniowe języka Java</span><span class="sxs-lookup"><span data-stu-id="79448-208">Java runtime environment</span></span>
<span data-ttu-id="79448-209">Tomcat jest napisany w języku Java.</span><span class="sxs-lookup"><span data-stu-id="79448-209">Tomcat is written in Java.</span></span> <span data-ttu-id="79448-210">Istnieją dwa rodzaje Java Development Kit (JDKs), OpenJDK i Oracle JDK.</span><span class="sxs-lookup"><span data-stu-id="79448-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="79448-211">Można wybrać hello żądanego.</span><span class="sxs-lookup"><span data-stu-id="79448-211">You can choose hello one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="79448-212">Zarówno JDKs mają prawie hello sam kod klasy hello w hello interfejsu API języka Java, ale jest różny kod hello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="79448-212">Both JDKs have almost hello same code for hello classes in hello Java API, but hello code for hello virtual machine is different.</span></span> <span data-ttu-id="79448-213">OpenJDK zwykle toouse otwarte biblioteki, podczas gdy zwykle Oracle JDK toouse zamknięte te.</span><span class="sxs-lookup"><span data-stu-id="79448-213">OpenJDK tends toouse open libraries, while Oracle JDK tends toouse closed ones.</span></span> <span data-ttu-id="79448-214">Oracle JDK ma więcej klasy, a niektóre stałe usterek i Oracle JDK jest stabilna więcej niż OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="79448-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="79448-215">Zainstaluj OpenJDK</span><span class="sxs-lookup"><span data-stu-id="79448-215">Install OpenJDK</span></span>  

<span data-ttu-id="79448-216">Użyj następującego polecenia toodownload OpenJDK hello.</span><span class="sxs-lookup"><span data-stu-id="79448-216">Use hello following command toodownload OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="79448-217">toocreate toocontain katalogu hello JDK plików:</span><span class="sxs-lookup"><span data-stu-id="79448-217">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="79448-218">tooextract hello JDK pliki w katalogu/usr/lib/jvm/hello:</span><span class="sxs-lookup"><span data-stu-id="79448-218">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="79448-219">Zainstaluj Oracle JDK</span><span class="sxs-lookup"><span data-stu-id="79448-219">Install Oracle JDK</span></span>


<span data-ttu-id="79448-220">Użyj hello następujące polecenia toodownload Oracle JDK z witryny sieci Web hello Oracle.</span><span class="sxs-lookup"><span data-stu-id="79448-220">Use hello following command toodownload Oracle JDK from hello Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="79448-221">toocreate toocontain katalogu hello JDK plików:</span><span class="sxs-lookup"><span data-stu-id="79448-221">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="79448-222">tooextract hello JDK pliki w katalogu/usr/lib/jvm/hello:</span><span class="sxs-lookup"><span data-stu-id="79448-222">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="79448-223">tooset Oracle JDK jako hello maszyny wirtualnej Java domyślne:</span><span class="sxs-lookup"><span data-stu-id="79448-223">tooset Oracle JDK as hello default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="79448-224">Upewnij się, że Java Instalacja powiodła się</span><span class="sxs-lookup"><span data-stu-id="79448-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="79448-225">Można użyć polecenia, takich jak powitania po tootest środowiska uruchomieniowego hello jest poprawnie zainstalowany:</span><span class="sxs-lookup"><span data-stu-id="79448-225">You can use a command like hello following tootest if hello Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="79448-226">Jeśli zainstalowano OpenJDK, powinien zostać wyświetlony komunikat podobnie następującej hello: ![OpenJDK pomyślnej instalacji wiadomości][14]</span><span class="sxs-lookup"><span data-stu-id="79448-226">If you installed OpenJDK, you should see a message like hello following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="79448-227">Jeśli zainstalowano Oracle JDK, powinien zostać wyświetlony komunikat podobnie następującej hello: ![komunikat instalacji pomyślne JDK Oracle][15]</span><span class="sxs-lookup"><span data-stu-id="79448-227">If you installed Oracle JDK, you should see a message like hello following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="79448-228">Zainstaluj Tomcat7</span><span class="sxs-lookup"><span data-stu-id="79448-228">Install Tomcat7</span></span>
<span data-ttu-id="79448-229">Użyj następującego polecenia tooinstall Tomcat7 hello.</span><span class="sxs-lookup"><span data-stu-id="79448-229">Use hello following command tooinstall Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="79448-230">Jeśli nie używasz Tomcat7, użyj hello odpowiednią odmianę tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="79448-230">If you are not using Tomcat7, use hello appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="79448-231">Upewnij się, że Tomcat7 Instalacja powiodła się</span><span class="sxs-lookup"><span data-stu-id="79448-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="79448-232">Po pomyślnym zainstalowaniu Tomcat7 toocheck Przeglądaj nazwa DNS serwera Tomcat tooyour.</span><span class="sxs-lookup"><span data-stu-id="79448-232">toocheck if Tomcat7 is successfully installed, browse tooyour Tomcat server’s DNS name.</span></span> <span data-ttu-id="79448-233">W tym artykule hello przykładowy adres URL jest http://tomcatexample.cloudapp.net/.</span><span class="sxs-lookup"><span data-stu-id="79448-233">In this article, hello example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="79448-234">Jeśli zostanie wyświetlony komunikat z takich jak następujące hello Tomcat7 jest poprawnie zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="79448-234">If you see a message like hello following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="79448-235">![Komunikat instalacji Tomcat7 powiodło się][16]</span><span class="sxs-lookup"><span data-stu-id="79448-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="79448-236">Instalowanie innych składników Tomcat7</span><span class="sxs-lookup"><span data-stu-id="79448-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="79448-237">Istnieją inne składniki opcjonalne Tomcat, które można zainstalować.</span><span class="sxs-lookup"><span data-stu-id="79448-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="79448-238">Użyj hello **tomcat7 stanie pamięci podręcznej wyszukiwania sudo** toosee polecenia wszystkie dostępne składniki hello.</span><span class="sxs-lookup"><span data-stu-id="79448-238">Use hello **sudo apt-cache search tomcat7** command toosee all of hello available components.</span></span> <span data-ttu-id="79448-239">Użyj następującego polecenia tooinstall hello niektórych składników przydatne.</span><span class="sxs-lookup"><span data-stu-id="79448-239">Use hello following commands tooinstall some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="79448-240">Faza 4: Konfigurowanie Tomcat7</span><span class="sxs-lookup"><span data-stu-id="79448-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="79448-241">Na tym etapie można administrować Tomcat.</span><span class="sxs-lookup"><span data-stu-id="79448-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="79448-242">Uruchamianie i zatrzymywanie Tomcat7</span><span class="sxs-lookup"><span data-stu-id="79448-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="79448-243">Serwer Tomcat7 Hello jest uruchamiana automatycznie po zainstalowaniu go.</span><span class="sxs-lookup"><span data-stu-id="79448-243">hello Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="79448-244">Można również uruchomić z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="79448-244">You can also start it with hello following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="79448-245">toostop Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="79448-245">toostop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="79448-246">Stan hello tooview Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="79448-246">tooview hello status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="79448-247">toorestart Tomcat usługi:</span><span class="sxs-lookup"><span data-stu-id="79448-247">toorestart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="79448-248">Administracja Tomcat7</span><span class="sxs-lookup"><span data-stu-id="79448-248">Tomcat7 administration</span></span>
<span data-ttu-id="79448-249">Można edytować hello Tomcat użytkownika konfiguracji pliku tooset się swoje poświadczenia administratora.</span><span class="sxs-lookup"><span data-stu-id="79448-249">You can edit hello Tomcat user configuration file tooset up your admin credentials.</span></span> <span data-ttu-id="79448-250">Witaj Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="79448-250">Use hello following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="79448-251">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="79448-251">Here is an example:</span></span>  
![Zrzut ekranu pokazujący hello sudo vi polecenia w danych wyjściowych][17]  

> [!NOTE]
> <span data-ttu-id="79448-253">Utwórz silne hasło dla nazwy użytkownika administratora hello.</span><span class="sxs-lookup"><span data-stu-id="79448-253">Create a strong password for hello admin username.</span></span>  

<span data-ttu-id="79448-254">Po zmodyfikowaniu tego pliku, należy ponownie uruchomić usługi Tomcat7 z hello tooensure polecenia czy hello zmiany zostały wprowadzone następujące:</span><span class="sxs-lookup"><span data-stu-id="79448-254">After editing this file, you should restart Tomcat7 services with hello following command tooensure that hello changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="79448-255">Otwórz przeglądarkę i wprowadź **http://<your tomcat server DNS name>/Menedżera/html** jako hello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="79448-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as hello URL.</span></span> <span data-ttu-id="79448-256">Na przykład hello w tym artykule adres URL hello jest http://tomcatexample.cloudapp.net/manager/html.</span><span class="sxs-lookup"><span data-stu-id="79448-256">For hello example in this article, hello URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="79448-257">Po połączeniu, powinny być widoczne następujące toohello coś podobnego:</span><span class="sxs-lookup"><span data-stu-id="79448-257">After connecting, you should see something similar toohello following:</span></span>  
![Zrzut ekranu przedstawiający hello Menedżer aplikacji sieci Web Tomcat][18]

## <a name="common-issues"></a><span data-ttu-id="79448-259">Typowe problemy</span><span class="sxs-lookup"><span data-stu-id="79448-259">Common issues</span></span>
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a><span data-ttu-id="79448-260">Nie można uzyskać dostęp do maszyny wirtualnej hello Tomcat i Moodle z hello Internet</span><span class="sxs-lookup"><span data-stu-id="79448-260">Can't access hello virtual machine with Tomcat and Moodle from hello Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="79448-261">Objaw</span><span class="sxs-lookup"><span data-stu-id="79448-261">Symptom</span></span>  
  <span data-ttu-id="79448-262">Tomcat jest uruchomiony, ale nie widać hello Tomcat domyślną stronę w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="79448-262">Tomcat is running but you can’t see hello Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="79448-263">Możliwe przyczyny</span><span class="sxs-lookup"><span data-stu-id="79448-263">Possible root cause</span></span>   

  * <span data-ttu-id="79448-264">port nasłuchu Tomcat Hello nie jest hello taki sam jak port prywatny hello punktu końcowego maszyny wirtualnej dla ruchu Tomcat.</span><span class="sxs-lookup"><span data-stu-id="79448-264">hello Tomcat listen port is not hello same as hello private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="79448-265">Sprawdź portu publicznego i prywatnego portu ustawienia punktu końcowego i upewnij się, że port prywatny hello jest taki sam, jak hello Tomcat hello nasłuchiwać portu.</span><span class="sxs-lookup"><span data-stu-id="79448-265">Check your public port and private port endpoint settings and make sure hello private port is hello same as hello Tomcat listen port.</span></span> <span data-ttu-id="79448-266">Zobacz "faza 1: Tworzenie obrazu" tego artykułu, aby uzyskać instrukcje dotyczące konfigurowania punktów końcowych dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="79448-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="79448-267">Witaj toodetermine Tomcat nasłuchiwać portu, otwórz /etc/httpd/conf/httpd.conf (Red Hat release) lub /etc/tomcat7/server.xml (wersja Debian).</span><span class="sxs-lookup"><span data-stu-id="79448-267">toodetermine hello Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="79448-268">Domyślnie program hello port nasłuchiwania Tomcat jest 8080.</span><span class="sxs-lookup"><span data-stu-id="79448-268">By default, hello Tomcat listen port is 8080.</span></span> <span data-ttu-id="79448-269">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="79448-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="79448-270">Jeśli używasz maszynę wirtualną, takie jak Debian i Ubuntu i mają toochange hello domyślnego portu z Tomcat nasłuchiwania (na przykład 8081), należy również otworzyć port hello hello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="79448-270">If you are using a virtual machine like Debian or Ubuntu and you want toochange hello default port of Tomcat Listen (for example 8081), you should also open hello port for hello operating system.</span></span> <span data-ttu-id="79448-271">Najpierw otwórz profilu hello:</span><span class="sxs-lookup"><span data-stu-id="79448-271">First, open hello profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="79448-272">Następnie usuń komentarz hello ostatniego wiersza i zmień "nie" za "yes".</span><span class="sxs-lookup"><span data-stu-id="79448-272">Then uncomment hello last line and change “no” too“yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="79448-273">Zapora Hello wyłączył hello nasłuchiwania portu Tomcat.</span><span class="sxs-lookup"><span data-stu-id="79448-273">hello firewall has disabled hello listen port of Tomcat.</span></span>

     <span data-ttu-id="79448-274">Może zobaczyć tylko hello Tomcat domyślną stronę z hello hosta lokalnego.</span><span class="sxs-lookup"><span data-stu-id="79448-274">You can only see hello Tomcat default page from hello local host.</span></span> <span data-ttu-id="79448-275">Hello problem jest najbardziej prawdopodobne, że hello portu, który jest nasłuch tooby Tomcat, jest blokowany przez zaporę hello.</span><span class="sxs-lookup"><span data-stu-id="79448-275">hello problem is most likely that hello port, which is listened tooby Tomcat, is blocked by hello firewall.</span></span> <span data-ttu-id="79448-276">Możesz użyć hello w3m narzędzie toobrowse hello strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="79448-276">You can use hello w3m tool toobrowse hello webpage.</span></span> <span data-ttu-id="79448-277">Witaj następujące polecenia Zainstaluj w3m i Przeglądaj toohello Tomcat domyślnej strony:</span><span class="sxs-lookup"><span data-stu-id="79448-277">hello following commands install w3m and browse toohello Tomcat default page:</span></span>  


        <span data-ttu-id="79448-278">sudo yum instalacji w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="79448-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="79448-279">w3m adresem http://localhost: 8080</span><span class="sxs-lookup"><span data-stu-id="79448-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="79448-280">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="79448-280">Solution</span></span>

  * <span data-ttu-id="79448-281">Jeśli hello port nasłuchiwania Tomcat nie jest hello sam jako port prywatny hello punktu końcowego hello maszyny wirtualnej toohello ruchu, należy zmienić port prywatny hello toobe hello tak samo jak hello port nasłuchiwania Tomcat.</span><span class="sxs-lookup"><span data-stu-id="79448-281">If hello Tomcat listen port is not hello same as hello private port of hello endpoint for traffic toohello virtual machine, you need change hello private port toobe hello same as hello Tomcat listen port.</span></span>   
  2. <span data-ttu-id="79448-282">Jeśli problem hello jest spowodowany przez zaporę/iptables, Dodaj następujące wiersze zbyt/etc/sysconfig/iptables hello.</span><span class="sxs-lookup"><span data-stu-id="79448-282">If hello issue is caused by firewall/iptables, add hello following lines too/etc/sysconfig/iptables.</span></span> <span data-ttu-id="79448-283">drugi wiersz Hello jest potrzebna tylko dla ruchu https:</span><span class="sxs-lookup"><span data-stu-id="79448-283">hello second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="79448-284">-A -p tcp -m tcp--dport 80 -j AKCEPTUJ wejściowych</span><span class="sxs-lookup"><span data-stu-id="79448-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="79448-285">-A -p tcp -m tcp--dport 443 -j AKCEPTUJ wejściowych</span><span class="sxs-lookup"><span data-stu-id="79448-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="79448-286">Upewnij się, że wierszy poprzedniej hello są pozycjonowane powyżej, które globalnie ograniczałyby dostępu, takich jak hello następujące: - wejściowych -j Odrzuć — Odrzuć with zabronione hostów protokołu icmp</span><span class="sxs-lookup"><span data-stu-id="79448-286">Make sure hello previous lines are positioned above any lines that would globally restrict access, such as hello following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="79448-287">tooreload hello iptables, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="79448-287">tooreload hello iptables, run hello following command:</span></span>

    service iptables restart

<span data-ttu-id="79448-288">To została przetestowana CentOS 6.3.</span><span class="sxs-lookup"><span data-stu-id="79448-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a><span data-ttu-id="79448-289">Pozwolono podczas ładowania projektu pliki zbyt/var/lib/tomcat7/webapps /</span><span class="sxs-lookup"><span data-stu-id="79448-289">Permission denied when you upload project files too/var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="79448-290">Objaw</span><span class="sxs-lookup"><span data-stu-id="79448-290">Symptom</span></span>
  <span data-ttu-id="79448-291">Gdy maszynę wirtualną tooyour tooconnect SFTP klienta (na przykład FileZilla) i przejdź zbyt/var/lib/tomcat7/webapps/toopublish witryny, zostanie wyświetlony błąd komunikat podobny toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="79448-291">When you use an SFTP client (such as FileZilla) tooconnect tooyour virtual machine and navigate too/var/lib/tomcat7/webapps/ toopublish your site, you get an error message similar toohello following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="79448-292">Możliwe przyczyny</span><span class="sxs-lookup"><span data-stu-id="79448-292">Possible root cause</span></span>
  <span data-ttu-id="79448-293">Nie masz żadnych uprawnień tooaccess hello /var/lib/tomcat7/webapps folderu.</span><span class="sxs-lookup"><span data-stu-id="79448-293">You have no permissions tooaccess hello /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="79448-294">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="79448-294">Solution</span></span>  
  <span data-ttu-id="79448-295">Wymagane jest uprawnienie tooget z hello konta głównego.</span><span class="sxs-lookup"><span data-stu-id="79448-295">You need tooget permission from hello root account.</span></span> <span data-ttu-id="79448-296">Nazwa głównego toohello użytkownika używane podczas przydzielania maszyny hello, można zmienić hello prawo własności do tego folderu.</span><span class="sxs-lookup"><span data-stu-id="79448-296">You can change hello ownership of that folder from root toohello username you used when you provisioned hello machine.</span></span> <span data-ttu-id="79448-297">Oto przykład nazwą konta azureuser hello:</span><span class="sxs-lookup"><span data-stu-id="79448-297">Here is an example with hello azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="79448-298">Użyj zbyt hello -R — opcja tooapply hello uprawnienia dla wszystkich plików w katalogu.</span><span class="sxs-lookup"><span data-stu-id="79448-298">Use hello -R option tooapply hello permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="79448-299">To polecenie działa również w przypadku katalogów.</span><span class="sxs-lookup"><span data-stu-id="79448-299">This command also works for directories.</span></span> <span data-ttu-id="79448-300">zmiany opcji -R Hello hello uprawnienia dla wszystkich plików i katalogów w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="79448-300">hello -R option changes hello permissions for all files and directories inside hello directory.</span></span> <span data-ttu-id="79448-301">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="79448-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="79448-302">To polecenie powoduje zmianę własności (użytkowników i grup) dla wszystkich plików i katalogów, które znajdują się w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="79448-302">This command changes ownership (both user and group) for all files and directories that are inside hello directory.</span></span>  

  <span data-ttu-id="79448-303">Witaj następujące polecenie tylko zmienia uprawnienia hello hello folder katalogu.</span><span class="sxs-lookup"><span data-stu-id="79448-303">hello following command only changes hello permission of hello folder directory.</span></span> <span data-ttu-id="79448-304">Witaj pliki i foldery w katalogu hello nie są zmieniane.</span><span class="sxs-lookup"><span data-stu-id="79448-304">hello files and folders inside hello directory are not changed.</span></span>  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
