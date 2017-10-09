---
title: aaaDeploy SAP IDES EHP7 z dodatkiem SP3 na platformie Azure w wersji 6.0 ERP SAP | Dokumentacja firmy Microsoft
description: "Wdrożenie SAP IDES EHP7 SP3 dla SAP ERP 6.0 na platformie Azure"
services: virtual-machines-windows
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 626c1523-1026-478f-bd8a-22c83b869231
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/16/2016
ms.author: hermannd
ms.openlocfilehash: 26d88c7b48a91d35602464c4f89ca7a30502c4b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a><span data-ttu-id="9b214-103">Wdrożenie SAP IDES EHP7 SP3 dla SAP ERP 6.0 na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="9b214-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span></span>
<span data-ttu-id="9b214-104">W tym artykule opisano sposób toodeploy SAP IDES systemu z programu SQL Server i systemu operacyjnego Windows hello na platformie Azure za pośrednictwem hello SAP chmury urządzenie biblioteki (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="9b214-104">This article describes how toodeploy an SAP IDES system running with SQL Server and hello Windows operating system on Azure via hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="9b214-105">Hello zrzuty ekranu pokazują hello krok po kroku procesu.</span><span class="sxs-lookup"><span data-stu-id="9b214-105">hello screenshots show hello step-by-step process.</span></span> <span data-ttu-id="9b214-106">toodeploy inne rozwiązanie, wykonaj te same czynności hello.</span><span class="sxs-lookup"><span data-stu-id="9b214-106">toodeploy a different solution, follow hello same steps.</span></span>

<span data-ttu-id="9b214-107">toostart z hello CAL SAP, przejdź toohello [biblioteki urządzenia chmury SAP](https://cal.sap.com/) witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9b214-107">toostart with hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="9b214-108">SAP ma również blog o hello nowe [SAP chmury urządzenia biblioteki 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="9b214-108">SAP also has a blog about hello new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

> [!NOTE]
<span data-ttu-id="9b214-109">Jak 29 maja 2017 za pomocą modelu wdrażania usługi Azure Resource Manager hello dodatkowo toohello preferowany bez wdrażania klasycznego modelu toodeploy hello SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="9b214-109">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="9b214-110">Firma Microsoft zaleca używanie hello nowego modelu wdrażania usługi Resource Manager i pominąć hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="9b214-110">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

<span data-ttu-id="9b214-111">Jeśli utworzono już konta SAP CAL, które używają modelu klasycznym hello, *należy toocreate innego konta SAP CAL*.</span><span class="sxs-lookup"><span data-stu-id="9b214-111">If you already created an SAP CAL account that uses hello classic model, *you need toocreate another SAP CAL account*.</span></span> <span data-ttu-id="9b214-112">To konto wymaga tooexclusively wdrażanie na platformie Azure przy użyciu hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9b214-112">This account needs tooexclusively deploy into Azure by using hello Resource Manager model.</span></span>

<span data-ttu-id="9b214-113">Po zalogowaniu w toohello SAP CAL, pierwsza strona hello zwykle poprowadzą toohello **rozwiązań** strony.</span><span class="sxs-lookup"><span data-stu-id="9b214-113">After you sign in toohello SAP CAL, hello first page usually leads you toohello **Solutions** page.</span></span> <span data-ttu-id="9b214-114">rozwiązania Hello są oferowane w hello SAP CAL stopniowo coraz, dlatego może być konieczne tooscroll sobą rozwiązania hello toofind, który ma.</span><span class="sxs-lookup"><span data-stu-id="9b214-114">hello solutions offered on hello SAP CAL are steadily increasing, so you might need tooscroll quite a bit toofind hello solution you want.</span></span> <span data-ttu-id="9b214-115">Hello wyróżnione systemu SAP IDES rozwiązania, które jest dostępne wyłącznie w systemie Azure przedstawiono proces wdrażania hello:</span><span class="sxs-lookup"><span data-stu-id="9b214-115">hello highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates hello deployment process:</span></span>

![Rozwiązania CAL SAP](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="9b214-117">Tworzenie konta w hello SAP CAL</span><span class="sxs-lookup"><span data-stu-id="9b214-117">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="9b214-118">toosign w toohello SAP licencji dostępu klienta na powitania po raz pierwszy, użyj użytkownika S SAP lub innego użytkownika w zarejestrowany SAP.</span><span class="sxs-lookup"><span data-stu-id="9b214-118">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="9b214-119">Następnie zdefiniuj SAP CAL konta, które jest używane przez urządzenia toodeploy SAP CAL hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9b214-119">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="9b214-120">W definicji konta hello musisz:</span><span class="sxs-lookup"><span data-stu-id="9b214-120">In hello account definition, you need to:</span></span>

    <span data-ttu-id="9b214-121">a.</span><span class="sxs-lookup"><span data-stu-id="9b214-121">a.</span></span> <span data-ttu-id="9b214-122">Wybierz model wdrożenia hello na platformie Azure (Resource Manager lub classic).</span><span class="sxs-lookup"><span data-stu-id="9b214-122">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="9b214-123">b.</span><span class="sxs-lookup"><span data-stu-id="9b214-123">b.</span></span> <span data-ttu-id="9b214-124">Wprowadź subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9b214-124">Enter your Azure subscription.</span></span> <span data-ttu-id="9b214-125">Konto SAP CAL można przypisać tylko tooone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9b214-125">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="9b214-126">Jeśli potrzebujesz więcej niż jedną subskrypcję, należy toocreate innego konta SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="9b214-126">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>
    
    <span data-ttu-id="9b214-127">c.</span><span class="sxs-lookup"><span data-stu-id="9b214-127">c.</span></span> <span data-ttu-id="9b214-128">Nadaj hello SAP CAL uprawnienia toodeploy do Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9b214-128">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="9b214-129">Następne kroki Hello pokazują, jak konto toocreate CAL SAP do wdrożenia usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9b214-129">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="9b214-130">Jeśli masz już konto SAP CAL, które jest połączone toohello klasycznego modelu wdrażania, możesz *muszą* toofollow toocreate te kroki nowe konto SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="9b214-130">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="9b214-131">nowe konto SAP CAL Hello musi toodeploy hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9b214-131">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="9b214-132">toocreate nowe CAL SAP konta, hello **kont** strony zawiera dwa wybory dla platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="9b214-132">toocreate a new SAP CAL account, hello **Accounts** page shows two choices for Azure:</span></span> 

    <span data-ttu-id="9b214-133">a.</span><span class="sxs-lookup"><span data-stu-id="9b214-133">a.</span></span> <span data-ttu-id="9b214-134">**Microsoft Azure (klasyczne)** jest hello klasycznego modelu wdrażania i nie jest preferowany.</span><span class="sxs-lookup"><span data-stu-id="9b214-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="9b214-135">b.</span><span class="sxs-lookup"><span data-stu-id="9b214-135">b.</span></span> <span data-ttu-id="9b214-136">**Microsoft Azure** jest hello nowego modelu wdrażania Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="9b214-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    ![Konta CAL SAP](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    <span data-ttu-id="9b214-138">Wybierz toodeploy w modelu Resource Manager hello **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="9b214-138">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Konta CAL SAP](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. <span data-ttu-id="9b214-140">Wprowadź hello Azure **identyfikator subskrypcji** znajdującymi się na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9b214-140">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span> 

    ![Identyfikator subskrypcji CAL SAP](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. <span data-ttu-id="9b214-142">Definicja tooauthorize hello SAP CAL toodeploy do hello subskrypcji platformy Azure, kliknij przycisk **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="9b214-142">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="9b214-143">powitania po stronie pojawia się na karcie przeglądarki hello:</span><span class="sxs-lookup"><span data-stu-id="9b214-143">hello following page appears in hello browser tab:</span></span>

    ![Logowania usług w chmurze programu Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. <span data-ttu-id="9b214-145">Jeśli jest wymieniona więcej niż jednego użytkownika, wybierz konto Microsoft hello jest coadministrator hello toobe połączonego elementu hello subskrypcji platformy Azure, które wybrano.</span><span class="sxs-lookup"><span data-stu-id="9b214-145">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="9b214-146">powitania po stronie pojawia się na karcie przeglądarki hello:</span><span class="sxs-lookup"><span data-stu-id="9b214-146">hello following page appears in hello browser tab:</span></span>

    ![Potwierdzenie usług w chmurze programu Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. <span data-ttu-id="9b214-148">Kliknij przycisk **zaakceptować**.</span><span class="sxs-lookup"><span data-stu-id="9b214-148">Click **Accept**.</span></span> <span data-ttu-id="9b214-149">Jeśli autoryzacji hello zakończy się pomyślnie, hello definicji konta SAP CAL Wyświetla ponownie.</span><span class="sxs-lookup"><span data-stu-id="9b214-149">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="9b214-150">Po pewnym czasie wyświetli się komunikat potwierdzający, pomyślnego hello procesu autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="9b214-150">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="9b214-151">Witaj tooassign nowo utworzony użytkownik tooyour konta SAP CAL, wprowadź użytkownika **identyfikator użytkownika** w hello pola tekstowego na powitania prawo i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="9b214-151">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span> 

    ![Skojarzenie toouser konta](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. <span data-ttu-id="9b214-153">Kliknij konto użytkownika hello Użyj toosign w toohello SAP CAL tooassociate **przeglądu**.</span><span class="sxs-lookup"><span data-stu-id="9b214-153">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 

9. <span data-ttu-id="9b214-154">toocreate hello skojarzenie swoją nazwę użytkownika i hello nowo utworzone konto SAP CAL, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9b214-154">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

    ![Skojarzenie tooaccount użytkownika](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

<span data-ttu-id="9b214-156">Pomyślnie utworzono konto SAP CAL, które jest w stanie:</span><span class="sxs-lookup"><span data-stu-id="9b214-156">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="9b214-157">Użyj modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="9b214-157">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="9b214-158">Wdrażanie systemów SAP do Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9b214-158">Deploy SAP systems into your Azure subscription.</span></span>

> [!NOTE]
<span data-ttu-id="9b214-159">Przed wdrożeniem hello SAP IDES rozwiązania opartego na systemie Windows i program SQL Server może być konieczne toosign dla subskrypcji SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="9b214-159">Before you can deploy hello SAP IDES solution based on Windows and SQL Server, you might need toosign up for an SAP CAL subscription.</span></span> <span data-ttu-id="9b214-160">W przeciwnym razie hello rozwiązania może być wyświetlany jako **zablokowany** na stronie Przegląd hello.</span><span class="sxs-lookup"><span data-stu-id="9b214-160">Otherwise, hello solution might show up as **Locked** on hello overview page.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="9b214-161">Wdrażanie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="9b214-161">Deploy a solution</span></span>
1. <span data-ttu-id="9b214-162">Po skonfigurowaniu konta SAP CAL, wybierz **hello rozwiązania SAP IDES w systemach Windows i program SQL Server** rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9b214-162">After you set up an SAP CAL account, select **hello SAP IDES solution on Windows and SQL Server** solution.</span></span> <span data-ttu-id="9b214-163">Kliknij przycisk **Utwórz wystąpienie**i Potwierdź hello warunki użytkowania i warunki.</span><span class="sxs-lookup"><span data-stu-id="9b214-163">Click **Create Instance**, and confirm hello usage and terms conditions.</span></span> 

2. <span data-ttu-id="9b214-164">Na powitania **podstawowe tryb: Utwórz wystąpienie** strony, musisz:</span><span class="sxs-lookup"><span data-stu-id="9b214-164">On hello **Basic Mode: Create Instance** page, you need to:</span></span>

    <span data-ttu-id="9b214-165">a.</span><span class="sxs-lookup"><span data-stu-id="9b214-165">a.</span></span> <span data-ttu-id="9b214-166">Wprowadź wystąpienia **nazwa**.</span><span class="sxs-lookup"><span data-stu-id="9b214-166">Enter an instance **Name**.</span></span>

    <span data-ttu-id="9b214-167">b.</span><span class="sxs-lookup"><span data-stu-id="9b214-167">b.</span></span> <span data-ttu-id="9b214-168">Wybierz platformy Azure **Region**.</span><span class="sxs-lookup"><span data-stu-id="9b214-168">Select an Azure **Region**.</span></span> <span data-ttu-id="9b214-169">Może być konieczne tooget subskrypcji SAP CAL oferowanych w wielu regionach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9b214-169">You might need an SAP CAL subscription tooget multiple Azure regions offered.</span></span>

    <span data-ttu-id="9b214-170">c.</span><span class="sxs-lookup"><span data-stu-id="9b214-170">c.</span></span>  <span data-ttu-id="9b214-171">Wprowadź wzorzec hello **hasło** hello rozwiązania, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="9b214-171">Enter hello master **Password** for hello solution, as shown:</span></span>

    ![Tryb CAL Basic SAP: Utworzenie wystąpienia](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. <span data-ttu-id="9b214-173">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9b214-173">Click **Create**.</span></span> <span data-ttu-id="9b214-174">Po pewnym czasie w zależności od rozmiaru hello i złożoność hello rozwiązania (powitalne SAP CAL zapewnia szacunkową), stan hello jest wyświetlany, jako aktywne i gotowe do użycia:</span><span class="sxs-lookup"><span data-stu-id="9b214-174">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use:</span></span> 

    ![Wystąpienia CAL SAP](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. <span data-ttu-id="9b214-176">grupy zasobów hello toofind i wszystkie jego obiekty, które zostały utworzone przez hello SAP CAL, przejdź toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9b214-176">toofind hello resource group and all its objects that were created by hello SAP CAL, go toohello Azure portal.</span></span> <span data-ttu-id="9b214-177">począwszy od hello wystąpienie takie same nazwy co w hello SAP CAL można znaleźć Hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9b214-177">hello virtual machine can be found starting with hello same instance name that was given in hello SAP CAL.</span></span>

    ![Obiekty grupy zasobów](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. <span data-ttu-id="9b214-179">W portalu SAP CAL hello, przejdź wystąpień toohello wdrożone i kliknij polecenie **Connect**.</span><span class="sxs-lookup"><span data-stu-id="9b214-179">On hello SAP CAL portal, go toohello deployed instances and click **Connect**.</span></span> <span data-ttu-id="9b214-180">zostanie wyświetlone następujące okno podręczne Hello:</span><span class="sxs-lookup"><span data-stu-id="9b214-180">hello following pop-up window appears:</span></span> 

    ![Połącz toohello wystąpienia](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. <span data-ttu-id="9b214-182">Zanim będzie możliwe użycie jednego z systemów toohello wdrożone tooconnect opcje hello, kliknij przycisk **Getting Started Guide**.</span><span class="sxs-lookup"><span data-stu-id="9b214-182">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> <span data-ttu-id="9b214-183">nazwy dokumentacji Hello hello użytkowników dla każdej z metod łączności hello.</span><span class="sxs-lookup"><span data-stu-id="9b214-183">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="9b214-184">Hello hasła dla tych użytkowników są ustawione hasło główne toohello zdefiniowane przez użytkownika na początku hello hello procesu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="9b214-184">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="9b214-185">W dokumentacji hello innym użytkownikom bardziej funkcjonalny są wyświetlane z haseł, których można użyć toosign w toohello wdrożony system.</span><span class="sxs-lookup"><span data-stu-id="9b214-185">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span>

    ![SAP dokumentacji-Zapraszamy!](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="9b214-187">W ciągu kilku godzin dobrej kondycji systemu SAP IDES jest wdrażana na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9b214-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span></span>

<span data-ttu-id="9b214-188">Jeśli zakupiono subskrypcję SAP CAL SAP w pełni obsługuje wdrożeniami hello SAP CAL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9b214-188">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="9b214-189">Kolejka Obsługa Hello jest BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="9b214-189">hello support queue is BC-VCM-CAL.</span></span>

