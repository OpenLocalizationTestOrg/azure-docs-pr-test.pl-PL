---
title: "Tworzenie tożsamości służbowe w usłudze AAD dla systemu Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć tożsamość firmy lub szkoły w usłudze Azure Active Directory do użycia z maszyn wirtualnych systemu Windows."
services: virtual-machines-windows
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d07dca34-618a-48aa-9971-03d9c1210f4a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 7694b959a384aaed213adc31e02debca31b7c131
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-to-use-with-windows-vms"></a><span data-ttu-id="cf87a-103">Tworzenie tożsamości służbowe w usłudze Azure Active Directory do użycia z maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="cf87a-103">Creating a Work or School identity in Azure Active Directory to use with Windows VMs</span></span>
<span data-ttu-id="cf87a-104">Jeśli utworzone osobiste konto platformy Azure lub osobistych subskrypcji MSDN i utworzyć konto platformy Azure, aby skorzystać z środków MSDN Azure — użyto *konta Microsoft* tożsamości, aby go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="cf87a-104">If you created a personal Azure account or have a personal MSDN subscription and created the Azure account to take advantage of the MSDN Azure credits -- you used a *Microsoft account* identity to create it.</span></span> <span data-ttu-id="cf87a-105">Wiele najważniejszych funkcji Azure-- [Szablony grupy zasobów](../../azure-resource-manager/resource-group-overview.md) przykładem — wymagają konta firmowego lub szkolnego (tożsamość zarządzane przez usługę Azure Active Directory) do pracy.</span><span class="sxs-lookup"><span data-stu-id="cf87a-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) to work.</span></span> <span data-ttu-id="cf87a-106">Aby wykonać instrukcjami poniżej, aby utworzyć nowe konta firmowego lub szkolnego, ponieważ na szczęście z czynności najważniejsze informacje osobiste konta platformy Azure jest pochodzi z domyślnej domeny usługi Azure Active Directory służy do tworzenia nowego konta firmowego lub szkolnego korzystające z funkcjami platformy Azure, które tego wymagają.</span><span class="sxs-lookup"><span data-stu-id="cf87a-106">You can follow the instructions below to create a new work or school account because fortunately, one of the best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use to create a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="cf87a-107">Jednak ostatnie zmiany umożliwiają Zarządzanie subskrypcją z dowolnego typu za pomocą konta Azure `azure login` metody logowania interakcyjnego opisanej [tutaj](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="cf87a-107">However, recent changes make it possible to manage your subscription with any type of Azure account using the `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="cf87a-108">Możesz użyć tego mechanizmu, lub możesz wykonać postępuj zgodnie z instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="cf87a-108">You can either use that mechanism, or you can follow the instructions that follow.</span></span> <span data-ttu-id="cf87a-109">Możesz również [tworzenie służbowego tożsamości w usłudze Azure Active Directory do użycia z maszyn wirtualnych systemu Linux](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cf87a-109">You can also [create a work or school identity in Azure Active Directory to use with Linux VMs](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

