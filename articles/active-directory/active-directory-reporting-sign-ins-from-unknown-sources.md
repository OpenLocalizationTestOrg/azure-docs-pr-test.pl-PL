---
title: "Logowania z nieznanych źródeł"
description: "Raport, który wskazuje użytkowników, którzy pomyślnie zalogowali się do katalogu z anonimowy serwer proxy adresu IP."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: 2f045543-1578-4972-bf70-b35310f23110
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 90006121e4b3392f6e3ecffb4a56aca330feb02f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-unknown-sources"></a><span data-ttu-id="ffa4a-103">Logowania z nieznanych źródeł</span><span class="sxs-lookup"><span data-stu-id="ffa4a-103">Sign ins from unknown sources</span></span>
<span data-ttu-id="ffa4a-104">Ten raport wskazuje użytkowników, którzy zalogowali się pomyślnie katalogu podczas przypisany klientowi adres IP, który został uznany przez firmę Microsoft jako adres IP anonimowy serwer proxy (na przykład adres IP w sieci Tor).</span><span class="sxs-lookup"><span data-stu-id="ffa4a-104">This report indicates users who have successfully signed in to your directory while assigned a client IP address that has been recognized by Microsoft as an anonymous proxy IP address (for example, a Tor IP address).</span></span> <span data-ttu-id="ffa4a-105">Te serwery proxy są często używane przez użytkowników, aby ukryć adres IP komputera, które mogą być używane do złośliwymi działaniami.</span><span class="sxs-lookup"><span data-stu-id="ffa4a-105">These proxies are often used by users that want to hide their computer’s IP address, and may be used for malicious intent.</span></span>

<span data-ttu-id="ffa4a-106">Wyniki z ten raport będzie przedstawiał liczbę razy użytkownik pomyślnie zalogował się do katalogu z tego adresu i adres IP serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="ffa4a-106">Results from this report will show the number of times a user successfully signed in to your directory from that address and the proxy’s IP address.</span></span>

![Logowania z nieznanych źródeł](./media/active-directory-reporting-sign-ins-from-unknown-sources/signInsFromUnknownSources.PNG)

