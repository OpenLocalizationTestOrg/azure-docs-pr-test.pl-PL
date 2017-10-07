---
title: "aaaWhat jest usługa Azure Key Vault? | Microsoft Docs"
description: "Usługa Azure Key Vault ułatwia ochronę kluczy kryptograficznych i kluczy tajnych używanych przez aplikacje i usługi w chmurze. Za pomocą usługi Azure Key Vault klient może szyfrować klucze i klucze tajne (takie jak klucze uwierzytelniania, klucze konta magazynu, klucze szyfrowania danych, pliki PFX oraz hasła) przy użyciu kluczy chronionych przez sprzętowe moduły zabezpieczeń (HSM, hardware security module)."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e759df6f-0638-43b1-98ed-30b3913f9b82
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 296fcce03658b96b84afab299b73681bbe8ac9fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-key-vault"></a>Co to jest usługa Azure Key Vault?
Usługa Azure Key Vault jest dostępna w większości regionów. Aby uzyskać więcej informacji, zobacz hello [cennik usługi Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Wprowadzenie
Usługa Azure Key Vault ułatwia ochronę kluczy kryptograficznych i kluczy tajnych używanych przez aplikacje i usługi w chmurze. Za pomocą usługi Key Vault możesz szyfrować klucze i klucze tajne (takie jak klucze uwierzytelniania, klucze konta magazynu, klucze szyfrowania danych, pliki PFX oraz hasła) przy użyciu kluczy chronionych przez sprzętowe moduły zabezpieczeń (HSM, hardware security module). W celu zapewnienia dodatkowego bezpieczeństwa możesz zaimportować lub wygenerować klucze w modułach HSM. Jeśli wybierzesz toodo procesów, Microsoft klucze w trybie FIPS 140-2 poziom 2 HSM zweryfikowanych (sprzęt i oprogramowanie układowe).  

Key Vault usprawnia proces zarządzania kluczami hello i umożliwia toomaintain kontrolę nad kluczami, które dostępu i szyfrowania danych. Deweloperzy mogą utworzyć klucze do programowania i testowania w minutach, a następnie bezproblemowo przeprowadzić ich migrację tooproduction kluczy. Administratorzy zabezpieczeń można przydzielić (lub odwołania) tookeys uprawnienia, zgodnie z potrzebami.

Użyj powitania po toobetter tabeli zrozumieć, jak usługi Key Vault może pomóc toomeet hello potrzeb deweloperom i administratorom zabezpieczeń.

| Rola | Opis problemu | Rozwiązanie usługi Azure Key Vault |
| --- | --- | --- |
| Deweloper aplikacji platformy Azure |"Chcę toowrite aplikacji dla platformy Azure, która używa kluczy do podpisywania i szyfrowania, ale chcę toobe te klucze zewnętrznych z mojej aplikacji tak, aby hello rozwiązanie jest odpowiednie dla aplikacji rozproszonej geograficznie. <br/><br/>Chcę także tych kluczy i kluczy tajnych toobe chroniony, bez konieczności toowrite hello kod samodzielnie. Również ma toobe tych kluczy i kluczy tajnych łatwe dla mnie toouse w moich aplikacjach z optymalną wydajnością." |√ Klucze są przechowywane w magazynie i w razie potrzeby wywoływane przez identyfikator URI.<br/><br/> √ Klucze są chronione przez platformę Azure przy użyciu branżowych standardów dotyczących algorytmów, długości klucza i sprzętowych modułów zabezpieczeń (HSM).<br/><br/> √ Klucze są przetwarzane w sprzętowych modułów zabezpieczeń, które znajdują się w hello takie same centrach danych platformy Azure jako aplikacji hello. Zapewnia to większą niezawodność i mniejsze opóźnienia niż Jeśli klucze hello znajdują się w innej lokalizacji, takich jak lokalnie. |
| Deweloper oprogramowania jako usługi (SaaS) |"Nie chcę hello odpowiedzialności lub potencjalne odpowiedzialności kluczy dzierżawy moich klientów i kluczy tajnych. <br/><br/>Chcę tooown klientom Witaj, dzięki czemu można I skoncentrować się na ten co robię najlepiej, która dostarcza hello podstawowych funkcji oprogramowania, zarządzać swoimi kluczami." |√ Klienci mogą importować własne klucze do platformy Azure i zarządzać nimi. Gdy aplikacja SaaS musi tooperform operacje kryptograficzne przy użyciu kluczy swoich klientów, usługa Key Vault robi te operacje w imieniu aplikacji hello. Aplikacja Hello nie widzieć klientom Witaj kluczy. |
| Chief Security Officer (CSO) |"Chcę tooknow, że nasze aplikacje są zgodne z sprzętowych modułów zabezpieczeń FIPS 140-2 poziom 2 w celu bezpiecznego zarządzania kluczami. <br/><br/>Chcę się upewnić, że Moja organizacja to kontrolę nad cyklem życia kluczy hello toomake, można monitorować użycie klucza. <br/><br/>I chociaż korzystamy z wielu usług platformy Azure i zasoby, ma klucze hello toomanage z jednej lokalizacji na platformie Azure". |√ Moduły HSM są zweryfikowane w trybie FIPS 140-2 poziom 2.<br/><br/>√ Usługa Key Vault jest zaprojektowana w taki sposób, aby firma Microsoft nie miała wglądu w Twoje klucze ani nie mogła ich wyodrębnić.<br/><br/>√ Rejestrowanie użycia klucza niemal w czasie rzeczywistym.<br/><br/>√ Magazyn hello udostępnia jeden interfejs, niezależnie od tego, jak wiele magazynów masz na platformie Azure, które regiony one pomocy technicznej i które aplikacje ich używają. |

Każdy posiadacz subskrypcji Azure może tworzyć magazyny kluczy i z nich korzystać. Mimo że usługa Key Vault przynosi korzyści głównie deweloperom i administratorom zabezpieczeń, może być wdrażana i zarządzana przez administratora organizacji, który zarządza innymi usługami platformy Azure dla organizacji. Na przykład administrator będzie Zaloguj się przy użyciu subskrypcji platformy Azure, utwórz magazyn dla organizacji hello w klawisze toostore i następnie odpowiadać dla zadań operacyjnych, takich jak:

* Tworzenie lub importowanie klucza lub klucza tajnego
* Odwoływanie lub usuwanie klucza lub klucza tajnego
* Autoryzowanie użytkowników lub aplikacje tooaccess hello magazynu kluczy, więc można następnie zarządzać lub używać jej kluczy i kluczy tajnych
* Konfigurowanie użycia klucza (na przykład rejestrowanie lub szyfrowanie)
* Monitorowanie użycia klucza

Administrator może następnie dostarczyć deweloperom identyfikatory URI toocall z poziomu ich aplikacji i dostarczyć administratorom zabezpieczeń informacje o rejestrowaniu użycia klucza. 

   ![Omówienie usługi Azure Key Vault][1]

Deweloperzy można również zarządzać kluczami hello bezpośrednio, za pomocą interfejsów API. Aby uzyskać więcej informacji, zobacz [hello przewodnik dewelopera usługi Key Vault](key-vault-developers-guide.md).

## <a name="next-steps"></a>Następne kroki
Aby zapoznać się z samouczkiem wprowadzającym dla administratora, zobacz [Wprowadzenie do usługi Azure Key Vault](key-vault-get-started.md).

Aby uzyskać więcej informacji na temat rejestrowania użycia usługi Key Vault, zobacz [Rejestrowanie usługi Azure Key Vault](key-vault-logging.md).

Aby uzyskać więcej informacji na temat używania kluczy i kluczy tajnych w usłudze Azure Key Vault, zobacz [Informacje o kluczach, kluczach tajnych i certyfikatach](https://msdn.microsoft.com/library/azure/dn903623\(v=azure.1\).aspx).

<!--Image references-->
[1]: ./media/key-vault-whatis/AzureKeyVault_overview.png
