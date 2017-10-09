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
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="e97e0-103">Synchronizacja programu Azure AD Connect: odwołanie do funkcji</span><span class="sxs-lookup"><span data-stu-id="e97e0-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="e97e0-104">W programie Azure AD Connect funkcje są używane toomanipulate wartość atrybutu podczas synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="e97e0-104">In Azure AD Connect, functions are used toomanipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="e97e0-105">Składnia funkcji hello Hello jest wyrazić przy użyciu hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="e97e0-105">hello Syntax of hello functions is expressed using hello following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="e97e0-106">Funkcji jest przeciążony i przyjmuje wiele składni, wyświetlane są wszystkie prawidłowe składni.</span><span class="sxs-lookup"><span data-stu-id="e97e0-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="e97e0-107">Funkcje Hello są silnie typizowane i sprawdź, czy typ hello przekazany typ hello udokumentowane dopasowań.</span><span class="sxs-lookup"><span data-stu-id="e97e0-107">hello functions are strongly typed and they verify that hello type passed in matches hello documented type.</span></span>  
<span data-ttu-id="e97e0-108">Jeśli typ hello nie jest zgodny, jest zgłaszany błąd.</span><span class="sxs-lookup"><span data-stu-id="e97e0-108">If hello type does not match, an error is thrown.</span></span>

<span data-ttu-id="e97e0-109">typy Hello są wyrażane z hello następującej składni:</span><span class="sxs-lookup"><span data-stu-id="e97e0-109">hello types are expressed with hello following syntax:</span></span>

* <span data-ttu-id="e97e0-110">**bin** — binarne</span><span class="sxs-lookup"><span data-stu-id="e97e0-110">**bin** – Binary</span></span>
* <span data-ttu-id="e97e0-111">**wartość logiczna** — wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="e97e0-111">**bool** – Boolean</span></span>
* <span data-ttu-id="e97e0-112">**DT** — UTC daty/godziny</span><span class="sxs-lookup"><span data-stu-id="e97e0-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="e97e0-113">**wyliczenia** — wyliczenie znanych — stałe</span><span class="sxs-lookup"><span data-stu-id="e97e0-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="e97e0-114">**EXP** — wyrażenie, które jest oczekiwany tooa tooevaluate wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="e97e0-114">**exp** – Expression, which is expected tooevaluate tooa Boolean</span></span>
* <span data-ttu-id="e97e0-115">**mvbin** — binarnego z wieloma wartościami</span><span class="sxs-lookup"><span data-stu-id="e97e0-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="e97e0-116">**mvstr** — ciąg z wieloma wartościami</span><span class="sxs-lookup"><span data-stu-id="e97e0-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="e97e0-117">**mvref** — odwołanie z wieloma wartościami</span><span class="sxs-lookup"><span data-stu-id="e97e0-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="e97e0-118">**num** — numeryczne</span><span class="sxs-lookup"><span data-stu-id="e97e0-118">**num** – Numeric</span></span>
* <span data-ttu-id="e97e0-119">**REF** — odwołanie</span><span class="sxs-lookup"><span data-stu-id="e97e0-119">**ref** – Reference</span></span>
* <span data-ttu-id="e97e0-120">**str** — ciąg</span><span class="sxs-lookup"><span data-stu-id="e97e0-120">**str** – String</span></span>
* <span data-ttu-id="e97e0-121">**var** — wariant (prawie) żadnego innego typu</span><span class="sxs-lookup"><span data-stu-id="e97e0-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="e97e0-122">**void** — nie zwraca wartości</span><span class="sxs-lookup"><span data-stu-id="e97e0-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="e97e0-123">Witaj funkcji z typami hello **mvbin**, **mvstr**, i **mvref** może pracować tylko na atrybuty wielowartościowe.</span><span class="sxs-lookup"><span data-stu-id="e97e0-123">hello functions with hello types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="e97e0-124">Funkcje z **bin**, **str**, i **ref** pracować nad atrybuty zarówno jedno- i wielowartościowych.</span><span class="sxs-lookup"><span data-stu-id="e97e0-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="e97e0-125">Informacje ogólne o funkcjach</span><span class="sxs-lookup"><span data-stu-id="e97e0-125">Functions Reference</span></span>
| <span data-ttu-id="e97e0-126">Lista funkcji</span><span class="sxs-lookup"><span data-stu-id="e97e0-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="e97e0-127">**Certyfikat**</span><span class="sxs-lookup"><span data-stu-id="e97e0-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="e97e0-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="e97e0-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="e97e0-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="e97e0-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="e97e0-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="e97e0-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="e97e0-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="e97e0-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="e97e0-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="e97e0-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="e97e0-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="e97e0-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="e97e0-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="e97e0-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="e97e0-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="e97e0-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="e97e0-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="e97e0-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="e97e0-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="e97e0-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="e97e0-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="e97e0-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="e97e0-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="e97e0-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="e97e0-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="e97e0-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="e97e0-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="e97e0-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="e97e0-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="e97e0-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="e97e0-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="e97e0-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="e97e0-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="e97e0-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="e97e0-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="e97e0-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="e97e0-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="e97e0-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="e97e0-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="e97e0-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="e97e0-148">CertVersion</span><span class="sxs-lookup"><span data-stu-id="e97e0-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="e97e0-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="e97e0-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="e97e0-150">**Konwersja**</span><span class="sxs-lookup"><span data-stu-id="e97e0-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="e97e0-151">CBool</span><span class="sxs-lookup"><span data-stu-id="e97e0-151">CBool</span></span>](#cbool) |[<span data-ttu-id="e97e0-152">CDate</span><span class="sxs-lookup"><span data-stu-id="e97e0-152">CDate</span></span>](#cdate) |[<span data-ttu-id="e97e0-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="e97e0-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="e97e0-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="e97e0-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="e97e0-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="e97e0-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="e97e0-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="e97e0-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="e97e0-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="e97e0-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="e97e0-158">CNum</span><span class="sxs-lookup"><span data-stu-id="e97e0-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="e97e0-159">CRef</span><span class="sxs-lookup"><span data-stu-id="e97e0-159">CRef</span></span>](#cref) |[<span data-ttu-id="e97e0-160">CStr</span><span class="sxs-lookup"><span data-stu-id="e97e0-160">CStr</span></span>](#cstr) |[<span data-ttu-id="e97e0-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="e97e0-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="e97e0-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="e97e0-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="e97e0-163">**Data i godzina**</span><span class="sxs-lookup"><span data-stu-id="e97e0-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="e97e0-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="e97e0-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="e97e0-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="e97e0-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="e97e0-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="e97e0-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="e97e0-167">Teraz</span><span class="sxs-lookup"><span data-stu-id="e97e0-167">Now</span></span>](#now) | |
| [<span data-ttu-id="e97e0-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="e97e0-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="e97e0-169">**Katalog**</span><span class="sxs-lookup"><span data-stu-id="e97e0-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="e97e0-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="e97e0-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="e97e0-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="e97e0-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="e97e0-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="e97e0-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="e97e0-173">**Ocena**</span><span class="sxs-lookup"><span data-stu-id="e97e0-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="e97e0-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="e97e0-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="e97e0-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="e97e0-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="e97e0-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="e97e0-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="e97e0-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="e97e0-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="e97e0-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="e97e0-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="e97e0-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="e97e0-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="e97e0-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="e97e0-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="e97e0-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="e97e0-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="e97e0-182">IsString</span><span class="sxs-lookup"><span data-stu-id="e97e0-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="e97e0-183">**Matematyczne**</span><span class="sxs-lookup"><span data-stu-id="e97e0-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="e97e0-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="e97e0-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="e97e0-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="e97e0-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="e97e0-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="e97e0-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="e97e0-187">**Wielowartościowe**</span><span class="sxs-lookup"><span data-stu-id="e97e0-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="e97e0-188">Zawiera</span><span class="sxs-lookup"><span data-stu-id="e97e0-188">Contains</span></span>](#contains) |[<span data-ttu-id="e97e0-189">Liczba</span><span class="sxs-lookup"><span data-stu-id="e97e0-189">Count</span></span>](#count) |[<span data-ttu-id="e97e0-190">Element</span><span class="sxs-lookup"><span data-stu-id="e97e0-190">Item</span></span>](#item) |[<span data-ttu-id="e97e0-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="e97e0-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="e97e0-192">Dołącz</span><span class="sxs-lookup"><span data-stu-id="e97e0-192">Join</span></span>](#join) |[<span data-ttu-id="e97e0-193">Removeduplicates —</span><span class="sxs-lookup"><span data-stu-id="e97e0-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="e97e0-194">Podziel</span><span class="sxs-lookup"><span data-stu-id="e97e0-194">Split</span></span>](#split) | | |
| <span data-ttu-id="e97e0-195">**Przepływ programu**</span><span class="sxs-lookup"><span data-stu-id="e97e0-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="e97e0-196">Błąd</span><span class="sxs-lookup"><span data-stu-id="e97e0-196">Error</span></span>](#error) |[<span data-ttu-id="e97e0-197">IIF</span><span class="sxs-lookup"><span data-stu-id="e97e0-197">IIF</span></span>](#iif) |[<span data-ttu-id="e97e0-198">Wybierz</span><span class="sxs-lookup"><span data-stu-id="e97e0-198">Select</span></span>](#select) |[<span data-ttu-id="e97e0-199">Przełącznik</span><span class="sxs-lookup"><span data-stu-id="e97e0-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="e97e0-200">Gdzie</span><span class="sxs-lookup"><span data-stu-id="e97e0-200">Where</span></span>](#where) |[<span data-ttu-id="e97e0-201">Z</span><span class="sxs-lookup"><span data-stu-id="e97e0-201">With</span></span>](#with) | | | |
| <span data-ttu-id="e97e0-202">**Tekst**</span><span class="sxs-lookup"><span data-stu-id="e97e0-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="e97e0-203">IDENTYFIKATOR GUID</span><span class="sxs-lookup"><span data-stu-id="e97e0-203">GUID</span></span>](#guid) |[<span data-ttu-id="e97e0-204">InStr</span><span class="sxs-lookup"><span data-stu-id="e97e0-204">InStr</span></span>](#instr) |[<span data-ttu-id="e97e0-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="e97e0-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="e97e0-206">LCase</span><span class="sxs-lookup"><span data-stu-id="e97e0-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="e97e0-207">Po lewej</span><span class="sxs-lookup"><span data-stu-id="e97e0-207">Left</span></span>](#left) |[<span data-ttu-id="e97e0-208">Długość</span><span class="sxs-lookup"><span data-stu-id="e97e0-208">Len</span></span>](#len) |[<span data-ttu-id="e97e0-209">Przytp</span><span class="sxs-lookup"><span data-stu-id="e97e0-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="e97e0-210">MID</span><span class="sxs-lookup"><span data-stu-id="e97e0-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="e97e0-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="e97e0-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="e97e0-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="e97e0-212">PadRight</span></span>](#padright) |[<span data-ttu-id="e97e0-213">PCase</span><span class="sxs-lookup"><span data-stu-id="e97e0-213">PCase</span></span>](#pcase) |[<span data-ttu-id="e97e0-214">Zamień</span><span class="sxs-lookup"><span data-stu-id="e97e0-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="e97e0-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="e97e0-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="e97e0-216">Prawo</span><span class="sxs-lookup"><span data-stu-id="e97e0-216">Right</span></span>](#right) |[<span data-ttu-id="e97e0-217">Przytk</span><span class="sxs-lookup"><span data-stu-id="e97e0-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="e97e0-218">TRIM</span><span class="sxs-lookup"><span data-stu-id="e97e0-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="e97e0-219">UCase</span><span class="sxs-lookup"><span data-stu-id="e97e0-219">UCase</span></span>](#ucase) |[<span data-ttu-id="e97e0-220">Word</span><span class="sxs-lookup"><span data-stu-id="e97e0-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="e97e0-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="e97e0-221">BitAnd</span></span>
<span data-ttu-id="e97e0-222">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-222">**Description:**</span></span>  
<span data-ttu-id="e97e0-223">Hello BitAnd — funkcja ustawia bitów określonej wartości.</span><span class="sxs-lookup"><span data-stu-id="e97e0-223">hello BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="e97e0-224">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="e97e0-225">Wartość1, wartość2: wartości liczbowe, które powinny być tematyczne razem</span><span class="sxs-lookup"><span data-stu-id="e97e0-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="e97e0-226">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-226">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-227">Ta funkcja konwertuje obu parametrów toohello binarna reprezentacja i ustawia bit:</span><span class="sxs-lookup"><span data-stu-id="e97e0-227">This function converts both parameters toohello binary representation and sets a bit to:</span></span>

* <span data-ttu-id="e97e0-228">0 — Jeśli jedno lub oba hello odpowiednich bitów w *maski* i *flagi* 0</span><span class="sxs-lookup"><span data-stu-id="e97e0-228">0 - if one or both of hello corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="e97e0-229">1 — Jeśli odpowiednich bitów hello są 1.</span><span class="sxs-lookup"><span data-stu-id="e97e0-229">1 - if both of hello corresponding bits are 1.</span></span>

<span data-ttu-id="e97e0-230">Innymi słowy zwraca 0 we wszystkich przypadkach, z wyjątkiem przypadków, gdy hello odpowiednich bitów oba parametry są 1.</span><span class="sxs-lookup"><span data-stu-id="e97e0-230">In other words, it returns 0 in all cases except when hello corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="e97e0-231">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="e97e0-232">Zwraca 7, ponieważ szesnastkowy "F" i "F7" zwrócić wartość toothis.</span><span class="sxs-lookup"><span data-stu-id="e97e0-232">Returns 7 because hexadecimal "F" AND "F7" evaluate toothis value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="e97e0-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="e97e0-233">BitOr</span></span>
<span data-ttu-id="e97e0-234">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-234">**Description:**</span></span>  
<span data-ttu-id="e97e0-235">Hello BitOr — funkcja ustawia bitów określonej wartości.</span><span class="sxs-lookup"><span data-stu-id="e97e0-235">hello BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="e97e0-236">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="e97e0-237">Wartość1, wartość2: wartości liczbowe, które powinny być zsumować logicznie razem</span><span class="sxs-lookup"><span data-stu-id="e97e0-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="e97e0-238">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-238">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-239">Ta funkcja konwertuje obu parametrów toohello binarna reprezentacja i ustawia bit too1, jeśli jeden lub oba hello odpowiednie bity maski i flagi 1 i too0 gdy odpowiednich bitów hello są 0.</span><span class="sxs-lookup"><span data-stu-id="e97e0-239">This function converts both parameters toohello binary representation and sets a bit too1 if one or both of hello corresponding bits in mask and flag are 1, and too0 if both of hello corresponding bits are 0.</span></span> <span data-ttu-id="e97e0-240">Innymi słowy zwraca 1 we wszystkich przypadkach, z wyjątkiem przypadków, w którym hello odpowiednich bitów oba parametry są równe 0.</span><span class="sxs-lookup"><span data-stu-id="e97e0-240">In other words, it returns 1 in all cases except where hello corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="e97e0-241">CBool</span><span class="sxs-lookup"><span data-stu-id="e97e0-241">CBool</span></span>
<span data-ttu-id="e97e0-242">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-242">**Description:**</span></span>  
<span data-ttu-id="e97e0-243">Witaj CBool-funkcja zwraca wartość logiczną na podstawie na powitania obliczone wyrażenie</span><span class="sxs-lookup"><span data-stu-id="e97e0-243">hello CBool function returns a Boolean based on hello evaluated expression</span></span>

<span data-ttu-id="e97e0-244">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="e97e0-245">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-245">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-246">Jeśli hello wyrażenie tooa wartość niezerową, a następnie CBool zwraca wartość PRAWDA, przeciwnym razie zwraca wartość False.</span><span class="sxs-lookup"><span data-stu-id="e97e0-246">If hello expression evaluates tooa nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="e97e0-247">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="e97e0-248">Zwraca wartość True, jeśli oba atrybuty mają hello tę samą wartość.</span><span class="sxs-lookup"><span data-stu-id="e97e0-248">Returns True if both attributes have hello same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="e97e0-249">CDate</span><span class="sxs-lookup"><span data-stu-id="e97e0-249">CDate</span></span>
<span data-ttu-id="e97e0-250">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-250">**Description:**</span></span>  
<span data-ttu-id="e97e0-251">Witaj CDate-funkcja zwraca wartość typu DateTime UTC z ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-251">hello CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="e97e0-252">Data i godzina nie jest typem atrybutu natywnego zsynchronizowane, ale jest używany przez niektóre funkcje.</span><span class="sxs-lookup"><span data-stu-id="e97e0-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="e97e0-253">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="e97e0-254">Wartość: Ciąg daty, godziny i opcjonalnie strefy czasowej</span><span class="sxs-lookup"><span data-stu-id="e97e0-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="e97e0-255">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-255">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-256">Witaj zwrócony ciąg jest zawsze w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="e97e0-256">hello returned string is always in UTC.</span></span>

<span data-ttu-id="e97e0-257">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="e97e0-258">Zwraca wartość typu DateTime na podstawie czasu rozpoczęcia hello pracownika</span><span class="sxs-lookup"><span data-stu-id="e97e0-258">Returns a DateTime based on hello employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="e97e0-259">Zwraca daty/godziny reprezentująca "2013-01-11: 00:00:00"</span><span class="sxs-lookup"><span data-stu-id="e97e0-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="e97e0-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="e97e0-260">CertExtensionOids</span></span>
<span data-ttu-id="e97e0-261">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-261">**Description:**</span></span>  
<span data-ttu-id="e97e0-262">Zwraca hello wartości identyfikatora Oid wszystkie rozszerzenia krytyczne hello obiektu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-262">Returns hello Oid values of all hello critical extensions of a certificate object.</span></span>

<span data-ttu-id="e97e0-263">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-264">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-265">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-265">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="e97e0-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="e97e0-266">CertFormat</span></span>
<span data-ttu-id="e97e0-267">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-267">**Description:**</span></span>  
<span data-ttu-id="e97e0-268">Zwraca hello nazwę formatu hello tego certyfikatu X.509v3.</span><span class="sxs-lookup"><span data-stu-id="e97e0-268">Returns hello name of hello format of this X.509v3 certificate.</span></span>

<span data-ttu-id="e97e0-269">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-270">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-271">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-271">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="e97e0-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="e97e0-272">CertFriendlyName</span></span>
<span data-ttu-id="e97e0-273">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-273">**Description:**</span></span>  
<span data-ttu-id="e97e0-274">Zwraca hello skojarzony aliasu dla certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-274">Returns hello associated alias for a certificate.</span></span>

<span data-ttu-id="e97e0-275">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-276">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-277">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-277">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="e97e0-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="e97e0-278">CertHashString</span></span>
<span data-ttu-id="e97e0-279">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-279">**Description:**</span></span>  
<span data-ttu-id="e97e0-280">Zwraca hello wartość skrótu SHA1 certyfikatu X.509v3 hello jako ciąg szesnastkowy.</span><span class="sxs-lookup"><span data-stu-id="e97e0-280">Returns hello SHA1 hash value for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="e97e0-281">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-282">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-283">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-283">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="e97e0-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="e97e0-284">CertIssuer</span></span>
<span data-ttu-id="e97e0-285">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-285">**Description:**</span></span>  
<span data-ttu-id="e97e0-286">Zwraca hello nazwa hello urzędu certyfikacji, który wystawił certyfikat X.509v3 hello.</span><span class="sxs-lookup"><span data-stu-id="e97e0-286">Returns hello name of hello certificate authority that issued hello X.509v3 certificate.</span></span>

<span data-ttu-id="e97e0-287">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-288">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-289">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-289">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="e97e0-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="e97e0-290">CertIssuerDN</span></span>
<span data-ttu-id="e97e0-291">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-291">**Description:**</span></span>  
<span data-ttu-id="e97e0-292">Zwraca hello nazwa wyróżniająca wystawcy certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="e97e0-292">Returns hello distinguished name of hello certificate issuer.</span></span>

<span data-ttu-id="e97e0-293">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-294">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-295">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-295">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="e97e0-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="e97e0-296">CertIssuerOid</span></span>
<span data-ttu-id="e97e0-297">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-297">**Description:**</span></span>  
<span data-ttu-id="e97e0-298">Zwraca hello Oid Witaj wystawca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-298">Returns hello Oid of hello certificate issuer.</span></span>

<span data-ttu-id="e97e0-299">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-300">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-301">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-301">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="e97e0-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="e97e0-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="e97e0-303">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-303">**Description:**</span></span>  
<span data-ttu-id="e97e0-304">Zwraca hello algorytm klucza informacje dotyczące tego certyfikatu X.509v3 jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="e97e0-304">Returns hello key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="e97e0-305">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-306">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-307">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-307">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="e97e0-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="e97e0-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="e97e0-309">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-309">**Description:**</span></span>  
<span data-ttu-id="e97e0-310">Zwraca parametry hello algorytm klucza certyfikatu X.509v3 hello jako ciąg szesnastkowy.</span><span class="sxs-lookup"><span data-stu-id="e97e0-310">Returns hello key algorithm parameters for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="e97e0-311">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-312">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-313">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-313">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="e97e0-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="e97e0-314">CertNameInfo</span></span>
<span data-ttu-id="e97e0-315">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-315">**Description:**</span></span>  
<span data-ttu-id="e97e0-316">Zwraca hello podmiot i Wystawca nazwy z certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-316">Returns hello subject and issuer names from a certificate.</span></span>

<span data-ttu-id="e97e0-317">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="e97e0-318">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-319">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-319">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="e97e0-320">X509NameType: Witaj wartość X509NameType hello tematu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-320">X509NameType: hello X509NameType value for hello subject.</span></span>
*   <span data-ttu-id="e97e0-321">includesIssuerName: Nazwa wystawcy hello true tooinclude; w przeciwnym razie wartość false.</span><span class="sxs-lookup"><span data-stu-id="e97e0-321">includesIssuerName: true tooinclude hello issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="e97e0-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="e97e0-322">CertNotAfter</span></span>
<span data-ttu-id="e97e0-323">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-323">**Description:**</span></span>  
<span data-ttu-id="e97e0-324">Zwraca datę hello według czasu lokalnego, po której certyfikat nie jest już prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="e97e0-324">Returns hello date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="e97e0-325">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-326">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-327">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-327">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="e97e0-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="e97e0-328">CertNotBefore</span></span>
<span data-ttu-id="e97e0-329">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-329">**Description:**</span></span>  
<span data-ttu-id="e97e0-330">Zwraca datę hello według czasu lokalnego, od której zaczyna obowiązywać certyfikat.</span><span class="sxs-lookup"><span data-stu-id="e97e0-330">Returns hello date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="e97e0-331">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-332">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-333">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-333">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="e97e0-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="e97e0-334">CertPublicKeyOid</span></span>
<span data-ttu-id="e97e0-335">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-335">**Description:**</span></span>  
<span data-ttu-id="e97e0-336">Zwraca hello Oid hello klucz publiczny certyfikatu X.509v3 hello.</span><span class="sxs-lookup"><span data-stu-id="e97e0-336">Returns hello Oid of hello public key for hello X.509v3 certificate.</span></span>

<span data-ttu-id="e97e0-337">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-338">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-339">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-339">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="e97e0-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="e97e0-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="e97e0-341">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-341">**Description:**</span></span>  
<span data-ttu-id="e97e0-342">Zwraca hello Oid hello parametrów klucza publicznego certyfikatu X.509v3 hello.</span><span class="sxs-lookup"><span data-stu-id="e97e0-342">Returns hello Oid of hello public key parameters for hello X.509v3 certificate.</span></span>

<span data-ttu-id="e97e0-343">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-344">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-345">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-345">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="e97e0-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="e97e0-346">CertSerialNumber</span></span>
<span data-ttu-id="e97e0-347">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-347">**Description:**</span></span>  
<span data-ttu-id="e97e0-348">Zwraca numer seryjny certyfikatu X.509v3 hello hello.</span><span class="sxs-lookup"><span data-stu-id="e97e0-348">Returns hello serial number of hello X.509v3 certificate.</span></span>

<span data-ttu-id="e97e0-349">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-350">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-351">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-351">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="e97e0-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="e97e0-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="e97e0-353">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-353">**Description:**</span></span>  
<span data-ttu-id="e97e0-354">Zwraca hello Oid hello algorytm używany toocreate hello podpisu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-354">Returns hello Oid of hello algorithm used toocreate hello signature of a certificate.</span></span>

<span data-ttu-id="e97e0-355">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-356">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-357">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-357">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="e97e0-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="e97e0-358">CertSubject</span></span>
<span data-ttu-id="e97e0-359">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-359">**Description:**</span></span>  
<span data-ttu-id="e97e0-360">Pobiera hello nazwa wyróżniająca podmiotu z certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-360">Gets hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="e97e0-361">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-362">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-363">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-363">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="e97e0-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="e97e0-364">CertSubjectNameDN</span></span>
<span data-ttu-id="e97e0-365">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-365">**Description:**</span></span>  
<span data-ttu-id="e97e0-366">Zwraca hello nazwa wyróżniająca podmiotu z certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-366">Returns hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="e97e0-367">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-368">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-369">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-369">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="e97e0-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="e97e0-370">CertSubjectNameOid</span></span>
<span data-ttu-id="e97e0-371">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-371">**Description:**</span></span>  
<span data-ttu-id="e97e0-372">Zwraca hello Oid hello nazwa podmiotu z certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-372">Returns hello Oid of hello subject name from a certificate.</span></span>

<span data-ttu-id="e97e0-373">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-374">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-375">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-375">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="e97e0-376">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="e97e0-376">CertThumbprint</span></span>
<span data-ttu-id="e97e0-377">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-377">**Description:**</span></span>  
<span data-ttu-id="e97e0-378">Zwraca hello odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-378">Returns hello thumbprint of a certificate.</span></span>

<span data-ttu-id="e97e0-379">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-380">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-381">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-381">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="e97e0-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="e97e0-382">CertVersion</span></span>
<span data-ttu-id="e97e0-383">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-383">**Description:**</span></span>  
<span data-ttu-id="e97e0-384">Zwraca hello wersja formatu X.509 certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-384">Returns hello X.509 format version of a certificate.</span></span>

<span data-ttu-id="e97e0-385">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-386">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-387">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-387">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="e97e0-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="e97e0-388">CGuid</span></span>
<span data-ttu-id="e97e0-389">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-389">**Description:**</span></span>  
<span data-ttu-id="e97e0-390">Hello funkcja CGuid konwertuje reprezentacja ciągu hello binarna reprezentacja tooits identyfikatora GUID.</span><span class="sxs-lookup"><span data-stu-id="e97e0-390">hello CGuid function converts hello string representation of a GUID tooits binary representation.</span></span>

<span data-ttu-id="e97e0-391">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="e97e0-392">Ciąg sformatowany w tym wzorcu: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx lub {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="e97e0-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="e97e0-393">Contains</span><span class="sxs-lookup"><span data-stu-id="e97e0-393">Contains</span></span>
<span data-ttu-id="e97e0-394">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-394">**Description:**</span></span>  
<span data-ttu-id="e97e0-395">funkcja zawiera Hello znajduje się ciąg wewnątrz atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="e97e0-395">hello Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="e97e0-396">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-396">**Syntax:**</span></span>  
<span data-ttu-id="e97e0-397">`num Contains (mvstring attribute, str search)`-uwzględniana wielkość liter</span><span class="sxs-lookup"><span data-stu-id="e97e0-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="e97e0-398">`num Contains (mvref attribute, str search)`-uwzględniana wielkość liter</span><span class="sxs-lookup"><span data-stu-id="e97e0-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="e97e0-399">Atrybut: hello toosearch atrybutów wielowartościowych.</span><span class="sxs-lookup"><span data-stu-id="e97e0-399">attribute: hello multi-valued attribute toosearch.</span></span>
* <span data-ttu-id="e97e0-400">wyszukiwania: string toofind w atrybucie hello.</span><span class="sxs-lookup"><span data-stu-id="e97e0-400">search: string toofind in hello attribute.</span></span>
* <span data-ttu-id="e97e0-401">Casetype: CaseInsensitive lub CaseSensitive w tabeli.</span><span class="sxs-lookup"><span data-stu-id="e97e0-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="e97e0-402">Zwraca indeks atrybutu wielowartościowego hello, w którym zostało znalezione ciąg hello.</span><span class="sxs-lookup"><span data-stu-id="e97e0-402">Returns index in hello multi-valued attribute where hello string was found.</span></span> <span data-ttu-id="e97e0-403">Jeśli nie zostanie znaleziony ciąg hello zwracane jest 0.</span><span class="sxs-lookup"><span data-stu-id="e97e0-403">0 is returned if hello string is not found.</span></span>

<span data-ttu-id="e97e0-404">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-404">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-405">Dla atrybutów wielowartościowych ciąg wyszukiwania hello znajduje podciągów hello wartości.</span><span class="sxs-lookup"><span data-stu-id="e97e0-405">For multi-valued string attributes, hello search finds substrings in hello values.</span></span>  
<span data-ttu-id="e97e0-406">Dla atrybutów odwołania hello przeszukane ciąg musi dokładnie odpowiadać toobe wartość hello uznane za pasujące.</span><span class="sxs-lookup"><span data-stu-id="e97e0-406">For reference attributes, hello searched string must exactly match hello value toobe considered a match.</span></span>

<span data-ttu-id="e97e0-407">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="e97e0-408">Jeśli atrybut proxyAddresses hello ma podstawowego adresu e-mail (wskazywanym przez wielkimi literami "SMTP:"), zwracany jest atrybut proxyAddress hello, przeciwnym razie zwraca błąd.</span><span class="sxs-lookup"><span data-stu-id="e97e0-408">If hello proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return hello proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="e97e0-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="e97e0-409">ConvertFromBase64</span></span>
<span data-ttu-id="e97e0-410">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-410">**Description:**</span></span>  
<span data-ttu-id="e97e0-411">Witaj ConvertFromBase64 funkcja konwertuje Witaj określony ciągu w kodowaniu base64 wartość tooa regularne.</span><span class="sxs-lookup"><span data-stu-id="e97e0-411">hello ConvertFromBase64 function converts hello specified base64 encoded value tooa regular string.</span></span>

<span data-ttu-id="e97e0-412">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-412">**Syntax:**</span></span>  
<span data-ttu-id="e97e0-413">`str ConvertFromBase64(str source)`-zakłada do kodowania Unicode</span><span class="sxs-lookup"><span data-stu-id="e97e0-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="e97e0-414">Źródło: ciąg kodowany w formacie Base64</span><span class="sxs-lookup"><span data-stu-id="e97e0-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="e97e0-415">Kodowanie: UTF8 Unicode i ASCII,</span><span class="sxs-lookup"><span data-stu-id="e97e0-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="e97e0-416">**Przykład**</span><span class="sxs-lookup"><span data-stu-id="e97e0-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="e97e0-417">Zwraca zarówno przykłady "*Witaj świecie!*"</span><span class="sxs-lookup"><span data-stu-id="e97e0-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="e97e0-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="e97e0-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="e97e0-419">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-419">**Description:**</span></span>  
<span data-ttu-id="e97e0-420">Hello ConvertFromUTF8Hex funkcja konwertuje hello określony ciąg tooa wartości Hex UTF8 zakodowany.</span><span class="sxs-lookup"><span data-stu-id="e97e0-420">hello ConvertFromUTF8Hex function converts hello specified UTF8 Hex encoded value tooa string.</span></span>

<span data-ttu-id="e97e0-421">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="e97e0-422">Źródło: ciągu zakodowanego 2-bajtowych UTF8</span><span class="sxs-lookup"><span data-stu-id="e97e0-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="e97e0-423">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-423">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-424">Witaj różnica w tej funkcji i ConvertFromBase64([],UTF8) w wyniku tego hello jest przyjazną dla atrybutu Nazwa Wyróżniająca hello.</span><span class="sxs-lookup"><span data-stu-id="e97e0-424">hello difference between this function and ConvertFromBase64([],UTF8) in that hello result is friendly for hello DN attribute.</span></span>  
<span data-ttu-id="e97e0-425">Ten format jest używany przez usługę Azure Active Directory jako nazwa Wyróżniająca.</span><span class="sxs-lookup"><span data-stu-id="e97e0-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="e97e0-426">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="e97e0-427">Zwraca "*Witaj świecie!*"</span><span class="sxs-lookup"><span data-stu-id="e97e0-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="e97e0-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="e97e0-428">ConvertToBase64</span></span>
<span data-ttu-id="e97e0-429">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-429">**Description:**</span></span>  
<span data-ttu-id="e97e0-430">Funkcja ConvertToBase64 Hello konwertuje tooa ciąg Unicode ciąg base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-430">hello ConvertToBase64 function converts a string tooa Unicode base64 string.</span></span>  
<span data-ttu-id="e97e0-431">Konwertuje wartość hello tablicy liczb całkowitych tooits równoważne reprezentację zakodowany z cyframi base-64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-431">Converts hello value of an array of integers tooits equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="e97e0-432">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="e97e0-433">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="e97e0-434">Zwraca "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span><span class="sxs-lookup"><span data-stu-id="e97e0-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="e97e0-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="e97e0-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="e97e0-436">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-436">**Description:**</span></span>  
<span data-ttu-id="e97e0-437">Funkcja ConvertToUTF8Hex Hello konwertuje tooa ciąg szesnastkowy UTF8 zakodowanych wartości.</span><span class="sxs-lookup"><span data-stu-id="e97e0-437">hello ConvertToUTF8Hex function converts a string tooa UTF8 Hex encoded value.</span></span>

<span data-ttu-id="e97e0-438">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="e97e0-439">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-439">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-440">format danych wyjściowych Hello tej funkcji jest używany przez usługę Azure Active Directory jako nazwa Wyróżniająca atrybutu format.</span><span class="sxs-lookup"><span data-stu-id="e97e0-440">hello output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="e97e0-441">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="e97e0-442">Zwraca 48656C6C6F20776F726C6421</span><span class="sxs-lookup"><span data-stu-id="e97e0-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="e97e0-443">Licznik</span><span class="sxs-lookup"><span data-stu-id="e97e0-443">Count</span></span>
<span data-ttu-id="e97e0-444">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-444">**Description:**</span></span>  
<span data-ttu-id="e97e0-445">Hello funkcji Count zwraca hello liczbę elementów w atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="e97e0-445">hello Count function returns hello number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="e97e0-446">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="e97e0-447">CNum</span><span class="sxs-lookup"><span data-stu-id="e97e0-447">CNum</span></span>
<span data-ttu-id="e97e0-448">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-448">**Description:**</span></span>  
<span data-ttu-id="e97e0-449">Hello funkcja CNum ciąg znaków i zwraca dane typu liczbowego.</span><span class="sxs-lookup"><span data-stu-id="e97e0-449">hello CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="e97e0-450">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="e97e0-451">CRef</span><span class="sxs-lookup"><span data-stu-id="e97e0-451">CRef</span></span>
<span data-ttu-id="e97e0-452">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-452">**Description:**</span></span>  
<span data-ttu-id="e97e0-453">Konwertuje ciąg tooa atrybut odwołania</span><span class="sxs-lookup"><span data-stu-id="e97e0-453">Converts a string tooa reference attribute</span></span>

<span data-ttu-id="e97e0-454">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="e97e0-455">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="e97e0-456">CStr</span><span class="sxs-lookup"><span data-stu-id="e97e0-456">CStr</span></span>
<span data-ttu-id="e97e0-457">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-457">**Description:**</span></span>  
<span data-ttu-id="e97e0-458">Witaj przez funkcję CStr konwertuje tooa string — typ danych.</span><span class="sxs-lookup"><span data-stu-id="e97e0-458">hello CStr function converts tooa string data type.</span></span>

<span data-ttu-id="e97e0-459">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="e97e0-460">wartość: może być liczbą, atrybut odwołania lub typu Boolean.</span><span class="sxs-lookup"><span data-stu-id="e97e0-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="e97e0-461">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="e97e0-462">Może zwrócić "cn = Jan, dc = contoso, dc = com"</span><span class="sxs-lookup"><span data-stu-id="e97e0-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="e97e0-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="e97e0-463">DateAdd</span></span>
<span data-ttu-id="e97e0-464">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-464">**Description:**</span></span>  
<span data-ttu-id="e97e0-465">Zwraca wartość typu Date zawierającą toowhich Data, w określonym przedziale czasu został dodany.</span><span class="sxs-lookup"><span data-stu-id="e97e0-465">Returns a Date containing a date toowhich a specified time interval has been added.</span></span>

<span data-ttu-id="e97e0-466">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="e97e0-467">Interwał: ciąg hello interwał czasu tooadd wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="e97e0-467">interval: String expression that is hello interval of time you want tooadd.</span></span> <span data-ttu-id="e97e0-468">ciąg Hello musi mieć jeden z hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="e97e0-468">hello string must have one of hello following values:</span></span>
  * <span data-ttu-id="e97e0-469">rrrr roku</span><span class="sxs-lookup"><span data-stu-id="e97e0-469">yyyy Year</span></span>
  * <span data-ttu-id="e97e0-470">q kwartału</span><span class="sxs-lookup"><span data-stu-id="e97e0-470">q Quarter</span></span>
  * <span data-ttu-id="e97e0-471">m miesiąc</span><span class="sxs-lookup"><span data-stu-id="e97e0-471">m Month</span></span>
  * <span data-ttu-id="e97e0-472">y dzień roku</span><span class="sxs-lookup"><span data-stu-id="e97e0-472">y Day of year</span></span>
  * <span data-ttu-id="e97e0-473">d dzień</span><span class="sxs-lookup"><span data-stu-id="e97e0-473">d Day</span></span>
  * <span data-ttu-id="e97e0-474">w dzień tygodnia</span><span class="sxs-lookup"><span data-stu-id="e97e0-474">w Weekday</span></span>
  * <span data-ttu-id="e97e0-475">TT tygodnia</span><span class="sxs-lookup"><span data-stu-id="e97e0-475">ww Week</span></span>
  * <span data-ttu-id="e97e0-476">h Godzina</span><span class="sxs-lookup"><span data-stu-id="e97e0-476">h Hour</span></span>
  * <span data-ttu-id="e97e0-477">n minutę</span><span class="sxs-lookup"><span data-stu-id="e97e0-477">n Minute</span></span>
  * <span data-ttu-id="e97e0-478">s drugi</span><span class="sxs-lookup"><span data-stu-id="e97e0-478">s Second</span></span>
* <span data-ttu-id="e97e0-479">wartość: hello liczbę jednostek ma tooadd.</span><span class="sxs-lookup"><span data-stu-id="e97e0-479">value: hello number of units you want tooadd.</span></span> <span data-ttu-id="e97e0-480">Mogą być dodatnie (tooget daty w przyszłości hello) lub wartość ujemną (tooget daty w przeszłości hello).</span><span class="sxs-lookup"><span data-stu-id="e97e0-480">It can be positive (tooget dates in hello future) or negative (tooget dates in hello past).</span></span>
* <span data-ttu-id="e97e0-481">Data: daty/godziny reprezentująca toowhich interwale hello jest dodawany.</span><span class="sxs-lookup"><span data-stu-id="e97e0-481">date: DateTime representing date toowhich hello interval is added.</span></span>

<span data-ttu-id="e97e0-482">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="e97e0-483">Dodaje 3 miesiące i zwraca wartość typu DateTime reprezentujący "2001-04-01".</span><span class="sxs-lookup"><span data-stu-id="e97e0-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="e97e0-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="e97e0-484">DateFromNum</span></span>
<span data-ttu-id="e97e0-485">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-485">**Description:**</span></span>  
<span data-ttu-id="e97e0-486">Funkcja DateFromNum Hello konwertuje wartość w tooa format daty Directory typu Data/Godzina.</span><span class="sxs-lookup"><span data-stu-id="e97e0-486">hello DateFromNum function converts a value in AD’s date format tooa DateTime type.</span></span>

<span data-ttu-id="e97e0-487">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="e97e0-488">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="e97e0-489">Zwraca wartość typu DateTime reprezentujący 2012-01-01-23:00:00</span><span class="sxs-lookup"><span data-stu-id="e97e0-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="e97e0-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="e97e0-490">DNComponent</span></span>
<span data-ttu-id="e97e0-491">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-491">**Description:**</span></span>  
<span data-ttu-id="e97e0-492">Hello DNComponent funkcja zwraca wartość hello określonego składnika DN z lewej strony.</span><span class="sxs-lookup"><span data-stu-id="e97e0-492">hello DNComponent function returns hello value of a specified DN component going from left.</span></span>

<span data-ttu-id="e97e0-493">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="e97e0-494">Nazwa wyróżniająca: hello odwołanie do atrybutu toointerpret</span><span class="sxs-lookup"><span data-stu-id="e97e0-494">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="e97e0-495">ComponentNumber: składnik hello tooreturn hello nazwa Wyróżniająca</span><span class="sxs-lookup"><span data-stu-id="e97e0-495">ComponentNumber: hello component in hello DN tooreturn</span></span>

<span data-ttu-id="e97e0-496">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="e97e0-497">Jeśli nazwa wyróżniająca "cn = Jan, ou =..." zwraca Jan</span><span class="sxs-lookup"><span data-stu-id="e97e0-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="e97e0-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="e97e0-498">DNComponentRev</span></span>
<span data-ttu-id="e97e0-499">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-499">**Description:**</span></span>  
<span data-ttu-id="e97e0-500">Witaj DNComponentRev funkcja zwraca wartość hello określonego składnika DN z prawej strony (hello end).</span><span class="sxs-lookup"><span data-stu-id="e97e0-500">hello DNComponentRev function returns hello value of a specified DN component going from right (hello end).</span></span>

<span data-ttu-id="e97e0-501">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="e97e0-502">Nazwa wyróżniająca: hello odwołanie do atrybutu toointerpret</span><span class="sxs-lookup"><span data-stu-id="e97e0-502">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="e97e0-503">ComponentNumber - składnik hello w tooreturn hello nazwa Wyróżniająca</span><span class="sxs-lookup"><span data-stu-id="e97e0-503">ComponentNumber - hello component in hello DN tooreturn</span></span>
* <span data-ttu-id="e97e0-504">Opcje: Kontroler domeny — Ignoruj wszystkie składniki z "dc ="</span><span class="sxs-lookup"><span data-stu-id="e97e0-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="e97e0-505">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-505">**Example:**</span></span>  
<span data-ttu-id="e97e0-506">Jeśli nazwa wyróżniająca "cn Jan, ou = (Atlanta), ou = GA, ou = = US, dc = contoso, dc = com" następnie</span><span class="sxs-lookup"><span data-stu-id="e97e0-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="e97e0-507">Obie zwracają NAS.</span><span class="sxs-lookup"><span data-stu-id="e97e0-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="e97e0-508">Błąd</span><span class="sxs-lookup"><span data-stu-id="e97e0-508">Error</span></span>
<span data-ttu-id="e97e0-509">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-509">**Description:**</span></span>  
<span data-ttu-id="e97e0-510">Witaj funkcji błędu jest używane tooreturn błędu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="e97e0-510">hello Error function is used tooreturn a custom error.</span></span>

<span data-ttu-id="e97e0-511">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="e97e0-512">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="e97e0-513">Jeśli hello atrybut accountName nie jest obecny, zgłoś błąd w obiekcie hello.</span><span class="sxs-lookup"><span data-stu-id="e97e0-513">If hello attribute accountName is not present, throw an error on hello object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="e97e0-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="e97e0-514">EscapeDNComponent</span></span>
<span data-ttu-id="e97e0-515">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-515">**Description:**</span></span>  
<span data-ttu-id="e97e0-516">Hello EscapeDNComponent funkcja przyjmuje jeden składnik nazwy domen i jego specjalne, dlatego może być reprezentowany w protokole LDAP.</span><span class="sxs-lookup"><span data-stu-id="e97e0-516">hello EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="e97e0-517">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="e97e0-518">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="e97e0-519">Sprawdza obiekt hello mogą być tworzone w katalogu LDAP, nawet wtedy, gdy atrybut displayName hello zawiera znaki, które należy użyć znaków ucieczki w protokole LDAP.</span><span class="sxs-lookup"><span data-stu-id="e97e0-519">Makes sure hello object can be created in an LDAP directory even if hello displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="e97e0-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="e97e0-520">FormatDateTime</span></span>
<span data-ttu-id="e97e0-521">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-521">**Description:**</span></span>  
<span data-ttu-id="e97e0-522">Funkcja FormatDateTime Hello jest używany tooformat tooa ciąg daty i godziny w określonym formacie</span><span class="sxs-lookup"><span data-stu-id="e97e0-522">hello FormatDateTime function is used tooformat a DateTime tooa string with a specified format</span></span>

<span data-ttu-id="e97e0-523">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="e97e0-524">wartość: wartości w formacie daty/godziny hello</span><span class="sxs-lookup"><span data-stu-id="e97e0-524">value: a value in hello DateTime format</span></span>
* <span data-ttu-id="e97e0-525">Format: ciąg reprezentujący tooconvert format hello do.</span><span class="sxs-lookup"><span data-stu-id="e97e0-525">format: a string representing hello format tooconvert to.</span></span>

<span data-ttu-id="e97e0-526">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-526">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-527">Witaj możliwe wartości dla hello formatu można znaleźć tutaj: [zdefiniowane przez użytkownika (funkcji Format) formaty daty i godziny](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="e97e0-527">hello possible values for hello format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="e97e0-528">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="e97e0-529">Wynikiem "2007-12-25".</span><span class="sxs-lookup"><span data-stu-id="e97e0-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="e97e0-530">Może spowodować "20140905081453.0Z"</span><span class="sxs-lookup"><span data-stu-id="e97e0-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="e97e0-531">IDENTYFIKATOR GUID</span><span class="sxs-lookup"><span data-stu-id="e97e0-531">GUID</span></span>
<span data-ttu-id="e97e0-532">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-532">**Description:**</span></span>  
<span data-ttu-id="e97e0-533">Funkcja Hello GUID generuje losowe nowego identyfikatora GUID</span><span class="sxs-lookup"><span data-stu-id="e97e0-533">hello function GUID generates a new random GUID</span></span>

<span data-ttu-id="e97e0-534">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="e97e0-535">IIF</span><span class="sxs-lookup"><span data-stu-id="e97e0-535">IIF</span></span>
<span data-ttu-id="e97e0-536">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-536">**Description:**</span></span>  
<span data-ttu-id="e97e0-537">Hello funkcji IIF zwraca jeden zestaw możliwych wartości na podstawie określonego warunku.</span><span class="sxs-lookup"><span data-stu-id="e97e0-537">hello IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="e97e0-538">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="e97e0-539">warunek: dowolna wartość lub wyrażenie, które mogą być obliczane tootrue, lub FAŁSZ.</span><span class="sxs-lookup"><span data-stu-id="e97e0-539">condition: any value or expression that can be evaluated tootrue or false.</span></span>
* <span data-ttu-id="e97e0-540">Wartość_dla_prawdy: Jeśli warunek hello tootrue, hello zwrócił wartość.</span><span class="sxs-lookup"><span data-stu-id="e97e0-540">valueIfTrue: If hello condition evaluates tootrue, hello returned value.</span></span>
* <span data-ttu-id="e97e0-541">Wartość_dla_fałszu: Jeśli warunek hello toofalse, hello zwrócił wartość.</span><span class="sxs-lookup"><span data-stu-id="e97e0-541">valueIfFalse: If hello condition evaluates toofalse, hello returned value.</span></span>

<span data-ttu-id="e97e0-542">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="e97e0-543">Jeśli użytkownik hello jest intern, zwraca toohello początku go innym zwraca alias użytkownika hello jest dodać hello alias użytkownika z "t-".</span><span class="sxs-lookup"><span data-stu-id="e97e0-543">If hello user is an intern, returns hello alias of a user with "t-" added toohello beginning of it, else returns hello user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="e97e0-544">InStr</span><span class="sxs-lookup"><span data-stu-id="e97e0-544">InStr</span></span>
<span data-ttu-id="e97e0-545">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-545">**Description:**</span></span>  
<span data-ttu-id="e97e0-546">Hello funkcji InStr znajduje pierwsze wystąpienie hello podciągu w ciągu</span><span class="sxs-lookup"><span data-stu-id="e97e0-546">hello InStr function finds hello first occurrence of a substring in a string</span></span>

<span data-ttu-id="e97e0-547">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="e97e0-548">ciąg_przeszukiwany: string toobe przeszukiwane</span><span class="sxs-lookup"><span data-stu-id="e97e0-548">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="e97e0-549">ciąg_poszukiwany: string toobe znaleziono</span><span class="sxs-lookup"><span data-stu-id="e97e0-549">stringmatch: string toobe found</span></span>
* <span data-ttu-id="e97e0-550">Rozpocznij: uruchamianie podciąg hello toofind pozycji</span><span class="sxs-lookup"><span data-stu-id="e97e0-550">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="e97e0-551">porównywanie: vbTextCompare lub vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="e97e0-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="e97e0-552">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-552">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-553">Zwraca hello pozycji, gdzie został znaleziony podciąg hello lub 0, jeśli nie znaleziono.</span><span class="sxs-lookup"><span data-stu-id="e97e0-553">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="e97e0-554">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-554">**Example:**</span></span>  
`InStr("hello quick brown fox","quick")`  
<span data-ttu-id="e97e0-555">Evalues too5</span><span class="sxs-lookup"><span data-stu-id="e97e0-555">Evalues too5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="e97e0-556">Oblicza too7</span><span class="sxs-lookup"><span data-stu-id="e97e0-556">Evaluates too7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="e97e0-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="e97e0-557">InStrRev</span></span>
<span data-ttu-id="e97e0-558">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-558">**Description:**</span></span>  
<span data-ttu-id="e97e0-559">Hello Funkcja InStrRev znajduje hello ostatniego wystąpienia podciągu w ciągu</span><span class="sxs-lookup"><span data-stu-id="e97e0-559">hello InStrRev function finds hello last occurrence of a substring in a string</span></span>

<span data-ttu-id="e97e0-560">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="e97e0-561">ciąg_przeszukiwany: string toobe przeszukiwane</span><span class="sxs-lookup"><span data-stu-id="e97e0-561">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="e97e0-562">ciąg_poszukiwany: string toobe znaleziono</span><span class="sxs-lookup"><span data-stu-id="e97e0-562">stringmatch: string toobe found</span></span>
* <span data-ttu-id="e97e0-563">Rozpocznij: uruchamianie podciąg hello toofind pozycji</span><span class="sxs-lookup"><span data-stu-id="e97e0-563">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="e97e0-564">porównywanie: vbTextCompare lub vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="e97e0-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="e97e0-565">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-565">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-566">Zwraca hello pozycji, gdzie został znaleziony podciąg hello lub 0, jeśli nie znaleziono.</span><span class="sxs-lookup"><span data-stu-id="e97e0-566">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="e97e0-567">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="e97e0-568">Zwraca 7</span><span class="sxs-lookup"><span data-stu-id="e97e0-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="e97e0-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="e97e0-569">IsBitSet</span></span>
<span data-ttu-id="e97e0-570">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-570">**Description:**</span></span>  
<span data-ttu-id="e97e0-571">Funkcja Hello IsBitSet testów, jeśli jest ustawiony bit lub nie</span><span class="sxs-lookup"><span data-stu-id="e97e0-571">hello function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="e97e0-572">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="e97e0-573">wartość: wartość liczbową evaluated.flag: wartość liczbową hello bit toobe obliczone</span><span class="sxs-lookup"><span data-stu-id="e97e0-573">value: a numeric value that is evaluated.flag: a numeric value that has hello bit toobe evaluated</span></span>

<span data-ttu-id="e97e0-574">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="e97e0-575">Zwraca wartość True, ponieważ ustawiono bit "4" w wartości szesnastkowe hello "F"</span><span class="sxs-lookup"><span data-stu-id="e97e0-575">Returns True because bit "4" is set in hello hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="e97e0-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="e97e0-576">IsDate</span></span>
<span data-ttu-id="e97e0-577">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-577">**Description:**</span></span>  
<span data-ttu-id="e97e0-578">Jeśli wyrażenie hello może być oblicza jako typu DateTime, a następnie hello Funkcja IsDate ocenia tooTrue.</span><span class="sxs-lookup"><span data-stu-id="e97e0-578">If hello expression can be evaluates as a DateTime type, then hello IsDate function evaluates tooTrue.</span></span>

<span data-ttu-id="e97e0-579">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="e97e0-580">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-580">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-581">Toodetermine należy użyć, jeśli CDate() mogą być skutecznie.</span><span class="sxs-lookup"><span data-stu-id="e97e0-581">Used toodetermine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="e97e0-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="e97e0-582">IsCert</span></span>
<span data-ttu-id="e97e0-583">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-583">**Description:**</span></span>  
<span data-ttu-id="e97e0-584">Zwraca wartość PRAWDA, jeśli dane pierwotne hello może być Zserializowany do obiektu certyfikatu .NET X509Certificate2.</span><span class="sxs-lookup"><span data-stu-id="e97e0-584">Returns true if hello raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="e97e0-585">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="e97e0-586">certificateRawData: certyfikat X.509 reprezentację tablicy bajtów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="e97e0-587">Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.</span><span class="sxs-lookup"><span data-stu-id="e97e0-587">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="e97e0-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="e97e0-588">IsEmpty</span></span>
<span data-ttu-id="e97e0-589">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-589">**Description:**</span></span>  
<span data-ttu-id="e97e0-590">Jeśli atrybut hello znajduje się w hello CS lub MV, ale ocenia tooan pusty ciąg, funkcja IsEmpty hello oblicza tooTrue.</span><span class="sxs-lookup"><span data-stu-id="e97e0-590">If hello attribute is present in hello CS or MV but evaluates tooan empty string, then hello IsEmpty function evaluates tooTrue.</span></span>

<span data-ttu-id="e97e0-591">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="e97e0-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="e97e0-592">IsGuid</span></span>
<span data-ttu-id="e97e0-593">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-593">**Description:**</span></span>  
<span data-ttu-id="e97e0-594">Jeśli ciąg hello może być przekonwertowany tooa identyfikator GUID, funkcja IsGuid hello obliczone tootrue.</span><span class="sxs-lookup"><span data-stu-id="e97e0-594">If hello string could be converted tooa GUID, then hello IsGuid function evaluated tootrue.</span></span>

<span data-ttu-id="e97e0-595">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="e97e0-596">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-596">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-597">Identyfikator GUID jest zdefiniowany jako ciąg, po jednej z tych wzorców: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx lub {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="e97e0-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="e97e0-598">Toodetermine należy użyć, jeśli CGuid() mogą być skutecznie.</span><span class="sxs-lookup"><span data-stu-id="e97e0-598">Used toodetermine if CGuid() can be successful.</span></span>

<span data-ttu-id="e97e0-599">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="e97e0-600">Jeśli hello StrAttribute ma format identyfikatora GUID, zwróć reprezentacja binarna, w przeciwnym razie zwraca wartość Null.</span><span class="sxs-lookup"><span data-stu-id="e97e0-600">If hello StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="e97e0-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="e97e0-601">IsNull</span></span>
<span data-ttu-id="e97e0-602">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-602">**Description:**</span></span>  
<span data-ttu-id="e97e0-603">Jeśli wyrażenie hello tooNull, hello IsNull funkcja zwraca wartość true.</span><span class="sxs-lookup"><span data-stu-id="e97e0-603">If hello expression evaluates tooNull, then hello IsNull function returns true.</span></span>

<span data-ttu-id="e97e0-604">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="e97e0-605">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-605">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-606">Dla atrybutu o wartości Null jest wyrażona hello braku atrybutu hello.</span><span class="sxs-lookup"><span data-stu-id="e97e0-606">For an attribute, a Null is expressed by hello absence of hello attribute.</span></span>

<span data-ttu-id="e97e0-607">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="e97e0-608">Zwraca wartość PRAWDA, jeśli atrybut hello nie jest obecny w hello CS lub MV.</span><span class="sxs-lookup"><span data-stu-id="e97e0-608">Returns True if hello attribute is not present in hello CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="e97e0-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="e97e0-609">IsNullOrEmpty</span></span>
<span data-ttu-id="e97e0-610">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-610">**Description:**</span></span>  
<span data-ttu-id="e97e0-611">Jeśli wyrażenie hello ma wartość null lub pusty ciąg, hello IsNullOrEmpty funkcja zwraca wartość true.</span><span class="sxs-lookup"><span data-stu-id="e97e0-611">If hello expression is null or an empty string, then hello IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="e97e0-612">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="e97e0-613">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-613">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-614">Dla atrybutu to oceni tooTrue Jeśli atrybut hello nie istnieje lub jest obecny, ale jest pustym ciągiem.</span><span class="sxs-lookup"><span data-stu-id="e97e0-614">For an attribute, this would evaluate tooTrue if hello attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="e97e0-615">Hello odwrotność funkcji ten nosi nazwę IsPresent.</span><span class="sxs-lookup"><span data-stu-id="e97e0-615">hello inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="e97e0-616">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="e97e0-617">Zwraca wartość PRAWDA, jeśli nie jest obecny lub jest pustym ciągiem hello CS lub MV hello atrybutu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-617">Returns True if hello attribute is not present or is an empty string in hello CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="e97e0-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="e97e0-618">IsNumeric</span></span>
<span data-ttu-id="e97e0-619">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-619">**Description:**</span></span>  
<span data-ttu-id="e97e0-620">Witaj IsNumeric funkcja zwraca wartość logiczną wskazującą, czy wyrażenie może przyjąć jako liczba typu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-620">hello IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="e97e0-621">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="e97e0-622">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-622">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-623">Toodetermine należy użyć, jeśli CNum() może być wyrażeniem hello tooparse powiodło się.</span><span class="sxs-lookup"><span data-stu-id="e97e0-623">Used toodetermine if CNum() can be successful tooparse hello expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="e97e0-624">IsString</span><span class="sxs-lookup"><span data-stu-id="e97e0-624">IsString</span></span>
<span data-ttu-id="e97e0-625">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-625">**Description:**</span></span>  
<span data-ttu-id="e97e0-626">Jeśli wyrażenie hello można być obliczane tooa typu string, a następnie funkcja IsString hello ocenia tooTrue.</span><span class="sxs-lookup"><span data-stu-id="e97e0-626">If hello expression can be evaluated tooa string type, then hello IsString function evaluates tooTrue.</span></span>

<span data-ttu-id="e97e0-627">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="e97e0-628">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-628">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-629">Toodetermine należy użyć, jeśli CStr() może być wyrażeniem hello tooparse powiodło się.</span><span class="sxs-lookup"><span data-stu-id="e97e0-629">Used toodetermine if CStr() can be successful tooparse hello expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="e97e0-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="e97e0-630">IsPresent</span></span>
<span data-ttu-id="e97e0-631">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-631">**Description:**</span></span>  
<span data-ttu-id="e97e0-632">Jeśli wyrażenie hello tooa ciąg, który nie jest równa Null i nie jest pusta, następnie hello IsPresent, funkcja zwraca wartość true.</span><span class="sxs-lookup"><span data-stu-id="e97e0-632">If hello expression evaluates tooa string that is not Null and is not empty, then hello IsPresent function returns true.</span></span>

<span data-ttu-id="e97e0-633">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="e97e0-634">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-634">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-635">Hello odwrotność funkcji ten nosi nazwę IsNullOrEmpty.</span><span class="sxs-lookup"><span data-stu-id="e97e0-635">hello inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="e97e0-636">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="e97e0-637">Element</span><span class="sxs-lookup"><span data-stu-id="e97e0-637">Item</span></span>
<span data-ttu-id="e97e0-638">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-638">**Description:**</span></span>  
<span data-ttu-id="e97e0-639">Hello elementu funkcja zwraca jeden element z ciągu/atrybutu wielowartościowego.</span><span class="sxs-lookup"><span data-stu-id="e97e0-639">hello Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="e97e0-640">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="e97e0-641">Atrybut: atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="e97e0-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="e97e0-642">Indeks: elementu tooan indeksu w ciągu wielowartościowe hello.</span><span class="sxs-lookup"><span data-stu-id="e97e0-642">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="e97e0-643">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-643">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-644">Hello funkcja elementu przydaje się wraz z hello funkcja zawiera ponieważ hello ostatnie funkcja zwraca element tooan indeksu hello hello atrybutów wielowartościowych.</span><span class="sxs-lookup"><span data-stu-id="e97e0-644">hello Item function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="e97e0-645">Zwraca błąd, jeśli indeks jest poza zakresem.</span><span class="sxs-lookup"><span data-stu-id="e97e0-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="e97e0-646">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="e97e0-647">Zwraca hello podstawowego adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="e97e0-647">Returns hello primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="e97e0-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="e97e0-648">ItemOrNull</span></span>
<span data-ttu-id="e97e0-649">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-649">**Description:**</span></span>  
<span data-ttu-id="e97e0-650">Hello ItemOrNull funkcja zwraca jeden element z ciągu/atrybutów wielowartościowych.</span><span class="sxs-lookup"><span data-stu-id="e97e0-650">hello ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="e97e0-651">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="e97e0-652">Atrybut: atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="e97e0-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="e97e0-653">Indeks: elementu tooan indeksu w ciągu wielowartościowe hello.</span><span class="sxs-lookup"><span data-stu-id="e97e0-653">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="e97e0-654">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-654">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-655">Hello funkcja ItemOrNull przydaje się wraz z hello funkcja zawiera ponieważ hello ostatnie funkcja zwraca element tooan indeksu hello atrybutu wielowartościowego hello.</span><span class="sxs-lookup"><span data-stu-id="e97e0-655">hello ItemOrNull function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="e97e0-656">Jeśli indeks jest poza zakresem, zwraca wartość Null.</span><span class="sxs-lookup"><span data-stu-id="e97e0-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="e97e0-657">Join</span><span class="sxs-lookup"><span data-stu-id="e97e0-657">Join</span></span>
<span data-ttu-id="e97e0-658">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-658">**Description:**</span></span>  
<span data-ttu-id="e97e0-659">funkcja sprzężenia Hello wielowartościowe ciąg znaków i zwraca ciąg pojedynczej wartości z określonego separatorem wstawione między każdym z elementów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-659">hello Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="e97e0-660">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="e97e0-661">Atrybut: atrybutu wielowartościowego zawierające ciągi toobe przyłączony.</span><span class="sxs-lookup"><span data-stu-id="e97e0-661">attribute: Multi-valued attribute containing strings toobe joined.</span></span>
* <span data-ttu-id="e97e0-662">Ogranicznik: dowolnego ciągu podciągów hello tooseparate używanych w hello zwrócony ciąg.</span><span class="sxs-lookup"><span data-stu-id="e97e0-662">delimiter: Any string, used tooseparate hello substrings in hello returned string.</span></span> <span data-ttu-id="e97e0-663">Pominięcie hello spacją ("") jest używany.</span><span class="sxs-lookup"><span data-stu-id="e97e0-663">If omitted, hello space character (" ") is used.</span></span> <span data-ttu-id="e97e0-664">Jeśli wartość ogranicznika jest ciągiem o zerowej długości ("") lub Nothing, wszystkie elementy na liście hello jest połączony z nie ograniczników.</span><span class="sxs-lookup"><span data-stu-id="e97e0-664">If Delimiter is a zero-length string ("") or Nothing, all items in hello list are concatenated with no delimiters.</span></span>

<span data-ttu-id="e97e0-665">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="e97e0-665">**Remarks**</span></span>  
<span data-ttu-id="e97e0-666">Występuje parzystość między hello sprzężenia i funkcje podziału.</span><span class="sxs-lookup"><span data-stu-id="e97e0-666">There is parity between hello Join and Split functions.</span></span> <span data-ttu-id="e97e0-667">Hello funkcja sprzężenia pobiera tablicę ciągów i dołącza je za pomocą ciągu ogranicznik tooreturn pojedynczy ciąg.</span><span class="sxs-lookup"><span data-stu-id="e97e0-667">hello Join function takes an array of strings and joins them using a delimiter string, tooreturn a single string.</span></span> <span data-ttu-id="e97e0-668">Hello funkcja podziału ciąg znaków i oddziela go na hello ogranicznik, tooreturn tablicy ciągów.</span><span class="sxs-lookup"><span data-stu-id="e97e0-668">hello Split function takes a string and separates it at hello delimiter, tooreturn an array of strings.</span></span> <span data-ttu-id="e97e0-669">Najważniejsza różnica jest jednak czy sprzężenia można ciągów z dowolnym ciągiem ogranicznik, podziału tylko rozdzielić ciągów za pomocą pojedynczy znak ogranicznika.</span><span class="sxs-lookup"><span data-stu-id="e97e0-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="e97e0-670">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="e97e0-671">Może zwrócić: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="e97e0-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="e97e0-672">LCase</span><span class="sxs-lookup"><span data-stu-id="e97e0-672">LCase</span></span>
<span data-ttu-id="e97e0-673">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-673">**Description:**</span></span>  
<span data-ttu-id="e97e0-674">Funkcja LCase Hello konwertuje wszystkie znaki w przypadku toolower ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-674">hello LCase function converts all characters in a string toolower case.</span></span>

<span data-ttu-id="e97e0-675">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="e97e0-676">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="e97e0-677">Zwraca "test".</span><span class="sxs-lookup"><span data-stu-id="e97e0-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="e97e0-678">Po lewej</span><span class="sxs-lookup"><span data-stu-id="e97e0-678">Left</span></span>
<span data-ttu-id="e97e0-679">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-679">**Description:**</span></span>  
<span data-ttu-id="e97e0-680">Funkcja po lewej stronie powitania zwraca określoną liczbę znaków od lewej hello ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-680">hello Left function returns a specified number of characters from hello left of a string.</span></span>

<span data-ttu-id="e97e0-681">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="e97e0-682">ciąg: hello tooreturn znaków z</span><span class="sxs-lookup"><span data-stu-id="e97e0-682">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="e97e0-683">NumChars: Liczba identyfikująca hello liczba tooreturn znaków od początku hello (po lewej) ciągu</span><span class="sxs-lookup"><span data-stu-id="e97e0-683">NumChars: a number identifying hello number of characters tooreturn from hello beginning (left) of string</span></span>

<span data-ttu-id="e97e0-684">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-684">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-685">Ciąg zawierający hello pierwsze numChars znaków w ciągu:</span><span class="sxs-lookup"><span data-stu-id="e97e0-685">A string containing hello first numChars characters in string:</span></span>

* <span data-ttu-id="e97e0-686">Jeśli numChars = 0, zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="e97e0-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="e97e0-687">Jeśli numChars < 0, zwraca ciąg wejściowy.</span><span class="sxs-lookup"><span data-stu-id="e97e0-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="e97e0-688">Jeśli ciąg ma wartość null, zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="e97e0-688">If string is null, return empty string.</span></span>

<span data-ttu-id="e97e0-689">Jeśli ciąg zawiera mniej znaków niż liczba hello określone w numChars, jest zwracany ciąg toostring identyczne, (tj. zawierający wszystkie znaki w parametrze 1).</span><span class="sxs-lookup"><span data-stu-id="e97e0-689">If string contains fewer characters than hello number specified in numChars, a string identical toostring (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="e97e0-690">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="e97e0-691">Zwraca wartość "Joh".</span><span class="sxs-lookup"><span data-stu-id="e97e0-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="e97e0-692">Długość</span><span class="sxs-lookup"><span data-stu-id="e97e0-692">Len</span></span>
<span data-ttu-id="e97e0-693">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-693">**Description:**</span></span>  
<span data-ttu-id="e97e0-694">Witaj Len, funkcja zwraca liczbę znaków w ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-694">hello Len function returns number of characters in a string.</span></span>

<span data-ttu-id="e97e0-695">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="e97e0-696">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="e97e0-697">Zwraca 8</span><span class="sxs-lookup"><span data-stu-id="e97e0-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="e97e0-698">Przytp</span><span class="sxs-lookup"><span data-stu-id="e97e0-698">LTrim</span></span>
<span data-ttu-id="e97e0-699">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-699">**Description:**</span></span>  
<span data-ttu-id="e97e0-700">Funkcja LTrim Hello usuwa spacji wiodących z ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-700">hello LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="e97e0-701">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="e97e0-702">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="e97e0-703">Zwraca "Test"</span><span class="sxs-lookup"><span data-stu-id="e97e0-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="e97e0-704">MID</span><span class="sxs-lookup"><span data-stu-id="e97e0-704">Mid</span></span>
<span data-ttu-id="e97e0-705">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-705">**Description:**</span></span>  
<span data-ttu-id="e97e0-706">Witaj Mid funkcja zwraca określoną liczbę znaków od określonej pozycji w ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-706">hello Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="e97e0-707">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="e97e0-708">ciąg: hello tooreturn znaków z</span><span class="sxs-lookup"><span data-stu-id="e97e0-708">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="e97e0-709">Rozpocznij: Liczba identyfikująca hello pozycji w ciągu znaków tooreturn z początkowej</span><span class="sxs-lookup"><span data-stu-id="e97e0-709">start: a number identifying hello starting position in string tooreturn characters from</span></span>
* <span data-ttu-id="e97e0-710">NumChars: Liczba identyfikująca hello liczba tooreturn znaków od pozycji w ciągu</span><span class="sxs-lookup"><span data-stu-id="e97e0-710">NumChars: a number identifying hello number of characters tooreturn from position in string</span></span>

<span data-ttu-id="e97e0-711">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-711">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-712">Uruchom numChars zwracanych znaków, zaczynając od pozycji w ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="e97e0-713">Ciąg zawierający numChars znaków od początku pozycji w ciągu:</span><span class="sxs-lookup"><span data-stu-id="e97e0-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="e97e0-714">Jeśli numChars = 0, zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="e97e0-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="e97e0-715">Jeśli numChars < 0, zwraca ciąg wejściowy.</span><span class="sxs-lookup"><span data-stu-id="e97e0-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="e97e0-716">Jeśli start > hello długość ciągu, zwraca ciąg wejściowy.</span><span class="sxs-lookup"><span data-stu-id="e97e0-716">If start > hello length of string, return input string.</span></span>
* <span data-ttu-id="e97e0-717">Jeśli start < = 0, zwraca ciąg wejściowy.</span><span class="sxs-lookup"><span data-stu-id="e97e0-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="e97e0-718">Jeśli ciąg ma wartość null, zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="e97e0-718">If string is null, return empty string.</span></span>

<span data-ttu-id="e97e0-719">Jeśli nie są znaki numChar pozostałych w ciągu od początku pozycji, jako wiele znaków, jak to możliwe są zwracane.</span><span class="sxs-lookup"><span data-stu-id="e97e0-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="e97e0-720">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="e97e0-721">Zwraca wartość "nie hn".</span><span class="sxs-lookup"><span data-stu-id="e97e0-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="e97e0-722">Zwraca "Nowak"</span><span class="sxs-lookup"><span data-stu-id="e97e0-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="e97e0-723">Teraz</span><span class="sxs-lookup"><span data-stu-id="e97e0-723">Now</span></span>
<span data-ttu-id="e97e0-724">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-724">**Description:**</span></span>  
<span data-ttu-id="e97e0-725">Witaj teraz funkcja zwraca wartość typu DateTime Określanie hello bieżącą datę i godzinę, zgodnie z tooyour komputera systemowej daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="e97e0-725">hello Now function returns a DateTime specifying hello current date and time, according tooyour computer's system date and time.</span></span>

<span data-ttu-id="e97e0-726">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="e97e0-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="e97e0-727">NumFromDate</span></span>
<span data-ttu-id="e97e0-728">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-728">**Description:**</span></span>  
<span data-ttu-id="e97e0-729">Hello NumFromDate funkcja zwraca datę w formacie daty przez usługi AD.</span><span class="sxs-lookup"><span data-stu-id="e97e0-729">hello NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="e97e0-730">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="e97e0-731">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="e97e0-732">Zwraca 129699324000000000</span><span class="sxs-lookup"><span data-stu-id="e97e0-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="e97e0-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="e97e0-733">PadLeft</span></span>
<span data-ttu-id="e97e0-734">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-734">**Description:**</span></span>  
<span data-ttu-id="e97e0-735">Hello PadLeft funkcji podkładki lewej tooa ciągu, określić przy użyciu znak dopełnienia podana długość.</span><span class="sxs-lookup"><span data-stu-id="e97e0-735">hello PadLeft function left-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="e97e0-736">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="e97e0-737">ciąg: hello toopad ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-737">string: hello string toopad.</span></span>
* <span data-ttu-id="e97e0-738">długość: liczba całkowita reprezentująca hello wymaganą długość ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-738">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="e97e0-739">padCharacter: ciąg składający się z toouse pojedynczy znak, jako znak konsoli hello</span><span class="sxs-lookup"><span data-stu-id="e97e0-739">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="e97e0-740">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-740">**Remarks:**</span></span>

* <span data-ttu-id="e97e0-741">Jeśli hello długość ciągu jest mniejsza niż długość, następnie padCharacter jest od wielokrotnie dołączany toohello (po lewej) ciągu, dopóki nie toolength równy długości.</span><span class="sxs-lookup"><span data-stu-id="e97e0-741">If hello length of string is less than length, then padCharacter is repeatedly appended toohello beginning (left) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="e97e0-742">padCharacter może być znaku spacji, ale nie może mieć wartości null.</span><span class="sxs-lookup"><span data-stu-id="e97e0-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="e97e0-743">Jeśli hello długość ciągu jest równy tooor większa niż długość, ciąg zostanie zwrócony bez zmian.</span><span class="sxs-lookup"><span data-stu-id="e97e0-743">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="e97e0-744">Jeśli ciąg ma długość większą niż lub równe toolength, jest zwracany ciąg toostring identyczne.</span><span class="sxs-lookup"><span data-stu-id="e97e0-744">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="e97e0-745">Jeśli hello długość ciągu jest mniejsza niż długość, nowy ciąg hello żądana się, że długość jest zwracana, zawierającą ciąg dopełniane przy padCharacter.</span><span class="sxs-lookup"><span data-stu-id="e97e0-745">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="e97e0-746">Jeśli ciąg ma wartość null, funkcja hello zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="e97e0-746">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="e97e0-747">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="e97e0-748">Zwraca wartość "000000User".</span><span class="sxs-lookup"><span data-stu-id="e97e0-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="e97e0-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="e97e0-749">PadRight</span></span>
<span data-ttu-id="e97e0-750">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-750">**Description:**</span></span>  
<span data-ttu-id="e97e0-751">Hello PadRight funkcji podkładki prawo tooa ciągu, określić przy użyciu znak dopełnienia podana długość.</span><span class="sxs-lookup"><span data-stu-id="e97e0-751">hello PadRight function right-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="e97e0-752">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="e97e0-753">ciąg: hello toopad ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-753">string: hello string toopad.</span></span>
* <span data-ttu-id="e97e0-754">długość: liczba całkowita reprezentująca hello wymaganą długość ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-754">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="e97e0-755">padCharacter: ciąg składający się z toouse pojedynczy znak, jako znak konsoli hello</span><span class="sxs-lookup"><span data-stu-id="e97e0-755">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="e97e0-756">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-756">**Remarks:**</span></span>

* <span data-ttu-id="e97e0-757">Jeśli hello długość ciągu jest mniejsza niż długość, następnie padCharacter jest wielokrotnie dołączany toohello końca (po prawej) ciągu, dopóki nie toolength równy długości.</span><span class="sxs-lookup"><span data-stu-id="e97e0-757">If hello length of string is less than length, then padCharacter is repeatedly appended toohello end (right) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="e97e0-758">padCharacter może być znaku spacji, ale nie może mieć wartości null.</span><span class="sxs-lookup"><span data-stu-id="e97e0-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="e97e0-759">Jeśli hello długość ciągu jest równy tooor większa niż długość, ciąg zostanie zwrócony bez zmian.</span><span class="sxs-lookup"><span data-stu-id="e97e0-759">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="e97e0-760">Jeśli ciąg ma długość większą niż lub równe toolength, jest zwracany ciąg toostring identyczne.</span><span class="sxs-lookup"><span data-stu-id="e97e0-760">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="e97e0-761">Jeśli hello długość ciągu jest mniejsza niż długość, nowy ciąg hello żądana się, że długość jest zwracana, zawierającą ciąg dopełniane przy padCharacter.</span><span class="sxs-lookup"><span data-stu-id="e97e0-761">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="e97e0-762">Jeśli ciąg ma wartość null, funkcja hello zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="e97e0-762">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="e97e0-763">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="e97e0-764">Zwraca wartość "User000000".</span><span class="sxs-lookup"><span data-stu-id="e97e0-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="e97e0-765">PCase</span><span class="sxs-lookup"><span data-stu-id="e97e0-765">PCase</span></span>
<span data-ttu-id="e97e0-766">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-766">**Description:**</span></span>  
<span data-ttu-id="e97e0-767">pierwszy znak każdego wyrazu odstępami w przypadku tooupper ciąg hello konwertuje Hello PCase funkcji i wszystkie inne znaki są konwertowane toolower case.</span><span class="sxs-lookup"><span data-stu-id="e97e0-767">hello PCase function converts hello first character of each space delimited word in a string tooupper case, and all other characters are converted toolower case.</span></span>

<span data-ttu-id="e97e0-768">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="e97e0-769">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-769">**Remarks:**</span></span>

* <span data-ttu-id="e97e0-770">Ta funkcja nie jest aktualnie dostępny tooconvert wielkość liter odpowiednie słowo, które jest całkowicie wielkie litery, takich jak akronim.</span><span class="sxs-lookup"><span data-stu-id="e97e0-770">This function does not currently provide proper casing tooconvert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="e97e0-771">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="e97e0-772">Zwraca "Test".</span><span class="sxs-lookup"><span data-stu-id="e97e0-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="e97e0-773">Zwraca "Test"</span><span class="sxs-lookup"><span data-stu-id="e97e0-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="e97e0-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="e97e0-774">RandomNum</span></span>
<span data-ttu-id="e97e0-775">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-775">**Description:**</span></span>  
<span data-ttu-id="e97e0-776">Witaj RandomNum funkcja zwraca liczbę losową między określonego interwału.</span><span class="sxs-lookup"><span data-stu-id="e97e0-776">hello RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="e97e0-777">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="e97e0-778">Rozpocznij: numer identyfikacyjny hello dolny limit hello toogenerate losowych wartości</span><span class="sxs-lookup"><span data-stu-id="e97e0-778">start: a number identifying hello lower limit of hello random value toogenerate</span></span>
* <span data-ttu-id="e97e0-779">końcowy: numer identyfikacyjny hello górny limit hello toogenerate losowych wartości</span><span class="sxs-lookup"><span data-stu-id="e97e0-779">end: a number identifying hello upper limit of hello random value toogenerate</span></span>

<span data-ttu-id="e97e0-780">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="e97e0-781">Może zwrócić 734.</span><span class="sxs-lookup"><span data-stu-id="e97e0-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="e97e0-782">Removeduplicates —</span><span class="sxs-lookup"><span data-stu-id="e97e0-782">RemoveDuplicates</span></span>
<span data-ttu-id="e97e0-783">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-783">**Description:**</span></span>  
<span data-ttu-id="e97e0-784">Hello removeduplicates — funkcja wielowartościowe ciąg znaków i upewnij się, że każda wartość jest unikatowa.</span><span class="sxs-lookup"><span data-stu-id="e97e0-784">hello RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="e97e0-785">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="e97e0-786">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="e97e0-787">Zwraca atrybutu oczyszczony proxyAddress, w której zostały usunięte wszystkie zduplikowane wartości.</span><span class="sxs-lookup"><span data-stu-id="e97e0-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="e97e0-788">Replace</span><span class="sxs-lookup"><span data-stu-id="e97e0-788">Replace</span></span>
<span data-ttu-id="e97e0-789">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-789">**Description:**</span></span>  
<span data-ttu-id="e97e0-790">Witaj funkcji Replace zamienia wszystkie wystąpienia ciągu tooanother ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-790">hello Replace function replaces all occurrences of a string tooanother string.</span></span>

<span data-ttu-id="e97e0-791">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="e97e0-792">ciąg: tooreplace ciągu wartości.</span><span class="sxs-lookup"><span data-stu-id="e97e0-792">string: A string tooreplace values in.</span></span>
* <span data-ttu-id="e97e0-793">OldValue: hello toosearch ciągu dla i tooreplace.</span><span class="sxs-lookup"><span data-stu-id="e97e0-793">OldValue: hello string toosearch for and tooreplace.</span></span>
* <span data-ttu-id="e97e0-794">NewValue: hello tooreplace ciąg do.</span><span class="sxs-lookup"><span data-stu-id="e97e0-794">NewValue: hello string tooreplace to.</span></span>

<span data-ttu-id="e97e0-795">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-795">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-796">Funkcja Hello rozpoznaje powitania po monikerów specjalne:</span><span class="sxs-lookup"><span data-stu-id="e97e0-796">hello function recognizes hello following special monikers:</span></span>

* <span data-ttu-id="e97e0-797">\n — nowy wiersz</span><span class="sxs-lookup"><span data-stu-id="e97e0-797">\n – New Line</span></span>
* <span data-ttu-id="e97e0-798">\r — powrót karetki</span><span class="sxs-lookup"><span data-stu-id="e97e0-798">\r – Carriage Return</span></span>
* <span data-ttu-id="e97e0-799">\t — karta</span><span class="sxs-lookup"><span data-stu-id="e97e0-799">\t – Tab</span></span>

<span data-ttu-id="e97e0-800">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="e97e0-801">Zastępuje CRLF przecinek i spacja i może spowodować zbyt "Co Microsoft sposób, Redmond, WA, USA"</span><span class="sxs-lookup"><span data-stu-id="e97e0-801">Replaces CRLF with a comma and space, and could lead too"One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="e97e0-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="e97e0-802">ReplaceChars</span></span>
<span data-ttu-id="e97e0-803">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-803">**Description:**</span></span>  
<span data-ttu-id="e97e0-804">Funkcja ReplaceChars Hello zamienia wszystkie wystąpienia hello ReplacePattern ciąg znaków.</span><span class="sxs-lookup"><span data-stu-id="e97e0-804">hello ReplaceChars function replaces all occurrences of characters found in hello ReplacePattern string.</span></span>

<span data-ttu-id="e97e0-805">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="e97e0-806">ciąg: tooreplace ciąg znaków.</span><span class="sxs-lookup"><span data-stu-id="e97e0-806">string: A string tooreplace characters in.</span></span>
* <span data-ttu-id="e97e0-807">ReplacePattern: ciąg zawierający słownik z tooreplace znaków.</span><span class="sxs-lookup"><span data-stu-id="e97e0-807">ReplacePattern: a string containing a dictionary with characters tooreplace.</span></span>

<span data-ttu-id="e97e0-808">Witaj format to {źródło1}: {nazwach target1}, {źródło2}: {target2}, {źródłoN}, {targetN} gdzie źródła jest hello znak toofind i obiekt docelowy hello ciąg tooreplace z.</span><span class="sxs-lookup"><span data-stu-id="e97e0-808">hello format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is hello character toofind and target hello string tooreplace with.</span></span>

<span data-ttu-id="e97e0-809">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-809">**Remarks:**</span></span>

* <span data-ttu-id="e97e0-810">Funkcja Hello przyjmuje każdego wystąpienia określonych źródeł i zastępuje je z obiektami docelowymi hello.</span><span class="sxs-lookup"><span data-stu-id="e97e0-810">hello function takes each occurrence of defined sources and replaces them with hello targets.</span></span>
* <span data-ttu-id="e97e0-811">Źródło Hello muszą być dokładnie jeden znak (unicode).</span><span class="sxs-lookup"><span data-stu-id="e97e0-811">hello source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="e97e0-812">Hello źródła nie może być pusta ani więcej niż jeden znak (Błąd analizy).</span><span class="sxs-lookup"><span data-stu-id="e97e0-812">hello source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="e97e0-813">Witaj docelowy może mieć wielu znaków, na przykład ö:oe, β:ss.</span><span class="sxs-lookup"><span data-stu-id="e97e0-813">hello target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="e97e0-814">Hello docelowym może być pusta, wskazującą znak hello powinna zostać usunięta.</span><span class="sxs-lookup"><span data-stu-id="e97e0-814">hello target can be empty indicating that hello character should be removed.</span></span>
* <span data-ttu-id="e97e0-815">Źródło Hello jest rozróżniana wielkość liter i muszą być identyczne.</span><span class="sxs-lookup"><span data-stu-id="e97e0-815">hello source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="e97e0-816">Witaj, (przecinek) i: (dwukropek) są zastrzeżone znaki i nie można zastąpić przy użyciu tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e97e0-816">hello , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="e97e0-817">Spacje i inne białe znaki w ciągu ReplacePattern hello są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="e97e0-817">Spaces and other white characters in hello ReplacePattern string are ignored.</span></span>

<span data-ttu-id="e97e0-818">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="e97e0-819">Zwraca Raksmorgas</span><span class="sxs-lookup"><span data-stu-id="e97e0-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="e97e0-820">Zwraca "ONeil" hello jeden znacznik jest zdefiniowany toobe usunięte.</span><span class="sxs-lookup"><span data-stu-id="e97e0-820">Returns "ONeil", hello single tick is defined toobe removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="e97e0-821">Prawo</span><span class="sxs-lookup"><span data-stu-id="e97e0-821">Right</span></span>
<span data-ttu-id="e97e0-822">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-822">**Description:**</span></span>  
<span data-ttu-id="e97e0-823">Funkcja prawo Hello zwraca określoną liczbę znaków od hello prawa (Zakończ) ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-823">hello Right function returns a specified number of characters from hello right (end) of a string.</span></span>

<span data-ttu-id="e97e0-824">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="e97e0-825">ciąg: hello tooreturn znaków z</span><span class="sxs-lookup"><span data-stu-id="e97e0-825">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="e97e0-826">NumChars: Liczba identyfikująca hello liczba tooreturn znaków od końca hello (po prawej) ciągu</span><span class="sxs-lookup"><span data-stu-id="e97e0-826">NumChars: a number identifying hello number of characters tooreturn from hello end (right) of string</span></span>

<span data-ttu-id="e97e0-827">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-827">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-828">Od ostatniej pozycji ciąg hello są zwracane NumChars znaki.</span><span class="sxs-lookup"><span data-stu-id="e97e0-828">NumChars characters are returned from hello last position of string.</span></span>

<span data-ttu-id="e97e0-829">Ciąg zawierający hello ostatnie numChars znaki w ciągu:</span><span class="sxs-lookup"><span data-stu-id="e97e0-829">A string containing hello last numChars characters in string:</span></span>

* <span data-ttu-id="e97e0-830">Jeśli numChars = 0, zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="e97e0-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="e97e0-831">Jeśli numChars < 0, zwraca ciąg wejściowy.</span><span class="sxs-lookup"><span data-stu-id="e97e0-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="e97e0-832">Jeśli ciąg ma wartość null, zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="e97e0-832">If string is null, return empty string.</span></span>

<span data-ttu-id="e97e0-833">Jeśli ciąg zawiera mniej znaków niż hello numer NumChars określony w, zwracany jest identyczne toostring ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-833">If string contains fewer characters than hello number specified in NumChars, a string identical toostring is returned.</span></span>

<span data-ttu-id="e97e0-834">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="e97e0-835">Zwraca wartość "Nowak".</span><span class="sxs-lookup"><span data-stu-id="e97e0-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="e97e0-836">Przytk</span><span class="sxs-lookup"><span data-stu-id="e97e0-836">RTrim</span></span>
<span data-ttu-id="e97e0-837">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-837">**Description:**</span></span>  
<span data-ttu-id="e97e0-838">Hello RTrim — funkcja usuwa spacje końcowe z ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-838">hello RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="e97e0-839">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="e97e0-840">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="e97e0-841">Zwraca "Test".</span><span class="sxs-lookup"><span data-stu-id="e97e0-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="e97e0-842">Wybierz pozycję</span><span class="sxs-lookup"><span data-stu-id="e97e0-842">Select</span></span>
<span data-ttu-id="e97e0-843">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-843">**Description:**</span></span>  
<span data-ttu-id="e97e0-844">Wszystkie wartości w atrybutu wielowartościowego (lub dane wyjściowe wyrażenia) na podstawie funkcji określony proces.</span><span class="sxs-lookup"><span data-stu-id="e97e0-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="e97e0-845">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="e97e0-846">element: reprezentuje element w hello atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="e97e0-846">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="e97e0-847">Atrybut: hello atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="e97e0-847">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="e97e0-848">wyrażenie: wyrażenie, które zwraca kolekcję wartości</span><span class="sxs-lookup"><span data-stu-id="e97e0-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="e97e0-849">warunek: dowolnej funkcji, które może przetworzyć elementu w atrybucie hello</span><span class="sxs-lookup"><span data-stu-id="e97e0-849">condition: any function that can process an item in hello attribute</span></span>

<span data-ttu-id="e97e0-850">**Przykłady:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="e97e0-851">Zwraca wszystkie wartości hello w hello atrybutów wielowartościowych faksów, po usunięciu łączniki (-).</span><span class="sxs-lookup"><span data-stu-id="e97e0-851">Return all hello values in hello multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="e97e0-852">Podziel</span><span class="sxs-lookup"><span data-stu-id="e97e0-852">Split</span></span>
<span data-ttu-id="e97e0-853">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-853">**Description:**</span></span>  
<span data-ttu-id="e97e0-854">Hello funkcja podziału oddzielone znakiem ogranicznika ciąg znaków i ułatwia wielokrotne wartości ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-854">hello Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="e97e0-855">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="e97e0-856">wartość: hello ciągu z tooseparate znak ogranicznika.</span><span class="sxs-lookup"><span data-stu-id="e97e0-856">value: hello string with a delimiter character tooseparate.</span></span>
* <span data-ttu-id="e97e0-857">Ogranicznik: pojedynczy toobe znak używany jako hello ogranicznika.</span><span class="sxs-lookup"><span data-stu-id="e97e0-857">delimiter: single character toobe used as hello delimiter.</span></span>
* <span data-ttu-id="e97e0-858">limit: maksymalną liczbę wartości, które może zwracać.</span><span class="sxs-lookup"><span data-stu-id="e97e0-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="e97e0-859">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="e97e0-860">Zwraca ciąg wielowartościowe z 2 elementami jest przydatne w przypadku hello proxyAddress atrybutu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-860">Returns a multi-valued string with 2 elements useful for hello proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="e97e0-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="e97e0-861">StringFromGuid</span></span>
<span data-ttu-id="e97e0-862">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-862">**Description:**</span></span>  
<span data-ttu-id="e97e0-863">Hello funkcji StringFromGuid trwa binarne identyfikator GUID i konwertuje ją tooa ciągu</span><span class="sxs-lookup"><span data-stu-id="e97e0-863">hello StringFromGuid function takes a binary GUID and converts it tooa string</span></span>

<span data-ttu-id="e97e0-864">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="e97e0-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="e97e0-865">StringFromSid</span></span>
<span data-ttu-id="e97e0-866">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-866">**Description:**</span></span>  
<span data-ttu-id="e97e0-867">Funkcja StringFromSid Hello konwertuje tablica bajtów zawierająca ciąg tooa identyfikator zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e97e0-867">hello StringFromSid function converts a byte array containing a security identifier tooa string.</span></span>

<span data-ttu-id="e97e0-868">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="e97e0-869">Przełącznik</span><span class="sxs-lookup"><span data-stu-id="e97e0-869">Switch</span></span>
<span data-ttu-id="e97e0-870">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-870">**Description:**</span></span>  
<span data-ttu-id="e97e0-871">Funkcja przełącznika Hello jest używany tooreturn pojedynczą wartość na podstawie ocenionych warunków.</span><span class="sxs-lookup"><span data-stu-id="e97e0-871">hello Switch function is used tooreturn a single value based on evaluated conditions.</span></span>

<span data-ttu-id="e97e0-872">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="e97e0-873">wyrażenie: wyrażenie wariant ma tooevaluate.</span><span class="sxs-lookup"><span data-stu-id="e97e0-873">expr: Variant expression you want tooevaluate.</span></span>
* <span data-ttu-id="e97e0-874">wartość: wartość toobe zwrócony, jeśli hello odpowiadającego wyrażenia jest wartość PRAWDA.</span><span class="sxs-lookup"><span data-stu-id="e97e0-874">value: Value toobe returned if hello corresponding expression is True.</span></span>

<span data-ttu-id="e97e0-875">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-875">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-876">Witaj argument funkcji przełącznika listy składa się z par wyrażeń i wartości.</span><span class="sxs-lookup"><span data-stu-id="e97e0-876">hello Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="e97e0-877">wyrażenia Hello są obliczane z tooright po lewej stronie, a jest zwracana wartość hello skojarzone z hello pierwsze wyrażenie tooevaluate tooTrue.</span><span class="sxs-lookup"><span data-stu-id="e97e0-877">hello expressions are evaluated from left tooright, and hello value associated with hello first expression tooevaluate tooTrue is returned.</span></span> <span data-ttu-id="e97e0-878">Jeśli części hello prawidłowo nie są sparowane, występuje błąd czasu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="e97e0-878">If hello parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="e97e0-879">Na przykład jeśli Wyr1 ma wartość PRAWDA, przełącznik zwraca wartość1.</span><span class="sxs-lookup"><span data-stu-id="e97e0-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="e97e0-880">Jeśli wyrażenie-1 jest wartość FAŁSZ, ale wyrażenie-2 ma wartość PRAWDA, przełącznik zwraca wartość-2 i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="e97e0-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="e97e0-881">Przełącznik zwraca rób jeśli:</span><span class="sxs-lookup"><span data-stu-id="e97e0-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="e97e0-882">Brak wyrażenia hello ma wartość True.</span><span class="sxs-lookup"><span data-stu-id="e97e0-882">None of hello expressions are True.</span></span>
* <span data-ttu-id="e97e0-883">pierwsze wyrażenie True Hello ma odpowiadającą mu wartość, która ma wartość Null.</span><span class="sxs-lookup"><span data-stu-id="e97e0-883">hello first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="e97e0-884">Przełącznik ocenia wszystkie wyrażenia, mimo że zwracany jest tylko jeden z nich.</span><span class="sxs-lookup"><span data-stu-id="e97e0-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="e97e0-885">Z tego powodu należy uważać na niepożądane skutki uboczne.</span><span class="sxs-lookup"><span data-stu-id="e97e0-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="e97e0-886">Na przykład jeśli hello oceny dowolne wyrażenie powoduje dzielenie przez zero, wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="e97e0-886">For example, if hello evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="e97e0-887">Wartość może być również hello błąd funkcji, która zwróci niestandardowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="e97e0-887">Value can also be hello Error function, which would return a custom string.</span></span>

<span data-ttu-id="e97e0-888">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="e97e0-889">Zwraca język hello używany w kilku miastach głównych, w przeciwnym razie zwraca błąd.</span><span class="sxs-lookup"><span data-stu-id="e97e0-889">Returns hello language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="e97e0-890">TRIM</span><span class="sxs-lookup"><span data-stu-id="e97e0-890">Trim</span></span>
<span data-ttu-id="e97e0-891">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-891">**Description:**</span></span>  
<span data-ttu-id="e97e0-892">Funkcja przycinania Hello usuwa spacji wiodących i końcowych białych z ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-892">hello Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="e97e0-893">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="e97e0-894">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="e97e0-895">Zwraca "Test".</span><span class="sxs-lookup"><span data-stu-id="e97e0-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="e97e0-896">Usuwa spacje dla każdej wartości w atrybucie proxyAddress hello początkowe i końcowe.</span><span class="sxs-lookup"><span data-stu-id="e97e0-896">Removes leading and trailing spaces for each value in hello proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="e97e0-897">UCase</span><span class="sxs-lookup"><span data-stu-id="e97e0-897">UCase</span></span>
<span data-ttu-id="e97e0-898">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-898">**Description:**</span></span>  
<span data-ttu-id="e97e0-899">Funkcja UCase Hello konwertuje wszystkie znaki w przypadku tooupper ciągu.</span><span class="sxs-lookup"><span data-stu-id="e97e0-899">hello UCase function converts all characters in a string tooupper case.</span></span>

<span data-ttu-id="e97e0-900">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="e97e0-901">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="e97e0-902">Zwraca "TEST".</span><span class="sxs-lookup"><span data-stu-id="e97e0-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="e97e0-903">gdzie</span><span class="sxs-lookup"><span data-stu-id="e97e0-903">Where</span></span>

<span data-ttu-id="e97e0-904">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-904">**Description:**</span></span>  
<span data-ttu-id="e97e0-905">Zwraca podzbiór wartości z atrybutu wielowartościowego (lub dane wyjściowe wyrażenia) na podstawie określonego warunku.</span><span class="sxs-lookup"><span data-stu-id="e97e0-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="e97e0-906">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="e97e0-907">element: reprezentuje element w hello atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="e97e0-907">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="e97e0-908">Atrybut: hello atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="e97e0-908">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="e97e0-909">warunek: dowolne wyrażenie, które mogą być obliczane tootrue, lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="e97e0-909">condition: any expression that can be evaluated tootrue or false</span></span>
* <span data-ttu-id="e97e0-910">wyrażenie: wyrażenie, które zwraca kolekcję wartości</span><span class="sxs-lookup"><span data-stu-id="e97e0-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="e97e0-911">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="e97e0-912">Zwróć wartości certyfikatu hello certyfikatu hello wielowartościowy atrybut użytkownika, które nie są wygasło.</span><span class="sxs-lookup"><span data-stu-id="e97e0-912">Return hello certificate values in hello multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="e97e0-913">Z</span><span class="sxs-lookup"><span data-stu-id="e97e0-913">With</span></span>
<span data-ttu-id="e97e0-914">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-914">**Description:**</span></span>  
<span data-ttu-id="e97e0-915">Hello z funkcją zapewnia toosimplify sposób złożone wyrażenie za pomocą zmiennej toorepresent Podwyrażenie, która pojawia się jeden lub więcej razy w hello wyrażenie złożone.</span><span class="sxs-lookup"><span data-stu-id="e97e0-915">hello With function provides a way toosimplify a complex expression by using a variable toorepresent a subexpression which appears one or more times in hello complex expression.</span></span>

<span data-ttu-id="e97e0-916">**Składnia:**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="e97e0-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="e97e0-917">Zmienna: reprezentuje hello wyrażenia podrzędnego.</span><span class="sxs-lookup"><span data-stu-id="e97e0-917">variable: Represents hello subexpression.</span></span>
* <span data-ttu-id="e97e0-918">Podwyrażenie: Podwyrażenie reprezentowany przez zmienną.</span><span class="sxs-lookup"><span data-stu-id="e97e0-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="e97e0-919">complexExpression: wyrażenie złożone.</span><span class="sxs-lookup"><span data-stu-id="e97e0-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="e97e0-920">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="e97e0-921">Jest funkcjonalnym odpowiednikiem:</span><span class="sxs-lookup"><span data-stu-id="e97e0-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="e97e0-922">Która zwraca tylko niewygasłe certyfikatu wartości w atrybucie certyfikatu użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="e97e0-922">Which returns only unexpired certificate values in hello userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="e97e0-923">Word</span><span class="sxs-lookup"><span data-stu-id="e97e0-923">Word</span></span>
<span data-ttu-id="e97e0-924">**Opis:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-924">**Description:**</span></span>  
<span data-ttu-id="e97e0-925">Hello Word funkcja zwraca słowa w ciągu, na podstawie parametrów opisujący hello ograniczniki toouse i tooreturn numer hello programu word.</span><span class="sxs-lookup"><span data-stu-id="e97e0-925">hello Word function returns a word contained within a string, based on parameters describing hello delimiters toouse and hello word number tooreturn.</span></span>

<span data-ttu-id="e97e0-926">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="e97e0-927">ciąg: hello tooreturn ciąg słowa.</span><span class="sxs-lookup"><span data-stu-id="e97e0-927">string: hello string tooreturn a word from.</span></span>
* <span data-ttu-id="e97e0-928">WordNumber: Liczba identyfikująca numer word powinna zostać zwrócona.</span><span class="sxs-lookup"><span data-stu-id="e97e0-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="e97e0-929">Ogranicznik: ciąg reprezentujący delimiter(s) hello, który ma być używane tooidentify słowa</span><span class="sxs-lookup"><span data-stu-id="e97e0-929">delimiters: a string representing hello delimiter(s) that should be used tooidentify words</span></span>

<span data-ttu-id="e97e0-930">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-930">**Remarks:**</span></span>  
<span data-ttu-id="e97e0-931">Każdy ciąg znaków w ciągu, rozdzielone hello jeden ze znaków hello w ograniczniki są identyfikowane jako słowa:</span><span class="sxs-lookup"><span data-stu-id="e97e0-931">Each string of characters in string separated by hello one of hello characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="e97e0-932">Jeśli liczba < 1, zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="e97e0-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="e97e0-933">Jeśli ciąg ma wartość null, zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="e97e0-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="e97e0-934">Jeśli ciąg zawiera mniej niż liczba słów lub ciąg nie zawiera słów identyfikowane przez ograniczniki, zwracany jest pustym ciągiem.</span><span class="sxs-lookup"><span data-stu-id="e97e0-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="e97e0-935">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="e97e0-935">**Example:**</span></span>  
`Word("hello quick brown fox",3," ")`  
<span data-ttu-id="e97e0-936">Zwraca "brązowy"</span><span class="sxs-lookup"><span data-stu-id="e97e0-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="e97e0-937">Zwróci "ma"</span><span class="sxs-lookup"><span data-stu-id="e97e0-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e97e0-938">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e97e0-938">Additional Resources</span></span>
* [<span data-ttu-id="e97e0-939">Opis deklaratywne wyrażenia inicjowania obsługi administracyjnej</span><span class="sxs-lookup"><span data-stu-id="e97e0-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="e97e0-940">Azure AD Connect Sync: Dostosowywanie opcji synchronizacji</span><span class="sxs-lookup"><span data-stu-id="e97e0-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="e97e0-941">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e97e0-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
