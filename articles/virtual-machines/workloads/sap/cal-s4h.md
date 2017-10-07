---
title: aaaDeploy SAP S/4HANA lub BW/4HANA na maszynie Wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Wdrożenie SAP S/4HANA lub BW/4HANA na maszynie Wirtualnej platformy Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="86376-103">Wdrożenie SAP S/4HANA lub BW/4HANA na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="86376-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="86376-104">W tym artykule opisano, jak toodeploy S/4HANA na platformie Azure przy użyciu hello SAP chmury urządzenie biblioteki (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="86376-104">This article describes how toodeploy S/4HANA on Azure by using hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="86376-105">toodeploy innych SAP HANA rozwiązań, takich jak BW/4HANA, wykonaj hello te same czynności.</span><span class="sxs-lookup"><span data-stu-id="86376-105">toodeploy other SAP HANA-based solutions, such as BW/4HANA, follow hello same steps.</span></span>

> [!NOTE]
<span data-ttu-id="86376-106">Aby uzyskać więcej informacji na temat hello SAP CAL Przejdź toohello [biblioteki urządzenia chmury SAP](https://cal.sap.com/) witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="86376-106">For more information about hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="86376-107">SAP ma również blog o hello [SAP chmury urządzenia biblioteki 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="86376-107">SAP also has a blog about hello [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="86376-108">Jak 29 maja 2017 za pomocą modelu wdrażania usługi Azure Resource Manager hello dodatkowo toohello preferowany bez wdrażania klasycznego modelu toodeploy hello SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="86376-108">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="86376-109">Firma Microsoft zaleca używanie hello nowego modelu wdrażania usługi Resource Manager i pominąć hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="86376-109">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

## <a name="step-by-step-process-toodeploy-hello-solution"></a><span data-ttu-id="86376-110">Krok po kroku proces toodeploy hello rozwiązania</span><span class="sxs-lookup"><span data-stu-id="86376-110">Step-by-step process toodeploy hello solution</span></span>

<span data-ttu-id="86376-111">powitania po sekwencji zrzuty ekranu pokazuje, jak toodeploy S/4HANA na platformie Azure przy użyciu hello SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="86376-111">hello following sequence of screenshots shows you how toodeploy S/4HANA on Azure by using hello SAP CAL.</span></span> <span data-ttu-id="86376-112">proces Hello działa hello taki sam sposób dla innych rozwiązań, takich jak BW/4HANA.</span><span class="sxs-lookup"><span data-stu-id="86376-112">hello process works hello same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="86376-113">Witaj **rozwiązań** strony przedstawiono niektóre hello SAP CAL HANA rozwiązań dostępnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="86376-113">hello **Solutions** page shows some of hello SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="86376-114">**SAP S/4HANA 1610 FPS01, urządzenia Fully-Activated** znajduje się w wierszu środkowej hello:</span><span class="sxs-lookup"><span data-stu-id="86376-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in hello middle row:</span></span>

![Rozwiązania CAL SAP](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="86376-116">Tworzenie konta w hello SAP CAL</span><span class="sxs-lookup"><span data-stu-id="86376-116">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="86376-117">toosign w toohello SAP licencji dostępu klienta na powitania po raz pierwszy, użyj użytkownika S SAP lub innego użytkownika w zarejestrowany SAP.</span><span class="sxs-lookup"><span data-stu-id="86376-117">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="86376-118">Następnie zdefiniuj SAP CAL konta, które jest używane przez urządzenia toodeploy SAP CAL hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="86376-118">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="86376-119">W definicji konta hello musisz:</span><span class="sxs-lookup"><span data-stu-id="86376-119">In hello account definition, you need to:</span></span>

    <span data-ttu-id="86376-120">a.</span><span class="sxs-lookup"><span data-stu-id="86376-120">a.</span></span> <span data-ttu-id="86376-121">Wybierz model wdrożenia hello na platformie Azure (Resource Manager lub classic).</span><span class="sxs-lookup"><span data-stu-id="86376-121">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="86376-122">b.</span><span class="sxs-lookup"><span data-stu-id="86376-122">b.</span></span> <span data-ttu-id="86376-123">Wprowadź subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="86376-123">Enter your Azure subscription.</span></span> <span data-ttu-id="86376-124">Konto SAP CAL można przypisać tylko tooone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="86376-124">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="86376-125">Jeśli potrzebujesz więcej niż jedną subskrypcję, należy toocreate innego konta SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="86376-125">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>

    <span data-ttu-id="86376-126">c.</span><span class="sxs-lookup"><span data-stu-id="86376-126">c.</span></span> <span data-ttu-id="86376-127">Nadaj hello SAP CAL uprawnienia toodeploy do Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="86376-127">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="86376-128">Następne kroki Hello pokazują, jak konto toocreate CAL SAP do wdrożenia usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="86376-128">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="86376-129">Jeśli masz już konto SAP CAL, które jest połączone toohello klasycznego modelu wdrażania, możesz *muszą* toofollow toocreate te kroki nowe konto SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="86376-129">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="86376-130">nowe konto SAP CAL Hello musi toodeploy hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="86376-130">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="86376-131">Utwórz nowe konto SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="86376-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="86376-132">Witaj **kont** strony zawiera trzy opcje dla platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="86376-132">hello **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="86376-133">a.</span><span class="sxs-lookup"><span data-stu-id="86376-133">a.</span></span> <span data-ttu-id="86376-134">**Microsoft Azure (klasyczne)** jest hello klasycznego modelu wdrażania i nie jest preferowany.</span><span class="sxs-lookup"><span data-stu-id="86376-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="86376-135">b.</span><span class="sxs-lookup"><span data-stu-id="86376-135">b.</span></span> <span data-ttu-id="86376-136">**Microsoft Azure** jest hello nowego modelu wdrażania Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="86376-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    <span data-ttu-id="86376-137">c.</span><span class="sxs-lookup"><span data-stu-id="86376-137">c.</span></span> <span data-ttu-id="86376-138">**Windows Azure obsługiwany przez 21Vianet** jest opcją w Chinach, który używa hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="86376-138">**Windows Azure operated by 21Vianet** is an option in China that uses hello classic deployment model.</span></span>

    <span data-ttu-id="86376-139">Wybierz toodeploy w modelu Resource Manager hello **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="86376-139">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Szczegóły konta CAL SAP](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="86376-141">Wprowadź hello Azure **identyfikator subskrypcji** znajdującymi się na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="86376-141">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span>

   ![Konta CAL SAP](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="86376-143">Definicja tooauthorize hello SAP CAL toodeploy do hello subskrypcji platformy Azure, kliknij przycisk **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="86376-143">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="86376-144">powitania po stronie pojawia się na karcie przeglądarki hello:</span><span class="sxs-lookup"><span data-stu-id="86376-144">hello following page appears in hello browser tab:</span></span>

   ![Logowania usług w chmurze programu Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="86376-146">Jeśli jest wymieniona więcej niż jednego użytkownika, wybierz konto Microsoft hello jest coadministrator hello toobe połączonego elementu hello subskrypcji platformy Azure, które wybrano.</span><span class="sxs-lookup"><span data-stu-id="86376-146">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="86376-147">powitania po stronie pojawia się na karcie przeglądarki hello:</span><span class="sxs-lookup"><span data-stu-id="86376-147">hello following page appears in hello browser tab:</span></span>

   ![Potwierdzenie usług w chmurze programu Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="86376-149">Kliknij przycisk **zaakceptować**.</span><span class="sxs-lookup"><span data-stu-id="86376-149">Click **Accept**.</span></span> <span data-ttu-id="86376-150">Jeśli autoryzacji hello zakończy się pomyślnie, hello definicji konta SAP CAL Wyświetla ponownie.</span><span class="sxs-lookup"><span data-stu-id="86376-150">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="86376-151">Po pewnym czasie wyświetli się komunikat potwierdzający, pomyślnego hello procesu autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="86376-151">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="86376-152">Witaj tooassign nowo utworzony użytkownik tooyour konta SAP CAL, wprowadź użytkownika **identyfikator użytkownika** w hello pola tekstowego na powitania prawo i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="86376-152">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span>

   ![Skojarzenie toouser konta](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="86376-154">Kliknij konto użytkownika hello Użyj toosign w toohello SAP CAL tooassociate **przeglądu**.</span><span class="sxs-lookup"><span data-stu-id="86376-154">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="86376-155">toocreate hello skojarzenie swoją nazwę użytkownika i hello nowo utworzone konto SAP CAL, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="86376-155">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

   ![Skojarzenie konta użytkownika tooSAP CAL](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="86376-157">Pomyślnie utworzono konto SAP CAL, które jest w stanie:</span><span class="sxs-lookup"><span data-stu-id="86376-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="86376-158">Użyj modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="86376-158">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="86376-159">Wdrażanie systemów SAP do Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="86376-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="86376-160">Teraz możesz rozpocząć toodeploy S/4HANA w subskrypcji użytkownika na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="86376-160">Now you can start toodeploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="86376-161">Przed kontynuowaniem należy sprawdzić, czy przydziały Azure core dla maszyn wirtualnych platformy Azure H serii.</span><span class="sxs-lookup"><span data-stu-id="86376-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="86376-162">W momencie hello hello SAP CAL używa toodeploy H serii maszyn wirtualnych Azure niektórych rozwiązań hello SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="86376-162">At hello moment, hello SAP CAL uses H-Series VMs of Azure toodeploy some of hello SAP HANA-based solutions.</span></span> <span data-ttu-id="86376-163">Subskrypcji platformy Azure może nie mieć żadnych przydziały core serii H H serii.</span><span class="sxs-lookup"><span data-stu-id="86376-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="86376-164">Jeśli tak, może być konieczne toocontact pomocy technicznej platformy Azure tooget przydziału co najmniej 16 rdzeni H serii.</span><span class="sxs-lookup"><span data-stu-id="86376-164">If so, you might need toocontact Azure support tooget a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="86376-165">Podczas wdrażania rozwiązania na platformie Azure w hello SAP CAL, może się okazać, że można wybrać tylko jeden region platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="86376-165">When you deploy a solution on Azure in hello SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="86376-166">toodeploy do regionów platformy Azure niż hello jedną sugerowanych hello SAP CAL, należy toopurchase CAL subskrypcji z SAP.</span><span class="sxs-lookup"><span data-stu-id="86376-166">toodeploy into Azure regions other than hello one suggested by hello SAP CAL, you need toopurchase a CAL subscription from SAP.</span></span> <span data-ttu-id="86376-167">Może okazać się również tooopen wiadomość z SAP toohave toodeliver konta użytkownika CAL do regionów platformy Azure niż hello początkowo sugerowane z nich.</span><span class="sxs-lookup"><span data-stu-id="86376-167">You also might need tooopen a message with SAP toohave your CAL account enabled toodeliver into Azure regions other than hello ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="86376-168">Wdrażanie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="86376-168">Deploy a solution</span></span>

<span data-ttu-id="86376-169">Umożliwia wdrażanie rozwiązania z hello **rozwiązań** strony hello SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="86376-169">Let's deploy a solution from hello **Solutions** page of hello SAP CAL.</span></span> <span data-ttu-id="86376-170">Witaj SAP CAL ma dwa toodeploy sekwencji:</span><span class="sxs-lookup"><span data-stu-id="86376-170">hello SAP CAL has two sequences toodeploy:</span></span>

- <span data-ttu-id="86376-171">Podstawowe sekwencji, która korzysta z jednej strony toodefine hello systemu toobe wdrożony</span><span class="sxs-lookup"><span data-stu-id="86376-171">A basic sequence that uses one page toodefine hello system toobe deployed</span></span>
- <span data-ttu-id="86376-172">Zaawansowane sekwencji, zapewniająca niektórych opcji rozmiarów maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="86376-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="86376-173">Przedstawiony tutaj toodeployment podstawowa ścieżka hello.</span><span class="sxs-lookup"><span data-stu-id="86376-173">We demonstrate hello basic path toodeployment here.</span></span>

1. <span data-ttu-id="86376-174">Na powitania **szczegóły konta** strony, musisz:</span><span class="sxs-lookup"><span data-stu-id="86376-174">On hello **Account Details** page, you need to:</span></span>

    <span data-ttu-id="86376-175">a.</span><span class="sxs-lookup"><span data-stu-id="86376-175">a.</span></span> <span data-ttu-id="86376-176">Wybierz konto SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="86376-176">Select an SAP CAL account.</span></span> <span data-ttu-id="86376-177">(Użyj konta, które jest skojarzone toodeploy z modelu wdrażania usługi Resource Manager hello).</span><span class="sxs-lookup"><span data-stu-id="86376-177">(Use an account that is associated toodeploy with hello Resource Manager deployment model.)</span></span>

    <span data-ttu-id="86376-178">b.</span><span class="sxs-lookup"><span data-stu-id="86376-178">b.</span></span> <span data-ttu-id="86376-179">Wprowadź wystąpienia **nazwa**.</span><span class="sxs-lookup"><span data-stu-id="86376-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="86376-180">c.</span><span class="sxs-lookup"><span data-stu-id="86376-180">c.</span></span> <span data-ttu-id="86376-181">Wybierz platformy Azure **Region**.</span><span class="sxs-lookup"><span data-stu-id="86376-181">Select an Azure **Region**.</span></span> <span data-ttu-id="86376-182">Witaj SAP CAL sugeruje regionu.</span><span class="sxs-lookup"><span data-stu-id="86376-182">hello SAP CAL suggests a region.</span></span> <span data-ttu-id="86376-183">Jeśli nie masz subskrypcji SAP CAL wymagają innego regionu Azure, należy tooorder licencji CAL subskrypcji z SAP.</span><span class="sxs-lookup"><span data-stu-id="86376-183">If you need another Azure region and you don't have an SAP CAL subscription, you need tooorder a CAL subscription with SAP.</span></span>

    <span data-ttu-id="86376-184">d.</span><span class="sxs-lookup"><span data-stu-id="86376-184">d.</span></span> <span data-ttu-id="86376-185">Wprowadź wzorzec **hasło** hello rozwiązania z dziewięciu osiem znaków.</span><span class="sxs-lookup"><span data-stu-id="86376-185">Enter a master **Password** for hello solution of eight or nine characters.</span></span> <span data-ttu-id="86376-186">hasło Hello jest używany dla administratorów hello hello różnych składników.</span><span class="sxs-lookup"><span data-stu-id="86376-186">hello password is used for hello administrators of hello different components.</span></span>

   ![Tryb CAL Basic SAP: Utworzenie wystąpienia](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="86376-188">Kliknij przycisk **Utwórz**, a w polu wiadomość hello jest wyświetlana, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="86376-188">Click **Create**, and in hello message box that appears, click **OK**.</span></span>

   ![SAP CAL obsługiwane rozmiary maszyn wirtualnych](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="86376-190">W hello **klucza prywatnego** okno dialogowe, kliknij przycisk **magazynu** toostore hello klucza prywatnego w hello SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="86376-190">In hello **Private Key** dialog box, click **Store** toostore hello private key in hello SAP CAL.</span></span> <span data-ttu-id="86376-191">Ochrona za pomocą hasła toouse hello klucza prywatnego, kliknij przycisk **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="86376-191">toouse password protection for hello private key, click **Download**.</span></span> 

   ![Klucz prywatny CAL SAP](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="86376-193">Witaj odczytu SAP CAL **ostrzeżenie** komunikatów, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="86376-193">Read hello SAP CAL **Warning** message, and click **OK**.</span></span>

   ![Ostrzeżenie CAL SAP](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="86376-195">Teraz hello wdrożenia ma miejsce.</span><span class="sxs-lookup"><span data-stu-id="86376-195">Now hello deployment takes place.</span></span> <span data-ttu-id="86376-196">Po pewnym czasie, w zależności od rozmiaru hello i złożoność hello rozwiązania (hello SAP CAL zapewnia szacunkową) hello zostanie wyświetlony stan jako aktywne i gotowe do użycia.</span><span class="sxs-lookup"><span data-stu-id="86376-196">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="86376-197">maszyny wirtualne hello toofind zebranych przez hello innych skojarzonych zasobów w jednej grupie zasobów, odwiedź toohello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="86376-197">toofind hello virtual machines collected with hello other associated resources in one resource group, go toohello Azure portal:</span></span> 

   ![Obiekty SAP CAL wdrożone w hello nowego portalu.](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="86376-199">W portalu SAP CAL hello, hello stan jest wyświetlany jako **Active**.</span><span class="sxs-lookup"><span data-stu-id="86376-199">On hello SAP CAL portal, hello status appears as **Active**.</span></span> <span data-ttu-id="86376-200">rozwiązanie toohello tooconnect, kliknij przycisk **Connect**.</span><span class="sxs-lookup"><span data-stu-id="86376-200">tooconnect toohello solution, click **Connect**.</span></span> <span data-ttu-id="86376-201">Różne opcje tooconnect toohello różnych składników są wdrażane w ramach tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="86376-201">Different options tooconnect toohello different components are deployed within this solution.</span></span>

   ![Wystąpienia CAL SAP](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="86376-203">Zanim będzie możliwe użycie jednego z systemów toohello wdrożone tooconnect opcje hello, kliknij przycisk **Getting Started Guide**.</span><span class="sxs-lookup"><span data-stu-id="86376-203">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> 

   ![Połącz toohello wystąpienia](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="86376-205">nazwy dokumentacji Hello hello użytkowników dla każdej z metod łączności hello.</span><span class="sxs-lookup"><span data-stu-id="86376-205">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="86376-206">Hello hasła dla tych użytkowników są ustawione hasło główne toohello zdefiniowane przez użytkownika na początku hello hello procesu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="86376-206">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="86376-207">W dokumentacji hello innym użytkownikom bardziej funkcjonalny są wyświetlane z haseł, których można użyć toosign w toohello wdrożony system.</span><span class="sxs-lookup"><span data-stu-id="86376-207">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span> 

    <span data-ttu-id="86376-208">Na przykład jeśli używasz hello SAP graficznego interfejsu użytkownika, który jest preinstalowany na maszynie zdalnej pulpitu systemu Windows hello hello S/4 systemu może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="86376-208">For example, if you use hello SAP GUI that's preinstalled on hello Windows Remote Desktop machine, hello S/4 system might look like this:</span></span>

   ![SM50 w hello preinstalowany SAP graficznego interfejsu użytkownika](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="86376-210">Lub jeśli używasz hello DBACockpit wystąpienia hello może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="86376-210">Or if you use hello DBACockpit, hello instance might look like this:</span></span>

   ![SM50 w hello DBACockpit SAP graficznego interfejsu użytkownika](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="86376-212">W ciągu kilku godzin dobrej kondycji urządzenia SAP S/4 jest wdrażana na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="86376-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="86376-213">Jeśli zakupiono subskrypcję SAP CAL SAP w pełni obsługuje wdrożeniami hello SAP CAL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="86376-213">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="86376-214">Kolejka Obsługa Hello jest BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="86376-214">hello support queue is BC-VCM-CAL.</span></span>







