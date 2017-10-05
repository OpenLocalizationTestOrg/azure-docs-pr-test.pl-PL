---
title: "Wymagania wstępne platformy Azure Data Catalog | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o wymaganiach wstępnych potrzebne Rozpoczynanie pracy z usługą Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 3fdef7bb58a5cd5dfbe4d37d9baf9c8e392ebe42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="84e8f-103">Wymagania wstępne usługi Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="84e8f-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="84e8f-104">Należy zadbać o kilka rzeczy przed rozpoczęciem konfigurowania usługi Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="84e8f-104">You need to take care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="84e8f-105">Nie martw się, ten proces nie długo.</span><span class="sxs-lookup"><span data-stu-id="84e8f-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="84e8f-106">Subskrypcja platformy Azure</span><span class="sxs-lookup"><span data-stu-id="84e8f-106">Azure subscription</span></span>
<span data-ttu-id="84e8f-107">Aby skonfigurować usługi Data Catalog, musi być właścicielem lub współwłaściciel subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="84e8f-107">To set up Data Catalog, you must be the owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="84e8f-108">Subskrypcje platformy Azure ułatwić organizowanie dostęp do zasobów usługi w chmurze, takich jak Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="84e8f-108">Azure subscriptions help you organize access to cloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="84e8f-109">Subskrypcje można także kontrolować sposób użycia zasobów jest zgłaszane, rozliczane i uregulowaniu płatności.</span><span class="sxs-lookup"><span data-stu-id="84e8f-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="84e8f-110">Każda subskrypcja może mieć oddzielne ustawienia rozliczeń i płatności, więc można dodać subskrypcji i plany, które zależą od działów, projektów, biuro regionalne i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="84e8f-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="84e8f-111">Każda usługa w chmurze należy do subskrypcji, i musisz mieć subskrypcję przed skonfigurowaniem usługi Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="84e8f-111">Every cloud service belongs to a subscription, and you need to have a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="84e8f-112">Aby dowiedzieć się więcej, zobacz artykuł [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md) (Zarządzanie kontami, subskrypcjami i rolami administracyjnymi).</span><span class="sxs-lookup"><span data-stu-id="84e8f-112">To learn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="84e8f-113">Usługa Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="84e8f-113">Azure Active Directory</span></span>
<span data-ttu-id="84e8f-114">Aby skonfigurować usługi Data Catalog, muszą być podpisane za pomocą konta użytkownika usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="84e8f-114">To set up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="84e8f-115">Usługa Azure AD umożliwia firmom łatwe zarządzanie tożsamościami i dostępem, zarówno w chmurze, jak i lokalnie.</span><span class="sxs-lookup"><span data-stu-id="84e8f-115">Azure AD provides an easy way for your business to manage identity and access, both in the cloud and on-premises.</span></span> <span data-ttu-id="84e8f-116">Użytkownicy mogą używać jednego konta firmowego lub szkolnego dla pojedynczego logowania do dowolnego chmury i lokalnych aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="84e8f-116">Users can use a single work or school account for single sign-in to any cloud and on-premises web application.</span></span> <span data-ttu-id="84e8f-117">Data Catalog używa usługi Azure AD do uwierzytelniania logowania.</span><span class="sxs-lookup"><span data-stu-id="84e8f-117">Data Catalog uses Azure AD to authenticate sign-in.</span></span> <span data-ttu-id="84e8f-118">Aby dowiedzieć się więcej, zobacz [co to jest usługa Azure Active Directory?](../active-directory/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="84e8f-118">To learn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="84e8f-119">Za pomocą [portalu Azure](http://portal.azure.com/), aby móc zalogować się za pomocą osobistego konta Microsoft lub Azure Active Directory konto służbowe.</span><span class="sxs-lookup"><span data-stu-id="84e8f-119">By using the [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="84e8f-120">Aby skonfigurować usługi Data Catalog za pomocą portalu Azure lub [portalu wykazu danych](http://www.azuredatacatalog.com), należy zalogować się przy użyciu konta usługi Azure Active Directory, a nie konta osobistego.</span><span class="sxs-lookup"><span data-stu-id="84e8f-120">To set up Data Catalog by using either the Azure portal or the [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="84e8f-121">Konfiguracja zasad w usłudze Active Directory</span><span class="sxs-lookup"><span data-stu-id="84e8f-121">Active Directory policy configuration</span></span>
<span data-ttu-id="84e8f-122">Może wystąpić sytuacja, w których można Zaloguj się do portalu wykazu danych, ale podczas próby Zaloguj się do narzędzia rejestracji źródła danych, możesz napotkać komunikat o błędzie, który uniemożliwia rejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="84e8f-122">You might encounter a situation where you can sign in to the Data Catalog portal, but when you attempt to sign in to the data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="84e8f-123">To zachowanie problem może wystąpić tylko wtedy, gdy komputer znajduje się w sieci firmowej lub może wystąpić, tylko wtedy, gdy nawiązywane z spoza sieci firmowej.</span><span class="sxs-lookup"><span data-stu-id="84e8f-123">This problem behavior might occur only when you're on the company network, or it might occur only when you're connecting from outside the company network.</span></span>

<span data-ttu-id="84e8f-124">Narzędzia rejestracji źródła danych korzysta z uwierzytelniania formularzy można sprawdzić poprawności poświadczeń użytkownika w usłudze Active Directory.</span><span class="sxs-lookup"><span data-stu-id="84e8f-124">The data source registration tool uses Forms Authentication to validate your user credentials against Active Directory.</span></span> <span data-ttu-id="84e8f-125">Aby pomóc Ci się zalogować pomyślnym, administrator usługi Active Directory należy włączyć uwierzytelnianie formularzy w ramach globalnych zasad uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="84e8f-125">To help you sign in successfully, an Active Directory administrator must enable Forms Authentication in the Global Authentication Policy.</span></span>

<span data-ttu-id="84e8f-126">W ramach globalnych zasad uwierzytelniania metody uwierzytelniania można włączyć oddzielnie w intranecie i ekstranecie połączenia, jak pokazano na poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="84e8f-126">In the Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in the following screenshot.</span></span> <span data-ttu-id="84e8f-127">Mogą wystąpić błędy logowania, jeśli nie włączono uwierzytelniania formularzy dla sieci, z którym się łączysz.</span><span class="sxs-lookup"><span data-stu-id="84e8f-127">Sign-in errors might occur if Forms Authentication is not enabled for the network from which you're connecting.</span></span>

 ![Usługi Active Directory globalnych zasad uwierzytelniania](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="84e8f-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="84e8f-129">Next steps</span></span>
<span data-ttu-id="84e8f-130">Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad uwierzytelniania](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="84e8f-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
