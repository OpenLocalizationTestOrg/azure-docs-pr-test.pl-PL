---
title: "Azure AD Connect: Deklaratywne inicjowania obsługi administracyjnej wyrażeń | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono deklaratywne wyrażenia inicjowania obsługi administracyjnej."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: e3ea53c8-3801-4acf-a297-0fb9bb1bf11d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: e3a03a97b10e04fb85261620879b2102e1db8465
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a><span data-ttu-id="363f8-103">Synchronizacja programu Azure AD Connect: opis deklaratywne wyrażenia inicjowania obsługi administracyjnej</span><span class="sxs-lookup"><span data-stu-id="363f8-103">Azure AD Connect sync: Understanding Declarative Provisioning Expressions</span></span>
<span data-ttu-id="363f8-104">Synchronizacja programu Azure AD Connect tworzy na aprowizacją deklaratywną po raz pierwszy wprowadzone w programie Forefront Identity Manager 2010.</span><span class="sxs-lookup"><span data-stu-id="363f8-104">Azure AD Connect sync builds on declarative provisioning first introduced in Forefront Identity Manager 2010.</span></span> <span data-ttu-id="363f8-105">Umożliwia wdrożenie logiki biznesowej tożsamości pełnej integracji bez konieczności pisania kodu skompilowanego.</span><span class="sxs-lookup"><span data-stu-id="363f8-105">It allows you to implement your complete identity integration business logic without the need to write compiled code.</span></span>

<span data-ttu-id="363f8-106">Integralną część aprowizacją deklaratywną jest język wyrażenia w przepływów atrybutów.</span><span class="sxs-lookup"><span data-stu-id="363f8-106">An essential part of declarative provisioning is the expression language used in attribute flows.</span></span> <span data-ttu-id="363f8-107">Język używany jest podzbiorem Visual Basic for Applications (VBA) Microsoft®.</span><span class="sxs-lookup"><span data-stu-id="363f8-107">The language used is a subset of Microsoft® Visual Basic® for Applications (VBA).</span></span> <span data-ttu-id="363f8-108">Ten język jest używany w programie Microsoft Office, a użytkownicy mający doświadczenie VBScript również rozpozna go.</span><span class="sxs-lookup"><span data-stu-id="363f8-108">This language is used in Microsoft Office and users with experience of VBScript will also recognize it.</span></span> <span data-ttu-id="363f8-109">Wyrażenie języka deklaratywne inicjowania obsługi tylko przy użyciu funkcji i nie jest języka structured.</span><span class="sxs-lookup"><span data-stu-id="363f8-109">The Declarative Provisioning Expression Language is only using functions and is not a structured language.</span></span> <span data-ttu-id="363f8-110">Nie ma żadnych metod ani instrukcji.</span><span class="sxs-lookup"><span data-stu-id="363f8-110">There are no methods or statements.</span></span> <span data-ttu-id="363f8-111">Funkcje zamiast tego są zagnieżdżone przepływem programu express.</span><span class="sxs-lookup"><span data-stu-id="363f8-111">Functions are instead nested to express program flow.</span></span>

<span data-ttu-id="363f8-112">Aby uzyskać więcej informacji, zobacz [Visual Basic dla odwołanie językowe aplikacje pakietu Office 2013 — Zapraszamy](https://msdn.microsoft.com/library/gg264383.aspx).</span><span class="sxs-lookup"><span data-stu-id="363f8-112">For more details, see [Welcome to the Visual Basic for Applications language reference for Office 2013](https://msdn.microsoft.com/library/gg264383.aspx).</span></span>

<span data-ttu-id="363f8-113">Atrybuty są silnie typizowane.</span><span class="sxs-lookup"><span data-stu-id="363f8-113">The attributes are strongly typed.</span></span> <span data-ttu-id="363f8-114">Funkcja akceptuje tylko atrybuty poprawnego typu.</span><span class="sxs-lookup"><span data-stu-id="363f8-114">A function only accepts attributes of the correct type.</span></span> <span data-ttu-id="363f8-115">Jest również wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="363f8-115">It is also case-sensitive.</span></span> <span data-ttu-id="363f8-116">Zarówno funkcja nazw i atrybut musi mieć odpowiednie wielkości liter lub zostanie zgłoszony błąd.</span><span class="sxs-lookup"><span data-stu-id="363f8-116">Both function names and attribute names must have proper casing or an error is thrown.</span></span>

## <a name="language-definitions-and-identifiers"></a><span data-ttu-id="363f8-117">Język definicji i identyfikatory</span><span class="sxs-lookup"><span data-stu-id="363f8-117">Language definitions and Identifiers</span></span>
* <span data-ttu-id="363f8-118">Funkcje mają nazwy, a następnie argumenty w nawiasach: FunctionName (argument 1, argument N).</span><span class="sxs-lookup"><span data-stu-id="363f8-118">Functions have a name followed by arguments in brackets: FunctionName(argument 1, argument N).</span></span>
* <span data-ttu-id="363f8-119">Atrybuty są identyfikowane za pomocą nawiasy kwadratowe: [attributeName]</span><span class="sxs-lookup"><span data-stu-id="363f8-119">Attributes are identified by square brackets: [attributeName]</span></span>
* <span data-ttu-id="363f8-120">Parametry są identyfikowane za pomocą procentu: % ParameterName %</span><span class="sxs-lookup"><span data-stu-id="363f8-120">Parameters are identified by percent signs: %ParameterName%</span></span>
* <span data-ttu-id="363f8-121">Stałe typu String są ujęte w cudzysłowy: na przykład "Contoso" (Uwaga: należy użyć cudzysłowów prostych "" oraz nie cudzysłów "")</span><span class="sxs-lookup"><span data-stu-id="363f8-121">String constants are surrounded by quotes: For example, "Contoso" (Note: must use straight quotes "" and not smart quotes “”)</span></span>
* <span data-ttu-id="363f8-122">Wartości numeryczne wyrażone bez cudzysłowów i powinien być dziesiętną.</span><span class="sxs-lookup"><span data-stu-id="363f8-122">Numeric values are expressed without quotes and expected to be decimal.</span></span> <span data-ttu-id="363f8-123">Wartości szesnastkowe są poprzedzane prefiksem & h</span><span class="sxs-lookup"><span data-stu-id="363f8-123">Hexadecimal values are prefixed with &H.</span></span> <span data-ttu-id="363f8-124">Na przykład 98052 & HFF</span><span class="sxs-lookup"><span data-stu-id="363f8-124">For example, 98052, &HFF</span></span>
* <span data-ttu-id="363f8-125">Wartości logiczna są wyrażane za pomocą stałych: True i False.</span><span class="sxs-lookup"><span data-stu-id="363f8-125">Boolean values are expressed with constants: True, False.</span></span>
* <span data-ttu-id="363f8-126">Literały i wbudowane stałe są wyrażane tylko ich nazwą: NULL, CRLF, IgnoreThisFlow</span><span class="sxs-lookup"><span data-stu-id="363f8-126">Built-in constants and literals are expressed with only their name: NULL, CRLF, IgnoreThisFlow</span></span>

### <a name="functions"></a><span data-ttu-id="363f8-127">Funkcje</span><span class="sxs-lookup"><span data-stu-id="363f8-127">Functions</span></span>
<span data-ttu-id="363f8-128">Aprowizacja deklaratywna używa wielu funkcji, aby umożliwić możliwości przekształcania wartości atrybutu.</span><span class="sxs-lookup"><span data-stu-id="363f8-128">Declarative provisioning uses many functions to enable the possibility to transform attribute values.</span></span> <span data-ttu-id="363f8-129">Funkcje te mogą być zagnieżdżane tak wyników z jednej funkcji jest przekazywana do innej funkcji.</span><span class="sxs-lookup"><span data-stu-id="363f8-129">These functions can be nested so the result from one function is passed in to another function.</span></span>

`Function1(Function2(Function3()))`

<span data-ttu-id="363f8-130">Pełną listę funkcji można znaleźć w [funkcji odwołanie](active-directory-aadconnectsync-functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="363f8-130">The complete list of functions can be found in the [function reference](active-directory-aadconnectsync-functions-reference.md).</span></span>

### <a name="parameters"></a><span data-ttu-id="363f8-131">Parametry</span><span class="sxs-lookup"><span data-stu-id="363f8-131">Parameters</span></span>
<span data-ttu-id="363f8-132">Parametr jest zdefiniowany przez łącznik lub przez administratora przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="363f8-132">A parameter is defined either by a Connector or by an administrator using PowerShell.</span></span> <span data-ttu-id="363f8-133">Parametry zwykle zawierają wartości, które różnią się od systemu, na przykład nazwa domeny użytkownika znajdują się w temacie.</span><span class="sxs-lookup"><span data-stu-id="363f8-133">Parameters usually contain values that are different from system to system, for example the name of the domain the user is located in.</span></span> <span data-ttu-id="363f8-134">Te parametry mogą być używane w przepływów atrybutów.</span><span class="sxs-lookup"><span data-stu-id="363f8-134">These parameters can be used in attribute flows.</span></span>

<span data-ttu-id="363f8-135">Łącznik usługi Active Directory przewidzianych reguł synchronizacji ruchu przychodzącego następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="363f8-135">The Active Directory Connector provided the following parameters for inbound Synchronization Rules:</span></span>

| <span data-ttu-id="363f8-136">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="363f8-136">Parameter Name</span></span> | <span data-ttu-id="363f8-137">Komentarz</span><span class="sxs-lookup"><span data-stu-id="363f8-137">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="363f8-138">Domain.Netbios</span><span class="sxs-lookup"><span data-stu-id="363f8-138">Domain.Netbios</span></span> |<span data-ttu-id="363f8-139">Format NetBIOS domeny obecnie importowany, na przykład FABRIKAMSALES</span><span class="sxs-lookup"><span data-stu-id="363f8-139">Netbios format of the domain currently being imported, for example FABRIKAMSALES</span></span> |
| <span data-ttu-id="363f8-140">Domain.FQDN</span><span class="sxs-lookup"><span data-stu-id="363f8-140">Domain.FQDN</span></span> |<span data-ttu-id="363f8-141">Format nazwy FQDN domeny obecnie importowany, na przykład sales.fabrikam.com</span><span class="sxs-lookup"><span data-stu-id="363f8-141">FQDN format of the domain currently being imported, for example sales.fabrikam.com</span></span> |
| <span data-ttu-id="363f8-142">Domain.LDAP</span><span class="sxs-lookup"><span data-stu-id="363f8-142">Domain.LDAP</span></span> |<span data-ttu-id="363f8-143">Format LDAP domeny obecnie importowany, na przykład kontroler domeny sprzedaż, DC = = firmy fabrikam, DC = com</span><span class="sxs-lookup"><span data-stu-id="363f8-143">LDAP format of the domain currently being imported, for example DC=sales,DC=fabrikam,DC=com</span></span> |
| <span data-ttu-id="363f8-144">Forest.Netbios</span><span class="sxs-lookup"><span data-stu-id="363f8-144">Forest.Netbios</span></span> |<span data-ttu-id="363f8-145">NetBIOS format nazwy lasu, w obecnie importowany, na przykład FABRIKAMCORP</span><span class="sxs-lookup"><span data-stu-id="363f8-145">Netbios format of the forest name currently being imported, for example FABRIKAMCORP</span></span> |
| <span data-ttu-id="363f8-146">Forest.FQDN</span><span class="sxs-lookup"><span data-stu-id="363f8-146">Forest.FQDN</span></span> |<span data-ttu-id="363f8-147">Format nazwy FQDN Nazwa lasu, w obecnie importowany, na przykład fabrikam.com</span><span class="sxs-lookup"><span data-stu-id="363f8-147">FQDN format of the forest name currently being imported, for example fabrikam.com</span></span> |
| <span data-ttu-id="363f8-148">Forest.LDAP</span><span class="sxs-lookup"><span data-stu-id="363f8-148">Forest.LDAP</span></span> |<span data-ttu-id="363f8-149">LDAP format nazwy lasu obecnie importowany, na przykład DC = Firma fabrikam, DC = com</span><span class="sxs-lookup"><span data-stu-id="363f8-149">LDAP format of the forest name currently being imported, for example DC=fabrikam,DC=com</span></span> |

<span data-ttu-id="363f8-150">System zawiera następujący parametr jest używany do pobierania identyfikator łącznika, w obecnie uruchomiona:</span><span class="sxs-lookup"><span data-stu-id="363f8-150">The system provides the following parameter, which is used to get the identifier of the Connector currently running:</span></span>  
`Connector.ID`

<span data-ttu-id="363f8-151">Oto przykład wypełniająca domeny atrybut metaverse z nazwą netbios domeny, w której znajduje się użytkownik:</span><span class="sxs-lookup"><span data-stu-id="363f8-151">Here is an example that populates the metaverse attribute domain with the netbios name of the domain where the user is located:</span></span>  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a><span data-ttu-id="363f8-152">Operatory</span><span class="sxs-lookup"><span data-stu-id="363f8-152">Operators</span></span>
<span data-ttu-id="363f8-153">Można użyć następujących operatorów:</span><span class="sxs-lookup"><span data-stu-id="363f8-153">The following operators can be used:</span></span>

* <span data-ttu-id="363f8-154">**Porównanie**: <, < =, <>, =, >, > =</span><span class="sxs-lookup"><span data-stu-id="363f8-154">**Comparison**: <, <=, <>, =, >, >=</span></span>
* <span data-ttu-id="363f8-155">**Matematyce**: +, -, \*, -</span><span class="sxs-lookup"><span data-stu-id="363f8-155">**Mathematics**: +, -, \*, -</span></span>
* <span data-ttu-id="363f8-156">**Ciąg**: & (konkatenacji)</span><span class="sxs-lookup"><span data-stu-id="363f8-156">**String**: & (concatenate)</span></span>
* <span data-ttu-id="363f8-157">**Logiczne**: & & (a), || (lub)</span><span class="sxs-lookup"><span data-stu-id="363f8-157">**Logical**: && (and), || (or)</span></span>
* <span data-ttu-id="363f8-158">**Kolejność obliczania**:)</span><span class="sxs-lookup"><span data-stu-id="363f8-158">**Evaluation order**: ( )</span></span>

<span data-ttu-id="363f8-159">Operatory są wykonywane od lewej do prawej i mają ten sam priorytet oceny.</span><span class="sxs-lookup"><span data-stu-id="363f8-159">Operators are evaluated left to right and have the same evaluation priority.</span></span> <span data-ttu-id="363f8-160">Oznacza to \* (mnożnik) nie jest obliczane przed - (odejmowanie).</span><span class="sxs-lookup"><span data-stu-id="363f8-160">That is, the \* (multiplier) is not evaluated before - (subtraction).</span></span> <span data-ttu-id="363f8-161">2\*(5 + 3) nie jest taka sama jak 2\*5 + 3.</span><span class="sxs-lookup"><span data-stu-id="363f8-161">2\*(5+3) is not the same as 2\*5+3.</span></span> <span data-ttu-id="363f8-162">Nawiasy () są używane do zmianie kolejności oceny od lewej do prawej oceny zlecenia nie jest odpowiedni.</span><span class="sxs-lookup"><span data-stu-id="363f8-162">The brackets ( ) are used to change the evaluation order when left to right evaluation order isn't appropriate.</span></span>

## <a name="multi-valued-attributes"></a><span data-ttu-id="363f8-163">Atrybuty wielowartościowe</span><span class="sxs-lookup"><span data-stu-id="363f8-163">Multi-valued attributes</span></span>
<span data-ttu-id="363f8-164">Funkcje mogą działać na atrybutach zarówno jedno- i wielowartościowych.</span><span class="sxs-lookup"><span data-stu-id="363f8-164">The functions can operate on both single-valued and multi-valued attributes.</span></span> <span data-ttu-id="363f8-165">W przypadku atrybutów wielowartościowych funkcja działa w każdej wartości i stosuje taką samą funkcję do każdej wartości.</span><span class="sxs-lookup"><span data-stu-id="363f8-165">For multi-valued attributes, the function operates over every value and applies the same function to every value.</span></span>

<span data-ttu-id="363f8-166">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="363f8-166">For example:</span></span>  
<span data-ttu-id="363f8-167">`Trim([proxyAddresses])`Czy przycinanie każdej wartości w atrybucie proxyAddress.</span><span class="sxs-lookup"><span data-stu-id="363f8-167">`Trim([proxyAddresses])` Do a Trim of every value in the proxyAddress attribute.</span></span>  
<span data-ttu-id="363f8-168">`Word([proxyAddresses],1,"@") & "@contoso.com"`Dla każdej wartości z @-sign, Zastąp domeny za pomocą @contoso.com.</span><span class="sxs-lookup"><span data-stu-id="363f8-168">`Word([proxyAddresses],1,"@") & "@contoso.com"` For every value with an @-sign, replace the domain with @contoso.com.</span></span>  
<span data-ttu-id="363f8-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])`Znajdź adres SIP i usunąć go z wartości.</span><span class="sxs-lookup"><span data-stu-id="363f8-169">`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])` Look for the SIP-address and remove it from the values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="363f8-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="363f8-170">Next steps</span></span>
* <span data-ttu-id="363f8-171">Dowiedz się więcej o model konfiguracji w [Aprowizacją deklaratywną opis](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="363f8-171">Read more about the configuration model in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>
* <span data-ttu-id="363f8-172">Zobacz, jak deklaratywne inicjowania obsługi administracyjnej jest używane out-of-box w [opis konfiguracji domyślnej](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="363f8-172">See how declarative provisioning is used out-of-box in [Understanding the default configuration](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
* <span data-ttu-id="363f8-173">W temacie jak zrobić praktyczne przy użyciu aprowizacją deklaratywną w [jak wprowadzić zmianę do domyślnej konfiguracji](active-directory-aadconnectsync-change-the-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="363f8-173">See how to make a practical change using declarative provisioning in [How to make a change to the default configuration](active-directory-aadconnectsync-change-the-configuration.md).</span></span>

<span data-ttu-id="363f8-174">**Tematy poglądowe**</span><span class="sxs-lookup"><span data-stu-id="363f8-174">**Overview topics**</span></span>

* [<span data-ttu-id="363f8-175">Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji</span><span class="sxs-lookup"><span data-stu-id="363f8-175">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="363f8-176">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="363f8-176">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

<span data-ttu-id="363f8-177">**Tematy odwołań**</span><span class="sxs-lookup"><span data-stu-id="363f8-177">**Reference topics**</span></span>

* [<span data-ttu-id="363f8-178">Synchronizacja programu Azure AD Connect: odwołanie do funkcji</span><span class="sxs-lookup"><span data-stu-id="363f8-178">Azure AD Connect sync: Functions Reference</span></span>](active-directory-aadconnectsync-functions-reference.md)

