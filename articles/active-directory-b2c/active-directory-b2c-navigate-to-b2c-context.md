---
title: "Azure Active Directory B2C: Przełączanie się na dzierżawę B2C | Microsoft Docs"
description: "Jak przełączyć się do kontekstu dzierżawy usługi Active Directory B2C"
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
ms.openlocfilehash: 40d8d57d974a949fbdc0a06eeceb2d06bfbaa09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="switching-to-your-azure-ad-b2c-tenant"></a><span data-ttu-id="83bfb-103">Przełączanie się do dzierżawy usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="83bfb-103">Switching to your Azure AD B2C tenant</span></span>

<span data-ttu-id="83bfb-104">Aby skonfigurować usługę Azure AD B2C, musisz być w kontekście swojej dzierżawy usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="83bfb-104">In order to configure Azure AD B2C, you need to be in the context of your Azure AD B2C tenant.</span></span>

## <a name="log-into-azure-ad-b2c-tenant"></a><span data-ttu-id="83bfb-105">Logowanie się do dzierżawy usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="83bfb-105">Log into Azure AD B2C tenant</span></span>

<span data-ttu-id="83bfb-106">Aby przejść do swojej dzierżawy usługi Azure AD B2C, musisz się zalogować do witryny Azure Portal jako administrator globalny dzierżawy usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="83bfb-106">To navigate to your Azure AD B2C tenant, you must be logged into the Azure portal as a global administrator of the Azure AD B2C tenant.</span></span>

1. <span data-ttu-id="83bfb-107">Zaloguj się do [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="83bfb-107">Sign into the [Azure portal](http://portal.azure.com).</span></span>
1. <span data-ttu-id="83bfb-108">Przełącz dzierżawy, klikając swój adres e-mail lub zdjęcie w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="83bfb-108">Switch tenants by clicking your email address or picture in the top-right corner.</span></span>
1. <span data-ttu-id="83bfb-109">Z wyświetlonej listy `Directory` wybierz dzierżawę usługi Azure AD B2C, którą chcesz zarządzać.</span><span class="sxs-lookup"><span data-stu-id="83bfb-109">In the `Directory` list that appears, select the Azure AD B2C tenant that you wish to manage.</span></span>

<span data-ttu-id="83bfb-110">Witryna Azure Portal zostanie odświeżona.</span><span class="sxs-lookup"><span data-stu-id="83bfb-110">The Azure Portal will refresh.</span></span>  <span data-ttu-id="83bfb-111">Od tej chwili kontekstem logowania w witrynie Azure Portal będzie Twoja dzierżawa usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="83bfb-111">Now you are signed into the Azure Portal in the context of your Azure AD B2C tenant.</span></span>

## <a name="navigate-to-the-b2c-features-blade"></a><span data-ttu-id="83bfb-112">Przechodzenie do bloku funkcji B2C</span><span class="sxs-lookup"><span data-stu-id="83bfb-112">Navigate to the B2C features blade</span></span>

1. <span data-ttu-id="83bfb-113">Kliknij pozycję **Przeglądaj** w obszarze nawigacji po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="83bfb-113">Click **Browse** on the left hand navigation.</span></span>
1. <span data-ttu-id="83bfb-114">Kliknij pozycję **> Więcej usług**, a następnie wyszukaj tekst `Azure AD B2C` w okienku nawigacyjnym po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="83bfb-114">Click **> More services** and then search for `Azure AD B2C` in the left navigation pane.</span></span>  <span data-ttu-id="83bfb-115">(Aby przypiąć tę pozycję do tablicy startowej po lewej stronie, kliknij gwiazdkę na lewo od usługi Azure AD B2C)</span><span class="sxs-lookup"><span data-stu-id="83bfb-115">(To pin to your left-hand Startboard, click the star to the left of Azure AD B2C)</span></span>
1. <span data-ttu-id="83bfb-116">Kliknij pozycję **Azure AD B2C**, aby otworzyć blok funkcji B2C.</span><span class="sxs-lookup"><span data-stu-id="83bfb-116">Click **Azure AD B2C** to access the B2C features blade.</span></span>
   
    ![Zrzut ekranu z blokiem przeglądania w poszukiwaniu funkcji B2C](./media/active-directory-b2c-get-started/b2c-browse.png)

> [!IMPORTANT]
> <span data-ttu-id="83bfb-118">Tylko administrator globalny dzierżawy B2C może uzyskiwać dostęp do bloku funkcji B2C.</span><span class="sxs-lookup"><span data-stu-id="83bfb-118">You need to be a Global Administrator of the B2C tenant to be able to access the B2C features blade.</span></span> <span data-ttu-id="83bfb-119">Administrator globalny innej dzierżawy ani użytkownik dowolnej dzierżawy nie mogą uzyskać dostępu do tego bloku.</span><span class="sxs-lookup"><span data-stu-id="83bfb-119">A Global Administrator from any other tenant or a user from any tenant cannot access it.</span></span>  <span data-ttu-id="83bfb-120">Na swoją dzierżawę B2C możesz przełączyć się, używając przełącznika dzierżawy w prawym górnym rogu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="83bfb-120">You can switch to your B2C tenant by using the tenant switcher in the top right corner of the Azure portal.</span></span>
