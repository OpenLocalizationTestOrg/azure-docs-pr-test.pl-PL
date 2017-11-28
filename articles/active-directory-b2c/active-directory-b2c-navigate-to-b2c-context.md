---
title: "Usługa Azure Active Directory B2C: Przełączanie tooa B2C dzierżawy | Dokumentacja firmy Microsoft"
description: "Jak dzierżawcy tooswitch w kontekście hello programu Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 0eb1b198-44d3-4065-9fae-16591a8d3eae
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/13/2017
ms.author: parakhj
ms.openlocfilehash: 572f9ab283ecac68d284bb04fdfc98575bcf9393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="switching-tooyour-azure-ad-b2c-tenant"></a><span data-ttu-id="d7e48-103">Przełączanie dzierżawy usługi Azure AD B2C tooyour</span><span class="sxs-lookup"><span data-stu-id="d7e48-103">Switching tooyour Azure AD B2C tenant</span></span>

<span data-ttu-id="d7e48-104">W kolejności tooconfigure usługi Azure AD B2C należy toobe w kontekście hello dzierżawy usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d7e48-104">In order tooconfigure Azure AD B2C, you need toobe in hello context of your Azure AD B2C tenant.</span></span>

## <a name="log-into-azure-ad-b2c-tenant"></a><span data-ttu-id="d7e48-105">Logowanie się do dzierżawy usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="d7e48-105">Log into Azure AD B2C tenant</span></span>

<span data-ttu-id="d7e48-106">dzierżawy usługi Azure AD B2C toonavigate tooyour, użytkownik musi być zalogowany do hello portalu Azure jako administrator globalny dzierżawy hello Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d7e48-106">toonavigate tooyour Azure AD B2C tenant, you must be logged into hello Azure portal as a global administrator of hello Azure AD B2C tenant.</span></span>

1. <span data-ttu-id="d7e48-107">Zaloguj się na powitania [portalu Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d7e48-107">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
1. <span data-ttu-id="d7e48-108">Przełącz dzierżawcy, klikając Twojego adresu e-mail lub obraz powitania prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="d7e48-108">Switch tenants by clicking your email address or picture in hello top-right corner.</span></span>
1. <span data-ttu-id="d7e48-109">W hello `Directory` listy, która pojawia się, że chcesz toomanage dzierżawy wybierz hello Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d7e48-109">In hello `Directory` list that appears, select hello Azure AD B2C tenant that you wish toomanage.</span></span>

<span data-ttu-id="d7e48-110">Witaj Azure Portal zostanie odświeżony.</span><span class="sxs-lookup"><span data-stu-id="d7e48-110">hello Azure Portal will refresh.</span></span>  <span data-ttu-id="d7e48-111">Obecnie zalogowano Cię na powitania portalu Azure w kontekście hello dzierżawy usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d7e48-111">Now you are signed into hello Azure Portal in hello context of your Azure AD B2C tenant.</span></span>

## <a name="navigate-toohello-b2c-features-blade"></a><span data-ttu-id="d7e48-112">Przejdź do bloku funkcji B2C toohello</span><span class="sxs-lookup"><span data-stu-id="d7e48-112">Navigate toohello B2C features blade</span></span>

1. <span data-ttu-id="d7e48-113">Kliknij przycisk **Przeglądaj** na powitania nawigacji po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="d7e48-113">Click **Browse** on hello left hand navigation.</span></span>
1. <span data-ttu-id="d7e48-114">Kliknij przycisk **> więcej usług** , a następnie wyszukaj `Azure AD B2C` w okienku nawigacji po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="d7e48-114">Click **> More services** and then search for `Azure AD B2C` in hello left navigation pane.</span></span>  <span data-ttu-id="d7e48-115">(toopin tooyour lewa tablicy startowej, kliknij przycisk lewej gwiazdy toohello hello usługi Azure AD B2C)</span><span class="sxs-lookup"><span data-stu-id="d7e48-115">(toopin tooyour left-hand Startboard, click hello star toohello left of Azure AD B2C)</span></span>
1. <span data-ttu-id="d7e48-116">Kliknij przycisk **usługi Azure AD B2C** tooaccess hello bloku funkcji B2C.</span><span class="sxs-lookup"><span data-stu-id="d7e48-116">Click **Azure AD B2C** tooaccess hello B2C features blade.</span></span>
   
    ![Zrzut ekranu przedstawiający blok funkcji tooB2C przeglądania](./media/active-directory-b2c-get-started/b2c-browse.png)

> [!IMPORTANT]
> <span data-ttu-id="d7e48-118">Należy toobe Administrator globalny dzierżawy B2C hello toobe bloku funkcji hello B2C tooaccess stanie.</span><span class="sxs-lookup"><span data-stu-id="d7e48-118">You need toobe a Global Administrator of hello B2C tenant toobe able tooaccess hello B2C features blade.</span></span> <span data-ttu-id="d7e48-119">Administrator globalny innej dzierżawy ani użytkownik dowolnej dzierżawy nie mogą uzyskać dostępu do tego bloku.</span><span class="sxs-lookup"><span data-stu-id="d7e48-119">A Global Administrator from any other tenant or a user from any tenant cannot access it.</span></span>  <span data-ttu-id="d7e48-120">Dzierżawy B2C tooyour można przełączać się przy użyciu przełącznik dzierżawy hello w hello prawym górnym rogu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d7e48-120">You can switch tooyour B2C tenant by using hello tenant switcher in hello top right corner of hello Azure portal.</span></span>
