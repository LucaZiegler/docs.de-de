### <a name="objectcontexttranslate-and-objectcontextexecutestorequery-now-support-enum-type"></a><span data-ttu-id="d4016-101">ObjectContext.Translate und ObjectContext.ExecuteStoreQuery unterstützen jetzt den Enumerationstyp</span><span class="sxs-lookup"><span data-stu-id="d4016-101">ObjectContext.Translate and ObjectContext.ExecuteStoreQuery now support enum type</span></span>

|   |   |
|---|---|
|<span data-ttu-id="d4016-102">Details</span><span class="sxs-lookup"><span data-stu-id="d4016-102">Details</span></span>|<span data-ttu-id="d4016-103">In .NET 4.0 konnte der generische Parameter <code>T</code> von <code>ObjectContext.Translate</code>- und <code>ObjectContext.ExecuteStoreQuery</code>-Methoden kein Enumerationstyp sein.</span><span class="sxs-lookup"><span data-stu-id="d4016-103">In .NET 4.0, the generic parameter <code>T</code> of <code>ObjectContext.Translate</code> and <code>ObjectContext.ExecuteStoreQuery</code> methods could not be an enum.</span></span> <span data-ttu-id="d4016-104">Dieses Szenario wird jetzt unterstützt.</span><span class="sxs-lookup"><span data-stu-id="d4016-104">That scenario is now supported.</span></span>|
|<span data-ttu-id="d4016-105">Vorschlag</span><span class="sxs-lookup"><span data-stu-id="d4016-105">Suggestion</span></span>|<span data-ttu-id="d4016-106">Wenn für einen Enumerationstyp in .NET 4.0 „Translate“ oder „ExecuteStoreQuery“ aufgerufen wurde, wurde „0“ zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="d4016-106">If Translate or ExecuteStoreQuery was called on an enum type in .NET 4.0, '0' was returned.</span></span> <span data-ttu-id="d4016-107">Wenn dieses Verhalten erwünscht war, sollten die Aufrufe durch eine konstante 0 (oder das entsprechende Enum-Äquivalent) ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="d4016-107">If that behavior was desirable, the calls should be replaced with a constant 0 (or the enum equivalent of it).</span></span>|
|<span data-ttu-id="d4016-108">Bereich</span><span class="sxs-lookup"><span data-stu-id="d4016-108">Scope</span></span>|<span data-ttu-id="d4016-109">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="d4016-109">Edge</span></span>|
|<span data-ttu-id="d4016-110">Version</span><span class="sxs-lookup"><span data-stu-id="d4016-110">Version</span></span>|<span data-ttu-id="d4016-111">4.5</span><span class="sxs-lookup"><span data-stu-id="d4016-111">4.5</span></span>|
|<span data-ttu-id="d4016-112">Typ</span><span class="sxs-lookup"><span data-stu-id="d4016-112">Type</span></span>|<span data-ttu-id="d4016-113">Laufzeit</span><span class="sxs-lookup"><span data-stu-id="d4016-113">Runtime</span></span>|
|<span data-ttu-id="d4016-114">Betroffene APIs</span><span class="sxs-lookup"><span data-stu-id="d4016-114">Affected APIs</span></span>|<ul><li><xref:System.Data.Objects.ObjectContext.Translate%60%601(System.Data.Common.DbDataReader)?displayProperty=nameWithType></li><li><xref:System.Data.Objects.ObjectContext.Translate%60%601(System.Data.Common.DbDataReader,System.String,System.Data.Objects.MergeOption)?displayProperty=nameWithType></li><li><xref:System.Data.Objects.ObjectContext.ExecuteStoreQuery%60%601(System.String,System.Object[])?displayProperty=nameWithType></li><li><xref:System.Data.Objects.ObjectContext.ExecuteStoreQuery%60%601(System.String,System.String,System.Data.Objects.MergeOption,System.Object[])?displayProperty=nameWithType></li></ul>|
