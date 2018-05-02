### <a name="listsort-algorithm-changed"></a><span data-ttu-id="65193-101">Der List.Sort-Algorithmus wurde geändert</span><span class="sxs-lookup"><span data-stu-id="65193-101">List.Sort algorithm changed</span></span>

|   |   |
|---|---|
|<span data-ttu-id="65193-102">Details</span><span class="sxs-lookup"><span data-stu-id="65193-102">Details</span></span>|<span data-ttu-id="65193-103">Ab .NET Framework 4.5 wird als Sortieralgorithmus von <xref:System.Collections.Generic.List%601?displayProperty=name> nicht mehr Quicksort, sondern Introsort verwendet.</span><span class="sxs-lookup"><span data-stu-id="65193-103">Beginning in .NET Framework 4.5, <xref:System.Collections.Generic.List%601?displayProperty=name>'s sort algorithm has changed (to be an introspective sort instead of a quick sort).</span></span> <span data-ttu-id="65193-104">Der Sortieralgorithmus von <xref:System.Collections.Generic.List%601?displayProperty=name> war noch nie stabil. Nun treten jedoch möglicherweise bei Sortiervorgängen in anderen Szenarios Instabilitäten auf.</span><span class="sxs-lookup"><span data-stu-id="65193-104"><xref:System.Collections.Generic.List%601?displayProperty=name>'s sort has never been stable, but this change may cause different scenarios to sort in unstable ways.</span></span> <span data-ttu-id="65193-105">Das bedeutet, dass gleichwertige Elemente bei aufeinanderfolgenden Aufrufen der API in verschiedenen Reihenfolgen sortiert werden.</span><span class="sxs-lookup"><span data-stu-id="65193-105">That simply means that equivalent items may sort in different orders in subsequent calls of the API.</span></span>|
|<span data-ttu-id="65193-106">Vorschlag</span><span class="sxs-lookup"><span data-stu-id="65193-106">Suggestion</span></span>|<span data-ttu-id="65193-107">Da der alte Sortieralgorithmus ebenfalls instabil war (wenn auch in anderer Hinsicht), sollte kein Code vorhanden sein, in dem gleichwertige Element immer in einer bestimmten Reihenfolge sortiert werden müssen.</span><span class="sxs-lookup"><span data-stu-id="65193-107">Because the old sort algorithm was also unstable (though in slightly different ways), there should be no code that depends on equivalent items always sorting in a particular order.</span></span> <span data-ttu-id="65193-108">Wenn andere Codeinstanzen auf dieses Verhalten oder das alte Verhalten angewiesen sind, sollte dieser Code durch die Einführung einer Vergleichsfunktion aktualisiert werden, die die Elemente deterministisch in der gewünschten Reihenfolge sortiert.</span><span class="sxs-lookup"><span data-stu-id="65193-108">If there are instances of code depending upon that and being lucky with the old behavior, that code should be updated to use a comparer that will deterministically sort the items in the desired order.</span></span>|
|<span data-ttu-id="65193-109">Bereich</span><span class="sxs-lookup"><span data-stu-id="65193-109">Scope</span></span>|<span data-ttu-id="65193-110">Transparent</span><span class="sxs-lookup"><span data-stu-id="65193-110">Transparent</span></span>|
|<span data-ttu-id="65193-111">Version</span><span class="sxs-lookup"><span data-stu-id="65193-111">Version</span></span>|<span data-ttu-id="65193-112">4.5</span><span class="sxs-lookup"><span data-stu-id="65193-112">4.5</span></span>|
|<span data-ttu-id="65193-113">Typ</span><span class="sxs-lookup"><span data-stu-id="65193-113">Type</span></span>|<span data-ttu-id="65193-114">Laufzeit</span><span class="sxs-lookup"><span data-stu-id="65193-114">Runtime</span></span>|
|<span data-ttu-id="65193-115">Betroffene APIs</span><span class="sxs-lookup"><span data-stu-id="65193-115">Affected APIs</span></span>|<ul><li><xref:System.Collections.Generic.List%601.Sort?displayProperty=nameWithType></li><li><xref:System.Collections.Generic.List%601.Sort(System.Collections.Generic.IComparer{%600})?displayProperty=nameWithType></li><li><xref:System.Collections.Generic.List%601.Sort(System.Comparison{%600})?displayProperty=nameWithType></li><li><xref:System.Collections.Generic.List%601.Sort(System.Int32,System.Int32,System.Collections.Generic.IComparer{%600})?displayProperty=nameWithType></li></ul>|
