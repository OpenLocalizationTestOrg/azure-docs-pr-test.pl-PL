---
title: "Wprowadzenie do usługi Azure MFA w chmurze | Microsoft Docs"
description: "Ta strona dotyczy usługi Microsoft Azure Multi-Factor Authentication i zawiera informacje umożliwiające rozpoczęcie korzystania z usługi Azure MFA w chmurze."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 6b2e6549-1a26-4666-9c4a-cbe5d64c4e66
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/24/2017
ms.author: kgremban
ms.openlocfilehash: 19f3228b874fc4e37bf83388dae4341428226482
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-the-cloud"></a><span data-ttu-id="bc049-103">Wprowadzenie do usługi Azure Multi-Factor Authentication w chmurze</span><span class="sxs-lookup"><span data-stu-id="bc049-103">Getting started with Azure Multi-Factor Authentication in the cloud</span></span>
<span data-ttu-id="bc049-104">W tym artykule opisano, jak rozpocząć korzystanie z usługi Azure Multi-Factor Authentication w chmurze.</span><span class="sxs-lookup"><span data-stu-id="bc049-104">This article walks through how to get started using Azure Multi-Factor Authentication in the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="bc049-105">Poniższa dokumentacja zawiera informacje dotyczące umożliwiania użytkownikom korzystania z **klasycznego portalu Azure**.</span><span class="sxs-lookup"><span data-stu-id="bc049-105">The following documentation provides information on how to enable users using the **Azure Classic Portal**.</span></span> <span data-ttu-id="bc049-106">Jeśli szukasz informacji na temat konfigurowania usługi Azure Multi-Factor Authentication dla użytkowników usługi O365, zobacz temat [Konfigurowanie usługi Multi-Factor Authentication dla usługi Office 365](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="bc049-106">If you are looking for information on how to set up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![Usługa MFA w chmurze](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="bc049-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bc049-108">Prerequisite</span></span>
<span data-ttu-id="bc049-109">[Utworzenie konta na potrzeby subskrypcji platformy Azure](https://azure.microsoft.com/pricing/free-trial/) — jeśli nie masz jeszcze subskrypcji platformy Azure, musisz utworzyć konto.</span><span class="sxs-lookup"><span data-stu-id="bc049-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need to sign-up for one.</span></span> <span data-ttu-id="bc049-110">Jeśli dopiero zaczynasz pracę i używasz usługi Azure MFA, możesz skorzystać z subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="bc049-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="bc049-111">Włączanie usługi Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="bc049-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="bc049-112">Dopóki użytkownicy będą mieli licencje obejmujące usługę Azure Multi-Factor Authentication, do jej włączenia nie będzie wymagane wykonanie żadnych czynności.</span><span class="sxs-lookup"><span data-stu-id="bc049-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need to do to turn on Azure MFA.</span></span> <span data-ttu-id="bc049-113">Możliwe jest rozpoczęcie wymagania weryfikacji dwuetapowej dla indywidualnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bc049-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="bc049-114">Licencje, które umożliwiają włączenie usługi Azure MFA, to:</span><span class="sxs-lookup"><span data-stu-id="bc049-114">The licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="bc049-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="bc049-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="bc049-116">Usługa Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="bc049-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="bc049-117">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="bc049-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="bc049-118">Jeśli nie masz żadnej z tych trzech licencji ani nie masz wystarczającej liczby licencji, aby obejmowały wszystkich użytkowników, to też nie stanowi problemu.</span><span class="sxs-lookup"><span data-stu-id="bc049-118">If you don't have one of these three licenses, or you don't have enough licenses to cover all of your users, that's ok too.</span></span> <span data-ttu-id="bc049-119">Konieczne jest tylko wykonanie dodatkowego kroku w celu [utworzenia dostawcy usługi Multi-Factor Authentication](multi-factor-authentication-get-started-auth-provider.md) w katalogu.</span><span class="sxs-lookup"><span data-stu-id="bc049-119">You just have to do an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="bc049-120">Włączanie weryfikacji dwuetapowej dla użytkowników</span><span class="sxs-lookup"><span data-stu-id="bc049-120">Turn on two-step verification for users</span></span>

<span data-ttu-id="bc049-121">Wykonaj jedną z procedur wymienionych w temacie [How to require two-step verification for a user or group (Jak wymagać weryfikacji dwuetapowej użytkownika lub grupy)](multi-factor-authentication-get-started-user-states.md), aby rozpocząć korzystanie z usługi Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="bc049-121">Use one of the procedures listed in [How to require two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) to start using Azure MFA.</span></span> <span data-ttu-id="bc049-122">Weryfikację dwuetapową możesz wymusić dla wszystkich logowań lub utworzyć zasady dostępu warunkowego, które wymuszają weryfikację dwuetapową tylko wtedy, gdy jest to pożądane.</span><span class="sxs-lookup"><span data-stu-id="bc049-122">You can choose to enforce two-step verification for all sign-ins, or you can create conditional access policies to require two-step verification only when it matters to you.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc049-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bc049-123">Next Steps</span></span>
<span data-ttu-id="bc049-124">Po skonfigurowaniu usługi Azure Multi-Factor Authentication w chmurze można przystąpić do konfigurowania wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="bc049-124">Now that you have set up Azure Multi-Factor Authentication in the cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="bc049-125">Aby uzyskać bardziej szczegółowe informacje, zobacz temat [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) (Konfigurowanie usługi Azure Multi-Factor Authentication).</span><span class="sxs-lookup"><span data-stu-id="bc049-125">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>

