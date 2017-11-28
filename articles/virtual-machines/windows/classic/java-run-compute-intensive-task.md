---
title: intensywnie aaaCompute aplikacji Java na maszynie Wirtualnej | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate maszyny wirtualnej platformy Azure, uruchomionym aplikacji Java obliczeniowych, które mogą być monitorowane przez inną aplikację Java."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a><span data-ttu-id="e5257-103">Jak zadanie toorun obliczeniowych w języku Java na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e5257-103">How toorun a compute-intensive task in Java on a virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="e5257-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e5257-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e5257-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="e5257-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e5257-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e5257-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="e5257-107">Przy użyciu platformy Azure możesz użyć zadań obliczeniowych toohandle maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5257-107">With Azure, you can use a virtual machine toohandle compute-intensive tasks.</span></span> <span data-ttu-id="e5257-108">Na przykład maszynę wirtualną można realizacji zadań i dostarczać wyniki tooclient maszyny lub aplikacji dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="e5257-108">For example, a virtual machine can handle tasks and deliver results tooclient machines or mobile applications.</span></span> <span data-ttu-id="e5257-109">Po przeczytaniu tego artykułu, trzeba będzie zrozumienia sposobu toocreate maszynę wirtualną działającą aplikację Java obliczeniowych mogą być monitorowane przez inną aplikację Java.</span><span class="sxs-lookup"><span data-stu-id="e5257-109">After reading this article, you will have an understanding of how toocreate a virtual machine that runs a compute-intensive Java application that can be monitored by another Java application.</span></span>

<span data-ttu-id="e5257-110">W tym samouczku założono, że wiesz, jak toocreate Java aplikacji konsoli, można zaimportować aplikacji Java tooyour bibliotek i może powodować generowanie archiwum Java (JAR).</span><span class="sxs-lookup"><span data-stu-id="e5257-110">This tutorial assumes you know how toocreate Java console applications, can import libraries tooyour Java application, and can generate a Java archive (JAR).</span></span> <span data-ttu-id="e5257-111">Przyjęto, że nie wie, Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e5257-111">No knowledge of Microsoft Azure is assumed.</span></span>

<span data-ttu-id="e5257-112">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="e5257-112">You will learn:</span></span>

* <span data-ttu-id="e5257-113">Jak toocreate maszynę wirtualną z Java Development Kit (JDK) już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="e5257-113">How toocreate a virtual machine with a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="e5257-114">Jak tooremotely zalogować tooyour maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5257-114">How tooremotely log in tooyour virtual machine.</span></span>
* <span data-ttu-id="e5257-115">Jak toocreate usługi magistrali przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="e5257-115">How toocreate a service bus namespace.</span></span>
* <span data-ttu-id="e5257-116">Jak toocreate aplikacji Java, która wykonuje zadanie obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="e5257-116">How toocreate a Java application that performs a compute-intensive task.</span></span>
* <span data-ttu-id="e5257-117">Jak toocreate aplikacji Java, która monitoruje hello postęp zadania obliczeniowych hello.</span><span class="sxs-lookup"><span data-stu-id="e5257-117">How toocreate a Java application that monitors hello progress of hello compute-intensive task.</span></span>
* <span data-ttu-id="e5257-118">Jak toorun hello aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="e5257-118">How toorun hello Java applications.</span></span>
* <span data-ttu-id="e5257-119">Jak toostop hello aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="e5257-119">How toostop hello Java applications.</span></span>

<span data-ttu-id="e5257-120">W tym samouczku będzie używać hello Problem sprzedawcy Traveling hello obliczeniowych zadań.</span><span class="sxs-lookup"><span data-stu-id="e5257-120">This tutorial will use hello Traveling Salesman Problem for hello compute-intensive task.</span></span> <span data-ttu-id="e5257-121">Witaj poniżej znajduje się przykład hello Java aplikacji uruchomionej hello obliczeniowych zadania.</span><span class="sxs-lookup"><span data-stu-id="e5257-121">hello following is an example of hello Java application running hello compute-intensive task.</span></span>

![Solver sprzedawcy Traveling Problem][solver_output]

<span data-ttu-id="e5257-123">Witaj poniżej znajduje się przykład hello zadanie obliczeniowych hello monitorowania aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="e5257-123">hello following is an example of hello Java application monitoring hello compute-intensive task.</span></span>

![Problem sprzedawcy Traveling klienta][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a><span data-ttu-id="e5257-125">toocreate maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e5257-125">toocreate a virtual machine</span></span>
1. <span data-ttu-id="e5257-126">Zaloguj się za toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e5257-126">Log in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e5257-127">Kliknij przycisk **nowy**, kliknij przycisk **obliczeniowe**, kliknij przycisk **maszyny wirtualnej**, a następnie kliknij przycisk **z galerii**.</span><span class="sxs-lookup"><span data-stu-id="e5257-127">Click **New**, click **Compute**, click **Virtual machine**, and then click **From Gallery**.</span></span>
3. <span data-ttu-id="e5257-128">W hello **wybierz obraz maszyny wirtualnej** okno dialogowe, wybierz opcję **JDK 7 systemu Windows Server 2012**.</span><span class="sxs-lookup"><span data-stu-id="e5257-128">In hello **Virtual machine image select** dialog box, select **JDK 7 Windows Server 2012**.</span></span>
   <span data-ttu-id="e5257-129">Należy pamiętać, że **JDK 6 systemu Windows Server 2012** jest dostępna w przypadku, gdy masz starsze aplikacje, które nie są jeszcze gotowy toorun w JDK 7.</span><span class="sxs-lookup"><span data-stu-id="e5257-129">Note that **JDK 6 Windows Server 2012** is available in case you have legacy applications that are not yet ready toorun in JDK 7.</span></span>
4. <span data-ttu-id="e5257-130">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="e5257-130">Click **Next**.</span></span>
5. <span data-ttu-id="e5257-131">W hello **konfiguracji maszyny wirtualnej** okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="e5257-131">In hello **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="e5257-132">Określ nazwę hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5257-132">Specify a name for hello virtual machine.</span></span>
   2. <span data-ttu-id="e5257-133">Określ toouse rozmiar hello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5257-133">Specify hello size toouse for hello virtual machine.</span></span>
   3. <span data-ttu-id="e5257-134">Wprowadź nazwę administratora hello w hello **nazwy użytkownika** pola.</span><span class="sxs-lookup"><span data-stu-id="e5257-134">Enter a name for hello administrator in hello **User Name** field.</span></span> <span data-ttu-id="e5257-135">Zapamiętaj to hasło nazwy i hello wprowadzanymi przez użytkownika będzie dalej, użyjesz ich podczas zdalnego logowania toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5257-135">Remember this name and hello password you will enter next, you will use them when you remotely log in toohello virtual machine.</span></span>
   4. <span data-ttu-id="e5257-136">Wprowadź hasło w hello **nowe hasło** pól i wprowadź go ponownie w hello **Potwierdź** pola.</span><span class="sxs-lookup"><span data-stu-id="e5257-136">Enter a password in hello **New password** field, and re-enter it in hello **Confirm** field.</span></span> <span data-ttu-id="e5257-137">Jest to hasło konta administratora hello.</span><span class="sxs-lookup"><span data-stu-id="e5257-137">This is hello Administrator account password.</span></span>
   5. <span data-ttu-id="e5257-138">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="e5257-138">Click **Next**.</span></span>
6. <span data-ttu-id="e5257-139">W hello dalej **konfiguracji maszyny wirtualnej** okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="e5257-139">In hello next **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="e5257-140">Dla **usługi w chmurze**, użyj domyślnej hello **Utwórz nową usługę w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="e5257-140">For **Cloud service**, use hello default **Create a new cloud service**.</span></span>
   2. <span data-ttu-id="e5257-141">Witaj wartość **nazwa DNS usługi w chmurze** musi być unikatowa w cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="e5257-141">hello value for **Cloud service DNS name** must be unique across cloudapp.net.</span></span> <span data-ttu-id="e5257-142">W razie potrzeby zmodyfikuj tę wartość, tym Azure oznacza jest unikatowa.</span><span class="sxs-lookup"><span data-stu-id="e5257-142">If needed, modify this value so that Azure indicates it is unique.</span></span>
   3. <span data-ttu-id="e5257-143">Określ region, grupę koligacji lub sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5257-143">Specify a region, affinity group, or virtual network.</span></span> <span data-ttu-id="e5257-144">Do celów tego samouczka, określ region, takich jak **zachodnie stany USA**.</span><span class="sxs-lookup"><span data-stu-id="e5257-144">For purposes of this tutorial, specify a region such as **West US**.</span></span>
   4. <span data-ttu-id="e5257-145">Dla **konta magazynu**, wybierz pozycję **użyć konta magazynu automatycznie generowanych**.</span><span class="sxs-lookup"><span data-stu-id="e5257-145">For **Storage Account**, select **Use an automatically generated storage account**.</span></span>
   5. <span data-ttu-id="e5257-146">Aby uzyskać **zestawu dostępności**, wybierz pozycję **(Brak)**.</span><span class="sxs-lookup"><span data-stu-id="e5257-146">For **Availability Set**, select **(None)**.</span></span>
   6. <span data-ttu-id="e5257-147">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="e5257-147">Click **Next**.</span></span>
7. <span data-ttu-id="e5257-148">W ostatnim hello **konfiguracji maszyny wirtualnej** okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="e5257-148">In hello final **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="e5257-149">Zaakceptuj hello domyślnych wpisów punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="e5257-149">Accept hello default endpoint entries.</span></span>
   2. <span data-ttu-id="e5257-150">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="e5257-150">Click **Complete**.</span></span>

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a><span data-ttu-id="e5257-151">Dziennik tooremotely w tooyour maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e5257-151">tooremotely log in tooyour virtual machine</span></span>
1. <span data-ttu-id="e5257-152">Zaloguj się na toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e5257-152">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e5257-153">Kliknij przycisk **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="e5257-153">Click **Virtual machines**.</span></span>
3. <span data-ttu-id="e5257-154">Kliknij nazwę hello hello maszyny wirtualnej, który chcesz toolog w.</span><span class="sxs-lookup"><span data-stu-id="e5257-154">Click hello name of hello virtual machine that you want toolog in to.</span></span>
4. <span data-ttu-id="e5257-155">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="e5257-155">Click **Connect**.</span></span>
5. <span data-ttu-id="e5257-156">Odpowiedz monity toohello jako maszyna wirtualna toohello tooconnect potrzebne.</span><span class="sxs-lookup"><span data-stu-id="e5257-156">Respond toohello prompts as needed tooconnect toohello virtual machine.</span></span> <span data-ttu-id="e5257-157">Po wyświetleniu monitu dla hello nazwę i hasło administratora, należy użyć wartości hello, podanych podczas tworzenia maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="e5257-157">When prompted for hello administrator name and password, use hello values that you provided when you created hello virtual machine.</span></span>

<span data-ttu-id="e5257-158">Uwaga tej funkcji usługi Azure Service Bus hello wymaga toobe certyfikat główny firmy CyberTrust Baltimore hello zainstalowane w ramach Twojego środowiska JRE **cacerts** przechowywania.</span><span class="sxs-lookup"><span data-stu-id="e5257-158">Note that hello Azure Service Bus functionality requires hello Baltimore CyberTrust Root certificate toobe installed as part of your JRE's **cacerts** store.</span></span> <span data-ttu-id="e5257-159">Ten certyfikat jest automatycznie uwzględnione w hello Java Runtime Environment (JRE) używane w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="e5257-159">This certificate is automatically included in hello Java Runtime Environment (JRE) used by this tutorial.</span></span> <span data-ttu-id="e5257-160">Jeśli nie masz ten certyfikat w Twojej środowiska JRE **cacerts** przechowywania, zobacz [Dodawanie toohello certyfikatu z magazynu certyfikatów urzędu certyfikacji Java] [ add_ca_cert] informacji na temat dodawania go (a także informacje o wyświetlaniu hello certyfikaty w magazynie cacerts).</span><span class="sxs-lookup"><span data-stu-id="e5257-160">If you do not have this certificate in your JRE **cacerts** store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert] for information on adding it (as well as information on viewing hello certificates in your cacerts store).</span></span>

## <a name="how-toocreate-a-service-bus-namespace"></a><span data-ttu-id="e5257-161">Jak toocreate usługi magistrali przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="e5257-161">How toocreate a service bus namespace</span></span>
<span data-ttu-id="e5257-162">kolejkuje toobegin przy użyciu usługi Service Bus na platformie Azure, musisz najpierw utworzyć przestrzeń nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="e5257-162">toobegin using Service Bus queues in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="e5257-163">Przestrzeń nazw usługi zapewnia kontener zakresu na potrzeby adresowania zasobów usługi Service Bus w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e5257-163">A service namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="e5257-164">toocreate przestrzeni nazw usługi:</span><span class="sxs-lookup"><span data-stu-id="e5257-164">toocreate a service namespace:</span></span>

1. <span data-ttu-id="e5257-165">Zaloguj się na toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e5257-165">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e5257-166">W okienku nawigacji w lewym dolnym hello hello klasycznego portalu Azure, kliknij przycisk **usługi Service Bus, kontroli dostępu i buforowanie**.</span><span class="sxs-lookup"><span data-stu-id="e5257-166">In hello lower-left navigation pane of hello Azure classic portal, click **Service Bus, Access Control & Caching**.</span></span>
3. <span data-ttu-id="e5257-167">W okienku lewej górnej hello hello klasycznego portalu Azure, kliknij przycisk hello **usługi Service Bus** węzeł, a następnie kliknij przycisk hello **nowy** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e5257-167">In hello upper-left pane of hello Azure classic portal, click hello **Service Bus** node, and then click hello **New** button.</span></span>  
   <span data-ttu-id="e5257-168">![Zrzut ekranu węzeł magistrali usług][svc_bus_node]</span><span class="sxs-lookup"><span data-stu-id="e5257-168">![Service Bus Node screenshot][svc_bus_node]</span></span>
4. <span data-ttu-id="e5257-169">W hello **tworzenie nowych Namespace usługi** okna dialogowego wprowadź **Namespace**, a następnie kliknij przycisk toomake się, że jest unikatowa, **Sprawdź dostępność** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e5257-169">In hello **Create a new Service Namespace** dialog box, enter a **Namespace**, and then toomake sure that it is unique, click the **Check Availability** button.</span></span>  
   <span data-ttu-id="e5257-170">![Utwórz nowy Namespace zrzut ekranu][create_namespace]</span><span class="sxs-lookup"><span data-stu-id="e5257-170">![Create a New Namespace screenshot][create_namespace]</span></span>
5. <span data-ttu-id="e5257-171">Po upewnieniu się, hello przestrzeni nazw jest dostępna, wybierz kraj lub region, w którym ma być hostowana przestrzeni nazw, a następnie kliknij hello **utworzyć Namespace** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e5257-171">After making sure hello namespace name is available, choose the country or region in which your namespace should be hosted, and then click hello **Create Namespace** button.</span></span>  
   
   <span data-ttu-id="e5257-172">utworzona przestrzeń nazw Hello pojawi się w hello klasycznego portalu Azure i przejście tooactivate chwilę.</span><span class="sxs-lookup"><span data-stu-id="e5257-172">hello namespace you created will then appear in hello Azure classic portal and takes a moment tooactivate.</span></span> <span data-ttu-id="e5257-173">Poczekaj, aż stan hello jest **Active** przed kontynuowaniem hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="e5257-173">Wait until hello status is **Active** before continuing with hello next step.</span></span>

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a><span data-ttu-id="e5257-174">Uzyskiwanie hello domyślnych poświadczeń zarządzania dla przestrzeni nazw hello</span><span class="sxs-lookup"><span data-stu-id="e5257-174">Obtain hello Default Management Credentials for hello namespace</span></span>
<span data-ttu-id="e5257-175">W operacji zarządzania tooperform kolejności, takich jak tworzenie kolejki w nowej przestrzeni nazw hello należy tooobtain hello zarządzania poświadczenia dla przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="e5257-175">In order tooperform management operations, such as creating a queue, on hello new namespace, you need tooobtain hello management credentials for the namespace.</span></span>

1. <span data-ttu-id="e5257-176">W okienku nawigacji po lewej stronie powitania kliknij hello **usługi Service Bus** węzeł, aby wyświetlić hello listę dostępnych przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="e5257-176">In hello left navigation pane, click hello **Service Bus** node to display hello list of available namespaces.</span></span>
   <span data-ttu-id="e5257-177">![Dostępne obszary nazw zrzut ekranu][avail_namespaces]</span><span class="sxs-lookup"><span data-stu-id="e5257-177">![Available Namespaces screenshot][avail_namespaces]</span></span>
2. <span data-ttu-id="e5257-178">Wybierz obszar nazw hello, nowo utworzoną z wyświetlonej listy hello.</span><span class="sxs-lookup"><span data-stu-id="e5257-178">Select hello namespace you just created from hello list shown.</span></span>
   <span data-ttu-id="e5257-179">![Zrzut ekranu listy Namespace][namespace_list]</span><span class="sxs-lookup"><span data-stu-id="e5257-179">![Namespace List screenshot][namespace_list]</span></span>
3. <span data-ttu-id="e5257-180">po prawej stronie powitania **właściwości** okienko zawiera listę właściwości hello nowej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="e5257-180">hello right-hand **Properties** pane lists hello properties for the new namespace.</span></span>
   <span data-ttu-id="e5257-181">![Zrzut ekranu okienka właściwości][properties_pane]</span><span class="sxs-lookup"><span data-stu-id="e5257-181">![Properties Pane screenshot][properties_pane]</span></span>
4. <span data-ttu-id="e5257-182">Witaj **domyślny klucz** jest ukryty.</span><span class="sxs-lookup"><span data-stu-id="e5257-182">hello **Default Key** is hidden.</span></span> <span data-ttu-id="e5257-183">Kliknij przycisk hello **widoku** przycisk poświadczenia zabezpieczeń hello toodisplay.</span><span class="sxs-lookup"><span data-stu-id="e5257-183">Click hello **View** button toodisplay hello security credentials.</span></span>
   <span data-ttu-id="e5257-184">![Zrzut ekranu klucz domyślny][default_key]</span><span class="sxs-lookup"><span data-stu-id="e5257-184">![Default Key screenshot][default_key]</span></span>
5. <span data-ttu-id="e5257-185">Zanotuj hello **domyślne wystawcy** i hello **domyślny klucz** jako użyje tych informacji poniżej tooperform operacje z przestrzenią nazw.</span><span class="sxs-lookup"><span data-stu-id="e5257-185">Make a note of hello **Default Issuer** and hello **Default Key** as you will use this information below tooperform operations with the namespace.</span></span>

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a><span data-ttu-id="e5257-186">Jak toocreate aplikacji Java, która wykonuje zadanie obliczeniowych</span><span class="sxs-lookup"><span data-stu-id="e5257-186">How toocreate a Java application that performs a compute-intensive task</span></span>
1. <span data-ttu-id="e5257-187">Na komputerze deweloperskim (który nie ma maszyny wirtualnej na powitania toobe utworzony), Pobierz hello [zestawu Azure SDK dla języka Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="e5257-187">On your development machine (which does not have toobe hello virtual machine that you created), download hello [Azure SDK for Java](https://azure.microsoft.com/develop/java/).</span></span>
2. <span data-ttu-id="e5257-188">Utwórz aplikację konsoli języka Java przy użyciu hello przykładowy kod na końcu hello w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="e5257-188">Create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="e5257-189">W tym samouczku użyjemy **TSPSolver.java** jako nazwa pliku hello Java.</span><span class="sxs-lookup"><span data-stu-id="e5257-189">In this tutorial, we'll use **TSPSolver.java** as hello Java file name.</span></span> <span data-ttu-id="e5257-190">Modyfikowanie hello **Twojego\_usługi\_magistrali\_przestrzeni nazw**, **Twojego\_usługi\_magistrali\_właściciela**i **Twojego\_usługi\_magistrali\_klucza** toouse symbole zastępcze z usługi service bus **przestrzeni nazw**, **domyślne wystawcy** i  **Domyślny klucz** wartości odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="e5257-190">Modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
3. <span data-ttu-id="e5257-191">Po kodowania, eksportu hello aplikacji tooa do uruchomienia Java archiwum (JAR) i hello pakietu wymaganych bibliotek na powitania wygenerowany JAR.</span><span class="sxs-lookup"><span data-stu-id="e5257-191">After coding, export hello application tooa runnable Java archive (JAR), and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="e5257-192">W tym samouczku użyjemy **TSPSolver.jar** jako nazwa JAR hello wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="e5257-192">In this tutorial, we'll use **TSPSolver.jar** as hello generated JAR name.</span></span>

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often tooprovide an update toohello console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a><span data-ttu-id="e5257-193">Jak toocreate aplikacji Java, która monitoruje hello postęp zadania obliczeniowych hello</span><span class="sxs-lookup"><span data-stu-id="e5257-193">How toocreate a Java application that monitors hello progress of hello compute-intensive task</span></span>
1. <span data-ttu-id="e5257-194">Na komputerze deweloperskim Utwórz aplikację konsoli języka Java przy użyciu hello przykładowy kod na końcu hello w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="e5257-194">On your development machine, create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="e5257-195">W tym samouczku użyjemy **TSPClient.java** jako nazwa pliku hello Java.</span><span class="sxs-lookup"><span data-stu-id="e5257-195">In this tutorial, we'll use **TSPClient.java** as hello Java file name.</span></span> <span data-ttu-id="e5257-196">Jak pokazano wcześniej, zmodyfikuj hello **Twojego\_usługi\_magistrali\_przestrzeni nazw**, **Twojego\_usługi\_magistrali\_właściciela**, i **Twojego\_usługi\_magistrali\_klucza** toouse symbole zastępcze z usługi service bus **przestrzeni nazw**, **domyślne wystawcy**i **domyślny klucz** wartości odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="e5257-196">As shown earlier, modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
2. <span data-ttu-id="e5257-197">Eksportuj tooa aplikacji hello JAR do uruchomienia i pakietów hello wymaganych bibliotek na powitania wygenerowany JAR.</span><span class="sxs-lookup"><span data-stu-id="e5257-197">Export hello application tooa runnable JAR, and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="e5257-198">W tym samouczku użyjemy **TSPClient.jar** jako nazwa JAR hello wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="e5257-198">In this tutorial, we'll use **TSPClient.jar** as hello generated JAR name.</span></span>

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display hello queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-toorun-hello-java-applications"></a><span data-ttu-id="e5257-199">Jak toorun hello aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="e5257-199">How toorun hello Java applications</span></span>
<span data-ttu-id="e5257-200">Uruchamianie aplikacji obliczeniowych hello, pierwszy toocreate hello kolejki, a następnie toosolve hello podróży Saleseman Problem, który doda hello bieżącego najlepszą trasę toohello kolejką usługi service bus.</span><span class="sxs-lookup"><span data-stu-id="e5257-200">Run hello compute-intensive application, first toocreate hello queue, then toosolve hello Traveling Saleseman Problem, which will add hello current best route toohello service bus queue.</span></span> <span data-ttu-id="e5257-201">Podczas hello obliczeniowych aplikacja jest uruchomiona (lub później), wykonywania powitania klienta toodisplay wyników z kolejką usługi service bus hello.</span><span class="sxs-lookup"><span data-stu-id="e5257-201">While hello compute-intensive application is running (or afterwards), run hello client toodisplay results from hello service bus queue.</span></span>

### <a name="toorun-hello-compute-intensive-application"></a><span data-ttu-id="e5257-202">toorun hello obliczeniowych aplikacji</span><span class="sxs-lookup"><span data-stu-id="e5257-202">toorun hello compute-intensive application</span></span>
1. <span data-ttu-id="e5257-203">Zaloguj się na tooyour maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5257-203">Log on tooyour virtual machine.</span></span>
2. <span data-ttu-id="e5257-204">Utwórz folder, w którym będzie działała aplikacja sieci.</span><span class="sxs-lookup"><span data-stu-id="e5257-204">Create a folder where you will run your application.</span></span> <span data-ttu-id="e5257-205">Na przykład **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="e5257-205">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="e5257-206">Kopiuj **TSPSolver.jar** za**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="e5257-206">Copy **TSPSolver.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="e5257-207">Utwórz plik o nazwie **c:\TSP\cities.txt** z powitania po zawartości.</span><span class="sxs-lookup"><span data-stu-id="e5257-207">Create a file named **c:\TSP\cities.txt** with hello following contents.</span></span>
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. <span data-ttu-id="e5257-208">W wierszu polecenia Zmień tooc:\TSP katalogów.</span><span class="sxs-lookup"><span data-stu-id="e5257-208">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="e5257-209">Upewnij się, że folder bin hello JRE znajduje się w zmiennej środowiskowej PATH hello.</span><span class="sxs-lookup"><span data-stu-id="e5257-209">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
7. <span data-ttu-id="e5257-210">Musisz kolejką usługi service bus toocreate hello przed rozpoczęciem powitalne TSP solver permutacji.</span><span class="sxs-lookup"><span data-stu-id="e5257-210">You'll need toocreate hello service bus queue before you run hello TSP solver permutations.</span></span> <span data-ttu-id="e5257-211">Witaj uruchom następujące polecenie kolejką usługi service bus toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="e5257-211">Run hello following command toocreate hello service bus queue.</span></span>
   
        java -jar TSPSolver.jar createqueue
8. <span data-ttu-id="e5257-212">Teraz, gdy hello Trwa tworzenie kolejki, możesz uruchomić hello TSP solver permutacji.</span><span class="sxs-lookup"><span data-stu-id="e5257-212">Now that hello queue is created, you can run hello TSP solver permutations.</span></span> <span data-ttu-id="e5257-213">Na przykład uruchom hello następujące polecenia toorun hello solver dla 8 miast.</span><span class="sxs-lookup"><span data-stu-id="e5257-213">For example, run hello following command toorun hello solver for 8 cities.</span></span>
   
        java -jar TSPSolver.jar 8
   
   <span data-ttu-id="e5257-214">Jeśli nie określisz numeru, zostanie on uruchomiony dla 10 miast.</span><span class="sxs-lookup"><span data-stu-id="e5257-214">If you don't specify a number, it will run for 10 cities.</span></span> <span data-ttu-id="e5257-215">Jak hello znalezieniem bieżącego najkrótszy tras, spowoduje to dodanie ich toohello kolejki.</span><span class="sxs-lookup"><span data-stu-id="e5257-215">As hello solver finds current shortest routes, it will add them toohello queue.</span></span>

> [!NOTE]
> <span data-ttu-id="e5257-216">Liczba, że określono, zostanie uruchomiony dłużej solver hello hello hello Hello większy.</span><span class="sxs-lookup"><span data-stu-id="e5257-216">hello larger hello number that you specify, hello longer hello solver will run.</span></span> <span data-ttu-id="e5257-217">Na przykład uruchomiony 14 miasta może potrwać kilka minut i uruchamiane przez 15 miasta może zająć kilka godzin.</span><span class="sxs-lookup"><span data-stu-id="e5257-217">For example, running for 14 cities could take several minutes, and running for 15 cities could take several hours.</span></span> <span data-ttu-id="e5257-218">Zwiększenie too16 lub więcej miast może spowodować dni środowiska uruchomieniowego (ostatecznie tygodnie, miesiące i lata).</span><span class="sxs-lookup"><span data-stu-id="e5257-218">Increasing too16 or more cities could result in days of runtime (eventually weeks, months, and years).</span></span> <span data-ttu-id="e5257-219">Jest to powodu toohello szybki wzrost hello liczbę permutacji obliczone przez moduł rozwiązywania hello jako hello liczba wzrasta miast.</span><span class="sxs-lookup"><span data-stu-id="e5257-219">This is due toohello rapid increase in hello number of permutations evaluated by hello solver as hello number of cities increases.</span></span>
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a><span data-ttu-id="e5257-220">Jak toorun hello monitorowania aplikacji klienta</span><span class="sxs-lookup"><span data-stu-id="e5257-220">How toorun hello monitoring client application</span></span>
1. <span data-ttu-id="e5257-221">Zaloguj się na komputerze tooyour, w którym będzie uruchamiany powitania klienta aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e5257-221">Log on tooyour machine where you will run hello client application.</span></span> <span data-ttu-id="e5257-222">To nie jest konieczne toobe hello tym samym komputerze, na którym działa hello **TSPSolver** aplikacji, mimo że można go.</span><span class="sxs-lookup"><span data-stu-id="e5257-222">This does not need toobe hello same machine running hello **TSPSolver** application, although it can be.</span></span>
2. <span data-ttu-id="e5257-223">Utwórz folder, w którym będzie działała aplikacja sieci.</span><span class="sxs-lookup"><span data-stu-id="e5257-223">Create a folder where you will run your application.</span></span> <span data-ttu-id="e5257-224">Na przykład **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="e5257-224">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="e5257-225">Kopiuj **TSPClient.jar** za**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="e5257-225">Copy **TSPClient.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="e5257-226">Upewnij się, że folder bin hello JRE znajduje się w zmiennej środowiskowej PATH hello.</span><span class="sxs-lookup"><span data-stu-id="e5257-226">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
5. <span data-ttu-id="e5257-227">W wierszu polecenia Zmień tooc:\TSP katalogów.</span><span class="sxs-lookup"><span data-stu-id="e5257-227">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="e5257-228">Uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="e5257-228">Run hello following command.</span></span>
   
        java -jar TSPClient.jar
   
    <span data-ttu-id="e5257-229">Opcjonalnie określ hello liczbę minut toosleep Between sprawdzanie hello kolejki, przekazując argument wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e5257-229">Optionally, specify hello number of minutes toosleep in between checking hello queue, by passing in a command-line argument.</span></span> <span data-ttu-id="e5257-230">Witaj domyślny okres uśpienia sprawdzania kolejki hello jest 3 minuty, który jest używany, jeśli żaden argument wiersza polecenia jest przekazywany za**TSPClient**.</span><span class="sxs-lookup"><span data-stu-id="e5257-230">hello default sleep period for checking hello queue is 3 minutes, which is used if no command-line argument is passed too**TSPClient**.</span></span> <span data-ttu-id="e5257-231">Toouse inną wartość dla interwału powitania uśpienia, na przykład jedną minutę, uruchomić hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="e5257-231">If you want toouse a different value for hello sleep interval, for example, one minute, run hello following command.</span></span>
   
        java -jar TSPClient.jar 1
   
    <span data-ttu-id="e5257-232">powitania klienta zostanie uruchomiony, dopóki nie widzi ona komunikatu w kolejce "Zakończ".</span><span class="sxs-lookup"><span data-stu-id="e5257-232">hello client will run until it sees a queue message of "Complete".</span></span> <span data-ttu-id="e5257-233">Należy pamiętać, że po uruchomieniu wielu wystąpień hello solver bez uruchamiania powitania klienta może być konieczne toorun powitania klienta kolejki pusty hello toocompletely wiele razy.</span><span class="sxs-lookup"><span data-stu-id="e5257-233">Note that if you run multiple occurrences of hello solver without running hello client, you may need toorun hello client multiple times toocompletely empty hello queue.</span></span> <span data-ttu-id="e5257-234">Alternatywnie można usunąć kolejki hello i utworzyć ją ponownie.</span><span class="sxs-lookup"><span data-stu-id="e5257-234">Alternatively, you can delete hello queue and then create it again.</span></span> <span data-ttu-id="e5257-235">kolejki hello toodelete, uruchom następujące hello **TSPSolver** (nie **TSPClient**) polecenia.</span><span class="sxs-lookup"><span data-stu-id="e5257-235">toodelete hello queue, run hello following **TSPSolver** (not **TSPClient**)  command.</span></span>
   
        java -jar TSPSolver.jar deletequeue
   
    <span data-ttu-id="e5257-236">Hello solver zostanie uruchomiony do momentu zakończenia badanie wszystkie trasy.</span><span class="sxs-lookup"><span data-stu-id="e5257-236">hello solver will run until it finishes examining all routes.</span></span>

## <a name="how-toostop-hello-java-applications"></a><span data-ttu-id="e5257-237">Jak toostop hello aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="e5257-237">How toostop hello Java applications</span></span>
<span data-ttu-id="e5257-238">Hello solver i aplikacje klienckie, można nacisnąć klawisz **klawisze Ctrl + C** tooexit, jeśli chcesz, aby tooend toonormal wcześniejszego wykonania.</span><span class="sxs-lookup"><span data-stu-id="e5257-238">For both hello solver and client applications, you can press **Ctrl+C** tooexit if you want tooend prior toonormal completion.</span></span>

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
