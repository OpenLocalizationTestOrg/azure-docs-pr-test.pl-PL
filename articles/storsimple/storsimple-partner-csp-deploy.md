---
title: "aaaMicrosoft Azure StorSimple i omówienie programu dostawcy rozwiązań w chmurze | Dokumentacja firmy Microsoft"
description: "Omówienie hello StorSimple i dostawcy usług Kryptograficznych dla partnerów usługi StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/08/2017
ms.author: alkohli
ms.openlocfilehash: b5d999f2fbb9a27e7404ff454957b29dbef56af6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="bfa05-103">Wdrażanie tablicy wirtualnego StorSimple programu dostawcy rozwiązania chmury</span><span class="sxs-lookup"><span data-stu-id="bfa05-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="bfa05-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="bfa05-104">Overview</span></span>

<span data-ttu-id="bfa05-105">Tablica wirtualnego StorSimple można wdrożyć hello partnerów Cloud Solution Provider (CSP) dla klientów.</span><span class="sxs-lookup"><span data-stu-id="bfa05-105">StorSimple Virtual Array can be deployed by hello Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="bfa05-106">Partner dostawcy usług Kryptograficznych można utworzyć usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="bfa05-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="bfa05-107">Następnie można toodeploy używane i zarządzanie tablicy wirtualnego StorSimple tej usługi i hello skojarzone udziałów, woluminów i kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="bfa05-107">This service can then be used toodeploy and manage StorSimple Virtual Array and hello associated shares, volumes, and backups.</span></span>

<span data-ttu-id="bfa05-108">W tym artykule opisano, jak dodać klienta lub nowego klienta istniejących tooan subskrypcji i utworzy toodeploy usługi tablicą wirtualnego StorSimple w dostawcy usług Kryptograficznych partnera dostawcy usług Kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="bfa05-108">This article describes how a CSP partner can add a customer or a new subscription tooan existing customer and then create a service toodeploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfa05-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bfa05-109">Prerequisites</span></span>

<span data-ttu-id="bfa05-110">Przed rozpoczęciem upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="bfa05-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="bfa05-111">Zarejestrowane w hello dostawcy usług Kryptograficznych programu.</span><span class="sxs-lookup"><span data-stu-id="bfa05-111">You are enrolled under hello CSP program.</span></span>
- <span data-ttu-id="bfa05-112">Masz poprawne [Centrum partnerskiego](http://partnercenter.microsoft.com/) poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="bfa05-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="bfa05-113">poświadczenia Hello pozwalają toosign toohello partnera portalu tooadd nowych klientów, wyszukiwać klientów lub przejdź tooa konta klienta z poziomu pulpitu nawigacyjnego hello partnera.</span><span class="sxs-lookup"><span data-stu-id="bfa05-113">hello credentials enable you toosign in toohello Partner portal tooadd new customers, search for customers, or navigate tooa customer account from hello Partner dashboard.</span></span> <span data-ttu-id="bfa05-114">Witaj dostawcy usług Kryptograficznych może działać jako StorSimple administrator w imieniu klienta hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bfa05-114">hello CSP can function as a StorSimple administrator on behalf of hello customer in hello Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="bfa05-115">Dodaj klienta</span><span class="sxs-lookup"><span data-stu-id="bfa05-115">Add a customer</span></span>

<span data-ttu-id="bfa05-116">Jeśli dodasz klienta subskrypcji jest tworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="bfa05-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="bfa05-117">tooadd klienta (i automatycznie utworzyć subskrypcję), wykonaj następujące kroki w portalu dla partnerów hello hello.</span><span class="sxs-lookup"><span data-stu-id="bfa05-117">tooadd a customer (and automatically create a subscription), perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="bfa05-118">Przejdź toohello [Centrum partnerskiego](http://partnercenter.microsoft.com/) i zaloguj się przy użyciu poświadczeń konta dostawcy usług Kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="bfa05-118">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="bfa05-119">Kliknij przycisk **pulpitu nawigacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="bfa05-119">Click **Dashboard**.</span></span>

     ![Pulpit nawigacyjny w Centrum partnerskiego](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="bfa05-121">W lewym okienku hello, kliknij przycisk **klientów**.</span><span class="sxs-lookup"><span data-stu-id="bfa05-121">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="bfa05-122">W prawym okienku hello, kliknij przycisk **dodać klienci**.</span><span class="sxs-lookup"><span data-stu-id="bfa05-122">In hello right-pane, click **Add customers**.</span></span> <span data-ttu-id="bfa05-123">Wprowadź szczegóły hello powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="bfa05-123">Enter hello details of hello customer.</span></span> <span data-ttu-id="bfa05-124">Kliknij przycisk **dalej: subskrypcji** toocreate subskrypcji klienta.</span><span class="sxs-lookup"><span data-stu-id="bfa05-124">Click **Next: Subscriptions** toocreate a customer subscription.</span></span>

    ![Dodaj klienta](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="bfa05-126">Wybierz **Microsoft Azure** oferty.</span><span class="sxs-lookup"><span data-stu-id="bfa05-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="bfa05-127">Przewiń w dół toohello hello strony i kliknij przycisk **przeglądu**.</span><span class="sxs-lookup"><span data-stu-id="bfa05-127">Scroll toohello bottom of hello page and click **Review**.</span></span>

    ![Przejrzyj informacje o subskrypcji](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="bfa05-129">Przejrzyj informacje o hello i kliknij przycisk **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="bfa05-129">Review hello information and click **Submit**.</span></span>

    ![Przedstawia subskrypcji](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="bfa05-131">Zapisz informacje o potwierdzenie hello do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="bfa05-131">Save hello confirmation information for future reference.</span></span>

    ![Zapisz potwierdzenia](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="bfa05-133">Znajdź fizyczną lub przejdź toohello klienta, który właśnie został dodany.</span><span class="sxs-lookup"><span data-stu-id="bfa05-133">Find or navigate toohello customer you just added.</span></span> <span data-ttu-id="bfa05-134">Kliknij przycisk hello **nazwa firmy** toodrill w dół do szczegółów hello.</span><span class="sxs-lookup"><span data-stu-id="bfa05-134">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Wyszukaj powitania klienta](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="bfa05-136">W lewym okienku hello, wybierz **Zarządzanie usługami**.</span><span class="sxs-lookup"><span data-stu-id="bfa05-136">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="bfa05-137">W hello prawym okienku w obszarze **administrowania usługami**, kliknij przycisk **portalu zarządzania Microsoft Azure** toosign w jako administratora platformy Azure dla klienta.</span><span class="sxs-lookup"><span data-stu-id="bfa05-137">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![Zaloguj się w portalu tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="bfa05-139">toocreate Menedżera urządzeń StorSimple, kliknij przycisk **+ nowy** i wyszukaj ścieżkę fizyczną lub przejdź zbyt**wirtualnego serii urządzenia StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="bfa05-139">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="bfa05-140">Aby uzyskać więcej informacji, przejdź zbyt[wdrożyć usługę Menedżer StorSimple urządzenia](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="bfa05-140">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Utwórz usługę Menedżer StorSimple urządzenia](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="bfa05-142">Dodaj subskrypcję</span><span class="sxs-lookup"><span data-stu-id="bfa05-142">Add a subscription</span></span>

<span data-ttu-id="bfa05-143">W niektórych przypadkach może być istniejący klient i należy tooadd subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bfa05-143">In some instances, you may have an existing customer, and you need tooadd a subscription.</span></span> <span data-ttu-id="bfa05-144">tooadd subskrypcji tooan istniejącego klienta, wykonaj następujące kroki w portalu dla partnerów hello hello.</span><span class="sxs-lookup"><span data-stu-id="bfa05-144">tooadd a subscription tooan existing customer, perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="bfa05-145">Przejdź toohello [Centrum partnerskiego](http://partnercenter.microsoft.com/) i zaloguj się przy użyciu poświadczeń konta dostawcy usług Kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="bfa05-145">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="bfa05-146">Kliknij przycisk **pulpitu nawigacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="bfa05-146">Click **Dashboard**.</span></span>

     ![Pulpit nawigacyjny w Centrum partnerskiego](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="bfa05-148">W lewym okienku hello, kliknij przycisk **klientów**.</span><span class="sxs-lookup"><span data-stu-id="bfa05-148">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="bfa05-149">Znajdź fizyczną lub przejdź toohello klienta, który ma tooadd subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bfa05-149">Find or navigate toohello customer you want tooadd a subscription to.</span></span> <span data-ttu-id="bfa05-150">Kliknij przycisk hello ![Ikona znacznika wyboru Rozwiń](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) ikona tooexpand hello wiersza dla nazwy firmy powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="bfa05-150">Click hello ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon tooexpand hello row for hello company name for your customer.</span></span> <span data-ttu-id="bfa05-151">W szczegółach powitania kliknij **dodawać subskrypcje**.</span><span class="sxs-lookup"><span data-stu-id="bfa05-151">In hello details, click **Add subscriptions**.</span></span>

    ![Klienci](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="bfa05-153">Sprawdź **Microsoft Azure** dla hello **Top oferty** w subskrypcji hello i kliknij przycisk **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="bfa05-153">Check **Microsoft Azure** for hello **Top offers** in hello subscription and click **Submit**.</span></span> <span data-ttu-id="bfa05-154">Spowoduje to utworzenie nowej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bfa05-154">This creates a new subscription.</span></span>

    ![Dodaj nową subskrypcję](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="bfa05-156">Po utworzeniu nowej subskrypcji, kliknij przycisk **<--klientów** w toohello tooreturn w lewym okienku hello **klientów** strony.</span><span class="sxs-lookup"><span data-stu-id="bfa05-156">After a new subscription is created, click **<-- Customers** in hello left-pane tooreturn toohello **Customers** page.</span></span> <span data-ttu-id="bfa05-157">Wyszukiwanie powitania klienta, dla którego utworzono subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bfa05-157">Search for hello customer for whom you just created a subscription.</span></span> <span data-ttu-id="bfa05-158">Kliknij przycisk hello **nazwa firmy** toodrill w dół do szczegółów hello.</span><span class="sxs-lookup"><span data-stu-id="bfa05-158">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Wyszukaj powitania klienta](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="bfa05-160">W lewym okienku hello, wybierz **Zarządzanie usługami**.</span><span class="sxs-lookup"><span data-stu-id="bfa05-160">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="bfa05-161">W hello prawym okienku w obszarze **administrowania usługami**, kliknij przycisk **portalu zarządzania Microsoft Azure** toosign w jako administratora platformy Azure dla klienta.</span><span class="sxs-lookup"><span data-stu-id="bfa05-161">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![Zaloguj się w portalu tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="bfa05-163">toocreate Menedżera urządzeń StorSimple, kliknij przycisk **+ nowy** i wyszukaj ścieżkę fizyczną lub przejdź zbyt**wirtualnego serii urządzenia StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="bfa05-163">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="bfa05-164">Aby uzyskać więcej informacji, przejdź zbyt[wdrożyć usługę Menedżer StorSimple urządzenia](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="bfa05-164">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Utwórz usługę Menedżer StorSimple urządzenia](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="bfa05-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bfa05-166">Next steps</span></span>

- <span data-ttu-id="bfa05-167">Jeśli masz więcej pytań dotyczących hello StorSimple w dostawcy usług Kryptograficznych, przejdź zbyt[StorSimple w dostawcy usług Kryptograficznych: często zadawane pytania](storsimple-partner-csp-faq.md).</span><span class="sxs-lookup"><span data-stu-id="bfa05-167">If you have more questions regarding hello StorSimple in CSP, go too[StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="bfa05-168">Jeśli jesteś gotowe toodeploy produkty StorSimple, przejdź zbyt[wdrażanie programu StorSimple w dostawcy usług Kryptograficznych](storsimple-partner-csp-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="bfa05-168">If you are ready toodeploy your StorSimple, go too[Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
