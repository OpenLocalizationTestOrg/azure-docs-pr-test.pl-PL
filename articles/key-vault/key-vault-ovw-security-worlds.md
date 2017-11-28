---
ms.assetid: 
title: "Względem zabezpieczeń usługi Azure Key Vault | Dokumentacja firmy Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 921bbd109c9ea98d8b5c286a7512bed026412d26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="bf01a-102">Środowiska usługi Azure Key Vault security World i geograficzne granice</span><span class="sxs-lookup"><span data-stu-id="bf01a-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="bf01a-103">Usługa Azure Key Vault jest usługą wielodostępnych i korzysta z puli sprzętowych modułów zabezpieczeń (HSM) w każdej lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bf01a-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="bf01a-104">Wszystkie moduły HSM w lokalizacjach Azure w tym samym regionie geograficznym udostępnianie tej samej granicy kryptograficznych (środowiska zabezpieczeń firmy Thales).</span><span class="sxs-lookup"><span data-stu-id="bf01a-104">All HSMs at Azure locations in the same geographic region share the same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="bf01a-105">Na przykład wschodnie stany USA i zachodnie stany USA udziału tego samego środowiska zabezpieczeń security world, ponieważ należą do lokalizacja geograficzna Stanów Zjednoczonych.</span><span class="sxs-lookup"><span data-stu-id="bf01a-105">For example, East US and West US share the same security world because they belong to the US geo location.</span></span> <span data-ttu-id="bf01a-106">Podobnie wszystkich lokalizacji platformy Azure w Japonii współużytkowanie tego samego środowiska zabezpieczeń security world i wszystkich lokalizacji platformy Azure w Australii, Indie i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="bf01a-106">Similarly, all Azure locations in Japan share the same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="bf01a-107">Zachowanie kopii zapasowej i przywracania</span><span class="sxs-lookup"><span data-stu-id="bf01a-107">Backup and restore behavior</span></span>

<span data-ttu-id="bf01a-108">Do magazynu kluczy w innej lokalizacji platformy Azure, można przywrócić kopii zapasowej klucza z magazynu kluczy w jednej lokalizacji platformy Azure, dopóki oba te warunki są spełnione:</span><span class="sxs-lookup"><span data-stu-id="bf01a-108">A backup taken of a key from a key vault in one Azure location can be restored to a key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="bf01a-109">Azure lokalizacji należeć do tej samej lokalizacji geograficznej</span><span class="sxs-lookup"><span data-stu-id="bf01a-109">Both of the Azure locations belong to the same geographical location</span></span>
- <span data-ttu-id="bf01a-110">Zarówno magazynów kluczy należą do tej samej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bf01a-110">Both of the key vaults belong to the same Azure subscription</span></span>

<span data-ttu-id="bf01a-111">Na przykład kopii zapasowej, w ramach danej subskrypcji klucza w magazynie kluczy w Indie Zachodnie można przywrócić tylko do innego magazynu kluczy w tej samej subskrypcji i lokalizacji geo. Indie Zachodnie, Indie środkowe lub Indie Południowe</span><span class="sxs-lookup"><span data-stu-id="bf01a-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored to another key vault in the same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="bf01a-112">Regiony i produktów</span><span class="sxs-lookup"><span data-stu-id="bf01a-112">Regions and products</span></span>

- [<span data-ttu-id="bf01a-113">Regiony platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bf01a-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="bf01a-114">Produkty firmy Microsoft według regionu</span><span class="sxs-lookup"><span data-stu-id="bf01a-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="bf01a-115">Regiony są mapowane do środowiska security World, wyświetlane jako głównych pozycji w tabelach:</span><span class="sxs-lookup"><span data-stu-id="bf01a-115">Regions are mapped to security worlds, shown as major headings in the tables:</span></span>

<span data-ttu-id="bf01a-116">W produktach artykule region, na przykład **Americas** karta zawiera wschód US, ŚRODKOWE stany USA, zachodnie stany USA wszystkie mapowania do obszaru Americas.</span><span class="sxs-lookup"><span data-stu-id="bf01a-116">In the products by region article, for example, the **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping to the Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="bf01a-117">Wyjątek jest nam wschodnie DOD i nam DOD centralnej własnych środowiska security World.</span><span class="sxs-lookup"><span data-stu-id="bf01a-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="bf01a-118">Podobnie na **Europy** karcie, Europa Północna, EUROPA i EUROPA ZACHODNIA, są mapowane na regionie Europy.</span><span class="sxs-lookup"><span data-stu-id="bf01a-118">Similarly, on the **Europe** tab, NORTH EUROPE and WEST EUROPE both map to the Europe region.</span></span> <span data-ttu-id="bf01a-119">Dotyczy to również na **Azja i Pacyfik** kartę.</span><span class="sxs-lookup"><span data-stu-id="bf01a-119">The same is also true on the **Asia Pacific** tab.</span></span>



