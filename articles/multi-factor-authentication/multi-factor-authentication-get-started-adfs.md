---
title: "krok aaaTwo weryfikacji i usług AD FS — usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Jest to hello Azure Multi-Factor authentication strony, opisujące, jak tooget pracę z usługą Azure MFA i usług AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="49242-103">Wprowadzenie do usługi Azure Multi-Factor Authentication i usług Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="49242-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="49242-104"><center>![Chmura](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="49242-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="49242-105">W przypadku organizacji, które sfederowały lokalną usługę Active Directory z usługą Azure Active Directory za pomocą usług AD FS, dostępne są dwie opcje używania usługi Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="49242-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="49242-106">Zabezpieczenie zasobów w chmurze za pomocą usługi Azure Multi-Factor Authentication lub usług Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="49242-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="49242-107">Zabezpieczenie zasobów w chmurze i zasobów lokalnych przy użyciu serwera usługi Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="49242-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="49242-108">Witaj w poniższej tabeli znajduje się podsumowanie hello weryfikacji środowisko obejmujące zabezpieczanie zasobów przy użyciu usługi Azure Multi-Factor Authentication i usług AD FS</span><span class="sxs-lookup"><span data-stu-id="49242-108">hello following table summarizes hello verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="49242-109">Proces weryfikacji — aplikacje korzystające z przeglądarki</span><span class="sxs-lookup"><span data-stu-id="49242-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="49242-110">Proces weryfikacji — aplikacje niekorzystające z przeglądarki</span><span class="sxs-lookup"><span data-stu-id="49242-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="49242-111">Zabezpieczanie zasobów usługi Azure AD za pomocą usługi Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="49242-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="49242-112">pierwszym krokiem weryfikacji Hello jest wykonywane lokalnie za pomocą usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="49242-112">hello first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="49242-113">drugim krokiem Hello to metoda telefoniczną przeprowadzane przy użyciu uwierzytelniania w chmurze.</span><span class="sxs-lookup"><span data-stu-id="49242-113">hello second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="49242-114">Zabezpieczanie zasobów usługi Azure AD za pomocą usług Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="49242-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="49242-115">pierwszym krokiem weryfikacji Hello jest wykonywane lokalnie za pomocą usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="49242-115">hello first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="49242-116">drugi etap Hello jest realizowany lokalnie przy zachowaniu hello oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="49242-116">hello second step is performed on-premises by honoring hello claim.</span></span></li> |

<span data-ttu-id="49242-117">Zastrzeżenia dotyczące haseł aplikacji używanych przez użytkowników federacyjnych:</span><span class="sxs-lookup"><span data-stu-id="49242-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="49242-118">Hasła aplikacji są weryfikowane przy użyciu uwierzytelniania w chmurze, co pozwala pominąć federację.</span><span class="sxs-lookup"><span data-stu-id="49242-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="49242-119">Federacja jest aktywnie używana tylko podczas konfigurowania hasła aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49242-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="49242-120">Ustawienia lokalnej kontroli dostępu klienta nie są uznawane przez hasła aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49242-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="49242-121">Nie będzie można lokalnie rejestrować uwierzytelniania haseł aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49242-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="49242-122">Wyłączenie/usunięcie konta może trwać toothree godzin synchronizacji katalogów, opóźnienie wyłączenia/usunięcia hasła aplikacji w hello tożsamość w chmurze.</span><span class="sxs-lookup"><span data-stu-id="49242-122">Account disable/deletion may take up toothree hours for directory sync, delaying disable/deletion of app passwords in hello cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49242-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="49242-123">Next steps</span></span>
<span data-ttu-id="49242-124">Aby uzyskać informacje na temat konfigurowania usługi Azure Multi-Factor Authentication lub powitania serwera usługi Azure Multi-Factor Authentication z usługami AD FS zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="49242-124">For information on setting up either Azure Multi-Factor Authentication or hello Azure Multi-Factor Authentication Server with AD FS, see hello following articles:</span></span>

* [<span data-ttu-id="49242-125">Zabezpieczanie zasobów w chmurze przy użyciu usługi Azure Multi-Factor Authentication i usług AD FS</span><span class="sxs-lookup"><span data-stu-id="49242-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="49242-126">Zabezpieczanie zasobów w chmurze i lokalnych przy użyciu serwera usługi Azure Multi-Factor Authentication i usług AD FS systemu Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="49242-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="49242-127">Zabezpieczanie zasobów w chmurze i zasobów lokalnych przy użyciu serwera usługi Azure Multi-Factor Authentication i usług AD FS 2.0</span><span class="sxs-lookup"><span data-stu-id="49242-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
