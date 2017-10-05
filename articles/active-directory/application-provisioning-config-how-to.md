---
title: "Jak skonfigurować Inicjowanie obsługi użytkowników dla aplikacji w galerii Azure AD | Dokumentacja firmy Microsoft"
description: "Jak można szybko skonfigurować konto użytkownika sformatowanego alokowania i anulowania alokowania aplikacjom wymienione w galerii aplikacji usługi Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2e38fcb30ea7632339a3ba8815a536872cfcc69e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-user-provisioning-to-an-azure-ad-gallery-application"></a><span data-ttu-id="67cac-103">Jak skonfigurować Inicjowanie obsługi użytkowników dla aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="67cac-103">How to configure user provisioning to an Azure AD Gallery application</span></span>

<span data-ttu-id="67cac-104">*Inicjowanie obsługi konta użytkownika* polega na tworzenie, aktualizowanie i/lub wyłączenie rekordów konta użytkowników w magazynie profil lokalny użytkownika aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67cac-104">*User account provisioning* is the act of creating, updating, and/or disabling user account records in an application’s local user profile store.</span></span> <span data-ttu-id="67cac-105">Większość chmury i aplikacji SaaS przechowywać role użytkowników i uprawnienia własny magazyn profilu użytkownika lokalnego, a jest obecność takich rekordu użytkownika w lokalnym magazynie *wymagane* potrzeby logowania jednokrotnego i uzyskiwania dostępu do pracy.</span><span class="sxs-lookup"><span data-stu-id="67cac-105">Most cloud and SaaS applications store the users role and permissions in their own local user profile store, and presence of such a user record in their local store is *required* for single sign-on and access to work.</span></span>

<span data-ttu-id="67cac-106">W portalu Azure **inicjowania obsługi administracyjnej** karcie w lewym okienku nawigacji dla aplikacji przedsiębiorstwa Wyświetla, jakie tryby inicjowania obsługi administracyjnej są obsługiwane dla danej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67cac-106">In the Azure portal, the **Provisioning** tab in the left navigation pane for an Enterprise App displays what provisioning modes are supported for that app.</span></span> <span data-ttu-id="67cac-107">Może to być jedną z dwóch wartości:</span><span class="sxs-lookup"><span data-stu-id="67cac-107">This can be one of two values:</span></span>

## <a name="configuring-an-application-for-manual-provisioning"></a><span data-ttu-id="67cac-108">Konfigurowanie aplikacji do ręcznego inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="67cac-108">Configuring an application for Manual Provisioning</span></span>

<span data-ttu-id="67cac-109">*Ręczne* inicjowania obsługi administracyjnej oznacza, że należy utworzyć konta użytkownika ręcznie przy użyciu metody dostarczone przez danej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67cac-109">*Manual* provisioning means that user accounts must be created manually using the methods provided by that app.</span></span> <span data-ttu-id="67cac-110">Może to oznaczać logowania do portalu administracyjnego dla danej aplikacji i dodawanie użytkowników przy użyciu interfejsu użytkownika opartego na sieci web.</span><span class="sxs-lookup"><span data-stu-id="67cac-110">This could mean logging into an administrative portal for that app and adding users using a web-based user interface.</span></span> <span data-ttu-id="67cac-111">Lub może być przekazywania arkusz kalkulacyjny zawierający szczegółów konta użytkownika, przy użyciu mechanizmu udostępniane przez tę aplikację.</span><span class="sxs-lookup"><span data-stu-id="67cac-111">Or it could be uploading a spreadsheet with user account detail, using a mechanism provided by that application.</span></span> <span data-ttu-id="67cac-112">Zapoznaj się z dokumentacją dostarczoną przez aplikację, lub skontaktuj się z deweloperem aplikacji, aby określić, czy mechanizmy wat są dostępne.</span><span class="sxs-lookup"><span data-stu-id="67cac-112">Consult the documentation provided by the app, or contact the app developer to determine wat mechanisms are available.</span></span>

<span data-ttu-id="67cac-113">Podręcznik jest tylko tryb wyświetlany dla danej aplikacji, oznacza, że nie usługi Azure AD automatycznego inicjowania obsługi administracyjnej łącznik został utworzony dla aplikacji jeszcze.</span><span class="sxs-lookup"><span data-stu-id="67cac-113">If Manual is the only mode shown for a given application, it means that no automatic Azure AD provisioning connector has been created for the app yet.</span></span> <span data-ttu-id="67cac-114">Lub oznacza to, że aplikacja nie obsługuje interfejsu API zarządzania wstępnych użytkownika, na których można utworzyć łącznik automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="67cac-114">Or it means the app does not support the pre-requisite user management API upon which to build an automated provisioning connector.</span></span>

<span data-ttu-id="67cac-115">Jeśli chcesz zażądać pomocy technicznej dla automatyczne Inicjowanie obsługi administracyjnej dla danej aplikacji, możesz też wypełnić żądania w <http://aka.ms/aadapprequest>.</span><span class="sxs-lookup"><span data-stu-id="67cac-115">If you would like to request support for automatic provisioning for a given app, you can fill out a request at <http://aka.ms/aadapprequest>.</span></span>

## <a name="configuring-an-application-for-automatic-provisioning"></a><span data-ttu-id="67cac-116">Konfigurowanie aplikacji do automatycznego inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="67cac-116">Configuring an application for Automatic Provisioning</span></span>

<span data-ttu-id="67cac-117">*Automatyczne* oznacza, że usługi Azure AD, inicjowania obsługi administracyjnej łącznik został opracowany dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67cac-117">*Automatic* means that an Azure AD provisioning connector has been developed for this application.</span></span> <span data-ttu-id="67cac-118">Aby uzyskać więcej informacji o usłudze Azure AD, inicjowania obsługi administracyjnej usługi oraz sposób jej działania, zobacz [zautomatyzować Inicjowanie obsługi użytkowników i anulowania zastrzeżenia do aplikacji SaaS w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span><span class="sxs-lookup"><span data-stu-id="67cac-118">For more information on the Azure AD provisioning service and how it works, see [Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span></span>

<span data-ttu-id="67cac-119">Aby uzyskać więcej informacji na temat sposobu obsługi administracyjnej konkretnych użytkowników i grup do aplikacji, zobacz [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span><span class="sxs-lookup"><span data-stu-id="67cac-119">For more information on how to provision specific users and groups to an application, see [Managing user account provisioning for enterprise apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span></span>

<span data-ttu-id="67cac-120">Rzeczywiste kroki wymagane do włączania i konfigurowania automatyczne udostępnianie się różnić w zależności od aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67cac-120">The actual steps required to enable and configure automatic provisioning vary depending on the application.</span></span>

>[!NOTE]
><span data-ttu-id="67cac-121">Należy zacząć od znajdowanie samouczek ustawień dotyczących przygotowywania Inicjowanie obsługi administracyjnej dla aplikacji, a także następujące te kroki konfigurowania aplikacji i usługi Azure AD, aby utworzyć połączenie inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="67cac-121">You should start by finding the setup tutorial specific to setting up provisioning for your application, and following those steps to configure both the app and Azure AD to create the provisioning connection.</span></span> 
>
>

<span data-ttu-id="67cac-122">Samouczki aplikacji można znaleźć w folderze [listy samouczki dotyczące integracji aplikacji SaaS w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span><span class="sxs-lookup"><span data-stu-id="67cac-122">App tutorials can be found at [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span></span>

<span data-ttu-id="67cac-123">Ważne jest, aby uwzględnić podczas konfigurowania udostępniania można przejrzeć i skonfigurować mapowanie atrybutów i przepływów pracy, określających, które użytkownik (lub grupa) właściwości przepływu z usługi Azure AD do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67cac-123">An important thing to consider when setting up provisioning be to review and configure the attribute mappings and workflows that define which user (or group) properties flow from Azure AD to the application.</span></span> <span data-ttu-id="67cac-124">Dotyczy to również ustawienie "zgodnej właściwości" używany do jednoznacznego identyfikowania i odpowiada użytkowników/grupy między tymi dwoma systemami.</span><span class="sxs-lookup"><span data-stu-id="67cac-124">This includes setting the “matching property” that be used to uniquely identify and match users/groups between the two systems.</span></span> <span data-ttu-id="67cac-125">Aby uzyskać więcej informacji na ten proces ważne.</span><span class="sxs-lookup"><span data-stu-id="67cac-125">For more information on this important process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67cac-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="67cac-126">Next steps</span></span>
[<span data-ttu-id="67cac-127">Dostosowywanie użytkownika udostępniania mapowań atrybutów dla aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67cac-127">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

