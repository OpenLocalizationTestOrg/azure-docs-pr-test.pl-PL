---
title: "aaaAzure referencyjne protokołu AD SAML | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie profile rejestracji jednokrotnej i jednym SAML Sign-Out hello w usłudze Azure Active Directory."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 88125cfc-45c1-448b-9903-a629d8f31b01
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.openlocfilehash: d540b8cd9352e3196a0f4a40f0070d0e61127bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Jak Azure Active Directory korzysta z protokołu SAML hello
Azure Active Directory (Azure AD) używa hello tooenable protokołu SAML 2.0 aplikacji użytkownicy tootheir środowisko tooprovide rejestracji jednokrotnej. Hello [rejestracji jednokrotnej](active-directory-single-sign-on-protocol-reference.md) i [jednym wylogowania](active-directory-single-sign-out-protocol-reference.md) SAML profilów usługi Azure AD wyjaśniają, jak SAML potwierdzeń, protokołów i powiązania są używane w hello tożsamości dostawcy usługi.

Protokół SAML wymaga hello dostawcy tożsamości (Azure AD) i hello usługi dostawcy (aplikacja hello) tooexchange informacje o sobie.

Gdy aplikacja jest zarejestrowana w usłudze Azure AD, Deweloper aplikacji hello rejestruje informacje związane z federacji z usługą Azure AD. Dotyczy to również hello **identyfikator URI przekierowania** aplikacji hello.

Usługa Azure Active Directory udostępnia specyficznego dla dzierżawy i wspólne (niezależny od dzierżawcy) pojedynczego logowania jednokrotnego i pojedynczego wylogowania punktów końcowych. Te adresy URL reprezentują lokalizacje adresowanego — nie są one tylko identyfikatory —, możesz przejść toohello punktu końcowego tooread hello metadanych.

* punkt końcowy Hello specyficznego dla dzierżawy znajduje się pod adresem `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.  Witaj <TenantDomainName> symbol zastępczy reprezentuje zarejestrowaną nazwę domeny lub identyfikator GUID dzierżawy usługi Azure AD dla identyfikatora dzierżawcy. Na przykład, metadanych Federacji hello hello contoso.com dzierżawy jest w: https://login.microsoftonline.com/contoso.com/FederationMetadata/2007-06/FederationMetadata.xml

* punkt końcowy Hello niezależny od dzierżawcy znajduje się pod adresem `https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml`. W tym adres punktu końcowego **wspólnej** zostanie wyświetlony, a nie nazwę domeny dzierżawy lub identyfikator.

Aby dowiedzieć się, dokumentów metadanych Federacji hello publikuje usługi Azure AD, zobacz [metadanych Federacji](active-directory-federation-metadata.md).
