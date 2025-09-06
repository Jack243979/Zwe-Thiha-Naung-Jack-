# Calculated Fields (Tableau syntax)

## Sales & Sorting
**Sales**

[quantity] * [list_price] * (1 - [discount])

**Clean Sales** (exclude null/zero for sorting & Top/Bottom)

IF SUM([Sales]) > 0 THEN SUM([Sales]) ELSE NULL END\

## Customer Loyalty
**Order Count per Customer** (LOD)

{ FIXED [customer_id] : COUNTD([order_id]) }

**Customer Type**

IF [Order Count per Customer] = 1 THEN 'One-time Buyer'
ELSE 'Repeat Customer' END


## Best Seller Highlight
**Max Sales by Product** (LOD)

{ FIXED [product_id] : SUM([Sales]) } 

**Global Max Sales** (LOD)

{ FIXED : MAX( { FIXED [product_id] : SUM([Sales]) } ) }

**Best Seller Name (Flag)**

IF { FIXED [product_id] : SUM([Sales]) } = [Global Max Sales]
THEN ATTR([product_name]) END

## No-Sale vs Has-Sale

IF ISNULL(SUM([Sales])) OR SUM([Sales]) = 0 THEN 'No Sales' ELSE 'Has Sales' END

## Top-N Customers (Parameter + Filter)
- **Parameter**: `pTopN` (Integer)
- **Field: Rank by Sales**

RANK_DENSE( SUM([Sales]) , 'desc' )

- **Field: Keep Top-N**

- [RANK by Sales] <= [pTopN]

## Year / Date helpers
**Order Year**

YEAR([order_date])

## Region bucketing (example US)

CASE [state]
WHEN 'CA' THEN 'West'
WHEN 'OR' THEN 'West'
WHEN 'WA' THEN 'West'
WHEN 'TX' THEN 'South'
WHEN 'NY' THEN 'Northeast'
ELSE 'Other'
END


