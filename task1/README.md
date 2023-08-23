# Week 1


➜  SAPAPIDevChallenge2023 git:(main) ✗ curl \         
  --silent \
  --url "https://services.odata.org/V4/Northwind/Northwind.svc/" \
  | jq '.value|=.[:5]'


➜  SAPAPIDevChallenge2023 git:(main) ✗ curl \
  --silent \
  --url "https://services.odata.org/V4/Northwind/Northwind.svc/" \
  | jq '.value[].name'           
"Categories"
"CustomerDemographics"
"Customers"
"Employees"
"Order_Details"
"Orders"
"Products"
"Regions"
"Shippers"
"Suppliers"
"Territories"
"Alphabetical_list_of_products"
"Category_Sales_for_1997"
"Current_Product_Lists"
"Customer_and_Suppliers_by_Cities"
"Invoices"
"Order_Details_Extendeds"
"Order_Subtotals"
"Orders_Qries"
"Product_Sales_for_1997"
"Products_Above_Average_Prices"
"Products_by_Categories"
"Sales_by_Categories"
"Sales_Totals_by_Amounts"
"Summary_of_Sales_by_Quarters"
"Summary_of_Sales_by_Years"
➜  SAPAPIDevChallenge2023 git:(main) ✗ 


➜  SAPAPIDevChallenge2023 git:(main) ✗ curl \
  --silent \
  --url "https://services.odata.org/V4/Northwind/Northwind.svc/" \
  | jq '.value|.[].name'
"Categories"
"CustomerDemographics"
"Customers"
"Employees"
"Order_Details"
"Orders"
"Products"
"Regions"
"Shippers"
"Suppliers"
"Territories"
"Alphabetical_list_of_products"
"Category_Sales_for_1997"
"Current_Product_Lists"
"Customer_and_Suppliers_by_Cities"
"Invoices"
"Order_Details_Extendeds"
"Order_Subtotals"
"Orders_Qries"
"Product_Sales_for_1997"
"Products_Above_Average_Prices"
"Products_by_Categories"
"Sales_by_Categories"
"Sales_Totals_by_Amounts"
"Summary_of_Sales_by_Quarters"
"Summary_of_Sales_by_Years"
➜  SAPAPIDevChallenge2023 git:(main) ✗ 


➜  SAPAPIDevChallenge2023 git:(main) ✗ curl \
  --silent \
  --url "https://services.odata.org/V4/Northwind/Northwind.svc/" \
  | jq '.value|.[].name' | sed 's/\"//g' | tr '\n' ','
Categories,CustomerDemographics,Customers,Employees,Order_Details,Orders,Products,Regions,Shippers,Suppliers,Territories,Alphabetical_list_of_products,Category_Sales_for_1997,Current_Product_Lists,Customer_and_Suppliers_by_Cities,Invoices,Order_Details_Extendeds,Order_Subtotals,Orders_Qries,Product_Sales_for_1997,Products_Above_Average_Prices,Products_by_Categories,Sales_by_Categories,Sales_Totals_by_Amounts,Summary_of_Sales_by_Quarters,Summary_of_Sales_by_Years,%
➜  SAPAPIDevChallenge2023 git:(main) ✗    


➜  SAPAPIDevChallenge2023 git:(main) ✗ curl \
  --silent \
  --url "https://services.odata.org/V4/Northwind/Northwind.svc/" \
  | jq '.value|.[].name' | sed 's/\"//g' | tr '\n' ','| sed 's/.$//'
Categories,CustomerDemographics,Customers,Employees,Order_Details,Orders,Products,Regions,Shippers,Suppliers,Territories,Alphabetical_list_of_products,Category_Sales_for_1997,Current_Product_Lists,Customer_and_Suppliers_by_Cities,Invoices,Order_Details_Extendeds,Order_Subtotals,Orders_Qries,Product_Sales_for_1997,Products_Above_Average_Prices,Products_by_Categories,Sales_by_Categories,Sales_Totals_by_Amounts,Summary_of_Sales_by_Quarters,Summary_of_Sales_by_Years%
➜  SAPAPIDevChallenge2023 git:(main) ✗ 

Categories,CustomerDemographics,Customers,Employees,Order_Details,Orders,Products,Regions,Shippers,Suppliers,Territories,Alphabetical_list_of_products,Category_Sales_for_1997,Current_Product_Lists,Customer_and_Suppliers_by_Cities,Invoices,Order_Details_Extendeds,Order_Subtotals,Orders_Qries,Product_Sales_for_1997,Products_Above_Average_Prices,Products_by_Categories,Sales_by_Categories,Sales_Totals_by_Amounts,Summary_of_Sales_by_Quarters,Summary_of_Sales_by_Years

SAPAPIDevChallenge2023 git:(main) ✗ curl \
  --include \
  --header "CommunityID: johnastill" \
  --url "https://developer-challenge.cfapps.eu10.hana.ondemand.com/v1/hash(value='Categories,CustomerDemographics,Customers,Employees,Order_Details,Orders,Products,Regions,Shippers,Suppliers,Territories,Alphabetical_list_of_products,Category_Sales_for_1997,Current_Product_Lists,Customer_and_Suppliers_by_Cities,Invoices,Order_Details_Extendeds,Order_Subtotals,Orders_Qries,Product_Sales_for_1997,Products_Above_Average_Prices,Products_by_Categories,Sales_by_Categories,Sales_Totals_by_Amounts,Summary_of_Sales_by_Quarters,Summary_of_Sales_by_Years')"