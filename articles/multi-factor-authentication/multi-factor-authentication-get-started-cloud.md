---
title: "aaaGet uruchomione usługi Azure MFA w chmurze hello | Dokumentacja firmy Microsoft"
description: "Jest to hello Microsoft Azure Multi-Factor authentication strony, opisujące, jak tooget pracę z usługą Azure MFA w chmurze hello."
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
ms.openlocfilehash: a4aaf44bf08d96f2baad155072fdd6e0e727ce8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-hello-cloud"></a><span data-ttu-id="38669-103">Wprowadzenie do korzystania z usługi Azure Multi-Factor Authentication w chmurze hello</span><span class="sxs-lookup"><span data-stu-id="38669-103">Getting started with Azure Multi-Factor Authentication in hello cloud</span></span>
<span data-ttu-id="38669-104">W tym artykule przedstawiono sposób uruchamiania przy użyciu usługi Azure Multi-Factor Authentication w chmurze hello tooget.</span><span class="sxs-lookup"><span data-stu-id="38669-104">This article walks through how tooget started using Azure Multi-Factor Authentication in hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="38669-105">Hello Poniższa dokumentacja zawiera informacje na temat sposobu hello tooenable użytkowników przy użyciu **klasycznego portalu Azure**.</span><span class="sxs-lookup"><span data-stu-id="38669-105">hello following documentation provides information on how tooenable users using hello **Azure Classic Portal**.</span></span> <span data-ttu-id="38669-106">Jeśli szukasz informacji na temat tooset zapasowej Azure Multi-Factor Authentication dla użytkowników usługi Office 365, zobacz [skonfigurować usługę Multi-Factor authentication dla usługi Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span><span class="sxs-lookup"><span data-stu-id="38669-106">If you are looking for information on how tooset up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![Uwierzytelniania MFA w chmurze hello](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="38669-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="38669-108">Prerequisite</span></span>
<span data-ttu-id="38669-109">[Załóż subskrypcji platformy Azure](https://azure.microsoft.com/pricing/free-trial/) — Jeśli nie masz już subskrypcję platformy Azure, należy dla jednej toosign w górę.</span><span class="sxs-lookup"><span data-stu-id="38669-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need toosign-up for one.</span></span> <span data-ttu-id="38669-110">Jeśli dopiero zaczynasz pracę i używasz usługi Azure MFA, możesz skorzystać z subskrypcji wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="38669-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="38669-111">Włączanie usługi Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="38669-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="38669-112">Tak długo, jak użytkownicy mają licencje, które obejmują usługi Azure Multi-Factor Authentication, nie ma nic konieczność tooturn toodo na usługę Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="38669-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="38669-113">Możliwe jest rozpoczęcie wymagania weryfikacji dwuetapowej dla indywidualnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="38669-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="38669-114">licencje Hello, które umożliwiają usługi Azure MFA są:</span><span class="sxs-lookup"><span data-stu-id="38669-114">hello licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="38669-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="38669-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="38669-116">Usługa Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="38669-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="38669-117">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="38669-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="38669-118">Jeśli nie masz żadnego z tych trzech licencji lub nie ma wystarczającej liczby licencji toocover wszystkich użytkowników, które ok zbyt.</span><span class="sxs-lookup"><span data-stu-id="38669-118">If you don't have one of these three licenses, or you don't have enough licenses toocover all of your users, that's ok too.</span></span> <span data-ttu-id="38669-119">Wystarczy toodo dodatkowego kroku i [Tworzenie dostawcy uwierzytelniania wieloskładnikowego](multi-factor-authentication-get-started-auth-provider.md) w katalogu.</span><span class="sxs-lookup"><span data-stu-id="38669-119">You just have toodo an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="38669-120">Włączanie weryfikacji dwuetapowej dla użytkowników</span><span class="sxs-lookup"><span data-stu-id="38669-120">Turn on two-step verification for users</span></span>

<span data-ttu-id="38669-121">Jedną z procedur hello na liście [jak toorequire weryfikacji dwuetapowej dla użytkownika lub grupy](multi-factor-authentication-get-started-user-states.md) toostart przy użyciu usługi Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="38669-121">Use one of hello procedures listed in [How toorequire two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) toostart using Azure MFA.</span></span> <span data-ttu-id="38669-122">Możesz wybrać tooenforce weryfikacji dwuetapowej dla wszystkich logowania lub weryfikacji dwuetapowej toorequire zasady dostępu warunkowego można utworzyć tylko wtedy, gdy ma znaczenia, tooyou.</span><span class="sxs-lookup"><span data-stu-id="38669-122">You can choose tooenforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when it matters tooyou.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38669-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="38669-123">Next Steps</span></span>
<span data-ttu-id="38669-124">Teraz, kiedy mają skonfigurowane uwierzytelnianie wieloskładnikowe Azure w chmurze hello, można skonfigurować i skonfigurować wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="38669-124">Now that you have set up Azure Multi-Factor Authentication in hello cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="38669-125">Aby uzyskać bardziej szczegółowe informacje, zobacz temat [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) (Konfigurowanie usługi Azure Multi-Factor Authentication).</span><span class="sxs-lookup"><span data-stu-id="38669-125">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>

