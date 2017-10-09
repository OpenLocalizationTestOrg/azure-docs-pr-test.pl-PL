---
title: "aaaUpload certyfikat interfejsu API zarządzania platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak athe tooupload interfejs API zarządzania certyfikatu dla hello klasycznego portalu Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="f6df1-103">Przekaż certyfikat zarządzania interfejsem API zarządzania platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f6df1-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="f6df1-104">Certyfikaty zarządzania Zezwalaj tooauthenticate z hello klasycznego modelu wdrażania dostarczany przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="f6df1-104">Management certificates allow you tooauthenticate with hello classic deployment model provided by Azure.</span></span> <span data-ttu-id="f6df1-105">Wiele programów i narzędzia (np. programu Visual Studio lub hello Azure SDK) należy użyć tych certyfikatów tooautomate Konfiguracja i wdrożenie różnych usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f6df1-105">Many programs and tools (such as Visual Studio or hello Azure SDK) use these certificates tooautomate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="f6df1-106">Ostrożnie!</span><span class="sxs-lookup"><span data-stu-id="f6df1-106">Be careful!</span></span> <span data-ttu-id="f6df1-107">Zezwalaj tych typów certyfikatów, każdy, kto jest uwierzytelniany w usłudze ich toomanage hello subskrypcji skojarzonych z nimi.</span><span class="sxs-lookup"><span data-stu-id="f6df1-107">These types of certificates allow anyone who authenticates with them toomanage hello subscription they are associated with.</span></span>
>
>

<span data-ttu-id="f6df1-108">Jeśli chcesz więcej informacji o certyfikatach Azure (takie jak tworzenie certyfikatu z podpisem własnym), zobacz [Omówienie certyfikatów dla usług w chmurze Azure](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span><span class="sxs-lookup"><span data-stu-id="f6df1-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="f6df1-109">Można również użyć [usługi Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate kodu klienta dla celów automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="f6df1-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="f6df1-110">Przekazywanie certyfikatu zarządzania</span><span class="sxs-lookup"><span data-stu-id="f6df1-110">Upload a management certificate</span></span>
<span data-ttu-id="f6df1-111">Po utworzeniu utworzony certyfikat zarządzania, (plik cer z tylko klucz publiczny hello) można przekazać go do portalu hello.</span><span class="sxs-lookup"><span data-stu-id="f6df1-111">Once you have a management certificate created, (.cer file with only hello public key) you can upload it into hello portal.</span></span> <span data-ttu-id="f6df1-112">Gdy certyfikat hello jest dostępne w portalu hello, każda osoba mająca zgodnego certyfikatu (klucz prywatny) łączenie się za pośrednictwem zasobów hello interfejs API zarządzania i dostęp hello hello skojarzone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f6df1-112">When hello certificate is available in hello portal, anyone with a matching certificate (private key) can connect through hello Management API and access hello resources for hello associated subscription.</span></span>

1. <span data-ttu-id="f6df1-113">Zaloguj się za toohello [portalu Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f6df1-113">Log in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="f6df1-114">Kliknij przycisk **więcej usług** na powitania Dolna lista usługi Azure, następnie wybierz **subskrypcje** w hello _ogólne_ grupy usług.</span><span class="sxs-lookup"><span data-stu-id="f6df1-114">Click **More services** at hello bottom Azure service list, then select **Subscriptions** in hello _General_ service group.</span></span>

    ![Menu subskrypcji](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="f6df1-116">Upewnij się, tooselect hello poprawną subskrypcję, które mają tooassociate z certyfikatem hello.</span><span class="sxs-lookup"><span data-stu-id="f6df1-116">Make sure tooselect hello correct subscription that you want tooassociate with hello certificate.</span></span>     
4. <span data-ttu-id="f6df1-117">Po wybraniu hello poprawną subskrypcję, naciśnij klawisz **certyfikaty zarządzania** w hello _ustawienia_ grupy.</span><span class="sxs-lookup"><span data-stu-id="f6df1-117">After you have selected hello correct subscription, press **Management certificates** in hello _Settings_ group.</span></span>

    ![Ustawienia](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="f6df1-119">Naciśnij klawisz hello **przekazać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f6df1-119">Press hello **Upload** button.</span></span>

    ![Przekaż na stronie certyfikatów](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="f6df1-121">Wypełnianie hello okna dialogowego informacji i naciśnij klawisz **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="f6df1-121">Fill out hello dialog information and press **Upload**.</span></span>

    ![Ustawienia](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="f6df1-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f6df1-123">Next steps</span></span>
<span data-ttu-id="f6df1-124">Teraz, gdy masz certyfikat zarządzania skojarzony z subskrypcją (po zainstalowaniu hello dopasowania certyfikatu lokalnie) programowo podłączeniem toohello [klasycznego modelu wdrażania interfejsu API REST](https://msdn.microsoft.com/library/azure/mt420159.aspx) i automatyzacji Witaj różnych zasobów platformy Azure, które są również powiązaną z jego subskrypcją.</span><span class="sxs-lookup"><span data-stu-id="f6df1-124">Now that you have a management certificate associated with a subscription, you can (after you have installed hello matching certificate locally) programmatically connect toohello [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate hello various Azure resources that are also associated with that subscription.</span></span>
