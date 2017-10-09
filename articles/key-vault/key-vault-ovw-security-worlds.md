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
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a>Środowiska usługi Azure Key Vault security World i geograficzne granice

Usługa Azure Key Vault jest usługą wielodostępnych i korzysta z puli sprzętowych modułów zabezpieczeń (HSM) w każdej lokalizacji platformy Azure. 

Wszystkie moduły HSM w lokalizacjach Azure w hello tego samego regionu geograficznego udziału hello tej samej granicy kryptograficznych (środowiska zabezpieczeń firmy Thales). Na przykład wschodnie stany USA i zachód udostępnianie USA hello tego samego środowiska zabezpieczeń security world, ponieważ należą lokalizacja geograficzna toohello Stanów Zjednoczonych. Podobnie wszystkich lokalizacji platformy Azure w Japonii udziału hello tego samego środowiska zabezpieczeń security world i wszystkich lokalizacji platformy Azure w Australii, Indie i tak dalej. 

## <a name="backup-and-restore-behavior"></a>Zachowanie kopii zapasowej i przywracania

Kopii zapasowej klucza z magazynu kluczy w jednej lokalizacji platformy Azure można przywrócić tooa magazynu kluczy w innej lokalizacji platformy Azure, dopóki oba te warunki są spełnione:

- Zarówno hello Azure lokalizacji należy toohello tej samej lokalizacji geograficznej
- Magazynów kluczy hello należeć toohello tej samej subskrypcji platformy Azure

Na przykład kopii zapasowej, w ramach danej subskrypcji klucza w magazynie kluczy w Indie Zachodnie może być tylko przywróconej tooanother magazynu kluczy w hello tej samej subskrypcji i lokalizacji geo. Indie Zachodnie, Indie środkowe lub Indie Południowe

## <a name="regions-and-products"></a>Regiony i produktów

- [Regiony platformy Azure](https://azure.microsoft.com/regions/)
- [Produkty firmy Microsoft według regionu](https://azure.microsoft.com/regions/services/)

Regiony są mapowane toosecurity względem, wyświetlane jako głównych pozycji w tabelach hello:

W produktach hello w artykule region, na przykład Witaj **Americas** karta zawiera wschód US, ŚRODKOWE stany USA, zachodnie stany USA wszystkie mapowania toohello Americas regionu. 

>[!NOTE]
>Wyjątek jest nam wschodnie DOD i nam DOD centralnej własnych środowiska security World. 

Podobnie na powitania **Europy** karcie, EUROPA Północna i EUROPA ZACHODNIA, są mapowane toohello regionie Europy. Witaj samo dotyczy również na powitania **Azja i Pacyfik** kartę.



