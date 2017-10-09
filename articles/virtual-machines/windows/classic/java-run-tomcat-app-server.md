---
title: Serwer aplikacji Java aaaRun w klasycznym maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Ten samouczek używa zasobów utworzone za pomocą hello klasycznego modelu wdrażania i pokazuje, jak toocreate wirtualnej systemu Windows maszyny i skonfiguruj go toorun Apache Tomcat aplikacji serwera."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="cd264-103">Jak toorun serwer aplikacji Java na maszynie wirtualnej utworzone z hello klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="cd264-103">How toorun a Java application server on a virtual machine created with hello classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cd264-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="cd264-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cd264-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="cd264-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="cd264-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cd264-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="cd264-107">Aby toodeploy szablon Menedżera zasobów aplikacji sieci Web Java 8 i Tomcat, zobacz [tutaj](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span><span class="sxs-lookup"><span data-stu-id="cd264-107">For a Resource Manager template toodeploy a webapp with Java 8 and Tomcat, see [here](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span></span>

<span data-ttu-id="cd264-108">Przy użyciu platformy Azure można użyć funkcji serwera tooprovide maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cd264-108">With Azure, you can use a virtual machine tooprovide server capabilities.</span></span> <span data-ttu-id="cd264-109">Na przykład maszynę wirtualną działającą na platformie Azure można toohost skonfigurowanego serwera aplikacji Java, takich jak Apache Tomcat.</span><span class="sxs-lookup"><span data-stu-id="cd264-109">As an example, a virtual machine running on Azure can be configured toohost a Java application server, such as Apache Tomcat.</span></span>

<span data-ttu-id="cd264-110">Po zakończeniu pracy w tym przewodniku, trzeba będzie zrozumienia sposobu toocreate maszynę wirtualną działających na platformie Azure i skonfigurować go toorun serwera aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="cd264-110">After completing this guide, you will have an understanding of how toocreate a virtual machine running on Azure and configure it toorun a Java application server.</span></span> <span data-ttu-id="cd264-111">Zostanie Dowiedz się i wykonaj następujące zadania hello:</span><span class="sxs-lookup"><span data-stu-id="cd264-111">You will learn and perform hello following tasks:</span></span>

* <span data-ttu-id="cd264-112">Jak toocreate wirtualnej maszynie, która ma Java Development Kit (JDK) już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="cd264-112">How toocreate a virtual machine that has a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="cd264-113">Jak zarejestrować tooremotely tooyour maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cd264-113">How tooremotely sign in tooyour virtual machine.</span></span>
* <span data-ttu-id="cd264-114">Jak tooinstall serwer aplikacji Java — Apache Tomcat — na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cd264-114">How tooinstall a Java application server--Apache Tomcat--on your virtual machine.</span></span>
* <span data-ttu-id="cd264-115">Jak toocreate punktu końcowego dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cd264-115">How toocreate an endpoint for your virtual machine.</span></span>
* <span data-ttu-id="cd264-116">Jak tooopen portu w hello zapory dla serwera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cd264-116">How tooopen a port in hello firewall for your application server.</span></span>

<span data-ttu-id="cd264-117">Witaj zakończone wyniki instalacji w Tomcat uruchomione na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cd264-117">hello completed installation results in Tomcat running on a virtual machine.</span></span>

![Maszyna wirtualna z systemem Apache Tomcat][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a><span data-ttu-id="cd264-119">toocreate maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cd264-119">toocreate a virtual machine</span></span>
1. <span data-ttu-id="cd264-120">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cd264-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="cd264-121">Kliknij przycisk **nowy**, kliknij przycisk **obliczeniowe**, następnie kliknij przycisk **zobaczyć wszystkie** w hello **wyróżnionych aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="cd264-121">Click **New**, click **Compute**, then click **See all** in hello **Featured apps**.</span></span>
3. <span data-ttu-id="cd264-122">Kliknij przycisk **JDK**, kliknij przycisk **JDK 8** w hello **JDK** okienka.</span><span class="sxs-lookup"><span data-stu-id="cd264-122">Click **JDK**, click **JDK 8** in hello **JDK** pane.</span></span>  
   <span data-ttu-id="cd264-123">Maszyny wirtualnej obrazy obsługujące **JDK 6** i **JDK 7** są dostępne, jeśli masz starsze aplikacje, które nie są gotowe toorun JDK 8.</span><span class="sxs-lookup"><span data-stu-id="cd264-123">Virtual machine images that support **JDK 6** and **JDK 7** are available if you have legacy applications that are not ready toorun in JDK 8.</span></span>
4. <span data-ttu-id="cd264-124">Wybierz w okienku hello JDK 8 **klasycznego**, następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="cd264-124">In hello JDK 8 pane, select **Classic**, then click **Create**.</span></span>
5. <span data-ttu-id="cd264-125">W hello **podstawy** bloku:</span><span class="sxs-lookup"><span data-stu-id="cd264-125">In hello **Basics** blade:</span></span>
   1. <span data-ttu-id="cd264-126">Określ nazwę hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cd264-126">Specify a name for hello virtual machine.</span></span>
   2. <span data-ttu-id="cd264-127">Wprowadź nazwę administratora hello w hello **nazwy użytkownika** pola.</span><span class="sxs-lookup"><span data-stu-id="cd264-127">Enter a name for hello administrator in hello **User Name** field.</span></span> <span data-ttu-id="cd264-128">Należy pamiętać, ta nazwa i hello skojarzone hasło w hello następnego pola.</span><span class="sxs-lookup"><span data-stu-id="cd264-128">Remember this name and hello associated password that follows in hello next field.</span></span> <span data-ttu-id="cd264-129">Należy je podczas zdalnego logowania toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cd264-129">You need them when you remotely sign in toohello virtual machine.</span></span>
   3. <span data-ttu-id="cd264-130">Wprowadź hasło w hello **nowe hasło** pola, a następnie wprowadź je ponownie w hello **Potwierdź hasło** pola.</span><span class="sxs-lookup"><span data-stu-id="cd264-130">Enter a password in hello **New password** field, and reenter it in hello **Confirm password** field.</span></span> <span data-ttu-id="cd264-131">Jest to hasło dla konta administratora hello.</span><span class="sxs-lookup"><span data-stu-id="cd264-131">This password is for hello Administrator account.</span></span>
   4. <span data-ttu-id="cd264-132">Wybierz odpowiednie hello **subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="cd264-132">Select hello appropriate **Subscription**.</span></span>
   5. <span data-ttu-id="cd264-133">Dla hello **grupy zasobów**, kliknij przycisk **Utwórz nowy** , a następnie wprowadź nazwę hello nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="cd264-133">For hello **Resource group**, click **Create new** and enter hello name of a new resource group.</span></span> <span data-ttu-id="cd264-134">Lub kliknij przycisk **Użyj istniejącego** i wybierz jedną z hello dostępnych grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="cd264-134">Or, click **Use existing** and select one of hello available resource groups.</span></span>
   6. <span data-ttu-id="cd264-135">Wybierz lokalizację, w którym hello znajduje się maszyna wirtualna, takich jak **południowo-środkowe stany**.</span><span class="sxs-lookup"><span data-stu-id="cd264-135">Select a location where hello virtual machine resides, such as **South Central US**.</span></span>
6. <span data-ttu-id="cd264-136">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="cd264-136">Click **Next**.</span></span>
7. <span data-ttu-id="cd264-137">W hello **rozmiar obrazu maszyny wirtualnej** bloku, wybierz opcję **A1 standardowe** lub inny odpowiedni obraz.</span><span class="sxs-lookup"><span data-stu-id="cd264-137">In hello **Virtual machine image size** blade, select **A1 Standard** or another appropriate image.</span></span>
8. <span data-ttu-id="cd264-138">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="cd264-138">Click **Select**.</span></span>

9. <span data-ttu-id="cd264-139">W hello **ustawienia** bloku, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="cd264-139">In hello **Settings** blade, click **OK**.</span></span> <span data-ttu-id="cd264-140">Można użyć wartości domyślnych hello przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="cd264-140">You can use hello default values provided by Azure.</span></span>  
10. <span data-ttu-id="cd264-141">W hello **Podsumowanie** bloku, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="cd264-141">In hello **Summary** blade, click **OK**.</span></span>

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a><span data-ttu-id="cd264-142">tooremotely logowania tooyour maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cd264-142">tooremotely sign in tooyour virtual machine</span></span>
1. <span data-ttu-id="cd264-143">Zaloguj się na toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cd264-143">Log on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cd264-144">Kliknij przycisk **maszyn wirtualnych (klasyczne)**.</span><span class="sxs-lookup"><span data-stu-id="cd264-144">Click **Virtual machines (classic)**.</span></span> <span data-ttu-id="cd264-145">W razie potrzeby kliknij **więcej usług** na powitania lewym dolnym rogu hello usługi kategoriach.</span><span class="sxs-lookup"><span data-stu-id="cd264-145">If needed, click **More services** at hello bottom left corner under hello service categories.</span></span> <span data-ttu-id="cd264-146">Witaj **maszyn wirtualnych (klasyczne)** wpis ma na liście hello **obliczeniowe** grupy.</span><span class="sxs-lookup"><span data-stu-id="cd264-146">hello **Virtual machines (classic)** entry is listed in hello **Compute** group.</span></span>
3. <span data-ttu-id="cd264-147">Kliknij nazwę hello hello maszyny wirtualnej, który chcesz toosign w.</span><span class="sxs-lookup"><span data-stu-id="cd264-147">Click hello name of hello virtual machine that you want toosign in to.</span></span>
4. <span data-ttu-id="cd264-148">Po uruchomieniu maszyny wirtualnej hello, menu u góry okienka hello hello zezwala na połączenia.</span><span class="sxs-lookup"><span data-stu-id="cd264-148">After hello virtual machine has started, a menu at hello top of hello pane allows connections.</span></span>
5. <span data-ttu-id="cd264-149">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="cd264-149">Click **Connect**.</span></span>
6. <span data-ttu-id="cd264-150">Odpowiedz monity toohello jako maszyna wirtualna toohello tooconnect potrzebne.</span><span class="sxs-lookup"><span data-stu-id="cd264-150">Respond toohello prompts as needed tooconnect toohello virtual machine.</span></span> <span data-ttu-id="cd264-151">Zwykle Zapisz lub Otwórz plik RDP hello zawierający szczegóły połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="cd264-151">Typically, you save or open hello .rdp file that contains hello connection details.</span></span> <span data-ttu-id="cd264-152">Może mieć hello toocopy adresu url: port jako ostatnia część hello pierwszy wiersz pliku RDP hello hello i wklej go w aplikacji zdalnej logowania.</span><span class="sxs-lookup"><span data-stu-id="cd264-152">You might have toocopy hello url:port as hello last part of hello first line of hello .rdp file and paste it in a remote sign-in application.</span></span>

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a><span data-ttu-id="cd264-153">tooinstall serwer aplikacji Java na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cd264-153">tooinstall a Java application server on your virtual machine</span></span>
<span data-ttu-id="cd264-154">Możesz skopiować maszynę wirtualną tooyour serwera aplikacji Java lub zainstalować serwer aplikacji Java za pomocą Instalatora.</span><span class="sxs-lookup"><span data-stu-id="cd264-154">You can copy a Java application server tooyour virtual machine, or you can install a Java application server through an installer.</span></span>

<span data-ttu-id="cd264-155">Ten samouczek używa Tomcat jako tooinstall serwera aplikacji Java hello.</span><span class="sxs-lookup"><span data-stu-id="cd264-155">This tutorial uses Tomcat as hello Java application server tooinstall.</span></span>

1. <span data-ttu-id="cd264-156">Gdy użytkownik jest zalogowany tooyour maszyny wirtualnej, otwórz sesję przeglądarki zbyt[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span><span class="sxs-lookup"><span data-stu-id="cd264-156">When you are signed in tooyour virtual machine, open a browser session too[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span></span>
2. <span data-ttu-id="cd264-157">Kliknij dwukrotnie łącze hello **Instalator usługi Windows 32-bitowe/64-bitowych**.</span><span class="sxs-lookup"><span data-stu-id="cd264-157">Double-click hello link for **32-bit/64-bit Windows Service Installer**.</span></span> <span data-ttu-id="cd264-158">Korzystając z tej techniki, Tomcat jest instalowany jako usługa systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="cd264-158">By using this technique, Tomcat installs as a Windows service.</span></span>
3. <span data-ttu-id="cd264-159">Po wyświetleniu monitu wybierz toorun hello Instalatora.</span><span class="sxs-lookup"><span data-stu-id="cd264-159">When prompted, choose toorun hello installer.</span></span>
4. <span data-ttu-id="cd264-160">W ramach hello **Apache Tomcat Instalator** monituje Kreator, wykonaj hello tooinstall Tomcat.</span><span class="sxs-lookup"><span data-stu-id="cd264-160">Within hello **Apache Tomcat Setup** wizard, follow hello prompts tooinstall Tomcat.</span></span> <span data-ttu-id="cd264-161">Witaj celów tego samouczka akceptując wartości domyślne hello funkcjonuje prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="cd264-161">For hello purposes of this tutorial, accepting hello defaults is fine.</span></span> <span data-ttu-id="cd264-162">Po przejściu hello **hello Kończenie pracy Kreatora instalacji programu Apache Tomcat** okno dialogowe, można opcjonalnie sprawdzić **Uruchom Apache Tomcat** toohave teraz start Tomcat.</span><span class="sxs-lookup"><span data-stu-id="cd264-162">When you reach hello **Completing hello Apache Tomcat Setup Wizard** dialog box, you can optionally check **Run Apache Tomcat** toohave Tomcat start now.</span></span> <span data-ttu-id="cd264-163">Kliknij przycisk **Zakończ** toocomplete hello Tomcat procesu instalacji.</span><span class="sxs-lookup"><span data-stu-id="cd264-163">Click **Finish** toocomplete hello Tomcat setup process.</span></span>

## <a name="toostart-tomcat"></a><span data-ttu-id="cd264-164">toostart Tomcat</span><span class="sxs-lookup"><span data-stu-id="cd264-164">toostart Tomcat</span></span>

<span data-ttu-id="cd264-165">Możesz ręcznie uruchomić Tomcat Otwieranie wiersza polecenia na maszynie wirtualnej i uruchomione polecenie hello **net&nbsp;start&nbsp;Tomcat8**.</span><span class="sxs-lookup"><span data-stu-id="cd264-165">You can manually start Tomcat by opening a command prompt on your virtual machine and running hello command **net&nbsp;start&nbsp;Tomcat8**.</span></span>

<span data-ttu-id="cd264-166">Po uruchomieniu Tomcat, można uzyskać dostęp Tomcat, wprowadzając adres URL hello <adresem http://localhost: 8080> w przeglądarce maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="cd264-166">Once Tomcat is running, you can access Tomcat by entering hello URL <http://localhost:8080> in hello virtual machine's browser.</span></span>

<span data-ttu-id="cd264-167">toosee Tomcat uruchomiona z zewnętrznych komputerów, należy toocreate punktu końcowego i otworzyć port.</span><span class="sxs-lookup"><span data-stu-id="cd264-167">toosee Tomcat running from external machines, you need toocreate an endpoint and open a port.</span></span>

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a><span data-ttu-id="cd264-168">toocreate punktu końcowego dla maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cd264-168">toocreate an endpoint for your virtual machine</span></span>
1. <span data-ttu-id="cd264-169">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cd264-169">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cd264-170">Kliknij przycisk **maszyn wirtualnych (klasyczne)**.</span><span class="sxs-lookup"><span data-stu-id="cd264-170">Click **Virtual machines (classic)**.</span></span>
3. <span data-ttu-id="cd264-171">Kliknij nazwę hello hello maszyny wirtualnej, która jest uruchomiony serwer aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="cd264-171">Click hello name of hello virtual machine that is running your Java application server.</span></span>
4. <span data-ttu-id="cd264-172">Kliknij przycisk **Punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="cd264-172">Click **Endpoints**.</span></span>
5. <span data-ttu-id="cd264-173">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="cd264-173">Click **Add**.</span></span>
6. <span data-ttu-id="cd264-174">W hello **dodać punkt końcowy** okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="cd264-174">In hello **Add endpoint** dialog box:</span></span>
   1. <span data-ttu-id="cd264-175">Określ nazwę dla punktu końcowego hello; na przykład **HttpIn**.</span><span class="sxs-lookup"><span data-stu-id="cd264-175">Specify a name for hello endpoint; for example, **HttpIn**.</span></span>
   2. <span data-ttu-id="cd264-176">Wybierz **TCP** protokołu hello.</span><span class="sxs-lookup"><span data-stu-id="cd264-176">Select **TCP** for hello protocol.</span></span>
   3. <span data-ttu-id="cd264-177">Określ **80** hello portu publicznego.</span><span class="sxs-lookup"><span data-stu-id="cd264-177">Specify **80** for hello public port.</span></span>
   4. <span data-ttu-id="cd264-178">Określ **8080** dla hello port prywatny.</span><span class="sxs-lookup"><span data-stu-id="cd264-178">Specify **8080** for hello private port.</span></span>
   5. <span data-ttu-id="cd264-179">Wybierz **wyłączone** dla hello pływającego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="cd264-179">Select **Disabled** for hello floating IP address.</span></span>
   6. <span data-ttu-id="cd264-180">Pozostaw hello listy kontroli dostępu jest.</span><span class="sxs-lookup"><span data-stu-id="cd264-180">Leave hello access control list as is.</span></span>
   7. <span data-ttu-id="cd264-181">Kliknij przycisk hello **OK** przycisk hello tooclose — okno dialogowe i utworzyć punktu końcowego hello.</span><span class="sxs-lookup"><span data-stu-id="cd264-181">Click hello **OK** button tooclose hello dialog box and create hello endpoint.</span></span>

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a><span data-ttu-id="cd264-182">tooopen port w Zaporze Windows hello dla maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cd264-182">tooopen a port in hello firewall for your virtual machine</span></span>
1. <span data-ttu-id="cd264-183">Zaloguj się tooyour maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cd264-183">Sign in tooyour virtual machine.</span></span>
2. <span data-ttu-id="cd264-184">Kliknij przycisk **Start systemu Windows**.</span><span class="sxs-lookup"><span data-stu-id="cd264-184">Click **Windows Start**.</span></span>
3. <span data-ttu-id="cd264-185">Kliknij przycisk **Panel sterowania**.</span><span class="sxs-lookup"><span data-stu-id="cd264-185">Click **Control Panel**.</span></span>
4. <span data-ttu-id="cd264-186">Kliknij przycisk **System i zabezpieczenia**, kliknij przycisk **zapory systemu Windows**, a następnie kliknij przycisk **Zaawansowane ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="cd264-186">Click **System and Security**, click **Windows Firewall**, and then click **Advanced Settings**.</span></span>
5. <span data-ttu-id="cd264-187">Kliknij przycisk **reguły ruchu przychodzącego**, a następnie kliknij przycisk **nową regułę**.</span><span class="sxs-lookup"><span data-stu-id="cd264-187">Click **Inbound Rules**, and then click **New Rule**.</span></span>  
   <span data-ttu-id="cd264-188">![Nowej reguły ruchu przychodzącego][NewIBRule]</span><span class="sxs-lookup"><span data-stu-id="cd264-188">![New inbound rule][NewIBRule]</span></span>
6. <span data-ttu-id="cd264-189">Dla hello **typ reguły**, wybierz pozycję **portu**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cd264-189">For hello **Rule Type**, select **Port**, and then click **Next**.</span></span>  
   <span data-ttu-id="cd264-190">![Nowy port reguły dla ruchu przychodzącego][NewRulePort]</span><span class="sxs-lookup"><span data-stu-id="cd264-190">![New inbound rule port][NewRulePort]</span></span>
7. <span data-ttu-id="cd264-191">Na powitania **protokoły i porty** ekranu wybierz **TCP**, określ **8080** jako hello **określonych portów lokalnych**, a następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="cd264-191">On hello **Protocol and Ports** screen, select **TCP**, specify **8080** as hello **Specific local port**, and then click **Next**.</span></span>  
  <span data-ttu-id="cd264-192">![Nowej reguły ruchu przychodzącego][NewRuleProtocol]</span><span class="sxs-lookup"><span data-stu-id="cd264-192">![New inbound rule ][NewRuleProtocol]</span></span>
8. <span data-ttu-id="cd264-193">Na powitania **akcji** ekranu wybierz **przyłączenia hello**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cd264-193">On hello **Action** screen, select **Allow hello connection**, and then click **Next**.</span></span>
   <span data-ttu-id="cd264-194">![Nowa akcja reguły dla ruchu przychodzącego][NewRuleAction]</span><span class="sxs-lookup"><span data-stu-id="cd264-194">![New inbound rule action][NewRuleAction]</span></span>
9. <span data-ttu-id="cd264-195">Na powitania **profilu** ekranu, upewnij się, że **domeny**, **prywatnej**, i **publicznego** są zaznaczone, a następnie kliknij przycisk **dalej** .</span><span class="sxs-lookup"><span data-stu-id="cd264-195">On hello **Profile** screen, ensure that **Domain**, **Private**, and **Public** are selected, and then click **Next**.</span></span>
   <span data-ttu-id="cd264-196">![Nowy profil reguły dla ruchu przychodzącego][NewRuleProfile]</span><span class="sxs-lookup"><span data-stu-id="cd264-196">![New inbound rule profile][NewRuleProfile]</span></span>
10. <span data-ttu-id="cd264-197">Na powitania **nazwa** ekranu, określ nazwę reguły hello, takich jak **HttpIn** (hello Nazwa reguły nie jest wymagane toomatch hello Nazwa punktu końcowego, jednak), a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="cd264-197">On hello **Name** screen, specify a name for hello rule, such as **HttpIn** (hello rule name is not required toomatch hello endpoint name, however), and then click **Finish**.</span></span>  
    <span data-ttu-id="cd264-198">![Nazwa nowej reguły ruchu przychodzącego][NewRuleName]</span><span class="sxs-lookup"><span data-stu-id="cd264-198">![New inbound rule name][NewRuleName]</span></span>

<span data-ttu-id="cd264-199">W tym momencie witryny sieci Web Tomcat powinien być widoczny z zewnętrznej przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="cd264-199">At this point, your Tomcat website should be viewable from an external browser.</span></span> <span data-ttu-id="cd264-200">W oknie przeglądarki hello adresu wpisz adres URL formularza hello  **http://*Twojego\_DNS\_nazwa*. cloudapp.net**, gdzie ***Twojego\_DNS\_nazwa*** jest określony, podczas tworzenia maszyny wirtualnej hello nazwa DNS hello.</span><span class="sxs-lookup"><span data-stu-id="cd264-200">In hello browser's address window, type a URL of hello form **http://*your\_DNS\_name*.cloudapp.net**, where ***your\_DNS\_name*** is hello DNS name you specified when you created hello virtual machine.</span></span>

## <a name="application-lifecycle-considerations"></a><span data-ttu-id="cd264-201">Zagadnienia dotyczące cyklu życia aplikacji</span><span class="sxs-lookup"><span data-stu-id="cd264-201">Application lifecycle considerations</span></span>
* <span data-ttu-id="cd264-202">Można tworzyć własne archiwum aplikacji sieci web (plik WAR) i dodaj go toohello **webapps** folderu.</span><span class="sxs-lookup"><span data-stu-id="cd264-202">You could create your own web application archive (WAR) and add it toohello **webapps** folder.</span></span> <span data-ttu-id="cd264-203">Na przykład Tworzenie podstawowego projektu sieci web dynamiczne strony usługi Java (JSP) i wyeksportować go jako plik WAR.</span><span class="sxs-lookup"><span data-stu-id="cd264-203">For example, create a basic Java Service Page (JSP) dynamic web project and export it as a WAR file.</span></span> <span data-ttu-id="cd264-204">Następnie skopiuj hello WAR toohello Apache Tomcat **webapps** folderu na maszynie wirtualnej hello, następnie uruchom go w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="cd264-204">Next, copy hello WAR toohello Apache Tomcat **webapps** folder on hello virtual machine, then run it in a browser.</span></span>
* <span data-ttu-id="cd264-205">Domyślnie po zainstalowaniu usługi Tomcat hello jest ustawiona toostart ręcznie.</span><span class="sxs-lookup"><span data-stu-id="cd264-205">By default when hello Tomcat service is installed, it is set toostart manually.</span></span> <span data-ttu-id="cd264-206">Możesz przełączyć go toostart automatycznie za pomocą przystawki usługi hello.</span><span class="sxs-lookup"><span data-stu-id="cd264-206">You can switch it toostart automatically by using hello Services snap-in.</span></span> <span data-ttu-id="cd264-207">Uruchom przystawkę usługi hello klikając **Start systemu Windows**, **narzędzia administracyjne**, a następnie **usług**.</span><span class="sxs-lookup"><span data-stu-id="cd264-207">Start hello Services snap-in by clicking **Windows Start**, **Administrative Tools**, and then **Services**.</span></span> <span data-ttu-id="cd264-208">Kliknij dwukrotnie hello **Apache Tomcat** usługi i ustaw **uruchamiana** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="cd264-208">Double-click hello **Apache Tomcat** service and set **Startup type** too**Automatic**.</span></span>

    ![Ustawienie toostart usługi automatycznie][service_automatic_startup]

    <span data-ttu-id="cd264-210">Witaj o konieczności Tomcat automatycznego uruchamiania jest czy rozpoczyna działanie po ponownym uruchomieniu maszyny wirtualnej hello (na przykład po zainstalowaniu aktualizacji oprogramowania, które wymagają ponownego uruchomienia).</span><span class="sxs-lookup"><span data-stu-id="cd264-210">hello benefit of having Tomcat start automatically is that it starts running when hello virtual machine is rebooted (for example, after software updates that require a reboot are installed).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd264-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cd264-211">Next steps</span></span>
<span data-ttu-id="cd264-212">Informacje na temat innych usług (takich jak magazynu Azure, magistrali usług i bazy danych SQL), które mogą zostać tooinclude z aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="cd264-212">You can learn about other services (such as Azure Storage, service bus, and SQL Database) that you may want tooinclude with your Java applications.</span></span> <span data-ttu-id="cd264-213">Wyświetl hello informacje są dostępne na powitania [Centrum deweloperów języka Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="cd264-213">View hello information available at hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
