---
title: "Synchronizacja programu Azure AD Connect: Włączanie Kosza AD | Dokumentacja firmy Microsoft"
description: "W tym temacie zaleca się używanie hello funkcji Kosz usługi AD z programem Azure AD Connect."
services: active-directory
keywords: "Kosz usługi AD, przypadkowego usunięcia, zakotwiczenie źródła"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="8587f-104">Synchronizacja programu Azure AD Connect: Włączanie Kosza usługi AD</span><span class="sxs-lookup"><span data-stu-id="8587f-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="8587f-105">Zaleca się włączenie funkcji Kosza hello AD dla katalogów Active lokalnych, które są synchronizowane tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="8587f-105">It is recommended that you enable hello AD Recycle Bin feature for your on-premises Active Directories, which are synchronized tooAzure AD.</span></span> 

<span data-ttu-id="8587f-106">Jeśli przypadkowo usunięto lokalnego obiektu użytkownika usługi Active Directory i przywracania go za pomocą funkcji hello Azure AD przywraca hello odpowiedni obiekt użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8587f-106">If you accidentally deleted an on-premises AD user object and restore it using hello feature, Azure AD restores hello corresponding Azure AD user object.</span></span>  <span data-ttu-id="8587f-107">Informacje dotyczące funkcji Kosza hello AD, można znaleźć w temacie tooarticle [omówienie scenariusza dla Przywracanie usunięte obiekty usługi Active Directory](https://technet.microsoft.com/library/dd379542.aspx).</span><span class="sxs-lookup"><span data-stu-id="8587f-107">For information about hello AD Recycle Bin feature, refer tooarticle [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a><span data-ttu-id="8587f-108">Korzyści hello AD włączania Kosza</span><span class="sxs-lookup"><span data-stu-id="8587f-108">Benefits of enabling hello AD recycle bin</span></span>
<span data-ttu-id="8587f-109">Ta funkcja pomaga z przywracaniem obiekty użytkownika usługi Azure AD, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="8587f-109">This feature helps with restoring Azure AD user objects by doing hello following:</span></span>

* <span data-ttu-id="8587f-110">Jeśli przypadkowo usunięto lokalnego obiektu użytkownika AD, hello odpowiedni obiekt użytkownika usługi Azure AD zostaną usunięte w hello następnego cyklu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="8587f-110">If you accidentally deleted an on-premises AD user object, hello corresponding Azure AD user object will be deleted in hello next sync cycle.</span></span> <span data-ttu-id="8587f-111">Domyślnie usługi Azure AD przechowuje obiekt użytkownika usługi Azure AD hello usunięte w stanie usunięte nietrwale przez 30 dni.</span><span class="sxs-lookup"><span data-stu-id="8587f-111">By default, Azure AD keeps hello deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="8587f-112">Jeśli masz lokalnej włączona funkcja Kosz usługi AD, można przywrócić usunięty hello lokalnymi obiektu użytkownika usługi Active Directory bez modyfikowania jej wartość zakotwiczenie źródła.</span><span class="sxs-lookup"><span data-stu-id="8587f-112">If you have on-premises AD Recycle Bin feature enabled, you can restore hello deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="8587f-113">Gdy hello odzyskane lokalnymi obiektu użytkownika usługi Active Directory jest zsynchronizowany tooAzure AD, Azure AD spowoduje przywrócenie hello odpowiadającego wszystkie usunięte nietrwale obiektu użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8587f-113">When hello recovered on-premises AD user object is synchronized tooAzure AD, Azure AD will restore hello corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="8587f-114">Informacje o atrybut zakotwiczenia źródła można znaleźć tooarticle [Azure AD Connect: zagadnienia dotyczące projektowania](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="8587f-114">For information about Source Anchor attribute, refer tooarticle [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="8587f-115">Jeśli nie masz lokalnego AD Odtwórz włączona funkcja Bin, może być wymagane toocreate AD obiektu tooreplace hello usuniętego obiektu user.</span><span class="sxs-lookup"><span data-stu-id="8587f-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required toocreate an AD user object tooreplace hello deleted object.</span></span> <span data-ttu-id="8587f-116">Jeśli usługi Azure AD Connect synchronizacji usługi skonfigurowanego toouse generowanych przez system AD atrybutu (na przykład ObjectGuid) dla atrybutu zakotwiczenia źródła hello, hello nowo utworzony obiekt użytkownika usługi Active Directory zostanie nie ma hello tę samą wartość zakotwiczenie źródła jako hello usunięty obiekt użytkownika usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8587f-116">If Azure AD Connect Synchronization Service is configured toouse system-generated AD attribute (such as ObjectGuid) for hello Source Anchor attribute, hello newly created AD user object will not have hello same Source Anchor value as hello deleted AD user object.</span></span> <span data-ttu-id="8587f-117">Gdy hello nowo utworzony obiekt użytkownika usługi Active Directory jest synchronizowane tooAzure AD, Azure AD tworzy nowy obiekt użytkownika usługi Azure AD zamiast Przywracanie obiektu user hello wszystkie usunięte nietrwale usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8587f-117">When hello newly created AD user object is synchronized tooAzure AD, Azure AD creates a new Azure AD user object instead of restoring hello soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="8587f-118">Domyślnie usługi Azure AD przechowuje usunięte obiekty użytkownika usługi Azure AD w stanie usunięte nietrwale przez 30 dni, zanim zostaną trwale usunięte.</span><span class="sxs-lookup"><span data-stu-id="8587f-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="8587f-119">Jednak Administratorzy może przyspieszyć hello usuwanie tych obiektów.</span><span class="sxs-lookup"><span data-stu-id="8587f-119">However, administrators can accelerate hello deletion of such objects.</span></span> <span data-ttu-id="8587f-120">Po hello obiekty zostaną trwale usunięte, nie mogą zostać odzyskane, nawet jeśli lokalne się, że włączono funkcję Kosz usługi AD.</span><span class="sxs-lookup"><span data-stu-id="8587f-120">Once hello objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="8587f-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8587f-121">Next steps</span></span>
<span data-ttu-id="8587f-122">**Tematy poglądowe**</span><span class="sxs-lookup"><span data-stu-id="8587f-122">**Overview topics**</span></span>

* [<span data-ttu-id="8587f-123">Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji</span><span class="sxs-lookup"><span data-stu-id="8587f-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="8587f-124">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8587f-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
