---
title: "Synchronizacja programu Azure AD Connect: odwołanie do funkcji | Dokumentacja firmy Microsoft"
description: "Odwołanie deklaratywne wyrażenia inicjowania obsługi administracyjnej w synchronizacja programu Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 926f52ef64eb79205dbfb344edc7d9bece2a6947
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="1b47d-103">Synchronizacja programu Azure AD Connect: odwołanie do funkcji</span><span class="sxs-lookup"><span data-stu-id="1b47d-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="1b47d-104">W programie Azure AD Connect funkcje są używane do modyfikowania wartości atrybutu podczas synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="1b47d-104">In Azure AD Connect, functions are used to manipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="1b47d-105">Składnia funkcji jest wyrażona w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="1b47d-105">The Syntax of the functions is expressed using the following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="1b47d-106">Funkcji jest przeciążony i przyjmuje wiele składni, wyświetlane są wszystkie prawidłowe składni.</span><span class="sxs-lookup"><span data-stu-id="1b47d-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="1b47d-107">Funkcje są silnie typizowane i sprawdź, czy typ przekazany dopasowań udokumentowanym typem.</span><span class="sxs-lookup"><span data-stu-id="1b47d-107">The functions are strongly typed and they verify that the type passed in matches the documented type.</span></span>  
<span data-ttu-id="1b47d-108">Jeśli typ nie jest zgodny, jest zgłaszany błąd.</span><span class="sxs-lookup"><span data-stu-id="1b47d-108">If the type does not match, an error is thrown.</span></span>

<span data-ttu-id="1b47d-109">Typy są wyrażane przy użyciu następującej składni:</span><span class="sxs-lookup"><span data-stu-id="1b47d-109">The types are expressed with the following syntax:</span></span>

* <span data-ttu-id="1b47d-110">**bin** — binarne</span><span class="sxs-lookup"><span data-stu-id="1b47d-110">**bin** – Binary</span></span>
* <span data-ttu-id="1b47d-111">**wartość logiczna** — wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="1b47d-111">**bool** – Boolean</span></span>
* <span data-ttu-id="1b47d-112">**DT** — UTC daty/godziny</span><span class="sxs-lookup"><span data-stu-id="1b47d-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="1b47d-113">**wyliczenia** — wyliczenie znanych — stałe</span><span class="sxs-lookup"><span data-stu-id="1b47d-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="1b47d-114">**EXP** — wyrażenie, które powinien zwrócić wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="1b47d-114">**exp** – Expression, which is expected to evaluate to a Boolean</span></span>
* <span data-ttu-id="1b47d-115">**mvbin** — binarnego z wieloma wartościami</span><span class="sxs-lookup"><span data-stu-id="1b47d-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="1b47d-116">**mvstr** — ciąg z wieloma wartościami</span><span class="sxs-lookup"><span data-stu-id="1b47d-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="1b47d-117">**mvref** — odwołanie z wieloma wartościami</span><span class="sxs-lookup"><span data-stu-id="1b47d-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="1b47d-118">**num** — numeryczne</span><span class="sxs-lookup"><span data-stu-id="1b47d-118">**num** – Numeric</span></span>
* <span data-ttu-id="1b47d-119">**REF** — odwołanie</span><span class="sxs-lookup"><span data-stu-id="1b47d-119">**ref** – Reference</span></span>
* <span data-ttu-id="1b47d-120">**str** — ciąg</span><span class="sxs-lookup"><span data-stu-id="1b47d-120">**str** – String</span></span>
* <span data-ttu-id="1b47d-121">**var** — wariant (prawie) żadnego innego typu</span><span class="sxs-lookup"><span data-stu-id="1b47d-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="1b47d-122">**void** — nie zwraca wartości</span><span class="sxs-lookup"><span data-stu-id="1b47d-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="1b47d-123">Funkcje z typami **mvbin**, **mvstr**, i **mvref** może pracować tylko na atrybuty wielowartościowe.</span><span class="sxs-lookup"><span data-stu-id="1b47d-123">The functions with the types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="1b47d-124">Funkcje z **bin**, **str**, i **ref** pracować nad atrybuty zarówno jedno- i wielowartościowych.</span><span class="sxs-lookup"><span data-stu-id="1b47d-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="1b47d-125">Informacje ogólne o funkcjach</span><span class="sxs-lookup"><span data-stu-id="1b47d-125">Functions Reference</span></span>
| <span data-ttu-id="1b47d-126">Lista funkcji</span><span class="sxs-lookup"><span data-stu-id="1b47d-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="1b47d-127">**Certyfikat**</span><span class="sxs-lookup"><span data-stu-id="1b47d-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="1b47d-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="1b47d-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="1b47d-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="1b47d-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="1b47d-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="1b47d-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="1b47d-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="1b47d-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="1b47d-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="1b47d-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="1b47d-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="1b47d-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="1b47d-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="1b47d-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="1b47d-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="1b47d-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="1b47d-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="1b47d-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="1b47d-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="1b47d-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="1b47d-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="1b47d-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="1b47d-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="1b47d-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="1b47d-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="1b47d-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="1b47d-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="1b47d-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="1b47d-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="1b47d-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="1b47d-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="1b47d-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="1b47d-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="1b47d-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="1b47d-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="1b47d-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="1b47d-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="1b47d-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="1b47d-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="1b47d-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="1b47d-148">CertVersion</span><span class="sxs-lookup"><span data-stu-id="1b47d-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="1b47d-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="1b47d-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="1b47d-150">**Konwersja**</span><span class="sxs-lookup"><span data-stu-id="1b47d-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="1b47d-151">CBool</span><span class="sxs-lookup"><span data-stu-id="1b47d-151">CBool</span></span>](#cbool) |[<span data-ttu-id="1b47d-152">CDate</span><span class="sxs-lookup"><span data-stu-id="1b47d-152">CDate</span></span>](#cdate) |[<span data-ttu-id="1b47d-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="1b47d-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="1b47d-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="1b47d-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="1b47d-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="1b47d-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="1b47d-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="1b47d-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="1b47d-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="1b47d-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="1b47d-158">CNum</span><span class="sxs-lookup"><span data-stu-id="1b47d-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="1b47d-159">CRef</span><span class="sxs-lookup"><span data-stu-id="1b47d-159">CRef</span></span>](#cref) |[<span data-ttu-id="1b47d-160">CStr</span><span class="sxs-lookup"><span data-stu-id="1b47d-160">CStr</span></span>](#cstr) |[<span data-ttu-id="1b47d-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="1b47d-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="1b47d-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="1b47d-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="1b47d-163">**Data i godzina**</span><span class="sxs-lookup"><span data-stu-id="1b47d-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="1b47d-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="1b47d-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="1b47d-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="1b47d-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="1b47d-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="1b47d-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="1b47d-167">Teraz</span><span class="sxs-lookup"><span data-stu-id="1b47d-167">Now</span></span>](#now) | |
| [<span data-ttu-id="1b47d-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="1b47d-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="1b47d-169">**Katalog**</span><span class="sxs-lookup"><span data-stu-id="1b47d-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="1b47d-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="1b47d-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="1b47d-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="1b47d-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="1b47d-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="1b47d-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="1b47d-173">**Ocena**</span><span class="sxs-lookup"><span data-stu-id="1b47d-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="1b47d-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="1b47d-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="1b47d-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="1b47d-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="1b47d-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="1b47d-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="1b47d-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="1b47d-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="1b47d-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="1b47d-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="1b47d-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="1b47d-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="1b47d-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="1b47d-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="1b47d-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="1b47d-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="1b47d-182">IsString</span><span class="sxs-lookup"><span data-stu-id="1b47d-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="1b47d-183">**Matematyczne**</span><span class="sxs-lookup"><span data-stu-id="1b47d-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="1b47d-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="1b47d-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="1b47d-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="1b47d-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="1b47d-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="1b47d-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="1b47d-187">**Wielowartościowe**</span><span class="sxs-lookup"><span data-stu-id="1b47d-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="1b47d-188">Zawiera</span><span class="sxs-lookup"><span data-stu-id="1b47d-188">Contains</span></span>](#contains) |[<span data-ttu-id="1b47d-189">Liczba</span><span class="sxs-lookup"><span data-stu-id="1b47d-189">Count</span></span>](#count) |[<span data-ttu-id="1b47d-190">Element</span><span class="sxs-lookup"><span data-stu-id="1b47d-190">Item</span></span>](#item) |[<span data-ttu-id="1b47d-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="1b47d-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="1b47d-192">Dołącz</span><span class="sxs-lookup"><span data-stu-id="1b47d-192">Join</span></span>](#join) |[<span data-ttu-id="1b47d-193">Removeduplicates —</span><span class="sxs-lookup"><span data-stu-id="1b47d-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="1b47d-194">Podziel</span><span class="sxs-lookup"><span data-stu-id="1b47d-194">Split</span></span>](#split) | | |
| <span data-ttu-id="1b47d-195">**Przepływ programu**</span><span class="sxs-lookup"><span data-stu-id="1b47d-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="1b47d-196">Błąd</span><span class="sxs-lookup"><span data-stu-id="1b47d-196">Error</span></span>](#error) |[<span data-ttu-id="1b47d-197">IIF</span><span class="sxs-lookup"><span data-stu-id="1b47d-197">IIF</span></span>](#iif) |[<span data-ttu-id="1b47d-198">Wybierz</span><span class="sxs-lookup"><span data-stu-id="1b47d-198">Select</span></span>](#select) |[<span data-ttu-id="1b47d-199">Przełącznik</span><span class="sxs-lookup"><span data-stu-id="1b47d-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="1b47d-200">Gdzie</span><span class="sxs-lookup"><span data-stu-id="1b47d-200">Where</span></span>](#where) |[<span data-ttu-id="1b47d-201">Z</span><span class="sxs-lookup"><span data-stu-id="1b47d-201">With</span></span>](#with) | | | |
| <span data-ttu-id="1b47d-202">**Tekst**</span><span class="sxs-lookup"><span data-stu-id="1b47d-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="1b47d-203">IDENTYFIKATOR GUID</span><span class="sxs-lookup"><span data-stu-id="1b47d-203">GUID</span></span>](#guid) |[<span data-ttu-id="1b47d-204">InStr</span><span class="sxs-lookup"><span data-stu-id="1b47d-204">InStr</span></span>](#instr) |[<span data-ttu-id="1b47d-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="1b47d-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="1b47d-206">LCase</span><span class="sxs-lookup"><span data-stu-id="1b47d-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="1b47d-207">Po lewej</span><span class="sxs-lookup"><span data-stu-id="1b47d-207">Left</span></span>](#left) |[<span data-ttu-id="1b47d-208">Długość</span><span class="sxs-lookup"><span data-stu-id="1b47d-208">Len</span></span>](#len) |[<span data-ttu-id="1b47d-209">Przytp</span><span class="sxs-lookup"><span data-stu-id="1b47d-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="1b47d-210">MID</span><span class="sxs-lookup"><span data-stu-id="1b47d-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="1b47d-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="1b47d-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="1b47d-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="1b47d-212">PadRight</span></span>](#padright) |[<span data-ttu-id="1b47d-213">PCase</span><span class="sxs-lookup"><span data-stu-id="1b47d-213">PCase</span></span>](#pcase) |[<span data-ttu-id="1b47d-214">Zamień</span><span class="sxs-lookup"><span data-stu-id="1b47d-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="1b47d-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="1b47d-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="1b47d-216">Prawo</span><span class="sxs-lookup"><span data-stu-id="1b47d-216">Right</span></span>](#right) |[<span data-ttu-id="1b47d-217">Przytk</span><span class="sxs-lookup"><span data-stu-id="1b47d-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="1b47d-218">TRIM</span><span class="sxs-lookup"><span data-stu-id="1b47d-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="1b47d-219">UCase</span><span class="sxs-lookup"><span data-stu-id="1b47d-219">UCase</span></span>](#ucase) |[<span data-ttu-id="1b47d-220">Word</span><span class="sxs-lookup"><span data-stu-id="1b47d-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="1b47d-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="1b47d-221">BitAnd</span></span>
<span data-ttu-id="1b47d-222">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-222">**Description:**</span></span>  
<span data-ttu-id="1b47d-223">Funkcja BitAnd ustawia określonym usługi bits na wartość.</span><span class="sxs-lookup"><span data-stu-id="1b47d-223">The BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="1b47d-224">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="1b47d-225">Wartość1, wartość2: wartości liczbowe, które powinny być tematyczne razem</span><span class="sxs-lookup"><span data-stu-id="1b47d-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="1b47d-226">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-226">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-227">Ta funkcja konwertuje oba parametry reprezentacja binarna i ustawia bit:</span><span class="sxs-lookup"><span data-stu-id="1b47d-227">This function converts both parameters to the binary representation and sets a bit to:</span></span>

* <span data-ttu-id="1b47d-228">0 — Jeśli jeden lub oba odpowiednich bitów w *maski* i *flagi* 0</span><span class="sxs-lookup"><span data-stu-id="1b47d-228">0 - if one or both of the corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="1b47d-229">1 — Jeśli odpowiednich bitów są 1.</span><span class="sxs-lookup"><span data-stu-id="1b47d-229">1 - if both of the corresponding bits are 1.</span></span>

<span data-ttu-id="1b47d-230">Innymi słowy zwraca 0 we wszystkich przypadkach, z wyjątkiem przypadków, gdy odpowiednich bitów oba parametry są 1.</span><span class="sxs-lookup"><span data-stu-id="1b47d-230">In other words, it returns 0 in all cases except when the corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="1b47d-231">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="1b47d-232">Zwraca 7, ponieważ ta wartość szesnastkową "F" i "F7".</span><span class="sxs-lookup"><span data-stu-id="1b47d-232">Returns 7 because hexadecimal "F" AND "F7" evaluate to this value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="1b47d-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="1b47d-233">BitOr</span></span>
<span data-ttu-id="1b47d-234">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-234">**Description:**</span></span>  
<span data-ttu-id="1b47d-235">Funkcja BitOr ustawia określonym usługi bits na wartość.</span><span class="sxs-lookup"><span data-stu-id="1b47d-235">The BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="1b47d-236">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="1b47d-237">Wartość1, wartość2: wartości liczbowe, które powinny być zsumować logicznie razem</span><span class="sxs-lookup"><span data-stu-id="1b47d-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="1b47d-238">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-238">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-239">Ta funkcja konwertuje oba parametry reprezentacja binarna i ustawia bit 1, jeśli jeden lub oba odpowiednich bitów w maski i flagi są 1 i 0, gdy oba odpowiednich bitów są 0.</span><span class="sxs-lookup"><span data-stu-id="1b47d-239">This function converts both parameters to the binary representation and sets a bit to 1 if one or both of the corresponding bits in mask and flag are 1, and to 0 if both of the corresponding bits are 0.</span></span> <span data-ttu-id="1b47d-240">Innymi słowy zwraca 1 we wszystkich przypadkach, z wyjątkiem przypadków, w którym odpowiednich bitów oba parametry są równe 0.</span><span class="sxs-lookup"><span data-stu-id="1b47d-240">In other words, it returns 1 in all cases except where the corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="1b47d-241">CBool</span><span class="sxs-lookup"><span data-stu-id="1b47d-241">CBool</span></span>
<span data-ttu-id="1b47d-242">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-242">**Description:**</span></span>  
<span data-ttu-id="1b47d-243">CBool-funkcja zwraca wartość logiczną na podstawie na obliczane wyrażenie</span><span class="sxs-lookup"><span data-stu-id="1b47d-243">The CBool function returns a Boolean based on the evaluated expression</span></span>

<span data-ttu-id="1b47d-244">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="1b47d-245">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-245">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-246">Jeśli wyrażenie ma wartość różną od zera, a następnie CBool zwraca wartość PRAWDA, przeciwnym razie zwraca wartość False.</span><span class="sxs-lookup"><span data-stu-id="1b47d-246">If the expression evaluates to a nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="1b47d-247">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="1b47d-248">Zwraca wartość True, jeśli oba atrybuty mają taką samą wartość.</span><span class="sxs-lookup"><span data-stu-id="1b47d-248">Returns True if both attributes have the same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="1b47d-249">CDate</span><span class="sxs-lookup"><span data-stu-id="1b47d-249">CDate</span></span>
<span data-ttu-id="1b47d-250">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-250">**Description:**</span></span>  
<span data-ttu-id="1b47d-251">CDate-funkcja zwraca wartość typu DateTime UTC z ciągu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-251">The CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="1b47d-252">Data i godzina nie jest typem atrybutu natywnego zsynchronizowane, ale jest używany przez niektóre funkcje.</span><span class="sxs-lookup"><span data-stu-id="1b47d-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="1b47d-253">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="1b47d-254">Wartość: Ciąg daty, godziny i opcjonalnie strefy czasowej</span><span class="sxs-lookup"><span data-stu-id="1b47d-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="1b47d-255">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-255">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-256">Zwrócony ciąg jest zawsze w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="1b47d-256">The returned string is always in UTC.</span></span>

<span data-ttu-id="1b47d-257">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="1b47d-258">Zwraca wartość typu DateTime na jego podstawie godzina rozpoczęcia</span><span class="sxs-lookup"><span data-stu-id="1b47d-258">Returns a DateTime based on the employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="1b47d-259">Zwraca daty/godziny reprezentująca "2013-01-11: 00:00:00"</span><span class="sxs-lookup"><span data-stu-id="1b47d-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="1b47d-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="1b47d-260">CertExtensionOids</span></span>
<span data-ttu-id="1b47d-261">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-261">**Description:**</span></span>  
<span data-ttu-id="1b47d-262">Zwraca wartości identyfikatora Oid rozszerzenia krytyczne obiektu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-262">Returns the Oid values of all the critical extensions of a certificate object.</span></span>

<span data-ttu-id="1b47d-263">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-264">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-265">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-265">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="1b47d-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="1b47d-266">CertFormat</span></span>
<span data-ttu-id="1b47d-267">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-267">**Description:**</span></span>  
<span data-ttu-id="1b47d-268">Zwraca nazwę formatu tego certyfikatu X.509v3.</span><span class="sxs-lookup"><span data-stu-id="1b47d-268">Returns the name of the format of this X.509v3 certificate.</span></span>

<span data-ttu-id="1b47d-269">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-270">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-271">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-271">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="1b47d-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="1b47d-272">CertFriendlyName</span></span>
<span data-ttu-id="1b47d-273">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-273">**Description:**</span></span>  
<span data-ttu-id="1b47d-274">Zwraca skojarzonego alias dla certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-274">Returns the associated alias for a certificate.</span></span>

<span data-ttu-id="1b47d-275">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-276">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-277">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-277">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="1b47d-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="1b47d-278">CertHashString</span></span>
<span data-ttu-id="1b47d-279">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-279">**Description:**</span></span>  
<span data-ttu-id="1b47d-280">Zwraca wartość skrótu SHA1 certyfikatu X.509v3 jako ciąg szesnastkowy.</span><span class="sxs-lookup"><span data-stu-id="1b47d-280">Returns the SHA1 hash value for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="1b47d-281">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-282">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-283">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-283">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="1b47d-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="1b47d-284">CertIssuer</span></span>
<span data-ttu-id="1b47d-285">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-285">**Description:**</span></span>  
<span data-ttu-id="1b47d-286">Zwraca nazwę urzędu certyfikacji, który wystawił certyfikat X.509v3.</span><span class="sxs-lookup"><span data-stu-id="1b47d-286">Returns the name of the certificate authority that issued the X.509v3 certificate.</span></span>

<span data-ttu-id="1b47d-287">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-288">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-289">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-289">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="1b47d-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="1b47d-290">CertIssuerDN</span></span>
<span data-ttu-id="1b47d-291">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-291">**Description:**</span></span>  
<span data-ttu-id="1b47d-292">Zwraca nazwa wyróżniająca wystawcy certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-292">Returns the distinguished name of the certificate issuer.</span></span>

<span data-ttu-id="1b47d-293">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-294">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-295">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-295">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="1b47d-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="1b47d-296">CertIssuerOid</span></span>
<span data-ttu-id="1b47d-297">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-297">**Description:**</span></span>  
<span data-ttu-id="1b47d-298">Zwraca identyfikator Oid wystawcy certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-298">Returns the Oid of the certificate issuer.</span></span>

<span data-ttu-id="1b47d-299">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-300">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-301">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-301">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="1b47d-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="1b47d-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="1b47d-303">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-303">**Description:**</span></span>  
<span data-ttu-id="1b47d-304">Zwraca informacje algorytm klucza dla tego certyfikatu X.509v3 jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-304">Returns the key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="1b47d-305">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-306">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-307">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-307">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="1b47d-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="1b47d-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="1b47d-309">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-309">**Description:**</span></span>  
<span data-ttu-id="1b47d-310">Zwraca parametry algorytm klucza certyfikatu X.509v3 jako ciąg szesnastkowy.</span><span class="sxs-lookup"><span data-stu-id="1b47d-310">Returns the key algorithm parameters for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="1b47d-311">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-312">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-313">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-313">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="1b47d-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="1b47d-314">CertNameInfo</span></span>
<span data-ttu-id="1b47d-315">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-315">**Description:**</span></span>  
<span data-ttu-id="1b47d-316">Zwraca podmiot i Wystawca nazwy z certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-316">Returns the subject and issuer names from a certificate.</span></span>

<span data-ttu-id="1b47d-317">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="1b47d-318">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-319">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-319">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="1b47d-320">X509NameType: Wartość X509NameType tematu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-320">X509NameType: The X509NameType value for the subject.</span></span>
*   <span data-ttu-id="1b47d-321">includesIssuerName: wartość true, aby uwzględnić nazwę wystawcy; w przeciwnym razie wartość false.</span><span class="sxs-lookup"><span data-stu-id="1b47d-321">includesIssuerName: true to include the issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="1b47d-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="1b47d-322">CertNotAfter</span></span>
<span data-ttu-id="1b47d-323">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-323">**Description:**</span></span>  
<span data-ttu-id="1b47d-324">Zwraca datę według czasu lokalnego, po której certyfikat nie jest już prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="1b47d-324">Returns the date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="1b47d-325">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-326">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-327">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-327">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="1b47d-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="1b47d-328">CertNotBefore</span></span>
<span data-ttu-id="1b47d-329">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-329">**Description:**</span></span>  
<span data-ttu-id="1b47d-330">Zwraca datę według czasu lokalnego, od której zaczyna obowiązywać certyfikat.</span><span class="sxs-lookup"><span data-stu-id="1b47d-330">Returns the date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="1b47d-331">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-332">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-333">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-333">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="1b47d-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="1b47d-334">CertPublicKeyOid</span></span>
<span data-ttu-id="1b47d-335">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-335">**Description:**</span></span>  
<span data-ttu-id="1b47d-336">Zwraca identyfikator Oid klucza publicznego certyfikatu X.509v3.</span><span class="sxs-lookup"><span data-stu-id="1b47d-336">Returns the Oid of the public key for the X.509v3 certificate.</span></span>

<span data-ttu-id="1b47d-337">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-338">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-339">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-339">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="1b47d-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="1b47d-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="1b47d-341">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-341">**Description:**</span></span>  
<span data-ttu-id="1b47d-342">Zwraca identyfikator Oid parametrów klucza publicznego certyfikatu X.509v3.</span><span class="sxs-lookup"><span data-stu-id="1b47d-342">Returns the Oid of the public key parameters for the X.509v3 certificate.</span></span>

<span data-ttu-id="1b47d-343">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-344">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-345">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-345">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="1b47d-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="1b47d-346">CertSerialNumber</span></span>
<span data-ttu-id="1b47d-347">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-347">**Description:**</span></span>  
<span data-ttu-id="1b47d-348">Zwraca numer seryjny certyfikatu X.509v3.</span><span class="sxs-lookup"><span data-stu-id="1b47d-348">Returns the serial number of the X.509v3 certificate.</span></span>

<span data-ttu-id="1b47d-349">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-350">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-351">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-351">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="1b47d-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="1b47d-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="1b47d-353">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-353">**Description:**</span></span>  
<span data-ttu-id="1b47d-354">Zwraca identyfikator Oid algorytm używany do tworzenia podpisu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-354">Returns the Oid of the algorithm used to create the signature of a certificate.</span></span>

<span data-ttu-id="1b47d-355">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-356">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-357">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-357">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="1b47d-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="1b47d-358">CertSubject</span></span>
<span data-ttu-id="1b47d-359">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-359">**Description:**</span></span>  
<span data-ttu-id="1b47d-360">Pobiera nazwa wyróżniająca podmiotu z certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-360">Gets the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="1b47d-361">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-362">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-363">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-363">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="1b47d-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="1b47d-364">CertSubjectNameDN</span></span>
<span data-ttu-id="1b47d-365">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-365">**Description:**</span></span>  
<span data-ttu-id="1b47d-366">Zwraca nazwa wyróżniająca podmiotu z certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-366">Returns the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="1b47d-367">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-368">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-369">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-369">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="1b47d-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="1b47d-370">CertSubjectNameOid</span></span>
<span data-ttu-id="1b47d-371">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-371">**Description:**</span></span>  
<span data-ttu-id="1b47d-372">Zwraca identyfikator Oid nazwy podmiotu z certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-372">Returns the Oid of the subject name from a certificate.</span></span>

<span data-ttu-id="1b47d-373">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-374">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-375">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-375">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="1b47d-376">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="1b47d-376">CertThumbprint</span></span>
<span data-ttu-id="1b47d-377">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-377">**Description:**</span></span>  
<span data-ttu-id="1b47d-378">Zwraca odcisk palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-378">Returns the thumbprint of a certificate.</span></span>

<span data-ttu-id="1b47d-379">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-380">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-381">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-381">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="1b47d-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="1b47d-382">CertVersion</span></span>
<span data-ttu-id="1b47d-383">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-383">**Description:**</span></span>  
<span data-ttu-id="1b47d-384">Zwraca wersja formatu X.509 certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-384">Returns the X.509 format version of a certificate.</span></span>

<span data-ttu-id="1b47d-385">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-386">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-387">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-387">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="1b47d-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="1b47d-388">CGuid</span></span>
<span data-ttu-id="1b47d-389">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-389">**Description:**</span></span>  
<span data-ttu-id="1b47d-390">Funkcja CGuid konwertuje jego reprezentacja binarna reprezentacja ciągu identyfikatora GUID.</span><span class="sxs-lookup"><span data-stu-id="1b47d-390">The CGuid function converts the string representation of a GUID to its binary representation.</span></span>

<span data-ttu-id="1b47d-391">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="1b47d-392">Ciąg sformatowany w tym wzorcu: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx lub {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="1b47d-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="1b47d-393">Contains</span><span class="sxs-lookup"><span data-stu-id="1b47d-393">Contains</span></span>
<span data-ttu-id="1b47d-394">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-394">**Description:**</span></span>  
<span data-ttu-id="1b47d-395">Funkcja zawiera wyszukuje ciąg wewnątrz atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="1b47d-395">The Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="1b47d-396">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-396">**Syntax:**</span></span>  
<span data-ttu-id="1b47d-397">`num Contains (mvstring attribute, str search)`-uwzględniana wielkość liter</span><span class="sxs-lookup"><span data-stu-id="1b47d-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="1b47d-398">`num Contains (mvref attribute, str search)`-uwzględniana wielkość liter</span><span class="sxs-lookup"><span data-stu-id="1b47d-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="1b47d-399">Atrybut: atrybutu wielowartościowego do wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1b47d-399">attribute: the multi-valued attribute to search.</span></span>
* <span data-ttu-id="1b47d-400">wyszukiwania: ciąg można znaleźć w atrybucie.</span><span class="sxs-lookup"><span data-stu-id="1b47d-400">search: string to find in the attribute.</span></span>
* <span data-ttu-id="1b47d-401">Casetype: CaseInsensitive lub CaseSensitive w tabeli.</span><span class="sxs-lookup"><span data-stu-id="1b47d-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="1b47d-402">Zwraca indeks atrybutów wielowartościowych, w którym zostało znalezione ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-402">Returns index in the multi-valued attribute where the string was found.</span></span> <span data-ttu-id="1b47d-403">0 jest zwracany, jeśli nie zostanie znaleziony ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-403">0 is returned if the string is not found.</span></span>

<span data-ttu-id="1b47d-404">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-404">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-405">Dla atrybutów wielowartościowych ciąg wyszukiwania wyszukuje podciągów w wartości.</span><span class="sxs-lookup"><span data-stu-id="1b47d-405">For multi-valued string attributes, the search finds substrings in the values.</span></span>  
<span data-ttu-id="1b47d-406">Dla atrybutów odwołania przeszukane ciąg musi dokładnie odpowiadać wartości być uznawane za zgodne.</span><span class="sxs-lookup"><span data-stu-id="1b47d-406">For reference attributes, the searched string must exactly match the value to be considered a match.</span></span>

<span data-ttu-id="1b47d-407">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="1b47d-408">Jeśli atrybut proxyAddresses ma podstawowego adresu e-mail (wskazywanym przez wielkimi literami "SMTP:"), zwracany jest ten atrybut proxyAddress, przeciwnym razie zwraca błąd.</span><span class="sxs-lookup"><span data-stu-id="1b47d-408">If the proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return the proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="1b47d-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="1b47d-409">ConvertFromBase64</span></span>
<span data-ttu-id="1b47d-410">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-410">**Description:**</span></span>  
<span data-ttu-id="1b47d-411">Funkcja ConvertFromBase64 konwertuje wartość określonego kodowanie base64 na regularne ciągu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-411">The ConvertFromBase64 function converts the specified base64 encoded value to a regular string.</span></span>

<span data-ttu-id="1b47d-412">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-412">**Syntax:**</span></span>  
<span data-ttu-id="1b47d-413">`str ConvertFromBase64(str source)`-zakłada do kodowania Unicode</span><span class="sxs-lookup"><span data-stu-id="1b47d-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="1b47d-414">Źródło: ciąg kodowany w formacie Base64</span><span class="sxs-lookup"><span data-stu-id="1b47d-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="1b47d-415">Kodowanie: UTF8 Unicode i ASCII,</span><span class="sxs-lookup"><span data-stu-id="1b47d-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="1b47d-416">**Przykład**</span><span class="sxs-lookup"><span data-stu-id="1b47d-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="1b47d-417">Zwraca zarówno przykłady "*Witaj świecie!*"</span><span class="sxs-lookup"><span data-stu-id="1b47d-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="1b47d-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="1b47d-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="1b47d-419">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-419">**Description:**</span></span>  
<span data-ttu-id="1b47d-420">Funkcja ConvertFromUTF8Hex konwertuje określoną wartość zakodowany szesnastkowo UTF8 na ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-420">The ConvertFromUTF8Hex function converts the specified UTF8 Hex encoded value to a string.</span></span>

<span data-ttu-id="1b47d-421">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="1b47d-422">Źródło: ciągu zakodowanego 2-bajtowych UTF8</span><span class="sxs-lookup"><span data-stu-id="1b47d-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="1b47d-423">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-423">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-424">Różnica między tej funkcji i ConvertFromBase64([],UTF8) że wynik jest przyjazna nazwa Wyróżniająca atrybutu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-424">The difference between this function and ConvertFromBase64([],UTF8) in that the result is friendly for the DN attribute.</span></span>  
<span data-ttu-id="1b47d-425">Ten format jest używany przez usługę Azure Active Directory jako nazwa Wyróżniająca.</span><span class="sxs-lookup"><span data-stu-id="1b47d-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="1b47d-426">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="1b47d-427">Zwraca "*Witaj świecie!*"</span><span class="sxs-lookup"><span data-stu-id="1b47d-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="1b47d-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="1b47d-428">ConvertToBase64</span></span>
<span data-ttu-id="1b47d-429">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-429">**Description:**</span></span>  
<span data-ttu-id="1b47d-430">Funkcja ConvertToBase64 konwertuje ciąg na ciąg Unicode w formacie base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-430">The ConvertToBase64 function converts a string to a Unicode base64 string.</span></span>  
<span data-ttu-id="1b47d-431">Konwertuje wartość tablicy liczb całkowitych do reprezentacji ciągu równoważne, który jest algorytmem base-64 cyfr.</span><span class="sxs-lookup"><span data-stu-id="1b47d-431">Converts the value of an array of integers to its equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="1b47d-432">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="1b47d-433">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="1b47d-434">Zwraca "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span><span class="sxs-lookup"><span data-stu-id="1b47d-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="1b47d-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="1b47d-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="1b47d-436">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-436">**Description:**</span></span>  
<span data-ttu-id="1b47d-437">Funkcja ConvertToUTF8Hex konwertuje ciąg na wartość zakodowany szesnastkowo UTF8.</span><span class="sxs-lookup"><span data-stu-id="1b47d-437">The ConvertToUTF8Hex function converts a string to a UTF8 Hex encoded value.</span></span>

<span data-ttu-id="1b47d-438">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="1b47d-439">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-439">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-440">Format danych wyjściowych tej funkcji jest używany przez usługę Azure Active Directory jako nazwa Wyróżniająca atrybutu format.</span><span class="sxs-lookup"><span data-stu-id="1b47d-440">The output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="1b47d-441">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="1b47d-442">Zwraca 48656C6C6F20776F726C6421</span><span class="sxs-lookup"><span data-stu-id="1b47d-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="1b47d-443">Licznik</span><span class="sxs-lookup"><span data-stu-id="1b47d-443">Count</span></span>
<span data-ttu-id="1b47d-444">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-444">**Description:**</span></span>  
<span data-ttu-id="1b47d-445">Funkcja Count zwraca liczbę elementów w atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="1b47d-445">The Count function returns the number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="1b47d-446">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="1b47d-447">CNum</span><span class="sxs-lookup"><span data-stu-id="1b47d-447">CNum</span></span>
<span data-ttu-id="1b47d-448">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-448">**Description:**</span></span>  
<span data-ttu-id="1b47d-449">Funkcja CNum ciąg znaków i zwraca dane typu liczbowego.</span><span class="sxs-lookup"><span data-stu-id="1b47d-449">The CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="1b47d-450">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="1b47d-451">CRef</span><span class="sxs-lookup"><span data-stu-id="1b47d-451">CRef</span></span>
<span data-ttu-id="1b47d-452">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-452">**Description:**</span></span>  
<span data-ttu-id="1b47d-453">Konwertuje ciąg na atrybut odwołania</span><span class="sxs-lookup"><span data-stu-id="1b47d-453">Converts a string to a reference attribute</span></span>

<span data-ttu-id="1b47d-454">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="1b47d-455">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="1b47d-456">CStr</span><span class="sxs-lookup"><span data-stu-id="1b47d-456">CStr</span></span>
<span data-ttu-id="1b47d-457">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-457">**Description:**</span></span>  
<span data-ttu-id="1b47d-458">Konwertuje funkcję CStr dla typu danych string.</span><span class="sxs-lookup"><span data-stu-id="1b47d-458">The CStr function converts to a string data type.</span></span>

<span data-ttu-id="1b47d-459">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="1b47d-460">wartość: może być liczbą, atrybut odwołania lub typu Boolean.</span><span class="sxs-lookup"><span data-stu-id="1b47d-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="1b47d-461">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="1b47d-462">Może zwrócić "cn = Jan, dc = contoso, dc = com"</span><span class="sxs-lookup"><span data-stu-id="1b47d-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="1b47d-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="1b47d-463">DateAdd</span></span>
<span data-ttu-id="1b47d-464">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-464">**Description:**</span></span>  
<span data-ttu-id="1b47d-465">Zwraca wartość typu Date zawierającą datę, do której dodano określony interwał.</span><span class="sxs-lookup"><span data-stu-id="1b47d-465">Returns a Date containing a date to which a specified time interval has been added.</span></span>

<span data-ttu-id="1b47d-466">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="1b47d-467">Interwał: String wyrażenie przedział czasu, które chcesz dodać.</span><span class="sxs-lookup"><span data-stu-id="1b47d-467">interval: String expression that is the interval of time you want to add.</span></span> <span data-ttu-id="1b47d-468">Ciąg musi mieć jedną z następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="1b47d-468">The string must have one of the following values:</span></span>
  * <span data-ttu-id="1b47d-469">rrrr roku</span><span class="sxs-lookup"><span data-stu-id="1b47d-469">yyyy Year</span></span>
  * <span data-ttu-id="1b47d-470">q kwartału</span><span class="sxs-lookup"><span data-stu-id="1b47d-470">q Quarter</span></span>
  * <span data-ttu-id="1b47d-471">m miesiąc</span><span class="sxs-lookup"><span data-stu-id="1b47d-471">m Month</span></span>
  * <span data-ttu-id="1b47d-472">y dzień roku</span><span class="sxs-lookup"><span data-stu-id="1b47d-472">y Day of year</span></span>
  * <span data-ttu-id="1b47d-473">d dzień</span><span class="sxs-lookup"><span data-stu-id="1b47d-473">d Day</span></span>
  * <span data-ttu-id="1b47d-474">w dzień tygodnia</span><span class="sxs-lookup"><span data-stu-id="1b47d-474">w Weekday</span></span>
  * <span data-ttu-id="1b47d-475">TT tygodnia</span><span class="sxs-lookup"><span data-stu-id="1b47d-475">ww Week</span></span>
  * <span data-ttu-id="1b47d-476">h Godzina</span><span class="sxs-lookup"><span data-stu-id="1b47d-476">h Hour</span></span>
  * <span data-ttu-id="1b47d-477">n minutę</span><span class="sxs-lookup"><span data-stu-id="1b47d-477">n Minute</span></span>
  * <span data-ttu-id="1b47d-478">s drugi</span><span class="sxs-lookup"><span data-stu-id="1b47d-478">s Second</span></span>
* <span data-ttu-id="1b47d-479">wartość: liczba jednostek, które chcesz dodać.</span><span class="sxs-lookup"><span data-stu-id="1b47d-479">value: The number of units you want to add.</span></span> <span data-ttu-id="1b47d-480">Może być liczbą dodatnią (Aby uzyskać daty w przyszłości) lub ujemną (Aby uzyskać daty w przeszłości).</span><span class="sxs-lookup"><span data-stu-id="1b47d-480">It can be positive (to get dates in the future) or negative (to get dates in the past).</span></span>
* <span data-ttu-id="1b47d-481">Data: daty/godziny reprezentująca datę, do którego jest dodawany interwał.</span><span class="sxs-lookup"><span data-stu-id="1b47d-481">date: DateTime representing date to which the interval is added.</span></span>

<span data-ttu-id="1b47d-482">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="1b47d-483">Dodaje 3 miesiące i zwraca wartość typu DateTime reprezentujący "2001-04-01".</span><span class="sxs-lookup"><span data-stu-id="1b47d-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="1b47d-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="1b47d-484">DateFromNum</span></span>
<span data-ttu-id="1b47d-485">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-485">**Description:**</span></span>  
<span data-ttu-id="1b47d-486">Konwertuje funkcję DateFromNum wartość daty AD w formacie do typu Data/Godzina.</span><span class="sxs-lookup"><span data-stu-id="1b47d-486">The DateFromNum function converts a value in AD’s date format to a DateTime type.</span></span>

<span data-ttu-id="1b47d-487">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="1b47d-488">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="1b47d-489">Zwraca wartość typu DateTime reprezentujący 2012-01-01-23:00:00</span><span class="sxs-lookup"><span data-stu-id="1b47d-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="1b47d-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="1b47d-490">DNComponent</span></span>
<span data-ttu-id="1b47d-491">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-491">**Description:**</span></span>  
<span data-ttu-id="1b47d-492">Funkcja DNComponent zwraca wartość określonego składnika DN z lewej strony.</span><span class="sxs-lookup"><span data-stu-id="1b47d-492">The DNComponent function returns the value of a specified DN component going from left.</span></span>

<span data-ttu-id="1b47d-493">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="1b47d-494">Nazwa wyróżniająca: atrybut odwołania, aby zinterpretować</span><span class="sxs-lookup"><span data-stu-id="1b47d-494">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="1b47d-495">ComponentNumber: Składnik DN do zwrócenia</span><span class="sxs-lookup"><span data-stu-id="1b47d-495">ComponentNumber: The component in the DN to return</span></span>

<span data-ttu-id="1b47d-496">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="1b47d-497">Jeśli nazwa wyróżniająca "cn = Jan, ou =..." zwraca Jan</span><span class="sxs-lookup"><span data-stu-id="1b47d-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="1b47d-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="1b47d-498">DNComponentRev</span></span>
<span data-ttu-id="1b47d-499">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-499">**Description:**</span></span>  
<span data-ttu-id="1b47d-500">Funkcja DNComponentRev zwraca wartość określonego składnika DN z prawej strony (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="1b47d-500">The DNComponentRev function returns the value of a specified DN component going from right (the end).</span></span>

<span data-ttu-id="1b47d-501">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="1b47d-502">Nazwa wyróżniająca: atrybut odwołania, aby zinterpretować</span><span class="sxs-lookup"><span data-stu-id="1b47d-502">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="1b47d-503">ComponentNumber - składnik w DN do zwrócenia</span><span class="sxs-lookup"><span data-stu-id="1b47d-503">ComponentNumber - The component in the DN to return</span></span>
* <span data-ttu-id="1b47d-504">Opcje: Kontroler domeny — Ignoruj wszystkie składniki z "dc ="</span><span class="sxs-lookup"><span data-stu-id="1b47d-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="1b47d-505">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-505">**Example:**</span></span>  
<span data-ttu-id="1b47d-506">Jeśli nazwa wyróżniająca "cn Jan, ou = (Atlanta), ou = GA, ou = = US, dc = contoso, dc = com" następnie</span><span class="sxs-lookup"><span data-stu-id="1b47d-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="1b47d-507">Obie zwracają NAS.</span><span class="sxs-lookup"><span data-stu-id="1b47d-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="1b47d-508">Błąd</span><span class="sxs-lookup"><span data-stu-id="1b47d-508">Error</span></span>
<span data-ttu-id="1b47d-509">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-509">**Description:**</span></span>  
<span data-ttu-id="1b47d-510">Funkcja błąd służy do zwracania błędów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="1b47d-510">The Error function is used to return a custom error.</span></span>

<span data-ttu-id="1b47d-511">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="1b47d-512">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="1b47d-513">Jeśli atrybut accountName nie jest obecny, zgłoś błąd w obiekcie.</span><span class="sxs-lookup"><span data-stu-id="1b47d-513">If the attribute accountName is not present, throw an error on the object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="1b47d-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="1b47d-514">EscapeDNComponent</span></span>
<span data-ttu-id="1b47d-515">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-515">**Description:**</span></span>  
<span data-ttu-id="1b47d-516">Funkcja EscapeDNComponent przyjmuje jeden składnik DN i jego specjalne, dlatego może być reprezentowany w protokole LDAP.</span><span class="sxs-lookup"><span data-stu-id="1b47d-516">The EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="1b47d-517">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="1b47d-518">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="1b47d-519">Zapewnia, że można można utworzyć obiektu w katalogu LDAP, nawet wtedy, gdy atrybut displayName zawiera znaki, które należy użyć znaków ucieczki w protokole LDAP.</span><span class="sxs-lookup"><span data-stu-id="1b47d-519">Makes sure the object can be created in an LDAP directory even if the displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="1b47d-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="1b47d-520">FormatDateTime</span></span>
<span data-ttu-id="1b47d-521">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-521">**Description:**</span></span>  
<span data-ttu-id="1b47d-522">Funkcja FormatDateTime jest używany do formatowania wartości daty i godziny do ciągu w określonym formacie</span><span class="sxs-lookup"><span data-stu-id="1b47d-522">The FormatDateTime function is used to format a DateTime to a string with a specified format</span></span>

<span data-ttu-id="1b47d-523">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="1b47d-524">wartość: wartości w formacie daty/godziny</span><span class="sxs-lookup"><span data-stu-id="1b47d-524">value: a value in the DateTime format</span></span>
* <span data-ttu-id="1b47d-525">Format: ciąg reprezentujący można przekonwertować na format.</span><span class="sxs-lookup"><span data-stu-id="1b47d-525">format: a string representing the format to convert to.</span></span>

<span data-ttu-id="1b47d-526">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-526">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-527">Możliwe wartości dla formatu można znaleźć tutaj: [zdefiniowane przez użytkownika (funkcji Format) formaty daty i godziny](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="1b47d-527">The possible values for the format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="1b47d-528">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="1b47d-529">Wynikiem "2007-12-25".</span><span class="sxs-lookup"><span data-stu-id="1b47d-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="1b47d-530">Może spowodować "20140905081453.0Z"</span><span class="sxs-lookup"><span data-stu-id="1b47d-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="1b47d-531">IDENTYFIKATOR GUID</span><span class="sxs-lookup"><span data-stu-id="1b47d-531">GUID</span></span>
<span data-ttu-id="1b47d-532">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-532">**Description:**</span></span>  
<span data-ttu-id="1b47d-533">Funkcja GUID generuje losowe nowego identyfikatora GUID</span><span class="sxs-lookup"><span data-stu-id="1b47d-533">The function GUID generates a new random GUID</span></span>

<span data-ttu-id="1b47d-534">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="1b47d-535">IIF</span><span class="sxs-lookup"><span data-stu-id="1b47d-535">IIF</span></span>
<span data-ttu-id="1b47d-536">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-536">**Description:**</span></span>  
<span data-ttu-id="1b47d-537">Funkcja IIF zwraca jeden zestaw możliwych wartości na podstawie określonego warunku.</span><span class="sxs-lookup"><span data-stu-id="1b47d-537">The IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="1b47d-538">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="1b47d-539">warunek: dowolna wartość lub wyrażenie, które może przyjąć wartość true lub false.</span><span class="sxs-lookup"><span data-stu-id="1b47d-539">condition: any value or expression that can be evaluated to true or false.</span></span>
* <span data-ttu-id="1b47d-540">Wartość_dla_prawdy: Jeśli warunek zwraca wartość true, zwracana wartość.</span><span class="sxs-lookup"><span data-stu-id="1b47d-540">valueIfTrue: If the condition evaluates to true, the returned value.</span></span>
* <span data-ttu-id="1b47d-541">Wartość_dla_fałszu: Jeśli warunek nie ma wartość false, zwracana wartość.</span><span class="sxs-lookup"><span data-stu-id="1b47d-541">valueIfFalse: If the condition evaluates to false, the returned value.</span></span>

<span data-ttu-id="1b47d-542">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="1b47d-543">Jeśli użytkownik jest intern, zwraca alias użytkownika z "t-" dodaną na początku jej inny alias użytkownika, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="1b47d-543">If the user is an intern, returns the alias of a user with "t-" added to the beginning of it, else returns the user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="1b47d-544">InStr</span><span class="sxs-lookup"><span data-stu-id="1b47d-544">InStr</span></span>
<span data-ttu-id="1b47d-545">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-545">**Description:**</span></span>  
<span data-ttu-id="1b47d-546">Funkcja InStr znajduje pierwsze wystąpienie podciągu w ciągu</span><span class="sxs-lookup"><span data-stu-id="1b47d-546">The InStr function finds the first occurrence of a substring in a string</span></span>

<span data-ttu-id="1b47d-547">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="1b47d-548">ciąg_przeszukiwany: ciąg do wyszukania</span><span class="sxs-lookup"><span data-stu-id="1b47d-548">stringcheck: string to be searched</span></span>
* <span data-ttu-id="1b47d-549">ciąg_poszukiwany: ciąg do znalezienia</span><span class="sxs-lookup"><span data-stu-id="1b47d-549">stringmatch: string to be found</span></span>
* <span data-ttu-id="1b47d-550">Rozpocznij: uruchamianie stanie Znajdź podciąg</span><span class="sxs-lookup"><span data-stu-id="1b47d-550">start: starting position to find the substring</span></span>
* <span data-ttu-id="1b47d-551">porównywanie: vbTextCompare lub vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="1b47d-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="1b47d-552">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-552">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-553">Zwraca pozycję, jeżeli został znaleziony podciąg lub 0, jeśli nie można odnaleźć.</span><span class="sxs-lookup"><span data-stu-id="1b47d-553">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="1b47d-554">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-554">**Example:**</span></span>  
`InStr("The quick brown fox","quick")`  
<span data-ttu-id="1b47d-555">Evalues 5</span><span class="sxs-lookup"><span data-stu-id="1b47d-555">Evalues to 5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="1b47d-556">Oblicza 7</span><span class="sxs-lookup"><span data-stu-id="1b47d-556">Evaluates to 7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="1b47d-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="1b47d-557">InStrRev</span></span>
<span data-ttu-id="1b47d-558">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-558">**Description:**</span></span>  
<span data-ttu-id="1b47d-559">Funkcja InStrRev znajduje ostatnie wystąpienie podciągu w ciągu</span><span class="sxs-lookup"><span data-stu-id="1b47d-559">The InStrRev function finds the last occurrence of a substring in a string</span></span>

<span data-ttu-id="1b47d-560">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="1b47d-561">ciąg_przeszukiwany: ciąg do wyszukania</span><span class="sxs-lookup"><span data-stu-id="1b47d-561">stringcheck: string to be searched</span></span>
* <span data-ttu-id="1b47d-562">ciąg_poszukiwany: ciąg do znalezienia</span><span class="sxs-lookup"><span data-stu-id="1b47d-562">stringmatch: string to be found</span></span>
* <span data-ttu-id="1b47d-563">Rozpocznij: uruchamianie stanie Znajdź podciąg</span><span class="sxs-lookup"><span data-stu-id="1b47d-563">start: starting position to find the substring</span></span>
* <span data-ttu-id="1b47d-564">porównywanie: vbTextCompare lub vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="1b47d-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="1b47d-565">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-565">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-566">Zwraca pozycję, jeżeli został znaleziony podciąg lub 0, jeśli nie można odnaleźć.</span><span class="sxs-lookup"><span data-stu-id="1b47d-566">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="1b47d-567">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="1b47d-568">Zwraca 7</span><span class="sxs-lookup"><span data-stu-id="1b47d-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="1b47d-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="1b47d-569">IsBitSet</span></span>
<span data-ttu-id="1b47d-570">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-570">**Description:**</span></span>  
<span data-ttu-id="1b47d-571">Funkcja IsBitSet testów, jeśli jest to nieco jest ustawiony lub nie</span><span class="sxs-lookup"><span data-stu-id="1b47d-571">The function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="1b47d-572">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="1b47d-573">wartość: wartość liczbową evaluated.flag: wartość liczbową bit ma zostać obliczone</span><span class="sxs-lookup"><span data-stu-id="1b47d-573">value: a numeric value that is evaluated.flag: a numeric value that has the bit to be evaluated</span></span>

<span data-ttu-id="1b47d-574">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="1b47d-575">Zwraca wartość True, ponieważ ustawiono bit "4" w wartości szesnastkowej "F"</span><span class="sxs-lookup"><span data-stu-id="1b47d-575">Returns True because bit "4" is set in the hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="1b47d-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="1b47d-576">IsDate</span></span>
<span data-ttu-id="1b47d-577">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-577">**Description:**</span></span>  
<span data-ttu-id="1b47d-578">Jeśli wyrażenie może być oblicza jako typu DateTime, a następnie funkcja IsDate ma wartość True.</span><span class="sxs-lookup"><span data-stu-id="1b47d-578">If the expression can be evaluates as a DateTime type, then the IsDate function evaluates to True.</span></span>

<span data-ttu-id="1b47d-579">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="1b47d-580">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-580">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-581">Używany do określenia, czy CDate() mogą być skutecznie.</span><span class="sxs-lookup"><span data-stu-id="1b47d-581">Used to determine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="1b47d-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="1b47d-582">IsCert</span></span>
<span data-ttu-id="1b47d-583">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-583">**Description:**</span></span>  
<span data-ttu-id="1b47d-584">Zwraca wartość PRAWDA, jeśli można serializować danych pierwotnych do obiektu certyfikatu .NET X509Certificate2.</span><span class="sxs-lookup"><span data-stu-id="1b47d-584">Returns true if the raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="1b47d-585">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="1b47d-586">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="1b47d-587">Tablica bajtów może być zakodowane pliku binarnego (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="1b47d-587">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="1b47d-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="1b47d-588">IsEmpty</span></span>
<span data-ttu-id="1b47d-589">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-589">**Description:**</span></span>  
<span data-ttu-id="1b47d-590">Jeśli atrybut znajduje się w CS lub MV, ale zwraca pusty ciąg, następnie funkcja IsEmpty ma wartość True.</span><span class="sxs-lookup"><span data-stu-id="1b47d-590">If the attribute is present in the CS or MV but evaluates to an empty string, then the IsEmpty function evaluates to True.</span></span>

<span data-ttu-id="1b47d-591">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="1b47d-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="1b47d-592">IsGuid</span></span>
<span data-ttu-id="1b47d-593">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-593">**Description:**</span></span>  
<span data-ttu-id="1b47d-594">Jeśli ciąg można przekonwertować na identyfikator GUID, funkcja IsGuid obliczone na wartość true.</span><span class="sxs-lookup"><span data-stu-id="1b47d-594">If the string could be converted to a GUID, then the IsGuid function evaluated to true.</span></span>

<span data-ttu-id="1b47d-595">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="1b47d-596">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-596">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-597">Identyfikator GUID jest zdefiniowany jako ciąg, po jednej z tych wzorców: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx lub {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="1b47d-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="1b47d-598">Używany do określenia, czy CGuid() mogą być skutecznie.</span><span class="sxs-lookup"><span data-stu-id="1b47d-598">Used to determine if CGuid() can be successful.</span></span>

<span data-ttu-id="1b47d-599">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="1b47d-600">Jeśli StrAttribute ma format identyfikatora GUID, zwróć reprezentacja binarna, w przeciwnym razie zwraca wartość Null.</span><span class="sxs-lookup"><span data-stu-id="1b47d-600">If the StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="1b47d-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="1b47d-601">IsNull</span></span>
<span data-ttu-id="1b47d-602">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-602">**Description:**</span></span>  
<span data-ttu-id="1b47d-603">Jeśli wyrażenie ma wartość Null, funkcja IsNull zwraca wartość true.</span><span class="sxs-lookup"><span data-stu-id="1b47d-603">If the expression evaluates to Null, then the IsNull function returns true.</span></span>

<span data-ttu-id="1b47d-604">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="1b47d-605">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-605">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-606">Dla atrybutu o wartości Null jest wyrażona braku atrybutu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-606">For an attribute, a Null is expressed by the absence of the attribute.</span></span>

<span data-ttu-id="1b47d-607">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="1b47d-608">Zwraca wartość PRAWDA, jeśli ten atrybut nie jest obecny w CS lub MV.</span><span class="sxs-lookup"><span data-stu-id="1b47d-608">Returns True if the attribute is not present in the CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="1b47d-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="1b47d-609">IsNullOrEmpty</span></span>
<span data-ttu-id="1b47d-610">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-610">**Description:**</span></span>  
<span data-ttu-id="1b47d-611">Jeśli wyrażenie ma wartość null lub pusty ciąg, funkcja IsNullOrEmpty zwraca wartość true.</span><span class="sxs-lookup"><span data-stu-id="1b47d-611">If the expression is null or an empty string, then the IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="1b47d-612">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="1b47d-613">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-613">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-614">Dla atrybutu to może zwrócić wartość True, jeśli ten atrybut nie istnieje lub jest obecny, ale jest pustym ciągiem.</span><span class="sxs-lookup"><span data-stu-id="1b47d-614">For an attribute, this would evaluate to True if the attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="1b47d-615">Odwrotność funkcji ten nosi nazwę IsPresent.</span><span class="sxs-lookup"><span data-stu-id="1b47d-615">The inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="1b47d-616">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="1b47d-617">Zwraca wartość PRAWDA, jeśli ten atrybut nie jest obecny lub jest pustym ciągiem CS lub MV.</span><span class="sxs-lookup"><span data-stu-id="1b47d-617">Returns True if the attribute is not present or is an empty string in the CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="1b47d-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="1b47d-618">IsNumeric</span></span>
<span data-ttu-id="1b47d-619">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-619">**Description:**</span></span>  
<span data-ttu-id="1b47d-620">Funkcja IsNumeric zwraca wartość logiczną wskazującą, czy wyrażenie może przyjąć jako liczba typu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-620">The IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="1b47d-621">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="1b47d-622">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-622">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-623">Używany do określenia, czy CNum() mogą być skutecznie można przeanalizować wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="1b47d-623">Used to determine if CNum() can be successful to parse the expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="1b47d-624">IsString</span><span class="sxs-lookup"><span data-stu-id="1b47d-624">IsString</span></span>
<span data-ttu-id="1b47d-625">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-625">**Description:**</span></span>  
<span data-ttu-id="1b47d-626">Jeśli do typu ciągu można obliczyć wyrażenia, następnie funkcja IsString ma wartość True.</span><span class="sxs-lookup"><span data-stu-id="1b47d-626">If the expression can be evaluated to a string type, then the IsString function evaluates to True.</span></span>

<span data-ttu-id="1b47d-627">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="1b47d-628">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-628">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-629">Używany do określenia, czy CStr() mogą być skutecznie można przeanalizować wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="1b47d-629">Used to determine if CStr() can be successful to parse the expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="1b47d-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="1b47d-630">IsPresent</span></span>
<span data-ttu-id="1b47d-631">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-631">**Description:**</span></span>  
<span data-ttu-id="1b47d-632">Jeśli wyrażenie na ciąg, który nie jest równa Null i nie jest pusta, funkcja IsPresent zwraca wartość true.</span><span class="sxs-lookup"><span data-stu-id="1b47d-632">If the expression evaluates to a string that is not Null and is not empty, then the IsPresent function returns true.</span></span>

<span data-ttu-id="1b47d-633">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="1b47d-634">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-634">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-635">Odwrotność funkcji ten nosi nazwę IsNullOrEmpty.</span><span class="sxs-lookup"><span data-stu-id="1b47d-635">The inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="1b47d-636">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="1b47d-637">Element</span><span class="sxs-lookup"><span data-stu-id="1b47d-637">Item</span></span>
<span data-ttu-id="1b47d-638">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-638">**Description:**</span></span>  
<span data-ttu-id="1b47d-639">Funkcja Item zwraca jeden element z ciągu/atrybutów wielowartościowych.</span><span class="sxs-lookup"><span data-stu-id="1b47d-639">The Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="1b47d-640">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="1b47d-641">Atrybut: atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="1b47d-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="1b47d-642">Indeks: indeks elementu w ciągu wielowartościowych.</span><span class="sxs-lookup"><span data-stu-id="1b47d-642">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="1b47d-643">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-643">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-644">Funkcja Item przydaje się wraz z funkcji zawiera, ponieważ to drugie funkcja zwraca indeks elementu w atrybutów wielowartościowych.</span><span class="sxs-lookup"><span data-stu-id="1b47d-644">The Item function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="1b47d-645">Zwraca błąd, jeśli indeks jest poza zakresem.</span><span class="sxs-lookup"><span data-stu-id="1b47d-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="1b47d-646">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="1b47d-647">Zwraca podstawowego adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="1b47d-647">Returns the primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="1b47d-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="1b47d-648">ItemOrNull</span></span>
<span data-ttu-id="1b47d-649">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-649">**Description:**</span></span>  
<span data-ttu-id="1b47d-650">Funkcja ItemOrNull zwraca jeden element z ciągu/atrybutów wielowartościowych.</span><span class="sxs-lookup"><span data-stu-id="1b47d-650">The ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="1b47d-651">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="1b47d-652">Atrybut: atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="1b47d-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="1b47d-653">Indeks: indeks elementu w ciągu wielowartościowych.</span><span class="sxs-lookup"><span data-stu-id="1b47d-653">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="1b47d-654">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-654">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-655">Funkcja ItemOrNull przydaje się wraz z funkcji zawiera, ponieważ to drugie funkcja zwraca indeks elementu w atrybutów wielowartościowych.</span><span class="sxs-lookup"><span data-stu-id="1b47d-655">The ItemOrNull function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="1b47d-656">Jeśli indeks jest poza zakresem, zwraca wartość Null.</span><span class="sxs-lookup"><span data-stu-id="1b47d-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="1b47d-657">Join</span><span class="sxs-lookup"><span data-stu-id="1b47d-657">Join</span></span>
<span data-ttu-id="1b47d-658">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-658">**Description:**</span></span>  
<span data-ttu-id="1b47d-659">Funkcja sprzężenia wielowartościowe ciąg znaków i zwraca ciąg pojedynczej wartości z określonego separatorem wstawione między każdym z elementów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-659">The Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="1b47d-660">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="1b47d-661">Atrybut: zawierającego ciągi, które ma zostać umieszczony atrybutów wielowartościowych.</span><span class="sxs-lookup"><span data-stu-id="1b47d-661">attribute: Multi-valued attribute containing strings to be joined.</span></span>
* <span data-ttu-id="1b47d-662">Ogranicznik: dowolny ciąg używany do rozdzielania podciągów w zwracany ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-662">delimiter: Any string, used to separate the substrings in the returned string.</span></span> <span data-ttu-id="1b47d-663">Pominięcie znak spacji ("") jest używany.</span><span class="sxs-lookup"><span data-stu-id="1b47d-663">If omitted, the space character (" ") is used.</span></span> <span data-ttu-id="1b47d-664">Jeśli wartość ogranicznika jest ciągiem o zerowej długości ("") lub Nothing, wszystkie elementy na liście są połączone z ogranicznikami nie.</span><span class="sxs-lookup"><span data-stu-id="1b47d-664">If Delimiter is a zero-length string ("") or Nothing, all items in the list are concatenated with no delimiters.</span></span>

<span data-ttu-id="1b47d-665">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="1b47d-665">**Remarks**</span></span>  
<span data-ttu-id="1b47d-666">Występuje parzystość między funkcji dołączania i podziału.</span><span class="sxs-lookup"><span data-stu-id="1b47d-666">There is parity between the Join and Split functions.</span></span> <span data-ttu-id="1b47d-667">Funkcja sprzężenia pobiera tablicę ciągów i dołącza je za pomocą ciągu ogranicznik, aby zwrócić pojedynczy ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-667">The Join function takes an array of strings and joins them using a delimiter string, to return a single string.</span></span> <span data-ttu-id="1b47d-668">Funkcja podziału ciąg znaków i oddziela go na ogranicznik, aby zwracało tablicę ciągów.</span><span class="sxs-lookup"><span data-stu-id="1b47d-668">The Split function takes a string and separates it at the delimiter, to return an array of strings.</span></span> <span data-ttu-id="1b47d-669">Najważniejsza różnica jest jednak czy sprzężenia można ciągów z dowolnym ciągiem ogranicznik, podziału tylko rozdzielić ciągów za pomocą pojedynczy znak ogranicznika.</span><span class="sxs-lookup"><span data-stu-id="1b47d-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="1b47d-670">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="1b47d-671">Może zwrócić: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="1b47d-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="1b47d-672">LCase</span><span class="sxs-lookup"><span data-stu-id="1b47d-672">LCase</span></span>
<span data-ttu-id="1b47d-673">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-673">**Description:**</span></span>  
<span data-ttu-id="1b47d-674">Funkcja LCase konwertuje wszystkie znaki w ciągu na małe litery.</span><span class="sxs-lookup"><span data-stu-id="1b47d-674">The LCase function converts all characters in a string to lower case.</span></span>

<span data-ttu-id="1b47d-675">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="1b47d-676">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="1b47d-677">Zwraca "test".</span><span class="sxs-lookup"><span data-stu-id="1b47d-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="1b47d-678">Po lewej</span><span class="sxs-lookup"><span data-stu-id="1b47d-678">Left</span></span>
<span data-ttu-id="1b47d-679">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-679">**Description:**</span></span>  
<span data-ttu-id="1b47d-680">Po lewej stronie funkcja zwraca określoną liczbę znaków z lewej strony ciągu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-680">The Left function returns a specified number of characters from the left of a string.</span></span>

<span data-ttu-id="1b47d-681">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="1b47d-682">ciągu: ciąg do zwracania znaków z</span><span class="sxs-lookup"><span data-stu-id="1b47d-682">string: the string to return characters from</span></span>
* <span data-ttu-id="1b47d-683">NumChars: Liczba identyfikująca liczbę znaków do zwrócenia z początku ciąg (po lewej)</span><span class="sxs-lookup"><span data-stu-id="1b47d-683">NumChars: a number identifying the number of characters to return from the beginning (left) of string</span></span>

<span data-ttu-id="1b47d-684">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-684">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-685">Ciąg zawierający pierwszych znaków numChars w ciągu:</span><span class="sxs-lookup"><span data-stu-id="1b47d-685">A string containing the first numChars characters in string:</span></span>

* <span data-ttu-id="1b47d-686">Jeśli numChars = 0, zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="1b47d-687">Jeśli numChars < 0, zwraca ciąg wejściowy.</span><span class="sxs-lookup"><span data-stu-id="1b47d-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="1b47d-688">Jeśli ciąg ma wartość null, zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-688">If string is null, return empty string.</span></span>

<span data-ttu-id="1b47d-689">Jeśli ciąg zawiera mniej znaków niż liczba numChars określony w, zostanie zwrócony ciąg jest taki sam jak ciąg (tj. zawierający wszystkie znaki w parametrze 1).</span><span class="sxs-lookup"><span data-stu-id="1b47d-689">If string contains fewer characters than the number specified in numChars, a string identical to string (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="1b47d-690">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="1b47d-691">Zwraca wartość "Joh".</span><span class="sxs-lookup"><span data-stu-id="1b47d-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="1b47d-692">Długość</span><span class="sxs-lookup"><span data-stu-id="1b47d-692">Len</span></span>
<span data-ttu-id="1b47d-693">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-693">**Description:**</span></span>  
<span data-ttu-id="1b47d-694">Funkcja Len zwraca liczbę znaków w ciągu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-694">The Len function returns number of characters in a string.</span></span>

<span data-ttu-id="1b47d-695">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="1b47d-696">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="1b47d-697">Zwraca 8</span><span class="sxs-lookup"><span data-stu-id="1b47d-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="1b47d-698">Przytp</span><span class="sxs-lookup"><span data-stu-id="1b47d-698">LTrim</span></span>
<span data-ttu-id="1b47d-699">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-699">**Description:**</span></span>  
<span data-ttu-id="1b47d-700">Funkcja LTrim usuwa spacji wiodących z ciągu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-700">The LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="1b47d-701">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="1b47d-702">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="1b47d-703">Zwraca "Test"</span><span class="sxs-lookup"><span data-stu-id="1b47d-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="1b47d-704">MID</span><span class="sxs-lookup"><span data-stu-id="1b47d-704">Mid</span></span>
<span data-ttu-id="1b47d-705">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-705">**Description:**</span></span>  
<span data-ttu-id="1b47d-706">Funkcja Mid zwraca określoną liczbę znaków od określonej pozycji w ciągu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-706">The Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="1b47d-707">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="1b47d-708">ciągu: ciąg do zwracania znaków z</span><span class="sxs-lookup"><span data-stu-id="1b47d-708">string: the string to return characters from</span></span>
* <span data-ttu-id="1b47d-709">Rozpocznij: Liczba identyfikująca początkowe położenie w ciągu do zwracania znaków z</span><span class="sxs-lookup"><span data-stu-id="1b47d-709">start: a number identifying the starting position in string to return characters from</span></span>
* <span data-ttu-id="1b47d-710">NumChars: Liczba identyfikująca liczbę znaków do zwrócenia z pozycji w ciągu</span><span class="sxs-lookup"><span data-stu-id="1b47d-710">NumChars: a number identifying the number of characters to return from position in string</span></span>

<span data-ttu-id="1b47d-711">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-711">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-712">Uruchom numChars zwracanych znaków, zaczynając od pozycji w ciągu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="1b47d-713">Ciąg zawierający numChars znaków od początku pozycji w ciągu:</span><span class="sxs-lookup"><span data-stu-id="1b47d-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="1b47d-714">Jeśli numChars = 0, zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="1b47d-715">Jeśli numChars < 0, zwraca ciąg wejściowy.</span><span class="sxs-lookup"><span data-stu-id="1b47d-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="1b47d-716">Jeśli start > długość ciągu, zwraca ciąg wejściowy.</span><span class="sxs-lookup"><span data-stu-id="1b47d-716">If start > the length of string, return input string.</span></span>
* <span data-ttu-id="1b47d-717">Jeśli start < = 0, zwraca ciąg wejściowy.</span><span class="sxs-lookup"><span data-stu-id="1b47d-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="1b47d-718">Jeśli ciąg ma wartość null, zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-718">If string is null, return empty string.</span></span>

<span data-ttu-id="1b47d-719">Jeśli nie są znaki numChar pozostałych w ciągu od początku pozycji, jako wiele znaków, jak to możliwe są zwracane.</span><span class="sxs-lookup"><span data-stu-id="1b47d-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="1b47d-720">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="1b47d-721">Zwraca wartość "nie hn".</span><span class="sxs-lookup"><span data-stu-id="1b47d-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="1b47d-722">Zwraca "Nowak"</span><span class="sxs-lookup"><span data-stu-id="1b47d-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="1b47d-723">Teraz</span><span class="sxs-lookup"><span data-stu-id="1b47d-723">Now</span></span>
<span data-ttu-id="1b47d-724">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-724">**Description:**</span></span>  
<span data-ttu-id="1b47d-725">Teraz funkcja zwraca wartość typu DateTime Określanie aktualnej daty i godziny, zgodnie z komputera datę i godzinę systemową.</span><span class="sxs-lookup"><span data-stu-id="1b47d-725">The Now function returns a DateTime specifying the current date and time, according to your computer's system date and time.</span></span>

<span data-ttu-id="1b47d-726">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="1b47d-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="1b47d-727">NumFromDate</span></span>
<span data-ttu-id="1b47d-728">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-728">**Description:**</span></span>  
<span data-ttu-id="1b47d-729">Funkcja NumFromDate zwraca datę w formacie daty przez usługi AD.</span><span class="sxs-lookup"><span data-stu-id="1b47d-729">The NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="1b47d-730">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="1b47d-731">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="1b47d-732">Zwraca 129699324000000000</span><span class="sxs-lookup"><span data-stu-id="1b47d-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="1b47d-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="1b47d-733">PadLeft</span></span>
<span data-ttu-id="1b47d-734">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-734">**Description:**</span></span>  
<span data-ttu-id="1b47d-735">PadLeft funkcja lewej podkładki ciąg do określonej długości, przy użyciu znaków podany dopełnienia.</span><span class="sxs-lookup"><span data-stu-id="1b47d-735">The PadLeft function left-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="1b47d-736">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="1b47d-737">ciągu: ciąg do konsoli.</span><span class="sxs-lookup"><span data-stu-id="1b47d-737">string: the string to pad.</span></span>
* <span data-ttu-id="1b47d-738">długość: liczba całkowita reprezentująca wymagana długość ciągu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-738">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="1b47d-739">padCharacter: ciąg składający się z jednego znaku do użycia jako znak konsoli</span><span class="sxs-lookup"><span data-stu-id="1b47d-739">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="1b47d-740">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-740">**Remarks:**</span></span>

* <span data-ttu-id="1b47d-741">Jeśli długość ciągu jest mniejsza niż długość, padCharacter wielokrotnie jest dołączany na początku (po lewej) ciągu do momentu jego długość jest równa długości.</span><span class="sxs-lookup"><span data-stu-id="1b47d-741">If the length of string is less than length, then padCharacter is repeatedly appended to the beginning (left) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="1b47d-742">padCharacter może być znaku spacji, ale nie może mieć wartości null.</span><span class="sxs-lookup"><span data-stu-id="1b47d-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="1b47d-743">Jeśli długość ciągu jest równa lub większa niż długość, ciąg zostanie zwrócony bez zmian.</span><span class="sxs-lookup"><span data-stu-id="1b47d-743">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="1b47d-744">Jeśli ciąg ma długość większą niż lub równa długości, zostanie zwrócony ciąg jest taki sam jak ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-744">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="1b47d-745">Jeśli długość ciągu jest mniejsza niż długość, nowy ciąg o długości żądaną zostanie zwrócony ciąg zawierający dopełniane przy padCharacter.</span><span class="sxs-lookup"><span data-stu-id="1b47d-745">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="1b47d-746">Jeśli ciąg ma wartość null, funkcja zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-746">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="1b47d-747">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="1b47d-748">Zwraca wartość "000000User".</span><span class="sxs-lookup"><span data-stu-id="1b47d-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="1b47d-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="1b47d-749">PadRight</span></span>
<span data-ttu-id="1b47d-750">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-750">**Description:**</span></span>  
<span data-ttu-id="1b47d-751">PadRight funkcja prawo podkładki ciąg do określonej długości, przy użyciu znaków podany dopełnienia.</span><span class="sxs-lookup"><span data-stu-id="1b47d-751">The PadRight function right-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="1b47d-752">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="1b47d-753">ciągu: ciąg do konsoli.</span><span class="sxs-lookup"><span data-stu-id="1b47d-753">string: the string to pad.</span></span>
* <span data-ttu-id="1b47d-754">długość: liczba całkowita reprezentująca wymagana długość ciągu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-754">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="1b47d-755">padCharacter: ciąg składający się z jednego znaku do użycia jako znak konsoli</span><span class="sxs-lookup"><span data-stu-id="1b47d-755">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="1b47d-756">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-756">**Remarks:**</span></span>

* <span data-ttu-id="1b47d-757">Jeśli długość ciągu jest mniejsza niż długość, następnie padCharacter jest wielokrotnie dodane do (po prawej) końca ciągu dopóki nie długości równej długości.</span><span class="sxs-lookup"><span data-stu-id="1b47d-757">If the length of string is less than length, then padCharacter is repeatedly appended to the end (right) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="1b47d-758">padCharacter może być znaku spacji, ale nie może mieć wartości null.</span><span class="sxs-lookup"><span data-stu-id="1b47d-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="1b47d-759">Jeśli długość ciągu jest równa lub większa niż długość, ciąg zostanie zwrócony bez zmian.</span><span class="sxs-lookup"><span data-stu-id="1b47d-759">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="1b47d-760">Jeśli ciąg ma długość większą niż lub równa długości, zostanie zwrócony ciąg jest taki sam jak ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-760">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="1b47d-761">Jeśli długość ciągu jest mniejsza niż długość, nowy ciąg o długości żądaną zostanie zwrócony ciąg zawierający dopełniane przy padCharacter.</span><span class="sxs-lookup"><span data-stu-id="1b47d-761">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="1b47d-762">Jeśli ciąg ma wartość null, funkcja zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-762">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="1b47d-763">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="1b47d-764">Zwraca wartość "User000000".</span><span class="sxs-lookup"><span data-stu-id="1b47d-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="1b47d-765">PCase</span><span class="sxs-lookup"><span data-stu-id="1b47d-765">PCase</span></span>
<span data-ttu-id="1b47d-766">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-766">**Description:**</span></span>  
<span data-ttu-id="1b47d-767">Funkcja PCase konwertuje pierwszy znak każdego wyrazu odstępami w ciągu na wielkie litery, a wszystkie inne znaki są konwertowane na małe litery.</span><span class="sxs-lookup"><span data-stu-id="1b47d-767">The PCase function converts the first character of each space delimited word in a string to upper case, and all other characters are converted to lower case.</span></span>

<span data-ttu-id="1b47d-768">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="1b47d-769">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-769">**Remarks:**</span></span>

* <span data-ttu-id="1b47d-770">Ta funkcja nie jest aktualnie dostępny prawidłowego wielkość liter można przekonwertować słowo, które jest całkowicie wielkie litery, takich jak skrót.</span><span class="sxs-lookup"><span data-stu-id="1b47d-770">This function does not currently provide proper casing to convert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="1b47d-771">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="1b47d-772">Zwraca "Test".</span><span class="sxs-lookup"><span data-stu-id="1b47d-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="1b47d-773">Zwraca "Test"</span><span class="sxs-lookup"><span data-stu-id="1b47d-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="1b47d-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="1b47d-774">RandomNum</span></span>
<span data-ttu-id="1b47d-775">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-775">**Description:**</span></span>  
<span data-ttu-id="1b47d-776">Funkcja RandomNum zwraca liczbę losową określonego interwału.</span><span class="sxs-lookup"><span data-stu-id="1b47d-776">The RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="1b47d-777">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="1b47d-778">Rozpocznij: Liczba identyfikująca dolny limit losowych wartości do wygenerowania</span><span class="sxs-lookup"><span data-stu-id="1b47d-778">start: a number identifying the lower limit of the random value to generate</span></span>
* <span data-ttu-id="1b47d-779">końcowy: Liczba identyfikująca górny limit losowych wartości do wygenerowania</span><span class="sxs-lookup"><span data-stu-id="1b47d-779">end: a number identifying the upper limit of the random value to generate</span></span>

<span data-ttu-id="1b47d-780">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="1b47d-781">Może zwrócić 734.</span><span class="sxs-lookup"><span data-stu-id="1b47d-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="1b47d-782">Removeduplicates —</span><span class="sxs-lookup"><span data-stu-id="1b47d-782">RemoveDuplicates</span></span>
<span data-ttu-id="1b47d-783">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-783">**Description:**</span></span>  
<span data-ttu-id="1b47d-784">Removeduplicates — funkcja wielowartościowe ciąg znaków i upewnij się, że każda wartość jest unikatowa.</span><span class="sxs-lookup"><span data-stu-id="1b47d-784">The RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="1b47d-785">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="1b47d-786">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="1b47d-787">Zwraca atrybutu oczyszczony proxyAddress, w której zostały usunięte wszystkie zduplikowane wartości.</span><span class="sxs-lookup"><span data-stu-id="1b47d-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="1b47d-788">Replace</span><span class="sxs-lookup"><span data-stu-id="1b47d-788">Replace</span></span>
<span data-ttu-id="1b47d-789">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-789">**Description:**</span></span>  
<span data-ttu-id="1b47d-790">Funkcja Replace zamienia wszystkie wystąpienia ciągu na inny ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-790">The Replace function replaces all occurrences of a string to another string.</span></span>

<span data-ttu-id="1b47d-791">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="1b47d-792">ciągu: ciąg, aby zastąpić wartości.</span><span class="sxs-lookup"><span data-stu-id="1b47d-792">string: A string to replace values in.</span></span>
* <span data-ttu-id="1b47d-793">OldValue: Ciąg do wyszukania oraz do zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="1b47d-793">OldValue: The string to search for and to replace.</span></span>
* <span data-ttu-id="1b47d-794">NewValue: Ciąg do zastąpienia w.</span><span class="sxs-lookup"><span data-stu-id="1b47d-794">NewValue: The string to replace to.</span></span>

<span data-ttu-id="1b47d-795">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-795">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-796">Funkcja rozpoznaje następujących monikerów specjalne:</span><span class="sxs-lookup"><span data-stu-id="1b47d-796">The function recognizes the following special monikers:</span></span>

* <span data-ttu-id="1b47d-797">\n — nowy wiersz</span><span class="sxs-lookup"><span data-stu-id="1b47d-797">\n – New Line</span></span>
* <span data-ttu-id="1b47d-798">\r — powrót karetki</span><span class="sxs-lookup"><span data-stu-id="1b47d-798">\r – Carriage Return</span></span>
* <span data-ttu-id="1b47d-799">\t — karta</span><span class="sxs-lookup"><span data-stu-id="1b47d-799">\t – Tab</span></span>

<span data-ttu-id="1b47d-800">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="1b47d-801">Zastępuje CRLF przecinek i spacja i może prowadzić do "Co Microsoft sposób, Redmond, WA, USA"</span><span class="sxs-lookup"><span data-stu-id="1b47d-801">Replaces CRLF with a comma and space, and could lead to "One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="1b47d-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="1b47d-802">ReplaceChars</span></span>
<span data-ttu-id="1b47d-803">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-803">**Description:**</span></span>  
<span data-ttu-id="1b47d-804">Funkcja ReplaceChars zamienia wszystkie wystąpienia znaków w ciągu ReplacePattern.</span><span class="sxs-lookup"><span data-stu-id="1b47d-804">The ReplaceChars function replaces all occurrences of characters found in the ReplacePattern string.</span></span>

<span data-ttu-id="1b47d-805">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="1b47d-806">ciągu: ciąg, aby zastąpić znaków.</span><span class="sxs-lookup"><span data-stu-id="1b47d-806">string: A string to replace characters in.</span></span>
* <span data-ttu-id="1b47d-807">ReplacePattern: ciąg zawierający słownik z znaki do zamiany.</span><span class="sxs-lookup"><span data-stu-id="1b47d-807">ReplacePattern: a string containing a dictionary with characters to replace.</span></span>

<span data-ttu-id="1b47d-808">Format to {źródło1}: {nazwach target1}, {źródło2}: {target2}, {źródłoN}, {targetN} gdzie źródła jest znak można znaleźć i docelowego należy zastąpić ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-808">The format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is the character to find and target the string to replace with.</span></span>

<span data-ttu-id="1b47d-809">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-809">**Remarks:**</span></span>

* <span data-ttu-id="1b47d-810">Funkcja przyjmuje każdego wystąpienia określonych źródeł i zastępuje je z elementami docelowymi.</span><span class="sxs-lookup"><span data-stu-id="1b47d-810">The function takes each occurrence of defined sources and replaces them with the targets.</span></span>
* <span data-ttu-id="1b47d-811">Źródło musi zawierać dokładnie jeden znak (unicode).</span><span class="sxs-lookup"><span data-stu-id="1b47d-811">The source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="1b47d-812">Źródło nie może być pusta ani więcej niż jeden znak (Błąd analizy).</span><span class="sxs-lookup"><span data-stu-id="1b47d-812">The source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="1b47d-813">Element docelowy może mieć wielu znaków, na przykład ö:oe, β:ss.</span><span class="sxs-lookup"><span data-stu-id="1b47d-813">The target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="1b47d-814">Element docelowy może być pusta, wskazującą, czy znak powinna zostać usunięta.</span><span class="sxs-lookup"><span data-stu-id="1b47d-814">The target can be empty indicating that the character should be removed.</span></span>
* <span data-ttu-id="1b47d-815">Źródło jest rozróżniana wielkość liter i muszą być identyczne.</span><span class="sxs-lookup"><span data-stu-id="1b47d-815">The source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="1b47d-816">(Przecinek) i: (dwukropek) są zastrzeżone znaki i nie można zastąpić przy użyciu tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="1b47d-816">The , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="1b47d-817">Spacje i inne białe znaki w ciągu ReplacePattern są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="1b47d-817">Spaces and other white characters in the ReplacePattern string are ignored.</span></span>

<span data-ttu-id="1b47d-818">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="1b47d-819">Zwraca Raksmorgas</span><span class="sxs-lookup"><span data-stu-id="1b47d-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="1b47d-820">Zwraca "ONeil", jeden znacznik zdefiniowano do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="1b47d-820">Returns "ONeil", the single tick is defined to be removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="1b47d-821">Prawo</span><span class="sxs-lookup"><span data-stu-id="1b47d-821">Right</span></span>
<span data-ttu-id="1b47d-822">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-822">**Description:**</span></span>  
<span data-ttu-id="1b47d-823">Funkcja PRAWY zwraca określoną liczbę znaków z prawej strony (Zakończ), ciągu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-823">The Right function returns a specified number of characters from the right (end) of a string.</span></span>

<span data-ttu-id="1b47d-824">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="1b47d-825">ciągu: ciąg do zwracania znaków z</span><span class="sxs-lookup"><span data-stu-id="1b47d-825">string: the string to return characters from</span></span>
* <span data-ttu-id="1b47d-826">NumChars: Liczba identyfikująca liczbę znaków, które ma zostać zwrócony przez (po prawej) końca ciągu</span><span class="sxs-lookup"><span data-stu-id="1b47d-826">NumChars: a number identifying the number of characters to return from the end (right) of string</span></span>

<span data-ttu-id="1b47d-827">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-827">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-828">Od ostatniej pozycji w ciągu są zwracane NumChars znaki.</span><span class="sxs-lookup"><span data-stu-id="1b47d-828">NumChars characters are returned from the last position of string.</span></span>

<span data-ttu-id="1b47d-829">Ciąg zawierający ostatnie znaki numChars w ciągu:</span><span class="sxs-lookup"><span data-stu-id="1b47d-829">A string containing the last numChars characters in string:</span></span>

* <span data-ttu-id="1b47d-830">Jeśli numChars = 0, zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="1b47d-831">Jeśli numChars < 0, zwraca ciąg wejściowy.</span><span class="sxs-lookup"><span data-stu-id="1b47d-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="1b47d-832">Jeśli ciąg ma wartość null, zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-832">If string is null, return empty string.</span></span>

<span data-ttu-id="1b47d-833">Jeśli ciąg zawiera mniej znaków niż liczba NumChars określony w, zostanie zwrócony ciąg jest taki sam jak ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-833">If string contains fewer characters than the number specified in NumChars, a string identical to string is returned.</span></span>

<span data-ttu-id="1b47d-834">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="1b47d-835">Zwraca wartość "Nowak".</span><span class="sxs-lookup"><span data-stu-id="1b47d-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="1b47d-836">Przytk</span><span class="sxs-lookup"><span data-stu-id="1b47d-836">RTrim</span></span>
<span data-ttu-id="1b47d-837">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-837">**Description:**</span></span>  
<span data-ttu-id="1b47d-838">Funkcja RTrim usuwa spacje końcowe z ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-838">The RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="1b47d-839">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="1b47d-840">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="1b47d-841">Zwraca "Test".</span><span class="sxs-lookup"><span data-stu-id="1b47d-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="1b47d-842">Wybierz pozycję</span><span class="sxs-lookup"><span data-stu-id="1b47d-842">Select</span></span>
<span data-ttu-id="1b47d-843">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-843">**Description:**</span></span>  
<span data-ttu-id="1b47d-844">Wszystkie wartości w atrybutu wielowartościowego (lub dane wyjściowe wyrażenia) na podstawie funkcji określony proces.</span><span class="sxs-lookup"><span data-stu-id="1b47d-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="1b47d-845">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="1b47d-846">element: reprezentuje element w atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="1b47d-846">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="1b47d-847">Atrybut: atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="1b47d-847">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="1b47d-848">wyrażenie: wyrażenie, które zwraca kolekcję wartości</span><span class="sxs-lookup"><span data-stu-id="1b47d-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="1b47d-849">warunek: dowolnej funkcji, które może przetworzyć elementu w atrybucie</span><span class="sxs-lookup"><span data-stu-id="1b47d-849">condition: any function that can process an item in the attribute</span></span>

<span data-ttu-id="1b47d-850">**Przykłady:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="1b47d-851">Zwraca wszystkie wartości w faksów atrybutu wielowartościowego, po usunięciu łączniki (-).</span><span class="sxs-lookup"><span data-stu-id="1b47d-851">Return all the values in the multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="1b47d-852">Podziel</span><span class="sxs-lookup"><span data-stu-id="1b47d-852">Split</span></span>
<span data-ttu-id="1b47d-853">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-853">**Description:**</span></span>  
<span data-ttu-id="1b47d-854">Funkcja podziału oddzielone znakiem ogranicznika ciąg znaków i ułatwia wielokrotne wartości ciągu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-854">The Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="1b47d-855">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="1b47d-856">wartość: ciąg do oddzielania znakiem ogranicznika.</span><span class="sxs-lookup"><span data-stu-id="1b47d-856">value: the string with a delimiter character to separate.</span></span>
* <span data-ttu-id="1b47d-857">Ogranicznik: pojedynczy znak ma być używany jako ogranicznik.</span><span class="sxs-lookup"><span data-stu-id="1b47d-857">delimiter: single character to be used as the delimiter.</span></span>
* <span data-ttu-id="1b47d-858">limit: maksymalną liczbę wartości, które może zwracać.</span><span class="sxs-lookup"><span data-stu-id="1b47d-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="1b47d-859">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="1b47d-860">Zwraca ciąg wielowartościowe z 2 elementami jest przydatne w przypadku atrybutu proxyAddress.</span><span class="sxs-lookup"><span data-stu-id="1b47d-860">Returns a multi-valued string with 2 elements useful for the proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="1b47d-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="1b47d-861">StringFromGuid</span></span>
<span data-ttu-id="1b47d-862">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-862">**Description:**</span></span>  
<span data-ttu-id="1b47d-863">Funkcja StringFromGuid przyjmuje binarny identyfikator GUID i konwertuje ją na ciąg</span><span class="sxs-lookup"><span data-stu-id="1b47d-863">The StringFromGuid function takes a binary GUID and converts it to a string</span></span>

<span data-ttu-id="1b47d-864">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="1b47d-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="1b47d-865">StringFromSid</span></span>
<span data-ttu-id="1b47d-866">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-866">**Description:**</span></span>  
<span data-ttu-id="1b47d-867">Funkcja StringFromSid konwertuje tablicę bajtów zawierającą identyfikator zabezpieczeń na ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-867">The StringFromSid function converts a byte array containing a security identifier to a string.</span></span>

<span data-ttu-id="1b47d-868">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="1b47d-869">Przełącznik</span><span class="sxs-lookup"><span data-stu-id="1b47d-869">Switch</span></span>
<span data-ttu-id="1b47d-870">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-870">**Description:**</span></span>  
<span data-ttu-id="1b47d-871">Funkcja przełącznika służy do zwracania pojedynczą wartość na podstawie ocenionych warunków.</span><span class="sxs-lookup"><span data-stu-id="1b47d-871">The Switch function is used to return a single value based on evaluated conditions.</span></span>

<span data-ttu-id="1b47d-872">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="1b47d-873">wyrażenie: użytkownik chce ocenić wyrażenia Variant.</span><span class="sxs-lookup"><span data-stu-id="1b47d-873">expr: Variant expression you want to evaluate.</span></span>
* <span data-ttu-id="1b47d-874">wartość: wartość zwracaną, jeśli odpowiednie wyrażenie ma wartość PRAWDA.</span><span class="sxs-lookup"><span data-stu-id="1b47d-874">value: Value to be returned if the corresponding expression is True.</span></span>

<span data-ttu-id="1b47d-875">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-875">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-876">Lista argumentów funkcji przełącznika składa się z par wyrażeń i wartości.</span><span class="sxs-lookup"><span data-stu-id="1b47d-876">The Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="1b47d-877">Wyrażenia są przetwarzane od lewej do prawej i jest zwracana wartość skojarzoną z pierwszym wyrażeniem, aby zwrócić wartość True.</span><span class="sxs-lookup"><span data-stu-id="1b47d-877">The expressions are evaluated from left to right, and the value associated with the first expression to evaluate to True is returned.</span></span> <span data-ttu-id="1b47d-878">Jeśli elementy nie są poprawnie sparowane, występuje błąd w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="1b47d-878">If the parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="1b47d-879">Na przykład jeśli Wyr1 ma wartość PRAWDA, przełącznik zwraca wartość1.</span><span class="sxs-lookup"><span data-stu-id="1b47d-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="1b47d-880">Jeśli wyrażenie-1 jest wartość FAŁSZ, ale wyrażenie-2 ma wartość PRAWDA, przełącznik zwraca wartość-2 i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="1b47d-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="1b47d-881">Przełącznik zwraca rób jeśli:</span><span class="sxs-lookup"><span data-stu-id="1b47d-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="1b47d-882">Brak wyrażenia mają wartość PRAWDA.</span><span class="sxs-lookup"><span data-stu-id="1b47d-882">None of the expressions are True.</span></span>
* <span data-ttu-id="1b47d-883">Pierwsze wyrażenie True ma odpowiadającą mu wartość, która ma wartość Null.</span><span class="sxs-lookup"><span data-stu-id="1b47d-883">The first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="1b47d-884">Przełącznik ocenia wszystkie wyrażenia, mimo że zwracany jest tylko jeden z nich.</span><span class="sxs-lookup"><span data-stu-id="1b47d-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="1b47d-885">Z tego powodu należy uważać na niepożądane skutki uboczne.</span><span class="sxs-lookup"><span data-stu-id="1b47d-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="1b47d-886">Na przykład jeśli oceny dowolne wyrażenie powoduje dzielenie przez zero, wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="1b47d-886">For example, if the evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="1b47d-887">Wartość może być również funkcja błąd, co powoduje zwrócenie niestandardowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-887">Value can also be the Error function, which would return a custom string.</span></span>

<span data-ttu-id="1b47d-888">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="1b47d-889">Zwraca język używany w niektórych miastach głównych, w przeciwnym razie zwraca błąd.</span><span class="sxs-lookup"><span data-stu-id="1b47d-889">Returns the language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="1b47d-890">TRIM</span><span class="sxs-lookup"><span data-stu-id="1b47d-890">Trim</span></span>
<span data-ttu-id="1b47d-891">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-891">**Description:**</span></span>  
<span data-ttu-id="1b47d-892">Funkcja przycinania usuwa spacji wiodących i końcowych białych z ciągu.</span><span class="sxs-lookup"><span data-stu-id="1b47d-892">The Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="1b47d-893">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="1b47d-894">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="1b47d-895">Zwraca "Test".</span><span class="sxs-lookup"><span data-stu-id="1b47d-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="1b47d-896">Usuwa spacje początkowe i końcowe spacje dla każdej wartości w atrybucie proxyAddress.</span><span class="sxs-lookup"><span data-stu-id="1b47d-896">Removes leading and trailing spaces for each value in the proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="1b47d-897">UCase</span><span class="sxs-lookup"><span data-stu-id="1b47d-897">UCase</span></span>
<span data-ttu-id="1b47d-898">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-898">**Description:**</span></span>  
<span data-ttu-id="1b47d-899">Funkcja UCase konwertuje wszystkie znaki w ciągu na wielkie litery.</span><span class="sxs-lookup"><span data-stu-id="1b47d-899">The UCase function converts all characters in a string to upper case.</span></span>

<span data-ttu-id="1b47d-900">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="1b47d-901">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="1b47d-902">Zwraca "TEST".</span><span class="sxs-lookup"><span data-stu-id="1b47d-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="1b47d-903">gdzie</span><span class="sxs-lookup"><span data-stu-id="1b47d-903">Where</span></span>

<span data-ttu-id="1b47d-904">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-904">**Description:**</span></span>  
<span data-ttu-id="1b47d-905">Zwraca podzbiór wartości z atrybutu wielowartościowego (lub dane wyjściowe wyrażenia) na podstawie określonego warunku.</span><span class="sxs-lookup"><span data-stu-id="1b47d-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="1b47d-906">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="1b47d-907">element: reprezentuje element w atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="1b47d-907">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="1b47d-908">Atrybut: atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="1b47d-908">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="1b47d-909">warunek: dowolne wyrażenie, które może przyjąć wartość true lub false</span><span class="sxs-lookup"><span data-stu-id="1b47d-909">condition: any expression that can be evaluated to true or false</span></span>
* <span data-ttu-id="1b47d-910">wyrażenie: wyrażenie, które zwraca kolekcję wartości</span><span class="sxs-lookup"><span data-stu-id="1b47d-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="1b47d-911">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="1b47d-912">Zwraca wartości certyfikatu w atrybutów wielowartościowych certyfikatu użytkownika, które nie są wygasło.</span><span class="sxs-lookup"><span data-stu-id="1b47d-912">Return the certificate values in the multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="1b47d-913">Z</span><span class="sxs-lookup"><span data-stu-id="1b47d-913">With</span></span>
<span data-ttu-id="1b47d-914">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-914">**Description:**</span></span>  
<span data-ttu-id="1b47d-915">Funkcja With umożliwia Uprość wyrażenie złożone, za pomocą zmiennej do reprezentowania Podwyrażenie, która pojawia się jeden lub więcej razy w złożonych wyrażeń.</span><span class="sxs-lookup"><span data-stu-id="1b47d-915">The With function provides a way to simplify a complex expression by using a variable to represent a subexpression which appears one or more times in the complex expression.</span></span>

<span data-ttu-id="1b47d-916">**Składnia:**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="1b47d-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="1b47d-917">Zmienna: reprezentuje Podwyrażenie.</span><span class="sxs-lookup"><span data-stu-id="1b47d-917">variable: Represents the subexpression.</span></span>
* <span data-ttu-id="1b47d-918">Podwyrażenie: Podwyrażenie reprezentowany przez zmienną.</span><span class="sxs-lookup"><span data-stu-id="1b47d-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="1b47d-919">complexExpression: wyrażenie złożone.</span><span class="sxs-lookup"><span data-stu-id="1b47d-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="1b47d-920">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="1b47d-921">Jest funkcjonalnym odpowiednikiem:</span><span class="sxs-lookup"><span data-stu-id="1b47d-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="1b47d-922">Która zwraca tylko niewygasłe certyfikatu wartości w atrybucie certyfikatu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1b47d-922">Which returns only unexpired certificate values in the userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="1b47d-923">Word</span><span class="sxs-lookup"><span data-stu-id="1b47d-923">Word</span></span>
<span data-ttu-id="1b47d-924">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-924">**Description:**</span></span>  
<span data-ttu-id="1b47d-925">Funkcja Word zwraca słowa w ciągu, na podstawie parametrów opisujące ograniczniki oraz numer programu word do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="1b47d-925">The Word function returns a word contained within a string, based on parameters describing the delimiters to use and the word number to return.</span></span>

<span data-ttu-id="1b47d-926">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="1b47d-927">ciągu: ciąg do zwrócenia słowa.</span><span class="sxs-lookup"><span data-stu-id="1b47d-927">string: the string to return a word from.</span></span>
* <span data-ttu-id="1b47d-928">WordNumber: Liczba identyfikująca numer word powinna zostać zwrócona.</span><span class="sxs-lookup"><span data-stu-id="1b47d-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="1b47d-929">Ogranicznik: ciąg reprezentujący delimiter(s), które mają być używane do identyfikowania słowa</span><span class="sxs-lookup"><span data-stu-id="1b47d-929">delimiters: a string representing the delimiter(s) that should be used to identify words</span></span>

<span data-ttu-id="1b47d-930">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-930">**Remarks:**</span></span>  
<span data-ttu-id="1b47d-931">Każdy ciąg znaków w ciągu, rozdzielone co znaków w ograniczniki są identyfikowane jako słowa:</span><span class="sxs-lookup"><span data-stu-id="1b47d-931">Each string of characters in string separated by the one of the characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="1b47d-932">Jeśli liczba < 1, zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="1b47d-933">Jeśli ciąg ma wartość null, zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b47d-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="1b47d-934">Jeśli ciąg zawiera mniej niż liczba słów lub ciąg nie zawiera słów identyfikowane przez ograniczniki, zwracany jest pustym ciągiem.</span><span class="sxs-lookup"><span data-stu-id="1b47d-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="1b47d-935">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="1b47d-935">**Example:**</span></span>  
`Word("The quick brown fox",3," ")`  
<span data-ttu-id="1b47d-936">Zwraca "brązowy"</span><span class="sxs-lookup"><span data-stu-id="1b47d-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="1b47d-937">Zwróci "ma"</span><span class="sxs-lookup"><span data-stu-id="1b47d-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b47d-938">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1b47d-938">Additional Resources</span></span>
* [<span data-ttu-id="1b47d-939">Opis deklaratywne wyrażenia inicjowania obsługi administracyjnej</span><span class="sxs-lookup"><span data-stu-id="1b47d-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="1b47d-940">Azure AD Connect Sync: Dostosowywanie opcji synchronizacji</span><span class="sxs-lookup"><span data-stu-id="1b47d-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="1b47d-941">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b47d-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
