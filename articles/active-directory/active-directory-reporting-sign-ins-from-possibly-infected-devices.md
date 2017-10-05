---
title: "Logowania z potencjalnie zainfekowanych urządzeń"
description: "Raport, który zawiera znak w prób, wykonanych z urządzeń, na których mogą być uruchomione niektóre złośliwe oprogramowanie (złośliwego oprogramowania)."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: d0361662-d970-4a66-8eb3-72e9f8824dcf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 3809e20937d8d9829675e20f893101cb849dcea2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-possibly-infected-devices"></a><span data-ttu-id="22855-103">Logowania z potencjalnie zainfekowanych urządzeń</span><span class="sxs-lookup"><span data-stu-id="22855-103">Sign ins from possibly infected devices</span></span>
<span data-ttu-id="22855-104">Ten raport próbuje zidentyfikować urządzenia użytkowników, która ma zostać zainfekowany i są teraz częścią botnet.</span><span class="sxs-lookup"><span data-stu-id="22855-104">This report attempts to identify your users' devices that that have become infected and are now part of a botnet.</span></span> <span data-ttu-id="22855-105">Firma Microsoft skorelowania logowania użytkowników z adresami IP, które wiemy, że można kontaktu z serwerami botnet adresów IP.</span><span class="sxs-lookup"><span data-stu-id="22855-105">We correlate IP addresses of users' sign-ins against IP addresses that we know to be in contact with botnet servers.</span></span>

<span data-ttu-id="22855-106">Zalecenie: W tym raporcie flagi adresy IP, nie urządzeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="22855-106">Recommendation: This report flags IP addresses, not user devices.</span></span> <span data-ttu-id="22855-107">Firma Microsoft zaleca, skontaktuj się z użytkownika i skanowanie wszystkich urządzeń użytkownika należy się upewnić.</span><span class="sxs-lookup"><span data-stu-id="22855-107">We recommend that you contact the user and scan all the user's devices to be certain.</span></span> <span data-ttu-id="22855-108">Istnieje również możliwość, że jest zainfekowany urządzenia osobiste użytkownika, lub czy kogoś innego niż użytkownik, który korzystał z tego samego adresu IP, jako użytkownik, ma zainfekowanego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="22855-108">It is also possible that a user's personal device is infected, or that someone other than the user, who was using the same IP address as the user, has an infected device.</span></span>

<span data-ttu-id="22855-109">Aby uzyskać więcej informacji na temat adresów infekcji złośliwym oprogramowaniem, zobacz [Centrum ochrony przed złośliwym oprogramowaniem](http://go.microsoft.com/fwlink/?linkid=335773).</span><span class="sxs-lookup"><span data-stu-id="22855-109">For more information about how to address malware infections, see the [Malware Protection Center](http://go.microsoft.com/fwlink/?linkid=335773).</span></span>

![Logowania z potencjalnie zainfekowanych urządzeń](./media/active-directory-reporting-sign-ins-from-possibly-infected-devices/signInsFromPossiblyInfectedDevices.PNG)

