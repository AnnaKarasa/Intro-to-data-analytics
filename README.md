# Intro-to-data-analytics
In this project, I was introduced to SQL and databases. The tasks were to create queries, that overviewed company's products and order history. 

Google Sheet with the results: https://docs.google.com/spreadsheets/d/1dot7FRHPTGRlDdt5FNCqLwreAY_ODQsg/edit?gid=1328200808#gid=1328200808 
SQL code:

1.1

SELECT

 product.ProductID AS ProductID,

 product.Name AS Name,

 product.ProductNumber AS ProductNumber,

 product.size AS Size,

 product.color AS Color,

 product.ProductSubcategoryID AS ProductSubcategoryID,

 productSubcategory.Name AS SubcategoryName

FROM

 `adwentureworks_db.product` AS Product

JOIN

 `adwentureworks_db.productsubcategory` AS productSubcategory

ON

Product.ProductSubcategoryID= productSubcategory.ProductSubcategoryID 

ORDER BY

 SubcategoryName




1.2

SELECT

 product.ProductID AS ProductID,

 product.Name AS Name,

 product.ProductNumber AS ProductNumber,

 product.size AS Size,

 product.color AS Color,

 product.ProductSubcategoryID AS ProductSubcategoryID,

 productSubcategory.Name AS SubcategoryName,

 productCategory.Name AS Category

FROM

 `adwentureworks_db.product` AS Product

JOIN

 `adwentureworks_db.productsubcategory` AS productSubcategory

ON

Product.ProductSubcategoryID= productSubcategory.ProductSubcategoryID

JOIN

`adwentureworks_db.productcategory` AS productCategory

ON

Product.ProductSubcategoryID= productCategory.ProductCategoryID

ORDER BY

Category




1.3

SELECT

 product.ProductID AS ProductID,

 product.Name AS Name,

 product.ProductNumber AS ProductNumber,

 product.size AS Size,

 product.color AS Color,

 product.ProductSubcategoryID AS ProductSubcategoryID,

 productSubcategory.Name AS SubcategoryName,

 productCategory.Name AS Category,

 product.ListPrice AS Product_Price,

 product.SellEndDate AS LastSale

FROM

 `adwentureworks_db.product` AS product

JOIN

 `adwentureworks_db.productsubcategory` AS productSubcategory

ON

 product.ProductSubcategoryID = productSubcategory.ProductSubcategoryID

JOIN

 `adwentureworks_db.productcategory` AS productCategory

ON

 productSubcategory.ProductCategoryID = productCategory.ProductCategoryID

WHERE

 product.ListPrice > 2000

 AND product.SellEndDate IS NULL

 AND productCategory.Name = 'Bike'

ORDER BY

 product.ListPrice DESC;




2.1

SELECT

 DISTINCT LocationID,

 COUNT (DISTINCT WorkOrderID) AS UniqueWorkOrders,

 COUNT (DISTINCT ProductID) AS UniqueProducts,

 SUM (ActualCost) AS TotalActualCost

FROM `adwentureworks_db.workorderrouting`

WHERE DATE (ActualStartDate) BETWEEN "2004-01-01" AND "2004-01-31"

GROUP BY LocationID




2.2.

SELECT

 wr.LocationID,

 l.Name AS LocationName,

 COUNT(DISTINCT wr.WorkOrderID) AS UniqueWorkOrders,

 COUNT(DISTINCT wr.ProductID) AS UniqueProducts,

 SUM(wr.ActualCost) AS TotalActualCost,

 AVG(DATE_DIFF(wr.ActualStartDate, wr.ActualEndDate, DAY)) AS AvgDays

FROM `adwentureworks_db.workorderrouting` wr

JOIN `adwentureworks_db.location` l ON wr.LocationID = l.LocationID

WHERE DATE(wr.ActualStartDate) BETWEEN "2004-01-01" AND "2004-01-31"

GROUP BY wr.LocationID, l.Name;




2.3.

SELECT 

 WorkOrderID, 

 SUM(ActualCost) AS TotalCost

FROM `adwentureworks_db.workorderrouting`

WHERE DATE(ActualStartDate) BETWEEN '2004-01-01' AND '2004-01-31'

GROUP BY WorkOrderID

HAVING SUM(ActualCost) > 300;




3.1.

SELECT

 sales_detail.SalesOrderId,

 sales_detail.OrderQty,

 sales_detail.UnitPrice,

 sales_detail.LineTotal,

 sales_detail.ProductId,

 sales_detail.SpecialOfferID,

 spec_offer_product.ModifiedDate AS ProductModifiedDate,

 spec_offer.Category AS SpecialOfferCategory,

 spec_offer.Description AS SpecialOfferDescription

FROM `tc-da-1.adwentureworks_db.salesorderdetail` AS sales_detail

LEFT JOIN `tc-da-1.adwentureworks_db.specialofferproduct` AS spec_offer_product

ON sales_detail.productId = spec_offer_product.ProductID

LEFT JOIN `tc-da-1.adwentureworks_db.specialoffer` AS spec_offer

ON sales_detail.SpecialOfferID = spec_offer.SpecialOfferID

ORDER BY LineTotal DESC;




3.2.

SELECT

 a.VendorId AS Id,

 vendorContact.ContactId,

 vendorContact.ContactTypeId,

 a.Name,

 a.CreditRating,

 a.ActiveFlag,

 c.AddressId,

 address.City

FROM

 tc-da-1.adwentureworks_db.vendor AS a

LEFT JOIN

 tc-da-1.adwentureworks_db.vendorcontact AS vendorContact

ON

 a.VendorId = vendorContact.VendorId

LEFT JOIN

 tc-da-1.adwentureworks_db.vendoraddress AS c

ON

 a.VendorId = c.VendorId

LEFT JOIN

 tc-da-1.adwentureworks_db.address AS address

ON

 c.AddressId = address.AddressId;

