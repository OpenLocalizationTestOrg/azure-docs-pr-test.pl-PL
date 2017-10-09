---
title: "aaaCreate służbowego tożsamości w usłudze AAD dla systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate służbowego tożsamości w usłudze Azure Active Directory toouse z maszyn wirtualnych systemu Linux."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: b0f86d77-c669-4aa1-a095-c2aa4d9105fe
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 54c3d0b0e89fe1b2d6a9b58a46776fe446ed72b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-linux-vms"></a><span data-ttu-id="3b89c-103">Tworzenie tożsamości służbowe w usłudze Azure Active Directory toouse z maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="3b89c-103">Creating a Work or School identity in Azure Active Directory toouse with Linux VMs</span></span>
<span data-ttu-id="3b89c-104">Jeśli utworzone osobiste konto platformy Azure lub osobistych subskrypcji MSDN i utworzyć hello konta Azure tootake z środków na korzystanie hello MSDN Azure — użyto *konta Microsoft* toocreate tożsamości go.</span><span class="sxs-lookup"><span data-stu-id="3b89c-104">If you created a personal Azure account or have a personal MSDN subscription and created hello Azure account tootake advantage of hello MSDN Azure credits -- you used a *Microsoft account* identity toocreate it.</span></span> <span data-ttu-id="3b89c-105">Wiele najważniejszych funkcji Azure-- [Szablony grupy zasobów](../../azure-resource-manager/resource-group-overview.md) przykładem — wymagają konta firmowego lub szkolnego (tożsamości zarządzanych przez usługę Azure Active Directory) toowork.</span><span class="sxs-lookup"><span data-stu-id="3b89c-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) toowork.</span></span> <span data-ttu-id="3b89c-106">Możesz wykonać instrukcje hello poniżej toocreate się, że nowe służbowego konta, ponieważ na szczęście z hello czynności najważniejsze informacje osobiste konta platformy Azure jest czy pochodzą z domyślną domenę usługi Azure Active Directory służy toocreate nowej pracy lub nauki konto, które można używać z funkcje platformy Azure, które tego wymagają.</span><span class="sxs-lookup"><span data-stu-id="3b89c-106">You can follow hello instructions below toocreate a new work or school account because fortunately, one of hello best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use toocreate a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="3b89c-107">Jednak najnowszych zmian była możliwa toomanage subskrypcji z dowolnego typu konta platformy Azure przy użyciu hello `azure login` metody logowania interakcyjnego opisanej [tutaj](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="3b89c-107">However, recent changes make it possible toomanage your subscription with any type of Azure account using hello `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="3b89c-108">Możesz użyć tego mechanizmu, lub możesz wykonać hello postępuj zgodnie z instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="3b89c-108">You can either use that mechanism, or you can follow hello instructions that follow.</span></span> <span data-ttu-id="3b89c-109">Możesz również [utworzyć tożsamość firmy lub szkoły w toouse usługi Azure Active Directory z maszynami wirtualnymi systemu Windows](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b89c-109">You can also [create a work or school identity in Azure Active Directory toouse with Windows VMs](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

