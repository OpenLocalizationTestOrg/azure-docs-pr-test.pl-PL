---
title: Znane sieci w klasycznym portalu Azure | Dokumentacja firmy Microsoft
description: "Konfigurując znane sieci, można uniknąć o adresy IP, które są własnością organizacji objętych ins logowania z wielu lokalizacji geograficznych i ins logowania z adresów IP z raportami podejrzanych działań."
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
ms.openlocfilehash: e4d51d1d2f09fca34d749879e21d49f785eac35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="known-networks"></a><span data-ttu-id="fc67d-103">Znane sieci</span><span class="sxs-lookup"><span data-stu-id="fc67d-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fc67d-104">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fc67d-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="fc67d-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fc67d-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="fc67d-106">Dostęp do usługi Azure Active Directory i raporty użycia umożliwia wgląd we integralności i bezpieczeństwa katalogu organizacji.</span><span class="sxs-lookup"><span data-stu-id="fc67d-106">You can use Azure Active Directory's access and usage reports to gain visibility into the integrity and security of your organization’s directory.</span></span> <span data-ttu-id="fc67d-107">Dzięki tym informacjom administratora katalogu można lepiej określić, gdzie może znajdować się możliwe zagrożenia bezpieczeństwa, tak aby ich odpowiednio zaplanować ich eliminowania.</span><span class="sxs-lookup"><span data-stu-id="fc67d-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan to mitigate those risks.</span></span>

<span data-ttu-id="fc67d-108">Możliwe jest który "*logowania z wielu lokalizacji geograficznych*"i"*logowania z adresów IP z podejrzaną aktywność*" raporty niepoprawnie Flaga adresy IP, które są rzeczywiście należących do użytkownika organizacja.</span><span class="sxs-lookup"><span data-stu-id="fc67d-108">It is possible that the “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="fc67d-109">Dzieje się tak na przykład, gdy:</span><span class="sxs-lookup"><span data-stu-id="fc67d-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="fc67d-110">Użytkownik w Twojej Boston office zalogował się zdalnie na centrum danych w sieci San Francisco uruchamia raportu "Logowania z wielu lokalizacji geograficznych"</span><span class="sxs-lookup"><span data-stu-id="fc67d-110">A user in your Boston office has signed in remotely to your data center in San Francisco triggers the “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="fc67d-111">Organizacji próbie logowania z wyzwalaczy niepoprawne hasło "Logowania z adresów IP z podejrzaną aktywność" raportu</span><span class="sxs-lookup"><span data-stu-id="fc67d-111">A user of your organization tries to sign-on several times with an incorrect password triggers the “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="fc67d-112">Aby uniknąć tych przypadkach generowania mylących raporty dotyczące zabezpieczeń, należy dodać znane zakresów adresów IP do listy publicznego adresu IP w organizacji.</span><span class="sxs-lookup"><span data-stu-id="fc67d-112">To prevent these cases from generating misleading security reports, you should add known IP address ranges to the list of your organization's public IP address.</span></span>    

### <a name="to-add-your-organizations-public-ip-address-ranges-perform-the-following-steps"></a><span data-ttu-id="fc67d-113">Aby dodać organizacji zakresy publicznych adresów IP, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fc67d-113">To add your organization’s public IP address ranges, perform the following steps:</span></span>

1. <span data-ttu-id="fc67d-114">Logowanie do [portalu zarządzania Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fc67d-114">Sign-on to the [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="fc67d-115">W okienku po lewej stronie kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fc67d-115">In the left pane, click **Active Directory**.</span></span> 

    ![Znane sieci](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="fc67d-117">W **katalogu** , a następnie wybierz katalog.</span><span class="sxs-lookup"><span data-stu-id="fc67d-117">In the **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="fc67d-118">W menu u góry kliknij **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="fc67d-118">In the menu on the top, click **Configure**.</span></span> 

    ![Znane sieci](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="fc67d-120">Na karcie Konfigurowanie przejdź do **Twojego zakresy organizacji publicznych adresów IP**</span><span class="sxs-lookup"><span data-stu-id="fc67d-120">On the Configure tab, go to **your organizations public IP address ranges**</span></span> 

    ![Znane sieci](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="fc67d-122">Kliknij przycisk **Dodawanie zakresów adresów IP znane**.</span><span class="sxs-lookup"><span data-stu-id="fc67d-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="fc67d-123">Dodaj zakresy adresów w wyświetlonym oknie dialogowym, a następnie kliknij przycisk wyboru, gdy wszystko będzie gotowe.</span><span class="sxs-lookup"><span data-stu-id="fc67d-123">Add your address ranges in the dialog box that appears, and then click the check button  when you are done.</span></span> 

    ![Znane sieci](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="fc67d-125">**Dodatkowe zasoby:**</span><span class="sxs-lookup"><span data-stu-id="fc67d-125">**Additional resources:**</span></span>

* [<span data-ttu-id="fc67d-126">Wyświetlanie raportów dostępu i użycia</span><span class="sxs-lookup"><span data-stu-id="fc67d-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="fc67d-127">Logowania z adresów IP związanych z podejrzanymi działaniami</span><span class="sxs-lookup"><span data-stu-id="fc67d-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="fc67d-128">Logowania z wielu lokalizacji geograficznych</span><span class="sxs-lookup"><span data-stu-id="fc67d-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)

