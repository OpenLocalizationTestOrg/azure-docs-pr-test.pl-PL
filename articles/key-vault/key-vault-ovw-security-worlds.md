---
ms.assetid: 
title: "środowiska security World usługi Key Vault aaaAzure | Dokumentacja firmy Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="a475e-102">Środowiska usługi Azure Key Vault security World i geograficzne granice</span><span class="sxs-lookup"><span data-stu-id="a475e-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="a475e-103">Usługa Azure Key Vault jest usługą wielodostępnych i korzysta z puli sprzętowych modułów zabezpieczeń (HSM) w każdej lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a475e-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="a475e-104">Wszystkie moduły HSM w lokalizacjach Azure w hello tego samego regionu geograficznego udziału hello tej samej granicy kryptograficznych (środowiska zabezpieczeń firmy Thales).</span><span class="sxs-lookup"><span data-stu-id="a475e-104">All HSMs at Azure locations in hello same geographic region share hello same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="a475e-105">Na przykład wschodnie stany USA i zachód udostępnianie USA hello tego samego środowiska zabezpieczeń security world, ponieważ należą lokalizacja geograficzna toohello Stanów Zjednoczonych.</span><span class="sxs-lookup"><span data-stu-id="a475e-105">For example, East US and West US share hello same security world because they belong toohello US geo location.</span></span> <span data-ttu-id="a475e-106">Podobnie wszystkich lokalizacji platformy Azure w Japonii udziału hello tego samego środowiska zabezpieczeń security world i wszystkich lokalizacji platformy Azure w Australii, Indie i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="a475e-106">Similarly, all Azure locations in Japan share hello same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="a475e-107">Zachowanie kopii zapasowej i przywracania</span><span class="sxs-lookup"><span data-stu-id="a475e-107">Backup and restore behavior</span></span>

<span data-ttu-id="a475e-108">Kopii zapasowej klucza z magazynu kluczy w jednej lokalizacji platformy Azure można przywrócić tooa magazynu kluczy w innej lokalizacji platformy Azure, dopóki oba te warunki są spełnione:</span><span class="sxs-lookup"><span data-stu-id="a475e-108">A backup taken of a key from a key vault in one Azure location can be restored tooa key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="a475e-109">Zarówno hello Azure lokalizacji należy toohello tej samej lokalizacji geograficznej</span><span class="sxs-lookup"><span data-stu-id="a475e-109">Both of hello Azure locations belong toohello same geographical location</span></span>
- <span data-ttu-id="a475e-110">Magazynów kluczy hello należeć toohello tej samej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a475e-110">Both of hello key vaults belong toohello same Azure subscription</span></span>

<span data-ttu-id="a475e-111">Na przykład kopii zapasowej, w ramach danej subskrypcji klucza w magazynie kluczy w Indie Zachodnie może być tylko przywróconej tooanother magazynu kluczy w hello tej samej subskrypcji i lokalizacji geo. Indie Zachodnie, Indie środkowe lub Indie Południowe</span><span class="sxs-lookup"><span data-stu-id="a475e-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored tooanother key vault in hello same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="a475e-112">Regiony i produktów</span><span class="sxs-lookup"><span data-stu-id="a475e-112">Regions and products</span></span>

- [<span data-ttu-id="a475e-113">Regiony platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a475e-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="a475e-114">Produkty firmy Microsoft według regionu</span><span class="sxs-lookup"><span data-stu-id="a475e-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="a475e-115">Regiony są mapowane toosecurity względem, wyświetlane jako głównych pozycji w tabelach hello:</span><span class="sxs-lookup"><span data-stu-id="a475e-115">Regions are mapped toosecurity worlds, shown as major headings in hello tables:</span></span>

<span data-ttu-id="a475e-116">W produktach hello w artykule region, na przykład Witaj **Americas** karta zawiera wschód US, ŚRODKOWE stany USA, zachodnie stany USA wszystkie mapowania toohello Americas regionu.</span><span class="sxs-lookup"><span data-stu-id="a475e-116">In hello products by region article, for example, hello **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping toohello Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="a475e-117">Wyjątek jest nam wschodnie DOD i nam DOD centralnej własnych środowiska security World.</span><span class="sxs-lookup"><span data-stu-id="a475e-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="a475e-118">Podobnie na powitania **Europy** karcie, EUROPA Północna i EUROPA ZACHODNIA, są mapowane toohello regionie Europy.</span><span class="sxs-lookup"><span data-stu-id="a475e-118">Similarly, on hello **Europe** tab, NORTH EUROPE and WEST EUROPE both map toohello Europe region.</span></span> <span data-ttu-id="a475e-119">Witaj samo dotyczy również na powitania **Azja i Pacyfik** kartę.</span><span class="sxs-lookup"><span data-stu-id="a475e-119">hello same is also true on hello **Asia Pacific** tab.</span></span>



