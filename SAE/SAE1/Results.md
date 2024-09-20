# SAÉ NoSQL - Résultat des requêtes

###  Requêtes SQL

1. Lister les clients n’ayant jamais effecuté une commande ;

| customerNumber | customerName                   |
|----------------|--------------------------------|
| 125            | Havel & Zbyszek Co             |
| 168            | American Souvenirs Inc         |
| 169            | Porto Imports Co.              |
| 206            | Asian Shopping Network, Co     |
| 223            | Natürlich Autos                |
| 237            | ANG Resellers                  |
| 247            | Messner Shopping Network       |
| 273            | Franken Gifts, Co              |
| 293            | BG&E Collectables              |
| 303            | Schuyler Imports               |
| 307            | Der Hund Imports               |
| 335            | Cramer Spezialitäten, Ltd      |
| 348            | Asian Treasures, Inc.          |
| 356            | SAR Distributors, Co           |
| 361            | Kommission Auto                |
| 369            | Lisboa Souveniers, Inc         |
| 376            | Precious Collectables          |
| 409            | Stuttgart Collectable Exchange |
| 443            | Feuer Online Stores, Inc       |
| 459            | Warburg Exchange               |
| 465            | Anton Designs, Ltd.            |
| 477            | Mit Vergnügen & Co.            |
| 480            | Kremlin Collectables, Co.      |
| 481            | Raanan Stores, Inc             |

2. Pour chaque employé, le nombre de clients, le nombre de commandes et le montant total de celles-ci ;

| employeeNumber | firstName | lastName  | numberOfCustomers | numberOfOrders | totalOrderAmount |
|----------------|-----------|-----------|-------------------|----------------|------------------|
| 1002           | Diane     | Murphy    | 0                 | 0              | NaN              |
| 1056           | Mary      | Patterson | 0                 | 0              | NaN              |
| 1076           | Jeff      | Firrelli  | 0                 | 0              | NaN              |
| 1088           | William   | Patterson | 0                 | 0              | NaN              |
| 1102           | Gerard    | Bondur    | 0                 | 0              | NaN              |
| 1143           | Anthony   | Bow       | 0                 | 0              | NaN              |
| 1165           | Leslie    | Jennings  | 6                 | 34             | 12674066.13      |
| 1166           | Leslie    | Thompson  | 6                 | 14             | 943442.48        |
| 1188           | Julie     | Firrelli  | 6                 | 14             | 1035043.99       |
| 1216           | Steve     | Patterson | 6                 | 18             | 1545990.08       |
| 1286           | Foon Yue  | Tseng     | 7                 | 17             | 1635226.60       |
| 1323           | George    | Vanauf    | 8                 | 22             | 1870933.55       |
| 1337           | Loui      | Bondur    | 6                 | 20             | 2093279.51       |
| 1370           | Gerard    | Hernandez | 7                 | 43             | 21850743.39      |
| 1401           | Pamela    | Castillo  | 10                | 31             | 2580550.55       |
| 1501           | Larry     | Bott      | 8                 | 22             | 2188718.80       |
| 1504           | Barry     | Jones     | 9                 | 25             | 2357369.87       |
| 1611           | Andy      | Fixter    | 5                 | 19             | 2352253.84       |
| 1612           | Peter     | Marsh     | 5                 | 19             | 2119701.72       |
| 1619           | Tom       | King      | 0                 | 0              | NaN              |
| 1621           | Mami      | Nishi     | 5                 | 16             | 1815463.17       |
| 1625           | Yoshimi   | Kato      | 0                 | 0              | NaN              |
| 1702           | Martin    | Gerard    | 6                 | 12             | 1014439.14       |
|                |           |           |                   |                |                  |

3. Idem pour chaque bureau (nombre de clients, nombre de commandes et montant total), avec en plus le nombre de clients d’un pays différent, s’il y en a ;

| officeCode | city          | officeCountry | numberOfCustomers | numberOfOrders | totalOrderAmount | customersFromDifferentCountry |
|------------|---------------|---------------|-------------------|----------------|------------------|-------------------------------|
| 1.0        | San Francisco | USA           | 12                | 48             | 13617508.61      | 0                             |
| 2.0        | Boston        | USA           | 12                | 32             | 2581034.07       | 0                             |
| 3.0        | NYC           | USA           | 15                | 39             | 3506160.15       | 3                             |
| 4.0        | Paris         | France        | 29                | 106            | 27539012.59      | 17                            |
| 5.0        | Tokyo         | Japan         | 5                 | 16             | 1815463.17       | 3                             |
| 6.0        | Sydney        | Australia     | 10                | 38             | 4471955.56       | 5                             |
| 7.0        | London        | UK            | 17                | 47             | 4546088.67       | 12                            |

4. Pour chaque produit, donner le nombre de commandes, la quantité totale commandée, et le nombre de clients différents (110 lignes);

| productCode | productName                           | numberOfOrders | totalQuantityOrdered | numberOfDistinctCustomers |
|-------------|---------------------------------------|----------------|----------------------|---------------------------|
| S10_1678    | 1969 Harley Davidson Ultimate Chopper | 28             | 1026.0               | 26                        |
| S10_1949    | 1952 Alpine Renault 1300              | 28             | 961.0                | 27                        |
| S10_2016    | 1996 Moto Guzzi 1100i                 | 28             | 999.0                | 26                        |
| S10_4698    | 2003 Harley-Davidson Eagle Drag Bike  | 28             | 985.0                | 25                        |
| S10_4757    | 1972 Alfa Romeo GTA                   | 28             | 1000.0               | 27                        |
| ...         | ...                                   | ...            | ...                  | ...                       |
| S700_3505   | The Titanic                           | 27             | 952.0                | 22                        |
| S700_3962   | The Queen Mary                        | 27             | 883.0                | 24                        |
| S700_4002   | American Airlines: MD-11S             | 28             | 1073.0               | 26                        |
| S72_1253    | Boeing X-32A JSF                      | 28             | 960.0                | 27                        |
| S72_3212    | Pont Yacht                            | 27             | 958.0                | 24                        |

5. Donner le nombre de commande pour chaque pays, ainsi que le montant total des commandes et le montant total payé : on veut conserver les clients n’ayant jamais commandé dans le résultat final ;

| country      | numberOfOrders | totalOrderAmount | totalPaidAmount |
|--------------|----------------|------------------|-----------------|
| Australia    | 19             | 2182269.38       | 2.482541e+07    |
| Austria      | 7              | 606187.59        | 4.090982e+06    |
| Belgium      | 7              | 283705.44        | 1.931535e+06    |
| Canada       | 7              | 448157.12        | 4.487022e+06    |
| Denmark      | 7              | 781357.50        | 7.001114e+06    |
| Finland      | 9              | 988745.73        | 1.009620e+07    |
| France       | 37             | 3160296.75       | 3.141444e+07    |
| Germany      | 7              | 576293.44        | 4.971661e+06    |
| Hong Kong    | 2              | 48784.36         | 7.805498e+05    |
| Ireland      | 2              | 115512.86        | 9.241029e+05    |
| Israel       | 0              | NaN              | NaN             |
| Italy        | 10             | 945208.16        | 1.324310e+07    |
| Japan        | 6              | 496898.36        | 4.837611e+06    |
| Netherlands  | 0              | NaN              | NaN             |
| New Zealand  | 15             | 1736137.04       | 1.710337e+07    |
| Norway       | 9              | 848125.78        | 8.870124e+06    |
| Philippines  | 3              | 282047.19        | 2.444409e+06    |
| Poland       | 0              | NaN              | NaN             |
| Portugal     | 0              | NaN              | NaN             |
| Russia       | 0              | NaN              | NaN             |
| Singapore    | 9              | 1038454.91       | 1.150336e+07    |
| South Africa | 0              | NaN              | NaN             |
| Spain        | 36             | 12665636.19      | 2.123241e+08    |
| Sweden       | 7              | 554287.75        | 6.541197e+06    |
| Switzerland  | 2              | 235427.12        | 3.649120e+06    |
| UK           | 13             | 1204373.23       | 1.506256e+07    |
| USA          | 112            | 14228729.12      | 1.957451e+08    |

6. On veut la table de contigence du nombre de commande entre la ligne de produits et le pays du client (127 lignes) ;

| productLine  | country   | numberOfOrders |
|--------------|-----------|----------------|
| Classic Cars | None      | 0              |
| Classic Cars | Australia | 12             |
| Classic Cars | Austria   | 5              |
| Classic Cars | Belgium   | 2              |
| Classic Cars | Canada    | 6              |
| ...          | ...       | ...            |
| Vintage Cars | Singapore | 4              |
| Vintage Cars | Spain     | 22             |
| Vintage Cars | Sweden    | 4              |
| Vintage Cars | UK        | 10             |
| Vintage Cars | USA       | 67             |

7. On veut la même table croisant la ligne de produits et le pays du client, mais avec le montant total payé dans chaque cellule ;

| productLine  | country   | totalPaidAmount |
|--------------|-----------|-----------------|
| Classic Cars | None      | NaN             |
| Classic Cars | Australia | 7504795.97      |
| Classic Cars | Austria   | 1884419.42      |
| Classic Cars | Belgium   | 166880.87       |
| Classic Cars | Canada    | 774924.01       |
| ...          | ...       | ...             |
| Vintage Cars | Singapore | 1941227.28      |
| Vintage Cars | Spain     | 39878490.66     |
| Vintage Cars | Sweden    | 1377094.16      |
| Vintage Cars | UK        | 4673162.78      |
| Vintage Cars | USA       | 47090713.86     |

8. Donner les 10 produits pour lesquels la marge moyenne est la plus importante (79 lignes) ;
| productCode | productName                          | averageMargin |
|-------------|--------------------------------------|---------------|
| S10_1949    | 1952 Alpine Renault 1300             | 99.006429     |
| S10_4698    | 2003 Harley-Davidson Eagle Drag Bike | 95.235000     |
| S18_3232    | 1992 Ferrari 360 Spider red          | 83.334906     |
| S12_2823    | 2002 Suzuki XREO                     | 83.201429     |
| S18_2795    | 1928 Mercedes-Benz SSK               | 82.696786     |
| S12_1108    | 2001 Ferrari Enzo                    | 81.043704     |
| S12_3891    | 1969 Ford Falcon                     | 77.335926     |
| S18_3685    | 1948 Porsche Type 356 Roadster       | 72.636800     |
| S18_2870    | 1999 Indy 500 Monte Carlo SS         | 71.794400     |
| S18_1749    | 1917 Grand Touring Sedan             | 70.432800     |

9. Lister les produits (avec le nom et le code du client) qui ont été vendus à perte :
    - Si un produit a été dans cette situation plusieurs fois, il doit apparaître plusieurs fois,
    - Une vente à perte arrive quand le prix de vente est inférieur au prix d’achat ;


| productCode | productName                         | customerName                 | customerNumber | priceEach | buyPrice |
|-------------|-------------------------------------|------------------------------|----------------|-----------|----------|
| S10_4962    | 1962 LanciaA Delta 16V              | Online Diecast Creations Co. | 363            | 61.99     | 103.42   |
| S18_2957    | 1934 Ford V8 Coupe                  | Online Diecast Creations Co. | 363            | 29.87     | 34.35    |
| S18_3136    | 18th Century Vintage Horse Carriage | Online Diecast Creations Co. | 363            | 47.04     | 60.74    |
| S12_3148    | 1969 Corvair Monza                  | Vitachrome Inc.              | 181            | 54.33     | 89.14    |
| S18_2319    | 1964 Mercedec Tour Bus              | Vitachrome Inc.              | 181            | 37.48     | 74.86    |
| ...         | ...                                 | ...                          | ...            | ...       | ...      |
| S10_4962    | 1962 LanciaA Delta 16V              | Anna's Decorations, Ltd      | 276            | 46.90     | 103.42   |
| S12_1666    | 1958 Setra Bus                      | Anna's Decorations, Ltd      | 276            | 63.20     | 77.90    |
| S18_2949    | 1913 Ford Model T Speedster         | Anna's Decorations, Ltd      | 276            | 45.25     | 60.78    |
| S18_2238    | 1998 Chrysler Plymouth Prowler      | Down Under Souveniers, Inc   | 323            | 69.81     | 101.51   |
| S12_1108    | 2001 Ferrari Enzo                   | Lyon Souveniers              | 250            | 69.12     | 95.59    |
