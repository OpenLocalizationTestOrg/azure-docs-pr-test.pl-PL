

## <a name="deployment-considerations"></a>Zagadnienia dotyczące wdrażania
* **Subskrypcja platformy Azure** — toodeploy więcej niż kilka wystąpień obliczeniowych, należy rozważyć inne opcje zakupu lub z subskrypcji. Jeśli używasz [bezpłatnego konta platformy Azure](https://azure.microsoft.com/free/), możesz użyć ograniczonej liczby rdzeni obliczeniowych platformy Azure.

* **Cennik i dostępności** -rozmiarów maszyn wirtualnych te są dostępne tylko w warstwy cenowej standardowa hello. Sprawdź [produkty dostępne według regionu] (https://azure.microsoft.com/regions/services/) dostępności w regionach platformy Azure. 
* **Limit przydziału rdzeni** — limit przydziału rdzeni hello tooincrease może być konieczne w Twojej subskrypcji platformy Azure z hello wartości domyślnej. Subskrypcji może również ograniczać hello liczba rdzeni, którą można wdrożyć w niektórych rodzin rozmiar maszyny Wirtualnej, włączając hello H-series. Zwiększ limit przydziału toorequest [otwarcia żądania pomocy technicznej online klienta](../articles/azure-supportability/how-to-create-azure-support-request.md) bez dodatkowych opłat. (Domyślne limity może się różnić w zależności od kategorii subskrypcji).
  
  > [!NOTE]
  > Jeśli masz wymagana pojemność na dużą skalę, skontaktuj się z pomocą techniczną platformy Azure. Przydziały Azure są środki ogranicza nie gwarantuje pojemności. Niezależnie od limitu przydziału naliczane są tylko opłaty dla rdzeni użycie.
  > 
  > 
* **Sieć wirtualna** — moduł Azure [sieci wirtualnej](https://azure.microsoft.com/documentation/services/virtual-network/) jest toouse niewymagane hello obliczeniowych wystąpień. Jednak w przypadku wielu wdrożeń należy co najmniej oparte na chmurze sieci wirtualnej platformy Azure lub połączenie lokacja lokacja, jeśli potrzebujesz tooaccess zasobów lokalnych. W razie potrzeby utwórz nową sieć wirtualną toodeploy hello wystąpień. Dodawanie sieci wirtualnej tooa obliczeniowych maszyn wirtualnych w grupie koligacji nie jest obsługiwane.
* **Zmiana rozmiaru** — ze względu na ich specjalne sprzętu można rozmiaru wystąpień obliczeniowych w hello sam rozmiar rodziny (serii H lub obliczeniowych A-series). Na przykład można zmienić tylko wirtualna H-series z jednego tooanother rozmiar H serii. Ponadto zmiana rozmiaru z innych niż — obliczeniowych tooa obliczeniowych rozmiar pamięci nie jest obsługiwana.  
