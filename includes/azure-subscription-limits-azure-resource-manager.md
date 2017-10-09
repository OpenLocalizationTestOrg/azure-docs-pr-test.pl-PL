| Zasób | Limit domyślny | Limit maksymalny |
| --- | --- | --- |
| Maszyny wirtualne na [subskrypcję](../articles/billing-buy-sign-up-azure-subscription.md) |10 000 <sup>1</sup> na region |10 000 na region |
| Całkowita liczba rdzeni maszyn wirtualnych na [subskrypcję](../articles/billing-buy-sign-up-azure-subscription.md) |20<sup>1</sup> na region | Kontakt z pomocą techniczną |
| Liczba rdzeni maszyn wirtualnych na serię (Dv2, F itp.) na [subskrypcję](../articles/billing-buy-sign-up-azure-subscription.md) |20<sup>1</sup> na region | Kontakt z pomocą techniczną |
| [Współadministratorzy](../articles/billing-add-change-azure-subscription-administrator.md) na subskrypcję |Nieograniczona liczba |Nieograniczona liczba |
| [Konta magazynu](../articles/storage/common/storage-create-storage-account.md) na subskrypcję |200 |200<sup>2</sup> |
| [Grupy kontenerów](../articles/azure-resource-manager/resource-group-overview.md) na subskrypcję |800 |800 |
| [Zestawy dostępności](../articles/virtual-machines/windows/manage-availability.md#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy) na subskrypcję |2000 na region |2000 na region |
| Odczyty interfejsu API usługi Resource Manager |15 000 na godzinę |15 000 na godzinę |
| Zapisy interfejsu API usługi Resource Manager |1200 na godzinę |1200 na godzinę |
| Rozmiar żądania interfejsu API usługi Resource Manager |4 194 304 bajty |4 194 304 bajty |
| Tagi na subskrypcję<sup>3</sup> |bez ograniczeń |bez ograniczeń |
| Obliczenia unikatowych tagów na subskrypcję<sup>3</sup> | 10 000 | 10 000 |
| [Usługi w chmurze](../articles/cloud-services/cloud-services-choose-me.md) na subskrypcję |Nie dotyczy<sup>4</sup> |Nie dotyczy<sup>4</sup> |
| [Grupy koligacji](../articles/virtual-network/virtual-networks-migrate-to-regional-vnet.md) na subskrypcję |Nie dotyczy<sup>4</sup> |Nie dotyczy<sup>4</sup> |

<sup>1</sup>Domyślne limity zależą od typu kategorii oferty, na przykład „bezpłatna wersja próbna”, „płatność zgodnie z rzeczywistym użyciem” i serii, na przykład Dv2, F, G itd.

<sup>2</sup>Obejmuje konta magazynu warstwy Standardowa i Premium. Jeśli potrzebujesz więcej niż 200 kont magazynu, wyślij żądanie za pośrednictwem [Pomocy technicznej platformy Azure](https://azure.microsoft.com/support/faq/). Hello Azure Storage team przejrzeć tej sprawy biznesowych i może zatwierdzić too250 kont magazynu.

<sup>3</sup>Liczba tagów, które można zastosować na subskrypcję, nie jest ograniczona. Hello liczba tagów na zasób lub grupa zasobów jest ograniczona too15. Zwraca tylko Menedżera zasobów [listę unikatową nazwę znacznika i wartości](/rest/api/resources/tags#Tags_List) w subskrypcji powitania po 10 000 lub mniej hello liczba tagów. Jednak można nadal znaleźć zasób w tagu gdy numer hello przekracza 10 000.  

<sup>4</sup>te funkcje nie są już wymagane z grup zasobów platformy Azure i hello Azure Resource Manager.

> [!NOTE]
> Jest ważne tooemphasize, który rdzeni maszyny wirtualnej ma regionalnych całkowitego limitu, a także regionalne limit rozmiaru serii (Dv2, F, itp.), który oddzielnie są wymuszane na.  Rozważmy na przykład subskrypcję z całkowitym limitem rdzeni maszyn wirtualnych dla regionu Wschodnie stany USA wynoszącym 30, limitem rdzeni dla serii A wynoszącym 30 i limitem rdzeni dla serii D wynoszącym 30.  Ta subskrypcja mogliby maszyn wirtualnych A1 toodeploy 30 lub 30 D1 maszyn wirtualnych lub kombinację Witaj dwie tooexceed łączną liczbę rdzeni 30 (na przykład 10 A1 maszyn wirtualnych i 20 D1 maszyn wirtualnych).  
> <!-- -->
> 
> 

