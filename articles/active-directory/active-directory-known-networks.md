---
title: aaaKnown sieci w hello klasycznego portalu Azure | Dokumentacja firmy Microsoft
description: "Konfigurując znane sieci, można uniknąć o adresy IP, które są własnością organizacji objęte hello dodatki logowania z wielu lokalizacji geograficznych i ins logowania z adresów IP z raportami podejrzanych działań."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a><span data-ttu-id="e6293-103">Znane sieci</span><span class="sxs-lookup"><span data-stu-id="e6293-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e6293-104">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e6293-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="e6293-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e6293-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="e6293-106">Umożliwia dostęp do usługi Azure Active Directory i użycia raporty toogain widoczność hello integralności i bezpieczeństwa w katalogu organizacji.</span><span class="sxs-lookup"><span data-stu-id="e6293-106">You can use Azure Active Directory's access and usage reports toogain visibility into hello integrity and security of your organization’s directory.</span></span> <span data-ttu-id="e6293-107">Dzięki tym informacjom administratora katalogu można lepiej określić, gdzie może znajdować się możliwe zagrożenia bezpieczeństwa, tak aby ich odpowiednio zaplanować toomitigate te zagrożenia.</span><span class="sxs-lookup"><span data-stu-id="e6293-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan toomitigate those risks.</span></span>

<span data-ttu-id="e6293-108">Możliwe, że Witaj "*logowania z wielu lokalizacji geograficznych*"i"*logowania z adresów IP z podejrzaną aktywność*" raporty niepoprawnie Flaga adresy IP, które są rzeczywiście należących do użytkownika organizacja.</span><span class="sxs-lookup"><span data-stu-id="e6293-108">It is possible that hello “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="e6293-109">Dzieje się tak na przykład, gdy:</span><span class="sxs-lookup"><span data-stu-id="e6293-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="e6293-110">Użytkownik w biurze Boston zalogował się zdalnie centrum danych tooyour hello wyzwalaczy Poznań "Ins logowania z wielu lokalizacji geograficznych" raportu</span><span class="sxs-lookup"><span data-stu-id="e6293-110">A user in your Boston office has signed in remotely tooyour data center in San Francisco triggers hello “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="e6293-111">Użytkownik z organizacji podejmuje toosign na z hello wyzwalaczy niepoprawne hasło "Ins logowania z adresów IP związanych z podejrzanymi działaniami" raport</span><span class="sxs-lookup"><span data-stu-id="e6293-111">A user of your organization tries toosign-on several times with an incorrect password triggers hello “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="e6293-112">tooprevent tych przypadkach zabezpieczeń mylących Generowanie raportów, należy dodać znane listę adresów IP zakresów toohello publicznego adresu IP w organizacji.</span><span class="sxs-lookup"><span data-stu-id="e6293-112">tooprevent these cases from generating misleading security reports, you should add known IP address ranges toohello list of your organization's public IP address.</span></span>    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a><span data-ttu-id="e6293-113">tooadd z zakresów w organizacji publicznego adresu IP, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e6293-113">tooadd your organization’s public IP address ranges, perform hello following steps:</span></span>

1. <span data-ttu-id="e6293-114">Logowania jednokrotnego toohello [portalu zarządzania Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e6293-114">Sign-on toohello [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="e6293-115">W okienku po lewej stronie powitania kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e6293-115">In hello left pane, click **Active Directory**.</span></span> 

    ![Znane sieci](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="e6293-117">W hello **katalogu** , a następnie wybierz katalog.</span><span class="sxs-lookup"><span data-stu-id="e6293-117">In hello **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="e6293-118">W menu hello na górze hello, kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="e6293-118">In hello menu on hello top, click **Configure**.</span></span> 

    ![Znane sieci](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="e6293-120">Na karcie Konfigurowanie hello Przejdź zbyt**Twojego zakresy organizacji publicznych adresów IP**</span><span class="sxs-lookup"><span data-stu-id="e6293-120">On hello Configure tab, go too**your organizations public IP address ranges**</span></span> 

    ![Znane sieci](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="e6293-122">Kliknij przycisk **Dodawanie zakresów adresów IP znane**.</span><span class="sxs-lookup"><span data-stu-id="e6293-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="e6293-123">Dodaj zakresy adresów w pojawi się okno dialogowe hello, a następnie kliknij przycisk wyboru hello, gdy wszystko będzie gotowe.</span><span class="sxs-lookup"><span data-stu-id="e6293-123">Add your address ranges in hello dialog box that appears, and then click hello check button  when you are done.</span></span> 

    ![Znane sieci](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="e6293-125">**Dodatkowe zasoby:**</span><span class="sxs-lookup"><span data-stu-id="e6293-125">**Additional resources:**</span></span>

* [<span data-ttu-id="e6293-126">Wyświetlanie raportów dostępu i użycia</span><span class="sxs-lookup"><span data-stu-id="e6293-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="e6293-127">Logowania z adresów IP związanych z podejrzanymi działaniami</span><span class="sxs-lookup"><span data-stu-id="e6293-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="e6293-128">Logowania z wielu lokalizacji geograficznych</span><span class="sxs-lookup"><span data-stu-id="e6293-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)

