---
title: "wymagania wstępne dotyczące aaaAzure Data Catalog | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o wymaganiach wstępnych hello, potrzebne tooget pracę z usługą Azure Data Catalog."
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
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="17eaa-103">Wymagania wstępne usługi Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="17eaa-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="17eaa-104">Należy tootake nad kilka rzeczy, przed rozpoczęciem konfigurowania usługi Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="17eaa-104">You need tootake care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="17eaa-105">Nie martw się, ten proces nie długo.</span><span class="sxs-lookup"><span data-stu-id="17eaa-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="17eaa-106">Subskrypcja platformy Azure</span><span class="sxs-lookup"><span data-stu-id="17eaa-106">Azure subscription</span></span>
<span data-ttu-id="17eaa-107">tooset się wykaz danych musi być właścicielem hello lub współwłaściciel subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="17eaa-107">tooset up Data Catalog, you must be hello owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="17eaa-108">Subskrypcje platformy Azure ułatwić organizowanie dostęp do zasobów usługi toocloud, takie jak Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="17eaa-108">Azure subscriptions help you organize access toocloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="17eaa-109">Subskrypcje można także kontrolować sposób użycia zasobów jest zgłaszane, rozliczane i uregulowaniu płatności.</span><span class="sxs-lookup"><span data-stu-id="17eaa-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="17eaa-110">Każda subskrypcja może mieć oddzielne ustawienia rozliczeń i płatności, więc można dodać subskrypcji i plany, które zależą od działów, projektów, biuro regionalne i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="17eaa-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="17eaa-111">Co usługa w chmurze należy tooa subskrypcji, i potrzebujesz toohave subskrypcji przed rozpoczęciem konfigurowania usługi Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="17eaa-111">Every cloud service belongs tooa subscription, and you need toohave a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="17eaa-112">toolearn więcej, zobacz [Zarządzanie kontami, subskrypcje i ról administracyjnych](../active-directory/active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="17eaa-112">toolearn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="17eaa-113">Usługa Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17eaa-113">Azure Active Directory</span></span>
<span data-ttu-id="17eaa-114">tooset się wykaz danych, użytkownik musi zalogować się przy użyciu konta użytkownika usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17eaa-114">tooset up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="17eaa-115">Usługa Azure AD zapewnia prosty sposób dla firm toomanage tożsamości i dostępu, zarówno w chmurze hello i lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="17eaa-115">Azure AD provides an easy way for your business toomanage identity and access, both in hello cloud and on-premises.</span></span> <span data-ttu-id="17eaa-116">Użytkownicy mogą używać jednego konta firmowego lub szkolnego dla pojedynczego tooany logowania w chmurze i lokalnych aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="17eaa-116">Users can use a single work or school account for single sign-in tooany cloud and on-premises web application.</span></span> <span data-ttu-id="17eaa-117">Data Catalog używa usługi Azure AD tooauthenticate logowania.</span><span class="sxs-lookup"><span data-stu-id="17eaa-117">Data Catalog uses Azure AD tooauthenticate sign-in.</span></span> <span data-ttu-id="17eaa-118">toolearn więcej, zobacz [co to jest usługa Azure Active Directory?](../active-directory/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17eaa-118">toolearn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="17eaa-119">Za pomocą hello [portalu Azure](http://portal.azure.com/), aby móc zalogować się za pomocą osobistego konta Microsoft lub Azure Active Directory konto służbowe.</span><span class="sxs-lookup"><span data-stu-id="17eaa-119">By using hello [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="17eaa-120">tooset się wykaz danych przy użyciu albo hello portalu Azure lub hello [portalu wykazu danych](http://www.azuredatacatalog.com), należy zalogować się przy użyciu konta usługi Azure Active Directory, a nie konta osobistego.</span><span class="sxs-lookup"><span data-stu-id="17eaa-120">tooset up Data Catalog by using either hello Azure portal or hello [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="17eaa-121">Konfiguracja zasad w usłudze Active Directory</span><span class="sxs-lookup"><span data-stu-id="17eaa-121">Active Directory policy configuration</span></span>
<span data-ttu-id="17eaa-122">Może wystąpić sytuacja, w których możesz zarejestrować się w portalu wykazu danych toohello, ale podczas próby toosign w narzędzia rejestracji źródła danych toohello, wystąpi komunikat o błędzie, który uniemożliwia rejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="17eaa-122">You might encounter a situation where you can sign in toohello Data Catalog portal, but when you attempt toosign in toohello data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="17eaa-123">To zachowanie problem może wystąpić tylko wtedy, gdy komputer znajduje się w sieci firmowej hello lub może wystąpić, tylko jeśli łączysz się z hello poza siecią firmową.</span><span class="sxs-lookup"><span data-stu-id="17eaa-123">This problem behavior might occur only when you're on hello company network, or it might occur only when you're connecting from outside hello company network.</span></span>

<span data-ttu-id="17eaa-124">narzędzia rejestracji źródła danych Hello korzysta z uwierzytelniania formularzy toovalidate poświadczenia użytkownika w usłudze Active Directory.</span><span class="sxs-lookup"><span data-stu-id="17eaa-124">hello data source registration tool uses Forms Authentication toovalidate your user credentials against Active Directory.</span></span> <span data-ttu-id="17eaa-125">toohelp logowania pomyślnie, administrator usługi Active Directory należy włączyć uwierzytelnianie formularzy w hello globalne zasady uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="17eaa-125">toohelp you sign in successfully, an Active Directory administrator must enable Forms Authentication in hello Global Authentication Policy.</span></span>

<span data-ttu-id="17eaa-126">Hello globalne zasady uwierzytelniania metody uwierzytelniania można połączeń włączone oddzielnie dla intranetu i ekstranetu, pokazane na powitania po zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="17eaa-126">In hello Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in hello following screenshot.</span></span> <span data-ttu-id="17eaa-127">Mogą wystąpić błędy logowania, jeśli nie włączono uwierzytelniania formularzy hello sieci, z którym się łączysz.</span><span class="sxs-lookup"><span data-stu-id="17eaa-127">Sign-in errors might occur if Forms Authentication is not enabled for hello network from which you're connecting.</span></span>

 ![Usługi Active Directory globalnych zasad uwierzytelniania](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="17eaa-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="17eaa-129">Next steps</span></span>
<span data-ttu-id="17eaa-130">Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad uwierzytelniania](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="17eaa-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
